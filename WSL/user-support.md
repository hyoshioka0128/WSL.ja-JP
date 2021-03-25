---
title: Linux ディストリビューションのユーザー アカウントを作成および更新する
description: Windows Subsystem for Linux を使用したユーザー アカウントとアクセス許可の管理のリファレンス。
keywords: BashOnWindows, bash, wsl, windows, windows subsystem for linux, windowssubsystem, ubuntu, ユーザー アカウント
ms.date: 05/12/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 3dcae6314db8fd32a446164725c42773660c454f
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104725959"
---
# <a name="create-a-user-account-and-password-for-your-new-linux-distribution"></a>新しい Linux ディストリビューションのユーザー アカウントとパスワードを作成する

[WSL を有効にし、Microsoft Store から Linux ディストリビューションをインストール](./install-win10.md)したら、新しくインストールされた Linux ディストリビューションを開くときに最初に実行する必要がある手順は、**ユーザー名** および **パスワード** を含むアカウントを作成することです。

- この **ユーザー名** および **パスワード** は、インストールする Linux ディストリビューションごとに固有であり、Windows ユーザー名とは関係ありません。

- ユーザーが **ユーザー名** および **パスワード** を作成すると、そのアカウントがディストリビューションの既定のユーザーとなり、起動時に自動的にサインインされます。

- このアカウントは、Linux 管理者と見なされ、`sudo` (Super User Do) 管理コマンドを実行できます。

- Windows Subsystem for Linux で実行されている各 Linux ディストリビューションには、独自の Linux ユーザー アカウントとパスワードがあります。  ディストリビューションの追加、再インストール、再設定を行うたびに、Linux ユーザー アカウントを構成する必要があります。

![Windows コンソールでの Ubuntu の展開](media/UbuntuInstall.png)

## <a name="update-and-upgrade-packages"></a>パッケージの更新とアップグレード

ほとんどのディストリビューションには、空または最小のパッケージ カタログが付属しています。 パッケージ カタログを定期的に更新し、ディストリビューションの推奨パッケージ マネージャーを使用して、インストールされているパッケージをアップグレードすることを強くお勧めします。 Debian または Ubuntu では、apt を使用します。

```bash
sudo apt update && sudo apt upgrade
```

Windows では、Linux ディストリビューションの更新やアップグレードは自動的に行われません。 これは、ほとんどの Linux ユーザーが自分で制御することを好むタスクです。

## <a name="reset-your-linux-password"></a>Linux パスワードの再設定

パスワードを変更するには、Linux ディストリビューション (Ubuntu など) を開き、コマンド `passwd` を入力します。

現在のパスワードを入力するよう求められ、新しいパスワードの入力を求められたら、新しいパスワードを確認します。

## <a name="forgot-your-password"></a>パスワードを忘れた場合

Linux ディストリビューションのパスワードを忘れた場合は、次のようにします。

1. PowerShell を開き、コマンド `wsl -u root` を使用して、既定の WSL ディストリビューションのルートを入力します。

    > 既定ではないディストリビューションで忘れたパスワードを更新する必要がある場合は、コマンド `wsl -d Debian -u root` を使用します。`Debian` は対象のディストリビューション名に置き換えます。

2. PowerShell 内のルート レベルでお客様の WSL ディストリビューションが開いたら、コマンド `passwd <WSLUsername>` を使用してパスワードを更新できます。ここで、`<WSLUsername>` は、パスワードを忘れてしまった DISTRO のアカウントのユーザー名です。

3. 新しい UNIX パスワードを入力し、そのパスワードを確認するように求められます。 パスワードが正常に更新されたことを示す通知が表示されたら、コマンド `exit` を使用して PowerShell 内の WSL を閉じます。

> [!NOTE]
> 古いバージョン (1703 (Creators Update) または 1709 (Fall Creators Update) など) の Windows オペレーティング システムを実行している場合、[アーカイブされたバージョンのこのユーザー アカウントの更新に関するドキュメント](./user-support-archived.md)を参照してください。
