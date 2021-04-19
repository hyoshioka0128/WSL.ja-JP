---
title: WSL のリリース ノート
description: Linux 用 Windows サブシステムのリリース ノートをお読みください。 これらのリリースノートには、修正された問題が説明されており、毎週更新されます。
keywords: リリース ノート, wsl, windows, Linux 用 Windows サブシステム, windowssubsystem, ubuntu
author: benhillis
ms.date: 04/08/2021
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: 296c8bd76180cf7d465998d182d005ec5233182f
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493614"
---
# <a name="release-notes-for-windows-subsystem-for-linux"></a>Windows Subsystem for Linux のリリース ノート

## <a name="build-21354"></a>ビルド 21354
ビルド 21354 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windows-insider/2021/04/07/announcing-windows-10-insider-preview-build-21354/)を参照してください。

* \\wsl プレフィックスが \\wsl.localhost に切り替えられ、"wsl" という名前のネットワーク上にコンピューターがある場合に問題が発生しないようにします。 \\wsl$ は引き続き機能します。
* wow プロセスの Linux クイック アクセス アイコンが有効になります。
* wslapi RegisterDistribution を介して常にバージョン 2 が渡されていた問題が更新されます。
* /usr/lib/wsl/lib ディレクトリの fmask が 222 に変更され、ファイルが実行可能としてマークされます [GH 3847]
* 仮想マシン プラットフォームが有効になっていない場合の wsl サービスのクラッシュが修正されます。

## <a name="build-21286"></a>ビルド 21286
ビルド 21286 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windows-insider/2021/01/06/announcing-windows-10-insider-preview-build-21286/)を参照してください。

* コマンドの現在の作業ディレクトリを設定する wsl.exe --cd コマンドが導入されます。
* NTSTATUS から Linux エラー コードへのマッピングが改善されます。 [GH 6063]
* wsl.exe --mount のエラー報告が改善されます。
* /etc/wsl.conf にスタートアップ コマンドを有効にするオプションを追加しました:
```
[boot]
command=<string>
```

## <a name="build-20226"></a>ビルド 20226
ビルド 20226 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windows-insider/2020/09/30/announcing-windows-10-insider-preview-build-20226/)を参照してください。

* LxssManager サービスのクラッシュを修正します。 [GH 5902]

## <a name="build-20211"></a>ビルド 20211
ビルド 20211 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windows-insider/2020/09/10/announcing-windows-10-insider-preview-build-20211/)を参照してください。

* 物理ディスクや仮想ディスクをマウントするための `wsl.exe --mount` を導入します。 詳細については、「[Windows および WSL 2 で Linux ファイルシステムにアクセスする](https://devblogs.microsoft.com/commandline/access-linux-filesystems-in-windows-and-wsl-2/)」を参照してください。
* VM がアイドル状態であるかどうかを確認する際の LxssManager サービスのクラッシュを修正します。 [GH 5768]
* 圧縮された VHD ファイルのサポート。 [GH 4103]
* c:\windows\system32\lxss\lib にインストールされている Linux ユーザー モード ライブラリが、OS アップグレードの際に保持されるようにします。 [GH 5848]
* `wsl --install --list-distributions` を使用して、インストールできる利用可能なディストリビューションを一覧表示する機能が追加されました。
* WSL インスタンスは、ユーザーがログオフすると終了されるようになりました。

## <a name="build-20190"></a>ビルド 20190
ビルド 20190 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/08/12/announcing-windows-10-insider-preview-build-20190/)を参照してください。

* WSL1 インスタンスが起動できなくなるバグを修正します。 [GH 5633]
* Windows プロセスの出力をリダイレクトする際のハングを修正します。 [GH 5648]
* VM アイドル タイムアウトを制御するための %userprofile%\\.wslconfig オプションを追加します (wsl2.vmIdleTimeout=<time_in_ms>)。
* WSL からアプリの実行エイリアスを起動する操作をサポートします。
* WSL2 カーネルとディストリビューションをインストールするためのサポートが wsl.exe --install に追加されました。

## <a name="build-20175"></a>ビルド 20175
ビルド 20175 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/07/22/announcing-windows-10-insider-preview-build-20175/)を参照してください。

* WSL2 VM の既定のメモリ割り当てを、ホスト メモリの 50% または 8 GB のどちらか少ない方になるように調整します [GH 4166]。
* URI 解析をサポートするために、\\\\wsl$ プレフィックスを \\\\wsl に変更します。 従来の \\\\wsl$ パスも引き続きサポートされます。
* amd64 で、入れ子になった WSL2 の仮想化を既定で有効にします。 これは、%userprofile%\\.wslconfig で無効にできます ([wsl2] nestedVirtualization=false)。
* wsl.exe --update で、Microsoft Update の開始を要求します。
* DrvFs で読み取り専用ファイルの名前変更をサポートします。
* エラー メッセージが常に適切なコードページで出力されるようにします。

## <a name="build-20150"></a>ビルド 20150
ビルド 20150 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/06/17/announcing-windows-10-insider-preview-build-20150/)を参照してください。

* WSL2 GPU コンピューティングの場合、詳しくは、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/06/17/announcing-windows-10-insider-preview-build-20150/)を参照してください。
* WSL を簡単に設定できるように wsl.exe --install コマンド ライン オプションを導入します。
* WSL2 カーネルへの更新を管理するための wsl.exe --update コマンド ライン オプションを導入します。 
* WSL2 を既定値として設定します。
* WSL2 vm の正常なシャットダウン タイムアウトを増やします。
* デバイス メモリをマッピングするときの virtio-9p 競合状態を修正します。
* UAC が無効になっている場合は、昇格された 9p サーバーを実行しないでください。

## <a name="build-19640"></a>ビルド 19640
ビルド 19640 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/06/03/announcing-windows-10-insider-preview-build-19640/)を参照してください。

* [WSL2] virtio-9p (drvfs) の安定性が向上しました。

## <a name="build-19555"></a>ビルド 19555
ビルド 19555 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2020/01/30/announcing-windows-10-insider-preview-build-19555/)を参照してください。

* [WSL2] インストールおよび変換の操作によって使用されるメモリの量を制限するには、メモリ cgroup を使用します [GH 4669]
* 機能の検出機能を向上させるため、Linux 用 Windows サブシステムのオプションのコンポーネントが有効になっていない場合 wsl.exe を使用します
* WSL のオプションのコンポーネントがインストールされていない場合、wsl.exe を変更してヘルプ テキストを出力します
* インスタンス作成時の競合状態を修正します
* すべてのコマンド ライン機能を含む wslclient.dll を作成します
* LxssManagerUser サービスの停止中にクラッシュしないようにします
* distroName パラメーターが NULL の場合に wslapi.dll ファスト フェールを修正します

## <a name="build-19041"></a>ビルド 19041
ビルド 19041 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/12/10/announcing-windows-10-insider-preview-build-19041/)を参照してください。

* [WSL2] プロセスを起動する前にシグナル マスクをクリアします
* [WSL2] Linux カーネルを 4.19.84 に更新します
* symlink が非相対である場合に /etc/resolv.conf symlink の作成を処理します

## <a name="build-19028"></a>ビルド 19028
ビルド 19028 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/11/19/announcing-windows-10-insider-preview-build-19028/)を参照してください。

* [WSL2] Linux カーネルを 4.19.81 に更新します
* [WSL2] /dev/net/tun to 0666 の既定のアクセス許可を変更します [GH 4629]
* [WSL2] Linux VM に割り当てられた既定のメモリ容量を、ホスト メモリの80% に調整します
* [WSL2] タイムアウトがある要求を処理するように相互運用サーバーを修正し、不適切な呼び出し元がサーバーを切断できないようにします

## <a name="build-19018"></a>ビルド 19018
ビルド 19018 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/11/05/announcing-windows-10-insider-preview-build-19018/)を参照してください。

* [WSL2] 9p マウントの既定値として cache=mmap を使用して dotnet アプリを修正します
* [WSL2] localhost リレーの修正プログラム [GH 4340]
* [WSL2] ディストリビューション間で状態を共有するためにクロスディストリビューション共有の tmpfs マウントを導入
* \\\\wsl$ の永続ネットワーク ドライブを復元する修正

## <a name="build-19013"></a>ビルド 19013
ビルド 19013 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/10/29/announcing-windows-10-insider-preview-build-19013/)を参照してください。

* [WSL2] WSL ユーティリティ VM のメモリ パフォーマンスを向上します。 使用されなくなったメモリは解放されてホストに戻されます。
* [WSL2] カーネル バージョンを 4.19.79 に更新します。 (CONFIG_HIGH_RES_TIMERS、CONFIG_TASK_XACCT、CONFIG_TASK_IO_ACCOUNTING、CONFIG_SCHED_HRTICK、CONFIG_BRIDGE_VLAN_FILTERING を追加)。
* [WSL2] stdin が閉じていないパイプ ハンドルであるケースに対処するために入力リレーを修正します [GH 4424]
* \\\\wsl$ 大文字と小文字を区別しないかどうかの確認を行います。
```
[wsl2]
pageReporting = <bool>    # Enable or disable the free memory page reporting feature (default true).
idleThreshold = <integer> # Set the idle threshold for memory compaction, 0 disables the feature (default 1).
```

## <a name="build-19002"></a>ビルド 19002
ビルド 19002 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/10/17/announcing-windows-10-insider-preview-build-19002/)を参照してください。

* [WSL] 一部の Unicode 文字の処理に関する問題を修正します: https://github.com/microsoft/terminal/issues/2770
* [WSL] ビルド間のアップグレードの直後に起動すると、まれにディストリビューションが登録解除されるケースを修正します。
* [WSL] インスタンスのアイドル タイマーがキャンセルされない場合にシャットダウンする wsl.exe の問題を修正します。

## <a name="build-18995"></a>ビルド 18995
ビルド 18995 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/10/03/announcing-windows-10-insider-preview-build-18995/)を参照してください。

* [WSL2] 操作が中断された後に DrvFs マウントの動作が停止する問題を修正します (例: ctrl-c) [GH 4377]
* [WSL2] hvsocket メッセージが非常に多い場合の処理を修正します [GH 4105]
* [WSL2] stdin がファイルの場合の相互運用に関する問題を修正します [GH 4475]
* [WSL2] 予期しないネットワークの状態が検出されたときにサービスがクラッシュする問題を修正します [GH 4474]
* [WSL2] 現在のプロセスに環境変数がない場合は、相互運用サーバーからディストリビューションの名前を照会します
* [WSL2] stdin がファイルの場合の相互運用に関する問題を修正します
* [WSL2] Linux カーネル バージョンを 4.19.72 に更新します
* [WSL2] .wslconfig を使用して追加のカーネル コマンド ライン パラメーターを指定する機能を追加します
```
[wsl2]
kernelCommandLine = <string> # Additional kernel command line arguments
```

## <a name="build-18990"></a>ビルド 18990
ビルド 18990 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/09/24/announcing-windows-10-insider-preview-build-18990/)を参照してください。

* \\\\wsl$ のディレクトリの一覧のパフォーマンスを向上します
* [WSL2] 追加のブート エントロピーを挿入します [GH 4416]
* [WSL2] su または sudo を使用する場合の Windows の相互運用を修正します [GH 4465]

## <a name="build-18980"></a>ビルド 18980
ビルド 18980 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/09/11/announcing-windows-10-insider-preview-build-18980/)を参照してください。

* FILE_READ_DATA を拒否するシンボリック リンクの読み取りを修正します。 これには、"C:\Document and Settings" など、下位互換性のために Windows が作成するすべてのシンボリック リンクや、ユーザー プロファイル ディレクトリ内の一連のシンボリック リンクが含まれます
* 予期しないファイル システム状態を致命的ではないものとします [GH 4334、4305]
* [WSL2] CPU/ファームウェアで仮想化がサポートされている場合に、arm64 のサポートを追加します
* [WSL2] 特権のないユーザーがカーネル ログを表示することを許可します
* [WSL2] stdout/stderr のソケットが閉じられているときの出力リレーを修正します [GH 4375]
* [WSL2] バッテリーおよび AC アダプターのパススルーをサポートします
* [WSL2] Linux カーネルを 4.19.67 に更新します
* /Etc/wsl.conf に既定のユーザー名を設定する機能を追加します。
```
[user]
default=<string>
```

## <a name="build-18975"></a>ビルド 18975
ビルド 18975 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/09/06/announcing-windows-10-insider-preview-build-18975/)を参照してください。

* [WSL2] 複数の localhost の信頼性に関する問題を修正しました [GH 4340]

## <a name="build-18970"></a>ビルド 18970
ビルド 18970 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/08/29/announcing-windows-10-insider-preview-build-18970/)を参照してください。

* [WSL2] システムがスリープ状態から再開するときにホスト時刻と時刻を同期します [GH 4245]
* [WSL2] 可能な場合、Windows ボリュームに NT シンボリック リンクを作成します。
* [WSL2] UTS、IPC、PID、および Mount の各名前空間にディストリビューションを作成します。
* [WSL2] サーバーが localhost に直接バインドするときの localhost ポート リレーを修正します [GH 4353]
* [WSL2] 出力がリダイレクトされるときの相互運用を修正します [GH 4337]
* [WSL2] 絶対 NT シンボリック リンクの変換をサポートします。
* [WSL2] カーネルを 4.19.59 に更新します
* [WSL2] eth0 のサブネット マスクを正しく設定します。
* [WSL2] 終了イベントが通知されたときにコンソール ワーカー ループから抜け出すようにロジックを変更します。
* [WSL2] ディストリビューションが実行されていないときに、ディストリビューション VHD を取り出します。
* [WSL2] 空の値を正しく処理するように構成の解析ライブラリを修正します。
* [WSL2] クロス ディストリビューション マウントを作成することにより、Docker Desktop をサポートします。 /etc/wsl.conf ファイルに次の行を追加することにより、ディストリビューションはこの動作をオプトインできます。
```
[automount]
crossDistro = true
```

## <a name="build-18945"></a>ビルド 18945
ビルド 18945 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/07/26/announcing-windows-10-insider-preview-build-18945/)を参照してください。

