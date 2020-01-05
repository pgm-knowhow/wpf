# Xaml(ScrollViewer)の実装

```
<ScrollViewer VerticalScrollBarVisibility="Auto" HorizontalScrollBarVisibility="Auto">
    <Grid>
        〜
    </Grid>
</ScrollViewer>
```
ScrollViewerにはControlを一つしか入れられないので、Grid等を置いてその中にControlを追加する

## 応用：ControlのScrollViewerをコードビハインドから取得する
```
/// <summary>
/// 要素に含まれるスクロールビューアーを取得します（見つからない時はnullを返します）
/// </summary>
private ScrollViewer GetScrollViewer(FrameworkElement element)
{
    if (VisualTreeHelper.GetChildrenCount(element) == 0)
    {
        return null;
    }

    FrameworkElement child = VisualTreeHelper.GetChild(element, 0) as FrameworkElement;

    if (child == null)
    {
        return null;
    }
    if (child is ScrollViewer)
    {
        return (ScrollViewer)child;
    }

    return this.GetScrollViewer(child);
}
```

- 上の関数の使用例
```
ScrollViewer scroll = this.GetScrollViewer( this.DataGrid1 );
scroll.PageDown();
scroll.PageLeft();
scroll.PageRight();
scroll.PageUp();
scroll.ScrollToBottom();
scroll.ScrollToEnd();
scroll.ScrollToHome();
scroll.ScrollToHorizontalOffset( offset:1 );
scroll.ScrollToLeftEnd();
scroll.ScrollToRightEnd();
scroll.ScrollToTop();
scroll.ScrollToVerticalOffset( offset:1 );
```
