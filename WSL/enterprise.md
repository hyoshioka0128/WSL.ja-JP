---
title: エンタープライズ向けの WSL
description: エンタープライズ環境で WSL を最適に使用する方法に関するリソースと手順。
keywords: BashOnWindows, bash, wsl, windows, linux 用 windows サブシステム, windowssubsystem, ubuntu, debian, suse, windows 10, エンタープライズ, デプロイ, オフライン, パッケージング, ストア, ディストリビューション, インストール, インストール
ms.date: 12/14/2020
ms.topic: article
ms.assetid: 7afaeacf-435a-4e58-bff0-a9f0d75b8a51
ms.custom: seodec18
ms.openlocfilehash: 8c5e1c84767423a2d415709d184c9e96a5a3de47
ms.sourcegitcommit: 17d5ea1fe571274c224202544f61035971d6e0e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2021
ms.locfileid: "100551015"
---
# <a name="windows-subsystem-for-linux-for-enterprise"></a>エンタープライズ向け Windows Subsystem for Linux

管理者またはマネージャーという立場で、すべての開発者に対して、同じ承認済みソフトウェアを使用することを必須にする場合があります。 このような一貫性があると、適切に定義された作業環境を作成するために役立ちます。 Linux 用 Windows サブシステムを使用すると、カスタムの WSL イメージをあるマシンから次のマシンにインポートおよびエクスポートできるので、この一貫性に役立ちます。 詳細については、以下のガイドを参照してください。

* [カスタムの WSL イメージを作成する](#creating-a-custom-wsl-image)
* [WSL イメージの配布](#distributing-your-wsl-image)
* [Linux のディストリビューションとパッケージの更新およびパッチ](#update-and-patch-linux-distributions-and-packages)
* [エンタープライズのセキュリティと制御のオプション](#enterprise-security-and-control-options)

## <a name="creating-a-custom-wsl-image"></a>カスタムの WSL イメージを作成する

一般に "イメージ" と呼ばれるものは、簡単に説明すると、ファイルに保存されたソフトウェアとそのコンポーネントのスナップショットです。 Linux 用 Windows サブシステムの場合、イメージは、サブシステム、そのディストリビューション、そのディストリビューションにインストールされているすべてのソフトウェアとパッケージで構成されます。

WSL イメージの作成を開始するには、まず [Linux 用 Windows サブシステムをインストールします](./install-win10.md)。

インストールしたら、ビジネス向け Microsoft Store を使用して適切な Linux ディストリビューションをダウンロードし、インストールします。 [ビジネス向け Microsoft Store](https://docs.microsoft.com/microsoft-store/sign-up-microsoft-store-for-business.) を使用してアカウントを作成する

### <a name="exporting-your-wsl-image"></a>WSL イメージのエクスポート

カスタムの WSL イメージをエクスポートするには、wsl --export `<Distro> <FileName>` を実行します。これにより、イメージは tar ファイルにラップされ、他のマシンに配布できるようになります。

## <a name="distributing-your-wsl-image"></a>WSL イメージの配布

共有デバイスまたはストレージ デバイスから WSL イメージを配布するには、wsl --import `<Distro> <InstallLocation> <FileName>` を実行します。これにより、指定した tar ファイルが新しい配布としてインポートされます。

## <a name="update-and-patch-linux-distributions-and-packages"></a>Linux のディストリビューションとパッケージの更新およびパッチ

Linux ユーザー領域の監視と管理には、Linux 構成マネージャー ツールを使用することを強くお勧めします。 選択できる Linux 構成マネージャーは多数あります。 WSL 2 に Puppet をインストールする方法については、この[ブログ投稿](http://www.craigloewen.com/blog/2019/12/04/running-puppet-quickly-in-wsl2/)を参照してください。

## <a name="enterprise-security-and-control-options"></a>エンタープライズのセキュリティと制御のオプション

現在、WSL には、エンタープライズ シナリオでのユーザー エクスペリエンスの変更について限られた制御メカニズムが用意されています。 エンタープライズ機能は現在も開発中ですが、サポートされている機能とサポートされていない機能の領域を次に示します。 この一覧に含まれていない新機能をリクエストするには、[GitHub リポジトリ](https://github.com/microsoft/WSL/issues?q=is%3Aissue+is%3Aopen+enterprise)で問題を報告してください。

### <a name="supported"></a>サポートされています

* `wsl --import` と `wsl --export` を使用して承認済みのイメージを内部で共有する
* [WSL Distro Launcher リポジトリ](https://github.com/microsoft/WSL-DistroLauncher)を使用して自社向けに独自の WSL ディストリビューションを作成する

まだサポートされていませんが、調査中である機能の一覧を次に示します。

### <a name="currently-unsupported"></a>現在はサポートされていません

WSL 内で現在サポートされていない、一般的な機能の一覧を次に示します。 Microsoft ではこれらの要求を把握しており、追加方法を調査しています。 

* WSL 内のユーザーとホスト マシン上の Windows ユーザーとの同期
* Windows ツールを使用した Linux ディストリビューションとパッケージの更新とパッチの管理
* Windows Update を使用して WSL ディストリビューションのコンテンツも更新する
* 自社内のユーザーがアクセスできるディストリビューションの制御
* WSL 内での必須サービス (ログまたは監視) の実行
* SCCM や Intune などの Windows 構成マネージャー ツールを使用した Linux インスタンスの監視
* McAfee のサポート
