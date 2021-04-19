---
title: Windows Server に Linux サブシステムをインストールする
description: Windows Server に Linux サブシステムをインストールする方法について説明します。 WSL は、Windows Server 2019 (バージョン 1709) 以降にインストールできます。
keywords: BashOnWindows, bash, wsl, windows, Linux 用 Windows サブシステム, windowssubsystem, ubuntu, windows server
ms.date: 05/12/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 5b20efbb58e35922cd783c4c192d02c7f3658aaf
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493514"
---
# <a name="windows-server-installation-guide"></a>Windows Server インストール ガイド

Linux 用 Windows サブシステムは、Windows Server 2019 (バージョン 1709) 以降にインストールできます。 このガイドでは、お使いのマシンで WSL を有効にする手順について説明します。

## <a name="enable-the-windows-subsystem-for-linux"></a>Linux 用 Windows サブシステムを有効にする

Windows 上で Linux ディストリビューションを実行する前に、"Linux 用 Windows サブシステム" オプション機能を有効にして再起動する必要があります。

管理者として PowerShell を開き、以下を実行します。

```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

```

## <a name="download-a-linux-distribution"></a>Linux ディストリビューションをダウンロードする

[これらの手順](install-manual.md)に従って、お気に入りの Linux ディストリビューションをダウンロードします。

## <a name="extract-and-install-a-linux-distribution"></a>Linux ディストリビューションを展開してインストールする

Linux ディストリビューションをダウンロードしたら、その内容を展開して手動でインストールするために、次の手順に従います。

1. PowerShell を使用して、`<distro>.appx` パッケージの内容を展開します。

    ```powershell
    Rename-Item .\Ubuntu.appx .\Ubuntu.zip
    Expand-Archive .\Ubuntu.zip .\Ubuntu
    ```

2. ターゲット フォルダーでディストリビューション ランチャー アプリケーションを実行します。 ランチャーには、通常、`<distro>.exe` という名前が付けられます (たとえば、`ubuntu.exe`)。

    ![Windows Server 上の展開された Ubuntu ディストリビューション](media/server-appx-expand.png)

> [!CAUTION]
> **エラー 0x8007007e が発生してインストールに失敗しました**:このエラーが発生した場合、お使いのシステムは WSL をサポートしていません。 Windows ビルド 16215 以降を実行していることを確認してください。 [ビルドを確認してください](troubleshooting.md#check-your-build-number)。 さらに、[WSL が有効になっていることを確認](troubleshooting.md#confirm-wsl-is-enabled)し、この機能を有効にした後にコンピューターが再起動されていることを確認してください。  

3. PowerShell を使用して、Windows 環境の PATH (この例では `C:\Users\Administrator\Ubuntu`) にディストリビューション パスを追加します。

```powershell
$userenv = [System.Environment]::GetEnvironmentVariable("Path&quot;, &quot;User")
[System.Environment]::SetEnvironmentVariable("PATH", $userenv + ";C:\Users\Administrator\Ubuntu", "User")
```

これで、「`<distro>.exe`」と入力して任意のパスからディストリビューションを起動できるようになりました。 たとえば、 `ubuntu.exe`と指定します。

インストールされたら、使用する前に[新しいディストリビューション インスタンスを初期化する](./install-win10.md)必要があります。