[WPF開発ノウハウ集](../index.md)
# Binding(DataGrid)の実装

- Xaml
    （Xamlについては [Xaml(DataGrid)の実装](../Xaml/DataGrid.md) の項を参照）
<br/>

- Xaml.cs

    コンストラクタの中等
    ```
    this.DataContext = <ViewModelのインスタンス>
    ```

- Row.cs

    DataGridの行の各セルの情報を保持するクラスを作成する
    ```
    public class Row 
    {
        public int LabelColumn { get; set; } = 0;
        public string TextBlockColumn { get; set; } = "TextBlock";
        public string TextBoxColumn { get; set; } = "TextBox";
        public bool CheckBoxColumn { get; set; } = false;
        public string ComboBoxColumn { get; set; } = ViewModel.ComboBox1.FirstOrDefault();
    } 
    ```

- ViewModel.cs
    ```
    public ObservableCollection<Row> DataGrid1 { get; } = new ObservableCollection<Row>();
    public static ObservableCollection<string> ComboBox1 { get; } = new ObservableCollection<string>()
    {
        "Item.1", "Item.2", "Item.3"
    };
    public ViewModel()
    {
        for( int i = 1; i < 100; i++ )
        {
            this.DataGrid1.Add( new Row() { LabelColumn = i } );
        }        
    }
    ```
