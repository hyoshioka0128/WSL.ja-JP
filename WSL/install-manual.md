---
title: Linux 用 Windows サブシステム (WSL) ディストリビューションを手動でダウンロードする
description: Linux 用 Windows サブシステム ディストリビューションを手動でダウンロードする方法について説明します。
keywords: wsl, linux 用 windows subsystem, 手動インストール, 手動でインストール, microsoft ストア, windows 10, curl, Add-AppxPackage, 長期的なサービス, LTSC
ms.date: 05/28/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: d948ce9d304314bdd15b98136b8a99ca35723139
ms.sourcegitcommit: e67eb4aedff57a304188ca3360aba25605f8bdb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746278"
---
# <a name="manually-download-windows-subsystem-for-linux-distro-packages"></a>Linux 用 Windows サブシステム ディストリビューション パッケージを手動でダウンロードする

Microsoft Store 経由で WSL Linux ディストリビューションをインストールすることができない (または必要ない) シナリオがいくつかあります。 具体的には、Microsoft Store をサポートしていない Windows サーバーまたは長期的なサービス (LTSC) デスクトップ OS SKU を実行している場合や、企業ネットワーク ポリシーや管理者が環境で Microsoft Store の使用を許可していない場合があります。

このような場合、WSL 自体は使用できても、ストアにアクセスできない場合に、WSL に Linux ディストリビューションをダウンロードしてインストールするにはどうすればよいでしょうか。

> 注: **Cmd、PowerShell、Linux および WSL ディストリビューションなどのコマンドライン シェル環境は、Windows 10 S モード上の実行が許可されていません**。 この制限は、S モードで提供される整合性と安全性の目標を確保するために存在します。詳細については、[この投稿](https://blogs.msdn.microsoft.com/commandline/2017/05/18/will-linux-distros-run-on-windows-10-s/)を参照してください。

## <a name="downloading-distros"></a>ディストリビューションのダウンロード

Microsoft Store アプリを使用できない場合は、以下のリンクをクリックして Linux ディストリビューションをダウンロードして手動でインストールできます。
* [Ubuntu 20.04](https://aka.ms/wslubuntu2004)
* [Ubuntu 20.04 ARM](https://aka.ms/wslubuntu2004arm)
* [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
* [Ubuntu 18.04 ARM](https://aka.ms/wsl-ubuntu-1804-arm)
* [Ubuntu 16.04](https://aka.ms/wsl-ubuntu-1604)
* [Debian GNU/Linux](https://aka.ms/wsl-debian-gnulinux)
* [Kali Linux](https://aka.ms/wsl-kali-linux-new)
* [OpenSUSE Leap 42](https://aka.ms/wsl-opensuse-42)
* [SUSE Linux Enterprise Server 12](https://aka.ms/wsl-sles-12)
* [WSL のための Fedora リミックス](https://github.com/WhitewaterFoundry/WSLFedoraRemix/releases/)

これにより、選択したフォルダーに `<distro>.appx` パッケージがダウンロードされます。 [インストール手順](#installing-your-distro)に従って、ダウンロードしたディストリビューションをインストールします。

## <a name="downloading-distros-via-the-command-line"></a>コマンド ラインからのディストリビューションのダウンロード
必要に応じて、コマンド ラインから好みのディストリビューションをダウンロードすることもできます。

 ### <a name="download-using-powershell"></a>PowerShell を使用してダウンロードする
 PowerShell を使用してディストリビューションをダウンロードするには、[Invoke-WebRequest](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-5.1) コマンドレットを使用します。 Ubuntu 16.04 をダウンロードする手順の例を次に示します。

```powershell
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile Ubuntu.appx -UseBasicParsing
```

> [!TIP]
> ダウンロードに時間がかかる場合は、`$ProgressPreference = 'SilentlyContinue'` を設定して進行状況バーをオフにします

### <a name="download-using-curl"></a>curl を使用してダウンロードする
Windows 10 Spring 2018 Update (またはそれ以降) には、コマンド ラインから Web 要求 (HTTP GET、POST、PUT などのコマンド) を呼び出すことができる一般的な [curl コマンドライン ユーティリティ](https://curl.haxx.se/)が含まれています。 `curl.exe` を使用して、上記のディストリビューションをダウンロードできます。

```console
curl.exe -L -o ubuntu-1604.appx https://aka.ms/wsl-ubuntu-1604
```

上記の例では、(`curl` だけでなく) `curl.exe` が実行され、PowerShell では、[Invoke-WebRequest](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-6) の PowerShell curl エイリアスではなく、実際の curl 実行可能ファイルが呼び出されます。

> 注: Cmd シェルや `.bat` / `.cmd` スクリプトを使用してダウンロード手順を呼び出したりスクリプトで実行したりする必要がある場合は、`curl` を使用することをお勧めします。

## <a name="installing-your-distro"></a>ディストリビューションのインストール
Windows 10 を使用している場合、PowerShell を使用してディストリビューションをインストールできます。 上記の手順でダウンロードしたディストリビューションを含むフォルダーに移動して、そのディレクトリで次のコマンドを実行します。この `app_name` は、ディストリビューションの .appx ファイルの名前です。  
```Powershell
Add-AppxPackage .\app_name.appx
```

Windows サーバーを使用している場合、インストール手順については、[Windows Server](install-on-server.md) のドキュメント ページを参照してください。

ディストリビューションがインストールされたら、通常の手順に従って [WSL 2 に更新](./install-win10.md#update-to-wsl-2)するか、[新しいユーザー アカウントとパスワードを作成](./user-support.md)します。
