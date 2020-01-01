# Binding(CheckBox))の実装

- Xaml
```
<CheckBox IsChecked="{Binding IsChecked1}">
```

- ViewModel
```
public bool IsChecked1 { get; set; } = false;
```
