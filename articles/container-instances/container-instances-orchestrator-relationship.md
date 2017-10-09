---
title: "aaaAzure wystąpień kontenera i aranżacji kontenera"
description: "Zrozumienie sposobu wystąpień kontenera Azure interakcji z orchestrators kontenera"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Wystąpień kontenera Azure i orchestrators kontenera

Ze względu na ich niewielki rozmiar i orientację aplikacji kontenerów dobrze nadają w środowiskach agile dostarczania i architektury mikrousługi systemem. zadanie Hello automatyzacji i zarządzanie dużą liczbę kontenerów i sposób ich interakcji nosi nazwę *aranżacji*. Kontener popularnych orchestrators obejmują Kubernetes DC/OS i Docker Swarm, które są dostępne w hello [usługi kontenera platformy Azure](https://docs.microsoft.com/azure/container-service/).

Wystąpień kontenera Azure zawiera niektóre z hello podstawowe planowanie możliwości platform aranżacji, ale nie obejmuje usług wyższa wartość hello czy tych platform zapewniają i w rzeczywistości może być uzupełniające się z nimi. W tym artykule opisano zakres hello obsługuje wystąpień kontenera Azure i jakiego orchestrators kontener może korzystać z niego.

## <a name="traditional-orchestration"></a>Tradycyjny aranżacji

Definicja standardowe Hello aranżacji obejmuje hello następujące zadania:

- **Planowanie**: danego obrazu kontenera i żądanie zasobu, Znajdź odpowiedniego komputera na powitania toorun kontenera.
- **Koligacja/przeciwko-affinity**: określić, że zestaw kontenery powinien uruchomione w pobliżu innych (na wydajność) lub wystarczająco liniami (dostępności).
- **Monitorowanie kondycji**: Obejrzyj niepowodzeń kontenera i automatycznie Zaplanuj je ponownie.
- **Tryb failover**: Śledź co działa na każdym komputerze i ponowne planowanie kontenery z węzłów toohealthy maszyn nie powiodło się.
- **Skalowanie**: Dodawanie lub usuwanie żądanie toomatch wystąpień kontenera, ręcznie lub automatycznie.
- **Sieć**: Podaj sieci nakładki koordynacji toocommunicate kontenery na wielu komputerach hosta.
- **Odnajdowanie usługi**: toolocate kontenery wzajemnie automatycznie włączyć nawet podczas przenoszenia między komputerami hostów i zmiana adresów IP.
- **Koordynowane uaktualnień aplikacji**: Zarządzanie aplikacją tooavoid uaktualnień kontenera czas przestoju i włączyć wycofywanie, jeśli jakaś nieprawidłowość.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orchestration z wystąpień kontenera platformy Azure: warstwowego podejścia

Wystąpień kontenera Azure umożliwia tooorchestration warstwowego podejścia, podając wszystkie hello planowania i możliwości zarządzania wymagane toorun jeden kontener, umożliwiając orchestrator platform toomanage kontenera wielu zadań na nim.

Ponieważ wszystkie hello podstawowej infrastruktury dla wystąpień kontenera jest zarządzane przez usługę Azure, platformy orchestrator nie jest konieczne tooconcern się z znajdowanie maszyny do odpowiedniego hosta, na które toorun jeden kontener. elastyczność Hello chmury hello gwarantuje, że co jest zawsze dostępna. Zamiast tego hello orchestrator można skoncentrować się na powitania zadania, które upraszczają programowanie hello architektury usługi kontenera, w tym skalowanie i skoordynowany sposób uaktualnienia.



## <a name="potential-scenarios"></a>Potencjalne scenariusze

Podczas integracji programu orchestrator z wystąpień kontenera Azure jest nadal rodzącego, przewidujemy, że mogą pojawić się w kilku różnych środowiskach:

### <a name="orchestration-of-container-instances-exclusively"></a>Orchestration wystąpień kontenera wyłącznie

Ponieważ szybkie rozpoczęcie i naliczać opłaty za hello drugie, środowisko wyłącznie na podstawie wystąpień kontenera Azure oferuje hello najszybszy sposób tooget uruchomiona i toodeal z obciążeniami wysokiej zmiennej.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Kombinacja wystąpień kontenera i kontenerów na maszynach wirtualnych

Dla długotrwałe, obciążeń stabilny, organizowanie kontenery w klastrze dedykowanych maszyn wirtualnych zwykle będzie tańsze niż uruchomienie tego samego kontenery hello z wystąpień kontenera. Jednak wystąpień kontenera oferuje doskonałe rozwiązanie do szybkiego rozszerzania i instytucje toodeal Twojego ogólną pojemność z nieoczekiwany lub krótkim okresie wzrostów użycia. Zamiast skalowania hello liczbę maszyn wirtualnych w klastrze, a następnie wdrażanie dodatkowych kontenerów na tych komputerach, hello orchestrator można po prostu zaplanować dodatkowe kontenery hello za pomocą wystąpień kontenera i usunąć je, gdy są one nie już potrzebne.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Przykładowe zastosowanie: Azure łącznik wystąpień kontenera dla Kubernetes

toodemonstrate jak kontenera platformy orchestration można zintegrować z wystąpień kontenera platformy Azure, możemy uruchomić budynku [łącznik próbki dla Kubernetes][aci-connector-k8s]. 

Witaj łącznika dla Kubernetes naśladuje hello [kubelet] [ kubelet-doc] przez zarejestrowanie jako węzeł o nieograniczonej pojemności i wysyła tworzenie hello [stanowiskami] [ pod-doc] jako kontenera grupy wystąpień kontenera platformy Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Łączniki dla innych orchestrators mogą być zbudowane analogicznie zintegrowaną z platformy podstawowych toocombine hello zasilania programu orchestrator hello interfejsu API za pomocą hello szybkość i łatwość zarządzania kontenerami w wystąpień kontenera platformy Azure.

> [!WARNING]
> Witaj ACI łącznika jest Kubernetes *eksperymentalne* i nie powinna być używana w środowisku produkcyjnym.

## <a name="next-steps"></a>Następne kroki

Tworzenie Twojego pierwszego kontenera z wystąpień kontenera Azure za pomocą hello [Przewodnik Szybki start dotyczący](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/