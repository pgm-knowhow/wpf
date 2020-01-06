# Tips(Window)

前回表示座標で起動するように実装したアプリがマルチウインドウ環境で<br/>
サブディスプレイを切断した状態でアプリを起動した場合にウインドウが表示されない問題の対策として<br/>
メインウインドウの表示座標が無効なら x=0/y=0 に移動させる処理を追加する<br/>

下の関数をコンストラクタでWindow表示後に実行
```
private void AdjustWindowPosition() {
    bool isMainWindowVisible = false;

    foreach( System.Windows.Forms.Screen display in System.Windows.Forms.Screen.AllScreens ) {
        if( display.WorkingArea.Contains( (int)this.Left, (int)this.Top ) ) {
            isMainWindowVisible = true;
            break;
        }
    }

    if( !isMainWindowVisible ) {
        this.Top = 0;
        this.Left = 0;
    }
}
```
