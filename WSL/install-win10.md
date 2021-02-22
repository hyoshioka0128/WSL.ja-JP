---
title: Windows Subsystem for Linux (WSL) を Windows 10 にインストールする
description: Windows 10 への WSL のインストール ガイド。Bash ターミナルを使用し、Ubuntu、Debian、SUSE、Kali、Fedora、Pengwin、Alpine などを含みます。
keywords: BashOnWindows, bash, wsl, windows, linux 用 windows サブシステム, windowssubsystem, ubuntu, debian, suse, windows 10, インストール, 有効にする, WSL2, バージョン 2
ms.date: 09/15/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 58375484d57e7cb65a807e7156a5dcdf166dac2e
ms.sourcegitcommit: 17d5ea1fe571274c224202544f61035971d6e0e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2021
ms.locfileid: "100551029"
---
# <a name="windows-subsystem-for-linux-installation-guide-for-windows-10"></a>Windows 10 用 Windows Subsystem for Linux のインストール ガイド

Linux 用 Windows サブシステム (WSL) をインストールするには、次の 2 つのオプションを使用できます。

- **[簡略化されたインストール](#simplified-installation-for-windows-insiders)** " *(プレビュー リリース)* ": `wsl --install`

    簡略化されたインストール コマンド `wsl --install` を使用するには、[Windows Insider Program](https://insider.windows.com/getting-started) に参加し、Windows 10 のプレビュー ビルド(OS ビルド 20262 以降) をインストールする必要がありますが、手動インストールの手順に従う必要がなくなります。 必要な操作は、管理者特権でコマンド ウィンドウを開いて `wsl --install` を実行するだけです。再起動後、WSL を使用する準備が整います。

- **[手動インストール](#manual-installation-steps)** :以下に示す 6 つの手順に従います。

    WSL の手動インストール手順を以下に示します。これを使用して、任意のバージョンの Windows 10 に Linux をインストールできます。

> [!NOTE]
> インストール プロセス中に問題が発生した場合は、このページの下部にある「[インストールのトラブルシューティング](#troubleshooting-installation)」セクションを確認してください。

## <a name="simplified-installation-for-windows-insiders"></a>Windows Insider 用の簡略化されたインストール

Linux 用 Windows サブシステムのインストール プロセスは、最新の Windows Insider の Windows 10 プレビュー ビルドで大幅に改善され、以下の手動の手順が 1 つのコマンドに置き換えられています。

簡略化されたインストール コマンド `wsl --install` を使用するには、以下を行う必要があります。

- [Windows Insider Program](https://insider.windows.com/getting-started) に参加する
- Windows 10 のプレビュー ビルド (OS ビルド 20262 以降) をインストールする。
- 管理者特権でコマンド ライン ウィンドウを開く

これらの要件を満たしたら、次のように WSL をインストールします。

- 管理者モードで開いたコマンド ラインに次のコマンドを入力します: `wsl.exe --install`
- マシンを再起動します

新しくインストールした Linux ディストリビューションを初めて起動すると、コンソール ウィンドウが開き、ファイルが圧縮解除されて PC 上に保存されるまで待機するように求められます。 今後のすべての起動には、1 秒もかかりません。

次に、[新しい Linux ディストリビューションのユーザー アカウントとパスワードを作成する](./user-support.md)必要があります。

**お疲れさまでした。これで、Windows オペレーティング システムと完全に統合された Linux ディストリビューションのインストールと設定が正常に完了しました。**

--install コマンドでは、次のアクションが実行されます。

- オプションの WSL および仮想マシン プラットフォームのコンポーネントを有効にする
- 最新の Linux カーネルをダウンロードしてインストールする
- WSL 2 を既定値として設定する
- Linux ディストリビューションをダウンロードしてインストールする " *(再起動が必要になる場合があります)* "

既定では、インストールされる Linux ディストリビューションは Ubuntu になります。 これは `wsl --install -d <Distribution Name>` を使用して変更できます。 " *(`<Distribution Name>` を目的のディストリビューションの名前に置き換えます。)* "`wsl --install -d <Distribution Name>` コマンドを使用して、最初のインストール後に追加の Linux ディストリビューションをマシンに追加することができます。

使用可能な Linux ディストリビューションの一覧を表示するには、「`wsl --list --online`」と入力します。

## <a name="manual-installation-steps"></a>手動インストールの手順

Windows Insider ビルドを使用していない場合は、以下の手順に従って、WSL に必要な機能を手動で有効にする必要があります。

## <a name="step-1---enable-the-windows-subsystem-for-linux"></a>手順 1 - Linux 用 Windows サブシステムを有効にする

Windows 上に Linux ディストリビューションをインストールする前に、まず "Linux 用 Windows サブシステム" オプション機能を有効にする必要があります。

管理者として PowerShell を開き、以下を実行します。

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

ここで、手順 2 に進み、WSL 2 に更新することをお勧めしますが、WSL 1 のみをインストールする場合は、マシンを **再起動** して、「[手順 6 - 選択した Linux ディストリビューションをインストールする](./install-win10.md#step-6---install-your-linux-distribution-of-choice)」に進むことができます。 WSL 2 に更新するには、マシンの **再起動を待ってから**、次の手順に進みます。

## <a name="step-2---check-requirements-for-running-wsl-2"></a>手順 2 - WSL 2 の実行に関する要件を確認する

WSL 2 に更新するには、Windows 10 を実行している必要があります。

- x64 システムの場合:**バージョン 1903** 以降、**ビルド 18362** 以上。
- ARM64 システムの場合:**バージョン 2004** 以降、**ビルド 19041** 以上。
- 18362 より前のビルドは WSL 2 をサポートしていません。 [Windows 更新アシスタント](https://www.microsoft.com/software-download/windows10)を使用して、お使いのバージョンの Windows を更新します。

バージョンとビルド番号を確認するには、**Windows ロゴ キー + R キー** を押して、「**winver**」と入力し、 **[OK]** を選択します。 (または、Windows コマンド プロンプトで `ver` コマンドを入力します)。 [設定] メニューで、[最新の Windows バージョンに更新](ms-settings:windowsupdate)します。

> [!NOTE]
> Windows 10 バージョン 1903 または 1909 を実行している場合は、Windows メニューから [設定] を開き、[更新とセキュリティ] に移動して、[更新プログラムのチェック] を選択します。 ビルド番号は、18362.1049+ または 18363.1049+ で、マイナー ビルド番号は .1049 より大きい必要があります。 詳細については、「[Windows 10 バージョン 1903 および 1909 で WSL 2 のサポート開始](https://devblogs.microsoft.com/commandline/wsl-2-support-is-coming-to-windows-10-versions-1903-and-1909/)」を参照してください。 また、[トラブルシューティング手順](./troubleshooting.md#im-on-windows-10-version-1903-and-i-still-do-not-see-options-for-wsl-2)も参照してください。

## <a name="step-3---enable-virtual-machine-feature"></a>手順 3: 仮想マシンの機能を有効にする

WSL 2 をインストールする前に、"**仮想マシン プラットフォーム**" オプション機能を有効にする必要があります。 この機能を使用するには、コンピューターに[仮想化機能](https://docs.microsoft.com/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed)が必要です。

管理者として PowerShell を開き、以下を実行します。

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

お使いのマシンを **再起動** して WSL のインストールを完了し、WSL 2 に更新します。

## <a name="step-4---download-the-linux-kernel-update-package"></a>手順 4 - Linux カーネル更新プログラム パッケージをダウンロードする

1. 最新のパッケージをダウンロードします。
    - [x64 マシン用 WSL2 Linux カーネル更新プログラム パッケージ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

    > [!NOTE]
    > ARM64 マシンを使用している場合は、代わりに [ARM64 パッケージ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)をダウンロードしてください。 使用しているマシンの種類がわからない場合は、コマンド プロンプトまたは PowerShell を開き、「`systeminfo | find "System Type"`」と入力します。

2. 前の手順でダウンロードした更新プログラム パッケージを実行します。 (ダブルクリックして実行します。管理者特権のアクセス許可を求めるメッセージが表示されます。[はい] を選択して、このインストールを承認します。)

インストールが完了したら、次の手順に進み、新しい Linux ディストリビューションをインストールする際の既定のバージョンとして WSL 2 を設定します。 (新しい Linux インストールを WSL 1 に設定する場合は、この手順をスキップしてください)。

> [!NOTE]
> 詳細については、[Windows コマンドラインのブログ](https://aka.ms/cliblog)にある[WSL2 Linux カーネルの更新プログラムに対する変更](https://devblogs.microsoft.com/commandline/wsl2-will-be-generally-available-in-windows-10-version-2004)に関するページを参照してください。

## <a name="step-5---set-wsl-2-as-your-default-version"></a>手順 5 - WSL 2 を既定のバージョンとして設定する

PowerShell を開いて次のコマンドを実行し、新しい Linux ディストリビューションをインストールする際の既定のバージョンとして WSL 2 を設定します。

```powershell
wsl --set-default-version 2
```

## <a name="step-6---install-your-linux-distribution-of-choice"></a>手順 6 - 選択した Linux ディストリビューションをインストールする

1. [Microsoft Store](https://aka.ms/wslstore) を開き、希望する Linux ディストリビューションを選択します。

    ![Microsoft Store での Linux ディストリビューションの表示](media/store.png)

    次のリンクを使用すると、各ディストリビューションの Microsoft Store ページが開きます。

    - [Ubuntu 16.04 LTS](https://www.microsoft.com/store/apps/9pjn388hp8c9)
    - [Ubuntu 18.04 LTS](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
    - [Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)
    - [openSUSE Leap 15.1](https://www.microsoft.com/store/apps/9NJFZK00FGKV)
    - [SUSE Linux Enterprise Server 12 SP5](https://www.microsoft.com/store/apps/9MZ3D1TRP8T1)
    - [SUSE Linux Enterprise Server 15 SP1](https://www.microsoft.com/store/apps/9PN498VPMF3Z)
    - [Kali Linux](https://www.microsoft.com/store/apps/9PKR34TNCV07)
    - [Debian GNU/Linux](https://www.microsoft.com/store/apps/9MSVKQC78PK6)
    - [WSL のための Fedora リミックス](https://www.microsoft.com/store/apps/9n6gdm4k2hnc)
    - [Pengwin](https://www.microsoft.com/store/apps/9NV1GV1PXZ6P)
    - [Pengwin Enterprise](https://www.microsoft.com/store/apps/9N8LP0X93VCP)
    - [Alpine WSL](https://www.microsoft.com/store/apps/9p804crf0395)

2. ディストリビューションのページで、[入手] を選択します。

    ![Microsoft Store での Linux ディストリビューション](media/UbuntuStore.png)

新しくインストールした Linux ディストリビューションを初めて起動すると、コンソール ウィンドウが開き、ファイルが圧縮解除されて PC に格納されるまで 1、2 分待つように求められます。 今後のすべての起動には、1 秒もかかりません。

次に、[新しい Linux ディストリビューションのユーザー アカウントとパスワードを作成する](./user-support.md)必要があります。

![Windows コンソールでの Ubuntu の展開](media/UbuntuInstall.png)

**お疲れさまでした。これで、Windows オペレーティング システムと完全に統合された Linux ディストリビューションのインストールと設定が正常に完了しました。**

## <a name="install-windows-terminal-optional"></a>Windows ターミナルをインストールする (省略可能)

Windows ターミナルでは、複数のタブ (複数の Linux コマンド ライン、Windows コマンド プロンプト、PowerShell、Azure CLI などをすばやく切り替える) が有効になり、カスタム キー バインド (タブを開くまたは閉じる、コピーと貼り付けを行うなどのためのショートカット キー) を作成でき、検索機能、カスタム テーマ (配色、フォント スタイルとサイズ、背景画像、ぼかし、透明度) を使用できます。 [詳細情報。](/windows/terminal)

[Windows ターミナルをインストール](/windows/terminal/get-started)します。

  ![Windows ターミナル](media/terminal.png)

## <a name="set-your-distribution-version-to-wsl-1-or-wsl-2"></a>ディストリビューションのバージョンを WSL 1 または WSL 2 に設定する

インストールされている各 Linux ディストリビューションに割り当てられている WSL バージョンを確認するには、PowerShell コマンド ラインを開き、次のコマンドを入力します ([Windows ビルド 18362 以上](ms-settings:windowsupdate)でのみ使用可能): `wsl -l -v`

```powershell
wsl --list --verbose
```

ディストリビューションで使用される WSL のバージョンを設定するには、以下を実行します。

```powershell
wsl --set-version <distribution name> <versionNumber>
```

`<distribution name>` は、お使いのディストリビューションの実際の名前に必ず置き換えてください。`<versionNumber>` は、数字の "1" または "2" に置き換えてください。 上記と同じコマンドで "2" を "1" に置き換えて実行することにより、いつでも WSL 1 に戻すことができます。

> [!NOTE]
> 対象のディストリビューションのサイズによっては、WSL 1 から WSL 2 への更新が完了するまでに数分かかる場合があります。 Windows 10 Anniversary Update または Creators Update から WSL 1 の古い (レガシ) インストールを実行している場合は、更新エラーが発生することがあります。 次の手順に従って、[レガシ ディストリビューションをアンインストールして削除](./install-legacy.md#uninstallingremoving-the-legacy-distro)します。
>
> `wsl --set-default-version` の結果が無効なコマンドである場合は、「`wsl --help`」と入力してください。 `--set-default-version` が表示されない場合は、お使いの OS によってサポートされていないことを意味しているため、バージョン 1903、ビルド 18362 以上に更新する必要があります。
>
> コマンドの実行後に、次のメッセージが表示される場合: `WSL 2 requires an update to its kernel component. For information please visit https://aka.ms/wsl2kernel`。 さらに MSI Linux カーネル更新パッケージをインストールする必要があります。

また、WSL 2 を既定のアーキテクチャにする場合は、次のコマンドを使用して実行できます。

```powershell
wsl --set-default-version 2
```

これにより、インストールされるすべての新しいディストリビューションのバージョンが WSL 2 に設定されます。

## <a name="troubleshooting-installation"></a>インストールのトラブルシューティング

関連エラーと推奨される修正を次に示します。 その他の一般的なエラーとその解決策については、[WSL のトラブルシューティングのページ](troubleshooting.md)を参照してください。

- **エラー 0x80070003 が発生してインストールに失敗しました**
  - Windows Subsystem for Linux はシステム ドライブ (通常、これは `C:` ドライブ) でのみ実行されます。 ディストリビューションがシステム ドライブに格納されていることを確認します。  
  - **[設定]** -> ** システム --> **[記憶域]** -> **その他のストレージ設定: [新しいコンテンツの保存先を変更する]** 
    を開きます。![C: ドライブにアプリをインストールするためのシステム設定の画像](media/AppStorage.png)

- **WslRegisterDistribution failed with error 0x8007019e (エラー0x8007019e で WslRegisterDistribution が失敗しました)**
  - Windows Subsystem for Linux オプション コンポーネントが有効になっていません。
  - **[コントロール パネル]**  ->  **[プログラムと機能]**  ->  **[Windows の機能の有効化または無効化]** を開いて、 **[Linux 用 Windows サブシステム]** をチェックするか、またはこの記事の冒頭に記載した PowerShell コマンドレットを使用してください。

- **インストールがエラー 0x80070003 またはエラー 0x80370102 で失敗した**
  - コンピューターの BIOS 内部で仮想化が有効になっていることを確認してください。 これを行う方法の手順は、コンピューターによって異なりますが、最も可能性が高いのは CPU 関連のオプションの下です。

- **アップグレードしようとしたときに次のエラーが発生する: `Invalid command line option: wsl --set-version Ubuntu 2`**
  - Linux 用 Windows サブシステムが有効になっていること、および Windows ビルド バージョン 18362 以上を使用していることをご確認ください。 WSL を有効にするには、PowerShell プロンプトで管理者特権を使用してこのコマンドを実行します: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`。

- **仮想ディスク システムの制限があるため、要求された操作を完了できませんでした。仮想ハード ディスク ファイルは、圧縮と暗号化が解除されている必要があります。また、スパースにすることはできません。**
  - [内容を圧縮] ([内容を暗号化] のチェックボックスがオンになっている場合はこれも) を選択解除するため、Linux ディストリビューションのプロファイル フォルダーを開きます。 これは、Windows ファイル システムのフォルダーにあります (例: `USERPROFILE%\AppData\Local\Packages\CanonicalGroupLimited...`)。
  - この Linux ディストリビューション プロファイル内に、LocalState フォルダーが存在します。 このフォルダーを右クリックして、オプションのメニューを表示します。 [プロパティ] > [詳細設定] の順に選択し、[内容を圧縮してディスク領域を節約する] および [内容を暗号化してデータをセキュリティで保護する] チェックボックスを確実にオフにします。 これを現在のフォルダーのみに適用するか、すべてのサブフォルダーとファイルに適用するかを確認するメッセージが表示された場合は、圧縮フラグをオフにしようとしているだけなので、[このフォルダーのみ] を選択します。 この操作を実行すると、`wsl --set-version` コマンドが機能するようになります。

![WSL ディストリビューションのプロパティ設定のスクリーンショット](media/troubleshooting-virtualdisk-compress.png)

> [!NOTE]
> この例では、Ubuntu 18.04 ディストリビューションの LocalState フォルダーの場所は次のとおりです。C:\Users\<my-user-name>\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu18.04onWindows_79rhkp1fndgsc
>
> この問題の最新情報が追跡されている [WSL ドキュメント GitHub スレッド #4103](https://github.com/microsoft/WSL/issues/4103) をご確認ください。

- **"wsl" という用語が、コマンドレット、関数、スクリプト ファイル、または操作可能なプログラムの名前として認識されません。**
  - [Linux 用 Windows サブシステムのオプション コンポーネントがインストールされている](./install-win10.md#step-3---enable-virtual-machine-feature)ことを確認してください。 また、ARM64 デバイスを使用し、PowerShell からこのコマンドを実行している場合も、このエラーを受け取ります。 代わりに、`wsl.exe`PowerShell Core[ またはコマンド プロンプトから ](/powershell/scripting/install/installing-powershell-core-on-windows) を実行します。

- **Error:この更新プログラムは、Linux 用 Windows サブシステムを搭載したマシンにのみ適用されます。**
  - Linux カーネル更新プログラム MSI パッケージをインストールするには、WSL が必要であり、最初に有効にする必要があります。 失敗した場合は、"`This update only applies to machines with the Windows Subsystem for Linux`" というメッセージが表示されます。
  - このメッセージが表示される理由として、次の 3 つが考えられます。

  1. WSL 2 をサポートしていない古いバージョンの Windows を使用しています。 バージョン要件と更新プログラムへのリンクについては、手順 2 を参照してください。

  2. WSL が有効になっていません。 手順 1 に戻り、お使いのマシンでオプションの WSL 機能が有効になっていることを確認する必要があります。

  3. WSL を有効にした後、再起動しないと、効力が発しません。マシンを再起動してから、もう一度お試しください。

- **Error:WSL 2 のカーネル コンポーネントを更新する必要があります。詳細については、 https://aka.ms/wsl2kernel をアクセスしてください。**
  - Linux カーネル パッケージが %SystemRoot%\system32\lxss\tools フォルダーにない場合、このエラーが発生します。 このインストール手順の手順 4 に従って Linux カーネル更新プログラム MSI パッケージをインストールすることにより、このエラーを解決できます。 [[プログラムの追加と削除]](ms-settings:appsfeatures-app) から MSI をアンインストールして、インストールし直すことが必要な場合があります。
