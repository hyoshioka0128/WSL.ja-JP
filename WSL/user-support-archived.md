---
title: 以前のバージョンの Windows での WSL ユーザーアカウントの更新
description: Windows Subsystem for Linux を使用して Linux ユーザーアカウントを更新するための、以前のバージョンの Windows のリファレンスです。
ms.date: 01/20/2020
ms.topic: article
ROBOTS: NOINDEX
ms.openlocfilehash: 069ce59a5e5b8b1466b0c127ebe37445afc13ae3
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104725949"
---
# <a name="wsl-user-account-updates-on-previous-windows-versions"></a>以前のバージョンの Windows での WSL ユーザーアカウントの更新

このコンテンツは、Linux 用サブシステムをサポートし、Linux ユーザーアカウントの更新をサポートする必要がある以前のバージョンの Windows オペレーティングシステムのユーザー向けにアーカイブされています。

最新のドキュメントについては、「 [Windows Subsystem For Linux のユーザーアカウント](./user-support.md)」を参照してください。

### <a name="for-creators-update-version-of-windows-and-earlier"></a>Windows およびそれ以前のバージョンの更新プログラムの場合

Windows 10 Creators Update 以前を実行している場合は、次のコマンドを実行して既定の Bash ユーザーを変更できます。

1. 既定のユーザーを `root` に変更します。

    ```console
    C:\> lxrun /setdefaultuser root
    ```

1. `bash.exe` を実行して、今度は `root` としてログインします。

    ```console
    C:\> bash.exe
    ```

1. ディストリビューションのパスワード コマンドを使用してパスワードを再設定し、Linux コンソールを閉じます。

    ```BASH
    $ passwd username
    $ exit
    ```

1. Windows CMD で、既定のユーザーを通常の Linux ユーザー アカウントに再設定して戻します。

    ```console
    C:\> lxrun.exe /setdefaultuser username
    ```

### <a name="for-fall-creators-update-and-later"></a>Fall Creators Update 以降の場合

特定のディストリビューションで使用できるコマンドを確認するには、`[distro.exe] /?` を実行します。
    
たとえば、Ubuntu がインストールされているとします。

```console
C:\> ubuntu.exe /?

Launches or configures a linux distribution.

Usage:
    <no args>
      - Launches the distro's default behavior. By default, this launches your default shell.

    run <command line>
      - Run the given command line in that distro, using the default configuration.
      - Everything after `run ` is passed to the linux LaunchProcess cal

    config [setting [value]]
      - Configure certain settings for this distro.
      - Settings are any of the following (by default)
        - `--default-user <username>`: Set the default user for this distro to <username>

    clean
      - Uninstalls the distro. The appx remains on your machine. This can be
        useful for "factory resetting" your instance. This removes the linux
        filesystem from the disk, but not the app from your PC, so you don't
        need to redownload the entire tar.gz again.

    help
      - Print this usage message.
```

Ubuntu を使用したステップ バイ ステップの手順:

1. CMD を開きます。
1. 既定の Linux ユーザーを `root` に設定します。

    ```console
    C:\> ubuntu config --default-user root
    ```    

1. Linux ディストリビューション (`ubuntu`) を起動します。  `root` として自動的にログインします。

1. `passwd` コマンドを使用してパスワードを再設定します。

    ```BASH
    $ passwd username
    ```

1. Windows CMD で、既定のユーザーを通常の Linux ユーザー アカウントに再設定して戻します。

    ```console
    C:\> ubuntu config --default-user username
    ```
