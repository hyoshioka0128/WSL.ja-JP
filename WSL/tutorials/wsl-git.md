---
title: WSL で Git の使用を開始する
description: Windows Subsystem for Linux でバージョン管理用の Git を設定する方法について説明します。
keywords: wsl、windows、windowssubsystem、gnu、linux、bash、git、github、バージョン管理
ms.date: 06/04/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 1e8a856e35682571d37ad57db39cec257ad22c56
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493624"
---
# <a name="get-started-using-git-on-windows-subsystem-for-linux"></a>Windows Subsystem for Linux で Git の使用を開始する

Git は、最も一般的に使用されるバージョン管理システムです。 Git を使用すると、ファイルに加えた変更を追跡できるため、実行された内容を記録し、必要に応じて、以前のバージョンのファイルに戻すことができます。 また、Git を使用するとコラボレーションが容易になり、複数の人が変更を1つのソースにマージできるようになります。

## <a name="git-can-be-installed-on-windows-and-on-wsl"></a>Git は、Windows および WSL にインストールできます。

重要な考慮事項: WSL を有効にして Linux ディストリビューションをインストールする場合は、Windows NTFS C:\ から分離した新しいファイルシステムをインストールします。コンピューター上のドライブ。 Linux では、ドライブに文字が指定されていません。 これらにはマウントポイントが指定されています。 ファイルシステムのルートは、 `/` ルートパーティションのマウントポイント、または WSL の場合はフォルダーです。 すべてが同じドライブであるとは限りません `/` 。 たとえば、ラップトップには、2つのバージョンの Ubuntu (20.04 と 18.04) と Debian がインストールされています。 これらの配布を開いた場合は、コマンドを使用してホームディレクトリを選択 `cd ~` し、コマンドを入力すると、 `explorer.exe .` Windows ファイルエクスプローラーが開き、その配布のディレクトリパスが表示されます。

| Linux ディストリビューション | ホームフォルダーにアクセスするための Windows パス |
| ----------- | ----------- |
| Ubuntu 20.04 | `\\wsl$\Ubuntu-20.04\home\username` |
| Ubuntu 18.04 | `\\wsl$\Ubuntu-18.04\home\username` |
| Debian | `\\wsl$\Debian\home\username` |
| Windows PowerShell | `C:\Users\username` |

> [!TIP]
> ではなく、WSL ディストリビューションコマンドラインから Windows ファイルディレクトリにアクセスしようとすると、を `C:\Users\username` 使用してディレクトリにアクセスし `/mnt/c/Users/username` ます。 Linux ディストリビューションでは、windows ファイルシステムがマウントされたドライブとして表示されるためです。

使用する予定の各ファイルシステムに Git をインストールする必要があります。

![ディストリビューションによる Git バージョンの表示](../media/git-versions.gif)

## <a name="installing-git"></a>Installing Git (Git のインストール) (Git のインストール)

Git は、ほとんどの Windows Subsystem for Linux ディストリビューションで既にインストールされていますが、最新バージョンに更新することもできます。 また、git 構成ファイルを設定する必要があります。

