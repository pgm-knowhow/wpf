# Binding(ComboBox)の実装

## Binding List

- Xaml
```
<ComboBox ItemsSource="{Binding ComboBox1}" SelectedIndex="{Binding SelectedIndex1}"/>
```

- Xaml.cs
コンストラクタの中等
```
this.DataContext = <ViewModelのインスタンス>
```

- ViewModel
```
public ObservableCollection<int> ComboBox1 { get; set; } = new ObservableCollection<int>() { 1, 2 };
public int SelectedIndex1 { get; set; } = 0;
```

## Binding Dictionary

- Xaml
```        
<ComboBox ItemsSource="{Binding ComboBox1}" SelectedValue="{Binding SelectedValue1}"
          SelectedValuePath="Key" DisplayMemberPath="Value"/>
```

- ViewModel
```
public Dictionary<int, string> ComboBox1 { get; set; } = new Dictionary<int, string>() 
{ 
  { 1, "str1" }, 
  { 2, "str2" } 
};
public int SelectedValue1 { get; set; } = 1;
```

