# Tips(ObservableCollection)

- ObservableCollectionに要素をAdd/DeleteするとINotifyPropertyChangedを使わなくても画面に反映される
- その代わりObservableCollectionはメインスレッド（UIスレッド）以外のスレッドから操作しようとすると例外になってしまう
- 以下のように実装することでメインスレッド以外のスレッド
からObservableCollectionを操作できる
```
Application.Current.Dispatcher.BeginInvoke(
    DispatcherPriority.Normal,
    new Action( () => {

        <ここでObservableCollectionを操作する>

    } )
);
```
 DispatcherPriorityには実行優先度によっていくつか選択肢がある
 [（よく使うのは Normal と BackGround）](https://docs.microsoft.com/dotnet/api/system.windows.threading.dispatcherpriority)
