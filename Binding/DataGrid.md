[WPF開発ノウハウ集](../index.md)
# Binding(DataGrid)の実装

- Xaml
    - （Xamlについては [Xaml(DataGrid)の実装](../Xaml/DataGrid.md) の項を参照）
<br/>

- Xaml.cs
    - コンストラクタの中等
    ```
        this.DataContext = <ViewModelのインスタンス>
    ```

- Row.cs
    - DataGridの行の各セルの情報を保持するクラスを作成
    ```
        using System.Linq;　/* FirstOrDefault()関数を使うために記述 */

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
    - ComboBox1に "Item.1"～"Item.3"を設定
    - DataGridには先頭セルに1～99を設定した行を99行設定

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
