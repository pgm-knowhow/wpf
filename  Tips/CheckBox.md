# Tips(CheckBox)

## CheckBoxにint型のプロパティをBindする

IValueConverterの実装例

- IValueConverterの実装
```
/// <summary>
/// int型のプロパティをCheckBoxにBindできるようにするIValueConverterの実装です
/// </summary>
public class IntToBoolConverter : IValueConverter 
{

    /// <summary>
    /// valueがint型の時、1ならtrueを、それ以外ならfalseを返します
    /// </summary>
    public object Convert( object value, Type targetType, object parameter, System.Globalization.CultureInfo culture ) 
    {
        if( value is int ) 
        {
            if( 1 == ( int )value ) 
            {
                return true;
            }
            return false;
        }
        return false;
    }

    /// <summary>
    /// valueがbool型の時、trueなら1を、それ以外なら0を返します
    /// </summary>
    public object ConvertBack( object value, Type targetType, object parameter, System.Globalization.CultureInfo culture ) 
    {
        if( value is bool ) 
        {
            if( ( bool )value ) 
            {
                return 1;
            }
            return 0;
        }
        return 0;
    }
}
```

- 使用例
```
<UserControl.Resources>
    <converter:IntToBoolConverter x:Key="IntToBool"/>
</UserControl.Resources>

<CheckBox IsChecked="{Binding Path=IntProperty, Converter={StaticResource IntToBool}}"/>
```
