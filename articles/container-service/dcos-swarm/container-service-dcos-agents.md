---
title: "Pule agenta DC/OS usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak działają pule publiczny i prywatny agenta z klastrem usługi kontenera platformy Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Pule agenta DC/OS usługi kontenera platformy Azure
Klastry DC/OS usługi kontenera platformy Azure zawierają węzły agenta w dwie pule, puli publicznych i prywatnych puli. Aplikację można wdrożyć do jednej puli wpływu na dostępność między komputerami w usłudze kontenera. Maszyny można połączenie z Internetem (publicznej) lub przechowywane wewnętrzny (prywatny). Ten artykuł zawiera krótki przegląd, dlatego są pule publiczne i prywatne.


* **Agenci prywatnej**: węźle prywatnego agent uruchomiony za pośrednictwem sieci bez obsługi routingu. Ta sieć jest dostępny tylko ze strefy administratora lub za pośrednictwem routera brzegowego publicznego strefy. Domyślnie DC/OS uruchamia aplikacje na węzłach prywatny agenta. 

* **Agentów publicznych**: węzłów agenta publicznego Uruchom aplikacje DC/OS i usługi za pośrednictwem publicznie dostępnej sieci. 

Aby uzyskać więcej informacji o zabezpieczeniach sieci DC/OS, zobacz [dokumentacji DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Wdrażanie pul agenta

Pule agenta DC/OS w usłudze kontenera platformy Azure są tworzone w następujący sposób:

* **Prywatnej puli** zawiera liczbę węzłów agenta, że możesz określić, kiedy użytkownik [wdrożyć klaster DC/OS](container-service-deployment.md). 

* **Puli publicznych** początkowo zawiera wstępnie określoną liczbę węzłów agenta. Ta pula jest automatycznie dodawane po zainicjowaniu obsługi klastra DC/OS.

Pula prywatnych i publicznych puli są zestawy skalowania maszyny wirtualnej platformy Azure. Po wdrożeniu mogą zmieniać rozmiar te pule.

## <a name="use-agent-pools"></a>Pule agenta
Domyślnie **Marathon** wdraża każdej nowej aplikacji *prywatnej* węzłów agenta. Należy jawnie wdrożenia aplikacji na *publicznego* węzłów podczas tworzenia aplikacji. Wybierz **opcjonalnie** i wprowadzić **slave_public** dla **zaakceptowane role zasobów** wartość. Ten proces jest udokumentowany [tutaj](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) i [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) dokumentacji.

## <a name="next-steps"></a>Następne kroki
* Przeczytaj więcej na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).

* Dowiedz się, jak [otwórz Zaporę](container-service-enable-public-access.md) dostarczany przez platformę Azure, aby zezwolić na publiczny dostęp do kontenerów DC/OS.

