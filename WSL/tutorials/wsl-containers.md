---
title: Windows Subsystem for Linux で Docker コンテナーの使用を開始する
description: Windows Subsystem for Linux で Docker コンテナーを設定する方法について説明します。
keywords: wsl、windows、windowssubsystem、windows 10、docker、コンテナー
ms.date: 08/28/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: efd28892d108ccaa9d1e0372108b73df876f450c
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104726029"
---
# <a name="get-started-with-docker-remote-containers-on-wsl-2"></a>WSL 2 での Docker リモート コンテナーの概要

このステップバイステップガイドでは、WSL 2 (windows Subsystem for Linux、バージョン 2) を使用して **Docker Desktop For Windows** をセットアップすることで、リモートコンテナーを使用した開発を始めることができます。

Windows 用 Docker デスクトップは無料で利用でき、docker 化アプリのビルド、配布、実行のための開発環境を提供します。 WSL 2 ベースのエンジンを有効にすることで、同じコンピューター上の Docker デスクトップで Linux と Windows の両方のコンテナーを実行できます。

## <a name="overview-of-docker-containers"></a>Docker コンテナーの概要

Docker は、コンテナーを使用してアプリケーションを作成、展開、および実行するために使用されるツールです。 コンテナーを使用すると、開発者はアプリを必要なすべての部分 (ライブラリ、フレームワーク、依存関係など) とともにパッケージ化し、すべてを 1 つのパッケージとして出荷できます。 コンテナーを使用すると、カスタマイズされた設定や、アプリを実行しているコンピューターに以前にインストールされていたライブラリが、アプリのコードの記述とテストに使用されたマシンと異なる可能性がある場合でも、アプリが同じように実行されることが保証されます。 これにより、開発者は、コードが実行されるシステムの心配をすることなく、コードの記述に集中できます。

Docker コンテナーは仮想マシンに似ていますが、仮想オペレーティング システム全体を作成するわけではありません。 代わりに、Docker により、アプリが実行されているシステムと同じ Linux カーネルを使用することができます。 これにより、アプリ パッケージにはホスト コンピューター上にまだ存在しない部分だけが必要になるため、パッケージ サイズが減り、パフォーマンスを向上させることができます。

[Kubernetes](/azure/aks/) などのツールで Docker コンテナーを使用する、継続的な可用性が、コンテナーの人気のもう 1 つの理由です。 これにより、複数のバージョンのアプリ コンテナーを異なるタイミングで作成できます。 更新またはメンテナンスのためにシステム全体を停止するのではなく、各コンテナー (およびその特定のマイクロサービス) をすぐに置き換えることができます。 すべての更新プログラムが含まれた新しいコンテナーを準備し、運用環境用にコンテナーを設定して、新しいコンテナーの準備ができたら、それをポイントするだけです。 また、コンテナーを使用して異なるバージョンのアプリをアーカイブし、必要に応じて安全のフォールバックとしてそれらを実行し続けることもできます。

詳細については、Microsoft Learn の [Docker コンテナーの概要](/learn/modules/intro-to-docker-containers/) に関するページを参照してください。

## <a name="prerequisites"></a>前提条件

