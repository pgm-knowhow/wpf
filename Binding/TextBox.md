# Binding(TextBox)の実装

- Xaml
    ```
    <TextBox Text="{Binding Text1}">
    ```

- Xaml.cs
    コンストラクタの中等
    ```
    this.DataContext = <ViewModelのインスタンス>
    ```

- ViewModel
    ```
    public string Text1 { get; set; } = "テキスト";
    ```
