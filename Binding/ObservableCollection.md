# ObservableCollectionの更新

ObservableCollectionはメインスレッド（UIスレッド）以外から操作しようとすると例外になってしまう
その場合以下のように実装する
```
Application.Current.Dispatcher.BeginInvoke(
    DispatcherPriority.Normal,
    new Action( () => {

        <ここでObservableCollectionを操作する>

    } )
);
```
 DispatcherPriorityには実行優先度によっていくつか選択肢がある
 （よく見るのは Normal と BackGround）
