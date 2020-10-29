---
title: WSL 2 Linux カーネルの更新
description: WSL 2 Linux カーネルを手動で更新するための手順
keywords: wsl, windows, linux カーネル, linux 用 windows サブシステム, カーネル
ms.date: 03/12/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 7bf2ef606d0bd23083f323117348aeea87c52b10
ms.sourcegitcommit: 609850fadd20687636b8486264e87af47c538111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2020
ms.locfileid: "92444808"
---
# <a name="updating-the-wsl-2-linux-kernel"></a>WSL 2 Linux カーネルの更新

WSL 2 内の Linux カーネルを手動で更新するには、次の手順に従ってください。

> [!NOTE] 
> インストーラーで WSL 1 が見つからない場合は、Linux カーネル更新プログラムのインストーラーを右クリックして [アンインストール] をクリックし、インストーラーを再実行します。

## <a name="download-the-linux-kernel-update-package"></a>Linux カーネル更新プログラム パッケージをダウンロードする

x64 マシン用の[最新の WSL2 Linux カーネル更新プログラム パッケージをダウンロード](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)してください。

> [!NOTE]
> ARM64 マシンを使用している場合は、代わりに [ARM64 パッケージ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)をダウンロードしてください。

## <a name="install-the-linux-kernel-update-package"></a>Linux カーネル更新プログラム パッケージをインストールする

Linux カーネル更新パッケージをインストールするには、次の手順に従ってください。

  1. 前の手順でダウンロードした更新プログラム パッケージを実行します。

  2. 管理者特権のアクセス許可の入力が求められます。このインストールを承認するには、[はい] を選択します。

  3. インストールが完了したら、WSL2 の使用を開始できます。

## <a name="future-plans-for-updating-the-wsl2-linux-kernel"></a>WSL2 Linux カーネルの更新に関する今後の計画

詳細については、[Windows コマンドラインのブログ](https://aka.ms/cliblog)にある[WSL2 Linux カーネルの更新プログラムに対する変更](https://devblogs.microsoft.com/commandline/wsl2-will-be-generally-available-in-windows-10-version-2004)に関するページを参照してください。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="this-update-only-applies-to-machines-with-the-windows-subsystem-for-linux"></a>この更新プログラムは、Linux 用 Windows サブシステムを搭載したコンピューターにのみ適用される
MSI カーネルをインストールするには、WSL が必要であり、最初に有効にする必要があります。 失敗した場合は、"`This update only applies to machines with the Windows Subsystem for Linux`" というメッセージが表示されます。 

このメッセージが表示される理由として、次の 3 つが考えられます。

1. WSL 2 をサポートしていない古いバージョンの Windows を使用しています。 [WSL 2 の要件](https://docs.microsoft.com/windows/wsl/install-win10#update-to-wsl-2)を確認し、WSL 2 を使用するようにアップグレードしてください。 
2. `Windows Subsystem for Linux` が有効になっていません。 [Linux 用 Windows サブシステムのインストール ガイド](https://docs.microsoft.com/windows/wsl/install-win10)に従ってください。
3. `Windows Subsystem for Linux` を有効にした後は再起動が必要になります。コンピューターを再起動して、もう一度やり直してください。

### `WSL 2 requires an update to its kernel component. For information please visit https://aka.ms/wsl2kernel`

%SystemRoot%\system32\lxss\tools\, にカーネルがない場合、その都度上記のエラーが発生する可能性があります。

これを解決するには、次のような方法があります。

1. このページの指示に従って Linux カーネルを手動でインストールしてください。
2. 'プログラムの追加と削除' から MSI をアンインストールしてから、もう一度インストールしてください。