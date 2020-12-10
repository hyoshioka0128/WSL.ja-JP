---
title: WSL 2 と WSL 1 の比較
description: Linux 用 Windows サブシステムのバージョン 1 とバージョン 2 を比較します。 WSL 2 の新機能について説明します。これには、実際の Linux カーネル、速度の向上、システム コールの完全な互換性が含まれます。 複数のオペレーティング ファイル システムをまたいでファイルを格納している場合は、WSL 1 の方が適しています。 WSL 2 の仮想ハードウェア ディスク (VHD) のサイズは拡張できます。
keywords: BashOnWindows, bash, wsl, windows, windowssubsystem, gnu, linux, ubuntu, debian, suse, windows 10, UX の変更, WSL 2, linux カーネル, ネットワーク アプリケーション, localhost, IPv6, 仮想ハードウェア ディスク, VHD, VHD の制限, VHD エラー
ms.date: 09/28/2020
ms.topic: conceptual
ms.localizationpriority: high
ms.custom: contperf-fy21q1
ms.openlocfilehash: ff2c9bc08b4fdfe8862f7d65fc5861fa242efef7
ms.sourcegitcommit: c92245ab2b763d6a357210a9b4470a0cafd786a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96857599"
---
# <a name="comparing-wsl-1-and-wsl-2"></a>WSL 1 と WSL 2 の比較

Linux 用 Windows サブシステムを WSL 1 から WSL 2 に更新する際の主な相違点と、そうする理由は次のとおりです。

- **ファイル システム パフォーマンスの向上**
- **システム コールの完全な互換性のサポート**

軽量のユーティリティ仮想マシン (VM) 内で Linux カーネルを実行するために、WSL 2 には最新の優れた仮想化テクノロジが使用されています。 ただし、WSL 2 は従来の VM エクスペリエンスではありません。

> [!div class="nextstepaction"]
> [WSL 1 をインストールし、WSL 2 に更新する](install-win10.md)

## <a name="comparing-features"></a>機能の比較

機能 | WSL 1 | WSL 2
--- | --- | ---
 Windows と Linux の統合| ✅|✅
 高速の起動時間| ✅ | ✅
 小さなリソース フット プリント| ✅ |✅
 現在のバージョンの VMware および VirtualBox での実行| ✅ | ✅
 マネージド VM| ❌ | ✅
 完全な Linux カーネル| ❌ |✅
 システム コールの完全な互換性| ❌ | ✅
 OS ファイル システム間でのパフォーマンス| ✅ | ❌

上の比較表からわかるように、WSL 2 のアーキテクチャは、いくつかの点で WSL 1 よりも優れています (OS ファイル システム間でのパフォーマンスを除く)。

## <a name="performance-across-os-file-systems"></a>OS ファイル システム間でのパフォーマンス

特殊な理由がない限り、複数のオペレーティング システム間でファイルを操作しないことをお勧めします。 Linux コマンド ライン (Ubuntu、OpenSUSE など) で作業している場合、最速のパフォーマンス速度を実現するには、ファイルを WSL ファイル システムに格納します。 Windows コマンド ライン (PowerShell、コマンド プロンプト) で作業している場合、ファイルを Windows ファイル システムに格納してください。

たとえば、WSL プロジェクト ファイルを格納する場合は、次のとおりです。

- Linux ファイル システムのルート ディレクトリを使用します: `\\wsl$\Ubuntu-18.04\home\<user name>\Project`
- Windows ファイル システムのルート ディレクトリではありません: `C:\Users\<user name>\Project`

現在実行中のすべてのディストリビューション (`wsl -l`) には、ネットワーク接続経由でアクセスできます。 アクセスするには、コマンド \[WIN+R\] (キーボード ショートカット) を実行するか、エクスプローラーのアドレス バーに「`\\wsl$`」と入力してそれぞれのディストリビューション名を検索し、そのルート ファイル システムにアクセスします。