### <a name="wsl"></a>WSL
* [WSL2] localhost:port を使用して、WSL2 のリスニング tcp ソケットにホストからアクセスできるようにします
* [WSL2] インストール/変換エラーの修正と、今後の問題を追跡するための追加の診断 [GH 4105] 
* [WSL2] WSL2 ネットワーク問題の診断能力を向上させます
* [WSL2] カーネル バージョンを 4.19.55 に更新します
* [WSL2] Docker に必要な構成オプションを使用してカーネルを更新します [GH 4165]
* [WSL2] ライトウェイト ユーティリティ VM に割り当てられる CPU の数を、ホストと同じになるように増やします (以前は、カーネル構成の CONFIG_NR_CPUS によって 8 個に制限されていました) [GH 4137]
* [WSL2] WSL2 ライトウェイト VM 用のスワップ ファイルを作成します
* [WSL2] \\\\wsl$\\distro (たとえば、sshfs) を使用してユーザー マウントを表示できるようにします [GH 4172]
* [WSL2] 9p ファイルシステムのパフォーマンスを改善します
* [WSL2] VHD ACL が無制限に拡張されないようにします [GH 4126]
* [WSL2] SquashFS と xt_conntrack をサポートするようにカーネル構成を更新します [GH 4107、4123]
* [WSL2] /etc/wsl.conf の interop.enabled オプションの修正 [GH 4140]
* [WSL2] ファイルシステムで EA がサポートされていない場合、ENOTSUP を返します
* [WSL2] \\\\wsl$ での CopyFile のハングを修正します
* 既定の umask を 0022 に切り替えて、filesystem.umask 設定を /etc/wsl.conf に追加します
* シンボリック リンクを正しく解決するように wslpath を修正します。これは、19h1 での不具合でした [GH 4078]
* WSL2 設定を調整するために %UserProfile%\\.wslconfig ファイルを導入します
```
[wsl2]
kernel=<path>              # An absolute Windows path to a custom Linux kernel.
memory=<size>              # How much memory to assign to the WSL2 VM.
processors=<number>        # How many processors to assign to the WSL2 VM.
swap=<size>                # How much swap space to add to the WSL2 VM. 0 for no swap file.
swapFile=<path>            # An absolute Windows path to the swap vhd.
localhostForwarding=<bool> # Boolean specifying if ports bound to wildcard or localhost in the WSL2 VM should be connectable from the host via localhost:port (default true).

# <path> entries must be absolute Windows paths with escaped backslashes, for example C:\\Users\\Ben\\kernel
# <size> entries must be size followed by unit, for example 8GB or 512MB
```

## <a name="build-18917"></a>ビルド 18917
ビルド 18917 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/06/12/announcing-windows-10-insider-preview-build-18917/)を参照してください。

### <a name="wsl"></a>WSL
* WSL 2 が利用可能になりました。 詳細については、[ブログ](https://devblogs.microsoft.com/commandline/wsl-2-is-now-available-in-windows-insiders/)を参照してください。
* シンボリック リンクを使用した Windows プロセスの起動が正常に機能しなかった不具合を修正します [GH 3999]
* wsl.exe --list --verbose、wsl.exe --list --quiet、および wsl.exe --import --version の各オプションを wsl.exe に追加します
* wsl.exe --shutdown オプションを追加します
* Plan 9:書き込みを成功させるためにディレクトリを開くことを許可します

## <a name="build-18890"></a>ビルド 18890
ビルド 18890 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/05/01/announcing-windows-10-insider-preview-build-18890/)を参照してください。

### <a name="wsl"></a>WSL
* ノンブロッキング ソケット リーク [GH 2913]
* ターミナルへの EOF 入力が後続の読み取りをブロックする可能性があります [GH 3421]
* wsl.conf を参照するように resolv.conf ヘッダーを更新します [GH 3928 で説明]
* epoll の delete コードでのデッドロック [GH 3922]
* --import および – export の引数のスペースを処理します [GH 3932]
* mmap を使用したファイルの拡張が正しく機能しません [GH 3939]
* ARM64 の \\\\wsl$ アクセスが正常に動作しないという問題を修正します
* wsl.exe 用のより適切な既定アイコンを追加します

## <a name="build-18342"></a>ビルド 18342
ビルド 18342 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/02/20/announcing-windows-10-insider-preview-build-18342/)を参照してください。

### <a name="wsl"></a>WSL
* ユーザーが Windows から WSL ディストリビューションの Linux ファイルにアクセスできるようにする機能を追加しました。 これらのファイルには、コマンド ラインを使用してアクセスできます。また、ファイル エクスプローラーや VSCode などの Windows アプリもこれらのファイルと対話できます。 \\\\wsl$\\<distro_name> に移動してファイルにアクセスするか、\\\\wsl$ に移動して実行中のディストリビューションの一覧を表示します。
* CPU 情報タグを追加し、Cpus_allowed[_list] の値を修正します [GH 2234]
* リーダー以外のスレッドからの exec をサポートします [GH 3800]
* 構成の更新エラーを致命的でないものとして処理します [GH 3785]
* オフセットを正しく処理するように binfmt を更新します [GH 3768]
* Plan 9 のネットワーク ドライブのマッピングを有効にします [GH 3854]
* バインド マウントのための Windows -> Linux および Linux -> Windows のパスの変換をサポートします
* 読み取り専用で開かれたファイルにマッピング用の読み取り専用セクションを作成します

## <a name="build-18334"></a>ビルド 18334
ビルド 18334 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2019/02/08/announcing-windows-10-insider-preview-build-18334/)を参照してください。

### <a name="wsl"></a>WSL
* Windows タイム ゾーンが Linux タイム ゾーンにマップされる方法を再設計します [GH 3747]
* メモリ リークを修正し、新しい文字列変換関数を追加します [GH 3746]
* スレッドがない threadgroup での SIGCONT は no-op です [GH 3741] 
* /proc/self/fd にソケットと epoll のファイル記述子を正しく表示します

## <a name="build-18305"></a>ビルド 18305
ビルド 18305 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/12/19/announcing-windows-10-insider-preview-build-18305/)を参照してください。

### <a name="wsl"></a>WSL
* プライマリ スレッドが終了すると、pthread はファイルへのアクセスを失います [GH 3589]
* 必要な場合を除き、TIOCSCTTY では "force" パラメーターが無視されます [GH 3652]
* wsl.exe コマンド ラインの機能強化と、インポート/エクスポートの機能の追加。
```
Usage: wsl.exe [Argument] [Options...] [CommandLine]

Arguments to run Linux binaries:

    If no command line is provided, wsl.exe launches the default shell.

    --exec, -e <CommandLine>
        Execute the specified command without using the default Linux shell.

    --
        Pass the remaining command line as is.

Options:
    --distribution, -d <DistributionName>
        Run the specified distribution.

    --user, -u <UserName>
        Run as the specified user.

Arguments to manage Windows Subsystem for Linux:

    --export <DistributionName> <FileName>
        Exports the distribution to a tar file.
        The filename can be - for standard output.

    --import <DistributionName> <InstallLocation> <FileName>
        Imports the specified tar file as a new distribution.
        The filename can be - for standard input.

    --list, -l [Options]
        Lists distributions.

        Options:
            --all
                List all distributions, including distributions that are currently
                being installed or uninstalled.

            --running
                List only distributions that are currently running.

    -setdefault, -s <DistributionName>
        Sets the distribution as the default.

    --terminate, -t <DistributionName>
        Terminates the distribution.

    --unregister <DistributionName>
        Unregisters the distribution.

    --upgrade <DistributionName>
        Upgrades the distribution to the WslFs file system format.

    --help
        Display usage information.
```

## <a name="build-18277"></a>ビルド 18277
ビルド 18277 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/11/07/announcing-windows-10-insider-preview-build-18277/)を参照してください。

### <a name="wsl"></a>WSL
* ビルド 18272 で発生した「そのようなインターフェイスはサポートされていません」というエラーを修正します [GH 3645]
* umount システム コールの MNT_FORCE フラグを無視します [GH 3605]
* 公式の CreatePseudoConsole API を使用するように WSL の相互運用を切り替えます
* FUTEX_WAIT の再起動時にタイムアウト値を保持しません

## <a name="build-18272"></a>ビルド 18272
ビルド18272の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/10/31/announcing-windows-10-insider-preview-build-18272/)を参照してください。

### <a name="wsl"></a>WSL
* **警告:** このビルドには、WSL を操作不能にする問題があります。 ディストリビューションを起動しようとすると、「そのようなインターフェイスはサポートされていません」というエラーが表示されます。 この問題は修正されており、次週の Insider Fast ビルドに組み込まれます。 このビルドをインストールした場合は、[設定] -> [更新とセキュリティ] -> [回復] を選択し、「前のバージョンの Windows 10 に戻す」を使用することで、前の Windows ビルドにロールバックできます。

## <a name="build-18267"></a>ビルド 18267
ビルド 18267 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/10/24/announcing-windows-10-insider-preview-build-18267/)を参照してください。

### <a name="wsl"></a>WSL
* ゾンビ プロセスが回収されず、無期限に存在し続ける問題を修正します。
* エラー メッセージが最大長を超えると、WslRegisterDistribution がハングします [GH 3592]
* DrvFs で読み取り専用ファイルに対して fsync を正常に実行できるようにします [GH 3556]
* 内部にシンボリック リンクを作成する前に /bin ディレクトリと /sbin ディレクトリが存在することを確認します [GH 3584]
* WSL インスタンスに対するインスタンス終了タイムアウト メカニズムを追加しました。 タイムアウトは現在 15 秒に設定されています。つまり、最後の WSL プロセスが終了してから 15 秒後にインスタンスが終了します。 ディストリビューションをすぐに終了するには、次を使用します。
```
wslconfig.exe /terminate <DistributionName>
```

## <a name="build-17763-1809"></a>ビルド 17763 (1809)
ビルド 17763 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/10/02/how-to-get-the-windows-10-october-2018-update/)を参照してください。

### <a name="wsl"></a>WSL
* Setpriority システム コールのアクセス許可チェックが厳しすぎて、同じスレッドの優先順位を変更できません [GH 1838]
* clock_gettime(CLOCK_BOOTTIME) に対して負値が返されないように、バイアスのかかっていない割り込み時間が起動時間に使用されていることを確認します [GH 3434]
* WSL binfmt インタープリターでシンボリック リンクを処理します [GH 3424]
* threadgroup リーダー ファイル記述子のクリーンアップの処理が改善されました。
* オーバーフローを回避するために、KeQueryPerformanceCounter ではなく KeQueryInterruptTimePrecise を使用するように WSL を切り替えます [GH 3252]
* Ptrace のアタッチにより、システム コールから無効な戻り値が返される場合があります [GH 1731]
* AF_UNIX に関連したいくつかの問題を修正します [GH 3371]
* 現在の作業ディレクトリが 5 文字未満の場合に WSL の相互運用が失敗する原因となる問題を修正します [GH 3379]
* 存在しないポートへのループバック接続の失敗による 1 秒間の遅延を回避します [GH 3286]
* /proc/sys/fs/file-max スタブ ファイルを追加します [GH 2893]
* より正確な IPV6 スコープ情報。
* PR_SET_PTRACER のサポート [GH 3053]
* エッジ トリガーされた epoll イベントをパイプ ファイルシステムが誤ってクリアします [GH 3276]
* NTFS シンボリック リンクによって起動された Win32 実行可能ファイルはシンボリック リンク名を考慮しません [GH 2909]
* ゾンビ サポートを強化しました [GH 1353]
* Windows の相互運用の動作を制御するための wsl.conf エントリを追加します [GH 1493]
  ```
    [interop]

    enabled=false # enable launch of Windows binaries; default is true

    appendWindowsPath=false # append Windows path to $PATH variable; default is true
  ```
* getsockname で必ずしも UNIX ソケット ファミリの種類が返されない問題を修正します [GH 1774]
* TIOCSTI のサポートを追加します [GH 1863]
* 接続処理中のノンブロッキング ソケットは、書き込み試行に対して EAGAIN を返します [GH 2846]
* マウントされた VHD での相互運用をサポートします [GH 3246、3291]
* ルート フォルダーでのアクセス許可チェックの問題を修正します [GH 3304]
* TTY キーボードの ioctl (KDGKBTYPE、KDGKBMODE、および KDSKBMODE) に対する制限付きサポート。
* Windows UI アプリは、バックグラウンドで起動された場合でも実行されます。
* wsl -u または --user オプションを追加します [GH 1203]
* 高速スタートアップが有効になっているときの WSL の起動問題を修正します [GH 2576]
* UNIX ソケットは切断されたピア資格情報を保持する必要があります [GH 3183]
* ノンブロッキング UNIX ソケットが EAGAIN で無限に失敗します [GH 3191]
* case=off が、drvfs マウントの新しい既定の種類です [GH 2937、3212、3328]
    * 詳細については、[ブログ](https://blogs.msdn.microsoft.com/commandline/2018/06/14/improved-per-directory-case-sensitivity-support-in-wsl/)を参照してください。
* 実行中のディストリビューションを停止するための wslconfig /terminate を追加します。
* スペースを含むパスを正しく処理しない WSL シェル コンテキスト メニュー エントリの問題を修正します。
* ディレクトリごとの大文字と小文字の区別を拡張属性として公開します
* ARM64: キャッシュのメンテナンス操作をエミュレートします。 [dotnet の問題](https://github.com/dotnet/core/issues/1561)を解決します。
* DrvFs: エスケープされた文字に対応するプライベート範囲内の文字のみをエスケープ解除します。
* ELF パーサー インタープリターの長さの検証での Off-by-one エラーを修正します [GH 3154]
* 過去の時刻が設定された WSL 絶対タイマーは起動しません [GH 3091]
* 新しく作成された再解析ポイントが、親ディレクトリにそのように表示されるようにします。
* DrvFs に大文字と小文字を区別するディレクトリをアトミックに作成します。
* ファイルが存在していてもマルチスレッドの操作で ENOENT が返される場合がある追加の問題を修正しました。 [GH 2712]
* UMCI が有効になっているときの WSL の起動エラーを修正しました。 [GH 3020]
* WSL を起動するエクスプローラーのコンテキスト メニューを追加します [GH 437、603、1836]。 使用するには、エクスプローラー ウィンドウで Shift キーを押しながら右クリックします。
* UNIX ソケットのノンブロッキング動作を修正します [GH 2822、3100]
* GH 2026 で報告されているように、ハングしている NETLINK コマンドを修正します。
* マウント伝達フラグのサポートを追加します [GH 2911]。
* truncate で INotify イベントが発生しない問題を修正します [GH 2978]。
* シェルを使用せずに 1 つのバイナリを呼び出す wsl.exe の --exec オプションを追加します。
* 特定のディストリビューションを選択する wsl.exe の --distribution オプションを追加します。
* dmesg の制限付きサポート。 アプリケーションは、dmesg にログを記録できるようになりました。 WSL ドライバーは、限られた情報を dmesg に記録します。 将来的には、ドライバーからのその他の情報や診断情報を伝達するように拡張できます。
    * 注: dmesg は、現在、`/dev/kmsg` デバイス インターフェイスを介してサポートされます。 `syslog` システム コール インターフェイスはまだサポートされていません。 そのため、一部の `dmesg` コマンド ラインのオプション (`-S`、`-C` など) は機能しません。
* ネイティブに一致するように、シリアル デバイスの既定の gid とモードを変更します [GH 3042]
* DrvFs で拡張属性がサポートされるようになりました。
    * 注: DrvFs では、拡張属性の名前にいくつかの制限があります。 一部の文字 ('/'、':'、'\*' など) は使用できません。また、DrvFs では拡張属性名の大文字と小文字は区別されません

## <a name="build-18252-skip-ahead"></a>ビルド 18252 (前へスキップ)
ビルド 18252 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/10/03/announcing-windows-10-insider-preview-build-18252/)を参照してください。

### <a name="wsl"></a>WSL
* init と bsdtar のバイナリを lxssmanager dll から別のツール フォルダーに移動します
* CLONE_FILES を使用しているときのファイル記述子の終了に関する競合を修正します
* DrvFs パスを変換するときに /proc/pid/mountinfo の省略可能なフィールドを処理します
* S_IFREG のメタデータのサポートなしに DrvFs mknod を正常に実行できるようにします
* DrvFs に作成される読み取り専用ファイルには readonly 属性セットが必要です [GH 3411]
* DrvFs のマウントを処理する /sbin/mount.drvfs ヘルパーを追加します
* DrvFs で POSIX rename を使用します。
* ボリューム GUID がないボリュームでのパスの変換を許可します。

## <a name="build-17738-fast"></a>ビルド 17738 (Fast)
ビルド 17738 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/08/14/announcing-windows-10-insider-preview-build-17738/)を参照してください。

