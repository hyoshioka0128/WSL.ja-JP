---
title: Windows Subsystem for Linux のトラブルシューティング
description: Windows Subsystem for Linux で Linux を実行しているときに発生する一般的なエラーと問題について詳しく説明します。
keywords: BashOnWindows, bash, wsl, windows, windowssubsystem, ubuntu
ms.date: 09/28/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: b328d348486567bb06325293b69a9c92d0fc55fa
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493403"
---
# <a name="troubleshooting-windows-subsystem-for-linux"></a>Windows Subsystem for Linux のトラブルシューティング

WSL に関連する問題のサポートについては、[GitHub 上の WSL 製品リポジトリ](https://github.com/Microsoft/wsl/issues)を参照してください。

## <a name="search-for-any-existing-issues-related-to-your-problem"></a>発生している問題に関連する既存の問題を検索します

技術的な問題については、[製品リポジトリ](https://github.com/Microsoft/wsl/issues)を使用します。

このドキュメントの内容に関連する問題については、[ドキュメント リポジトリ](https://github.com/MicrosoftDocs/wsl/issues)を使用します。

## <a name="submit-a-bug-report"></a>バグ報告の送信

WSL の関数または機能に関連するバグについては、製品リポジトリに問題を報告します: https://github.com/Microsoft/wsl/issues

## <a name="submit-a-feature-request"></a>機能リクエストの送信

WSL の機能または互換性に関連する新しい機能をリクエストする場合は、[製品リポジトリに問題を報告します](https://github.com/Microsoft/wsl/issues)。

## <a name="contribute-to-the-docs"></a>ドキュメントに投稿する

WSL ドキュメントに投稿するには、ドキュメント リポジトリに pull request を送信します: https://github.com/MicrosoftDocs/wsl/issues

## <a name="terminal-or-command-line"></a>ターミナルまたはコマンド ライン

最後に、問題が Windows ターミナル、Windows コンソール、またはコマンドライン UI に関連している場合は、Windows ターミナル リポジトリを使用します: https://github.com/microsoft/terminal

## <a name="common-issues"></a>一般的な問題

### <a name="im-on-windows-10-version-1903-and-i-still-do-not-see-options-for-wsl-2"></a>Windows 10 バージョン 1903 を使用しているものの、WSL 2 のオプションがまだ表示されない

これはおそらく、お客様のマシンが WSL 2 のバックポートをまだ取得していないことが原因です。 これの最も簡単な解決方法は、Windows 設定に移動し、[更新プログラムの確認] をクリックして最新の更新プログラムをお客様のシステムにインストールすることです。 [バックポート取得の詳細な手順](https://devblogs.microsoft.com/commandline/wsl-2-support-is-coming-to-windows-10-versions-1903-and-1909/#how-do-i-get-it)をご覧ください。

[更新プログラムの確認] を押しても更新プログラムが届かない場合は、[手動で KB4566116 をインストール](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4566116)することができます。  

### <a name="error-0x1bc-when-wsl---set-default-version-2"></a>エラー: 0x1bc (`wsl --set-default-version 2` の場合)

これは、[表示言語] または [システム ロケール] の設定が英語ではない場合に発生する可能性があります。

```powershell
wsl --set-default-version 2
Error: 0x1bc
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
```

`0x1bc` の実際のエラーは次のとおりです。

```powershell
WSL 2 requires an update to its kernel component. For information please visit https://aka.ms/wsl2kernel
```

詳細については、問題 [5749](https://github.com/microsoft/WSL/issues/5749) を参照してください。

### <a name="cannot-access-wsl-files-from-windows"></a>Windows から WSL ファイルにアクセスできない

9P プロトコル ファイル サーバーは、Linux 側のサービスを提供して、Windows が Linux ファイル システムにアクセスできるようにします。 Windows で `\\wsl$` を使用して WSL にアクセスできない場合は、9P が正常に開始されなかった可能性があります。

これを確認するには、`dmesg |grep 9p` によってスタートアップ ログをチェックして、エラーを表示します。 正常な出力は次のようになります。

```bash
[    0.363323] 9p: Installing v9fs 9p2000 file system support
[    0.363336] FS-Cache: Netfs '9p' registered for caching
[    0.398989] 9pnet: Installing 9P2000 support
```

この問題の詳細については、[この Github スレッド](https://github.com/microsoft/wsl/issues/5307)を参照してください。

### <a name="cant-start-wsl-2-distribution-and-only-see-wsl-2-in-output"></a>WSL 2 ディストリビューションを開始できず、出力で 'WSL 2' のみが表示される

表示言語が英語でない場合は、切り捨てられたエラー テキストが表示される可能性があります。

```powershell
C:\Users\me>wsl
WSL 2
```

この問題を解決するには、`https://aka.ms/wsl2kernel` にアクセスし、そのドキュメント ページの指示に従って手動でカーネルをインストールしてください。 

### <a name="command-not-found-when-executing-windows-exe-in-linux"></a>Linux で Windows の .exe を実行すると、`command not found` と表示される

ユーザーは、notepad.exe などの Windows の実行可能ファイルを Linux から直接実行できます。 場合によっては、次のように "command not found" と表示されることがあります。 

```Bash
$ notepad.exe
-bash: notepad.exe: command not found
```

$PATH に Win32 パスがないと、相互運用によって .exe が検出されません。
これを確認するには、Linux で `echo $PATH` を実行します。 出力に Win32 パス (たとえば、/mnt/c/Windows) が表示されるはずです。
Windows パスが表示されない場合は、Linux シェルによって PATH が上書きされている可能性があります。 

次に、Debian 上で /etc/profile が原因でこの問題が起こった例を示します。

```Bash
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
fi
```

Debian での正しい方法は、上記の行を削除することです。
以下に示すように、割り当て時に $PATH を追加することもできますが、これは WSL と VSCode に関連する[その他の問題](https://salsa.debian.org/debian/WSL/-/commit/7611edba482fd0b3f67143aa0fc1e2cc1d4100a6)につながります。

```Bash
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$PATH"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:$PATH"
fi
```

詳細については、問題 [5296](https://github.com/microsoft/WSL/issues/5296) と問題 [5779](https://github.com/microsoft/WSL/issues/5779) を参照してください。

### <a name="error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed"></a>"Error:0x80370102 The virtual machine could not be started because a required feature is not installed." (エラー: 0x80370102 必要な機能がインストールされていないため、仮想マシンを起動できませんでした。)

仮想マシン プラットフォームの Windows 機能を有効にし、BIOS で仮想化が有効になっていることを確認してください。

1. [Hyper-V のシステム要件](/windows-server/virtualization/hyper-v/system-requirements-for-hyper-v-on-windows#:~:text=on%20Windows%20Server.-,General%20requirements,the%20processor%20must%20have%20SLAT.)を確認

2. マシンが VM の場合は、[入れ子になった仮想化](./wsl2-faq.yml#can-i-run-wsl-2-in-a-virtual-machine-)を手動で有効にしてください。 管理者で Powershell を起動し、次を実行します。

    ```powershell
    Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
    ```

3. 仮想化を有効にする方法については、お使いの PC の製造元のガイドラインに従ってください。 一般に、これらの機能が CPU で確実に有効になるようにするには、システム BIOS の使用が必要になる場合があります。 このプロセスの手順は、マシンによって異なる場合があります。一例として、Bleeping Computer による[この記事](https://www.bleepingcomputer.com/tutorials/how-to-enable-cpu-virtualization-in-your-computer-bios/)を参照してください。

4. `Virtual Machine Platform` のオプションのコンポーネントを有効にしたら、コンピューターを再起動してください。

### <a name="bash-loses-network-connectivity-once-connected-to-a-vpn"></a>VPN に接続されると、bash のネットワーク接続が切断される

Windows で VPN に接続した後、bash のネットワーク接続が切断される場合は、bash 内からこの回避策を試してください。 この回避策により、`/etc/resolv.conf` を使用して DNS 解決を手動で上書きできます。

1. `ipconfig.exe /all` を実行して、VPN の DNS サーバーをメモします
2. `sudo cp /etc/resolv.conf /etc/resolv.conf.new` で、既存の resolv.conf のコピーを作成します
3. `sudo unlink /etc/resolv.conf` で、現在の resolv.conf のリンクを解除します
4. `sudo mv /etc/resolv.conf.new /etc/resolv.conf`
5. `/etc/resolv.conf` を開きます。そして、 <br/>
   a。 ファイルから最初の行を削除します。この行の内容は "\# This file was automatically generated by WSL. To stop automatic generation of this file, remove this line." です。 <br/>
   b. DNS サーバーの一覧の最初のエントリとして、上記 (1) の DNS エントリ を追加します。 <br/>
   c. ファイを閉じます。 <br/>

VPN を切断したら、変更を `/etc/resolv.conf` に戻す必要があります。 これを行うには、次の手順を実行します。

1. `cd /etc`
2. `sudo mv resolv.conf resolv.conf.new`
3. `sudo ln -s ../run/resolvconf/resolv.conf resolv.conf`

### <a name="starting-wsl-or-installing-a-distribution-returns-an-error-code"></a>WSL の開始またはディストリビューションのインストールでエラー コードが返される

[こちらの手順](https://github.com/Microsoft/WSL/blob/master/CONTRIBUTING.md#8-detailed-logs)に従って、詳細なログを収集し、Microsoft の GitHub で問題を提出してください。

### <a name="updating-bash-on-ubuntu-on-windows"></a>Bash on Ubuntu on Windows の更新

Bash on Ubuntu on Windows には、更新が必要になることがある 2 つのコンポーネントがあります。

1. Windows Subsystem for Linux
  
   Bash on Ubuntu on Windows のこの部分をアップグレードすると、[リリース ノート](./release-notes.md)で概説されている新しい修正が有効になります。 Windows Insider Program をサブスクライブしていることと、ビルドが最新であることを確認してください。 Ubuntu インスタンスのリセットなど、より細かな制御を行うには、[コマンド リファレンスに関するページ](./reference.md)を確認してください。

2. Ubuntu ユーザー バイナリ

   Bash on Ubuntu on Windows のこの部分をアップグレードすると、apt-get を使用してインストールしたアプリケーションを含む Ubuntu ユーザー バイナリにすべての更新プログラムがインストールされます。 更新するには、Bash で次のコマンドを実行します。
  
   1. `apt-get update`
   2. `apt-get upgrade`
  
### <a name="apt-get-upgrade-errors"></a>apt-get アップグレードのエラー

一部のパッケージでは、まだ Microsoft が実装していない機能が使用されています。 たとえば、`udev` はまだサポートされていないため、`apt-get upgrade` エラーがいくつか発生します。

`udev` に関連する問題を修正するには、次の手順に従います。

1. 次の内容を `/usr/sbin/policy-rc.d` に記述して、変更を保存します。
  
   ```bash
   #!/bin/sh
   exit 101
   ```
  
2. 実行のアクセス許可を `/usr/sbin/policy-rc.d` に追加します。

   ```bash
   chmod +x /usr/sbin/policy-rc.d
   ```
  
3. 次のコマンドを実行します。

   ```bash
   dpkg-divert --local --rename --add /sbin/initctl
   ln -s /bin/true /sbin/initctl
   ```
  
### <a name="error-0x80040306-on-installation"></a>"Error:0x80040306" がインストール時に発生

これは、従来のコンソールがサポートされていないということと関連があります。
従来のコンソールをオフにするには、以下を実行します。

1. cmd.exe を開きます。
1. タイトル バーを右クリックして、[プロパティ] を選択し、[従来のコンソールを使う] をオフにします。
1. [OK] をクリックします。

### <a name="error-0x80040154-after-windows-update"></a>"Error:0x80040154" が Windows Update 後に発生

Windows Update 時に Windows Subsystem for Linux 機能が無効になる可能性があります。 その場合は、この Windows 機能を再度有効にする必要があります。 Windows Subsystem for Linux を有効にする手順については、[インストール ガイド](./install-win10.md)をご覧ください。

### <a name="changing-the-display-language"></a>表示言語の変更

WSL インストールでは、Windows インストールのロケールに合わせて Ubuntu ロケールを自動的に変更しようとします。  この動作が不要な場合は、次のコマンドを実行して、インストールの完了後に Ubuntu ロケールを変更できます。  この変更を有効にするには、bash.exe を再起動する必要があります。

次の例は、ロケールを en-US に変更します。

```bash
sudo update-locale LANG=en_US.UTF8
```

### <a name="installation-issues-after-windows-system-restore"></a>Windows システムの復元後のインストールの問題

1. `%windir%\System32\Tasks\Microsoft\Windows\Windows Subsystem for Linux` フォルダーを削除します。 <br/>
  **注: オプションの機能が完全にインストールされて動作している場合は、この操作を行わないでください。**
2. WSL オプション機能を有効にします (まだ有効にされていない場合)
3. 再起動します
4. lxrun /uninstall /full
5. Bash をインストールします

### <a name="no-internet-access-in-wsl"></a>WSL でインターネットにアクセスできない

一部のユーザーにより、WSL でのインターネット アクセスをブロックする特定のファイアウォール アプリケーションに関する問題が報告されています。  報告されているファイアウォールは次のとおりです。

1. Kaspersky
2. AVG
3. Avast
4. Symantec Endpoint Protection

ファイアウォールをオフにすると、アクセスできる場合があります。  場合によっては、ファイアウォールをインストールするだけでアクセスがブロックされるようです。

### <a name="permission-denied-error-when-using-ping"></a>ping 使用時のアクセス拒否エラー

[Windows Anniversary Update (バージョン 1607)](./release-notes.md#build-14388-to-windows-10-anniversary-update) では、WSL で ping を実行するには、Windows の **管理者特権** が必要です。  ping を実行するには、管理者として Bash on Ubuntu on Windows を実行するか、管理者特権を使用して CMD/PowerShell プロンプトから bash.exe を実行します。

Windows の最新バージョン ([Build 14926 以降](./release-notes.md#build-14926)) では、管理者特権は不要になりました。

### <a name="bash-is-hung"></a>Bash がハングしている

bash を使用しているときに bash がハングしている (またはデッドロックされている) か、入力に応答していないことに気付いた場合は、Microsoft が問題を診断できるようにメモリ ダンプを収集して報告してください。 次の手順によりシステムがクラッシュすることに注意してください。 それが問題である場合は、この操作を行わないでください。または、これを行う前に作業を保存してください。

メモリ ダンプを収集するには

1. メモリ ダンプの種類を "完全なメモリ ダンプ" に変更します。 ダンプの種類を変更するときに、現在の種類をメモしておきます。

2. [こちらの手順](https://techcommunity.microsoft.com/t5/Core-Infrastructure-and-Security/How-to-Force-a-Diagnostic-Memory-Dump-When-a-Computer-Hangs/ba-p/257809)を使用して、キーボード コントロールを使ってクラッシュを構成します。

3. ハングまたはデッドロックを再現します。

4. (2) のキー シーケンスを使用してシステムをクラッシュさせます。

5. システムはクラッシュし、メモリ ダンプを収集します。

6. システムが再起動したら、memory.dmp を secure@microsoft.com に報告します。 ダンプ ファイルの既定の場所は、%SystemRoot%\memory.dmp です。つまり、C: がシステム ドライブである場合は、C:\Windows\memory.dmp になります。 メールには、ダンプは WSL or Bash on Windows チーム向けであることを記載します。

7. メモリ ダンプの種類を元の設定に戻します。

### <a name="check-your-build-number"></a>ビルド番号を確認する

PC のアーキテクチャと Windows ビルド番号を確認するには、次を開きます。  
**[設定]**  >  **[システム]**  >  **[バージョン情報]**

**[OS ビルド]** フィールドと **[システムの種類]** フィールドを探します。  
    ![ビルドとシステムの種類のフィールドのスクリーンショット](media/system.png)

Windows Server のビルド番号を確認するには、PowerShell で次を実行します。  

``` PowerShell
systeminfo | Select-String "^OS Name","^OS Version"
```

### <a name="confirm-wsl-is-enabled"></a>WSL が有効になっていることを確認する

Windows Subsystem for Linux が有効になっていることを確認するには、PowerShell で次を実行します。  

``` PowerShell
Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

### <a name="openssh-server-connection-issues"></a>OpenSSH サーバーの接続に関する問題

SSH サーバーに接続しようとしましたが、次のエラーで失敗しました。"Connection closed by 127.0.0.1 port 22" (127.0.0.1 ポート 22 によって接続は閉じられました)。

1. OpenSSH サーバーが実行されていることを確認します。

   ```bash
   sudo service ssh status
   ```

   次のチュートリアルに従っていることも確認します。 https://ubuntu.com/server/docs/service-openssh

2. sshd サービスを停止し、デバッグ モードで sshd を開始します。

   ```bash
   sudo service ssh stop
   sudo /usr/sbin/sshd -d
   ```

3. スタートアップ ログを調べて、HostKey が使用可能であり、次のようなログ メッセージが表示されていないことを確認します。

   ```BASH
   debug1: sshd version OpenSSH_7.2, OpenSSL 1.0.2g  1 Mar 2016
   debug1: key_load_private: incorrect passphrase supplied to decrypt private key
   debug1: key_load_public: No such file or directory
   Could not load host key: /etc/ssh/ssh_host_rsa_key
   debug1: key_load_private: No such file or directory
   debug1: key_load_public: No such file or directory
   Could not load host key: /etc/ssh/ssh_host_dsa_key
   debug1: key_load_private: No such file or directory
   debug1: key_load_public: No such file or directory
   Could not load host key: /etc/ssh/ssh_host_ecdsa_key
   debug1: key_load_private: No such file or directory
   debug1: key_load_public: No such file or directory
   Could not load host key: /etc/ssh/ssh_host_ed25519_key
   ```

このようなメッセージが表示されていて、`/etc/ssh/` の下にそれらのキーがない場合は、キーを再生成するか、単に purge openssh-server と install openssh-server を実行する必要があります。

```BASH
sudo apt-get purge openssh-server
sudo apt-get install openssh-server
```

### <a name="the-referenced-assembly-could-not-be-found-when-enabling-the-wsl-optional-feature"></a>"参照されているアセンブリが見つかりませんでした。" WSL オプション機能を有効にする場合

このエラーは、インストール状態が正しくないことに関係があります。 この問題を解決するには、次の手順を実行してください。

- PowerShell から WSL 機能を有効にするコマンドを実行している場合、代わりに GUI を使用してみてください。[スタート] メニューを開き、[Windows の機能の有効化または無効化] を検索して、一覧で [Windows Subsystem for Linux] を選択すると、オプションのコンポーネントがインストールされます。

- [設定]、[更新] の順に移動し、[更新プログラムの確認] をクリックして、Windows のバージョンを更新します

- 上記の両方が失敗し、WSL にアクセスする必要がある場合は、インプレース アップグレードを検討してください。インストール メディアを使用して Windows 10 を再インストールし、[すべて保持] を選択することにより、アプリとファイルが確実に保持されます。 これを行うための手順については、[「Windows 10 を再インストールする」のページ](https://support.microsoft.com/help/4000735/windows-10-reinstall)をご覧ください。

### <a name="correct-ssh-related-permission-errors"></a>(SSH 関連の) アクセス許可のエラーを修正する

以下のエラーが表示される場合:

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0777 for '/home/artur/.ssh/private-key.pem' are too open.
```

これを修正するには、```/etc/wsl.conf``` ファイルに以下を追加します。

```bash
[automount]
enabled = true
options = metadata,uid=1000,gid=1000,umask=0022
```

このコマンドを追加すると、メタデータが組み込まれ、WSL から見た Windows ファイルに対するファイルのアクセス許可が変更されることにご注意ください。 詳細については、[ファイル システムのアクセス許可](./file-permissions.md)を参照してください。

### <a name="running-windows-commands-fails-inside-a-distribution"></a>ディストリビューション内で Windows コマンドを実行できない

[Microsoft Store で入手できる](install-win10.md#step-6---install-your-linux-distribution-of-choice)一部のディストリビューションにはまだ完全な互換性がなく、すぐに[ターミナル](https://en.wikipedia.org/wiki/Linux_console)で Windows コマンドを実行することができません。 `powershell.exe /c start .` や他の Windows コマンドを実行して、エラー `-bash: powershell.exe: command not found` が発生した場合は、次の手順に従って解決できます。

1. WSL ディストリビューション内で `echo $PATH` を実行します。  
   `/mnt/c/Windows/system32` が含まれていない場合は、何かによって標準の PATH 変数が再定義されています。
2. `cat /etc/profile` を使用してプロファイル設定を確認します。  
   PATH 変数の割り当てが含まれている場合は、ファイルを編集し、 **#** 文字を使って PATH の割り当てブロックをコメントアウトします。
3. wsl.conf が存在するかどうかをチェックし (`cat /etc/wsl.conf`)、`appendWindowsPath=false` が含まれていないことを確認します。含まれていた場合はコメントアウトします。
4. cmd、PowerShell のどちらかで、`wsl -t ` に続けてディストリビューション名を入力するか、`wsl --shutdown` を実行して、ディストリビューションを再起動します。

### <a name="unable-to-boot-after-installing-wsl-2"></a>WSL 2 のインストール後に起動できない

WSL 2 をインストールした後に起動できない問題が発生しています。 Microsoft がこれらの問題を完全に診断したところ、[バッファー サイズの変更](https://github.com/microsoft/WSL/issues/4784#issuecomment-639219363)または[適切なドライバーのインストール](https://github.com/microsoft/WSL/issues/4784#issuecomment-675702244)によってこの問題に対処できることがユーザーにより報告されました。 この問題の最新の更新プログラムについては、こちらの [Github イシュー](https://github.com/microsoft/WSL/issues/4784)を参照してください。 
