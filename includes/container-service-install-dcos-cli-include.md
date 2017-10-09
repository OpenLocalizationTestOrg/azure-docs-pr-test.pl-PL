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
> Te informacje dotyczą pracy z klastrami usługi ACS opartymi na kontrolerach domeny/systemach operacyjnych. Brak toodo nie konieczności to w przypadku klastrów usługi ACS opartymi na Swarm.
> 
> 

Najpierw [połączenia klastra tooyour ACS systemu DC/OS](../articles/container-service/container-service-connect.md). Po wykonaniu tej hello interfejsu wiersza polecenia DC/OS można zainstalować na komputerze klienckim z poleceniami hello poniżej:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Jeśli używasz starszej wersji środowiska Python, mogą zostać wyświetlone ostrzeżenia „InsecurePlatformWarnings”. Możesz je bezpiecznie zignorować.

W kolejności tooget pracę bez ponownego uruchamiania powłoki Uruchom polecenie:

```bash
source ~/.bashrc
```

Ta czynność nie będzie konieczna w przypadku uruchomienia nowych powłok.

Teraz można potwierdzić tego hello instalowania interfejsu wiersza polecenia:

```bash
dcos --help
```