---
title: aaaAzure wytyczne maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o hello klucza projekt i implementację wskazówki dotyczące wdrażania maszyn wirtualnych systemu Linux na platformie Azure"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 0f779f791005441b6b16e106a3dc5a095bb33034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Wskazówki dotyczące maszyn wirtualnych platformy Azure dla systemu Linux
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł skupia się na powitania opis wymaganych czynności umożliwiające tworzenie i zarządzanie maszynach wirtualnych (VM) związane z planowaniem w środowisku platformy Azure.

## <a name="implementation-guidelines-for-vms"></a>Implementacja — wskazówki dla maszyn wirtualnych
Decyzje:

* Jak wiele maszyn wirtualnych są wymagane dla różnych warstwach aplikacji i składników infrastruktury?
* Jakie zasoby Procesora i pamięci jest konieczne każdej maszyny Wirtualnej, i jakie są wymagania dotyczące magazynu hello?

Zadania:

* Zdefiniuj hello obciążeń dla twojej aplikacji i hello zasobów powitalne wymagają maszyn wirtualnych.
* Wyrównuje hello zapotrzebowania na zasoby dla każdej maszyny Wirtualnej z hello odpowiedniego typu maszyny Wirtualnej rozmiaru i magazynu.
* Definiowanie grup zasobów do różnych warstw hello i składników infrastruktury.
* Definiowanie konwencji nazewnictwa sieci maszyny Wirtualnej.
* Tworzenie maszyn wirtualnych przy użyciu hello interfejsu wiersza polecenia Azure, sieci web portalu, lub z szablonami usługi Resource Manager.

## <a name="virtual-machines"></a>Maszyny wirtualne
Jeden z głównych zasobów hello w środowisku platformy Azure jest prawdopodobnie maszyn wirtualnych. Ten zasób jest, gdzie uruchomić aplikacji, baz danych, usługi uwierzytelniania,... itd.

Jest ważne toounderstand hello [różnych rozmiarów maszyn wirtualnych](sizes.md) toocorrectly rozmiar środowiska z punktu widzenia wydajności i kosztów. Jeśli maszyny wirtualne nie ma wystarczającej liczby rdzeni procesora CPU lub pamięci, wydajność aplikacji wystąpi niezależnie od tego, jak został zaprojektowany i rozwinięte. Przejrzyj hello sugerowane obciążeń dla każdej maszyny Wirtualnej serii jako punkt początkowy zdecydują których rozmiar toouse maszyny Wirtualnej dla każdego składnika w infrastrukturze. Możesz [Zmień rozmiar maszyny Wirtualnej hello](change-vm-size.md) po wdrożeniu.

Magazyn odgrywa kluczową rolę w wydajność maszyny Wirtualnej. Wysoka obciążeń We/Wy i najwyższą wydajność, które używają dysków SSD, można użyć magazynu w warstwie standardowa, używającym dysków regularne Obracająca lub magazyn w warstwie Premium. Jako z hello rozmiar maszyny Wirtualnej są kosztów zagadnienia tooselecting hello nośniku. Możesz przeczytać hello [artykułu wskazówki dotyczące infrastruktury magazynu](infrastructure-storage-solutions-guidelines.md) toounderstand jak toodesign odpowiednie magazynu dla uzyskania optymalnej wydajności maszyn wirtualnych.

## <a name="resource-groups"></a>Grupy zasobów
Składniki, takie jak maszyny wirtualne są logicznie pogrupowane w celu ułatwienia zarządzania i obsługi przy użyciu [grup zasobów platformy Azure](../../azure-resource-manager/resource-group-overview.md). Za pomocą grup zasobów, można utworzyć, zarządzanie i monitorowanie wszystkich zasobów hello wchodzące w skład danej aplikacji. Można też wdrożyć [kontroli dostępu opartej na rolach](../../active-directory/role-based-access-control-what-is.md) toogrant tooothers dostępu w ramach wymagają zasobów hello tooonly zespołu. Zająć tooplan czasu limit grup zasobów i przypisań ról. Istnieją różne podejścia tooactually projektowania i wdrażania grup zasobów, dlatego należy się tooread hello [artykułu wytyczne grup zasobów](infrastructure-resource-groups-guidelines.md) toounderstand najlepszego toobuild limit maszyn wirtualnych.

## <a name="templates"></a>Szablony
Można tworzyć szablony, zdefiniowane przez deklaratywne pliki w formacie JSON, toocreate maszyn wirtualnych. Szablony zwykle również kompilacji hello wymagane magazynu, sieci, interfejsów sieciowych, adresów IP, itp. oraz hello maszyn wirtualnych, same. Dla rozwoju i tooeasily do celów testowych są replikowane w środowiskach produkcyjnych, można użyć szablonów toocreate spójne odtworzenia środowiskach i na odwrót. Możesz przeczytać dodatkowe informacje [tworzenia szablonów i korzystanie z](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand jak ich używać do tworzenia i wdrażania maszyn wirtualnych.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