- コンピューターで Windows 10 が実行されていること、バージョン2004、**ビルド 18362** 以降 [に更新さ](ms-settings:windowsupdate)れていることを確認します。
- [WSL を有効にし、Linux ディストリビューションをインストールして、wsl 2 に更新](../install-win10.md)します。
- [Linux カーネル更新パッケージをダウンロードしてインストール](../install-win10.md#step-4---download-the-linux-kernel-update-package)します。
- [Visual Studio Code をインストール](https://code.visualstudio.com/download)します *(省略可能)*。 これにより、リモート Docker コンテナー内でコードおよびデバッグを行い、Linux ディストリビューションに接続する機能など、最適なエクスペリエンスが提供されます。
- [Windows ターミナルをインストール](/windows/terminal/get-started)します *(省略可能)*。 これにより、同じインターフェイス (Ubuntu、Debian、PowerShell、Azure CLI など) で複数のターミナルをカスタマイズして開く機能など、最適なエクスペリエンスが得られます。
- Docker [Hub で DOCKER ID にサインアップ](https://hub.docker.com/signup)します *(省略可能)*。

> [!NOTE]
> Wsl は、WSL バージョン1または WSL 2 モードの両方でディストリビューションを実行できます。 これを確認するには、PowerShell を開き、「」と入力し `wsl -l -v` ます。 次のように入力して、ディストリビューションが WSL 2 を使用するように設定されていることを確認し `wsl --set-version  <distro> 2` ます。 `<distro>`をディストリビューション名 (Ubuntu 18.04 など) に置き換えます。
> 
> WSL バージョン1では、Windows と Linux の基本的な違いにより、Docker エンジンは WSL 内で直接実行できませんでした。そのため、Docker チームは、Hyper-v Vm と LinuxKit を使用して代替ソリューションを開発しました。 ただし、WSL 2 は、完全なシステムコールの容量を持つ Linux カーネルで実行されるようになったため、Docker は WSL 2 で完全に実行できます。 つまり、Linux コンテナーはエミュレーションなしでネイティブに実行できるため、Windows と Linux の両方のツール間でパフォーマンスと相互運用性が向上します。

## <a name="install-docker-desktop"></a>Docker Desktop のインストール

Docker Desktop for Windows でサポートされている WSL 2 バックエンドでは、Linux ベースの開発環境で作業し、コードの編集とデバッグに Visual Studio Code を使用し、Windows の Microsoft Edge ブラウザーでコンテナーを実行できます。

Docker をインストールするには ( [WSL 2](../install-win10.md)を既にインストールした後):

1. [Docker Desktop](https://docs.docker.com/docker-for-windows/wsl/#download)をダウンロードし、インストール手順に従います。

2. インストールが完了したら、Windows の [スタート] メニューから Docker Desktop を起動し、タスクバーの [非表示のアイコン] メニューから Docker アイコンを選択します。 アイコンを右クリックして [Docker コマンド] メニューを表示し、[設定] を選択します。
    ![Docker デスクトップダッシュボードアイコン](../media/docker-starting.png)

3. [**設定**]  >  **[全般**] で [wsl 2 ベースのエンジンを使用する] がオンになっていることを確認します。
    ![Docker Desktop の全般設定](../media/docker-running.png)

4. [**設定**] [リソース] [  >    >  **wsl 統合**] の順に移動して、Docker 統合を有効にするインストール済みの wsl 2 ディストリビューションを選択します。
    ![Docker デスクトップリソースの設定](../media/docker-dashboard.png)

5. Docker がインストールされていることを確認するには、次のように入力して、WSL ディストリビューション (Ubuntu など) を開き、バージョンとビルド番号を表示します。 `docker --version`

6. 次のものを使用して単純な組み込みの Docker イメージを実行することで、インストールが正しく機能することをテストします。 `docker run hello-world`

> [!TIP]
> いくつかの便利な Docker コマンドを次に示します。
>
> - `docker` を入力して、Docker CLI で使用できるコマンドを一覧表示します。
> - `docker <COMMAND> --help` を使用して、特定のコマンドの情報を一覧表示します。
> - `docker image ls --all` を使用して、お使いのマシン上の docker イメージを一覧表示します (この時点では hello world イメージのみ)。
> - コンピューターのコンテナーを一覧表示 `docker container ls --all` する: または `docker ps -a` (-a show all フラグを指定しない場合は、実行中のコンテナーのみが表示されます)
> - 次のように、WSL 2 コンテキストで使用可能な統計とリソース (CPU & メモリ) を含む、Docker のインストールに関するシステム全体の情報を一覧表示します。 `docker info`

## <a name="develop-in-remote-containers-using-vs-code"></a>VS Code を使用したリモートコンテナーでの開発

WSL 2 で Docker を使用してアプリの開発を開始するには、リモート WSL 拡張機能と Docker 拡張機能と共に VS Code を使用することをお勧めします。

- [VS Code Remote WSL 拡張機能をインストール](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)します。 この拡張機能を使用すると、VS Code の WSL で実行されている Linux プロジェクトを開くことができます (パスの問題、バイナリの互換性、またはその他の OS 間の課題について心配する必要はありません)。

- [VS code Remote-Containers 拡張機能をインストール](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)します。 この拡張機能を使用すると、コンテナー内のプロジェクトフォルダーまたはリポジトリを開くことができます。これにより、Visual Studio Code の完全な機能セットを利用して、コンテナー内で開発作業を行うことができます。

- [VS Code Docker 拡張機能をインストール](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)します。 この拡張機能により、VS Code の内部からコンテナー化アプリケーションをビルド、管理、およびデプロイする機能が追加されます。 (実際に開発環境としてコンテナーを使用するには、Remote-Container の拡張機能が必要です)。

Docker を使用して、既存のアプリプロジェクトの開発コンテナーを作成しましょう。

1. この例では、Python 開発環境の [Django に関する Hello World](/windows/python/web-frameworks#hello-world-tutorial-for-django) 記事のソースコードを使用して、ドキュメントを設定します。独自のプロジェクトソースコードを使用する場合は、この手順を省略できます。 GitHub から HelloWorld-Django web アプリをダウンロードするには、WSL ターミナル (Ubuntu など) を開き、次のように入力します。 `git clone https://github.com/mattwojo/helloworld-django.git`

    > [!NOTE]
    > コードは、ツールを使用しているのと同じファイルシステムに常に格納してください。 これにより、ファイルアクセスのパフォーマンスが向上します。 この例では、Linux ディストリビューション (Ubuntu) を使用して、WSL ファイルシステムにプロジェクトファイルを格納し `\\wsl\` ます。 Windows ファイルシステムにプロジェクトファイルを格納すると、WSL の Linux ツールを使用してこれらのファイルにアクセスするときに、処理が大幅に遅くなります。

2. WSL ターミナルから、このプロジェクトのソースコードフォルダーにディレクトリを変更します。

    ```bash
    cd helloworld-django
    ```

3. 次のように入力して、ローカルのリモート WSL 拡張サーバーで実行されている VS Code でプロジェクトを開きます。

    ```bash
    code .
    ```

    VS Code インスタンスの左下隅にある緑色のリモートインジケーターを確認して、WSL Linux ディストリビューションに接続していることを確認します。

    ![WSL リモートインジケーターの VS Code](../media/vscode-remote-indicator.png)

4. VS Code コマンドパレット (Ctrl + Shift + P) で、「 **リモートコンテナー: コンテナー内のフォルダーを開く...** 」と入力します。入力を開始したときにこのコマンドが表示されない場合は、上にリンクされているリモートコンテナー拡張機能がインストールされていることを確認してください。

    ![リモートコンテナーコマンドの VS Code](../media/docker-extension.png)

5. コンテナー化するプロジェクトフォルダーを選択します。 ここでは、次のようになります。 `\\wsl\Ubuntu-20.04\home\mattwojo\repos\helloworld-django\`

    ![リモートコンテナーフォルダーの VS Code](../media/docker-extension2.png)

6. プロジェクトフォルダー (リポジトリ) に DevContainer 構成がまだないため、コンテナー定義の一覧が表示されます。 表示されるコンテナー構成定義の一覧は、プロジェクトの種類に基づいてフィルター処理されます。 Django プロジェクトの場合は、Python 3 を選択します。

    ![リモートコンテナー構成定義の VS Code](../media/docker-extension3.png)

7. VS Code の新しいインスタンスが開き、新しいイメージの構築が開始されます。ビルドが完了すると、コンテナーが開始されます。 新しい `.devcontainer` フォルダーが、およびファイル内のコンテナー構成情報と共に表示され `Dockerfile` `devcontainer.json` ます。  

    ![VS Code devcontainer フォルダー](../media/docker-extension4.png)

8. プロジェクトが引き続き WSL とコンテナー内の両方に接続されていることを確認するには、VS Code 統合ターミナル (Ctrl + Shift + ~) を開きます。 次のように入力してオペレーティングシステムを確認します。 `uname` `python3 --version` Uname が "Linux" として返されたので、WSL 2 エンジンにまだ接続していることを確認できます。 Python のバージョン番号は、WSL 分布にインストールされている Python のバージョンとは異なる可能性のあるコンテナーの構成に基づいています。

9. Visual Studio Code を使用してコンテナー内でアプリを実行およびデバッグするには、最初に [ **実行** ] メニューを開きます (Ctrl + Shift + D キーを押すか、左端のメニューバーで [] タブを選択します)。 次に、[ **実行とデバッグ** ] を選択してデバッグ構成を選択し、プロジェクトに最適な構成を選択します (この例では "Django" になります)。 これにより、 `launch.json` プロジェクトのフォルダーにファイルが作成され、 `.vscode` アプリを実行する手順が表示されます。

    ![デバッグ構成を実行 VS Code には](../media/vscode-run-config.png)

10. VS Code 内から [デバッグ] [デバッグの開始]**を選択し**  >  ます (または、 **F5** キーを押します)。 これにより VS Code 内のターミナルが開き、" http://127.0.0.1:8000/ コントロール-C を使用してサーバーを起動しています" という結果が表示されます。 Ctrl キーを押しながら、表示されるアドレスを選択して、既定の web ブラウザーでアプリを開き、そのコンテナー内で実行されているプロジェクトを確認します。

    ![Docker コンテナーを実行 VS Code](../media/vscode-running-in-container.png)

これで、WSL 2 バックエンドを使用している Docker Desktop を使用してリモート開発コンテナーが正常に構成されました。これは、VS Code を使用してコーディング、ビルド、実行、配置、またはデバッグを行うことができます。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="wsl-docker-context-deprecated"></a>WSL docker コンテキストの非推奨

WSL 用の Docker の早期技術プレビューを使用していた場合は、"wsl" という名前の Docker コンテキストを使用している可能性があります。これは現在非推奨とされ、使用されなくなりました。 を確認するには、コマンドを使用 `docker context ls` します。 この "wsl" コンテキストを削除して、コマンドでエラーを回避できます。 `docker context rm wsl` Windows と WSL2 の両方に既定のコンテキストを使用します。

この非推奨の wsl コンテキストで発生する可能性のあるエラーには、次のものがあります。 `docker wsl open //./pipe/docker_wsl: The system cannot find the file specified.``error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_wsl/v1.40/images/json?all=1: open //./pipe/docker_wsl: The system cannot find the file specified.`

この問題の詳細については、 [windows 10 で Windows System For Linux (WSL2) で Docker をセットアップする方法に関する説明](https://www.hanselman.com/blog/HowToSetUpDockerWithinWindowsSystemForLinuxWSL2OnWindows10.aspx)を参照してください。

### <a name="trouble-finding-docker-image-storage-folder"></a>Docker イメージストレージフォルダーの検索に問題があります

Docker では、データを格納するために2つのディストリビューションフォルダーが作成されます。
- \\wsl $-dockerdesktop
- \\wsl $/dockerdata

これらのフォルダーを見つけるには、WSL Linux ディストリビューションを開き、「」と入力します。エクスプローラー `explorer.exe .` でフォルダーを表示するには、「」と入力します。 「」と入力します。 `\\wsl\<distro name>\mnt\wsl` `<distro name>` は、実際の配布の名前 (ie) に置き換えます。これらのフォルダーを表示するには、Ubuntu-20.04) を参照してください。

WSL で docker ストレージの場所を見つける方法の詳細については、 [wsl リポジトリ](https://github.com/microsoft/WSL/issues/4176) またはこの [stackoverlow の投稿](https://stackoverflow.com/questions/62380124/where-docker-image-is-stored-with-docker-desktop-for-windows)にあるこの問題を参照してください。

WSL での一般的なトラブルシューティングの問題の詳細については、 [トラブルシューティング](../troubleshooting.md) に関するドキュメントを参照してください。

## <a name="additional-resources"></a>その他のリソース

- [Docker ドキュメント: WSL 2 を使用した Docker デスクトップのベストプラクティス](https://docs.docker.com/docker-for-windows/wsl/#best-practices)
- [Windows 用 Docker デスクトップに関するフィードバック: ファイルの発行](https://github.com/docker/for-win/issues)
- [VS Code のブログ: 開発環境の選択に関するガイドライン](https://code.visualstudio.com/docs/containers/choosing-dev-environment#_guidelines-for-choosing-a-development-environment)
- [VS Code ブログ: WSL 2 での Docker の使用](https://code.visualstudio.com/blogs/2020/03/02/docker-in-wsl2)
- [VS Code ブログ: WSL 2 でのリモートコンテナーの使用](https://code.visualstudio.com/blogs/2020/07/01/containers-wsl)
- [前の selminutes ポッドキャスト: Simon の開発者にとって Docker の気持ちを作る](https://hanselminutes.com/736/making-docker-lovely-for-developers-with-simon-ferquel)
