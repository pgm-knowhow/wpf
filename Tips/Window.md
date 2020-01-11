# Tips(Window)

前回表示座標で起動するように実装したアプリが、マルチウインドウ環境で
サブディスプレイを切断した状態で起動した時に、メインディスプレイの表示領域外で起動してしまい操作できなくなる現象の対策<br/>

- メインウインドウの表示座標が無効なら x=0/y=0 に移動させる処理をWindow表示後に実行する<br/>

（以下は関数として実装した例）
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
