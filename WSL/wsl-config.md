---
title: Linux ディストリビューションの管理
description: Windows Subsystem for Linux で実行されている複数の Linux ディストリビューションの一覧表示と構成に関するリファレンス。
keywords: BashOnWindows, bash, wsl, windows, windows subsystem for linux, windowssubsystem, ubuntu, wsl.conf, wslconfig
ms.date: 03/26/2021
ms.topic: article
ms.openlocfilehash: 6a18fe22740f01536e46df206f3d2cf7dc6b54d4
ms.sourcegitcommit: 18ce6b800db6bca7643de0c2bea02fb383761bcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2021
ms.locfileid: "105994110"
---
# <a name="wsl-commands-and-launch-configurations"></a>WSL コマンドと起動構成

## <a name="ways-to-run-wsl"></a>WSL を実行する方法

WSL を [インストール](install-win10.md)した Linux ディストリビューションを実行するには、いくつかの方法があります。

1. Windows の [スタート] メニューにアクセスし、インストールされているディストリビューションの名前を入力して、Linux ディストリビューションを開きます。 たとえば、"Ubuntu" のようになります。
2. Windows のコマンドプロンプトまたは PowerShell から、インストールされている配布の名前を入力します。 例: `ubuntu`
3. Windows コマンドプロンプトまたは PowerShell から、現在のコマンドライン内で既定の Linux ディストリビューションを開くには、「」と入力し `wsl.exe` ます。
4. Windows コマンドプロンプトまたは PowerShell から、現在のコマンドライン内で既定の Linux ディストリビューションを開くには、「」と入力し `wsl [command]` ます。

どの方法を使用すべきかは、作業内容によって異なります。 Windows プロンプトまたは PowerShell ウィンドウ内で WSL コマンドラインを開いて終了する場合は、コマンドを入力します `exit` 。

## <a name="launch-wsl-by-distribution"></a>ディストリビューションによって WSL を起動する

ディストリビューション固有のアプリケーションを使用してディストリビューションを実行すると、そのディストリビューションが独自のコンソール ウィンドウで起動します。

![[スタート] メニューからの WSL の起動](media/start-launch.png)

これは、Microsoft Store で [起動] をクリックすることと同じです。

![Microsoft Store からの WSL の起動](media/store-launch.png)

`[distribution].exe` を実行して、コマンド ラインからディストリビューションを実行することもできます。

この方法でコマンド ラインからディストリビューションを実行すると、作業ディレクトリが現在のディレクトリからディストリビューションのホーム ディレクトリに自動的に変更されるという欠点があります。

**例: (PowerShell を使用)**

```console
PS C:\Users\sarah> pwd

Path
----
C:\Users\sarah

PS C:\Users\sarah> ubuntu

scooley@scooley-elmer:~$ pwd
/home/scooley
scooley@scooley-elmer:~$ exit
logout

PS C:\Users\sarah>
```

### <a name="wsl-and-wsl-command"></a>wsl および wsl [コマンド]

コマンド ラインから WSL を実行する最善の方法は、`wsl.exe` を使用することです。

**例: (PowerShell を使用)**

```console
PS C:\Users\sarah> pwd

Path
----
C:\Users\sarah

PS C:\Users\sarah> wsl

scooley@scooley-elmer:/mnt/c/Users/sarah$ pwd
/mnt/c/Users/sarah
```

`wsl` は、現在の作業ディレクトリを適切に維持するだけでなく、1 つのコマンドを Windows コマンドとともに実行できます。

**例: (PowerShell を使用)**

```console
PS C:\Users\sarah> Get-Date

Sunday, March 11, 2018 7:54:05 PM

PS C:\Users\sarah> wsl
scooley@scooley-elmer:/mnt/c/Users/sarah$ date
Sun Mar 11 19:55:47 DST 2018
scooley@scooley-elmer:/mnt/c/Users/sarah$ exit
logout

PS C:\Users\sarah> wsl date
Sun Mar 11 19:56:57 DST 2018
```

**例: (PowerShell を使用)**