Git をインストールするには、 [Linux サイト用の Git ダウンロードに関する](https://git-scm.com/download/linux) ページを参照してください。 各 Linux ディストリビューションには、独自のパッケージマネージャーとインストールコマンドがあります。

Ubuntu/Debian の最新の安定した Git バージョンについては、次のコマンドを入力します。

```bash
sudo apt-get install git
```

> [!NOTE]
> また、 [Git For Windows](https://git-scm.com/download/win) をまだインストールしていない場合にもインストールすることができます。

## <a name="git-config-file-setup"></a>Git 構成ファイルのセットアップ

Git 構成ファイルを設定するには、作業中のディストリビューションのコマンドラインを開き、次のコマンドで名前を設定します ("your Name" を Git ユーザー名に置き換えます)。

```bash
git config --global user.name "Your Name"
```

次のコマンドを使用して電子メールを設定します (" youremail@domain.com " は、Git アカウントで使用する電子メールに置き換えてください)。

```bash
git config --global user.email "youremail@domain.com"
```

> [!TIP]
> まだ Git アカウントを持っていない場合は、[GitHub でそれにサインアップ](https://github.com/join)することができます。 以前に Git を使用したことがない場合、入門用の [GitHub ガイド](https://guides.github.com/)が役に立ちます。 git 構成を編集する必要がある場合は、nano のような組み込みのテキスト エディターを使用してそれを行うことができます: `nano ~/.gitconfig`

[2 要素認証 (2FA) を使用](https://help.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)してアカウントをセキュリティで保護することをお勧めします。

## <a name="git-credential-manager-setup"></a>Git Credential Manager のセットアップ

Git Credential Manager を使用すると、リモート Git サーバーを認証することができます。これには、2要素認証のような複雑な認証パターン、Azure Active Directory、またはすべての git プッシュに SSH キーパスワードを必要とする SSH リモート Url の使用などがあります。 Git Credential Manager は、GitHub などのサービスの認証フローに統合されています。ユーザーがホスティング プロバイダーに対して認証されると、新しい認証トークンが要求されます。 その後、トークンを [Windows 資格情報マネージャー](https://support.microsoft.com/help/4026814/windows-accessing-credential-manager)に安全に格納します。 2 回目以降は、Git を使用してホスティング プロバイダーと通信することができ、再認証は必要ありません。 Windows 資格情報マネージャーにあるトークンへのアクセスだけが行われることになります。

WSL ディストリビューションで使用するように Git Credential Manager をセットアップするには、ディストリビューションを開き、次のコマンドを入力します。

```Bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe"
```

これで、WSL ディストリビューション内で実行するすべての Git 操作で、資格情報マネージャーが使用されるようになります。 ホスト用に既にキャッシュされている資格情報がある場合は、それらへのアクセスが資格情報マネージャーから行われます。 そうでない場合は、Linux コンソールを使用しているとしても、資格情報を要求するダイアログ応答が表示されます。

> [!NOTE]
> コード署名セキュリティに GPG キーを使用している場合は、 [GPG キーを GitHub の電子メールに関連付ける](https://help.github.com/en/github/authenticating-to-github/associating-an-email-with-your-gpg-key)必要があります。

## <a name="adding-a-git-ignore-file"></a>Git Ignore ファイルの追加

プロジェクトには、ファイルを追加することをお勧め [します](https://help.github.com/en/articles/ignoring-files) 。 GitHub では、使用事例に従って整理されたファイル設定を使用して [、便利なテンプレートのコレクションを](https://github.com/github/gitignore) 提供しています。 たとえば、 [Node.js プロジェクトの GitHub の既定の gitemplate テンプレート](https://github.com/github/gitignore/blob/master/Node.gitignore)は次のようになります。

[Github web サイトを使用して新しいリポジトリを作成](https://help.github.com/articles/create-a-repo)することを選択した場合は、README ファイルを使用してリポジトリを初期化するためのチェックボックスがあります。特定のプロジェクトの種類に対してファイルがセットアップされ、必要に応じてライセンスを追加するためのオプションがあります。

## <a name="git-and-vs-code"></a>Git と VS Code

Visual Studio Code には、Git のサポートが組み込まれています。これには、変更内容を表示し、さまざまな git コマンドを処理するソース管理タブが含まれます。 [VS Code の Git サポートの](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)詳細については、こちらをご覧ください。

## <a name="git-line-endings"></a>Git の行の終わり

Windows、WSL、またはコンテナー間で同じリポジトリフォルダーを使用している場合は、一貫性のある行の終わりを設定してください。

Windows と Linux では異なる既定の行の終わりが使用されるため、Git では、変更されたファイルのうち、行の終わりとは異なるものが多数報告される場合があります。 これが行われないようにするには、ファイルを使用する `.gitattributes` か、Windows 側でグローバルに行の終了変換を無効にします。 Git の [行の終了問題の解決について](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-containers-resulting-in-many-modified-files)は、この VS Code のドキュメントを参照してください。

## <a name="additional-resources"></a>その他のリソース

* [WSL & VS Code](./wsl-vscode.md)
* [GitHub の学習ラボ: オンラインコース](https://lab.github.com/)
* [Git 視覚化ツール](http://git-school.github.io/visualizing-git/)
* [Git ツール-資格情報の保存](https://git-scm.com/book/it/v2/Git-Tools-Credential-Storage)
