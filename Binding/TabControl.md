[WPF開発ノウハウ集](../index.md)
# Binding(TabControl)の実装

## Xaml
```
<TabControl ItemsSource="{Binding Path=TabList}">
    <TabControl.ItemTemplate>
        <DataTemplate>
            <Label Content="{Binding Path=tabHeader}"/>
        </DataTemplate>
    </TabControl.ItemTemplate>
    <TabControl.ContentTemplate>
        <DataTemplate>
            <!-- Tabの内容は別途実装 -->
            <local:TabView/>
        </DataTemplate>
    </TabControl.ContentTemplate>
</TabControl>
```
- TabItemのContentに入れる内容はUserControl等で別途実装

## ViewModel
```
public TabControlViewModel
{
    public ObservableCollection<TabViewModel> TabList { get; } = new ObservableCollection<TabViewModel>();
}
```
- TabControlViewModelはTabControlのViewModel
- TabViewModelはTabItemのViewModel