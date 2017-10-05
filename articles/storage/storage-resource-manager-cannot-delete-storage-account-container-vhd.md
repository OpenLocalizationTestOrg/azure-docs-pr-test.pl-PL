---
title: "Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde

Może pojawić się błędy podczas próby usunięcia konta magazynu platformy Azure, kontenera lub wirtualnego dysku twardego (VHD) w [portalu Azure](https://portal.azure.com). Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów w celu rozwiązania problemu z wdrożenia usługi Azure Resource Manager.

Jeśli w tym artykule nie rozwiązania Azure problemu, odwiedź fora Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Możesz zamieścić problemu na tych fora lub do @AzureSupport w serwisie Twitter. Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptoms"></a>Objawy
### <a name="scenario-1"></a>Scenariusz 1
Podczas próby usunięcia dysku VHD na koncie magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:

**Nie można usunąć obiektu blob "vhds/BlobName.vhd". Błąd: Jest obecnie dzierżawy w obiekcie blob i identyfikator dzierżawy nie został określony w żądaniu.**

Ten problem może wystąpić, ponieważ maszyna wirtualna (VM) ma dzierżawę na wirtualny dysk twardy, który próbujesz usunąć.

### <a name="scenario-2"></a>Scenariusz 2
Podczas próby usunięcia kontenera na koncie magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:

**Nie można usunąć kontenera magazynu "VHD". Błąd: Jest obecnie dzierżawy w kontenerze i identyfikator dzierżawy nie został określony w żądaniu.**

Ten problem może wystąpić, ponieważ kontener wirtualnego dysku twardego, który jest zablokowany w stanie dzierżawy.

### <a name="scenario-3"></a>Scenariusz 3
Podczas usuwania konta magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:

**Nie można usunąć konta magazynu "StorageAccountName". Błąd: Nie można usunąć konta magazynu z powodu jego artefakty są nadal używane.**

Ten problem może wystąpić, ponieważ konto magazynu zawiera wirtualny dysk twardy jest w stanie dzierżawy.

## <a name="solution"></a>Rozwiązanie 
Aby rozwiązać te problemy, należy określić wirtualnego dysku twardego, który jest przyczyną błędu i skojarzonego VM. Następnie odłącz wirtualny dysk twardy z maszyny Wirtualnej (w przypadku dysków z danymi) lub Usuń maszynę Wirtualną, która korzysta z wirtualnego dysku twardego (dysków systemu operacyjnego). To spowoduje usunięcie dzierżawy z wirtualnego dysku twardego i umożliwia jego do usunięcia. 

Aby to zrobić, użyj jednej z następujących metod:

### <a name="method-1---use-azure-storage-explorer"></a>Metoda 1 - użyj Eksploratora magazynu Azure

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>Krok 1 zidentyfikować wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu

1. Podczas usuwania konta magazynu, zostanie wyświetlony komunikat okno dialogowe podobne do poniższych: 

    ![komunikat podczas usuwania konta magazynu](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Sprawdź **adres URL dysku** do identyfikowania magazynu konto i wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu. W poniższym przykładzie ciąg przed ". blob.core.windows.net" jest nazwa konta magazynu, a Nazwa wirtualnego dysku twardego jest "SCCM2012-2015-08-28.vhd".  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a>Krok 2 usunąć wirtualny dysk twardy za pomocą Eksploratora usługi Storage platformy Azure

1. Pobierz i zainstaluj najnowszą wersję [Eksploratora usługi Storage Azure](http://storageexplorer.com/). To narzędzie jest aplikacją autonomiczną firmy Microsoft, która pozwala łatwo pracować z danymi usługi Azure Storage w systemie Windows, system macOS i Linux.
2. Otwórz Eksploratora usługi Storage platformy Azure, wybierz opcję ![Ikona konta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) na pasku po lewej stronie wybierz środowisku platformy Azure, a następnie zaloguj się.

3. Wybierz wszystkie subskrypcje lub subskrypcji, która zawiera konta magazynu, który chcesz usunąć.

    ![Dodaj subskrypcję](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Przejdź do uzyskiwanej w adresie URL dysku wcześniej, wybierz konto magazynu **kontenerów obiektów Blob** > **wirtualne dyski twarde** i wyszukaj wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu.
5. Jeśli zostanie znaleziony wirtualny dysk twardy, sprawdź **nazwę maszyny Wirtualnej** kolumny można znaleźć maszyny Wirtualnej, który używa tego wirtualnego dysku twardego.

    ![Sprawdź maszyny wirtualnej](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Usuń dzierżawy z dysku VHD za pomocą portalu Azure. Aby uzyskać więcej informacji, zobacz [Usuń dzierżawy z wirtualnego dysku twardego](#remove-the-lease-from-the-vhd). 

7. Przejdź do Eksploratora magazynu Azure, kliknij prawym przyciskiem myszy dysk VHD, a następnie wybierz delete.

8. Usuwa konto magazynu.

### <a name="method-2---use-azure-portal"></a>Metoda 2 - użyj portalu Azure 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>: Krok 1 wirtualny dysk twardy, który uniemożliwia usunięcie konta magazynu

1. Podczas usuwania konta magazynu, zostanie wyświetlony komunikat okno dialogowe podobne do poniższych: 

    ![komunikat podczas usuwania konta magazynu](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Sprawdź **adres URL dysku** do identyfikowania magazynu konto i wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu. W poniższym przykładzie ciąg przed ". blob.core.windows.net" jest nazwa konta magazynu, a Nazwa wirtualnego dysku twardego jest "SCCM2012-2015-08-28.vhd".  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
3. W menu Centrum wybierz **wszystkie zasoby**. Przejdź do konta magazynu, a następnie wybierz **obiekty BLOB** > **wirtualne dyski twarde**.

    ![Zrzut ekranu przedstawiający portal, konto magazynu i kontener "VHD" wyróżnione](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Odszukaj wirtualny dysk twardy, który mamy uzyskany z adresu URL dysku wcześniej. Następnie określ, którego używa wirtualna wirtualnego dysku twardego. Zazwyczaj można określić, której maszyna wirtualna znajduje się wirtualny dysk twardy sprawdzana jest nazwa wirtualnego dysku twardego:

Maszyna wirtualna w modelu programowania usługi Resource Manager

   * Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd
   * Dyski danych należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd

Maszynę Wirtualną w klasycznym modelu programowania

   * Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Dyski danych należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-the-lease-from-the-vhd"></a>Krok 2: Usuń dzierżawy z wirtualnego dysku twardego

[Usuń dzierżawy z wirtualnego dysku twardego](#remove-the-lease-from-the-vhd), a następnie usunąć konto magazynu.

## <a name="what-is-a-lease"></a>Co to jest dzierżawa?
Dzierżawa jest blokady, który może służyć do kontrolowania dostępu do obiektów blob (na przykład dysk VHD). Gdy obiektu blob jest dzierżawiony, właściciele dzierżawy może uzyskać dostęp do obiektu blob. Dzierżawa jest ważne z następujących powodów:

* Zapobiega uszkodzenie danych, jeśli wiele właścicieli spróbuj zapisać tę samą część obiektu blob w tym samym czasie.
* Obiekt blob uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).
* Konto magazynu uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).

### <a name="remove-the-lease-from-the-vhd"></a>Usuń dzierżawy z wirtualnego dysku twardego
Jeśli wirtualny dysk twardy, dysk systemu operacyjnego, należy usunąć maszynę Wirtualną, aby usunąć dzierżawy:

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Na **Centrum** menu, wybierz opcję **maszyn wirtualnych**.
3. Wybierz maszynę Wirtualną, która przechowuje dzierżawę na dysku VHD.
4. Upewnij się, że nic nie jest aktywnie przy użyciu maszyny wirtualnej i nie są już potrzebne maszyny wirtualnej.
5. W górnej części **szczegóły maszyny Wirtualnej** bloku, wybierz opcję **usunąć**, a następnie kliknij przycisk **tak** o potwierdzenie.
6. Maszyna wirtualna powinien zostać usunięty, ale wirtualnego dysku twardego mogą być przechowywane. Jednak dysku VHD nie powinni mieć dzierżawę na nim. Może upłynąć kilka minut, aż dzierżawa do zwolnienia. Aby zweryfikować, że zwolnieniu dzierżawy, przejdź do **wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >   **wirtualne dyski twarde**. W **właściwości obiektu Blob** okienku **stanu dzierżawy** wartość powinna być **odblokowany**.

Jeśli wirtualny dysk twardy jest dysk z danymi, odłącz wirtualny dysk twardy z maszyny Wirtualnej, aby usunąć dzierżawy:

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Na **Centrum** menu, wybierz opcję **maszyn wirtualnych**.
3. Wybierz maszynę Wirtualną, która przechowuje dzierżawę na dysku VHD.
4. Wybierz **dysków** na **szczegóły maszyny Wirtualnej** bloku.
5. Wybierz dysk danych, który przechowuje dzierżawę na dysku VHD. Można określić, który wirtualny dysk twardy jest podłączony w dysku, sprawdzając adres URL dysku VHD.
6. Określ, z pewnością, że nic nie jest aktywnie przy użyciu dysku danych.
7. Kliknij przycisk **Detach** na **dysku szczegóły** bloku.
8. Dysk powinien teraz można odłączyć od maszyny Wirtualnej, i wirtualnego dysku twardego nie może mieć dzierżawę na nim. Może upłynąć kilka minut, aż dzierżawa do zwolnienia. Aby zweryfikować zwolnienie dzierżawy, przejdź do **wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >  **wirtualne dyski twarde**. W **właściwości obiektu Blob** okienku **stanu dzierżawy** wartość powinna być **odblokowany**.

## <a name="next-steps"></a>Następne kroki
* [Usunięcie konta magazynu](storage-create-storage-account.md#delete-a-storage-account)
* [Sposób podziału zablokowanym dzierżawy magazynu obiektów blob na platformie Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
