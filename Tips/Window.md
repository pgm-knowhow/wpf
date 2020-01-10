[WPF開発ノウハウ集](../index.md)
# Tips(Window)

前回表示座標で起動するように実装したアプリがマルチウインドウ環境で<br/>
サブディスプレイを切断した状態でアプリを起動した場合に、ウインドウがメインディスプレイの外で起動してしまい表示されない現象の対策<br/>

- メインウインドウの表示座標が無効なら x=0/y=0 に移動させる処理を追加
(以下の関数をWindow表示後に実行する）
```
private void AdjustWindowPosition() 
{
    bool isMainWindowVisible = false;

    foreach( System.Windows.Forms.Screen display in System.Windows.Forms.Screen.AllScreens ) 
    {
        if( display.WorkingArea.Contains( (int)this.Left, (int)this.Top ) ) 
        {
            isMainWindowVisible = true;
            break;
        }
    }

    if( !isMainWindowVisible ) 
    {
        this.Top = 0;
        this.Left = 0;
    }
}
```
