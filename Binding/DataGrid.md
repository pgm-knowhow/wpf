[WPF開発ノウハウ集](../index.md)
# Binding(DataGrid)の実装

- Xaml
    ```
    <DataGrid ItemsSource="{Binding DataGrid1}">
    ```

- Xaml.cs
コンストラクタの中等
    ```
    this.DataContext = <ViewModelのインスタンス>
    ```

- ViewModel
    ```
    public class Row 
    {
        public int Row1 { get; set; } = 0;
        public string Row2 { get; set; } = string.Empty;
    }
    public ObservableCollection<Row> DataGrid1 { get; } = new ObservableCollection<Row>()
    {
        new Row() { Row1 = 1, Row2 = "abc" },
        new Row() { Row1 = 2, Row2 = "def" }
    };
    ```
    DataGridは表示だけで入力がないので set; は不要（入力はDataGrid上のDataGridRowやDataGridCellが対象）