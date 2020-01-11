# Tips(Label)

- LabelのContentに代入する文字列に"_"を使うと勝手に右隣の文字のアンダースコアとして表示される<br/>
　（Labelが"_"をAltショートカットに自動変換する）
　これを防ぐために文字列を直接代入する代わりにTextBlockを入れてそのTextBlockに文字を設定する方法は下記のとおり
    ```
    <Label>
        <TextBlock Text="Sample_Text">
    </label>
    ```

    Styleとして定義する場合の実装例
    ```
    <Style TargetType="{x:Type Label}">
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type Label}">
                    <TextBlock IsEnabled="{TemplateBinding IsEnabled}"
                            　　MinHeight="{TemplateBinding MinHeight}"
                            　　MinWidth="{TemplateBinding MinWidth}"
                            　　Margin="{TemplateBinding Margin}"
                            　　Padding="{TemplateBinding Padding}"
                            　　VerticalAlignment="{TemplateBinding VerticalContentAlignment}"
                            　　HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}"
                            　　Background="{TemplateBinding Background}"
                            　　Foreground="{TemplateBinding Foreground}">
                    </TextBlock>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
    ```
