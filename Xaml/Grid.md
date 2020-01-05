# Xaml(Grid)の実装

2列x3行のグリッド
```
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto"/>
            <ColumnDefinition Width="Auto"/>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <Label Grid.Column="0" Grid.Row="0" Content="a1"/>
        <Label Grid.Column="1" Grid.Row="0" Content="b1"/>

        <Label Grid.Column="0" Grid.Row="1" Content="a2"/>
        <Label Grid.Column="1" Grid.Row="1" Content="b2"/>

        <Label Grid.Column="0" Grid.Row="2" Content="a3"/>
        <Label Grid.Column="1" Grid.Row="2" Content="b3"/>

    </Grid>
```
WidthとHeightをAutoに設定しておくと、表示時にグリッド各セルに設定したコントロールの内容に応じて自動サイズ調整が働く

- 隣の列、隣の行との結合
```
<Label Grid.Column="0" Grid.Row="0" Content="a1"
       Grid.ColumnSpan="2" Grid.RowSpan="2">
```

- メモ
ColumnSpanで結合すると列幅の自動調整が効かない。。。と思っていたが勘違い？