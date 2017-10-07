---
title: grupy aaaResource dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello klucza projekt i implementację wytyczne dotyczące wdrażanie grup zasobów w usługach infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>Zasady dla grup zasobów platformy Azure dla maszyn wirtualnych systemu Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na sposób toologically tworzenia środowiska i grupy wszystkich składników hello w grupach zasobów.

## <a name="implementation-guidelines-for-resource-groups"></a>Implementacja — wskazówki dla grup zasobów
Decyzje:

* Będą toobuild limit grup zasobów hello podstawowe składniki infrastruktury lub kompletna aplikacja wdrożenia?
* Czy potrzebna jest tooResource dostępu toorestrict grupy przy użyciu kontroli dostępu opartej na rolach?

Zadania:

* Zdefiniuj co podstawowe składniki infrastruktury i grup zasobów, należy w wersji dedykowanej.
* Przegląd sposobu tooimplement szablony Menedżera zasobów dla spójne, powtarzalnych wdrożeń.
* Zdefiniuj role dostępu użytkownika należy kontrolować dostęp tooResource grupy.
* Utwórz zestaw hello grup zasobów zgodnie z konwencją nazewnictwa. Możesz użyć programu Azure PowerShell lub portalu hello.

## <a name="resource-groups"></a>Grupy zasobów
Na platformie Azure możesz logicznie grupować powiązane zasoby, takie jak kont magazynu, sieci wirtualnych i toodeploy maszynach wirtualnych (VM), zarządzania i obsługi je jako pojedynczy element. Takie podejście umożliwia łatwiejsze aplikacji toodeploy podczas przechowywania hello wszystkich powiązanych zasobów razem z punktu widzenia zarządzania lub toogrant inne grupy toothat dostępu do zasobów. Nazwy grup zasobów może zawierać maksymalnie 90 znaków długości. Aby uzyskać bardziej kompleksowego wglądu grup zasobów, przeczytaj hello [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Kluczowym elementem grupy tooResource ma zdolność toobuild Twoje środowisko za pomocą szablonów. Szablon jest po prostu pliku JSON, który deklaruje hello, sieci, magazynu i zasoby obliczeniowe. Można również definiować wszelkie pokrewne skrypty lub tooapply konfiguracji. Za pomocą tych szablonów, możesz tworzyć spójne, odtworzenia wdrożeń dla aplikacji. Takie podejście umożliwia łatwe toobuild środowisko rozwoju, a następnie użyj tego samego toocreate szablonu wdrożenia produkcyjnego, albo na odwrót. Lepsze zrozumienie za pomocą szablonów, należy przeczytać [hello Przewodnik po szablonie](../../azure-resource-manager/resource-manager-template-walkthrough.md) który przeprowadzi Cię przez każdy krok hello zbudowaniu szablonu.

Istnieją dwa różne podejścia, które należy wykonać podczas projektowania środowiska z grupami zasobów:

* Grupy zasobów dla każdego wdrożenia aplikacji, które łączy hello kont magazynu, sieci wirtualnych i podsieci, maszyn wirtualnych, załadować równoważenia itp.
* Scentralizowane grup zasobów, zawierające podstawowe wirtualne sieci i podsieci lub magazynu konta. Aplikacje są następnie własne grupy zasobów, zawierających tylko maszyny wirtualne, usługi równoważenia obciążenia, interfejsy sieciowe itp.

Skalowanie w poziomie, tworzenie scentralizowane grup zasobów w sieciach wirtualnych i podsieci umożliwia łatwiejsze toobuild między lokalizacjami sieci połączeń dla opcji łączności hybrydowego. informacje o innym podejściu Hello jest dla każdej aplikacji toohave własnych sieci wirtualnych, które wymagają konfiguracji i konserwacji.  [Kontrola dostępu oparta na rolach](../../active-directory/role-based-access-control-what-is.md) zapewniają dostęp toocontrol szczegółowego sposób tooResource grup. Dla aplikacji produkcyjnych można kontrolować hello użytkowników, którzy mogą uzyskiwać dostęp do tych zasobów lub zasobów infrastruktury core hello można ograniczyć tylko toowork inżynierów infrastruktury z nimi. Właściciele Twojej aplikacji mają tylko składniki aplikacji toohello dostępu w ramach ich nie hello podstawowej infrastruktury platformy Azure środowiska i grupy zasobów. Podczas projektowania środowiska, należy wziąć pod uwagę hello użytkowników, którzy wymagają dostępu do zasobów toohello i odpowiednio projektu grupy zasobów. 

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

