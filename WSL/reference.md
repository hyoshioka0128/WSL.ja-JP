---
title: Windows Subsystem for Linux のコマンド リファレンス
description: Linux コマンドを実行するための引数など、Linux 用 Windows サブシステムを管理するコマンドの一覧をご覧ください。
keywords: BashOnWindows, bash, wsl, windows, windows subsystem for linux, windowssubsystem, ubuntu
ms.date: 09/15/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 8e7f722cfe57ab0229ed7baff9091cc811232274
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104725749"
---
# <a name="command-reference-for-windows-subsystem-for-linux"></a>Windows Subsystem for Linux のコマンド リファレンス

Windows Subsystem for Linux を操作する最良の方法は、`wsl.exe` コマンドを使用することです。

## <a name="set-wsl-2-as-your-default-version"></a>WSL 2 を既定のバージョンとして設定する

PowerShell で次のコマンドを実行して、新しい Linux ディストリビューションをインストールするときに WSL 2 を既定のバージョンとして設定します。

```powershell
wsl --set-default-version 2
```

## <a name="set-your-distribution-version-to-wsl-1-or-wsl-2"></a>ディストリビューションのバージョンを WSL 1 または WSL 2 に設定する

インストールされている各 Linux ディストリビューションに割り当てられている WSL バージョンを確認するには、PowerShell コマンド ラインを開き、次のコマンドを入力します ([Windows ビルド 19041 以上](ms-settings:windowsupdate)でのみ使用可能): `wsl -l -v`

```bash
wsl --list --verbose
```

ディストリビューションで使用される WSL のバージョンを設定するには、以下を実行します。

```bash
wsl --set-version <distribution name> <versionNumber>
```

`<distribution name>` は、お使いのディストリビューションの実際の名前に必ず置き換えてください。`<versionNumber>` は、数字の "1" または "2" に置き換えてください。 上記と同じコマンドで "2" を "1" に置き換えて実行することにより、いつでも WSL 1 に戻すことができます。

また、WSL 2 を既定のアーキテクチャにする場合は、次のコマンドを使用して実行できます。

```bash
wsl --set-default-version 2
```

これにより、インストールされるすべての新しいディストリビューションのバージョンが WSL 2 に設定されます。

## `wsl.exe`

Windows バージョン 1903 以降で `wsl.exe` を使用する場合のすべてのオプションを含む一覧を次に示します。

使用法: `wsl [Argument] [Options...] [CommandLine]`

### <a name="arguments-for-running-linux-commands"></a>Linux コマンドを実行するための引数

* **引数なし**

  コマンド ラインが指定されていない場合、wsl.exe で既定のシェルが起動されます。

* **--exec、-e \<CommandLine>**
  
  既定の Linux シェルを使用せずに、指定したコマンドを実行します。

* **--**
  
  残りのコマンドラインをそのまま渡します。

上記のコマンドでは、次のオプションも使用できます。

* **--distribution、-d \<Distro>**

  指定されたディストリビューションを実行します。

* **--user、-u \<UserName>**

  指定されたユーザーとして実行します。

### <a name="arguments-for-managing-windows-subsystem-for-linux"></a>Windows Subsystem for Linux を管理するための引数

* **--export \<Distro> \<FileName>**
  
  ディストリビューションを tar ファイルにエクスポートします。 標準出力の場合、ファイル名は - でもかまいません。

* **--import \<Distro> \<InstallLocation> \<FileName>**
  
  指定した tar ファイルを新しいディストリビューションとしてインポートします。 標準入力の場合、ファイル名は - でもかまいません。

* **--list、-l [Options]**
  
  ディストリビューションを一覧表示します。

  オプション:
  * **--all**

    現在インストール中またはアンインストール中のディストリビューションを含む、すべてのディストリビューションを一覧表示します。

  * **--running**

    現在実行中のディストリビューションのみを一覧表示します。

