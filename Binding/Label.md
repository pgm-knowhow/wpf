# Binding(Label)の実装

- Xaml
```
<Label Content="{Binding Label1}">
```

- Xaml.cs
コンストラクタの中等
```
this.DataContext = <ViewModelのインスタンス>
```

- ViewModel
```
public string Label1 { get; } = "ラベル";
```
Labelは表示だけで入力がないので set; は不要