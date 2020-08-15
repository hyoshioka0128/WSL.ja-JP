---
title: WSL 2 と WSL 1 の比較
description: Linux 用 Windows サブシステムのバージョン 1 とバージョン 2 を比較します。 ヒント - バージョン 2 では、実際の Linux カーネルが実行され、パフォーマンスが向上し、より高速になりますが、Windows と Linux の両方のファイル システムで作業している場合は WSL 1 が適しています。
keywords: BashOnWindows, bash, wsl, windows, windowssubsystem, gnu, linux, ubuntu, debian, suse, windows 10, UX の変更, WSL 2, linux カーネル, ネットワーク アプリケーション, localhost, IPv6, 仮想ハードウェア ディスク, VHD, VHD の制限, VHD エラー
ms.date: 07/22/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: ea2c92030a895076be17ad2b99fe34719f84a47f
ms.sourcegitcommit: b494c8a76f867d69fa7fff4878c4e38140eaeb8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87235466"
---
# <a name="comparing-wsl-1-and-wsl-2"></a>WSL 1 と WSL 2 の比較

Linux 用 Windows サブシステムを新しいバージョンに更新する主な目的は、**ファイル システムのパフォーマンスを向上させ**、**システム コールの完全な互換性**をサポートすることです。 

軽量のユーティリティ仮想マシン (VM) 内で Linux カーネルを実行するために、WSL 2 には最新の優れた仮想化テクノロジが使用されています。 ただし、WSL 2 は従来の VM エクスペリエンスではありません。 [WSL 2 アーキテクチャの詳細については、こちらをご覧ください](#wsl-2-architecture)。

## <a name="comparing-features"></a>機能の比較

機能 | WSL 1 | WSL 2
--- | --- | ---
 Windows と Linux の統合| ✅|✅
 高速の起動時間| ✅ | ✅
 小さなリソース フット プリント| ✅ |✅
 現在のバージョンの VMware と VirtualBox での実行| ✅ | ✅
 マネージド VM| ❌ | ✅
 完全な Linux カーネル| ❌ |✅
 システム コールの完全な互換性| ❌ | ✅
 OS ファイル システム間でのパフォーマンス| ✅ | ❌

WSL 1 を既に使用していて、WSL 2 にアップグレードする場合は、 手順に従って [WSL 2 に更新](./install-win10.md#update-to-wsl-2)してください。

WSL 2 は、Windows 10、バージョン 2004、ビルド 19041 以上でのみ使用できます。 Windows のバージョンを確認するには **Windows キー + R** キーを押します。次に「**winver**」と入力し、 **[OK]** を選択します (または、Windows コマンド プロンプトで `ver` コマンドを入力します)。 [最新の Windows バージョンに更新する](ms-settings:windowsupdate)必要がある場合があります。 19041 より前のビルドでは、WSL はまったくサポートされていません。

> [!NOTE]
> WSL 2 は [VMWare 15.5.5+](https://blogs.vmware.com/workstation/2020/05/vmware-workstation-now-supports-hyper-v-mode.html) と [VirtualBox 6+](https://www.virtualbox.org/wiki/Changelog-6.0) で動作します。

## <a name="use-the-linux-file-system-for-faster-performance"></a>Linux ファイル システムを使用してパフォーマンスを向上させる

最速のパフォーマンス速度を実現するために最適化するには、プロジェクト ファイルを (Windows ファイル システムではなく) Linux ファイル システムに格納してください。

たとえば、WSL プロジェクト ファイルを格納する場合は、次のとおりです。

* Linux ファイル システムのルート ディレクトリを使用します: `\\wsl$\Ubuntu-18.04\home\<user name>\Project`
* Windows ファイル システムのルート ディレクトリではありません: `C:\Users\<user name>\Project`

WSL ディストリビューション (Ubuntu など) を使用して作業しているプロジェクト ファイルは、より高速なファイル システム アクセスを利用するために、Linux ルート ファイル システムに配置する必要があります。

Linux ルート ファイル システムには、エクスプローラーなどの Windows アプリやツールを使用してアクセスできます。 Linux ディストリビューション (Ubuntu など) を開いてみてください。また、次のコマンドを入力して、Linux ホーム ディレクトリにいることを確認してください: `cd ~`。 次に、以下を入力して、エクスプローラーで Linux ファイル システムを開きます " *(末尾のピリオドを忘れないでください)* ": `explorer.exe .`

## <a name="exceptions-for-using-wsl-1-rather-than-wsl-2"></a>例外的に WSL 2 ではなく WSL 1 を使用する場合

WSL2 ではより高速なパフォーマンスと 100% のシステム コールの互換性が提供されるため、WSL 2 を使用することをお勧めします。 ただし、WSL 1 を使用する方が好ましいシナリオもいくつかあります。 次の場合は、WSL 1 の使用を検討してください。

* プロジェクト ファイルを Windows ファイル システムに格納する必要がある。
  * WSL Linux ディストリビューションを使用して Windows ファイル システム上のプロジェクト ファイルにアクセスする予定で、これらのファイルを Linux ファイル システムに格納できない場合は、WSL 1 を使用することにより、OS ファイル システム間でより高速なパフォーマンスを実現できます。
* 同じファイルに対して Windows と Linux の両方のツールを使用したクロスコンパイルを必要とするプロジェクト。
  * Windows オペレーティング システムと Linux オペレーティング システムの間のファイル パフォーマンスは WSL 1 の方が WSL 2 よりも高速です。そのため、Windows アプリケーションを使用して Linux ファイルにアクセスする場合、現時点では WSL 1 を使用する方がより高速なパフォーマンスを得られます。

> [!NOTE]
> VS Code [Remote WSL 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)を試すことを検討してください。Linux コマンド ライン ツールを使用してプロジェクト ファイルを Linux ファイル システム上に格納できるだけでなく、Windows 上で VS Code を使用して、インターネット ブラウザーでプロジェクトを作成、編集、デバッグ、実行できるようになります。Linux ファイル システムと Windows ファイル システムをまたぐ処理に伴うパフォーマンスの低下は発生しません。 [詳しくはこちらをご覧ください](https://code.visualstudio.com/docs/remote/wsl)。

## <a name="wsl-2-architecture"></a>WSL 2 のアーキテクチャ

従来の VM エクスペリエンスは起動に時間がかかり、分離され、大量のリソースが消費され、管理に時間がかかります。 WSL 2 にこのような特徴はありません。

WSL 2 には、Windows と Linux の間のシームレスな統合、高速な起動時間、小さなリソース フットプリントをはじめとする WSL 1 の利点があるうえ、VM の構成や管理が必要ありません。 WSL 2 には VM が使用されますが、バックグラウンドで管理および実行されるため、WSL 1 とユーザー エクスペリエンスは同じです。

### <a name="full-linux-kernel"></a>完全な Linux カーネル

WSL 2 の Linux カーネルは、kernel.org で入手できるソースに基づいて、最新の安定したブランチから Microsoft によって構築されています。このカーネルは WSL 2 向けに特別にチューニングされており、サイズとパフォーマンスの最適化によって Windows 上で優れた Linux エクスペリエンスが提供されます。 カーネルは、Windows の更新プログラムによって保守されます。つまり、自分で管理しなくても、最新のセキュリティ修正プログラムとカーネルの機能強化を利用できます。

[WSL 2 Linux カーネルはオープン ソースです](https://github.com/microsoft/WSL2-Linux-Kernel)。 詳細については、カーネルを構築したチームによって書かれたブログ投稿「[Windows に Linux カーネルを同梱する](https://devblogs.microsoft.com/commandline/shipping-a-linux-kernel-with-windows/)」を参照してください。

### <a name="increased-file-io-performance"></a>ファイル IO パフォーマンスの向上

WSL 2 を使用すると、git clone、npm install、apt update、apt upgrade などのあらゆるファイル集約型の操作が大きく高速化されます。

実際どのくらい高速になるかは、実行しているアプリと、ファイル システムとのやり取りの方法によって変わります。 初期バージョンの WSL 2 は、zip 圧縮された tarball を展開する場合、WSL 1 と比べて最大 20 倍速くなります。また、さまざまなプロジェクトで git clone、npm install、および cmake を使用する場合は、約 2 倍から 5 倍速くなります。

### <a name="full-system-call-compatibility"></a>システム コールの完全な互換性

Linux バイナリでは、システム コールを使用して、ファイルへのアクセス、メモリの要求、プロセスの作成などの機能を実行します。 WSL 1 では WSL チームが構築した変換レイヤーが使用されていましたが、WSL 2 にはシステム コールの完全な互換性を持つ独自の Linux カーネルが含まれています。 次のような利点があります。

* **[Docker](https://code.visualstudio.com/blogs/2020/03/02/docker-in-wsl2)** など、WSL 内で実行できるまったく新しいアプリのセット。

* Linux カーネルに対する更新プログラムがすぐに使用可能になります (WSL チームが更新プログラムを実装して変更を追加するまで待つ必要はありません)。

### <a name="wsl-2-uses-a-smaller-amount-of-memory-on-startup"></a>WSL 2 は起動時のメモリ使用量が少ない

WSL 2 では、メモリ フットプリントが小さな実際の Linux カーネル上で軽量のユーティリティ VM を使用します。 このユーティリティは、仮想アドレスが使用されるメモリを起動時に割り当てます。 これは、WSL 1 で必要とされていたよりも少ない割合の合計メモリで起動するように構成されています。

## <a name="accessing-network-applications"></a>ネットワーク アプリケーションへのアクセス

### <a name="accessing-linux-networking-apps-from-windows-localhost"></a>Windows からの Linux ネットワーク アプリへのアクセス (localhost)

Linux ディストリビューションでネットワーク アプリ (たとえば、Node.js または SQL Server で実行されるアプリ) を構築する場合、(通常の場合と同様に) `localhost` を使用して (Microsoft Edge または Chrome インターネット ブラウザーなどの) Windows アプリからアクセスすることができます。

ただし、Windows の古いバージョン (ビルド 18945 以下) を実行している場合は、Linux ホスト VM の IP アドレスを取得する (または[最新の Windows バージョンに更新する](ms-settings:windowsupdate)) 必要があります。

Linux ディストリビューションが動作する仮想マシンの IP アドレスを確認するには、次の手順に従います。

* WSL ディストリビューション (つまり、Ubuntu) から、次のコマンドを実行します: `ip addr`
* `eth0` インターフェイスの `inet` 値の下で目的のアドレスを見つけてコピーします。
* grep ツールがインストールされている場合は、次のコマンドを使用して出力をフィルター処理することにより、これをより簡単に見つけることができます: `ip addr | grep eth0`
* この IP アドレスを使用して Linux サーバーに接続します。

次の図は、これを実行するために、Edge ブラウザーを使用して Node.js サーバーに接続する例です。

![Windows からの Linux ネットワーク アプリケーションへのアクセス](media/wsl2-network-w2l.jpg)

### <a name="accessing-windows-networking-apps-from-linux-host-ip"></a>Linux からの Windows ネットワーク アプリへのアクセス (ホスト IP)

Linux ディストリビューション (つまり、Ubuntu) から Windows 上で実行されているネットワーク アプリ (たとえば、Node.js または SQL Server で実行されるアプリ) にアクセスする場合は、ホスト マシンの IP アドレスを使用する必要があります。 これは一般的なシナリオではありませんが、次の手順に従ってこれを実現できます。
    - Linux ディストリビューションから次のコマンドを実行して、ホスト マシンの IP アドレスを取得します: `cat /etc/resolv.conf`
    - 次の語句の後に IP アドレスをコピーします: `nameserver`。
    - コピーした IP アドレスを使用して、Windows サーバーに接続します。

次の図は、これを実行するために、curl を介して Windows で実行されている Node.js サーバーに接続する例です。

![Windows からの Linux ネットワーク アプリケーションへのアクセス](media/wsl2-network-l2w.png)

### <a name="additional-networking-considerations"></a>ネットワークに関する追加の考慮事項

#### <a name="connecting-via-remote-ip-addresses"></a>リモート IP アドレスを使用した接続

リモート IP アドレスを使用してアプリケーションに接続すると、ローカル エリア ネットワーク (LAN) からの接続として扱われます。 これは、アプリケーションで LAN 接続を受け入れることができるようにする必要があることを意味します。

たとえば、場合によっては、`127.0.0.1` ではなく `0.0.0.0` にアプリケーションをバインドする必要があります。 Flask を使用する Python アプリの例では、次のコマンドを使用してこれを実行できます: `app.run(host='0.0.0.0')`。 これらの変更を行うと、LAN からの接続が許可されるため、セキュリティに注意してください。

#### <a name="accessing-a-wsl-2-distribution-from-your-local-area-network-lan"></a>ローカル エリア ネットワーク (LAN) からの WSL 2 ディストリビューションへのアクセス

WSL 1 ディストリビューションを使用している場合、LAN からアクセスできるようにコンピューターが設定されていれば、WSL で実行されているアプリケーションに LAN からもアクセスできます。

WSL 2 では、これは既定の動作ではありません。 WSL 2 には、独自の一意の IP アドレスを持つ仮想化されたイーサネット アダプターがあります。 現在、このワークフローを有効にするには、通常の仮想マシンの場合と同じ手順を実行する必要があります。 (Microsoft は、このエクスペリエンスを改善する方法を検討しています)。

#### <a name="ipv6-access"></a>IPv6 アクセス

WSL 2 ディストリビューションは、現在、IPv6 のみのアドレスに到達できません。 Microsoft は、この機能の追加に取り組んでいます。

## <a name="expanding-the-size-of-your-wsl-2-virtual-hardware-disk"></a>WSL 2 仮想ハードウェア ディスクのサイズの拡張

WSL 2 では、仮想ハードウェア ディスク (VHD) を使用して Linux ファイルを格納します。 場合によっては、その最大サイズに達したときにサイズを拡張する必要があります。

WSL 2 VHD では、ext4 ファイル システムが使用されます。 この VHD は、ストレージのニーズに合わせて自動的にサイズが変更されます。初期の最大サイズは 256 GB です。 ディストリビューションが 256 GB を超えるサイズになると、ディスク領域が不足していることを示すエラーが表示されます。 このエラーは、VHD サイズを拡張することで修正できます。

256 GB を超えて VHD の最大サイズを拡張するには、次のようにします。

1. 次のコマンドを使用して、すべての WSL インスタンスを終了します: `wsl --shutdown`

2. ディストリビューションのインストール パッケージ名 ("PackageFamilyName") を見つけます
    * PowerShell を使用して、次のコマンドを入力します ("distro" はディストリビューション名です):
    * `Get-AppxPackage -Name "*<distro>*" | Select PackageFamilyName`

3. WSL 2 のインストールで使用される VHD ファイルの `fullpath` を特定します。これが `pathToVHD` になります。
     * `%LOCALAPPDATA%\Packages\<PackageFamilyName>\LocalState\<disk>.vhdx`

4. 次のコマンドを実行して、WSL 2 VHD のサイズを変更します。
   * 管理者特権で Windows コマンド プロンプトを開き、次のように入力します。
      * `diskpart`
      * `Select vdisk file="<pathToVHD>"`
      * `expand vdisk maximum="<sizeInMegaBytes>"`

5. WSL ディストリビューション (たとえば、Ubuntu) を起動します。

6. Linux ディストリビューションのコマンド ラインから次のコマンドを実行して、ファイル システムのサイズを拡張できることを WSL に認識させます。
    * `sudo mount -t devtmpfs none /dev`
    * `mount | grep ext4`
    * `/dev/sdXX` のようなこのエントリの名前をコピーします (X は他の文字を表します)
    * `sudo resize2fs /dev/sdXX`
    * 前の手順でコピーした値を使用します。 resize2fs のインストールが必要になる場合もあります: `apt install resize2fs`

> [!NOTE]
> 通常、Windows ツールまたはエディターを使用して、AppData フォルダー内にある WSL 関連ファイルを変更、移動、またはアクセスしないでください。 そうすると、Linux ディストリビューションが破損する可能性があります。