* **--set-default、-s \<Distro>**
  
  このディストリビューションを既定値として設定します。

* **--terminate、-t \<Distro>**
  
  指定されたディストリビューションを終了します。

* **--unregister \<Distro>**
  
  ディストリビューションの登録を解除します。

* **--help** 使用方法に関する情報を表示します。

## <a name="additional-commands"></a>その他のコマンド

Windows Subsystem for Linux を操作するための過去のコマンドもあります。 これらの機能は、`wsl.exe` 内に含まれますが、引き続き使用できます。

### `wslconfig.exe`

このコマンドでは、WSL ディストリビューションを構成できます。 そのオプションの一覧を次に示します。

使用法: `wslconfig [Argument] [Options...]`

#### <a name="arguments"></a>引数

* **/l、/list [Options]**
  
  登録済みのディストリビューションを一覧表示します。
  
オプション:

* **/all** 現在インストール中またはアンインストール中のディストリビューションを含む、すべてのディストリビューションをオプションで一覧表示します。

* **/running** 現在実行中のディストリビューションのみを一覧表示します。

* **/s、/setdefault \<Distro>** このディストリビューションを既定値として設定します。

* **/t、/terminate \<Distro>** このディストリビューションを終了します。

* **/u、/unregister \<Distro>** このディストリビューションの登録を解除します。

* **/upgrade \<Distro>** このディストリビューションを WslFs ファイル システム形式にアップグレードします。

### `bash.exe`

このコマンドは、bash シェルを開始するために使用されます。 このコマンドで使用できるオプションを次に示します。

使用法: `bash [Options...]`

* **オプションの指定なし**
  
  現在のディレクトリで Bash シェルを起動します。 Bash シェルがインストールされていない場合は、`lxrun /install` が自動的に実行されます。

* **~**
  
  `bash ~` で、ユーザーのホームディレクトリに bash シェルが起動されます。  `cd ~` の実行と似ています。

* **-c "\<command>"**
  
  コマンドを実行し、出力を行って、Windows のコマンド プロンプトに戻ります。

  例: `bash -c "ls"` のようにします。

## <a name="deprecated-commands"></a>非推奨のコマンド

`lxrun.exe` は、Windows Subsystem for Linux をインストールして管理するために使用された最初のコマンドでした。 これは、Windows 10 1803 以降では非推奨です。

`lxrun.exe` コマンドは、Windows Subsystem for Linux (WSL) を直接操作するために使用できます。  これらのコマンドは `\Windows\System32` ディレクトリにインストールされ、Windows コマンド プロンプトまたは PowerShell 内で実行できます。

| コマンド                     | 説明                     |
|:----------------------------|:---------------------------|
| `lxrun`                     | lxrun コマンドは、WSL インスタンスの管理に使用されます。 |
| `lxrun /install`            | ダウンロードとインストールのプロセスを開始します。 <br/> **/y** を追加すると、すべてのプロンプトを省略できます。  確認プロンプトが自動的に受け入れられ、既定のユーザーはルートに設定されます。          |
| `lxrun /uninstall`          | Ubuntu イメージをアンインストールして削除します。  既定では、これで、ユーザーの Ubuntu ホーム ディレクトリは削除されません。 <br/> **/y** を追加すると、確認プロンプトを自動的に受け入れることができます。 <br/>**/full** を指定すると、ユーザーの Ubuntu ホーム ディレクトリをアンインストールして削除します。         |
| `lxrun /setdefaultuser <userName>`     | Ubuntu ユーザーの既定の Bash を設定します。 指定されたユーザーが存在しない場合は、パスワードの入力が求められます。  詳細については、 https://aka.ms/wslusers をご覧ください。 <br/> **/y** を指定すると、パスワードの入力を求めるプロンプトは省略されます。  ユーザーはパスワードなしで作成されます。|
| `lxrun /update`            | サブシステムのパッケージ インデックスを更新します。          |
