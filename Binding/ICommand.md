# ICommandの実装

- ICommandはButtonコントロール、ContextMenuのBinding先として実装する
- ICommandの実装例は下記のとおり
```
using System;
using System.Windows.Input;

namespace Common.relaycommand.src {
	/// <summary>
	/// ICommandの実装
	/// </summary>
	public class RelayCommand : ICommand {

		/// <summary>
		/// コマンドの実体
		/// </summary>
		readonly Action _execute;

		/// <summary>
		/// コマンドの実行可能判別処理の実体
		/// </summary>
		readonly Func<bool> _canExecute;


		/// <summary>
		/// コンストラクタ
		/// </summary>
		/// <param name="execute">コマンドの実体</param>
		public RelayCommand( Action execute ) : this( execute, null ) { }


		/// <summary>
		/// コンストラクタ
		/// </summary>
		/// <param name="execute">コマンドの実態</param>
		/// <param name="canExecute">コマンドの実行可能判別処理の実体</param>
		/// <exception cref="ArgumentNullException"/>
		public RelayCommand( Action execute, Func<bool> canExecute ) {
			if( execute == null ) {
				throw new ArgumentNullException( "execute" );
			}
			this._execute = execute;
			this._canExecute = canExecute;
		}


		/// <summary>
		/// ICommandのCanExecuteの実装です
		/// 現在の状態でこのコマンドを実行できるかどうかを判断するメソッドを定義します
		/// </summary>
		/// <param name="parameter">コマンドで使用されたデータ、必要がない場合は null に設定できます</param>
		/// <returns>このコマンドを実行できる場合は true／それ以外の場合は false</returns>
		public bool CanExecute( Object parameter ) {
			return _canExecute == null || _canExecute();
		}


		/// <summary>
		/// ICommandのCanExecuteChangedイベントハンドラの実装です
		/// コマンドを実行するかどうかに影響するような変更があった場合に発生します
		/// </summary>
		public event EventHandler CanExecuteChanged {
			add {
				CommandManager.RequerySuggested += value;
			}
			remove {
				CommandManager.RequerySuggested += value;
			}
		}


		/// <summary>
		/// CanExecuteChanged イベントを発行します
		/// 同じView（ViewModel）のすべてのコマンドに対して再評価がおこなわれるため
		/// 各コマンドに対して呼ぶ必要はありません
		/// </summary>
		public static void RaiseCanExecuteChanged() {
			CommandManager.InvalidateRequerySuggested();
		}


		/// <summary>
		/// ICommandのExecuteの実装です
		/// コマンドの起動時に呼び出されるメソッドを定義します
		/// </summary>
		/// <param name="parameter">コマンドで使用されたデータ、必要がない場合は null に設定できます</param>
		public void Execute( Object parameter ) {
			_execute();
		}


	}


	/// <summary>
	/// ICommandの実装（ジェネリクス対応版）
	/// </summary>
	/// <typeparam name="T"></typeparam>
	public class RelayCommand<T> : ICommand {

		/// <summary>
		/// コマンドの実体
		/// </summary>
		readonly Action<T> _execute;

		/// <summary>
		/// コマンドの実行可能判別処理の実体
		/// </summary>
		readonly Predicate<T> _canExecute;


		/// <summary>
		/// コンストラクタ
		/// </summary>
		/// <param name="execute">コマンドの実体</param>
		public RelayCommand( Action<T> execute ) : this( execute, null ) { }


		/// <summary>
		/// コンストラクタ
		/// </summary>
		/// <param name="execute">コマンドの実体</param>
		/// <param name="canExecute">コマンドの実行可能判別処理の実体</param>
		public RelayCommand( Action<T> execute, Predicate<T> canExecute ) {
			if( execute == null ) {
				throw new ArgumentNullException( "execute" );
			}
			this._execute = execute;
			this._canExecute = canExecute;
		}


		/// <summary>
		/// ICommandのCanExecuteの実装です
		/// 現在の状態でこのコマンドを実行できるかどうかを判断するメソッドを定義します
		/// </summary>
		/// <param name="parameter">コマンドで使用されたデータ、必要がない場合は null に設定できます</param>
		/// <returns>このコマンドを実行できる場合は true／それ以外の場合は false</returns>
		public bool CanExecute( Object parameter ) {
			return this._canExecute == null || this._canExecute( ( T ) parameter );
		}


		/// <summary>
		/// ICommandのCanExecuteChangedイベントハンドラの実装です
		/// コマンドを実行するかどうかに影響するような変更があった場合に発生します
		/// </summary>
		public event EventHandler CanExecuteChanged {
			add {
				CommandManager.RequerySuggested += value;
			}
			remove {
				CommandManager.RequerySuggested += value;
			}
		}


		/// <summary>
		/// CanExecuteChanged イベントを発行します
		/// 同じView（ViewModel）のすべてのコマンドに対して再評価がおこなわれるため
		/// 各コマンドに対して呼ぶ必要はありません
		/// </summary>
		public static void RaiseCanExecuteChanged() {
			CommandManager.InvalidateRequerySuggested();
		}


		/// <summary>
		/// ICommandのExecuteの実装です
		/// コマンドの起動時に呼び出されるメソッドを定義します
		/// </summary>
		/// <param name="parameter">コマンドで使用されたデータ、必要がない場合は null に設定できます</param>
		public void Execute( Object parameter ) {
			_execute( ( T ) parameter );
		}


	}
}
```

## ICommandの使用例

- Xaml
```
<ContextMenuService.ContextMenu>
    <ContextMenu Name="contextMenu">
        <MenuItem Name="AddMenu" Header="Add" Command="{Binding Path=AddCommand}"/>
    </ContextMenu>
</ContextMenuService.ContextMenu>
```

- Xaml.cs<br/>
コンストラクタの中等に実装して画面の要素をViewModelに渡す引数を登録する<br/>
ViewModelに引数を渡す必要がない場合は省略可
```
this.AddMenu.CommandParameter = this.dataGrid;
```

- ViewModel
```
public ICommand AddCommand => new RelayCommand<DataGrid>( this.AddProcess, this.IsAddExecutable );
private void AddProcess( DataGrid dataGrid )
{
    〜ここに処理を実装〜
}
private bool IsAddExecutable( DataGrid dataGrid )
{
    〜ここに処理の実行可否を返す処理を実装〜
    （falseを返した場合Buttonコントロール、ContextMenuは非活性として表示される）
}
```
