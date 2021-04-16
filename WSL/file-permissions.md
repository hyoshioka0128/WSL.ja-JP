---
title: WSL のファイルのアクセス許可
description: WSL が Windows でファイルのアクセス許可を特定する方法について
keywords: BashOnWindows, bash, wsl, wsl2, windows, linux 用 windows サブシステム, windowssubsystem, ubuntu, debian, suse, windows 10, ファイル, アクセス許可
ms.date: 01/14/2020
ms.topic: article
ms.assetid: 7afaeacf-435a-4e58-bff0-a9f0d75b8a51
ms.localizationpriority: high
ms.openlocfilehash: 01bf0d66267a64a7fba21d2cdeca3fe68a9b42fa
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493524"
---
# <a name="file-permissions-for-wsl"></a>WSL のファイルのアクセス許可

このページでは、特に NT ファイル システム上の Windows 内のリソースにアクセスした際に、Linux 用 Windows サブシステム全体で Linux のファイルのアクセス許可がどのように解釈されるかについて詳しく説明します。 このドキュメントでは、[Linux ファイル システムのアクセス許可の構造](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)と [umask コマンド](https://en.wikipedia.org/wiki/Umask)について基本的な知識があることを前提としています。

WSL から Windows ファイルにアクセスした際、ファイルのアクセス許可は Windows のアクセス許可から計算されるか、WSL によってファイルに追加されたメタデータから読み取られます。 このメタデータは、既定では有効になっていません。

## <a name="wsl-metadata-on-windows-files"></a>Windows ファイルの WSL メタデータ

WSL のマウント オプションとしてメタデータが有効な場合、Windows NT ファイルの拡張属性を追加および解釈することで、Linux ファイル システムのアクセス許可を提供することができます。

WSL では、次の 4 つの NTFS 拡張属性を追加できます。

| 属性名 | 説明 |
| --- | --- |
| $LXUID | ユーザー所有者 ID |
| $LXGID | グループ所有者 ID |
| $LXMOD | ファイル モード (ファイル システムのアクセス許可の 8 進数と種類。例: 0777) |
| $LXDEV | デバイス (デバイス ファイルの場合) |

さらに、通常のファイルやディレクトリではないファイル (例: シンボリック リンク、FIFO、ブロック デバイス、UNIX ソケット、文字デバイス) には、NTFS [再解析ポイント](/windows/win32/fileio/reparse-points)もあります。 これにより、特定のディレクトリ内のファイルの種類を、その拡張属性を照会しなくても、はるかにすばやく特定できます。

## <a name="file-access-scenarios"></a>ファイル アクセスのシナリオ

以下は、Linux 用 Windows サブシステムを使用してさまざまな方法でファイルにアクセスするときに、アクセス許可がどのように特定されるかを説明したものです。

### <a name="accessing-files-in-the-windows-drive-file-system-drvfs-from-linux"></a>Linux から Windows ドライブ ファイル システム (DrvFS) のファイルにアクセスする

これらのシナリオは、WSL から (ほとんどの場合 `/mnt/c` 経由で) Windows ファイルにアクセスする場合に生じるものです。

#### <a name="reading-file-permissions-from-an-existing-windows-file"></a>既存の Windows ファイルからファイルのアクセス許可を読み取る

結果は、ファイルに既存のメタデータがあるかどうかによって異なります。

##### <a name="drvfs-file-does-not-have-metadata-default"></a>DrvFS ファイルにメタデータがない場合 (既定)

ファイルにメタデータが関連付けられていない場合は、Windows ユーザーの有効なアクセス許可が読み取りビット、書き込みビット、または実行ビットに変換され、これらが "ユーザー"、"グループ"、および "その他" に対して同じ値として設定されます。 たとえば、Windows ユーザー アカウントにファイルの読み取りおよび実行アクセス権がある一方で書き込みアクセス権がない場合、これは "ユーザー"、"グループ"、および "その他" に対して `r-x` と表示されます。 Windows でファイルに "読み取り専用" 属性が設定されている場合、Linux で書き込みアクセス権は付与されません。

##### <a name="the-file-has-metadata"></a>ファイルにメタデータがある場合

ファイルにメタデータが存在する場合は、Windows ユーザーの有効なアクセス許可を変換する代わりに、これらのメタデータ値がそのまま使用されます。

#### <a name="changing-file-permissions-on-an-existing-windows-file-using-chmod"></a>chmod を使用して既存の Windows ファイルのファイル アクセス許可を変更する

結果は、ファイルに既存のメタデータがあるかどうかによって異なります。

##### <a name="chmod-file-does-not-have-metadata-default"></a>chmod ファイルにメタデータがない場合 (既定)

chmod の効果は 1 つだけです。ファイルのすべての書き込み属性を削除すると、Windows ファイルに "読み取り専用" 属性が設定されます。これは、Linux の SMB (Server Message Block) クライアントである CIFS (Common Internet File System) と同じ動作であるためです。

##### <a name="chmod-file-has-metadata"></a>chmod ファイルにメタデータがある場合

chmod を使用すると、ファイルの既存のメタデータに応じて、メタデータを変更または追加できます。 

たとえメタデータに示されていても、Windows 上で与えられている以上のアクセス権を自分に与えることはできないことに注意してください。 たとえば、`chmod 777` を使用してファイルに対する書き込みアクセス許可があることを示すメタデータを設定することはできますが、そのファイルへのアクセスを試みたときにそのファイルに書き込むことはできません。 これは、相互運用性により、Windows ファイルに対するすべての読み取りまたは書き込みコマンドが Windows ユーザーのアクセス許可を介してルーティングされるためです。

#### <a name="creating-a-file-in-drivefs"></a>DriveFS にファイルを作成する

結果は、メタデータが有効になっているかどうかによって異なります。

##### <a name="metadata-is-not-enabled-default"></a>メタデータが有効になっていない場合 (既定)

新しく作成されたファイルの Windows アクセス許可は、特定のセキュリティ記述子なしで Windows でファイルを作成した場合と同じく、親のアクセス許可から継承されます。

##### <a name="metadata-is-enabled"></a>メタデータが有効になっている場合

ファイルのアクセス許可ビットは Linux umask に従うように設定され、ファイルと共にメタデータが保存されます。

#### <a name="which-linux-user-and-linux-group-owns-the-file"></a>どの Linux ユーザーおよび Linux グループがファイルを所有しているか 

結果は、ファイルに既存のメタデータがあるかどうかによって異なります。

##### <a name="user-file-does-not-have-metadata-default"></a>ユーザー ファイルにメタデータがない場合 (既定)

既定のシナリオでは、Windows ドライブを自動マウントするときに、任意のファイルのユーザー ID (UID) が WSL ユーザーのユーザー ID に設定され、グループ ID (GID) が WSL ユーザーのプリンシパル グループ ID に設定されるように指定します。

##### <a name="user-file-has-metadata"></a>ユーザー ファイルにメタデータがある場合

メタデータに指定されている UID および GID は、ファイルのユーザー所有者およびグループ所有者として適用されます。

### <a name="accessing-linux-files-from-windows-using-wsl"></a>`\\wsl$` を使用して Windows から Linux ファイルにアクセスする

`\\wsl$` 経由で Linux ファイルにアクセスする場合は、WSL ディストリビューションの既定のユーザーが使用されます。 したがって、Linux ファイルにアクセスするすべての Windows アプリに、既定のユーザーと同じアクセス許可が付与されます。

#### <a name="creating-a-new-file"></a>新しいファイルを作成する

Windows から WSL ディストリビューション内に新しいファイルを作成する場合は、既定の umask が適用されます。 既定の umask は `022` です。つまり、"グループ" と "その他" に対する書き込みアクセス許可を除くすべてのアクセス許可が許可されます。 

### <a name="accessing-files-in-the-linux-root-file-system-from-linux"></a>Linux から Linux ルート ファイル システム内のファイルにアクセスする

Linux ルート ファイル システム内で作成、変更、またはアクセスされるすべてのファイルには、新しく作成されたファイルに umask を適用するといった標準の Linux 規則が適用されます。

## <a name="configuring-file-permissions"></a>ファイルのアクセス許可を構成する

wsl.conf 内でマウント オプションを使用して、Windows ドライブ内のファイルのアクセス許可を構成できます。 マウント オプションを使用すると、`umask`、`dmask`、および `fmask` のアクセス許可マスクを設定できます。 `umask` はすべてのファイルに適用され、`dmask` はディレクトリにのみ適用されます。`fmask` はファイルにのみ適用されます。 これらのアクセス許可のマスクは、ファイルに適用されるときに論理 OR 演算が適用されます。たとえば、`umask` の値が `023` で、`fmask` の値が `022` の場合、ファイルに対する結果のアクセス許可マスクは `023` になります。

これを行う方法については、「[ディストリビューションごとの起動設定を wslconf で構成する](./wsl-config.md#configure-per-distro-launch-settings-with-wslconf)」を参照してください。