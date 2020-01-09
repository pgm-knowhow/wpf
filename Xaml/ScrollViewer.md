[WPF開発ノウハウ集](../index.md)
# Xaml(ScrollViewer)の実装

```
<ScrollViewer VerticalScrollBarVisibility="Auto" HorizontalScrollBarVisibility="Auto">
    <Grid>
        〜
    </Grid>
</ScrollViewer>
```
ScrollViewerにはControlを一つしか入れられないので、Grid等を置いてその中にControlを追加する