### <a name="wsl"></a>WSL
* Setpriority システム コールのアクセス許可チェックが厳しすぎて、同じスレッドの優先順位を変更できません [GH 1838]
* clock_gettime(CLOCK_BOOTTIME) に対して負値が返されないように、バイアスのかかっていない割り込み時間が起動時間に使用されていることを確認します [GH 3434]
* WSL binfmt インタープリターでシンボリック リンクを処理します [GH 3424]
* threadgroup リーダー ファイル記述子のクリーンアップの処理が改善されました。

## <a name="build-17728-fast"></a>ビルド 17728 (Fast)
ビルド 17728 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/07/31/announcing-windows-10-insider-preview-build-17728/)を参照してください。

### <a name="wsl"></a>WSL
* オーバーフローを回避するために、KeQueryPerformanceCounter ではなく KeQueryInterruptTimePrecise を使用するように WSL を切り替えます [GH 3252]
* Ptrace のアタッチにより、システム コールから無効な戻り値が返される場合があります [GH 1731]
* AF_UNIX に関連した複数の問題を修正します [GH 3371]
* 現在の作業ディレクトリが 5 文字未満の場合に WSL の相互運用が失敗する原因となる問題を修正します [GH 3379]

## <a name="build-18204-skip-ahead"></a>ビルド 18204 (前へスキップ)
ビルド 18204 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/07/25/announcing-windows-10-insider-preview-build-17723-and-build-18204/)を参照してください。

### <a name="wsl"></a>WSL
* エッジ トリガーされた epoll イベントをパイプ ファイルシステムが誤ってクリアします [GH 3276]
* NTFS シンボリック リンクによって起動された Win32 実行可能ファイルはシンボリック リンク名を考慮しません [GH 2909]

## <a name="build-17723-fast"></a>ビルド 17723 (Fast)
ビルド 17723 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/07/25/announcing-windows-10-insider-preview-build-17723-and-build-18204/)を参照してください。

### <a name="wsl"></a>WSL
* 存在しないポートへのループバック接続の失敗による 1 秒間の遅延を回避します [GH 3286]
* /proc/sys/fs/file-max スタブ ファイルを追加します [GH 2893]
* より正確な IPV6 スコープ情報。
* PR_SET_PTRACER のサポート [GH 3053]
* エッジ トリガーされた epoll イベントをパイプ ファイルシステムが誤ってクリアします [GH 3276]
* NTFS シンボリック リンクによって起動された Win32 実行可能ファイルはシンボリック リンク名を考慮しません [GH 2909]

## <a name="build-17713"></a>ビルド 17713
ビルド 17713 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/07/11/announcing-windows-10-insider-preview-build-17713/)を参照してください。

### <a name="wsl"></a>WSL
* ゾンビ サポートを強化しました [GH 1353]
* Windows の相互運用の動作を制御するための wsl.conf エントリを追加します [GH 1493]
  ```
    [interop]

    enabled=false # enable launch of Windows binaries; default is true

    appendWindowsPath=false # append Windows path to $PATH variable; default is true
  ```
* getsockname で必ずしも UNIX ソケット ファミリの種類が返されない問題を修正します [GH 1774]
* TIOCSTI のサポートを追加します [GH 1863]
* 接続処理中のノンブロッキング ソケットは、書き込み試行に対して EAGAIN を返します [GH 2846]
* マウントされた VHD での相互運用をサポートします [GH 3246、3291]
* ルート フォルダーでのアクセス許可チェックの問題を修正します [GH 3304]
* TTY キーボードの ioctl (KDGKBTYPE、KDGKBMODE、および KDSKBMODE) に対する制限付きサポート。
* Windows UI アプリは、バックグラウンドで起動された場合でも実行されます。

## <a name="build-17704"></a>ビルド 17704
ビルド 17704 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/06/27/announcing-windows-10-insider-preview-build-17704/)を参照してください。

### <a name="wsl"></a>WSL
* wsl -u または --user オプションを追加します [GH 1203]
* 高速スタートアップが有効になっているときの WSL の起動問題を修正します [GH 2576]
* UNIX ソケットは切断されたピア資格情報を保持する必要があります [GH 3183]
* ノンブロッキング UNIX ソケットが EAGAIN で無限に失敗します [GH 3191]
* case=off が、drvfs マウントの新しい既定の種類です [GH 2937、3212、3328]
    * 詳細については、[ブログ](https://blogs.msdn.microsoft.com/commandline/2018/06/14/improved-per-directory-case-sensitivity-support-in-wsl/)を参照してください。
* 実行中のディストリビューションを停止するための wslconfig /terminate を追加します。

## <a name="build-17692"></a>ビルド 17692
ビルド 17692 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/06/14/announcing-windows-10-insider-preview-build-17692)を参照してください。

### <a name="wsl"></a>WSL
* スペースを含むパスを正しく処理しない WSL シェル コンテキスト メニュー エントリの問題を修正します。
* ディレクトリごとの大文字と小文字の区別を拡張属性として公開します
* ARM64: キャッシュのメンテナンス操作をエミュレートします。 [dotnet の問題](https://github.com/dotnet/core/issues/1561)を解決します。
* DrvFs: エスケープされた文字に対応するプライベート範囲内の文字のみをエスケープ解除します。

## <a name="build-17686"></a>ビルド 17686
ビルド 17686 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/06/06/announcing-windows-10-insider-preview-build-17686)を参照してください。

### <a name="wsl"></a>WSL
* ELF パーサー インタープリターの長さの検証での Off-by-one エラーを修正します [GH 3154]
* 過去の時刻が設定された WSL 絶対タイマーは起動しません [GH 3091]
* 新しく作成された再解析ポイントが、親ディレクトリにそのように表示されるようにします。
* DrvFs に大文字と小文字を区別するディレクトリをアトミックに作成します。

## <a name="build-17677"></a>ビルド 17677
ビルド 17677 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/05/24/announcing-windows-10-insider-preview-build-17677/)を参照してください。

### <a name="wsl"></a>WSL
* ファイルが存在していてもマルチスレッドの操作で ENOENT が返される場合がある追加の問題を修正しました。 [GH 2712]
* UMCI が有効になっているときの WSL の起動エラーを修正しました。 [GH 3020]

## <a name="build-17666"></a>ビルド 17666
ビルド 17666 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/05/09/announcing-windows-10-insider-preview-build-17666/)を参照してください。

### <a name="wsl"></a>WSL
#### <a name="warning-there-is-an-issue-preventing-wsl-from-running-on-some-amd-chipsets-gh-3134-a-fix-is-ready-and-making-its-way-to-the-insider-build-branch"></a>警告:一部の AMD チップセットに WSL の実行を妨げる問題があります [GH 3134]。 修正は準備できており、間もなく Insider ビルド ブランチで公開されます。
* WSL を起動するエクスプローラーのコンテキスト メニューを追加します [GH 437、603、1836]。 使用するには、エクスプローラー ウィンドウで Shift キーを押しながら右クリックします。
* UNIX ソケットのノンブロッキング動作を修正します [GH 2822、3100]
* GH 2026 で報告されているように、ハングしている NETLINK コマンドを修正します。
* マウント伝達フラグのサポートを追加します [GH 2911]。
* truncate で INotify イベントが発生しない問題を修正します [GH 2978]。
* シェルを使用せずに 1 つのバイナリを呼び出す wsl.exe の --exec オプションを追加します。
* 特定のディストリビューションを選択する wsl.exe の --distribution オプションを追加します。

## <a name="build-17655-skip-ahead"></a>ビルド 17655 (前へスキップ)
ビルド 17655 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/04/25/announcing-windows-10-insider-preview-build-17655-for-skip-ahead/)を参照してください。

### <a name="wsl"></a>WSL
* dmesg の制限付きサポート。 アプリケーションは、dmesg にログを記録できるようになりました。 WSL ドライバーは、限られた情報を dmesg に記録します。 将来的には、ドライバーからのその他の情報や診断情報を伝達するように拡張できます。
    * 注: 現在、dmesg は `/dev/kmsg` デバイス インターフェイスを介してサポートされています。 `syslog` システム コール インターフェイスはまだサポートされていません。 そのため、一部の `dmesg` コマンド ラインのオプション (`-S`、`-C` など) は機能しません。
* ファイルが存在している場合でもマルチスレッドの操作で ENOENT が返される場合がある問題を修正しました。 [GH 2712]

## <a name="build-17639-skip-ahead"></a>ビルド 17639 (前へスキップ)
ビルド 17639 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/04/04/announcing-windows-10-insider-preview-build-17639-for-skip-ahead/)を参照してください。

### <a name="wsl"></a>WSL
* ネイティブに一致するように、シリアル デバイスの既定の gid とモードを変更します [GH 3042]
* DrvFs で拡張属性がサポートされるようになりました。
    * 注: DrvFs では、拡張属性の名前にいくつかの制限があります。 特に、一部の文字 ('/'、':'、'\*' など) は使用できません。また、拡張属性名は DrvFs では大文字と小文字が区別されません

## <a name="build-17133-fast"></a>ビルド 17133 (Fast)
ビルド 17133 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/03/27/announcing-windows-10-insider-preview-build-17133-for-fast/)を参照してください。

### <a name="wsl"></a>WSL
* WSL でのハングの修正。 [GH 3039、3034]

## <a name="build-17128-fast"></a>ビルド 17128 (Fast)
ビルド 17128 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/03/23/announcing-windows-10-insider-preview-build-17128-for-fast/)を参照してください。

### <a name="wsl"></a>WSL
* None

## <a name="build-17627-skip-ahead"></a>ビルド 17627 (前へスキップ)
ビルド 17627 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/03/21/announcing-windows-10-insider-preview-build-17627-for-skip-ahead/)を参照してください。

### <a name="wsl"></a>WSL
* futex の pi 対応操作のサポートを追加します。 [GH 1006]
    * 優先順位は現在サポートされている WSL 機能ではないため、制限がありますが、標準の使用はブロック解除する必要がある点に留意してください。
* WSL プロセスに対する Windows ファイアウォールのサポート。 [GH 1852]
    * たとえば、WSL python プロセスが任意のポートでリッスンできるようにするには、次の管理者特権の Windows コマンドを使用します: ```netsh.exe advfirewall firewall add rule name=wsl_python dir=in action=allow program="C:\users\<username>\appdata\local\packages\canonicalgrouplimited.ubuntuonwindows_79rhkp1fndgsc\localstate\rootfs\usr\bin\python2.7" enable=yes```
    * ファイアウォール規則を追加する方法の詳細については、[リンク](https://support.microsoft.com/help/947709/how-to-use-the-netsh-advfirewall-firewall-context-instead-of-the-netsh)を参照してください。
* WSL を使用するときにユーザーの既定のシェルを考慮します。 [GH 2372]
* すべてのネットワーク インターフェイスをイーサネットとして報告します。 [GH 2996]
* 破損した /etc/passwd ファイルの処理が改善。 [GH 3001]

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17618-skip-ahead"></a>ビルド 17618 (前へスキップ)
ビルド 17618 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/03/07/announcing-windows-10-insider-preview-build-17618-skip-ahead/)を参照してください。

### <a name="wsl"></a>WSL
* NT 相互運用のために pseudoconsole 機能を導入します [GH 988、1366、1433、1542、2370、2406]。
* レガシ インストール メカニズム (lxrun.exe) は非推奨となりました。 ディストリビューションをインストールするためのサポートされているメカニズムは、Microsoft Store 経由です。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17110"></a>ビルド 17110
ビルド 17110 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/02/27/announcing-windows-10-insider-preview-build-17110-fast/)を参照してください。

### <a name="wsl"></a>WSL
* /init を Windows から終了することを許可します [GH 2928]。
* DrvFs では、ディレクトリごとの大文字小文字の区別が既定で使用されるようになりました ("case = dir" マウント オプションと同等)。
    * "case=force" (以前の動作) を使用するには、レジストリ キーを設定する必要があります。 "case=force" を使用する必要がある場合は、次のコマンドを実行して有効にします: reg add HKLM\SYSTEM\CurrentControlSet\Services\lxss /v DrvFsAllowForceCaseSensitivity /t REG_DWORD /d 1
    * 以前のバージョンの Windows に含まれている WSL で作成された既存のディレクトリがあり、大文字と小文字を区別する必要がある場合は、次の fsutil.exe を使用して大文字と小文字を区別するように指定します: fsutil.exe file setcasesensitiveinfo <path> enable
* uname システム コールから NULL の終了文字列が返されます。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17107"></a>ビルド 17107
ビルド 17107 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/02/23/announcing-windows-10-insider-preview-build-17107-fast-ring/)を参照してください。

### <a name="wsl"></a>WSL
* マスター pty エンドポイントで TCSETSF と TCSETSW をサポートします [GH 2552]。
* 相互運用プロセスを同時に開始すると、EINVAL が発生します [GH 2813]。
* /proc/pid/status に適切なトレース状態を表示するように PTRACE_ATTACH を修正します。
* CLEARTID フラグと SETTID フラグの両方を指定して複製された、有効期間の短いプロセスが、TID アドレスをクリアせずに終了する場合がある競合を修正します。
* 17093 より前のビルドから移行するときに、Linux ファイルシステムのディレクトリをアップグレードする際にメッセージを表示します。 17093 のファイルシステムの変更について詳しくは、[17093](https://github.com/MicrosoftDocs/WSL/blob/live/WSL/release-notes.md#build-17093) のリリース ノートを参照してください。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17101"></a>ビルド 17101
ビルド 17101 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/02/14/announcing-windows-10-insider-preview-build-17101-fast-build-17604-skip-ahead/)を参照してください。

### <a name="wsl"></a>WSL
* signalfd のサポート。 [GH 129]
* 無効な NTFS 文字を含むファイル名を、プライベート Unicode 文字としてエンコードすることによってサポートします。 [GH 1514]
* 書き込みがサポートされていない場合、自動マウントは読み取り専用にフォールバックします。 [GH 2603]
* Unicode サロゲート ペア (絵文字など) の貼り付けを許可します。 [GH 2765]
* /proc および /sys 内の疑似ファイルは、select、poll、epoll などから、読み書き可能を返します。[GH 2838]
* レジストリが改ざんされているか破損している場合にサービスが無限ループに入る原因となる問題を修正します。
* iproute2 の新しい (アップストリーム 4.14) バージョンで機能するように netlink メッセージを修正します。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17093"></a>ビルド 17093
ビルド 17093 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)を参照してください。

