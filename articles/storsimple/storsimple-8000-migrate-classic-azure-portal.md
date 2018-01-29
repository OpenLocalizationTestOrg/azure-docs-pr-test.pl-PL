---
title: "Migrowanie kont magazynu, subskrypcji dla usługi Menedżer StorSimple urządzenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przeprowadzić migrację subskrypcji, konta magazynu dla Twojego service8000 Menedżera urządzeń StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/26/2017
ms.author: alkohli
ms.openlocfilehash: edac2635086106f83b30316ab190bead5245f195
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="migrate-subscriptions-and-storage-accounts-associated-with-storsimple-device-manager-service"></a>Migrowanie subskrypcji i kont magazynu skojarzonych z usługą Menedżera urządzeń StorSimple

Konieczne może być Przesuń usługi StorSimple rejestrowania nowych lub nową subskrypcję. Scenariusze migracji są albo zmian konta lub centrum danych. Skorzystaj z poniższej tabeli, aby zrozumieć, która z tych scenariuszy są obsługiwane m.in. szczegółowy opis kroków, aby przenieść.

## <a name="account-changes"></a>Zmiany konta

| Można przeniesiesz...| Obsługiwane| Czas przestoju| Proces pomocy technicznej platformy Azure| Podejście|
|-----|-----|-----|-----|-----|
| Całej subskrypcji (w tym StorSimple konta usługi i magazyn) do innej rejestracji? | Tak       | Nie       | **Transfer rejestracji**<br>Za pomocą:<li>Podczas zakupu nowego zobowiązania Azure w obszarze nowej umowy.</li><li>Użytkownik chce migrować wszystkie konta i subskrypcji z rejestracji starego do nowego. Dotyczy to również wszystkich usług platformy Azure w ramach starego subskrypcji.</li> | **Krok 1: Otwórz bilet pomocy technicznej operacji Enterprise Azure.**<li>Przejdź do [http://aka.ms/AzureEnt](http://aka.ms/AzureEnt).</li><li> Wybierz **administracji rejestracji** , a następnie wybierz **transferu z jednego rejestracji do nowej rejestracji**.<br>**Krok 2: Podaj wymagane informacje**<br>Obejmują:<li>numer rejestracji źródła</li><li> numer rejestracji docelowego</li><li>Data wprowadzenia transferu|
| Usługi StorSimple z istniejącego konta do nowej rejestracji?    | Tak       | Nie       | **Transfer konta**<br>Za pomocą:<li>Jeśli nie chcesz transferu pełnej rejestracji.</li><li>Chcesz przenieść określonych kont do nowej rejestracji.</li>| **Krok 1: Otwórz bilet pomocy technicznej operacji Enterprise Azure.**<li>Przejdź do [http://aka.ms/AzureEnt](http://aka.ms/AzureEnt).</li><li>Wybierz **administracji rejestracji** , a następnie wybierz **transferu konta EA nowej rejestracji**.<br>**Krok 2: Podaj wymagane informacje**<br>Obejmują:<li>numer rejestracji źródła</li><li> numer rejestracji docelowego</li><li>Data wprowadzenia transferu|
| Usługi StorSimple z jedną subskrypcję do innej subskrypcji?      | Nie        |    Tak         | Żaden proces ręczny|<li>Przeprowadź migrację danych poza urządzenia StorSimple.</li><li>Wykonaj resetowania do ustawień fabrycznych urządzenia, to usuwa wszystkie dane lokalne na urządzeniu.</li><li>Rejestrowanie urządzenia z nową subskrypcję usługi Menedżer StorSimple urządzenia.</li><li>Migrację danych do urządzenia.|
| Urządzenia StorSimple z jedną usługę Menedżer StorSimple urządzenia do innej usługi w innym regionie?      | Nie        | Tak            | Żaden proces ręczny |Taka sama jak powyżej.|
| Konto magazynu do nowej grupy zasobów lub subskrypcji?     | Tak        | Nie             |Przenieś konta magazynu do innej subskrypcji lub grupy zasobów |Po przeniesieniu Jeśli klucze dostępu do konta magazynu są aktualizowane, użytkownik należy skonfigurować klucze dostępu ręcznie dla konta magazynu zmigrowane za pośrednictwem usługi Menedżer StorSimple urządzenia.|
| Konto klasycznego magazynu do konta magazynu usługi Azure Resource Manager      | Tak        | Nie             |Migracja z klasycznego do usługi Azure Resource Manager |<li>Aby uzyskać szczegółowe instrukcje dotyczące sposobu przeprowadzenia migracji konta magazynu ze środowiska klasycznego do usługi Azure Resource Manager, przejdź do [migracji konta magazynu classic](../virtual-machines/windows/migration-classic-resource-manager-ps.md#step-62-migrate-a-storage-account).</li><li> Jeśli klucze dostępu do konta magazynu są aktualizowane po migracji, użytkownik musi zsynchronizować klucze dostępu dla konta magazynu zmigrowane za pośrednictwem usługi Menedżer StorSimple urządzenia. To jest zapewnienie urządzenia StorSimple w dalszym ciągu działać normalnie i są w stanie warstwy podstawowej lub tworzenia kopii zapasowej danych na platformie Azure. Aby uzyskać szczegółowe informacje dotyczące synchronizacji klucze dostępu, [przepływu pracy obrotu](storsimple-8000-manage-storage-accounts.md#key-rotation-of-storage-accounts).</li><li> W przypadku urządzenia z chmury StorSimple Jeśli konto klasycznego magazynu migracji, ale podstawowej maszyny wirtualnej nadal pozostaje w klasycznym, urządzenia powinny działać prawidłowo. Jeśli dla urządzenia chmury podstawowej maszyny wirtualnej jest migrowana, Dezaktywuj i usuń funkcje nie będzie działać.</li><li> Należy utworzyć nowe urządzenia StorSimple w chmurze w portalu Azure i następnie przełączyć się z starszych urządzeń chmury. Nie można utworzyć urządzenia chmury StorSimple w nowego przy użyciu konta magazynu w klasycznym portalu Azure, muszą mieć konta magazynu usługi Azure Resource Manager. Aby uzyskać więcej informacji, przejdź do [wdrażanie i zarządzanie nimi urządzenia chmury StorSimple](storsimple-8000-cloud-appliance-u2.md).</li>|Taka sama jak powyżej.|

## <a name="datacenter-changes"></a>Zmiany w centrum danych

| Można przeniesiesz...| Obsługiwane|Czas przestoju| Proces pomocy technicznej platformy Azure| Podejście|
|-----|-----|-----|-----|-----|
| Usługi StorSimple z jednego centrum danych Azure do innego? | Nie | Tak |Żaden proces ręczny  |<li>Przeprowadź migrację danych poza urządzenia StorSimple.</li><li>Wykonaj resetowania do ustawień fabrycznych urządzenia, to usuwa wszystkie dane lokalne na urządzeniu.</li><li>Rejestrowanie urządzenia z nową subskrypcję do nowej usługi Menedżer StorSimple urządzenia.</li><li>Migrację danych do urządzenia.|
| Konto magazynu z jednego centrum danych Azure do innego? | Nie |Tak  |Żaden proces ręczny  | Taka sama jak powyżej.|

## <a name="next-steps"></a>Następne kroki

* [Wdrażanie usługi Menedżer StorSimple urządzenia](storsimple-8000-manage-service.md)
* [Wdrażanie urządzenia z serii StorSimple 8000 w portalu Azure](storsimple-8000-deployment-walkthrough-u2.md)
