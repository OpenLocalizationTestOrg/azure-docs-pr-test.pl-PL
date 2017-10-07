---
title: "pule agenta aaaDC/OS usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak działają hello agenta publicznego i prywatnego pule z klastrem usługi kontenera platformy Azure DC/OS"
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
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Pule agenta DC/OS usługi kontenera platformy Azure
Klastry DC/OS usługi kontenera platformy Azure zawierają węzły agenta w dwie pule, puli publicznych i prywatnych puli. Aplikację można wdrożyć puli tooeither wpływu na dostępność między komputerami w usłudze kontenera. Hello maszyny mogą być narażone toohello internet (publicznej) lub wewnętrzny (prywatny). Ten artykuł zawiera krótki przegląd, dlatego są pule publiczne i prywatne.


* **Agenci prywatnej**: węźle prywatnego agent uruchomiony za pośrednictwem sieci bez obsługi routingu. Ta sieć jest dostępny tylko ze strefy admin hello lub za pośrednictwem routera brzegowego publicznego strefy hello. Domyślnie DC/OS uruchamia aplikacje na węzłach prywatny agenta. 

* **Agentów publicznych**: węzłów agenta publicznego Uruchom aplikacje DC/OS i usługi za pośrednictwem publicznie dostępnej sieci. 

Aby uzyskać więcej informacji o zabezpieczeniach sieci DC/OS, zobacz hello [dokumentacji DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Wdrażanie pul agenta

pule agenta DC/OS Hello w usłudze kontenera platformy Azure są tworzone w następujący sposób:

* Hello **prywatnej puli** zawiera hello liczbę węzłów agenta, że możesz określić, kiedy użytkownik [wdrożyć klaster DC/OS hello](container-service-deployment.md). 

* Witaj **puli publicznych** początkowo zawiera wstępnie określoną liczbę węzłów agenta. Ta pula jest automatycznie dodawane po zainicjowaniu obsługi klastra DC/OS hello.

Hello puli prywatnych i puli publicznych hello są zestawy skalowania maszyny wirtualnej platformy Azure. Po wdrożeniu mogą zmieniać rozmiar te pule.

## <a name="use-agent-pools"></a>Pule agenta
Domyślnie **Marathon** wdraża żadnych nowych aplikacji toohello *prywatnej* węzłów agenta. Należy wdrożyć toohello aplikacji hello tooexplicitly *publicznego* węzłów podczas tworzenia aplikacji hello hello. Wybierz hello **opcjonalnie** i wprowadzić **slave_public** dla hello **zaakceptowane role zasobów** wartość. Ten proces jest udokumentowany [tutaj](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) w hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) dokumentacji.

## <a name="next-steps"></a>Następne kroki
* Przeczytaj więcej na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).

* Dowiedz się, jak za[Otwórz zaporę Windows hello](container-service-enable-public-access.md) podał Azure tooallow dostępu publicznego tooyour DC/OS kontenerów.