#### <a name="important"></a>重要:
このビルドにアップグレードした後に初めて WSL を開始するときに、Linux ファイルシステムのディレクトリをアップグレードする作業を実行する必要があります。 この処理には数分かかる場合があるため、WSL の開始に時間がかかっているように見えることがあります。 これは、ストアからインストールされた各ディストリビューションにつき 1 回のみ発生します。
* DrvFs での大文字と小文字の区別のサポートを改善しました。
    * DrvFs では、ディレクトリごとの大文字小文字の区別がサポートされるようになりました。 これは、ディレクトリに設定できる新しいフラグで、これらのディレクトリ内のすべての操作を大文字と小文字を区別して扱う必要があることを示します。これにより、Windows アプリケーションでも、大文字と小文字のみが異なるファイルを正しく開くことが可能になります。
    * DrvFs には、ディレクトリごとに大文字と小文字の区別を制御する新しいマウント オプションがあります
        * case=force: すべてのディレクトリは、大文字小文字を区別して処理されます (ドライブのルートを除く)。 WSL で作成された新しいディレクトリは、大文字と小文字が区別されます。 これは、新しいディレクトリに大文字小文字を区別するようにマークを付けることを除き、従来の動作です。
        * case=dir: ディレクトリごとの大文字小文字の区別フラグを持つディレクトリのみが、大文字と小文字を区別して扱われます。他のディレクトリでは、大文字と小文字は区別されません。 WSL で作成された新しいディレクトリは、大文字と小文字が区別されます。
        * case=off: ディレクトリごとの大文字小文字の区別フラグを持つディレクトリのみが、大文字と小文字を区別して扱われます。他のディレクトリでは、大文字と小文字は区別されません。 WSL で作成された新しいディレクトリは、大文字と小文字を区別しないようにマークが付けられます。
    * 注: 以前のリリースの WSL によって作成されたディレクトリにはこのフラグが設定されていないため、"case=dir" オプションを使用しても、大文字と小文字を区別して処理されません。 既存のディレクトリにこのフラグを設定する方法は、近日公開予定です。
    * これらのオプションを使用したマウントの例 (既存のドライブの場合、別のオプションを使用してマウントする前にマウントを解除する必要があります): sudo mount -t drvfs C: /mnt/c -o case=dir
    * 現時点では、case=force がまだ既定のオプションです。 これは将来、case=dir に変更されます。
* DrvFs をマウントするときに Windows パスでスラッシュを使用できるようになりました。例: sudo mount -t drvfs //server/share /mnt/share
* WSL は、インスタンスの開始時に /etc/fstab ファイルを処理するようになりました [GH 2636]。
    * これは、DrvFs ドライブを自動的にマウントする前に行われます。fstab によって既にマウントされているドライブは自動的には再マウントされないため、特定のドライブのマウント ポイントを変更することができます。
    * この動作は、wsl.conf を使用して無効にすることができます。
* /proc 内の mount、mountinfo、および mountstats の各ファイルは、円記号やスペースなどの特殊文字を正しくエスケープ処理します [GH 2799]
* WSL シンボリック リンクなどの DrvFs で作成された特殊ファイル、またはメタデータが有効になっている場合の FIFO やソケットを、Windows からコピーおよび移動できるようになりました。

#### <a name="wsl-is-more-configurable-with-wslconf"></a>WSL は、wsl.conf を使用してさらに構成可能です
サブシステムを起動するたびに適用される WSL の特定の機能を自動的に構成するための方法を追加しました。 これには自動マウント オプションとネットワーク構成が含まれます。 詳細については、次のブログ投稿を参照してください: https://aka.ms/wslconf

#### <a name="af_unix-allows-socket-connections-between-linux-processes-on-wsl-and-windows-native-processes"></a>AF_UNIX により、WSL 上の Linux プロセスと Windows ネイティブ プロセス間のソケット接続が可能になります
WSL と Windows のアプリケーションは、UNIX ソケット経由で相互に通信できるようになりました。 Windows でサービスを実行し、それを Windows と WSL の両方のアプリで使用できるようにする場合を考えてみましょう。 これは、UNIX ソケットを使用することで可能になりました。 詳細については、次のブログ投稿をお読みください: https://aka.ms/afunixinterop

### <a name="wsl"></a>WSL
* MAP_NORESERVE で mmap() をサポートします [GH 121、2784]
* CLONE_PTRACE と CLONE_UNTRACED をサポートします [GH 121、2781]
* 複製で SIGCHLD 以外の終了シグナルを処理します [GH 121、2781]
* /proc/sys/fs/inotify/max_user_instances および /proc/sys/fs/inotify/max_user_watches をスタブします [GH 1705]
* ゼロ以外のオフセットの読み込みヘッダーを含む ELF バイナリの読み込みエラー [GH 1884]
* イメージを読み込むときにページの末尾バイトをゼロ設定します。
* execve が警告なしにプロセスを終了するケースを削減します

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17083"></a>ビルド 17083
ビルド 17083 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/01/24/announcing-windows-10-insider-preview-build-17083-for-pc/)を参照してください。

### <a name="wsl"></a>WSL
* epoll に関連したバグチェックを修正しました [GH 2798、2801、2857]
* ASLR をオフにする際のハングを修正しました [GH 1185, 2870]
* mmap 操作がアトミックに見えるようにします [GH 2732]

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17074"></a>ビルド 17074
ビルド 17074 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2018/01/11/announcing-windows-10-insider-preview-build-17074-pc/)を参照してください。

### <a name="wsl"></a>WSL
* DrvFs メタデータのストレージ形式を修正しました [GH 2777] </br>
**重要:** このビルドより前に作成された DrvFs メタデータは、正しく表示されないか、まったく表示されません。 影響を受けるファイルを修正するには、chmod と chown を使用してメタデータを再適用します。
* 複数のシグナルと再開可能なシステム コールの問題を修正しました。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17063"></a>ビルド 17063
ビルド 17063 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-windows-10-insider-preview-build-17063-pc/)を参照してください。

### <a name="wsl"></a>WSL
* DrvFs で追加の Linux メタデータがサポートされます。 これにより、chmod/chown を使用してファイルの所有者とモードを設定できるほか、FIFO、UNIX ソケット、デバイス ファイルなどの特殊ファイルを作成することも可能になります。 現時点では、これはまだ試験段階のため、既定では無効になっています。
**注:** DrvFs で使用されるメタデータ形式のバグを修正しました。 メタデータは実験のためにこのビルドでは機能しますが、今後のビルドでは、このビルドで作成されたメタデータは正しく読み取られません。  変更したファイルの所有者を手動で更新する必要がある場合があり、カスタム デバイス ID を持つデバイスは再作成しなければなりません。

  有効にするには、メタデータ オプションを使用して DrvFs をマウントします (既存のマウントで有効にするには、最初にマウントを解除する必要があります)。

  ```bash
  mount -t drvfs C: /mnt/c -o metadata
  ```

  Linux のアクセス許可は、追加のメタデータとしてファイルに追加されます。Windows のアクセス許可には影響はありません。  Windows エディターを使用してファイルを編集すると、メタデータが削除されることがありますので注意してください。 この場合、そのファイルは既定のアクセス許可に戻ります。

* メタデータなしでファイルを制御するためのマウント オプションを DrvFs に追加しました。
  * uid: 全ファイルの所有者に使用されるユーザー ID。
  * gid: 全ファイルの所有者に使用されるグループ ID。
  * umask: 全ファイルとディレクトリに対して除外するアクセス許可の 8 進数のマスク。
  * fmask: すべての標準ファイルに対して除外するアクセス許可の 8 進数のマスク。
  * dmask: 全ディレクトリに対して除外するアクセス許可の 8 進数のマスク。

  たとえば、次のように入力します。
  ```
  mount -t drvfs C: /mnt/c -o uid=1000,gid=1000,umask=22,fmask=111
  ```

  メタデータ オプションと組み合わせて、メタデータのないファイルに対する既定のアクセス許可を指定します。

* WSL と Win32 の間で環境変数がどのように流れるかを構成するために、新しい環境変数 `WSLENV` を導入しました。

  たとえば、次のように入力します。

  ``` bash
  WSLENV=GOPATH/l:USERPROFILE/pu:DISPLAY
  ```

  `WSLENV` は、Win32 から WSL プロセスを起動するとき、または WSL から Win32 プロセスを起動するときに含めることができる環境変数のコロン区切りリストです。  各変数の末尾にはスラッシュを付け、その後に、変換方法を指定するフラグを指定できます。
  * p:この値は、WSL パスと Win32 パスの間で変換されるパスです。
  * l:この値は、パスのリストです。 WSL では、コロンで区切られたリストです。 Win32 では、セミコロンで区切られたリストです。
  * u:この値は、Win32 から WSL を呼び出すときにのみ含める必要があります
  * w:この値は、WSL から Win32 を呼び出すときにのみ含める必要があります

  .bashrc またはユーザーのカスタム Windows 環境で `WSLENV` を設定できます。

* drvfs マウントは、tar、cp -p からのタイムスタンプを正しく保持します (GH 1939)
* drvfs シンボリック リンクは正しいサイズを報告します (GH 2641)
* 非常に大きい IO サイズに対して読み取り/書き込みが機能します (GH 2653)
* waitpid はプロセス グループ ID で機能します (GH 2534)
* 大きな予約領域での mmap のパフォーマンスが大幅に改善しました。ghc のパフォーマンスが改善します (GH 1671)
* READ_IMPLIES_EXEC のパーソナリティ サポート。maxima および clisp を修正します (GH 1185)
* mprotect で PROT_GROWSDOWN がサポートされます。clisp を修正します (GH 1128)
* オーバーコミット モードでのページ フォールトの修正。sbcl の修正 (GH 1128)
* clone でより多くのフラグの組み合わせがサポートされます
* epoll ファイルの select/epoll をサポートします (以前は操作なし)。
* 未実装のシステム コールの ptrace を通知します。
* resolv.conf ネームサーバーを生成しているときに実行されていないインターフェイスを無視します [GH 2694]
* 物理アドレスのないネットワーク インターフェイスを列挙します。 [GH 2685]
* その他のバグ修正と機能強化。

### <a name="linux-tools-available-to-developers-on-windows"></a>開発者は Windows 上で Linux ツールを利用できるようになりました

* Windows コマンド ライン ツールチェーンに、bsdtar (tar) と curl が含まれます。
  これらの 2 つの新しいツールの追加に関する詳細と、それを使った Windows での開発者エクスペリエンスの形成については、[こちらのブログ](https://aka.ms/tarcurlwindows)を参照してください。

*   `AF_UNIX` は、Windows Insider SDK (17061+) で利用可能です。
  `AF_UNIX` の詳細と、Windows 上で開発者がそれをどのように使用できるかについては、[こちらのブログ](https://blogs.msdn.microsoft.com/commandline/2017/12/19/af_unix-comes-to-windows/)をお読みください。

### <a name="console"></a>コンソール
* 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。


## <a name="build-17046"></a>ビルド 17046

ビルド 17046 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/11/22/announcing-windows-10-insider-preview-build-17046-pc)を参照してください。

### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- アクティブ ターミナルなしでプロセスの実行を許可します。 [GH 709、1007、1511、2252、2391 など]
- CLONE_VFORK および CLONE_VM のサポートの強化。 [GH 1878、2615]
- WSL ネットワーク操作で TDI フィルター ドライバーをスキップします。 [GH 1554]
- DrvFs は、特定の条件に適合したときに NT シンボリック リンクを作成します。 [GH 353、1475、2602]
    - リンク対象は、相対パスである必要があり、マウント ポイントやシンボリック リンクと交差してはならず、存在している必要があります。
    - 開発者モードが有効になっていない場合、ユーザーは SE_CREATE_SYMBOLIC_LINK_PRIVILEGE を持っている必要があります (このためには、通常、管理者特権で wsl.exe を起動する必要があります)。
    - それ以外の状況でも、DrvFs は WSL シンボリック リンクを作成します。
- 管理者特権と非管理者特権での WSL インスタンスの同時実行を許可します。
- /proc/sys/kernel/yama/ptrace_scope をサポートします
- WSL<->Windows のパスの変換を実行するために wslpath を追加します。 [GH 522、1243、1834、2327 など]
  ```
    wslpath usage:
      -a    force result to absolute path format
      -u    translate from a Windows path to a WSL path (default)
      -w    translate from a WSL path to a Windows path
      -m    translate from a WSL path to a Windows path, with '/' instead of '\\'

      EX: wslpath 'c:\users'
  ```
  #### <a name="console"></a>コンソール
- 修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。


## <a name="build-17040"></a>ビルド 17040

ビルド 17040 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/11/16/announcing-windows-10-insider-preview-build-17040-pc)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- 17035 以降修正なし。

#### <a name="console"></a>コンソール
- 17035 以降修正なし。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17035"></a>ビルド 17035

ビルド 17035 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/11/08/announcing-windows-10-insider-preview-build-17035-pc)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- DrvFs 上のファイルにアクセスすると、時々 EINVAL で失敗することがあります。 [GH 2448]

#### <a name="console"></a>コンソール
- VT モードで行を挿入または削除するときに一部の色が失われます。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17025"></a>ビルド 17025

ビルド 17025 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/10/25/announcing-windows-10-insider-preview-build-17025-pc)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- 新しいフォアグラウンド プロセス グループで初期プロセスを開始します [GH 1653、2510]。
- SIGHUP 配信の修正 [GH 2496]。
- 指定されていない場合、既定の仮想ブリッジ名を生成します [GH 2497]。
- /proc/sys/kernel/random/boot_id を実装します [GH 2518]。
- 追加の相互運用 stdout/stderr パイプの修正。
- syncfs システム コールをスタブします。

#### <a name="console"></a>コンソール
- サード パーティ コンソールの入力 VT 変換を修正します [GH 111]

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="build-17017"></a>ビルド 17017

ビルド 17017 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/10/13/announcing-windows-10-insider-preview-build-17017-pc)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- 空の ELF プログラム ヘッダーを無視します [GH 330]。
- LxssManager が非対話型ユーザーに対して WSL インスタンスを作成することを許可します (ssh およびスケジュールされたタスクのサポート) [GH 777、1602]。
- WSL->Win32-> WSL ("開始") シナリオをサポートします [GH 1228]。
- 相互運用によって起動されたコンソール アプリの終了に対する制限付きサポート [GH 1614]。
- devpts のマウント オプションをサポートします [GH 1948]。
- Ptrace が子のスタートアップをブロックします [GH 2333].
- EPOLLET で一部のイベントが欠落します [GH 2462].
- PTRACE_GETSIGINFO でより多くのデータが返されます。
- lseek を指定した Getdents により、誤った結果が生成されます。
- これ以上データがないパイプで入力を待機することによる、いくつかの Win32 相互運用アプリのハングを修正します。
- tty/pty ファイルに対する O_ASYNC サポート。
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
テストを実行中。

## <a name="fall-creators-update"></a>Fall Creators Update

## <a name="build-16288"></a>ビルド 16288

ビルド 16288 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/09/12/announcing-windows-10-insider-preview-build-16288-pc-build-15250-mobile/#7pLWQbj23JisfzV5.97/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- ソケット ファイル記述子の uid、gid、およびモードを正しく初期化して報告します [GH 2490]
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
16273 以降変更はありません

## <a name="build-16278"></a>ビルド 16278

ビルド 162738 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/08/29/announcing-windows-10-insider-preview-build-16278-pc/#HMz6Xq7Su68WKi0t.97/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- LX MM 状態を解除するときに、ファイルによってサポートされているセクションのマップされたビューを明示的にマップ解除します [GH 2415]
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
16273 以降変更はありません

## <a name="build-16275"></a>ビルド 16275

ビルド 162735 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/08/25/announcing-windows-10-insider-preview-build-16275-pc-build-15245-mobile/#8QkxWqQbY37yZslV.97/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- このリリースでは、WSL に関連する変更はありません。

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
16273 以降変更はありません

