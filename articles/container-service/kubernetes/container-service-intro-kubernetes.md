---
title: "tooAzure aaaIntroduction usługi kontenera dla Kubernetes | Dokumentacja firmy Microsoft"
description: "Usługa kontenera platformy Azure dla Kubernetes umożliwia proste toodeploy aplikacji i zarządzanie nimi na podstawie kontenera na platformie Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, Containers, Microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Wprowadzenie tooAzure usługi kontenera dla Kubernetes
Usługa kontenera platformy Azure dla Kubernetes umożliwia proste toocreate, konfigurowanie i Zarządzanie klastrem maszyn wirtualnych, które są wstępnie skonfigurowane toorun konteneryzowanych aplikacji. Umożliwia możesz toouse Twojego posiadane umiejętności lub sięgać duży i rosnącym treści doświadczenia społeczności, toodeploy i Zarządzaj aplikacjami w kontenerze w systemie Microsoft Azure.

Za pomocą usługi kontenera platformy Azure, można skorzystać z hello korporacyjnej funkcji platformy Azure, zachowując przenośność aplikacji za pośrednictwem Kubernetes i hello Docker format obrazu.

## <a name="using-azure-container-service-for-kubernetes"></a>Używanie usługi Azure Container Service ma potrzeby rozwiązania Kubernetes
Naszym celem z usługi kontenera platformy Azure jest tooprovide środowisko macierzyste kontenera za pomocą open source, narzędzia i technologie, które są obecnie popularnością wśród klientów. końcowy toothis uwidaczniamy hello standardowe Kubernetes punkty końcowe interfejsu API. Za pomocą tych standardowych punktów końcowych, można wykorzystać dowolne oprogramowanie, które jest w stanie mówić tooa Kubernetes klastra. Możesz wybrać narzędzie [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) lub [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Tworzenie klastra Kubernetes przy użyciu usługi Azure Container Service
toobegin przy użyciu usługi kontenera platformy Azure, wdrażanie klastra usługi kontenera platformy Azure z hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) lub za pośrednictwem portalu hello (hello wyszukiwania portalu Marketplace dla **usługi kontenera platformy Azure**). Jeśli jesteś użytkownikiem zaawansowanym, który musi mieć większą kontrolę nad hello szablonów usługi Azure Resource Manager, można użyć typu open source hello [aparat acs](https://github.com/Azure/acs-engine) toobuild projektu własne niestandardowe Kubernetes klastra i wdróż je za pośrednictwem hello `az` interfejsu wiersza polecenia.

### <a name="using-kubernetes"></a>Korzystanie z rozwiązania Kubernetes
Narzędzie Kubernetes automatyzuje proces wdrażania i skalowania aplikacji konteneryzowanych oraz zarządzania nimi. Narzędzie to obejmuje bogaty zestaw funkcji, m.in.:
* automatyczne pakowanie pudełek,
* mechanizm samonaprawiania
* skalowanie w poziomie,
* odnajdywanie usług i równoważenie obciążenia,
* zautomatyzowane wprowadzanie i wycofywanie zmian,
* zarządzanie kluczami tajnymi i konfiguracją,
* aranżacja magazynu,
* wykonywanie partii zadań.

Diagram architektury rozwiązania Kubernetes wdrażanej za pomocą usługi Azure Container Service:

![Usługa kontenera platformy Azure skonfigurowane toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Filmy wideo

Obsługa klastra Kubernetes w usłudze Azure Container Service (Azure Friday, styczeń 2017 r.):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Narzędzia do tworzenia i wdrażania aplikacji w systemie Kubernetes (Azure OpenDev, czerwiec 2017 r.):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Następne kroki

Eksploruj hello [szybkiego startu Kubernetes](container-service-kubernetes-walkthrough.md) toobegin dzisiaj Eksplorowanie usługi kontenera platformy Azure.
