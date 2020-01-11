[WPF開発ノウハウ集](../index.md)
# Tips(Database)

## 複数のSQL問合せを行う際の接続シーケンス

SQL問合せではSQLステートメントの実行時間以上に接続・切断に時間がかかるので、複数のSQL問合せが必要な場合はなるべく接続・切断の回数が少なくなるように注意する

- 悪い例
```
    接続
    SQL実行
    切断

    接続
    SQL実行
    切断
```

- 良い例
```
    接続
    SQL実行
    SQL実行
    切断
```

## DB切断を確実に完了したい時（System.Data.SQLite）

System.Data.Sqlite.SQLiteConnection.Close()を実行しても、その後ガベージコレクションが実行されるまでデータベースのインスタンスは開放されない<br/>
プログラム・プロセスからDBファイルを開放したい（削除、置換したい時等）場合は、切断後にガベージコレクションを手動で呼出す必要がある

- 例
```
    conn.Close();

    GC.Collect();
    GC.WaitForPendingFinalizers();

    File.Delete( "<DBファイルパス>" );
```
