# ToggleButtonを実装する

ToggleButtonはCheckBoxの代替として用意した
- テキスト非依存のOn/Off表現
- Binding対応
- IsEnabled="False"時の非活性表示対応

## Xaml
```
<UserControl x:Class="Common.usercontrol.src.ToggleButton"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             IsEnabledChanged="UserControl_IsEnabledChanged"
             MouseUp="UserControl_MouseUp" MouseEnter="UserControl_MouseEnter" MouseLeave="UserControl_MouseLeave">

    <UserControl.Resources>
        <Style x:Key="CustomFocusVisualStyle">
            <Setter Property="Control.Template">
                <Setter.Value>
                    <ControlTemplate>
                        <Border BorderBrush="DodgerBlue" BorderThickness="1"/>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </UserControl.Resources>

    <Border Name="border" MinWidth="40" BorderThickness="1" BorderBrush="Gray" Background="WhiteSmoke" CornerRadius="9">
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="*"/>
                <ColumnDefinition Width="*"/>
            </Grid.ColumnDefinitions>

            
            <TextBlock Grid.Column="0" Name="textOn" Text="" FontSize="8" Foreground="Gray"
                       VerticalAlignment="Center" HorizontalAlignment="Center"/>

            <TextBlock Grid.Column="1" Name="textOff" Text="" FontSize="8" Foreground="Gray"
                       VerticalAlignment="Center" HorizontalAlignment="Center"/>

            
            <Button Grid.Column="0" Name="btnOn" FocusVisualStyle="{x:Null}"
                    VerticalAlignment="Stretch" HorizontalAlignment="Stretch" 
                    BorderThickness="1" BorderBrush="DimGray" Background="#FFEBEBEC" 
                    Visibility="Visible" Click="Btn_Click"
                    GotKeyboardFocus="BtnOn_GotKeyboardFocus" LostKeyboardFocus="BtnOff_LostKeyboardFocus">
                <Button.Template>
                    <ControlTemplate TargetType="Button">
                        <Border Name="border" Margin="1" CornerRadius="9" ClipToBounds="True" 
                                BorderBrush="{TemplateBinding BorderBrush}" 
                                BorderThickness="{TemplateBinding BorderThickness}" 
                                Background="{TemplateBinding Background}">
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

            <Button Grid.Column="1" Name="btnOff" FocusVisualStyle="{x:Null}"
                    VerticalAlignment="Stretch" HorizontalAlignment="Stretch"
                    BorderThickness="1" BorderBrush="DimGray" Background="#FFEBEBEC" 
                    Visibility="Collapsed" Click="Btn_Click" 
                    GotKeyboardFocus="BtnOn_GotKeyboardFocus" LostKeyboardFocus="BtnOff_LostKeyboardFocus">
                <Button.Template>
                    <ControlTemplate TargetType="Button">
                        <Border Name="border" Margin="1" CornerRadius="9" ClipToBounds="True" 
                                BorderBrush="{TemplateBinding BorderBrush}" 
                                BorderThickness="{TemplateBinding BorderThickness}" 
                                Background="{TemplateBinding Background}">
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
            
        </Grid>
        <Border.Triggers>
        </Border.Triggers>
    </Border>
</UserControl>
```

## Xaml.cs
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace Common.usercontrol.src
{
    /// <summary>
    /// ToggleButton.xaml の相互作用ロジック
    /// </summary>
    public partial class ToggleButton : UserControl
    {
        public ToggleButton()
        {
            this.InitializeComponent();
        }

        #region DependencyProperty Loop
        public static readonly DependencyProperty IsToggledOnProperty = DependencyProperty.Register(
            "IsToggledOn",
            typeof( bool ),
            typeof( ToggleButton ),
            new FrameworkPropertyMetadata( false, FrameworkPropertyMetadataOptions.BindsTwoWayByDefault, new PropertyChangedCallback( ToggleButton.OnToggleChanged ) )
        );

        [System.Diagnostics.CodeAnalysis.SuppressMessage( "Style", "IDE1006:Naming Styles" )]
        public bool IsToggledOn
        {
            get
            {
                return (bool)this.GetValue( ToggleButton.IsToggledOnProperty );
            }
            set
            {
                this.SetValue( ToggleButton.IsToggledOnProperty, value );
            }
        }

        private static void OnToggleChanged( DependencyObject obj, DependencyPropertyChangedEventArgs e )
        {
            ToggleButton toggleButton = obj as ToggleButton;
            if( toggleButton != null )
            {
                toggleButton.Toggle();
            }
        }
        #endregion

        private void Btn_Click( object sender, RoutedEventArgs e )
        {
            this.IsToggledOn = !this.IsToggledOn;
        }

        private void UserControl_MouseUp( object sender, MouseButtonEventArgs e )
        {
            this.IsToggledOn = !this.IsToggledOn;
        }

        private void UserControl_MouseEnter( object sender, MouseEventArgs e )
        {
            if( this.IsEnabled )
            {
                this.border.BorderBrush = Brushes.DodgerBlue;
            }
        }

        private void UserControl_MouseLeave( object sender, MouseEventArgs e )
        {
            if( this.IsEnabled )
            {
                this.border.BorderBrush = Brushes.Gray;
            }
        }

        private void BtnOn_GotKeyboardFocus( object sender, KeyboardFocusChangedEventArgs e )
        {
            if( this.IsEnabled )
            {
                this.border.BorderBrush = Brushes.DodgerBlue;
            }
        }

        private void BtnOff_LostKeyboardFocus( object sender, KeyboardFocusChangedEventArgs e )
        {
            if( this.IsEnabled )
            {
                this.border.BorderBrush = Brushes.Gray;
            }
        }

        public void Toggle()
        {
            if( this.IsToggledOn )
            {
                this.border.Background = Brushes.PaleGreen;
                this.btnOn.Visibility = Visibility.Collapsed;
                this.btnOff.Visibility = Visibility.Visible;
                this.btnOff.Focus();
            }
            else
            {
                this.border.Background = Brushes.WhiteSmoke;
                this.btnOff.Visibility = Visibility.Collapsed;
                this.btnOn.Visibility = Visibility.Visible;
                this.btnOn.Focus();
            }
        }

        private void UserControl_IsEnabledChanged( object sender, DependencyPropertyChangedEventArgs e )
        {
            if( this.IsEnabled )
            {
                if( this.IsToggledOn )
                {
                    this.border.Background = Brushes.PaleGreen;
                }
                else
                {
                    this.border.Background = Brushes.WhiteSmoke;
                }
                this.border.BorderBrush = Brushes.Gray;
                this.textOff.Foreground = Brushes.Black;
                this.textOn.Foreground = Brushes.Black;

                this.btnOff.BorderThickness = new Thickness( 1 );
                this.btnOn.BorderThickness = new Thickness( 1 );
            }
            else
            {
                if( this.IsToggledOn )
                {
                    this.border.Background = (Brush)( new BrushConverter().ConvertFromString( "#FFE4FFE4" ) );
                }
                else
                {
                    this.border.Background = Brushes.WhiteSmoke;
                }
                this.border.BorderBrush = Brushes.LightGray;
                this.textOff.Foreground = Brushes.LightGray;
                this.textOn.Foreground = Brushes.LightGray;

                this.btnOff.BorderThickness = new Thickness( 0 );
                this.btnOn.BorderThickness = new Thickness( 0 );
            }
        }
    }
}
```


