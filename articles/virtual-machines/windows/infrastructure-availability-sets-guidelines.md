---
title: Ustawia aaaAvailability dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania zestawów dostępności w usługach infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc35fd1e913434d9facb94116edb1b1c30447c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>Dostępność Azure ustawia wskazówki dla maszyn wirtualnych systemu Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Ten artykuł skupia się na powitania opis wymaganych czynności związane z planowaniem dla zestawy dostępności tooensure aplikacji, pozostaje dostępne podczas planowanego lub nieplanowanego zdarzenia.

## <a name="implementation-guidelines-for-availability-sets"></a>Implementacja — wskazówki zestawów dostępności
Decyzje:

* Jak wiele zestawów dostępności potrzebujesz w hello różnych ról i warstw w infrastrukturze aplikacji?

Zadania:

* Zdefiniuj hello liczbę maszyn wirtualnych w poszczególnych warstwach aplikacji, które są wymagane.
* Stwierdzić, czy wymagane tooadjust hello liczbę błędów lub aktualizacji toobe domen używane dla aplikacji.
* Zdefiniuj hello wymagane zestawy dostępności przy użyciu konwencji nazewnictwa i co maszyny wirtualne znajdują się w nich. Maszyna wirtualna tylko może znajdować się w zestawie dostępności.

## <a name="availability-sets"></a>Zestawy dostępności
Na platformie Azure maszynach wirtualnych (VM) można umieścić w logiczne grupowanie tooa o nazwie zestawu dostępności. Po utworzeniu maszyn wirtualnych w zbiorze dostępności hello platformy Azure rozdziela umieszczania hello tych maszyn wirtualnych między hello podstawowej infrastruktury. Powinno być toohello zdarzeń planowanych konserwacji platformy Azure lub używany sprzęt / infrastruktury błędów, użyj hello zestawów dostępności zapewnia, że co najmniej jedna maszyna wirtualna jest uruchomiona.

Najlepszym rozwiązaniem aplikacje nie powinien znajdować się na jednej maszynie Wirtualnej. Zestaw dostępności zawierający jednej maszyny Wirtualnej nie uzyskują żadnej ochrony przed planowanego lub nieplanowanego zdarzenia w hello platformy Azure. Witaj [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) wymaga co najmniej dwóch maszyn wirtualnych w ramach dostępność zestawu tooallow hello dystrybucji maszyn wirtualnych na powitania podstawowej infrastruktury. Jeśli używasz [Azure Premium Storage](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello umowy SLA platformy Azure stosuje tooa pojedynczy maszyny Wirtualnej.

Witaj podstawowej infrastruktury na platformie Azure jest podzielony na toomultiple sprzętu klastrów. Każdy klaster sprzętu może obsługiwać rozmiary zakres maszyny Wirtualnej. Zestaw dostępności może być hostowana w klastrze pojedynczego sprzętu w dowolnym momencie w czasie. W związku z tym hello rozmiary zakres maszyny Wirtualnej, które może istnieć w zestawie dostępności pojedynczego jest toohello ograniczony zakres maszyny Wirtualnej rozmiary obsługiwane przez hello sprzętu klastra. Hello sprzętu klastra dla zestawu dostępności hello jest wybrany, gdy hello pierwszym wdrożeniu maszyny Wirtualnej w zestawie dostępności hello lub uruchamianie hello pierwsza maszyna wirtualna w zestawie dostępności, gdzie wszystkie maszyny wirtualne są obecnie w stanie zatrzymana alokację hello. Hello następującego polecenia programu PowerShell może być toodetermine używane hello zakres maszyny Wirtualnej rozmiarów dostępnych dla zestawu dostępności: "Get-AzureRmVMSize - ResourceGroupName \<ciąg\> - AvailabilitySetName \<ciąg\> "

Każdy klaster sprzętu jest podzielony na domeny aktualizacji toomultiple i domen błędów. Te domeny są definiowane przez hosty z jakiego Udostępnianie wspólnych cyklu aktualizacji lub udziału podobne fizycznej infrastruktury, takich jak power i sieci. Azure automatycznie dystrybuuje maszyn wirtualnych w zestawie między domenami toomaintain dostępności i odporności na uszkodzenia dostępności. W zależności od rozmiaru hello aplikacji i hello liczbę maszyn wirtualnych w zestawie dostępności, można dostosować hello liczby domen mają toouse. Możesz przeczytać dodatkowe informacje [zarządzania, dostępność i stosowania aktualizacji i odporność domen](manage-availability.md).

Podczas projektowania infrastruktury aplikacji, należy zaplanować hello warstwy aplikacji, których używasz. Grupy maszyn wirtualnych, które pełnią hello sam cel w zestawach tooavailability, takich jak zbiór dostępności dla maszyn wirtualnych frontonu usług IIS. Utwórz oddzielne zbiór dostępności dla maszyn wirtualnych zaplecza uruchomiony program SQL Server. Celem Hello jest tooensure każdego składnika aplikacji jest chroniony przez zestaw dostępności, a co najmniej raz wystąpienia zawsze pozostaje uruchomiona.

Moduły równoważenia obciążenia mogą zostać użyte przed każdym toowork warstwy aplikacji obok zestawu dostępności i upewnij się, że ruch zawsze może być kierowany tooa uruchomione wystąpienie. Bez modułu równoważenia obciążenia maszyny wirtualne mogą nadal działać w całej zdarzeń planowanych lub nieplanowanych konserwacji, ale użytkownikowi końcowemu może nie być tooresolve mogli je, jeśli hello podstawowej maszyny Wirtualnej jest niedostępne.

Utwórz projekt swojej aplikacji w celu zapewnienia wysokiej dostępności w warstwie magazynu. Witaj najlepszym rozwiązaniem jest zbyt[dysków zarządzanych maszyn wirtualnych w zestawie dostępności](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Jeśli obecnie używasz niezarządzane dysków, zdecydowanie zalecamy zbyt[przekonwertować maszyny wirtualne w zestawie dostępności dysków zarządzanych toouse](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
