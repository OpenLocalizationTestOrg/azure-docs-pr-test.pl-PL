---
title: "Upewnij się, hello dysku D: dysku danych maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toochange litery dysków dla maszyny Wirtualnej systemu Windows tak, aby można było używać dysków D: hello jako dysk danych."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Użyj dysku D: hello jako dysk z danymi na maszynie Wirtualnej systemu Windows
Jeśli aplikacja wymaga hello toouse danych toostore dysku D, wykonaj te instrukcje toouse inną literę dysku tymczasowym hello. Nigdy nie używaj danych toostore dysku tymczasowym hello konieczność tookeep.

Jeśli po zmianie rozmiaru lub **Stop (Deallocate)** maszyny wirtualnej, może to wywołać umieszczania nowej funkcji hypervisor hello maszyn wirtualnych tooa. Planowanego lub nieplanowanego zdarzenia konserwacji może być również przyczyną tego rozmieszczenia. W tym scenariuszu dysku tymczasowym hello będzie przypisywać ich toohello pierwszą dostępną literę dysku. Jeśli masz aplikację, która wymaga specjalnie hello D: dysku, należy toofollow, te kroki tootemporarily przenoszenia hello pagefile.sys dołączyć nowego dysku danych i przypisać jej literę hello D, a następnie przenieś hello pagefile.sys kopii toohello tymczasowej stacji. Po wykonaniu tych czynności Azure nie wycofania hello D: Jeśli hello maszyna wirtualna zostanie przeniesiona tooa innej funkcji hypervisor.

Aby uzyskać więcej informacji o używaniu dysku tymczasowym hello Azure, zobacz [opis hello tymczasowej stacji na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Dołączenie dysku danych hello
Najpierw należy maszyny wirtualnej toohello tooattach hello dane dysku. toodo to przy użyciu portalu hello, zobacz [jak tooattach zarządzanych danych na dysku w portalu Azure hello](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Tymczasowo przenieść pagefile.sys tooC dysku
1. Połącz toohello maszyny wirtualnej. 
2. Kliknij prawym przyciskiem myszy hello **Start** menu i wybierz **systemu**.
3. W menu po lewej stronie powitania, wybierz **Zaawansowane ustawienia systemu**.
4. W hello **wydajności** zaznacz **ustawienia**.
5. Wybierz hello **zaawansowane** kartę.
6. W hello **pamięci wirtualnej** zaznacz **zmiany**.
7. Wybierz hello **C** dysk, a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.
8. Wybierz hello **D** dysk, a następnie kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.
9. Kliknij przycisk Zastosuj. Zostanie wyświetlone ostrzeżenie komputera hello musi toobe hello zmiany tootake mają wpływ na ponowne uruchomienie.
10. Uruchom ponownie maszynę wirtualną hello.

## <a name="change-hello-drive-letters"></a>Zmień litery dysków hello
1. Raz hello ponownego uruchomienia maszyny Wirtualnej, zaloguj się ponownie toohello maszyny Wirtualnej.
2. Kliknij przycisk hello **Start** menu i typ **diskmgmt.msc** i naciśnij Enter. Rozpocznie się Zarządzanie dyskami.
3. Kliknij prawym przyciskiem myszy **D**hello magazyn tymczasowy dysku i wybierz **Zmień literę dysku i ścieżki**.
4. W obszarze literę dysku, wybierz inny dysk takich jak **T** , a następnie kliknij przycisk **OK**. 
5. Kliknij prawym przyciskiem myszy na powitania dysku danych, a następnie wybierz **Zmień literę dysku i ścieżki**.
6. W obszarze literę dysku, należy wybrać dysk **D** , a następnie kliknij przycisk **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Przenieś pagefile.sys wstecz toohello magazyn tymczasowy dysku
1. Kliknij prawym przyciskiem myszy hello **Start** menu i wybierz **systemu**
2. W menu po lewej stronie powitania, wybierz **Zaawansowane ustawienia systemu**.
3. W hello **wydajności** zaznacz **ustawienia**.
4. Wybierz hello **zaawansowane** kartę.
5. W hello **pamięci wirtualnej** zaznacz **zmiany**.
6. Wybierz dysk systemu operacyjnego hello **C** i kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.
7. Wybierz dysk magazyn tymczasowy hello **T** , a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.
8. Kliknij przycisk **Zastosuj**. Zostanie wyświetlone ostrzeżenie komputera hello musi toobe hello zmiany tootake mają wpływ na ponowne uruchomienie.
9. Uruchom ponownie maszynę wirtualną hello.

## <a name="next-steps"></a>Następne kroki
* Można zwiększyć maszyny wirtualnej dostępne tooyour hello magazynu za pomocą [dołączenie dysku danych dodatkowych](attach-managed-disk-portal.md).

