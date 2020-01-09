[WPF開発ノウハウ集](../index.md)
# Binding(CheckBox)の実装

- Xaml
    ```
    <CheckBox IsChecked="{Binding IsChecked1}">
    ```

- Xaml.cs
コンストラクタの中等
    ```
    this.DataContext = <ViewModelのインスタンス>
    ```

- ViewModel
    ```
    public bool IsChecked1 { get; set; } = false;
    ```