## <a name="build-16273"></a>ビルド 16273

ビルド 16273 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/08/23/announcing-windows-10-insider-preview-build-16273-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- DrvFs がディレクトリに対して間違ったファイルの種類を報告することがあった問題を修正しました [GH 2392]
- uevent を使用するプログラムのブロックを解除するために NETLINK_KOBJECT_UEVENT ソケットの作成を許可します [GH 1121、2293、2242、2295、2235、648、637]
- ノンブロッキング接続のサポートを追加します [GH 903、1391、1584、1585、1829、2290、2314]
- CLONE_FS clone システム コール フラグを実装します [GH 2242]
- NT 相互運用でタブや引用符が正しく処理されないことに関する問題を修正します [GH 1625、2164]
- WSL インスタンスを再起動しようとしたときにアクセスが拒否されるエラーを解決します [GH 651、2095]
- futex の FUTEX_REQUEUE 操作と FUTEX_CMP_REQUEUE 操作を実装します [GH 2242]
- さまざまな SysFs ファイルのアクセス許可を修正します [GH 2214]
- セットアップ中の Haskell スタックのハングを修正します [GH 2290]
- binfmt_misc の 'C'、'O'、および 'P' のフラグを実装します [GH 2103]
- /proc/sys/kernel /shmmax /shmmni & /threads-max を追加します [GH 1753]
- ioprio_set システム コールの部分的サポートを追加します [GH 498]
- SO_REUSEPORT をスタブし、netlink ソケットに対する SO_PASSCRED のサポートを追加します [GH 69]
- ディストリビューションを現在インストールまたはアンインストールしている場合に、RegisterDistribuiton から別のエラー コードが返されます。
- wslconfig.exe によって部分的にインストールされた WSL ディストリビューションの登録解除を許可します
- udp::msg_peek からの python ソケット テストのハングを修正します
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
テストの合計:1904<br/>
スキップされたテストの合計:209<br/>
失敗の合計:229<br/>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/16273)<br/>

## <a name="build-16257"></a>ビルド 16257

ビルド 16257 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/08/02/announcing-windows-10-insider-preview-build-16257-pc-build-15237-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- prlimit64 システム コールを実装します
- ulimit -n (setrlimit RLIMIT_NOFILE) に対するサポートを追加します [GH 1688]
- TCP ソケットに対して MSG_MORE をスタブします [GH 2351]
- 無効な AT_EXECFN 補助ベクトルの動作を修正します [GH 2133]
- console/tty のコピー/貼り付けの動作を修正し、改善された完全バッファー処理を追加します [GH 2204、2131]
- set-user-ID プログラムと set-group-ID プログラムの補助ベクトルに AT_SECURE を設定します [GH 2031]
- 疑似ターミナルのマスター エンドポイントが TIOCPGRP を処理しません [GH 1063]
- LxFs でのディレクトリの巻き戻しについて lseek を修正します [GH 2310]
- 高い使用率の後に /dev/ptmx がロックします [GH 1882]
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- すべての場所での横線とアンダースコアの修正 [GH 2168]
- プロセス順序の変更により NPM のクローズが困難になった問題の修正 [GH 2170]
- 新しいカラー スキームを追加しました: https://blogs.msdn.microsoft.com/commandline/2017/08/02/updating-the-windows-console-colors/

### <a name="ltp-results"></a>LTP の結果:
16251 以降変更はありません

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`prlimit64`<br/>

### <a name="known-issues"></a>の既知の問題
#### <a name="github-issue-2392-windows-folders-not-recognized-by-wsl-"></a>[GitHub の問題 2392:Windows フォルダーが WSL によって認識されない...](https://github.com/Microsoft/BashOnWindows/issues/2392)
ビルド 16257 で、WSL には、`/mnt/c/...` を介して Windows ファイル/フォルダーを列挙するときに問題があります。
この問題は修正済みであり、2017 年 8 月 14 日から始まる週の間に Insiders ビルドでリリースされます。

<br/>

## <a name="build-16251"></a>ビルド 16251

ビルド 16251 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/07/26/announcing-windows-10-insider-preview-build-16251-pc-build-15235-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- WSL のオプション コンポーネントからベータ タグを削除します。詳細については、[ブログ投稿](https://blogs.msdn.microsoft.com/commandline/2017/07/28/windows-subsystem-for-linux-out-of-beta/)を参照してください。
- exec で set-user-ID と set-group-ID のバイナリに対して保存されている set uid と gid を正しく初期化します [GH 962、1415、2072]
- ptrace PTRACE_O_TRACEEXIT に対するサポートを追加しました [GH 555]
- ptrace PTRACE_GETFPREGS と PTRACE_GETREGSET (NT_FPREGSET を使用) に対するサポートを追加しました [GH 555]
- 無視されたシグナルでの停止について ptrace を修正しました
- その他の機能強化とバグ修正

#### <a name="console"></a>コンソール
- このリリースでは、コンソールに関連する変更はありません。

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:768</br>
失敗したテストの数:244</br>
スキップされたテストの数:96</br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/16251)<br/>

</br>

## <a name="build-16241"></a>ビルド 16241

ビルド 16241 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/07/13/announcing-windows-10-insider-preview-build-16241-pc-build-15230-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
#### <a name="wsl"></a>WSL
- このリリースでは、WSL に関連する変更はありません。

#### <a name="console"></a>コンソール
- [こちら](https://www.reddit.com/r/Windows10/comments/6in82t/i_believe_ive_found_the_most_obscure_bug_ever/)で最初に報告された、交差行の DEC に対して誤った文字が出力されることの修正
- コード ページ 65001 (utf8) に出力テキストが表示されないことの修正
- ある色の RGB 値に対して行われた変更を、選択の変更時にパレットの他の部分に転送しないでください。 これにより、コンソール プロパティ シートがずっと使いやすくなります。
- Ctrl+S が正しく機能していないように見えます
- Un-Bold/-Dim が ANSI エスケープ コードにまったく存在しません [GH 2174]
- コンソールで Vim の色のテーマが正しくサポートされていません [GH 1706]
- 特定の文字を貼り付けられません [GH 2149]
- 編集/コマンド ライン上に存在するときに、bash ウィンドウのサイズ変更で、サイズ変更のリフローの操作が正しく行われません [GH ConEmu 1123]
- Ctrl-L を押しても画面はダーティな状態のままです [GH 1978]
- HDPI に VT を表示する際のコンソール レンダリングのバグ [GH 1907]
- Unicode 文字 U+30FB で日本語の文字が正しく表示されません [GH 2146]
- その他の機能強化とバグ修正

</br>

## <a name="build-16237"></a>ビルド 16237

ビルド 16237 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/07/07/announcing-windows-10-insider-preview-build-16237-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定
- LxFs で EA がないファイルには既定の属性を使用します (root、root、0000)
- 拡張属性を使用するディストリビューションのサポートを追加しました
- getdents と getdents64 によって返されるエントリのパディングを修正します
- shmctl SHM_STAT システム コールのアクセス許可チェックを修正します [GH 2068]
- tty の正しくない初期 epoll 状態を修正しました [GH 2231]
- DrvFs readdir ですべてのエントリが返されない問題を修正します [GH 2077]
- ファイルのリンクが解除されているときの LxFs readdir を修正します [GH 2077]
- リンクが解除されている drvfs ファイルを procfs を介して再オープンできるようにします
- WSL の機能を無効にするためのグローバル レジストリ キー オーバーライドを追加しました (相互運用/ドライブのマウント)
- DrvFs (および LxFs) の "stat" での間違ったブロック カウントを修正します [GH 1894]
- その他の機能強化とバグ修正

</br>

## <a name="build-16232"></a>ビルド 16232

ビルド 16232 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/06/28/announcing-windows-10-insider-preview-build-16232-pc-build-15228-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- このリリースでは、WSL に関連する変更はありません。

</br>

## <a name="build-16226"></a>ビルド 16226

ビルド 16226 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/06/21/announcing-windows-10-insider-preview-build-16226-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定
- xattr に関連したシステム コールのサポート (getxattr、setxattr、listxattr、removexattr)。
- security.capablity xattr のサポート。
- 特定のファイルシステムとフィルター (MS 以外の SMB サーバーを含む) との互換性を改善しました。 [GH #1952]
- OneDrive プレースホルダー、GVFS プレースホルダー、および Compact OS 圧縮ファイルのサポートを強化しました。
- その他の機能強化とバグ修正

</br>

## <a name="build-16215"></a>ビルド 16215

ビルド 16215 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/06/08/announcing-windows-10-insider-preview-build-16215-pc-build-15222-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- WSL で開発者モードが不要になりました。
- drvfs でディレクトリ ジャンクションをサポートします。
- WSL ディストリビューション appx パッケージのアンインストールを処理します。
- プライベート マッピングと共有マッピングを表示するように procfs を更新します。
- 部分的にインストールまたはアンインストールされたディストリビューションをクリーンアップする wslconfig.exe の機能を追加します。
- TCP ソケットに対する IP_MTU_DISCOVER のサポートを追加しました。 [GH 1639、2115、2205]
- AF_INADDR へのルート用のプロトコル ファミリを推測します。
- シリアル デバイスの機能強化 [GH 1929]。

</br>

## <a name="build-16199"></a>ビルド 16199

ビルド 16199 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/05/17/announcing-windows-10-insider-preview-build-16199-pc-build-15215-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- これらのリリースでは、WSL に関連する変更はありません。

</br>

## <a name="build-16193"></a>ビルド 16193

ビルド 16193 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/05/11/announcing-windows-10-insider-preview-build-16193-pc-build-15213-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- SIGCONT の送信と threadgroup の終了との間の競合状態 [GH 1973]
- FILE_DEVICE_CONSOLE ではなく FILE_DEVICE_NAMED_PIPE を報告するように tty デバイスと pty デバイスを変更します [GH 1840]
- IP_OPTIONS の SSH 修正
- DrvFs のマウントを init デーモンに移動しました [GH 1862、1968、1767、1933]
- 後続の NT シンボリック リンクに対するサポートを DrvFs に追加しました。

</br>

## <a name="build-16184"></a>ビルド 16184

ビルド 16184 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/04/28/announcing-windows-10-insider-preview-build-16184-pc-build-15208-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- apt パッケージのメンテナンス タスク (lxrun.exe/update) を削除しました
- Node.js の Windows プロセスから出力が表示されない問題を修正しました [GH 1840]
- lxcore での配置要件を緩和します [GH 1794]
- 複数のシステム コールで AT_EMPTY_PATH フラグの処理を修正しました。
- 開いているハンドルがある DrvFs ファイルを削除するとファイルで未定義の動作が示される問題を修正しました [GH 544、966、1357、1535、1615]
- /etc/hosts は、Windows hosts ファイルからエントリを継承するようになりました (%windir%\system32\drivers\etc\hosts) [GH 1495]

</br>

## <a name="build-16179"></a>ビルド 16179

ビルド 16179 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/04/19/announcing-windows-10-insider-preview-build-16179-pc-build-15205-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- 今週は、WSL の変更はありません。

</br>

## <a name="build-16176"></a>ビルド 16176

ビルド 16176 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/04/14/announcing-windows-10-insider-preview-build-16176-pc-build-15204-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定

- [シリアル サポートを有効にしました](/archive/blogs/wsl/serial-support-on-the-windows-subsystem-for-linux)
- IP ソケット オプション IP_OPTIONS を追加しました [GH 1116]
- (nginx/PHP-FPM にファイルをアップロード中に) pwritev 関数を実装しました [GH 1506]
- IP ソケット オプション IP_MULTICAST_IF および IPV6_MULTICAST_IF を追加しました [GH 990]
- ソケット オプション IP_MULTICAST_LOOP および IPV6_MULTICAST_LOOP に対するサポート [GH 1678]
- apps node、traceroute、dig、nslookup、host に対する IP(V6)_MTU ソケット オプションを追加しました
- IP ソケット オプション IPV6_UNICAST_HOPS を追加しました
- [ファイルシステムの機能強化](/archive/blogs/wsl/file-system-improvements-to-the-windows-subsystem-for-linux)
    * UNC パスのマウントを許可します
    * drvfs で CDFS のサポートを有効にします
    * drvfs でネットワーク ファイル システムのアクセス許可を正しく処理します
    * drvfs へのリモート ドライブのサポートを追加します
    * drvfs で FAT のサポートを有効にします
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果
15042 以降変更はありません

</br>

## <a name="build-16170"></a>ビルド 16170

ビルド 16170 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/04/07/announcing-windows-10-insider-preview-build-16170-pc/)を参照してください。<br/>

WSL のテストに関する取り組みを説明する新しい[ブログ投稿](/archive/blogs/wsl/testing-the-windows-subsystem-for-linux)をリリースしました。

### <a name="fixed"></a>固定

- ソケット オプション IP_ADD_MEMBERSHIP および IPV6_ADD_MEMBERSHIP をサポートします [GH 1678]
- PTRACE_OLDSETOPTIONS のサポートを追加します。 [GH 1692]
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果
15042 以降変更はありません

</br>

## <a name="build-15046-to-windows-10-creators-update"></a>ビルド 15046 から Windows 10 Creators Update まで
Windows 10 の Creators Update への組み込みが予定されている WSL の修正または機能はこれ以上ありません。 WSL のリリース ノートは、次回の主要な Windows Update をターゲットとする追加に向けて、今後数週間のうちに再開されます。 ビルド 15046 の一般的な Windows 情報および今後の Insider リリースについては、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/02/28/announcing-windows-10-insider-preview-build-15046-pc/)を参照してください。 <br/><br/>
 <br/>

## <a name="build-15042"></a>ビルド 15042

ビルド 15042 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/02/24/announcing-windows-10-insider-preview-build-15042-pc-build-15043-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定

- ".." で終わるパスを削除する際のデッドロックの修正
- FIONBIO が成功時に 0 を返さないという問題を修正しました [GH 1683]
- inet データグラム ソケットの長さゼロの読み取りの問題を修正しました
- drvfs inode 参照での競合状態が原因で発生する可能性があるデッドロックを修正します [GH 1675]
- UNIX ソケット補助データに対する拡張サポート、SCM_CREDENTIALS および SCM_RIGHTS [GH 514、613、1326]
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:737</br>
不合格の数 (失敗した、スキップしたなど):255

</br>

## <a name="build-15031"></a>ビルド 15031

ビルド 15031 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/02/08/announcing-windows-10-insider-preview-build-15031-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

- time(2) が散発的に不適切な動作をするバグを修正しました。
- *SIGPROCMASK システム コールによってシグナル マスクが破損する問題を修正しました。
- WSL プロセス作成通知で完全な長さのコマンド ラインが返されるようになりました。 [GH 1632]
- WSL は、GDB のハングについて ptrace を介してスレッドの終了を報告するようになりました。 [GH 1196]
- tmux の IO が大量に行われた後に ptys がハングするバグを修正しました。 [GH 1358]
- 複数のシステム コール (futex、semtimedop、ppoll、sigtimedwait、itimer、timer_create) でタイムアウトの検証を修正しました
- eventfd EFD_SEMAPHORE のサポートを追加しました [GH 452]
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:737</br>
不合格の数 (失敗した、スキップしたなど):255 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15031)<br/>

<br/>

