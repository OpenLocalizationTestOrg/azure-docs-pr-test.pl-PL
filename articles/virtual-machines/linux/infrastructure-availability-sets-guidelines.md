---
title: "Zestawy dostępności dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące wdrażania zestawów dostępności w usługach infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5fad478a8fbbdeef2fe72f0b8f2ebe32852bbc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Zestawy Azure dostępności dla maszyn wirtualnych systemu Linux — wskazówki

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na kroki planowania wymagane dla zestawów dostępności upewnić się, Twoje aplikacje pozostaje dostępna podczas planowanego lub nieplanowanego zdarzenia.

## <a name="implementation-guidelines-for-availability-sets"></a>Implementacja — wskazówki zestawów dostępności
Decyzje:

* Jak wiele zestawów dostępności potrzebujesz dla różnych ról i warstw w infrastrukturze aplikacji?

Zadania:

* Zdefiniuj liczbę maszyn wirtualnych w poszczególnych warstwach aplikacji, które są wymagane.
* Określ, czy należy Dostosuj liczbę błędów lub zaktualizuj domeny do użycia dla aplikacji.
* Definiowanie zestawów dostępności wymagane przy użyciu konwencji nazewnictwa i co maszyny wirtualne znajdują się w nich. Maszyna wirtualna tylko może znajdować się w zestawie dostępności. 

## <a name="availability-sets"></a>Zestawy dostępności
Na platformie Azure maszynach wirtualnych (VM) można umieścić w na grupę logiczną o nazwie zestawu dostępności. Po utworzeniu maszyn wirtualnych w zbiorze dostępności platformy Azure dystrybuuje rozmieszczenie tych maszyn wirtualnych w ramach podstawowej infrastruktury. Powinno być zdarzeniem zaplanowanej konserwacji do platformy Azure lub używany sprzęt / odporność infrastruktury, korzystanie z zestawów dostępności zapewnia, że co najmniej jedna maszyna wirtualna jest uruchomiona.

Najlepszym rozwiązaniem aplikacje nie powinien znajdować się na jednej maszynie Wirtualnej. Zestaw dostępności zawierający jednej maszyny Wirtualnej nie uzyskują żadnej ochrony przed planowanego lub nieplanowanego zdarzenia w ramach platformy Azure. [Umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) wymaga co najmniej dwóch maszyn wirtualnych w ramach zestawu umożliwiają dystrybucję maszyn wirtualnych w infrastrukturze podstawowej dostępności. Jeśli używasz [Azure Premium Storage](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), umowy SLA platformy Azure ma zastosowanie do jednej maszyny Wirtualnej.

Podstawowej infrastruktury na platformie Azure jest podzielony na wiele klastrów sprzętu. Każdy klaster sprzętu może obsługiwać rozmiary zakres maszyny Wirtualnej. Zestaw dostępności może być hostowana w klastrze pojedynczego sprzętu w dowolnym momencie w czasie. W związku z tym rozmiarów zakresu z maszyn wirtualnych, które może istnieć w zestawie dostępności pojedynczego jest ograniczona do rozmiarów zakres maszyny Wirtualnej obsługuje sprzętu klastra. Klaster sprzętu dla zestawu dostępności jest zaznaczona, po wdrożeniu pierwszej maszyny Wirtualnej w zestawie dostępności lub podczas uruchamiania pierwsza maszyna wirtualna w zestawie dostępności, którym wszystkich maszyn wirtualnych są obecnie w stanie zatrzymana alokację. Następujące polecenia interfejsu wiersza polecenia może służyć do określenia zestawu dostępności dostępnych rozmiarów zakres maszyny Wirtualnej: "az rozmiarów maszyn wirtualnych listy---lokalizacji \<ciąg\>"

Każdy klaster sprzętu jest podzielony na wiele domen aktualizacji i domen błędów. Te domeny są definiowane przez hosty z jakiego Udostępnianie wspólnych cyklu aktualizacji lub udziału podobne fizycznej infrastruktury, takich jak power i sieci. Azure automatycznie dystrybuuje maszyn wirtualnych w ramach zestawu między domenami, aby zachować dostępność i odporność na uszkodzenia dostępności. W zależności od rozmiaru aplikacji, a liczba maszyn wirtualnych w zestawie dostępności można dostosować liczby domen, którego chcesz użyć. Możesz przeczytać dodatkowe informacje [zarządzania, dostępność i stosowania aktualizacji i odporność domen](manage-availability.md).

Podczas projektowania infrastruktury aplikacji należy zaplanować warstwy aplikacji do użycia. Ustawia grupy maszyn wirtualnych, które służą tych samych celów w dostępności, takich jak zbiór dostępności dla maszyn wirtualnych frontonu systemem nginx lub Apache. Utwórz oddzielne zbiór dostępności dla maszyn wirtualnych zaplecza uruchomiony bazy danych MongoDB lub MySQL. Celem jest zapewnienie każdego składnika aplikacji jest chroniony przez zestaw dostępności i co najmniej raz wystąpienia zawsze pozostaje uruchomiona.

Na początku każdej warstwy aplikacji do pracy obok zestawu dostępności i upewnij się, że ruch zawsze mogą być kierowane do uruchomionego wystąpienia mogą zostać użyte usługi równoważenia obciążenia. Bez modułu równoważenia obciążenia maszyny wirtualne mogą nadal działać w całej zdarzeń planowanych lub nieplanowanych konserwacji, ale użytkownikowi końcowemu może nie móc rozwiązać je, jeśli podstawowej maszyny Wirtualnej jest niedostępny.

Utwórz projekt swojej aplikacji w celu zapewnienia wysokiej dostępności w warstwie magazynu. Najlepszym rozwiązaniem jest [dysków zarządzanych maszyn wirtualnych w zestawie dostępności](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Jeśli obecnie używasz niezarządzane dysków, zdecydowanie zaleca się [przekonwertować maszyny wirtualne w zestawie dostępności do zarządzanych dysków](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

