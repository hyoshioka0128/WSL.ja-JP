---
title: WSL 2 (プレビュー) で Linux ディスクのマウントを開始する
description: WSL 2 でディスクマウントを設定する方法と、そのアクセス方法について説明します。
keywords: wsl、windows、windowssubsystem、gnu、linux、bash、disk、ext4、filesystem、mount
ms.date: 06/08/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 8c67b0f34dcde925bb91979e9153049fdd474db3
ms.sourcegitcommit: dee2bf22c0c9f5725122a155d2876fcb2b7427d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92211736"
---
# <a name="get-started-mounting-a-linux-disk-in-wsl-2-preview"></a>WSL 2 (プレビュー) で Linux ディスクのマウントを開始する

Windows でサポートされていない Linux ディスクフォーマットにアクセスする場合は、WSL 2 を使用してディスクをマウントし、そのコンテンツにアクセスすることができます。

このチュートリアルでは、WSL2 にアタッチするディスクとパーティションを識別する手順、それらをマウントする方法、およびそれらへのアクセス方法について説明します。

> [!NOTE]
> WSL 2 にディスクを接続するには、管理者アクセス権が必要です。

## <a name="identify-the-disk"></a>ディスクを識別する

Windows で使用可能なディスクを一覧表示するには、次のように実行します。

```powershell
wmic diskdrive list brief
```

ディスクパスは、' DeviceID ' 列で使用できます。 通常、の `\\.\PHYSICALDRIVE*` 形式で指定します。

## <a name="list-and-select-the-partitions-to-mount-in-wsl-2"></a>WSL 2 でマウントするパーティションを一覧表示して選択します

ディスクが識別されたら、次のように実行します。

```powershell
wsl --mount <DiskPath> --bare
```

これにより、WSL 2 でディスクを使用できるようになります。

アタッチされたら、WSL 2 内で次のコマンドを実行してパーティションを一覧表示できます。

```powershell
lsblk
```

これにより、使用可能なブロックデバイスとそのパーティションが表示されます。

Linux 内部では、ブロックデバイスはとして識別され  `/dev/<Device><Partition>` ます。 たとえば、次のように指定します。は、ディスクのパーティション番号3です `sdb` 。

出力例:

```powershell
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sdb      8:16   0    1G  0 disk
├─sdb2   8:18   0   50M  0 part
├─sdb3   8:19   0  873M  0 part
└─sdb1   8:17   0  100M  0 part
sdc      8:32   0  256G  0 disk /
sda      8:0    0  256G  0 disk
```

## <a name="identifying-the-filesystem-type"></a>ファイルシステムの種類の識別

ディスクまたはパーティションのファイルシステムの種類がわからない場合は、次のコマンドを使用できます。

```powershell
blkid <BlockDevice>
```

これにより、検出されたファイルシステムの種類 (形式の下) が出力され `TYPE="<Filesystem>"` ます。

## <a name="mount-the-selected-partitions"></a>選択したパーティションをマウントします

マウントするパーティションを特定したら、各パーティションで次のコマンドを実行します。 

```powershell
wsl --mount <DiskPath> --partition <PartitionNumber> --type <Filesystem>
```

> [!NOTE]
> ディスク全体を1つのボリュームとしてマウントする場合 (つまり、ディスクがパーティション分割されていない場合) は、を `--partition` 省略できます。
> 
> 省略した場合、既定のファイルシステムの種類は "ext4" になります。

## <a name="access-the-disk-content"></a>ディスクコンテンツにアクセスする

マウントされると、構成値が指すパスでディスクにアクセスできるように `automount.root` なります。 既定値は `/mnt/wsl` です。

Windows では、ファイルエクスプローラーから: `\\wsl$\\<Distro>\\<Mountpoint>` (任意の Linux ディストリビューションを選択) に移動して、ディスクにアクセスできます。

## <a name="unmount-the-disk"></a>ディスクのマウント解除

WSL 2 からディスクのマウントを解除して切断する場合は、次のように実行します。

```powershell
wsl --unmount <DiskPath>
```

## <a name="command-line-reference"></a>コマンド ライン リファレンス

### <a name="mouting-a-specific-filesystem"></a>特定のファイルシステムの場合

既定では、WSL 2 は ext4 としてデバイスをマウントしようとします。 別のファイルシステムを指定するには、次のように実行します。

```powershell
wsl --mount <DiskPath> -t <FileSystem>
```

たとえば、ディスクを fat としてマウントするには、次のように実行します。

```
wsl --mount <Diskpath> -t vfat
```

> [!NOTE]
> WSL2 で使用可能なファイルシステムを一覧表示するには、次のように実行します。 `cat /proc/filesystems`

### <a name="mouting-a-specific-partition"></a>特定のパーティションを指定する

既定では、WSL 2 はディスク全体をマウントしようとします。 特定のパーティションをマウントするには、次のように実行します。

```
wsl --mount <Diskpath> -p <PartitionIndex>
```

これは、ディスクが MBR (マスターブートレコード) または GPT (GUID パーティションテーブル) のいずれかである場合にのみ機能します。 [パーティションスタイルについては、「MBR と GPT](/windows-server/storage/disk-management/initialize-new-disks#about-partition-styles---gpt-and-mbr)」を参照してください。

### <a name="specifying-mount-options"></a>マウントオプションの指定

マウントオプションを指定するには、次のように実行します。

```powershell
wsl --mount <DiskPath> -o <MountOptions>
```

例:

```powershell
wsl --mount <DiskPath> -o "data=ordered"
```

> [!NOTE]
> 現時点では、ファイルシステム固有のオプションのみがサポートされています。 などの汎用オプション `ro, rw, noatime, ...` はサポートされていません。

### <a name="attaching-the-disk-without-mounting-it"></a>マウントせずにディスクを接続する

ディスク構成が上記のいずれのオプションでもサポートされていない場合は、を実行してディスクをマウントせずに WSL 2 に接続できます。

```powershell
wsl --mount <DiskPath> --bare
```

これにより、ブロックデバイスは WSL 2 内で使用できるようになり、そこから手動でマウントすることができます。 `lsblk`WSL 2 内で利用可能なブロックデバイスを一覧表示するには、を使用します。

### <a name="detaching-a-disk"></a>ディスクのデタッチ

WSL 2 からディスクを切断するには、次のように実行します。

```powershell
wsl --unmount [DiskPath]
```

`Diskpath`を省略すると、接続されているすべてのディスクがマウント解除され、デタッチされます。

> [!NOTE]
> 1つのディスクのマウント解除に失敗した場合は、を実行して WSL 2 を強制的に終了させることができ `wsl --shutdown` ます。これにより、ディスクが切断されます。

## <a name="limitations"></a>制限事項

- 現時点では、ディスク全体のみを WSL 2 に接続できます。つまり、パーティションのみをアタッチすることはできません。 具体的にでは、このデバイスは Windows からデタッチできないため、を使用して `wsl --mount` ブートデバイスのパーティションを読み取ることはできません。

- USB フラッシュドライブは現時点ではサポートされていないため、WSL 2 へのアタッチに失敗します。 ただし、USB ディスクはサポートされています。

- によってマウントできるのは、カーネルでネイティブでサポートされているファイルシステムだけ `wsl --mount` です。 これは、を呼び出すことによって、インストールされているファイルシステムドライバー (たとえば、ntfs 3g など) を使用できないことを意味 `wsl --mount` します。
