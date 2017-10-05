---
title: "Grupy zasobów dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące wdrażania grup zasobów w usługach infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 452acde571164a3ab4ce2dcccf99d2aed90361fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Zasady dla grup zasobów platformy Azure dla maszyn wirtualnych systemu Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na logicznie tworzenia środowiska i grupach wszystkich składników w grupach zasobów.

## <a name="implementation-guidelines-for-resource-groups"></a>Implementacja — wskazówki dla grup zasobów
Decyzje:

* Zamierzasz tworzenia grup zasobów przez podstawowe składniki infrastruktury lub kompletna aplikacja wdrożenia?
* Należy ograniczyć dostęp do grupy zasobów przy użyciu kontroli dostępu opartej na rolach?

Zadania:

* Zdefiniuj co podstawowe składniki infrastruktury i grup zasobów, należy w wersji dedykowanej.
* Przejrzyj implementowania szablony Menedżera zasobów dla wdrożeń spójny, odtworzenia.
* Zdefiniuj role dostępu użytkownika należy do kontrolowania dostępu do grupy zasobów.
* Utwórz zestaw grup zasobów zgodnie z konwencją nazewnictwa. Można użyć wiersza polecenia platformy Azure lub portalu.

## <a name="resource-groups"></a>Grupy zasobów
Na platformie Azure logicznie grupują zasoby pokrewne, takie jak konta magazynu, sieci wirtualnych i maszyn wirtualnych (VM) do wdrażania, zarządzania i obsługi je jako pojedynczy element. Takie podejście ułatwia do wdrażania aplikacji przy jednoczesnym zachowaniu wszystkie powiązane zasoby razem z punktu widzenia zarządzania lub uzyskać inne dostęp do tej grupy zasobów. Nazwy grup zasobów może zawierać maksymalnie 90 znaków długości. Dla bardziej kompleksowego wglądu grup zasobów, możesz przeczytać [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

To kluczowa funkcja dostępna na grupy zasobów jest możliwość tworzenia środowiska przy użyciu pliku JSON, który deklaruje sieci, magazynu i zasoby obliczeniowe. Można również definiować ani pokrewne skrypty niestandardowe konfiguracje do zastosowania. Za pomocą tych szablonów JSON, możesz tworzyć spójne, odtworzenia wdrożeń dla aplikacji. To rozwiązanie umożliwia środowisko rozwoju kompilacji, a następnie użyj tego samego szablonu do utworzenia wdrożenia produkcyjnego, albo na odwrót. Aby lepiej zrozumieć o za pomocą szablonów, należy przeczytać [wskazówki szablonu](../../azure-resource-manager/resource-manager-template-walkthrough.md) który przeprowadzi Cię przez każdy krok zbudowaniu szablonu JSON.

Istnieją dwa różne podejścia, które należy wykonać podczas projektowania środowiska z grupami zasobów:

* Grupy zasobów dla każdego wdrożenia aplikacji, które łączy kont magazynu, sieci wirtualnych i podsieci, maszyn wirtualnych, załadować równoważenia itp.
* Scentralizowane grup zasobów, zawierające podstawowe wirtualne sieci i podsieci lub magazynu konta. Aplikacje są następnie własne grupy zasobów, zawierających tylko maszyny wirtualne, usługi równoważenia obciążenia, interfejsy sieciowe itp.

Jak można skalowania w poziomie, tworzenie scentralizowane grup zasobów dla sieci wirtualnych i podsieci ułatwia tworzenie między lokalizacjami sieci połączeń dla opcji łączności hybrydowego. Innym podejściem jest dla każdej aplikacji ma własnych sieci wirtualnych, które wymagają konfiguracji i konserwacji. [Kontrola dostępu oparta na rolach](../../active-directory/role-based-access-control-what-is.md) umożliwiają szczegółową kontrolę dostępu do grupy zasobów. Dla aplikacji produkcyjnych można kontrolować użytkowników, którzy mogą uzyskiwać dostęp do tych zasobów lub zasobów infrastruktury podstawowej można ograniczyć tylko infrastruktury engineers, aby pracować z nimi. Właściciele Twojej aplikacji tylko mają dostęp do składników aplikacji w ramach ich grupy zasobów i nie podstawowej infrastruktury platformy Azure środowiska. Podczas projektowania środowiska, należy wziąć pod uwagę użytkowników, którzy wymagają dostępu do zasobów i odpowiednio projektu grupy zasobów. 

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

