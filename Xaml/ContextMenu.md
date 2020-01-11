[WPF開発ノウハウ集](../index.md)
# Xaml(ContextMenu)の実装

- Xaml
コンテキストメニューを実装したい場所に以下のように追加

```
<ContextMenuService.ContextMenu>
    <ContextMenu>
        <MenuItem Name="AddMenu" Header="Add" Command="{Binding AddCommand"/>
    </ContextMenu>
</ContextMenuService.ContextMenu>
```
（Bindingについては [Binding(ICommand)の実装](../Binding/ICommand.md) の項を参照）

