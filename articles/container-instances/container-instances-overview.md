---
title: "Omówienie wystąpień kontenera aaaAzure | Dokumentacja platformy Azure"
description: "Informacje dotyczące usługi Azure Container Instances"
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Azure Container Instances

Kontenery staje się szybko hello preferowany sposób toopackage, wdrażanie i zarządzanie aplikacjami w chmurze. Wystąpień kontenera Azure oferuje hello najszybszym i Najprostszym sposobem toorun kontenera na platformie Azure, bez konieczności tooprovision wszystkie maszyny wirtualne i bez konieczności tooadopt wyższego poziomu usługi. 

Usługa Azure Container Instances to doskonałe rozwiązanie dla wszystkich scenariuszy, które może działać w kontenerach izolowanych, w tym w przypadku prostych aplikacji, automatyzacji zadań i zadań kompilacji. W scenariuszach, w którym musisz mieć pełne aranżacji kontenera, w wielu kontenerów, automatyczne skalowanie i uaktualnień aplikacji w skoordynowany sposób, w tym odnajdywania usługi zalecamy hello [usługi kontenera platformy Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Krótki czas uruchamiania

Kontenery oferują znaczące korzyści związane z uruchamianiem w porównaniu do maszyn wirtualnych. Wystąpień kontenera platformy Azure możesz uruchomić kontenera na platformie Azure w sekundach bez tooprovision potrzeby hello i zarządzenie maszynami wirtualnymi.

## <a name="hypervisor-level-security"></a>Zabezpieczenia na poziomie funkcji hypervisor

W przeszłości kontenery oferowały zarządzanie zasobami i izolację zależności aplikacji, ale nie były wystarczająco odporne na użycie wielu obcych dzierżaw. Dzięki usłudze Azure Container Instances aplikacja jest izolowana w kontenerze w takim samym stopniu, w jakim byłaby w maszynie wirtualnej.

## <a name="custom-sizes"></a>Rozmiary niestandardowe

Kontenery są zwykle zoptymalizowane toorun, który tylko jedną aplikację, ale hello musi dokładnie te aplikacje mogą się znacznie różnić. W usłudze Azure Container Instances możesz zażądać dokładnie tylu rdzeni i pamięci, ile potrzebujesz. Płacisz oparte na możesz poprosić, rozliczony przez hello drugie, tak aby precyzyjne zoptymalizować wydatki na podstawie Twoich potrzeb.

## <a name="public-ip-connectivity"></a>Łączność przy użyciu publicznych adresów IP

Wystąpieniami kontenera Azure mogą uwidaczniać kontenerów bezpośrednio toohello internet z publicznym adresem IP. W przyszłości hello firma Microsoft będzie rozwiń naszych sieci możliwości integracji tooinclude z sieciami wirtualnymi, obciążenia równoważenia i innych części core hello Azure infrastruktura sieci.

## <a name="persistent-storage"></a>Magazyn trwały

tooretrieve i utrwalić stanu z wystąpień kontenera platformy Azure, firma Microsoft oferuje udziały plików bezpośrednie instalowanie Azure.

## <a name="linux-and-windows-containers"></a>Kontenery systemów Linux i Windows

Z wystąpień kontenera platformy Azure można zaplanować zarówno systemu Windows i Linux kontenerów hello tego samego interfejsu API. Wystarczy wskazać hello podstawowy typ systemu operacyjnego i wszystkich innych urządzeń jest identyczny.

## <a name="co-scheduled-groups"></a>Grupy planowane wspólnie

Usługa Azure Container Instances obsługuje planowanie grup wielu kontenerów, które współużytkują maszynę hosta, sieć lokalną, magazyn i cykl życia. Dzięki temu można toocombine głównej aplikacji z innymi działającą w roli pomocniczych, takich jak rejestrowanie.

## <a name="next-steps"></a>Następne kroki

Spróbuj przeprowadzić wdrożenie tooAzure kontenera, z jednego polecenia za pomocą naszych [Przewodnik Szybki Start](container-instances-quickstart.md).
