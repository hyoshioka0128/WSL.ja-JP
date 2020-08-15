---
title: Windows Subsystem for Linux で VS Code の使用を開始する
description: Windows Subsystem for Linux を使用してコードを作成およびデバッグするための VS Code を設定する方法について説明します。
keywords: wsl、windows、windowssubsystem、gnu、linux、bash、vs code、remote extension、debug、path、visual studio
ms.date: 05/28/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: f5d7bd4f582f504ea3c4bd814454b1dc881ffed2
ms.sourcegitcommit: 97cc93f8e26391c09a31a4ab42c4b5e9d98d1c32
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86948656"
---
# <a name="get-started-using-visual-studio-code-with-windows-subsystem-for-linux"></a>Windows Subsystem for Linux で Visual Studio Code の使用を開始する

Visual Studio Code をリモート WSL 拡張機能と共に使用すると、WSL を完全な開発環境として VS Code から直接使用できます。 次のようにすることができます。

* Linux ベースの環境での開発
* Linux 固有のツールチェーンとユーティリティを使用する
* Outlook や Office などの生産性向上ツールへのアクセスを維持しながら、Windows の快適さを利用して Linux ベースのアプリケーションを実行およびデバッグする
* VS Code 組み込みターミナルを使用して、選択した Linux ディストリビューションを実行します。
* [Intellisense コード補完](https://code.visualstudio.com/docs/editor/intellisense) [、インライン処理、](https://code.visualstudio.com/docs/python/linting)[デバッグサポート](https://code.visualstudio.com/docs/nodejs/nodejs-debugging)、[コードスニペット](https://code.visualstudio.com/docs/editor/userdefinedsnippets)、[単体テスト](https://code.visualstudio.com/docs/python/testing)などの VS Code 機能を活用する
* VS Code の組み込みの[Git サポート](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)を使用して、バージョン管理を簡単に管理
* WSL プロジェクトでコマンドと拡張機能を直接実行する VS Code
* パスの問題、バイナリの互換性、またはその他の OS 間の課題を気にせずに、Linux またはマウントされた Windows ファイルシステム (/mnt/c など) のファイルを編集します。

## <a name="install-vs-code-and-the-remote-wsl-extension"></a>VS Code とリモート WSL 拡張機能をインストールする

* [VS Code インストールページ](https://code.visualstudio.com/download)にアクセスし、32または64ビットインストーラーを選択します。 (WSL ファイルシステムではなく) Windows に Visual Studio Code をインストールします。

* インストール中に**追加のタスクを選択**するように求めるメッセージが表示されたら、[**パスの追加**] オプションをオンにして、wsl 内のフォルダーをコードコマンドで簡単に開くことができるようにします。

* [リモート開発拡張機能パック](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)をインストールします。 この拡張パックには、リモート SSH およびリモートコンテナーの拡張機能に加えて、リモートの WSL 拡張機能が含まれており、コンテナー、リモートコンピューター、または WSL で任意のフォルダーを開くことができます。

> [!IMPORTANT]
> リモート WSL 拡張機能をインストールするには、VS Code の[1.35 リリース](https://code.visualstudio.com/updates/v1_35)バージョン以降が必要になります。 リモート WSL 拡張機能を使用せずに VS Code で WSL を使用することはお勧めしません。オートコンプリート、デバッグ、インライン処理などのサポートが失われるためです。楽しい事実: この WSL 拡張機能は $HOME/.vscode/extensions にインストールされます (PowerShell でコマンドを入力してください `ls $HOME\.vscode\extensions\` )。

## <a name="update-your-linux-distribution"></a>Linux ディストリビューションを更新する

一部の WSL Linux ディストリビューションでは、VS Code サーバーが起動するために必要なライブラリが不足しています。 パッケージマネージャーを使用して、Linux ディストリビューションに追加のライブラリを追加できます。

たとえば、Debian または Ubuntu を更新するには、次のように使用します。

```bash
sudo apt-get update
```

Wget (web サーバーからコンテンツを取得するため) および ca 証明書を追加するには (SSL ベースのアプリケーションが SSL 接続の信頼性を確認できるようにするため)、次のように入力します。

```bash
sudo apt-get install wget ca-certificates
```

## <a name="open-a-wsl-project-in-visual-studio-code"></a>Visual Studio Code で WSL プロジェクトを開く

### <a name="from-the-command-line"></a>コマンドラインから

WSL ディストリビューションからプロジェクトを開くには、ディストリビューションのコマンドラインを開き、次のように入力します。`code .`

![VS Code リモートサーバーで WSL プロジェクトを開く](../media/wsl-open-vs-code.gif)

### <a name="from-vs-code"></a>VS Code から

コマンドパレットを表示するには、ショートカット: VS Code を使用して、VS Code リモートオプションにアクセスすることもできます。 `CTRL+SHIFT+P` 入力すると、[ `VSCODE-REMOTE` VS Code のリモートオプションがすべて表示されます。これにより、リモートセッションでフォルダーを再度開き、開く配布を指定することができます。

![VS Code のコマンドパレット](../media/vscode-remote-command-palette.png)

## <a name="extensions-inside-of-vs-code-remote"></a>VS Code リモート内の拡張機能

リモート WSL 拡張機能は、VS Code を "クライアント/サーバー" アーキテクチャに分割します。このアーキテクチャでは、Windows コンピューター上で実行されているクライアント (ユーザーインターフェイス) と、リモートで実行されているサーバー (コード、Git、プラグインなど) が使用されます。

VS Code リモートで実行しているときに、[拡張機能] タブを選択すると、ローカルコンピューターと WSL 分散の間に分割された拡張機能の一覧が表示されます。

[テーマ](https://marketplace.visualstudio.com/search?target=VSCode&category=Themes&sortBy=Installs)などのローカル拡張機能のインストールは、1回だけインストールする必要があります。

[Python 拡張](https://marketplace.visualstudio.com/items?itemName=ms-python.python)機能などの一部の拡張機能や、lint デバッグなどを処理するものは、リモートの wsl ディストリビューションごとに個別にインストールする必要があります。 WSL リモートにインストールされていない拡張機能がローカルにインストールされている場合は、VS Code によって、警告アイコンと ⚠ 緑色の [wsl にインストール] ボタンが表示されます。

![リモート WSL 拡張機能とローカル拡張機能の VS Code](../media/vscode-remote-wsl-extensions.png)

詳細については、VS Code のドキュメントを参照してください。

* WSL で VS Code リモートが開始されると、シェルスタートアップスクリプトは実行されません。 追加のコマンドを実行する方法、または環境を変更する方法の詳細については、この[高度な環境セットアップスクリプト](https://code.visualstudio.com/docs/remote/wsl#_advanced-environment-setup-script)に関する記事を参照してください。

* WSL コマンドラインから VS Code を起動するときに問題が発生する場合は、 この[トラブルシューティングガイド](https://code.visualstudio.com/docs/remote/troubleshooting#_fixing-problems-with-the-code-command-not-working)には、パス変数の変更、依存関係の欠落に関する拡張機能のエラーの解決、Git 行の終了に関する問題の解決、リモートコンピューターへのローカル VSIX のインストール、ブラウザーウィンドウの起動、ブロック localhost ポート、web ソケットの起動、拡張データの格納エラーなどに関するヒントが記載されています。

## <a name="install-git-optional"></a>Git のインストール (省略可能)

共同作業で開発する場合や、(GitHub のような) オープンソース サイトでプロジェクトをホストする場合のために、VS Code では [Git によるバージョン管理](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)がサポートされています。 VS Code の [ソース管理] タブでは、すべての変更が追跡され、一般的な Git コマンド (追加、コミット、プッシュ、プル) が UI に組み込まれています。

Git をインストールするには、「[Windows Subsystem For Linux で動作するように Git を設定する](./wsl-git.md)」を参照してください。

## <a name="install-windows-terminal-optional"></a>Windows ターミナルをインストールする (省略可能)

新しい Windows ターミナルでは、複数のタブが有効になり (コマンドプロンプト、PowerShell、または複数の Linux ディストリビューションをすばやく切り替えることができます)、カスタムキーバインド (タブを開いたり閉じたりするための独自のショートカットキーを作成する、コピーと貼り付けなど)、絵文字☺、カスタムテーマ (配色、フォントスタイルとサイズ、背景画像、 詳細については、 [Windows ターミナルのドキュメント](https://docs.microsoft.com/windows/terminal)を参照してください。

1. [Microsoft Store で Windows ターミナル](https://www.microsoft.com/store/apps/9n0dx20hk701)を取得します: ストアを介してインストールすると、更新プログラムが自動的に処理されます。

2. インストールが完了したら、Windows ターミナルを開き、 **[設定]** を選択して、`profile.json` ファイルによってターミナルをカスタマイズします。

## <a name="additional-resources"></a>その他の情報

* [リモート開発の VS Code](https://code.visualstudio.com/docs/remote/remote-overview)
* [リモート開発のヒントとテクニック](https://code.visualstudio.com/docs/remote/troubleshooting)
* [WSL を使用したリモート開発のチュートリアル](https://code.visualstudio.com/remote-tutorials/wsl/getting-started)
* [WSL 2 および VS Code での Docker の使用](https://code.visualstudio.com/blogs/2020/03/02/docker-in-wsl2)
* [VS Code での C++ と WSL の使用](https://code.visualstudio.com/docs/cpp/config-wsl)
* [Linux 用のリモート R サービス](https://docs.microsoft.com/visualstudio/rtvs/setting-up-remote-r-service-on-linux?view=vs-2017)

他にも検討をお勧めする拡張機能として、次のようなものがあります。

* [他のエディターからのキーマップ](https://marketplace.visualstudio.com/search?target=VSCode&category=Keymaps&sortBy=Downloads): これらの拡張機能は、別のテキスト エディター (Atom、Sublime、Vim、eMacs、Notepad++ など) から移行する場合に、ご利用の環境を快適に保つのに役立ちます。
* [設定の同期](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync): GitHub を使用して、異なるインストール間で VS Code の設定を同期させることができます。 複数のコンピューターで作業する場合、この機能によってコンピューター間で環境の一貫性を保つことができます。
* [Chrome のデバッガー](https://code.visualstudio.com/blogs/2016/02/23/introducing-chrome-debugger-for-vs-code): Linux でサーバー側で開発を完了したら、クライアント側を開発してテストする必要があります。 この拡張機能により、ご利用の VS Code エディターと Chrome ブラウザーのデバッグ サービスが統合され、効率がより向上します。