```console
PS C:\Users\sarah> Get-VM

Name            State CPUUsage(%) MemoryAssigned(M) Uptime   Status
----            ----- ----------- ----------------- ------   ------
Server17093     Off   0           0                 00:00:00 Opera...
Ubuntu          Off   0           0                 00:00:00 Opera...
Ubuntu (bionic) Off   0           0                 00:00:00 Opera...
Windows         Off   0           0                 00:00:00 Opera...


PS C:\Users\sarah> Get-VM | wsl grep "Ubuntu"
Ubuntu          Off   0           0                 00:00:00 Opera...
Ubuntu (bionic) Off   0           0                 00:00:00 Opera...
PS C:\Users\sarah>
```

## <a name="managing-multiple-linux-distributions"></a>複数の Linux ディストリビューションの管理

Windows 10 バージョン 1903 [以降](ms-settings:windowsupdate)では、を使用して `wsl.exe` Windows Subsystem for Linux (wsl) でのディストリビューションを管理できます。これには、使用可能なディストリビューションの一覧表示、既定の配布の設定、およびディストリビューションのアンインストールが含まれます。

各 Linux ディストリビューションは、個別に独自の構成を管理します。 ディストリビューション固有のコマンドを確認するには、`[distro.exe] /?` を実行します。  たとえば、「 `ubuntu /?` 」のように指定します。

## <a name="list-distributions"></a>ディストリビューションの一覧表示

`wsl -l` , `wsl --list`  
WSL で利用可能な Linux ディストリビューションを一覧表示します。  一覧表示されているディストリビューションは、インストールされており、使用できる状態です。

`wsl --list --all` 現在使用できないすべてのディストリビューションを含む、すべてのディストリビューションを一覧表示します。  インストールのプロセス中、アンインストールのプロセス中、または破損した状態の可能性があります。  

`wsl --list --running` 現在実行中のすべてのディストリビューションを一覧表示します。

## <a name="set-a-default-distribution"></a>既定のディストリビューションの設定

既定の WSL ディストリビューションは、コマンド ラインで `wsl` を実行するときに実行されるものです。

`wsl -s <DistributionName>`, `wsl --setdefault <DistributionName>`

既定のディストリビューションを `<DistributionName>` に設定します。

**例: (PowerShell を使用)**  
`wsl -s Ubuntu` の場合、既定のディストリビューションが Ubuntu に設定されます。  これで、`wsl npm init` を実行すると、Ubuntu で実行されるようになります。  `wsl` を実行すると、Ubuntu セッションが開きます。

## <a name="unregister-and-reinstall-a-distribution"></a>ディストリビューションの登録解除と再インストール

Linux ディストリビューションは Microsoft Store を介してインストールできますが、そのストアを介してアンインストールすることはできません。  WSL Config を使用すると、ディストリビューションの登録解除/アンインストールを行うことができます。

登録を解除すると、ディストリビューションを再インストールすることもできます。

> **注意:** 登録が解除されると、その配布に関連付けられているすべてのデータ、設定、およびソフトウェアが完全に失われます。  ストアから再インストールすると、ディストリビューションのクリーン コピーがインストールされます。

`wsl --unregister <DistributionName>`  
ディストリビューションを再インストールまたはクリーンアップできるように、WSL からその登録が解除されます。

たとえば、`wsl --unregister Ubuntu` の場合、WSL で使用可能なディストリビューションから Ubuntu が削除されます。  `wsl --list` を実行すると、それは一覧に表示されません。

再インストールするには、Microsoft Store でディストリビューションを見つけて、[起動] を選択します。

## <a name="run-as-a-specific-user"></a>特定のユーザーとしての実行

`wsl -u <Username>`, `wsl --user <Username>`

指定されたユーザーとして WSL を実行します。 ユーザーは WSL ディストリビューション内に存在する必要があることに注意してください。

## <a name="change-the-default-user-for-a-distribution"></a>配布の既定のユーザーを変更する

`<DistributionName> config --default-user <Username>`

ディストリビューションログインの既定のユーザーを変更します。 既定のユーザーになるには、ユーザーが既にディストリビューション内に存在している必要があります。 

たとえば、 `ubuntu config --default-user johndoe` Ubuntu ディストリビューションの既定のユーザーを "johndoe" ユーザーに変更します。

