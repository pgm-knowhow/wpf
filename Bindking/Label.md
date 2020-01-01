# Binding(Label)の実装

- Xaml
```
<Label Content="{Binding Label1}">
```

- ViewModel
```
public string Label1 { get; } = "ラベル";
```
Labelは表示だけで入力がないので set; は不要