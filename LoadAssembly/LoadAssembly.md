[WPF開発ノウハウ集](../index.md)
# 外部アセンブリを動的に読み込む

#### アプリケーション起動後に外部アセンブリ(.dllファイル等)を読み込んで利用することができる


- 外部アセンブリから特定の親クラスを継承したクラスを取得する場合
```
using System.Reflection; /* Assemblyを使用するために記述 */

Type getInheritance( string filePath )
{
    Assembly dll = Assembly.LoadFrom( filePath );
    foreach( Type type in dll.GetTypes() )
    {
        if( type.IsClass )
        {
            if( type.IsSubclassOf( typeof( <親クラス> ) ) )
            {
                return type;
            }
        }
    }
    return null;
}
```

- 外部アセンブリから特定のインターフェースを実装したクラスを取得する場合
```
using System.Reflection; /* Assemblyを使用するために記述 */

Type getImplement( string filePath )
{
    Assembly dll = Assembly.LoadFrom( string filePath );
    foreach( Type type in dll.GetTypes() )
    {
        if( type.IsClass )
        {
            if( type.GetInterface( typeof( <インターフェース> ).FullName ) != null )
            {
                return type;
            }
        }
    }
    return null;
}
```

- 取得したクラスのインスタンスを生成する
```
object getInstance( Type type )
{
    return Activator.CreateInstance( type );
}
```
