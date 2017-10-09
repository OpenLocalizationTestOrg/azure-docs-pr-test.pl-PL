---
title: Witaj aaaInstall interfejsu wiersza polecenia DC/OS | Dokumentacja firmy Microsoft
description: Zainstaluj hello interfejsu wiersza polecenia DC/OS.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, mikrousługi, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="d9a9d-104">Te informacje dotyczą pracy z klastrami usługi ACS opartymi na kontrolerach domeny/systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d9a9d-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="d9a9d-105">Brak toodo nie konieczności to w przypadku klastrów usługi ACS opartymi na Swarm.</span><span class="sxs-lookup"><span data-stu-id="d9a9d-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="d9a9d-106">Najpierw [połączenia klastra tooyour ACS systemu DC/OS](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d9a9d-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="d9a9d-107">Po wykonaniu tej hello interfejsu wiersza polecenia DC/OS można zainstalować na komputerze klienckim z poleceniami hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9a9d-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="d9a9d-108">Jeśli używasz starszej wersji środowiska Python, mogą zostać wyświetlone ostrzeżenia „InsecurePlatformWarnings”.</span><span class="sxs-lookup"><span data-stu-id="d9a9d-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="d9a9d-109">Możesz je bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="d9a9d-109">You can safely ignore these.</span></span>

<span data-ttu-id="d9a9d-110">W kolejności tooget pracę bez ponownego uruchamiania powłoki Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="d9a9d-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="d9a9d-111">Ta czynność nie będzie konieczna w przypadku uruchomienia nowych powłok.</span><span class="sxs-lookup"><span data-stu-id="d9a9d-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="d9a9d-112">Teraz można potwierdzić tego hello instalowania interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="d9a9d-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```