## <a name="build-15025"></a>ビルド 15025

ビルド 15025 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/02/01/announcing-windows-10-insider-preview-build-15025-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

- grep 2.27 を破損したバグの修正 [GH 1578]
- eventfd2 システム コールに対して EFD_SEMAPHORE フラグを実装しました [GH 452]
- /proc/[pid]/net/ipv6_route を実装しました [GH 1608]
- Unix ストリーム ソケットに対するシグナル駆動型 IO のサポート [GH 393、68]
- F_GETPIPE_SZ および F_SETPIPE_SZ をサポートします [GH 1012]
- recvmmsg() システム コールを実装します [GH 1531]
- epoll_wait() が待機していなかったというバグを修正しました [GH 1609]
- /proc/version_signature を実装
- Tee システム コールは、両方のファイル記述子が同じパイプを参照している場合にエラーを返すようになりました
- UNIX ソケットに対する SO_PEERCRED の正しい動作を実装しました
- tkill システム コールの無効なパラメーター処理を修正しました
- drvfs のパフォーマンスを向上させるための変更
- Ruby の IO ブロックに対する軽微な修正
- inet ソケットの MSG_DONTWAIT フラグに対して recvmsg() が EINVAL を返すという問題を修正しました [GH 1296]
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:732</br>
不合格の数 (失敗した、スキップしたなど):255 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15025)<br/>

<br/>

## <a name="build-15019"></a>ビルド 15019

ビルド 15019 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/01/27/announcing-windows-10-insider-preview-build-15019-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

- htop などのツールに対して procfs で CPU 使用量が誤って報告されるバグを修正しました (GH 823、945、971)
- 既存のファイルに対して O_TRUNC を使用して open () を呼び出すと、inotify は IN_OPEN の前に IN_MODIFY を生成するようになりました
- Postgress を有効にするための UNIX ソケット getsockopt SO_ERROR に対する修正 [GH 61、1354]
- GO 言語に対して /proc/sys/net/core/somaxconn を実装します
- Apt-get パッケージ更新のバックグラウンド タスクは、非表示で実行されるようになりました
- ipv6 localhost のスコープをクリアします (Spring-Framework(Java) エラー)。
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:714 </br>
不合格の数 (失敗した、スキップしたなど):249 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15019)<br/>

<br/>

## <a name="build-15014"></a>ビルド 15014

ビルド 15014 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/01/19/announcing-windows-10-insider-preview-build-15014-for-pc-and-mobile-hello-windows-insiders-today-we-are-excited-to-be-releasing-windows-10-insider-preview-build-15014-for-pc-and-mobile)を参照してください。<br/>


### <a name="fixed"></a>固定

