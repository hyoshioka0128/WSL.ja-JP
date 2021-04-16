---
title: WSL を使用したデータベースの追加または接続
description: Windows Subsystem for Linux で MySQL MongoDB、PostgreSQL、SQLite、Microsoft SQL Server、または Redis を設定する方法について説明します。
keywords: wsl、windows、windowssubsystem、MySQL MongoDB、PostgreSQL、SQLite、Microsoft SQL Server、Redis、windows 10
ms.date: 04/07/2021
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7fd5cc05282025dd9e0d7fa505e3667c8f67c5a9
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493584"
---
# <a name="get-started-with-databases-on-windows-subsystem-for-linux"></a>Windows Subsystem for Linux でデータベースを使ってみる

このステップバイステップガイドでは、WSL 内のプロジェクトをデータベースに接続する方法について説明します。 MySQL、PostgreSQL、MongoDB、Redis、Microsoft SQL Server、または SQLite の使用を開始します。

## <a name="prerequisites"></a>前提条件

- [バージョン 2004](ms-settings:windowsupdate)、**ビルド 19041** 以上に更新された Windows 10 を実行している。
- [Wsl が有効になり、インストールされ、wsl 2 に更新されました](../install-win10.md)。
- [Linux ディストリビューションがインストールされている](../install-win10.md#step-6---install-your-linux-distribution-of-choice) (例については Ubuntu 18.04)。
- Ubuntu 18.04 のディストリビューションが [WSL 2 モードで実行](../install-win10.md#set-your-distribution-version-to-wsl-1-or-wsl-2)されていることを確認します。 (WSL は、v1 または v2 モードの両方でディストリビューションを実行できます。)これは PowerShell を開き、「`wsl -l -v`」と入力することによって確認できます。

## <a name="differences-between-database-systems"></a>データベースシステム間の相違点

データベースシステムの最も [一般的な選択肢](https://insights.stackoverflow.com/survey/2019#technology-_-databases) は次のとおりです。

- [MySQL](https://www.mysql.com/why-mysql/) (SQL)
- [PostgreSQL](https://www.postgresql.org/about/) (SQL)
- [Microsoft SQL Server](/sql) (SQL)
- [SQLite](https://www.sqlite.org/about.html) (SQL)
- [MongoDB](https://www.mongodb.com/what-is-mongodb) (NoSQL)
- [Redis](https://redis.io/topics/introduction) (NoSQL)

**MySQL** は、オープンソースの SQL リレーショナルデータベースで、データ型が相互に関連している可能性のある1つ以上のテーブルにデータを整理します。 この機能は垂直方向にスケーラブルであるため、1つの究極のコンピューターで作業が行われます。 現在、4つのデータベースシステムで最も広く使用されています。

**PostgreSQL** (Postgres とも呼ばれます) もオープンソースの SQL リレーショナルデータベースであり、拡張性と標準への準拠を重視しています。 現在は JSON も処理できますが、一般的には、構造化データ、垂直方向の規模拡張、および、e コマースや金融取引などの ACID 準拠のニーズに適しています。

**Microsoft SQL Server** には、Azure 上の Windows、SQL SERVER ON LINUX、SQL の SQL Server が含まれています。 これらは、ソフトウェアアプリケーションによって要求されたデータの格納と取得の主な機能を備えたサーバーに設定されたリレーショナルデータベース管理システムでもあります。

**SQLite** は、オープンソースの自己完結型の "サーバーレス" データベースです。低メモリ環境でも、移植性、信頼性、優れたパフォーマンスが確保されています。

**MongoDB** は、JSON を使用してスキーマフリーデータを格納するように設計されたオープンソースの NoSQL ドキュメントデータベースです。 水平方向にスケーラブルなので、複数の小さなマシンで作業が行われます。 柔軟性と非構造化データに適しており、リアルタイム分析をキャッシュしています。

**Redis** は、オープンソースのメモリ内の NoSQL データ構造ストアです。 ドキュメントではなく、ストレージにキーと値のペアを使用します。 Redis は、柔軟性、パフォーマンス、および幅広い言語のサポートのために認識されています。 キャッシュまたはメッセージブローカーとして使用するのに十分な柔軟性があり、リスト、セット、ハッシュなどのデータ構造を使用できます。

選択するデータベースの種類は、データベースを使用するアプリケーションの種類に応じて決める必要があります。 構造化データベースと非構造化データベースの長所と短所を検討し、ユースケースに基づいて選択することをお勧めします。

## <a name="install-mysql"></a>MySQL をインストールする

WSL に MySQL をインストールするには (Ubuntu 18.04):

1. WSL ターミナルを開きます (Ubuntu 18.04)。
2. `sudo apt update` を実行して Ubuntu パッケージを更新します。
3. パッケージが更新されたら、次のものを使用して MySQL をインストールします。 `sudo apt install mysql-server`
4. `mysql --version` を実行してインストールを確認し、バージョン番号を取得します。

また、含まれているセキュリティスクリプトを実行することもできます。 これにより、リモートルートログインやサンプルユーザーなどの、安全性の低い既定のオプションの一部が変更されます。 セキュリティスクリプトを実行するには:

1. MySQL サーバーを起動します。 `sudo /etc/init.d/mysql start`
2. セキュリティスクリプトのプロンプトを開始します。 `sudo mysql_secure_installation`
3. 最初のプロンプトで、パスワードの検証プラグインを設定するかどうかを確認するメッセージが表示されます。これを使用すると、MySQL パスワードの強度をテストできます。 次に、MySQL ルートユーザーのパスワードを設定し、匿名ユーザーを削除するかどうかを決定し、ルートユーザーがローカルとリモートの両方でログインできるようにするかどうかを決定し、テストデータベースを削除するかどうかを決定し、最後に特権テーブルを直ちに再読み込みするかどうかを決定します。

MySQL プロンプトを開くには、次のように入力します。 `sudo mysql`

使用できるデータベースを確認するには、MySQL プロンプトで次のように入力します。 `SHOW DATABASES;`

新しいデータベースを作成するには、次のように入力します。 `CREATE DATABASE database_name;`

データベースを削除するには、次のように入力します。 ` DROP DATABASE database_name;`

MySQL データベースの操作の詳細については、 [mysql のドキュメント](https://dev.mysql.com/doc/mysql-getting-started/en/)を参照してください。

VS Code で MySQL データベースを操作するには、 [mysql 拡張機能](https://marketplace.visualstudio.com/items?itemName=cweijan.vscode-mysql-client2)を試してください。

## <a name="install-postgresql"></a>PostgreSQL のインストール

WSL に PostgreSQL をインストールするには (Ubuntu 18.04):

1. WSL ターミナルを開きます (Ubuntu 18.04)。
2. `sudo apt update` を実行して Ubuntu パッケージを更新します。
3. パッケージが更新されたら、`sudo apt install postgresql postgresql-contrib` を実行して PostgreSQL (およびいくつかの便利なユーティリティが含まれている -contrib パッケージ) をインストールします。
4. `psql --version` を実行してインストールを確認し、バージョン番号を取得します。

PostgreSQL をインストールした後は、次の 3 つのコマンドについて覚えておく必要があります。

- データベースの状態を確認する `sudo service postgresql status`
- データベースの実行を開始する `sudo service postgresql start`
- データベースの実行を停止する `sudo service postgresql stop`

既定の管理者ユーザー `postgres` には、データベースに接続するパスワードを割り当てる必要があります。 パスワードを設定するには:

1. コマンド `sudo passwd postgres` を入力します。
2. 新しいパスワードを入力するように求めるメッセージが表示されます。
3. ターミナルを閉じ、開き直します。

[Psql](https://www.postgresql.org/docs/10/app-psql.html)シェルで PostgreSQL を実行するには、次のようにします。

1. `sudo service postgresql start` を実行して postgres サービスを開始します。
2. `sudo -u postgres psql` を実行して postgres サービスに接続し、psql シェルを開きます。

正常に psql シェルに入ると、コマンドラインが `postgres=#` のように変わります。

> [!NOTE]
> または、`su - postgres` を使用して postgres ユーザーに切り替え、コマンド `psql` を入力することで psql シェルを開くことができます。

Postgres = # enter を終了するに `\q` は、またはショートカットキーを使用します: Ctrl + D

PostgreSQL のインストールで作成されたユーザー アカウントを確認するには、WSL ターミナルから `psql -c "\du"` を使用します。または、psql シェルが開いている場合は、`\du` を実行します。 このコマンドでは、アカウントのユーザー名、ロール属性の一覧、およびロールグループのメンバーの列が表示されます。 `q` を入力すると、終了してコマンド ラインに戻ります。

PostgreSQL データベースの操作の詳細については、 [postgresql のドキュメント](https://www.postgresql.org/docs/13/tutorial-createdb.html)を参照してください。

VS Code で PostgreSQL データベースを使用するには、 [postgresql の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-ossdata.vscode-postgresql)を試してください。

## <a name="install-mongodb"></a>MongoDB をインストールする

WSL に MongoDB をインストールするには (Ubuntu 18.04):

1. WSL ターミナルを開きます (Ubuntu 18.04)。
2. `sudo apt update` を実行して Ubuntu パッケージを更新します。
3. パッケージが更新されたら、`sudo apt-get install mongodb` を実行して MongoDB をインストールします。
4. `mongod --version` を実行してインストールを確認し、バージョン番号を取得します。

MongoDB をインストールした後は、次の 3 つのコマンドについて覚えておく必要があります。

- データベースの状態を確認する `sudo service mongodb status`
- データベースの実行を開始する `sudo service mongodb start`
- データベースの実行を停止する `sudo service mongodb stop`

> [!NOTE]
> チュートリアルや記事で、`sudo systemctl status mongodb` コマンドが使用されている場合があります。 軽量状態を維持するために、WSL には `systemd` (Linux のサービス管理システム) は含まれていません。 代わりに、SysVinit を使用してマシン上のサービスを開始します。 違いはほとんどありませんが、チュートリアルで `sudo systemctl` が使用されている場合は、代わりに `sudo /etc/init.d/` を使用します。 たとえば、`sudo /etc/init.d/mongodb status` は WSL では `sudo systemctl status mongodb` になります。または、`sudo service mongodb status` を使用することもできます。

ローカルサーバーで Mongo データベースを実行するには、次のようにします。

1. データベースの状態を確認します。データベースを既に起動している場合を `sudo service mongodb status` 除き、[Fail] (失敗) の応答が表示されます。

2. データベースを起動します。 `sudo service mongodb start` [OK] の応答が表示されます。

3. データベースサーバーに接続し、診断コマンドを実行して確認します。これにより、 `mongo --eval 'db.runCommand({ connectionStatus: 1 })'` 現在のデータベースのバージョン、サーバーのアドレスとポート、および status コマンドの出力が出力されます。 応答の "ok" フィールドに `1` の値は、サーバーが動作していることを示しています。

4. MongoDB のサービスの実行を停止するには、`sudo service mongodb stop` と入力します。

> [!NOTE]
> MongoDB には、データを /data/db に格納する、ポート 27017 で実行するなど、いくつかの既定のパラメーターがあります。 また、`mongod` はデーモン (データベースのホスト プロセス) であり、`mongo` は `mongod` の特定のインスタンスに接続するコマンドライン シェルです。

VS Code は、 [Azure CosmosDB 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)を使用した mongodb データベースの操作をサポートしており、VS Code 内から mongodb データベースを作成、管理、クエリできます。 詳細については、「VS Code ドキュメント: [MongoDB の](https://code.visualstudio.com/docs/azure/mongodb)使用」を参照してください。

詳細については、MongoDB のドキュメントを参照してください。

- [MongoDB の使用の概要](https://docs.mongodb.com/manual/introduction/)
- [ユーザーの作成](https://docs.mongodb.com/manual/tutorial/create-users/)
- [リモートホスト上の MongoDB インスタンスに接続する](https://docs.mongodb.com/manual/mongo/#mongodb-instance-on-a-remote-host)
- [CRUD: 作成、読み取り、更新、削除](https://docs.mongodb.com/manual/crud/)
- [リファレンスドキュメント](https://docs.mongodb.com/manual/reference/)

## <a name="install-microsoft-sql-server"></a>Microsoft SQL Server のインストール:

WSL (Ubuntu 18.04) に SQL Server をインストールするには、次のクイックスタートに従ってください。 [ubuntu で SQL Server をインストールし、データベースを作成](/sql/linux/quickstart-install-connect-ubuntu)します。

VS Code で Microsoft SQL Server データベースを操作するには、 [MSSQL 拡張子](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)を試してください。

## <a name="install-sqlite"></a>SQLite をインストールする

WSL に SQLite をインストールするには (Ubuntu 18.04):

1. WSL ターミナルを開きます (Ubuntu 18.04)。
2. `sudo apt update` を実行して Ubuntu パッケージを更新します。
3. パッケージが更新されたら、次のように SQLite3 をインストールします。 `sudo apt install sqlite3`
4. `sqlite3 --version` を実行してインストールを確認し、バージョン番号を取得します。

"Example. db" という名前のテストデータベースを作成するには、次のように入力します。 `sqlite3 example.db`

SQLite データベースの一覧を表示するには、次のように入力します。 `.databases`

データベースの状態を確認するには、次のように入力します。 `.dbinfo ?DB?`

SQLite プロンプトを終了するには、次のように入力します。 `.exit`

SQLite データベースの操作の詳細については、 [sqlite のドキュメント](https://www.sqlite.org/quickstart.html)を参照してください。

VS Code で SQLite データベースを使用するには、 [sqlite 拡張機能](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)を試してください。

## <a name="install-redis"></a>Redis のインストール

WSL に Redis をインストールするには (Ubuntu 18.04):

1. WSL ターミナルを開きます (Ubuntu 18.04)。
2. `sudo apt update` を実行して Ubuntu パッケージを更新します。
3. パッケージが更新されたら、次のものを使用して Redis をインストールします。 `sudo apt install redis-server`
4. `redis-server --version` を実行してインストールを確認し、バージョン番号を取得します。

Redis サーバーの実行を開始するには、次のようにします。 `sudo service redis-server start`

Redis が動作しているかどうかを確認します (redis は、Redis と対話するためのコマンドラインインターフェイスユーティリティです)。これにより、 `redis-cli ping` "、" という応答が返されます。

Redis サーバーの実行を停止するには、次のようにします。 `sudo service redis-server stop`

Redis データベースの使用方法の詳細については、 [redis のドキュメント](https://redis.io/topics/quickstart)を参照してください。

VS Code で Redis データベースを使用するには、 [redis 拡張機能](https://marketplace.visualstudio.com/items?itemName=cweijan.vscode-redis-client)を試してください。

## <a name="see-services-running-and-set-up-profile-aliases"></a>「実行中のサービス」と「プロファイルの別名の設定」を参照してください。

現在 WSL ディストリビューションで実行されているサービスを表示するには、次のように入力します。 `service --status-all`

`sudo service mongodb start`、`sudo service postgres start`、`sudo -u postgrest psql` などの入力は面倒な場合があります。  これらのコマンドをすばやく使えるように、また覚えやすくするために、WSL 上の `.profile` ファイルでエイリアスを設定することを検討してください。

これらのコマンドを実行するためのカスタム エイリアス (ショートカット) を設定するには、次の手順を実行します。

1. WSL ターミナルを開き、`cd ~` と入力してルート ディレクトリに移動します。
2. `sudo nano .profile` と入力して、ターミナルの設定を制御する `.profile` ファイルを、ターミナルのテキスト エディター Nano で開きます。
3. ファイルの最後に次の内容を追加します (`# set PATH` 設定は変更しないでください)。

    ```bash
    # My Aliases
    alias start-pg='sudo service postgresql start'
    alias run-pg='sudo -u postgres psql'
    ```

    以後、`start-pg` と入力して postgresql サービスの実行を開始し、`run-pg` と入力して psql シェルを開くことができます。 `start-pg` および `run-pg` は任意の名前に変更できますが、postgres が既に使用しているコマンドを上書きしないよう注意してください。

4. 新しいエイリアスを追加したら、**Ctrl + X** キーを使用して Nano テキスト エディターを終了し、保存の確認に対して `Y` (はい) を選択して Enter キーを押します (ファイル名は `.profile` のままにします)。
5. WSL ターミナルを閉じて開き直してから、新しいエイリアス コマンドを試してみてください。

## <a name="additional-resources"></a>その他のリソース

- [Windows 10 での開発環境のセットアップ](/windows/dev-environment/)
