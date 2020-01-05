# Xaml(TabControl)の実装

## Xaml

```
<TabControl>
    <TabItem Header="タブ１">
        <Grid>
            〜タブに表示する内容〜
        </Grid>
    </TabItem>
    <TabItem Header="タブ２">
        <Grid>
            〜タブに表示する内容〜
        </Grid>
    </TabItem>
</TabControl>
```

タブヘッダにLabelを使う場合
```
<TabControl>
    <TabItem>
        <TabItem.Header>
            <Label Content="タブ１">
        </TabItem.Header>
        <Grid>
            〜タブに表示する内容〜
        </Grid>
    </TabItem>
    <TabItem>
        <TabItem.Header>
            <Label Content="タブ２">
        </TabItem.Header>
        <Grid>
            〜タブに表示する内容〜
        </Grid>
    </TabItem>
</TabControl>
```

## Xaml.cs

- コードビハインドからTabItemを追加する
```
this.TabControl.Items.Add( new TabItem() { Header = "タブ１", Content = <UserControlインスタンス等> } );
```