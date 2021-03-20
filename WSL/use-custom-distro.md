---
title: WSL で使用する Linux ディストリビューションをインポートする
description: Windows Subsystem for Linux で使用する Linux ディストリビューションをインポートする方法について説明します。
keywords: BashOnWindows、bash、wsl、windows、windows サブシステム、ディストリビューション、カスタム
ms.date: 02/17/2021
ms.topic: article
ms.openlocfilehash: e2f014600880de427f0c1b9a9bf54260798e8e25
ms.sourcegitcommit: aa6a9cb0d5daa62d8fd0e463a0fe5fa82612087c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104729324"
---
# <a name="import-any-linux-distribution-to-use-with-wsl"></a>WSL で使用する Linux ディストリビューションをインポートする 

Windows Subsystem for Linux (WSL) 内の任意の Linux ディストリビューションを使用できます。これは、 [Microsoft Store](https://www.microsoft.com/en-us/search/shop/apps?q=linux)で使用できない場合でも、tar ファイルを使用してインポートします。 

この記事では、Docker コンテナーを使用して tar ファイルを取得することにより、WSL で使用するために Linux ディストリビューション [Centos](https://www.centos.org/)をインポートする方法について説明します。 このプロセスは、Linux ディストリビューションをインポートするために適用できます。

## <a name="obtain-a-tar-file-for-the-distribution"></a>配布用の tar ファイルを取得する

まず、ディストリビューションのすべての Linux バイナリを含む tar ファイルを取得する必要があります。

Tar ファイルはさまざまな方法で取得できます。次の2つがあります。

- 提供された tar ファイルをダウンロードします。 Alpine の例については、 [Alpine Linux ダウンロード](https://alpinelinux.org/downloads/) サイトの「ミニルートファイルシステム」セクションを参照してください。
- Linux ディストリビューションコンテナーを検索し、インスタンスを tar ファイルとしてエクスポートします。 次の例では、 [Centos コンテナー](https://hub.docker.com/_/centos)を使用してこのプロセスを示します。

### <a name="obtaining-a-tar-file-for-centos-example"></a>CentOS サンプル用の tar ファイルの取得

この例では、WSL ディストリビューション内で Docker を使用して、CentOS の tar ファイルを取得します。

#### <a name="prerequisites"></a>前提条件

- Wsl [2 を実行している Linux ディストリビューションがインストールされている Wsl が有効になっ](./install-win10.md#manual-installation-steps)ている必要があります。
- WSL 2 エンジンが有効になっていて、次の手順で使用するディストリビューションに統合されていることを [確認した状態で、Docker Desktop For Windows がインストールされ](./tutorials/wsl-containers.md#install-docker-desktop) ている必要があります。

#### <a name="export-the-tar-from-a-container"></a>コンテナーからの tar のエクスポート

1. Microsoft Store (この例では Ubuntu) から既にインストールされている Linux ディストリビューションのコマンドライン (Bash) を開きます。 

2. Docker サービスを開始します。 

```bash
sudo service docker start
```

3. Docker 内で CentOS コンテナーを実行します。

```bash
docker run -t centos bash ls /
```

4. Grep と awk を使用して CentOS コンテナー ID を取得します。

```bash
dockerContainerID=$(docker container ls -a | grep -i centos | awk '{print $1}')
```

5. マウントされた c ドライブ上の tar ファイルにコンテナー ID をエクスポートします。

```bash
docker export $dockerContainerID > /mnt/c/temp/centos.tar
```

![上記のコマンドの実行例](./media/run-any-distro-tarfile.png)

このプロセスでは、WSL でローカルに使用するためにインポートできるように、Docker コンテナーから CentOS tar ファイルをエクスポートします。

## <a name="import-the-tar-file-into-wsl"></a>WSL に tar ファイルをインポートする

Tar ファイルを準備したら、コマンドを使用してインポート `wsl --import <Distro> <InstallLocation> <FileName>` できます。

### <a name="importing-centos-example"></a>CentOS のインポートの例

CentOS 配布 tar ファイルを WSL にインポートするには、次のようにします。

1. PowerShell を開き、ディストリビューションを格納するフォルダーが作成されていることを確認します。

```PowerShell
cd C:\temp
mkdir E:\wslDistroStorage\CentOS
```

2. コマンドを使用して、 `wsl --import <DistroName> <InstallLocation> <InstallTarFile>` tar ファイルをインポートします。 

```PowerShell
wsl --import CentOS E:\wslDistroStorage\CentOS .\centos.tar
```

3. コマンドを使用し `wsl -l -v` て、インストールされているディストリビューションを確認します。

![WSL で実行されている上記のコマンドの例](./media/run-any-distro-import.png)

4. 最後に、コマンドを使用し `wsl -d CentOS` て、新しくインポートした CentOS Linux ディストリビューションを実行します。

## <a name="add-wsl-specific-components-like-a-default-user"></a>既定のユーザーのような WSL 固有のコンポーネントを追加する

既定では、--import を使用する場合は、常にルートユーザーとして開始されます。 独自のユーザーアカウントを設定することもできますが、セットアッププロセスは、各 Linux ディストリビューションによって若干異なることに注意してください。

先ほどインポートした CentOS ディストリビューションでユーザーアカウントを設定するには、まず PowerShell を開き、次のコマンドを使用して CentOS でブートします。

```PowerShell
wsl -d CentOS
```

次に、CentOS コマンドラインを開きます。 このコマンドを使用して、sudo とパスワード設定ツールを CentOS にインストールし、ユーザーアカウントを作成して、既定のユーザーとして設定します。 この例では、ユーザー名は ' caloewen ' になります。 

```bash
yum update -y && yum install passwd sudo -y
myUsername=caloewen
adduser -G wheel $myUsername
echo -e "[user]\ndefault=$myUsername" >> /etc/wsl.conf
passwd $myUsername
```

そのインスタンスを終了し、すべての WSL インスタンスが終了していることを確認する必要があります。 PowerShell で次のコマンドを実行して、新しい既定のユーザーを表示するには、もう一度ディストリビューションを開始します。

```PowerShell
wsl --shutdown
wsl -d CentOS
```

`[caloewen@loewen-dev]$`これで、この例に基づいて出力が表示されます。

![WSL で実行されている上記のコードの例](./media/run-any-distro-customuser.png)

WSL 設定の構成の詳細については、「 [起動コマンド & 構成](./wsl-config.md#configure-per-distro-launch-settings-with-wslconf)」を参照してください。

## <a name="use-a-custom-linux-distribution"></a>カスタム Linux ディストリビューションを使用する

UWP アプリとしてパッケージ化された独自のカスタマイズされた Linux ディストリビューションを作成できます。これは、Microsoft Store で使用できる WSL ディストリビューションと同じように動作します。 詳細については、「 [WSL 用のカスタム Linux ディストリビューションの作成](./build-custom-distro.md)」を参照してください。
