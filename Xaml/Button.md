# Buttonの実装

## 標準的なボタン

- Xaml
```
<Button Content="Addボタン" Command="{Binding AddCommand">
```
（Bindingについては "ICommandの実装" の項を参照）

## 応用（ハンバーガーボタン）
見た目を四角でなく円形にして、ボタン押下時にContextMenuを呼び出す

- Xaml
```
<UserControl.Resources>
    <Style x:Key="CustomFocusVisualStyle">
        <Setter Property="Control.Template">
            <Setter.Value>
                <ControlTemplate>
                    <Border CornerRadius="20" BorderBrush="DodgerBlue" BorderThickness="1"/>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</UserControl.Resources>

<UserControl>
    <Button Content="Ξ" Foreground="Black" Padding="7,2,7,2" MinHeight="23" MinWidth="23" Click="Button_Click"
            FocusVisualStyle="{StaticResource ResourceKey=CustomFocusVisualStyle}">
        <Button.Template>
            <ControlTemplate TargetType="Button">
                <Border Name="border" CornerRadius="20" ClipToBounds="True"
                        BorderBrush="DimGray" BorderThickness="0.75" Background="{TemplateBinding Background}">
                    <!--{TemplateBinding Background}-->
                    <ContentPresenter VerticalAlignment="Center" HorizontalAlignment="Center" />
                </Border>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsMouseOver" Value="True">
                        <Setter TargetName="border" Property="Background" Value="LightBlue" />
                        <Setter TargetName="border" Property="BorderBrush" Value="DodgerBlue" />
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Button.Template>
    </Button>
</UserControl>
```

- Xaml.cs
```
private void Button_Click( object sender, RoutedEventArgs e )
{
    e.Handled = true;
    this._channelTableView.contextMenu.PlacementTarget = this._channelTableView.dataGrid;
    this._channelTableView.contextMenu.IsOpen = true;
}
```