> [!NOTE]
> 配布の名前を確認できない場合は、コマンドの [ [ディストリビューションの一覧](#list-distributions) ] を参照して、インストールされているディストリビューションの正式な名前を一覧表示します。 

## <a name="run-a-specific-distribution"></a>特定のディストリビューションの実行

`wsl -d <DistributionName>`, `wsl --distribution <DistributionName>`

WSL の指定したディストリビューションの実行は、既定値を変更する必要なしに、特定のディストリビューションにコマンドを送信するために使用できます。

## <a name="managing-multiple-linux-distributions-in-earlier-windows-versions"></a>以前のバージョンの Windows での複数の Linux ディストリビューションの管理

バージョン1903より前の Windows 10 では、WSL Config ( `wslconfig.exe` ) コマンドラインツールを使用して、Windows Subsystem For linux (wsl) で実行されている linux ディストリビューションを管理する必要があります。  これにより、使用可能なディストリビューションの一覧表示、既定のディストリビューションの設定、およびディストリビューションのアンインストールを行うことができます。

WSL Config はディストリビューションにまたがる設定やそれらを調整する設定に役立ちますが、各 Linux ディストリビューションは個別に独自の構成を管理します。  ディストリビューション固有のコマンドを確認するには、`[distro.exe] /?` を実行します。  たとえば、「 `ubuntu /?` 」のように指定します。

wslconfig で使用可能なオプションをすべて表示するには、`wslconfig /?` を実行します。

```console
wslconfig.exe
Performs administrative operations on Windows Subsystem for Linux

Usage:
    /l, /list [/all] - Lists registered distributions.
        /all - Optionally list all distributions, including distributions that
               are currently being installed or uninstalled.
    /s, /setdefault <DistributionName> - Sets the specified distribution as the default.
    /u, /unregister <DistributionName> - Unregisters a distribution.
```

ディストリビューションを一覧表示するには、次のように使用します。

`wslconfig /list`  
WSL で利用可能な Linux ディストリビューションを一覧表示します。  一覧表示されているディストリビューションは、インストールされており、使用できる状態です。

`wslconfig /list /all`  
現在使用できないディストリビューションを含む、すべてのディストリビューションを一覧表示します。  インストールのプロセス中、アンインストールのプロセス中、または破損した状態の可能性があります。  

コマンドラインでを実行したときに実行される既定のディストリビューションを設定するには、次のようにし `wsl` ます。

`wslconfig /setdefault <DistributionName>` 既定の分布をに設定 `<DistributionName>` します。

**例: (PowerShell を使用)**  
`wslconfig /setdefault Ubuntu` の場合、既定のディストリビューションが Ubuntu に設定されます。  これで、`wsl npm init` を実行すると、Ubuntu で実行されるようになります。  `wsl` を実行すると、Ubuntu セッションが開きます。

配布を登録解除して再インストールするには:

`wslconfig /unregister <DistributionName>`  
ディストリビューションを再インストールまたはクリーンアップできるように、WSL からその登録が解除されます。

たとえば、`wslconfig /unregister Ubuntu` の場合、WSL で使用可能なディストリビューションから Ubuntu が削除されます。  `wslconfig /list` を実行すると、それは一覧に表示されません。

再インストールするには、Microsoft Store でディストリビューションを見つけて、[起動] を選択します。

## <a name="configure-per-distro-launch-settings-with-wslconf"></a>ディストリビューションごとの起動設定を wslconf で構成する

> **Windows ビルド17093以降で使用可能**

を使用してサブシステムを起動するたびに適用される WSL の機能を自動的に構成 `wsl.conf` します。 これには自動マウント オプションとネットワーク構成が含まれます。

`wsl.conf` は、`/etc/wsl.conf` 内の各 Linux ディストリビューションにあります。 そのファイルがそこになければ、自分で作成できます。 WSL は、ファイルの存在を検出し、その内容を読み取ります。 ファイルが見つからないか、形式が正しくない (つまり、不適切なマークアップ形式である) 場合、WSL は通常どおりに起動を続けます。

`wsl.conf`ディストリビューションに追加できるサンプルファイルを次に示します。

```console
# Enable extra metadata options by default
[automount]
enabled = true
root = /windir/
options = "metadata,umask=22,fmask=11"
mountFsTab = false

# Enable DNS – even though these are turned on by default, we'll specify here just to be explicit.
[network]
generateHosts = true
generateResolvConf = true
```

同じディストリビューションに対して複数の Linux シェルを起動する場合は、Linux サブシステムが実行を停止するまで待機する必要があります。これには、ディストリビューションシェルの最後のインスタンスを閉じてから約8秒かかることがあります。 配布を起動した場合 (Ubuntu) で、wsl の conf ファイルを変更し、配布を終了してから再起動します。 Wsl の conf ファイルへの変更がすぐに有効になることを想定しています。 現在のところ、サブシステムが実行されている可能性があります。 変更を取得するのに十分な時間を確保するために、再起動する前にサブシステムが停止するまで最大8秒間待機する必要があります。 PowerShell とコマンドを使用して、Linux ディストリビューション (シェル) がまだ実行されているかどうかを確認でき `wsl --list --running` ます。 ディストリビューションが実行されていない場合は、"実行中のディストリビューションがありません" という応答が返されます。 これで、ディストリビューションを再起動して、適用された wsl の更新プログラムを確認できます。

### <a name="configuration-options"></a>構成オプション

.ini 規則に従って、キーはセクションの下で宣言されます。 

Wsl では、、、、およびの4つのセクションがサポートさ `automount` `network` `interop` れてい `user` ます。

#### <a name="automount"></a>automount

セクション: `[automount]`

| key        | value                          | default      | notes                                                                                                                                                                                                                                                                                                                          |
|:-----------|:-------------------------------|:-------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled    | boolean                        | true         | `true` にすると、固定ドライブ (つまり、 `C:/` または`D:/`) は `/mnt` の下に DrvFs で自動的にマウントされます。  `false` ドライブは自動的にマウントされませんが、手動またはを使用してマウントすることもでき `fstab` ます。                                                                                                             |
| mountFsTab | boolean                        | true         | `true` にすると、WSL 開始時に処理されるように `/etc/fstab` を設定します。 /etc/fstab は、SMB 共有などの他のファイル システムを宣言できるファイルです。 そのため、起動時にこれらのファイル システムを WSL 内で自動的にマウントできます。                                                                                                                |
| root       | String                         | `/mnt/`      | 固定ドライブが自動的にマウントされるディレクトリを設定します。 たとえば、`/windir/` に WSL のディレクトリがあり、それをルートとして指定すると、固定ドライブは `/windir/c` でマウントされることが予想されます。                                                                                              |
| options    | 値のコンマ区切りのリスト | 空の文字列 | この値は、既定の DrvFs マウント オプション文字列に追加されます。 **DrvFs 固有のオプションのみを指定できます。** マウント バイナリが通常、フラグに解析するオプションはサポートされていません。 これらのオプションを明示的に指定する場合は、それを行う対象のドライブすべてを /etc/fstab に含める必要があります。 |

既定では、WSL は uid と gid を既定のユーザーの値に設定します (Ubuntu ディストリビューションでは、既定のユーザーは uid = 1000、gid = 1000 で作成されます)。 ユーザーがこのキーを使用して gid または uid オプションを明示的に指定した場合、関連する値は上書きされます。 それ以外の場合は、既定値が常に追加されます。

**注:** これらのオプションは、自動的にマウントされたすべてのドライブのマウントオプションとして適用されます。 特定のドライブのみのオプションを変更するには、代わりに /etc/fstab を使用します。

#### <a name="mount-options"></a>マウント オプション

Windows ドライブ (DrvFs) にさまざまなマウント オプションを設定すると、Windows ファイルのファイルのアクセス許可を計算する方法を制御できます。 次のオプションを使用できます。

| Key | 説明 | Default |
|:----|:----|:----|
|uid| すべてのファイルの所有者に使用するユーザー ID | WSL ディストリビューションの既定のユーザー ID (初回インストールの場合、既定値は 1000)
|gid| すべてのファイルの所有者に使用するグループ ID | WSL ディストリビューションの既定のグループ ID (初回インストールの場合、既定値は 1000)
|umask | すべてのファイルとディレクトリに対して除外するアクセス許可の 8 進数のマスク | 000
|fmask | すべてのファイルに対して除外するアクセス許可の 8 進数のマスク | 000
|dmask | すべてのディレクトリに対して除外するアクセス許可の 8 進数のマスク | 000
|metadata | Linux システムのアクセス許可をサポートするためにメタデータを Windows ファイルに追加するかどうか | disabled

**注:** アクセス許可マスクは、ファイルまたはディレクトリに適用される前に論理 OR 演算によって配置されます。 

#### <a name="network"></a>ネットワーク

セクションのラベル: `[network]`

| key | value | default | notes|
|:----|:----|:----|:----|
| generateHosts | boolean | `true` | `true` にすると、`/etc/hosts` を生成するように WSL を設定します。 `hosts` ファイルには、IP アドレスに対応するホスト名の静的マップが含まれています。 |
| generateResolvConf | boolean | `true` | `true` にすると、`/etc/resolv.conf` を生成するように WSL を設定します。 `resolv.conf` には、指定されたホスト名をその IP アドレスに解決できる DNS リストが含まれています。 | 

#### <a name="interop"></a>interop

セクションのラベル: `[interop]`

次のオプションは、Insider Build 17713 以降で使用できます。

| key | value | default | notes|
|:----|:----|:----|:----|
| enabled | boolean | `true` | このキーの設定により、WSL で Windows プロセスの起動をサポートするかどうかが決まります。 |
| appendWindowsPath | boolean | `true` | このキーの設定により、WSL が Windows パス要素を $PATH 環境変数に追加するかどうかが決まります。 |

#### <a name="user"></a>user

セクションのラベル: `[user]`

これらのオプションは、ビルド18980以降で使用できます。

| key | value | default | notes|
|:----|:----|:----|:----|
| default | string | 最初の実行時に作成された最初のユーザー名 | このキーを設定すると、最初に WSL セッションを開始したときに実行するユーザーを指定します。 |

## <a name="configure-global-options-with-wslconfig"></a>Wslconfig を使用してグローバルオプションを構成する

> **Windows ビルド19041以降で使用可能**

グローバル WSL オプションを構成するには、 `.wslconfig` ユーザーフォルダーのルートディレクトリにファイルを配置し `C:\Users\<yourUserName>\.wslconfig` ます。 これらのファイルの多くは WSL 2 に関連しています。そのため、 `wsl --shutdown` wsl 2 VM をシャットダウンしてから wsl インスタンスを再起動して変更を反映するために、を実行することが必要になる場合があります。

サンプルの wslconfig ファイルを次に示します。

```console
[wsl2]
kernel=C:\\temp\\myCustomKernel
memory=4GB # Limits VM memory in WSL 2 to 4 GB
processors=2 # Makes the WSL 2 VM use two virtual processors
```

このファイルには、次のオプションを含めることができます。

### <a name="wsl-2-settings"></a>WSL 2 の設定

セクションのラベル: `[wsl2]`

これらの設定は、WSL 2 ディストリビューションを電源にする VM に影響します。

| key | value | default | notes|
|:----|:----|:----|:----|
| kernel | string | Microsoft が構築したカーネルの受信トレイ | カスタム Linux カーネルへの絶対 Windows パス。 |
| メモリ | サイズ | Windows または 8 GB のメモリ合計の 50% (どちらか少ない方)20175より前のビルドの場合: Windows 上の合計メモリの80% | WSL 2 VM に割り当てるメモリの量。 |
| 状況 | number | Windows 上の同じプロセッサ数 | WSL 2 VM に割り当てるプロセッサの数。 |
| localhostForwarding | boolean | `true` | WSL 2 VM のワイルドカードまたは localhost にバインドされたポートが localhost: port を介してホストから接続可能である必要があるかどうかを指定するブール値。 |
| カーネルコマンドライン | string | 空白 | 追加のカーネルコマンドライン引数。 |
| swap | サイズ | Windows 上のメモリサイズの25% が最も近い GB に切り上げられます | WSL 2 VM に追加するスワップ領域の大きさ。スワップファイルがない場合は0です。 |
| スワップ | string | %USERPROFILE%\AppData\Local\Temp\swap.vhdx | スワップバーチャルハードディスクへの絶対 Windows パス。 |

* メモ: この値は Windows ビルド19041では true であり、Insider プログラムの Windows ビルドでは異なる場合があります。

値がのエントリは `path` 、エスケープされた円記号を含む Windows パスである必要があります。次に例を示します。 `C:\\Temp\\myCustomKernel`

値を持つエントリは、 `size` サイズの後に単位 (やなど) が続く必要があり `8GB` `512MB` ます。