- Ctrl+C は意図したとおりに動作するようになりました
- htop と ps auxw は正しいリソース使用量を表示するようになりました (GH #516)
- NT 例外からシグナルへの基本的な変換。 (GH #513)
- fallocate は、領域が不足しているときに、EINVAL ではなく ENOSPC で失敗するようになりました (GH #1571)
- /proc/sys/kernel/sem を追加します。
- semop システム コールと semtimedop システム コールを実装しました
- IP_RECVTOS および IPV6_RECVTCLASS ソケット オプションでの nslookup エラーを修正しました (GH 69)
- ソケット オプション IP_RECVTTL および IPV6_RECVHOPLIMIT に対するサポート
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:709 </br>
不合格の数 (失敗した、スキップしたなど):255 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15014)<br/>

### <a name="syscall-summary"></a>システム コールの概要
システム コールの合計:384 </br>
実装の合計:235 </br>
スタブの合計:22 </br>
未実装の合計:127 </br>
[詳細な内訳](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15014/Syscalls.txt)<br/>

<br/>

## <a name="build-15007"></a>ビルド 15007

ビルド 15007 の一般的な Windows 情報については、[Windows ブログ]( https://blogs.windows.com/windowsexperience/2017/01/12/announcing-windows-10-insider-preview-build-15007-pc-mobile)を参照してください。<br/>


### <a name="known-issue"></a>既知の問題

- コンソールが一部の Ctrl + <key> 入力を認識しないという既知のバグがあります。  これには、通常の "c" キーが押されたものとして機能する ctrl-c コマンドが含まれます。

  - 対応策 :代替キーを Ctrl+C にマップします。 たとえば、Ctrl+K を Ctrl+C にマップするには、`stty intr \^k` を実行します。  このマッピングはターミナルごとに行い、*毎回* bash が起動されるたびに実行する必要があります。 ユーザーはオプションを探索し、これを `.bashrc` に含めることができます。

### <a name="fixed"></a>固定

- 実行中の WSL が CPU コアの 100% を消費するという問題を修正しました
- ソケット オプション IP_PKTINFO、IPV6_RECVPKTINFO がサポートされるようになりました。 (GH #851、987)
- lxcore でネットワーク インターフェイスの物理アドレスが 16 バイトに切り捨てられます (GH #1452、1414、1343、468、308)
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:709 </br>
不合格の数 (失敗した、スキップしたなど):255 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15007)<br/>

<br/>

## <a name="build-15002"></a>ビルド 15002

ビルド 15002 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2017/01/09/announcing-windows-10-insider-preview-build-15002-pc/)を参照してください。<br/>


### <a name="known-issue"></a>既知の問題

2 つの既知の問題:
- コンソールが一部の Ctrl + <key> 入力を認識しないという既知のバグがあります。  これには、通常の "c" キーが押されたものとして機能する ctrl-c コマンドが含まれます。

  - 対応策 :代替キーを Ctrl+C にマップします。 たとえば、Ctrl+K を Ctrl+C にマップするには、`stty intr \^k` を実行します。  このマッピングはターミナルごとに行い、*毎回* bash が起動されるたびに実行する必要があります。 ユーザーはオプションを探索し、これを `.bashrc` に含めることができます。

- WSL が実行されている間、システム スレッドは CPU コアの 100% を消費します。  根本原因は、内部で対処されて修正されています。

### <a name="fixed"></a>固定

- すべての bash セッションは、同じアクセス許可レベルで作成することが必要になりました。  別のレベルでセッションを開始しようとすると、ブロックされます。  つまり、管理コンソールと非管理コンソールを同時に実行することはできません。 (GH #626)
<br/>
- 次の NETLINK_ROUTE メッセージを実装しました (Windows 管理者が必要)
     - RTM_NEWADDR (`ip addr add` をサポート)
     - RTM_NEWROUTE (`ip route add` をサポート)
     - RTM_DELADDR (`ip addr del` をサポート)
     - RTM_DELROUTE (`ip route del` をサポート)
- 更新するパッケージについてのスケジュールされたタスク チェックは、従量課金接続では実行されなくなります (GH #1371)
- 次のようにパイプがスタックするエラーを修正しました。bash -c "ls -alR /" | bash -c "cat" (GH #1214)
- TCP_KEEPCNT ソケット オプションを実装しました (GH #843)
- IP_MTU_DISCOVER INET ソケット オプションを実装しました (GH #720、717、170、69)
- NT パス参照を使用して init から NT バイナリを実行する従来の機能を削除しました。 (GH #1325)
- グループ/その他の読み取りアクセスを許可するように /dev/kmsg のモードを修正します (0644) (GH #1321)
- /proc/sys/kernel/random/uuid を実装しました (GH #1092)
- プロセスの開始時刻が 2432 年と表示されていたエラーを修正しました (GH #974)
- 既定の TERM 環境変数を xterm-256color に切り替えました (GH #1446)
- プロセスのフォーク中のプロセス コミットの計算方法を変更しました。 (GH #1286)
- /proc/sys/vm/overcommit_memory を実装しました。 (GH #1286)
- /proc/net/route ファイルを実装しました (GH #69)
- ショートカット名が誤ってローカライズされるエラーを修正しました (GH #696)
- プログラム ヘッダーが PATH_MAX 以下でなければならないことを誤って検証をしている elf 解析ロジックを修正しました。 (GH #1048)
- procfs、sysfs、cgroupfs、および binfmtfs に対する statfs コールバックを実装しました (GH #1378)
- 閉じない AptPackageIndexUpdate ウィンドウを修正しました (GH #1184、さらに GH #1193 でも説明)
- ASLR パーソナリティ ADDR_NO_RANDOMIZE のサポートを追加しました。 (GH #1148、1128)
- AV 中の適切な gdb スタック トレースのために PTRACE_GETSIGINFO、SIGSEGV を改善しました (GH #875)
- patchelf バイナリに対する Elf の解析は失敗しなくなりました。 (GH #471)
- /etc/resolv.conf に伝搬される VPN DNS (GH #416、1350)
- より信頼性の高いデータ転送のための TCP クローズに対する機能強化。 (GH #610、616、1025、1335)
- 開いているファイルの数が多すぎるときに適切なエラー コードが返されるようになりました (EMFILE)。 (GH #1126、2090)
- Windows の監査ログは、プロセス作成の監査でイメージ名を報告するようになりました。
- bash ウィンドウ内から bash.exe を起動すると、正常に失敗するようになりました
- 相互運用が LxFs の作業ディレクトリにアクセスできないときのエラー メッセージを追加しました (例: notepad.exe .bashrc)
- Windows のパスが WSL で切り捨てられていた問題を修正しました
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:690 </br>
不合格の数 (失敗した、スキップしたなど):274 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/15002)<br/>

<br/>

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`shmctl`<br/>
`shmget`<br/>
`shmdt`<br/>
`shmat`<br/>
<br/>

## <a name="build-14986"></a>ビルド 14986

ビルド 14986 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/12/07/announcing-windows-10-insider-preview-build-14986-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

- Netlink および Pty の IOCTL でのバグチェックを修正しました
- カーネルのバージョンは、Xenial との一貫性のために 4.4.0-43 を報告するようになりました
- 入力が 'nul:' に向けられたときに Bash.exe が起動するようになりました (GH #1259)
- スレッド ID が procfs で正しく報告されるようになりました (GH #967)
- IN_UNMOUNT | IN_Q_OVERFLOW | IN_IGNORED | IN_ISDIR のフラグが inotify_add_watch() でサポートされるようになりました (GH #1280)
- timer_create システム コールおよび関連するシステム コールを実装します。  これにより GHC サポートが有効になります (GH #307)
- Ping で 0.000 ミリ秒の時間が返される問題を修正しました (GH #1296)
- 開いているファイルの数が多すぎるときに適切なエラー コードを返します。
- インターフェイスのハードウェア アドレスが 32 バイトの場合 (Teredo インターフェイスなど) に、Netlink のネットワーク インターフェイス データの要求が EINVAL で失敗する WSL の問題を修正しました
   - Linux の "ip" ユーティリティには、WSL が 32 バイトのハードウェア アドレスを報告した場合にクラッシュするバグが含まれていることに留意してください。 これは、WSL ではなく、"ip" のバグです。 "ip" ユーティリティは、ハードウェア アドレスの出力に使用される文字列バッファーの長さをハードコーディングしますが、そのバッファーは 32 バイトのハードウェア アドレスを出力するには小さすぎます。
- その他の修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:669 </br>
不合格の数 (失敗した、スキップしたなど):258 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14986)<br/>

<br/>

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`timer_create`<br/>
`timer_delete`<br/>
`timer_gettime`<br/>
`timer_settime`<br/>
<br/>

## <a name="build-14971"></a>ビルド 14971

ビルド 14971 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/11/17/announcing-windows-10-insider-preview-build-14971-for-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

 - Microsoft の制御を超える状況により、Windows Subsystem for Linux のこのビルドには更新はありません。  定期的にスケジュールされた更新は、次のリリースから再開されます。

### <a name="ltp-results"></a>LTP の結果:
14965 から変更されていません </br>
合格したテストの数:664 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14965)<br/>

<br/>

## <a name="build-14965"></a>ビルド 14965

ビルド 14965 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/11/09/announcing-windows-10-insider-preview-build-14965-for-mobile-and-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

- Netlink ソケット NETLINK_ROUTE プロトコルの RTM_GETLINK と RTM_GETADDR に対するサポート (GH #468)
  - ネットワークの列挙に対して ifconfig コマンドと ip コマンドを有効にします
  - 詳細については、[WSL ネットワークに関するブログ投稿](https://blogs.msdn.microsoft.com/wsl/2016/11/08/225/)を参照してください。

- /sbin は、既定でユーザーのパスに含まれるようになりました
- NT ユーザー パスが既定で WSL パスに追加されるようになりました (つまり、Linux パスに System32 を追加せずに notepad.exe を入力できるようになりました)
- /proc/sys/kernel/cap_last_cap のサポートを追加しました
- 現在の作業ディレクトリに ANSI 以外の文字が含まれている場合、WSL から NT バイナリを起動できるようになりました (GH #1254)
- 切断された UNIX ストリーム ソケットでのシャットダウンを許可します。
- PR_GET_PDEATHSIG のサポートを追加しました。
- CLONE_PARENT のサポートを追加しました
- 次のようにパイプがスタックするエラーを修正しました。bash -c "ls -alR /" | bash -c "cat" (GH #1214)
- 現在のターミナルに接続する要求を処理します。
- /proc/<pid>/oom_score_adj を書き込み可能としてマークします。
- /sys/fs/cgroup フォルダーを追加します。
- sched_setaffinity は、アフィニティ ビット マスクの数を返します
- インタープリター パスの長さが 64 文字未満でなければならないことを誤って想定している ELF 検証ロジックを修正します。 (GH #743)
- オープン ファイル記述子により、コンソール ウィンドウが開いたままになることがあります (GH #1187)
- rename() がターゲット名の末尾スラッシュで失敗したエラーを修正しました (GH #1008)
- /proc/net/dev ファイルを実装します
- タイマー精度が原因の 0.000 ミリ秒の Ping を修正します。
- /proc/self/environ を実装しました (GH #730)
- その他のバグ修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:664 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14965)<br/>

<br/>

## <a name="build-14959"></a>ビルド 14959

ビルド 14959 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/11/03/announcing-windows-10-insider-preview-build-14959-for-mobile-and-pc/#iI82GufJxMF3POU1.97)を参照してください。<br/>


### <a name="fixed"></a>固定

- Windows の Pico プロセス通知を改善しました。  [WSL ブログ](/archive/blogs/wsl/wsl-antivirus-and-firewall-compatibility)に追加情報があります。
- Windows の相互運用性での安定性を向上させました
- エンタープライズ データ保護 (EDP) が有効になっているときに bash.exe を起動すると発生するエラー 0x80070057 を修正しました
- その他のバグ修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:665 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14959)<br/>

<br/>

## <a name="build-14955"></a>ビルド 14955

ビルド 14955 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/10/25/announcing-windows-10-insider-preview-build-14955-for-mobile-and-pc/#guGXQzKVFrZIDUYR.97)を参照してください。<br/>


### <a name="fixed"></a>固定

 - Microsoft の制御を超える状況により、Windows Subsystem for Linux のこのビルドには更新はありません。  定期的にスケジュールされた更新は、次のリリースから再開されます。

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:665 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14955)<br/>

<br/>

## <a name="build-14951"></a>ビルド 14951

ビルド 14951 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/10/19/announcing-windows-10-insider-preview-build-14951-for-mobile-and-pc/)を参照してください。<br/>


### <a name="new-feature-windows--ubuntu-interoperability"></a>新機能:Windows/Ubuntu の相互運用性
Windows バイナリを WSL コマンド ラインから直接呼び出せるようになりました。  これによりユーザーは、今まで可能ではなかった方法で Windows 環境およびシステムと対話ができるようになります。  簡単な例として、ユーザーは次のコマンドを実行できるようになりました。

```bash
$ export PATH=$PATH:/mnt/c/Windows/System32
$ notepad.exe
$ ipconfig.exe | grep IPv4 | cut -d: -f2
$ ls -la | findstr.exe foo.txt
$ cmd.exe /c dir
```

詳細については、以下を参照してください。

- [相互運用に関する WSL チームのブログ](/archive/blogs/wsl/windows-and-ubuntu-interoperability)<br/>
- [MSDN 相互運用のドキュメント](./interop.md)<br/>

### <a name="fixed"></a>固定

- すべての新しい WSL インスタンスで Ubuntu 16.04 (Xenial) がインストールされるようになりました。  既存の 14.04 (Trusty) インスタンスを使用しているユーザーは自動的にアップグレードされません。
- インストール中に設定されたロケールが表示されるようになりました
- ファイルへの WSL プロセスのリダイレクトが必ずしも機能しないというバグを含む、ターミナルの機能強化
- コンソールの有効期間は bash.exe の有効期間に関連付けられている必要があります
- コンソール ウィンドウのサイズは、バッファー サイズではなく表示サイズを使用する必要があります
- その他のバグ修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:665 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14951)<br/>

<br/>

## <a name="build-14946"></a>ビルド 14946

ビルド 14946 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/10/13/announcing-windows-10-insider-preview-build-14946-for-pc-and-mobile/#xj8GdVooEqo4H7H7.97)を参照してください。<br/>


### <a name="fixed"></a>固定

- スペースまたは引用符を含む NT ユーザー名を持つユーザーの WSL ユーザー アカウントの作成を妨げる問題を修正しました。 
- stat でディレクトリのリンク数に対して 0 が返されるように、VolFs と DrvFs を変更します
- IPV6_MULTICAST_HOPS ソケット オプションをサポートします。
- 1 つの tty につき 1 つのコンソール I/O ループに制限します。 たとえば、次のコマンドが可能です。
  - bash -c "echo data" | bash -c "ssh user@example.com 'cat > foo.txt'"

- /proc/cpuinfo でスペースをタブに置き換えます (GH #1115)
- DrvFs は、マウントされた Windows ボリュームと一致する名前で mountinfo に表示されるようになりました
- /home と /root が正しい名前で mountinfo に表示されるようになりました
- その他のバグ修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:665 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14946)<br/>

<br/>

## <a name="build-14942"></a>ビルド 14942

ビルド 14942 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/onefourninefourtwoooooo)を参照してください。<br/>


### <a name="fixed"></a>固定

- SSH をブロックしていた "ATTEMPTED EXECUTE OF NOEXECUTE MEMORY" ネットワーク クラッシュを含め、複数のバグチェックに対処しました
- DrvFs の Windows アプリケーションから生成された通知に対する inotifiy のサポートが有効になりました
- mongod に対して TCP_KEEPIDLE および TCP_KEEPINTVL を実装します。 (GH #695)
- pivot_root システム コールを実装します
- SO_DONTROUTE に対してソケット オプションを実装します
- その他のバグ修正と機能強化


### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:665 </br>
不合格の数 (失敗した、スキップしたなど):263 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14942)<br/>

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`pivot_root`<br/>
<br/>

## <a name="build-14936"></a>ビルド 14936

ビルド 14936 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/09/28/announcing-windows-10-insider-preview-build-14936-for-pc/)を参照してください。<br/>


注: WSL は、今後のリリースで Ubuntu 14.04 (Trusty) ではなく、Ubuntu バージョン 16.04 (Xenial) をインストールします。  この変更は、新しいインスタンスをインストールする Insiders に適用されます (lxrun.exe、あるいは bash.exe のインストールまたは初回の実行)。  Trusty を使用する既存のインスタンスは、自動的にアップグレードされません。 ユーザーは、do-release-upgrade コマンドを使用して、Trusty イメージを Xenial にアップグレードできます。

### <a name="known-issue"></a>既知の問題
WSL では、いくつかのソケット実装で問題が発生しています。  バグチェックを実行するとクラッシュし、エラー "ATTEMPTED EXECUTE OF NOEXECUTE MEMORY" が出されます。  この問題の最も一般的な発現は、SSH を使用したときのクラッシュです。  根本原因は内部ビルドで修正され、最も早い機会に Insiders にプッシュされます。

### <a name="fixed"></a>固定

- chroot システム コールを実装しました
- ~~Drvfs 上の Windows アプリケーションから生成された通知のサポートを含む~~ inotify の機能強化
  - 訂正:Windows アプリケーションからの変更に対する Inotify のサポートは、現時点では利用できません。
- IPV6::<port n> へのソケット バインドで、IPV6_V6ONLY がサポートされるようになりました (GH #68、#157、#393、#460、#674、#740、#982、#996)
- waitid システム コールに対する WNOWAIT 動作を実装しました (GH #638)
- IP ソケット オプション IP_HDRINCL と IP_TTL のサポート
- 長さゼロの read() はすぐに戻ります (GH #975)
- .tar ファイルに NULL 終端文字を含まないファイル名とファイル名のプレフィックスを正しく処理します。
- /dev/null に対する epoll サポート
- /dev/alarm タイム ソースを修正します
- Bash -c はファイルにリダイレクトできるようになりました
- その他のバグ修正と機能強化

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:664 </br>
不合格の数 (失敗した、スキップしたなど):264 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14936)<br/>

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`chroot`<br/>
<br/>

## <a name="build-14931"></a>ビルド 14931

ビルド 14931 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/09/21/announcing-windows-10-insider-preview-build-14931-for-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定

 - Microsoft の制御を超える状況により、Windows Subsystem for Linux のこのビルドには更新はありません。  定期的にスケジュールされた更新は、次のリリースから再開されます。

<br/>

## <a name="build-14926"></a>ビルド 14926

ビルド 14926 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/09/14/announcing-windows-10-insider-preview-build-14926-for-pc-and-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定

- 管理者特権を持たないコンソールで Ping が機能するようになりました
- Ping6 が、この場合も管理者特権なしでサポートされるようになりました
- WSL を使用して変更されたファイルに対する Inotify サポート。 (GH #216)
  - サポートされるフラグ:
    - inotify_init1:LX_O_CLOEXEC、LX_O_NONBLOCK
    - inotify_add_watch イベント:LX_IN_ACCESS、LX_IN_MODIFY、LX_IN_ATTRIB、LX_IN_CLOSE_WRITE、LX_IN_CLOSE_NOWRITE、LX_IN_OPEN、LX_IN_MOVED_FROM、LX_IN_MOVED_TO、LX_IN_CREATE、LX_IN_DELETE、LX_IN_DELETE_SELF、LX_IN_MOVE_SELF
    - inotify_add_watch 属性:LX_IN_DONT_FOLLOW、LX_IN_EXCL_UNLINK、LX_IN_MASK_ADD、LX_IN_ONESHOT、LX_IN_ONLYDIR
    - 出力の読み取り:LX_IN_ISDIR、LX_IN_IGNORED
  - 既知の問題:Windows アプリケーションからファイルを変更してもイベントは生成されません
- Unix ソケットで SCM_CREDENTIALS がサポートされるようになりました

### <a name="ltp-results"></a>LTP の結果:
合格したテストの数:651 </br>
不合格の数 (失敗した、スキップしたなど):258 </br>
[LTP テスト実行ログ](https://github.com/Microsoft/CommandLine-Documentation/tree/live/LTP_Results/14926)<br/>

<br/>

## <a name="build-14915"></a>ビルド 14915

ビルド 14915 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/08/31/announcing-windows-10-insider-preview-build-14915-for-pc-and-mobile)を参照してください。<br/>


### <a name="fixed"></a>固定
-  UNIX データグラム ソケットに対する Socketpair (GH #262)
- SO_REUSEADDR に対する UNIX ソケット サポート
- SO_BROADCAST に対する UNIX ソケット サポート (GH #568)
- SOCK_SEQPACKET に対する UNIX ソケット サポート (GH #758、#546)
- UNIX データグラム ソケット send、recv、および shutdown に対するサポートの追加
- 固定されていないアドレスに対する無効な mmap パラメーター検証によるバグチェックの修正。 (GH #847)
- ターミナルの状態の中断/再開のサポート
- Screen ユーティリティのブロックを解除する TIOCPKT ioctl のサポート (GH #774)
    - 既知の問題:ファンクション キーが動作しません
- 解放されたメンバー 'ReaderReady' が LxpTimerFdWorkerRoutine によってアクセスされる原因となる TimerFd での競合を修正しました (GH #814)
- futex、poll、および clock_nanosleep に対する再起動可能システム コールのサポートを有効にします
- bind mount のサポートを追加しました
- マウント名前空間に対する unshare のサポート
    - 既知の問題:`unshare(CLONE_NEWNS)` を使用して新しいマウント名前空間を作成するときに、現在の作業ディレクトリは引き続き古い名前空間を指します
- その他の機能強化とバグ修正

<br/>

## <a name="build-14905"></a>ビルド 14905

ビルド 14905 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/08/17/announcing-windows-10-insider-preview-build-14905-for-pc-mobile/)を参照してください。<br/>


### <a name="fixed"></a>固定
- 再起動可能システム コールがサポートされるようになりました (GH #349、GH #520)
- / で終了するディレクトリへのシンボリック リンクが動作するようになりました (GH #650)
- /dev/random に対する RNDGETENTCNT ioctl を実装しました
- /proc/[pid]/mounts、/proc/[pid]/mountinfo、および /proc/[pid]/mountstats のファイルを実装しました
- その他のバグ修正と機能強化

</br>

## <a name="build-14901"></a>ビルド 14901
Windows 10 Anniversary Update リリース以降の最初の Insider ビルド。

ビルド 14901 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/08/11/announcing-windows-10-insider-preview-build-14901-for-pc/)を参照してください。<br/>


### <a name="fixed"></a>固定
- 末尾のスラッシュの問題を修正しました
    - `$ mv a/c/ a/b/` などのコマンドが機能するようになりました
- インストールで、Ubuntu のロケールを Windows のロケールに設定すべきかどうかを確認するプロンプトが出されるようになりました
- ns フォルダーに対する Procfs のサポート
- tmpfs、procfs、および sysfs のファイルシステムに対して mount と unmount を追加しました
- mknod[at] 32 ビット ABI の署名を修正します
- UNIX ソケットをディスパッチ モデルに移行しました
- setsockopt を使用して設定された INET ソケットの recv バッファー サイズを優先します
- MSG_CMSG_CLOEXEC Unix ソケット受信メッセージ フラグを実装します
- Linux プロセスの stdin/stdout パイプのリダイレクト (GH #2)
    - CMD で bash -c コマンドのパイプを許可します。  例:  >dir | bash -c "grep foo"
- 複数のページ ファイルがあるシステムに Bash をインストールできるようになりました (GH #538、#358)
- 既定の INET ソケット バッファー サイズは、既定の Ubuntu セットアップのものと一致している必要があります
- xattr システム コールを listxattr に合わせて配置します
- SIOCGIFCONF から有効な IPv4 アドレスを持つインターフェイスのみを返します
- ptrace によって挿入される際のシグナルの既定のアクションを修正します
- /proc/sys/vm/min_free_kbytes を実装します
- sigreturn でコンテキストを復元するときにマシン コンテキスト レジスタの値を使用します
    - これにより、一部のユーザーで java と javac がハングしていた問題が解決されます
- /proc/sys/kernel/hostname を実装します

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`waitid`<br/>
`epoll_pwait`<br/>

<br/>

## <a name="build-14388-to-windows-10-anniversary-update"></a>ビルド 14388 から Windows 10 Anniversary Update まで
ビルド 14388 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/14388wip)を参照してください。 <br/>

### <a name="fixed"></a>固定
- 8/2 の Windows 10 Anniversary Update の準備をするための修正
  - Anniversary Update での WSL の詳細情報については、こちらの[ブログ](/archive/blogs/wsl/)を参照してください

<br/>

## <a name="build-14376"></a>ビルド 14376
ビルド 14376 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/06/28/announcing-windows-10-insider-preview-build-14376-for-pc-and-mobile/)を参照してください。 <br/>

### <a name="fixed"></a>固定
- apt-get がハングするいくつかのインスタンスを削除しました (GH #493)
- 空のマウントが正しく処理されなかった問題を修正しました
- ramdisk が正しくマウントされなかった問題を修正しました
- フラグをサポートするように UNIX ソケット accept を変更します (一部 GH #451)
- 一般的なネットワークに関連したブルースクリーンを修正しました
- /proc/[pid]/task にアクセスするときのブルースクリーンを修正しました (GH #523)
- 一部の pty シナリオでの高い CPU 使用率を修正しました (GH #488、#504)
- その他のバグ修正と機能強化

<br/>

## <a name="build-14371"></a>ビルド 14371
ビルド 14371 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/06/22/announcing-windows-10-insider-preview-build-14371-for-pc/)を参照してください。 <br/>

### <a name="fixed"></a>固定
- ptrace を使用する際の SIGCHLD と wait () のタイミングの競合を修正しました
- パスの末尾に / がある場合の一部の動作を修正しました (GH #432)
- 子への開いたハンドルのために rename/unlink が失敗する問題を修正しました
- その他のバグ修正と機能強化

<br/>

## <a name="build-14366"></a>ビルド 14366
ビルド 14366 の一般的な Windows 情報については、[Windows ブログ](https://blogs.windows.com/windowsexperience/2016/06/14/announcing-windows-10-insider-preview-build-14366-mobile-build-14364/)を参照してください。 <br/>

### <a name="fixed"></a>固定
- シンボリック リンクを使用したファイル作成の修正
-   Python 用 listxattr を追加しました (GH 385)
-   その他のバグ修正と機能強化

### <a name="syscall-support"></a>システム コールのサポート
-   次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`listxattr`<br/>
<br/>

## <a name="build-14361"></a>ビルド 14361
ビルド 14361 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/wip14361)を参照してください。 <br/>

### <a name="fixed"></a>固定
- Bash on Ubuntu on Windows で実行しているときに、DrvFs で大文字と小文字が区別されるようになりました。
  - ユーザーは、/mnt/c ドライブで case.txt と CASE.TXT を使用できます
  - 大文字小文字の区別は、Bash on Ubuntu on Windows でのみサポートされています。 Bash の外では、NTFS はファイルを正しく報告しますが、Windows からのファイルの操作で、予期しない動作が発生する場合があります。
  - 各ボリュームのルート (つまり、/mnt/c) では大文字小文字の区別はありません
  - Windows でのこれらのファイルの処理について詳しくは、[こちら](https://support.microsoft.com/kb/100625)を参照してください。
- pty / tty のサポートが大幅に強化されました。  TMUX のようなアプリケーションがサポートされるようになりました (GH #40)
- ユーザー アカウントが必ずしも作成されないというインストールの問題を修正しました
- 非常に長い引数リストを使用できるように、コマンド ラインの引数の構造を最適化しました。 (GH #153)
- DrvFs から read_only ファイルの削除および chmod を実行できるようになりました
- 切断時にターミナルがハングする一部のインスタンスを修正しました (GH #43)
- chmod および chown が tty デバイスで機能するようになりました
- localhost として 0.0.0.0 および :: への接続を許可します (GH #388)
- Sendmsg/recvmsg は、>1 の IO ベクトル長を処理するようになりました (一部 GH #376)
- ユーザーは、自動生成された hosts ファイルをオプトアウトできるようになりました (GH #398)
- インストール中に Linux のロケールを NT のロケールに自動的に一致させます (GH #11)
- /proc/sys/vm/swappiness ファイルを追加しました (GH #306)
- strace が正常に終了するようになりました
- /proc/self/fd を使用したパイプの再オープンを許可します (GH #222)
- DrvFs で %LOCALAPPDATA%\lxss の下のディレクトリが非表示になります (GH #270)
- bash.exe ~ の処理の改善。  "bash ~ -c ls" のようなコマンドがサポートされるようになりました (GH #467)
- ソケットが、シャットダウン中に使用可能な epoll read を通知するようになりました (GH #271)
- lxrun /uninstall でファイルとフォルダーの削除ジョブが改善されました
- ps -f を修正しました (GH #246)
- xEmacs などの x11 アプリのサポートを強化しました (GH #481)
- 既定の Ubuntu 設定に一致するように初期スレッドのスタック サイズを更新しました。また、get_rlimit システム コールにサイズを正しく報告します (GH #172、#258)
- Pico プロセスのイメージ名の報告を改善しました (監査のためなど)
- df コマンドに対して /proc/mountinfo を実装しました
- 子名のシンボリック リンクのエラー コードを修正しました (. および ..)
- その他のバグ修正と機能強化

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`GETTIMER`<br/>
`MKNODAT`<br/>
`RENAMEAT`<br/>
`SENDFILE`<br/>
`SENDFILE64`<br/>
`SYNC_FILE_RANGE`<br/>
<br/>

## <a name="build-14352"></a>ビルド 14352
ビルド 14352 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/wip14352)を参照してください。<br/>


### <a name="fixed"></a>固定
- 大きなファイルが正しくダウンロードまたは作成されなかった問題を修正しました。  これにより、npm と他のシナリオのブロックが解除されます (GH #3、GH #313)
- ソケットがハングするいくつかのインスタンスを削除しました
- いくつかの ptrace エラーを修正しました
- WSL で 255 文字を超えるファイル名が許可される問題を修正しました
- 英語以外の文字のサポートが強化されました
- 現在の Windows タイムゾーンのデータを追加し、既定として設定します
- マウント ポイントごとに一意のデバイス ID (JRE 修正 – GH #49)
- "."{}および ".." を含むパスの問題を修正します
- Fifo のサポートを追加しました (GH #71)
- ネイティブ Ubuntu 形式に一致するように resolv.conf の形式を更新しました
- 一部の procfs のクリーンアップ
- 管理者コンソールの Ping を有効にしました (GH #18)

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`FALLOCATE`<br/>
`EXECVE`<br/>
`LGETXATTR`<br/>
`FGETXATTR`<br/>
<br/>

## <a name="build-14342"></a>ビルド 14342
ビルド 14342 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/wip14342)を参照してください。 <br/>

VolFs および DriveFs の情報については、[WSL ブログ](/archive/blogs/wsl/)を参照してください。 <br/>

### <a name="fixed"></a>固定
- Windows ユーザーのユーザー名に Unicode 文字が含まれている場合のインストールの問題を修正しました
- FAQ にある apt-get update udev の回避策が、初回の実行時に既定で提供されるようになりました
- DriveFs (/mnt/<drive>) ディレクトリでシンボリック リンクを有効にしました
- シンボリック リンクが DriveFs と VolFs 間で機能するようになりました
- アドレス指定された最上位のパス解析の問題に対処し、ls .// が期待どおりに動作するようになりました
- DriveFs での npm install、および -g オプションが機能するようになりました
- PHP サーバーの起動を妨げている問題を修正しました
- ネイティブ Ubuntu により近く一致するように $PATH などの既定の環境値を更新しました
- apt パッケージ キャッシュを更新するための Windows での週単位のメンテナンス タスクを追加しました
- ELF ヘッダー検証の問題を修正しました。WSL ですべての Melkor オプションがサポートされるようになりました
- Zsh シェルが機能するようになりました
- プリコンパイル済みの Go バイナリがサポートされるようになりました
- Bash.exe の初回実行時のプロンプトが正しくローカライズされるようになりました
- /proc/meminfo が正しい情報を返すようになりました
- ソケットが VFS でサポートされるようになりました
- /dev が tempfs としてマウントされるようになりました
- Fifo がサポートされるようになりました
- マルチコア システムが /proc/cpuinfo に正しく表示されるようになりました
- 初回実行時のダウンロードにおける追加の改善とエラー メッセージ
- システム コールの機能強化とバグ修正。 サポートされるシステム コールの一覧を以下に示します。
- その他のバグ修正と機能強化

### <a name="known-issues"></a>の既知の問題
- 場合によって、DriveFs で '..' が正しく解決されません

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装がある新しい、または強化されたシステム コールの一覧です。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`FCHOWNAT`<br/>
`GETEUID`<br/>
`GETGID`<br/>
`GETRESUID`<br/>
`GETXATTR`<br/>
`PTRACE`<br/>
`SETGID`<br/>
`SETGROUPS`<br/>
`SETHOSTNAME`<br/>
`SETXATTR`<br/>
<br/>

## <a name="build-14332"></a>ビルド 14332

ビルド 14332 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/wip14332)を参照してください。 <br/>


### <a name="fixed"></a>固定
- DNS エントリの優先順位付けを含め、resolv.conf の生成が改善されました
- /mnt ドライブと /mnt 以外のドライブとの間のファイルとディレクトリの移動に関する問題
- シンボリック リンクを使って tar ファイルを作成できるようになりました
- インスタンス作成時に既定の /run/lock ディレクトリを追加しました
- 適切な stat 情報を返すように /dev/null を更新します
- 初回実行時のダウンロードにおける追加エラー
- システム コールの機能強化とバグ修正。 サポートされるシステム コールの一覧を以下に示します。
- その他のバグ修正と機能強化

### <a name="syscall-support"></a>システム コールのサポート
以下は、WSL に何らかの実装がある新しいシステム コールです。 この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`READLINKAT`<br/>
<br/>

## <a name="build-14328"></a>ビルド 14328

ビルド 14332 の一般的な Windows 情報については、[Windows ブログ](https://aka.ms/wip14328)を参照してください。 <br/>


### <a name="new-features"></a>新機能
* Linux ユーザーがサポートされるようになりました。  Bash on Ubuntu on Windows をインストールすると、Linux ユーザーの作成を求めるプロンプトが表示されます。  詳細については、 https://aka.ms/wslusers にアクセスしてください
* ホスト名は、Windows コンピューター名に設定されるようになりました。@localhost はもう使用されません
* ビルド 14328 の詳細についは、次を参照してください: https://aka.ms/wip14328

### <a name="fixed"></a>固定
* /mnt/<drive> 以外のファイルに対するシンボリック リンクの機能強化
    * npm install が機能するようになりました
    * jdk / jre は、[こちら](https://xubuntugeek.blogspot.com/2012/09/how-to-install-oracle-jdk-7-manually-in.html)の説明を使用してインストールできるようになりました。
    * 既知の問題: シンボリック リンクは Windows マウントでは機能しません。  機能は今後のビルドで使用できるようになる予定です
* top と htop が表示されるようになりました
* 一部のインストール エラーに対する追加のエラー メッセージ
* システム コールの機能強化とバグ修正。  サポートされるシステム コールの一覧を以下に示します。
* その他のバグ修正と機能強化

### <a name="syscall-support"></a>システム コールのサポート
次に示すのは、WSL に何らかの実装があるシステム コールの一覧です。  この一覧にあるシステム コールは、少なくとも 1 つのシナリオではサポートされていますが、現時点では、一部のパラメーターがサポートされていない可能性があります。

`ACCEPT`<br/>
`ACCEPT4`<br/>
`ACCESS`<br/>
`ALARM`<br/>
`ARCH_PRCTL`<br/>
`BIND`<br/>
`BRK`<br/>
`CAPGET`<br/>
`CAPSET`<br/>
`CHDIR`<br/>
`CHMOD`<br/>
`CHOWN`<br/>
`CLOCK_GETRES`<br/>
`CLOCK_GETTIME`<br/>
`CLOCK_NANOSLEEP`<br/>
`CLONE`<br/>
`CLOSE`<br/>
`CONNECT`<br/>
`CREAT`<br/>
`DUP`<br/>
`DUP2`<br/>
`DUP3`<br/>
`EPOLL_CREATE`<br/>
`EPOLL_CREATE1`<br/>
`EPOLL_CTL`<br/>
`EPOLL_WAIT`<br/>
`EVENTFD`<br/>
`EVENTFD2`<br/>
`EXECVE`<br/>
`EXIT`<br/>
`EXIT_GROUP`<br/>
`FACCESSAT`<br/>
`FADVISE64`<br/>
`FCHDIR`<br/>
`FCHMOD`<br/>
`FCHMODAT`<br/>
`FCHOWN`<br/>
`FCHOWNAT`<br/>
`FCNTL64`<br/>
`FDATASYNC`<br/>
`FLOCK`<br/>
`FORK`<br/>
`FSETXATTR`<br/>
`FSTAT64`<br/>
`FSTATAT64`<br/>
`FSTATFS64`<br/>
`FSYNC`<br/>
`FTRUNCATE`<br/>
`FTRUNCATE64`<br/>
`FUTEX`<br/>
`GETCPU`<br/>
`GETCWD`<br/>
`GETDENTS`<br/>
`GETDENTS64`<br/>
`GETEGID`<br/>
`GETEGID16`<br/>
`GETEUID`<br/>
`GETEUID16`<br/>
`GETGID`<br/>
`GETGID16`<br/>
`GETGROUPS`<br/>
`GETPEERNAME`<br/>
`GETPGID`<br/>
`GETPGRP`<br/>
`GETPID`<br/>
`GETPPID`<br/>
`GETPRIORITY`<br/>
`GETRESGID`<br/>
`GETRESGID16`<br/>
`GETRESUID`<br/>
`GETRESUID16`<br/>
`GETRLIMIT`<br/>
`GETRUSAGE`<br/>
`GETSID`<br/>
`GETSOCKNAME`<br/>
`GETSOCKOPT`<br/>
`GETTID`<br/>
`GETTIMEOFDAY`<br/>
`GETUID`<br/>
`GETUID16`<br/>
`GETXATTR`<br/>
`GET_ROBUST_LIST`<br/>
`GET_THREAD_AREA`<br/>
`INOTIFY_ADD_WATCH`<br/>
`INOTIFY_INIT`<br/>
`INOTIFY_RM_WATCH`<br/>
`IOCTL`<br/>
`IOPRIO_GET`<br/>
`IOPRIO_SET`<br/>
`KEYCTL`<br/>
`KILL`<br/>
`LCHOWN`<br/>
`LINK`<br/>
`LINKAT`<br/>
`LISTEN`<br/>
`LLSEEK`<br/>
`LSEEK`<br/>
`LSTAT64`<br/>
`MADVISE`<br/>
`MKDIR`<br/>
`MKDIRAT`<br/>
`MKNOD`<br/>
`MLOCK`<br/>
`MMAP`<br/>
`MMAP2`<br/>
`MOUNT`<br/>
`MPROTECT`<br/>
`MREMAP`<br/>
`MSYNC`<br/>
`MUNLOCK`<br/>
`MUNMAP`<br/>
`NANOSLEEP`<br/>
`NEWUNAME`<br/>
`OPEN`<br/>
`OPENAT`<br/>
`PAUSE`<br/>
`PERF_EVENT_OPEN`<br/>
`PERSONALITY`<br/>
`PIPE`<br/>
`PIPE2`<br/>
`POLL`<br/>
`PPOLL`<br/>
`PRCTL`<br/>
`PREAD64`<br/>
`PROCESS_VM_READV`<br/>
`PROCESS_VM_WRITEV`<br/>
`PSELECT6`<br/>
`PTRACE`<br/>
`PWRITE64`<br/>
`READ`<br/>
`READLINK`<br/>
`READV`<br/>
`REBOOT`<br/>
`RECV`<br/>
`RECVFROM`<br/>
`RECVMSG`<br/>
`RENAME`<br/>
`RMDIR`<br/>
`RT_SIGACTION`<br/>
`RT_SIGPENDING`<br/>
`RT_SIGPROCMASK`<br/>
`RT_SIGRETURN`<br/>
`RT_SIGSUSPEND`<br/>
`RT_SIGTIMEDWAIT`<br/>
`SCHED_GETAFFINITY`<br/>
`SCHED_GETPARAM`<br/>
`SCHED_GETSCHEDULER`<br/>
`SCHED_GET_PRIORITY_MAX`<br/>
`SCHED_GET_PRIORITY_MIN`<br/>
`SCHED_SETAFFINITY`<br/>
`SCHED_SETPARAM`<br/>
`SCHED_SETSCHEDULER`<br/>
`SCHED_YIELD`<br/>
`SELECT`<br/>
`SEND`<br/>
`SENDMMSG`<br/>
`SENDMSG`<br/>
`SENDTO`<br/>
`SETDOMAINNAME`<br/>
`SETGID`<br/>
`SETGROUPS`<br/>
`SETHOSTNAME`<br/>
`SETITIMER`<br/>
`SETPGID`<br/>
`SETPRIORITY`<br/>
`SETREGID`<br/>
`SETRESGID`<br/>
`SETRESUID`<br/>
`SETREUID`<br/>
`SETRLIMIT`<br/>
`SETSID`<br/>
`SETSOCKOPT`<br/>
`SETTIMEOFDAY`<br/>
`SETUID`<br/>
`SETXATTR`<br/>
`SET_ROBUST_LIST`<br/>
`SET_THREAD_AREA`<br/>
`SET_TID_ADDRESS`<br/>
`SHUTDOWN`<br/>
`SIGACTION`<br/>
`SIGALTSTACK`<br/>
`SIGPENDING`<br/>
`SIGPROCMASK`<br/>
`SIGRETURN`<br/>
`SIGSUSPEND`<br/>
`SOCKET`<br/>
`SOCKETCALL`<br/>
`SOCKETPAIR`<br/>
`SPLICE`<br/>
`STAT64`<br/>
`STATFS64`<br/>
`SYMLINK`<br/>
`SYMLINKAT`<br/>
`SYNC`<br/>
`SYSINFO`<br/>
`TEE`<br/>
`TGKILL`<br/>
`TIME`<br/>
`TIMERFD_CREATE`<br/>
`TIMERFD_GETTIME`<br/>
`TIMERFD_SETTIME`<br/>
`TIMES`<br/>
`TKILL`<br/>
`TRUNCATE`<br/>
`TRUNCATE64`<br/>
`UMASK`<br/>
`UMOUNT`<br/>
`UMOUNT2`<br/>
`UNLINK`<br/>
`UNLINKAT`<br/>
`UNSHARE`<br/>
`UTIME`<br/>
`UTIMENSAT`<br/>
`UTIMES`<br/>
`VFORK`<br/>
`WAIT4`<br/>
`WAITPID`<br/>
`WRITE`<br/>
`WRITEV`<br/>
