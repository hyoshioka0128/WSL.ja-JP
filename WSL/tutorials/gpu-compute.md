---
title: WSL での GPU 高速化による ML トレーニング
description: 詳細については、NVIDIA CUDA、DirectML、PyTorch の WSL 2 サポートに関するページを参照してください。 Machine Learning トレーニングを実行するときの GPU アクセラレーションのための Windows Subsystem for Linux サポートについては、「」を参照してください。
keywords: wsl、windows、windows サブシステム、gpu コンピューティング、gpu アクセラレーション、NVIDIA、CUDA、DirectML、、PyTorch、NVIDIA CUDA preview、GPU ドライバー、NVIDIA Container Toolkit、Docker
ms.date: 04/07/2021
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 0123c4fc93e3c3a017302a2044068287ec29fe9b
ms.sourcegitcommit: 7f4a813fdcbfca65412ecb2311f0b5c8b546fef8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107493484"
---
# <a name="gpu-accelerated-machine-learning-training-in-the-windows-subsystem-for-linux"></a>Windows Subsystem for Linux での GPU アクセラレータによる機械学習トレーニング

GPU コンピューティングのサポートは、最も要求の厳しい WSL 機能 #1、Windows Insider プログラムを使用してプレビューできるようになりました。 [ブログの投稿をお読みください](https://blogs.windows.com/windowsdeveloper/?p=55781)。

## <a name="what-is-gpu-compute"></a>GPU コンピューティングとは

多くのコンピューティング処理を要するタスクで GPU アクセラレーションを利用することは、"GPU コンピューティング" と呼ばれます。 GPU コンピューティングでは、GPU (グラフィックスプロセッシングユニット) を活用して、計算量の多いワークロードを高速化し、並列処理を使用して、多くの場合、CPU だけを利用するよりも、必要な計算を高速に実行します。 この並列処理によって、CPU 上で実行されている場合に、これらの計算負荷が高いワークロードで処理速度が大幅に向上します。 機械学習モデルのトレーニングは、このような負荷の高いタスクを実行するために GPU コンピューティングによって時間が大幅に短縮される優れた例です。

## <a name="install-and-set-up"></a>インストールと設定

WSL 2 のサポートと、DirectML ドキュメント内の [GPU アクセラレーショントレーニングガイド](/windows/win32/direct3d12/gpu-accelerated-training) で機械学習モデルのトレーニングを開始する方法の詳細については、こちらを参照してください。このガイドの内容は次のとおりです。

* DirectML を使用した、初級または学生向けのセットアップに関するガイダンス
* 既存の CUDA ML ワークフローの実行を開始するためのプロフェッショナル向けガイダンス
