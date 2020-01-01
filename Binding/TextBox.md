# Binding(TextBox))の実装

- Xaml
```
<TextBox Text="{Binding Text1}">
```

- ViewModel
```
public string Text1 { get; set; } = "テキスト";
```