また、WSL の Linux [ターミナル](https://en.wikipedia.org/wiki/Linux_console)内で Windows コマンドを使用することもできます。 Linux ディストリビューション (Ubuntu など) を開いてみてください。コマンド `cd ~` を入力して、Linux ホーム ディレクトリにいることを確認してください。 次に、以下を入力して、エクスプローラーで Linux ファイル システムを開きます " *(末尾のピリオドを忘れないでください)* ": `powershell.exe /c start .`

> [!IMPORTANT]
> エラー **-bash: powershell.exe: command not found** が発生した場合は、[WSL トラブルシューティング ページ](troubleshooting.md#running-windows-commands-fails-inside-a-distribution)を参照して解決してください。

WSL 2 は、Windows 10 (バージョン 1903、ビルド 18362 以上) でのみ使用できます。 Windows のバージョンを確認するには **Windows ロゴ キー + R** キーを押します。次に「**winver**」と入力し、 **[OK]** を選択します (または、Windows コマンド プロンプトで `ver` コマンドを入力します)。 [最新の Windows バージョンに更新する](ms-settings:windowsupdate)必要がある場合があります。 18362 より前のビルドでは、WSL はまったくサポートされていません。

> [!NOTE]
> WSL 2 は [VMware 15.5.5+](https://blogs.vmware.com/workstation/2020/05/vmware-workstation-now-supports-hyper-v-mode.html) と [VirtualBox 6+](https://www.virtualbox.org/wiki/Changelog-6.0) で動作します。 詳細については、[WSL 2 に関するよくあるご質問](./wsl2-faq.md#will-i-be-able-to-run-wsl-2-and-other-3rd-party-virtualization-tools-such-as-vmware-or-virtualbox)を参照してください。

## <a name="whats-new-in-wsl-2"></a>WSL 2 の新機能

WSL 2 では、基盤となるアーキテクチャの大きな見直しが行われ、新機能を有効にするために仮想化テクノロジと Linux カーネルが使用されています。 この更新の主な目標は、ファイル システムのパフォーマンスを向上させることと、システム コールの完全な互換性を追加することです。

- [WSL 2 のシステム要件](./install-win10.md#step-2---update-to-wsl-2)
- [WSL 1 から WSL 2 に更新する](./install-win10.md#step-2---update-to-wsl-2)
- [WSL 2 に関してよく寄せられる質問](./wsl2-faq.md)

### <a name="wsl-2-architecture"></a>WSL 2 のアーキテクチャ

従来の VM エクスペリエンスは起動に時間がかかり、分離され、大量のリソースが消費され、管理に時間がかかる場合があります。 WSL 2 にこのような特徴はありません。

WSL 2 には、Windows と Linux の間のシームレスな統合、高速な起動時間、小さなリソース フットプリントをはじめとする WSL 1 の利点があるうえ、VM の構成や管理が必要ありません。 WSL 2 には VM が使用されますが、バックグラウンドで管理および実行されるため、WSL 1 とユーザー エクスペリエンスは同じです。

### <a name="full-linux-kernel"></a>完全な Linux カーネル

WSL 2 の Linux カーネルは、kernel.org で入手できるソースに基づいて、最新の安定したブランチから Microsoft によって構築されています。このカーネルは WSL 2 向けに特別にチューニングされており、サイズとパフォーマンスの最適化によって Windows 上で優れた Linux エクスペリエンスが提供されます。 カーネルは、Windows の更新プログラムによって保守されます。つまり、自分で管理しなくても、最新のセキュリティ修正プログラムとカーネルの機能強化を利用できます。

[WSL 2 Linux カーネルはオープン ソースです](https://github.com/microsoft/WSL2-Linux-Kernel)。 詳細については、カーネルを構築したチームによって書かれたブログ投稿「[Windows に Linux カーネルを同梱する](https://devblogs.microsoft.com/commandline/shipping-a-linux-kernel-with-windows/)」を参照してください。

### <a name="increased-file-io-performance"></a>ファイル IO パフォーマンスの向上

WSL 2 を使用すると、git clone、npm install、apt update、apt upgrade などのあらゆるファイル集約型の操作が大きく高速化されます。

実際どのくらい高速になるかは、実行しているアプリと、ファイル システムとのやり取りの方法によって変わります。 初期バージョンの WSL 2 は、zip 圧縮された tarball を展開する場合、WSL 1 と比べて最大 20 倍速くなります。また、さまざまなプロジェクトで git clone、npm install、および cmake を使用する場合は、約 2 倍から 5 倍速くなります。

### <a name="full-system-call-compatibility"></a>システム コールの完全な互換性

Linux バイナリでは、システム コールを使用して、ファイルへのアクセス、メモリの要求、プロセスの作成などの機能を実行します。 WSL 1 では WSL チームが構築した変換レイヤーが使用されていましたが、WSL 2 にはシステム コールの完全な互換性を持つ独自の Linux カーネルが含まれています。 次のような利点があります。

- **[Docker](tutorials/wsl-containers.md)** など、WSL 内で実行できるまったく新しいアプリのセット。

- Linux カーネルに対する更新プログラムがすぐに使用可能になります (WSL チームが更新プログラムを実装して変更を追加するまで待つ必要はありません)。

### <a name="wsl-2-uses-a-smaller-amount-of-memory-on-startup"></a>WSL 2 は起動時のメモリ使用量が少ない

WSL 2 では、メモリ フットプリントが小さな実際の Linux カーネル上で軽量のユーティリティ VM を使用します。 このユーティリティは、仮想アドレスが使用されるメモリを起動時に割り当てます。 これは、WSL 1 で必要とされていたよりも少ない割合の合計メモリで起動するように構成されています。

## <a name="exceptions-for-using-wsl-1-rather-than-wsl-2"></a>例外的に WSL 2 ではなく WSL 1 を使用する場合

WSL2 ではより高速なパフォーマンスと 100% のシステム コールの互換性が提供されるため、WSL 2 を使用することをお勧めします。 ただし、WSL 1 を使用する方が好ましいシナリオもいくつかあります。 次の場合は、WSL 1 の使用を検討してください。

- プロジェクト ファイルを Windows ファイル システムに格納する必要がある。 WSL 1 を使用すると、Windows からマウントされたファイルにより高速にアクセスできます。
  - WSL Linux ディストリビューションを使用して Windows ファイル システム上のプロジェクト ファイルにアクセスする予定で、これらのファイルを Linux ファイル システムに格納できない場合は、WSL 1 を使用することにより、OS ファイル システム間でより高速なパフォーマンスを実現できます。
- 同じファイルに対して Windows と Linux の両方のツールを使用したクロスコンパイルを必要とするプロジェクト。
  - Windows オペレーティング システムと Linux オペレーティング システムの間のファイル パフォーマンスは WSL 1 の方が WSL 2 よりも高速です。そのため、Windows アプリケーションを使用して Linux ファイルにアクセスする場合、現時点では WSL 1 を使用する方がより高速なパフォーマンスを得られます。

> [!NOTE]
> VS Code [Remote WSL 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)を試すことを検討してください。Linux コマンド ライン ツールを使用してプロジェクト ファイルを Linux ファイル システム上に格納できるだけでなく、Windows 上で VS Code を使用して、インターネット ブラウザーでプロジェクトを作成、編集、デバッグ、実行できるようになります。Linux ファイル システムと Windows ファイル システムをまたぐ処理に伴うパフォーマンスの低下は発生しません。 [詳しくはこちらをご覧ください](tutorials/wsl-vscode.md)。

## <a name="accessing-network-applications"></a>ネットワーク アプリケーションへのアクセス

### <a name="accessing-linux-networking-apps-from-windows-localhost"></a>Windows からの Linux ネットワーク アプリへのアクセス (localhost)

Linux ディストリビューションでネットワーク アプリ (たとえば、Node.js または SQL Server で実行されるアプリ) を構築する場合、(通常の場合と同様に) `localhost` を使用して (Microsoft Edge または Chrome インターネット ブラウザーなどの) Windows アプリからアクセスすることができます。

ただし、Windows の古いバージョン (ビルド 18945 以下) を実行している場合は、Linux ホスト VM の IP アドレスを取得する (または[最新の Windows バージョンに更新する](ms-settings:windowsupdate)) 必要があります。

Linux ディストリビューションが動作する仮想マシンの IP アドレスを確認するには、次の手順に従います。

- WSL ディストリビューション (つまり、Ubuntu) から、次のコマンドを実行します: `ip addr`
- `eth0` インターフェイスの `inet` 値の下で目的のアドレスを見つけてコピーします。
- grep ツールがインストールされている場合は、次のコマンドを使用して出力をフィルター処理することにより、これをより簡単に見つけることができます: `ip addr | grep eth0`
- この IP アドレスを使用して Linux サーバーに接続します。

次の図は、これを実行するために、Edge ブラウザーを使用して Node.js サーバーに接続する例です。

![Edge を使用して NodeJS サーバーに接続する](media/wsl2-network-w2l.jpg)

### <a name="accessing-windows-networking-apps-from-linux-host-ip"></a>Linux からの Windows ネットワーク アプリへのアクセス (ホスト IP)

Linux ディストリビューション (つまり、Ubuntu) から Windows 上で実行されているネットワーク アプリ (たとえば、Node.js または SQL Server で実行されるアプリ) にアクセスする場合は、ホスト マシンの IP アドレスを使用する必要があります。 これは一般的なシナリオではありませんが、次の手順に従ってこれを実現できます。

1. Linux ディストリビューションから次のコマンドを実行して、ホスト マシンの IP アドレスを取得します: `cat /etc/resolv.conf`
2. 次の語句の後に IP アドレスをコピーします: `nameserver`。
3. コピーした IP アドレスを使用して、Windows サーバーに接続します。

次の図は、これを実行するために、curl を介して Windows で実行されている Node.js サーバーに接続する例です。

![Curl を介して Windows で NodeJS サーバーに接続する](media/wsl2-network-l2w.png)

### <a name="additional-networking-considerations"></a>ネットワークに関する追加の考慮事項

#### <a name="connecting-via-remote-ip-addresses"></a>リモート IP アドレスを使用した接続

リモート IP アドレスを使用してアプリケーションに接続すると、ローカル エリア ネットワーク (LAN) からの接続として扱われます。 これは、アプリケーションで LAN 接続を受け入れることができるようにする必要があることを意味します。

たとえば、場合によっては、`127.0.0.1` ではなく `0.0.0.0` にアプリケーションをバインドする必要があります。 Flask を使用する Python アプリの例では、次のコマンドを使用してこれを実行できます: `app.run(host='0.0.0.0')`。 これらの変更を行うと、LAN からの接続が許可されるため、セキュリティに注意してください。

#### <a name="accessing-a-wsl-2-distribution-from-your-local-area-network-lan"></a>ローカル エリア ネットワーク (LAN) からの WSL 2 ディストリビューションへのアクセス

WSL 1 ディストリビューションを使用している場合、LAN からアクセスできるようにコンピューターが設定されていれば、WSL で実行されているアプリケーションに LAN からもアクセスできます。

WSL 2 では、これは既定の動作ではありません。 WSL 2 には、独自の一意の IP アドレスを持つ仮想化されたイーサネット アダプターがあります。 現在、このワークフローを有効にするには、通常の仮想マシンの場合と同じ手順を実行する必要があります。 (Microsoft は、このエクスペリエンスを改善する方法を検討しています)。

次に、ホスト上のポート 4000 でリッスンし、それを IP アドレス 192.168.101.100 の WSL 2 VM のポート 4000 に接続するポート プロキシを追加する PowerShell コマンドの例を示します。

```powershell
netsh interface portproxy add v4tov4 listenport=4000 listenaddress=0.0.0.0 connectport=4000 connectaddress=192.168.101.100
```

#### <a name="ipv6-access"></a>IPv6 アクセス

WSL 2 ディストリビューションは、現在、IPv6 のみのアドレスに到達できません。 Microsoft は、この機能の追加に取り組んでいます。

## <a name="expanding-the-size-of-your-wsl-2-virtual-hard-disk"></a>WSL 2 仮想ハード ディスクのサイズの拡張

WSL 2 では、仮想ハード ディスク (VHD) を使用して Linux ファイルを格納します。 WSL 2 では、VHD は Windows ハード ディスク ドライブ上で *.vhdx* ファイルとして表されます。

WSL 2 VHD では、ext4 ファイル システムが使用されます。 この VHD は、ストレージのニーズに合わせて自動的にサイズが変更されます。初期の最大サイズは 256 GB です。 Linux ファイルで必要とされる記憶領域がこのサイズを超える場合は、拡張が必要になることがあります。 ディストリビューションが 256 GB を超えるサイズになると、ディスク領域が不足していることを示すエラーが表示されます。 このエラーは、VHD サイズを拡張することで修正できます。

256 GB を超えて VHD の最大サイズを拡張するには、次のようにします。

1. 次のコマンドを使用して、すべての WSL インスタンスを終了します: `wsl --shutdown`

2. ディストリビューションのインストール パッケージ名 ("PackageFamilyName") を見つけます
    - PowerShell を使用して、次のコマンドを入力します ("distro" はディストリビューション名です):
    - `Get-AppxPackage -Name "*<distro>*" | Select PackageFamilyName`

3. WSL 2 のインストールで使用される VHD ファイルの `fullpath` を特定します。これが `pathToVHD` になります。
     - `%LOCALAPPDATA%\Packages\<PackageFamilyName>\LocalState\<disk>.vhdx`

4. 次のコマンドを実行して、WSL 2 VHD のサイズを変更します。
   - 管理者特権で Windows コマンド プロンプトを開き、次のように入力します。

      ```powershell
      diskpart
      DISKPART> Select vdisk file="<pathToVHD>"
      DISKPART> detail vdisk
      ```

   - **detail** コマンドの出力を確認します。  出力には **[仮想サイズ]** の値が含まれます。  これは現在の最大値です。  この値を MB (メガバイト) に変換します。  サイズ変更した後の新しい値は、この値より大きくなければなりません。  たとえば、**detail** の出力に **[仮想サイズ:256 GB]** と示されている場合、**256000** より大きい値を指定する必要があります。  新しいサイズを MB (メガバイト) 単位にしたら、**diskpart** で次のコマンドを入力します。

      ```powershell
      DISKPART> expand vdisk maximum=<sizeInMegaBytes>
      ```

   - **diskpart** を終了します。

      ```powershell
      DISKPART> exit
      ```

5. WSL ディストリビューション (たとえば、Ubuntu) を起動します。

6. Linux ディストリビューションのコマンド ラインから次のコマンドを実行して、ファイル システムのサイズを拡張できることを WSL に認識させます。

   > [!NOTE]
   > 最初の **mount** コマンドへの応答として、 **/dev: none already mounted on /dev** というメッセージが表示されることがあります。  このメッセージは無視しても問題ありません。

   ```powershell
      sudo mount -t devtmpfs none /dev
      mount | grep ext4
   ```

   `/dev/sdX` のようなこのエントリの名前をコピーします (X は他の文字を表します)。  次の例では、**X** の値は **b** です。

   ```powershell
      sudo resize2fs /dev/sdb <sizeInMegabytes>M
   ```

   > [!NOTE]
   > **resize2fs** のインストールが必要になる場合があります。  その場合は、`sudo apt install resize2fs` というコマンドを使用してこれをインストールできます。

   出力は次のようになります。

   ```bash
      resize2fs 1.44.1 (24-Mar-2018)
      Filesystem at /dev/sdb is mounted on /; on-line resizing required
      old_desc_blocks = 32, new_desc_blocks = 38
      The filesystem on /dev/sdb is now 78643200 (4k) blocks long.
      ```

> [!NOTE]
> 通常、Windows ツールまたはエディターを使用して、AppData フォルダー内にある WSL 関連ファイルを変更、移動、またはアクセスしないでください。 そうすると、Linux ディストリビューションが破損する可能性があります。
