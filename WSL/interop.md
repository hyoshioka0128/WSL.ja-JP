---
title: Linux との Windows の相互運用性
description: Windows Subsystem for Linux で実行されている Linux ディストリビューションとの Windows の相互運用性について説明します。
ms.date: 05/12/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 3b6a6eab43d7d6534a0151b54c7db0071c8e5c77
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104725829"
---
# <a name="windows-interoperability-with-linux"></a>Linux との Windows の相互運用性

Windows Subsystem for Linux (WSL) は、Windows と Linux 間の統合を継続的に向上させています。  次の操作を行います。

* Windows ツール (つまり、notepad.exe) を Linux コマンド ライン (つまり、Ubuntu) から実行する。
* Linux ツール (つまり、grep) を Windows コマンド ライン (つまり、PowerShell) から実行する。
* Linux と Windows の間で環境変数を共有する。 (ビルド 17063 以降)

> [!NOTE]
> Creators Update (2017 年 10 月、ビルド 16299) または Anniversary Update (2016 年 8 月、ビルド 14393) を実行している場合は、「[Windows 10 の以前のバージョン](#earlier-versions-of-windows-10)」に進んでください。

## <a name="run-linux-tools-from-a-windows-command-line"></a>Windows コマンド ラインからの Linux ツールの実行

`wsl <command>` (または `wsl.exe <command>`) を使用して、Windows コマンド プロンプト (CMD) または PowerShell から Linux バイナリを実行します。

たとえば、次のように入力します。

```powershell
C:\temp> wsl ls -la
<- contents of C:\temp ->
```

この方法で起動されるバイナリには、次の特性があります。

* 現在の CMD または PowerShell プロンプトと同じ作業ディレクトリを使用します。
* WSL の既定のユーザーとして実行されます。
* 呼び出し元のプロセスおよびターミナルと同じ Windows 管理者権限を持ちます。

`wsl` (または `wsl.exe`) に続く Linux コマンドは、WSL での任意のコマンド実行と同様に処理されます。  sudo、パイプ処理、ファイル リダイレクトなどが機能します。

sudo を使用して既定の Linux ディストリビューションを更新する例:

```powershell
C:\temp> wsl sudo apt-get update
```

このコマンドを実行すると、既定の Linux ディストリビューションのユーザー名が一覧表示され、パスワードの入力を求められます。 パスワードを正しく入力すると、ディストリビューションによって更新プログラムがダウンロードされます。

## <a name="mixing-linux-and-windows-commands"></a>Linux と Windows のコマンドを組み合わせて使用する

PowerShell を使用して Linux と Windows のコマンドを組み合わせて使用するいくつかの例を次に示します。

Linux コマンド `ls -la` を使用してファイルを一覧表示し、PowerShell コマンド `findstr` を使用して "git" を含む単語の結果をフィルター処理するには、次のようにコマンドを組み合わせます。

```powershell
wsl ls -la | findstr "git"
```

Linux コマンド `dir` を使用してファイルを一覧表示し、PowerShell コマンド `grep` を使用して "git" を含む単語の結果をフィルター処理するには、次のようにコマンドを組み合わせます。

```powershell
C:\temp> dir | wsl grep git
```

Linux コマンド `ls -la` を使用してファイルを一覧表示し、PowerShell コマンド `> out.txt` を使用してその一覧を "out.txt" という名前のテキスト ファイルに出力するには、次のようにコマンドを組み合わせます。

```powershell
C:\temp> wsl ls -la > out.txt
```

`wsl.exe` に渡されるコマンドは、変更なしで WSL プロセスに転送されます。  ファイル パスは WSL 形式で指定する必要があります。

PowerShell を使用して、Linux コマンド `ls -la` を使用して `/proc/cpuinfo` Linux ファイル システム パス内のファイルを一覧表示するには、次のようにします。

```powershell
C:\temp> wsl ls -la /proc/cpuinfo
```

PowerShell を使用して、Linux コマンド `ls -la` を使用して `C:\Program Files` Windows ファイル システム パス内のファイルを一覧表示するには、次のようにします。

```powershell
C:\temp> wsl ls -la "/mnt/c/Program Files"
```

## <a name="run-windows-tools-from-linux"></a>Linux からの Windows ツールの実行

WSL では、`[tool-name].exe` を使用して、WSL コマンド ラインから Windows ツールを直接実行することができます。  たとえば、`notepad.exe` のように指定します。

<!-- Craig - could you help add a section with an example here to explain this scenario: "To access your Linux files using a Windows tool, use `\\wsl$\<distroName>\'` as the file path." Currently it I can just enter `notepad.exe foo.txt` and it seems to work fine, so explaining a situation where the file path is needed would be helpful. -->

この方法で実行されるアプリケーションには、次の特性があります。

* ほとんどの場合、作業ディレクトリを WSL コマンド プロンプトとして保持します (例外については後述します)。
* WSL プロセスと同じアクセス許可権限が与えられています。
* アクティブな Windows ユーザーとして実行されます。
* CMD プロンプトから直接実行されたかのように、Windows タスク マネージャーに表示されます。

WSL で実行される Windows 実行可能ファイルは、ネイティブの Linux 実行可能ファイルと同様に処理されます。パイプ処理、リダイレクト、さらにバックグラウンド処理も想定どおりに機能します。

Linux ディストリビューション (たとえば、Ubuntu) から Windows ツール `ipconfig.exe` を実行し、Linux ツール `grep` を使用して "IPv4" の結果をフィルター処理し、Linux ツール `cut` を使用して列フィールドを削除するには、次のように入力します。

```bash
ipconfig.exe | grep IPv4 | cut -d: -f2
```

Windows と Linux のコマンドを組み合わせた例を試してみましょう。 Linux ディストリビューション (つまり、Ubuntu) を開き、テキスト ファイルを作成します: `touch foo.txt`。 次に、Linux コマンド `ls -la` を使用して直接ファイルとその作成の詳細を一覧表示し、さらに Windows PowerShell ツール `findstr.exe` を使用して結果をフィルター処理して `foo.txt` ファイルのみが結果に表示されるようにします。

```bash
ls -la | findstr.exe foo.txt
```

Windows ツールは、ファイル拡張子を含み、ファイルの大文字と小文字が一致し、実行可能である必要があります。  非実行可能ファイルにはバッチ スクリプトが含まれます。  `dir` などの CMD ネイティブ コマンドは、`cmd.exe /C` コマンドを使用して実行できます。

たとえば、次のように入力して、Windows ファイル システムの C:\ ディレクトリの内容を一覧表示します。

```bash
cmd.exe /C dir
```

または、`ping` コマンドを使用して、エコー要求を microsoft.com Web サイトに送信します。

```bash
ping.exe www.microsoft.com
```

パラメーターは、変更されずに Windows バイナリに渡されます。 たとえば、次のコマンドを実行すると `C:\temp\foo.txt` が `notepad.exe` で開かれます。

```bash
notepad.exe "C:\temp\foo.txt"
```

以下も有効です。

```bash
notepad.exe C:\\temp\\foo.txt
```

## <a name="share-environment-variables-between-windows-and-wsl"></a>Windows と WSL の間での環境変数の共有

WSL と Windows は `WSLENV` を共有します。これは、Windows と WSL で実行される Linux ディストリビューションをつなぐために作成された特殊な環境変数です。

`WSLENV` 変数のプロパティ:

* 共有され、Windows と WSL の両方の環境に存在します。
* Windows と WSL の間で共有する環境変数の一覧です。
* Windows と WSL で適切に機能するように環境変数をフォーマットできます。
* WSL と Win32 間のフローに役立ちます。

> [!NOTE]
> 17063 より前では、WSL がアクセスできる唯一の Windows 環境変数は `PATH` でした (そのため、WSL で Win32 実行可能ファイルを起動できました)。 17063 以降、`WSLENV` がサポートされるようになります。
> WSLENV では、大文字と小文字が区別されます。

## <a name="wslenv-flags"></a>WSLENV フラグ

`WSLENV` には、環境変数の変換方法に影響を与える 4 つのフラグがあります。

`WSLENV` のフラグ:

* `/p` - WSL/Linux スタイル パスと Win32 パスの間でパスを変換します。
* `/l` - 環境変数がパスのリストであることを示します。
* `/u` - Win32 から WSL を実行する場合にのみ、この環境変数を含める必要があることを示します。
* `/w` - WSL から Win32 を実行する場合にのみ、この環境変数を含める必要があることを示します。

フラグは、必要に応じて組み合わせることができます。

[WSLENV の詳細](https://devblogs.microsoft.com/commandline/share-environment-vars-between-wsl-and-windows/)をご覧ください。これには、WSLENV の値を他の定義済みの環境変数の連結に設定し (各変数の末尾にはスラッシュが付けられ、その後に、値の変換方法を指定するフラグが続く)、スクリプトによって変数を渡す例や FAQ なども含まれます。 この記事には、WSL と Win32 の間で GOPATH を共有するように構成された、[Go プログラミング言語](https://golang.org/)により開発環境を設定する例も含まれています。

## <a name="disable-interoperability"></a>相互運用性の無効化

ユーザーは、ルートとして次のコマンドを実行することで、1 つの WSL セッションに対して Windows ツールを実行する機能を無効にできます。

```bash
echo 0 > /proc/sys/fs/binfmt_misc/WSLInterop
```

Windows バイナリを再び有効にするには、すべての WSL セッションを終了して bash.exe を再実行するか、ルートとして次のコマンドを実行します。

```bash
echo 1 > /proc/sys/fs/binfmt_misc/WSLInterop
```

相互運用の無効化は、WSL セッション間で保持されません。新しいセッションが開始されると、相互運用は再び有効になります。

## <a name="earlier-versions-of-windows-10"></a>Windows 10 の以前のバージョン

以前の Windows 10 バージョンでは、相互運用性コマンドにいくつかの違いがあります。 Windows 10 の Creators Update (2017 年 10 月、Build 16299) バージョンまたは Anniversary Update (2016 年 8 月、Build 14393) バージョンを実行している場合は[最新の Windows バージョンに更新する](ms-settings:windowsupdate)ことをお勧めします。ただし、これが不可能な場合のために、相互運用性に関する相違点のいくつかを次にまとめてあります。

要約:

* `bash.exe` は `wsl.exe` に置き換えられました。
* 1 つのコマンドを実行する場合の `-c` オプションは、`wsl.exe` で必要ありません。
* Windows パスは WSL `$PATH` に含まれています。
* 相互運用を無効にするプロセスは変更されていません。

Linux コマンドは Windows コマンド プロンプトまたは PowerShell から実行できますが、初期の Windows バージョンでは `bash` コマンドを使用することが必要になる場合があります。 たとえば、次のように入力します。

```powershell
C:\temp> bash -c "ls -la"
```

sudo、パイプ処理、ファイル リダイレクトなどが想定どおりに機能します。

`bash -c` に渡される WSL コマンドは、変更なしで WSL プロセスに転送されます。  ファイル パスは WSL 形式で指定する必要があり、関連文字をエスケープするように注意する必要があります。 例:

```console
C:\temp> bash -c "ls -la /proc/cpuinfo"
```

または

```powershell
C:\temp> bash -c "ls -la \"/mnt/c/Program Files\""
```

以前のバージョンの Windows 10 の WSL ディストリビューションから Windows ツールを呼び出す場合は、ディレクトリ パスを指定する必要があります。 たとえば、WSL コマンド ラインから次のように入力します。

```bash
/mnt/c/Windows/System32/notepad.exe
```

WSL では、これらの実行可能ファイルはネイティブの Linux 実行可能ファイルと同様に処理されます。  これは、Linux パスへのディレクトリの追加や、コマンド間でのパイプ処理が想定どおりに機能することを意味します。  たとえば、次のように入力します。

```bash
export PATH=$PATH:/mnt/c/Windows/System32
```
または

```bash
ipconfig.exe | grep IPv4 | cut -d: -f2
```

Windows バイナリは、ファイル拡張子を含み、ファイルの大文字と小文字が一致し、実行可能である必要があります。  バッチ スクリプトや `dir` などのコマンドを含む非実行可能ファイルは、`/mnt/c/Windows/System32/cmd.exe /C` コマンドを使用して実行できます。 たとえば、次のように入力します。

```bash
/mnt/c/Windows/System32/cmd.exe /C dir
```

## <a name="additional-resources"></a>その他の資料

* [2016 年からの相互運用性に関する WSL のブログの投稿](/archive/blogs/wsl/windows-and-ubuntu-interoperability)