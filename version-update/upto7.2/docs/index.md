# Zabbix のバージョン更新手続き

* 7.0 -> 7.2 の手順を示します。

## Version 7.2 要求事項

* [System requirements](https://www.zabbix.com/documentation/current/en/manual/installation/requirements)

## 7.0 -> 7.2 後方互換性のない変更について

* [Oracle DB](https://www.oracle.com/jp/database/) サポートが削除されました。

## [サーバのアップグレード手順(公式)](https://www.zabbix.com/documentation/current/en/manual/installation/upgrade/sources)

1. [サーバを停止する。](./service-stop.md)
1. 既存の [zabbixデータベース](./backenddb.md)の[バックアップ](./dbbackup.md)
1. [設定ファイル](./config.md)、[PHPファイル](./phpscript.md)、[Zabbixバイナリのバックアップ](./zabbix-files-backup.md)
1. 新しいサーババイナリを[インストール](./pkg-or-ports-install.md)
1. サーバ[構成パラメータを確認](./parameter-check.md)する。
1. 新しいZabbixバイナリの[起動](./service-up.md)

## データベース Update　に関する諸項目

* Zabbixサーバーは自動的にデータベースをアップグレードします。
* 起動すると、Zabbixサーバーは現在(必須およびオプション)と必要なデータベースバージョンを報告します。
* 現在の必須バージョンが必要のバージョンよりも古い場合、Zabbixサーバーは必要なデータベースアップグレードパッチを自動的に実行します。
* データベースのアップグレードの開始レベルと進行状況レベル(パーセント)は、Zabbixサーバーログファイルに書き込まれます。
* アップグレードが完了すると、ログファイルに「データベースのアップグレードが完全に完了した」メッセージが書き込まれます

### 更新に失敗したとき

* アップグレードパッチのいずれかが失敗した場合、Zabbixサーバーは起動しません。
* また、現在の必須データベースバージョンが必要なものよりも新しい場合、Zabbixサーバーは起動しません。
* Zabbixサーバーは、現在の必須データベースバージョンが必須バージョンに対応する場合にのみ起動します。

> 8673:20161117:104750.259 current database version (mandatory/optional): 03040000/03040000
       8673:20161117:104750.259 required mandatory version: 03040000
---

* サーバ起動前にチェックスべき項目
  * データベースユーザが十分な権限を有することを確認
    * Table 作成 ☐
    * Table 削除 ☐
    * Index 作成 ☐
    * Index 削除 ☐
  * 十分な空きディスク容量があるかを確認

## 新しいZabbix PHP Webスクリプトをインストール
