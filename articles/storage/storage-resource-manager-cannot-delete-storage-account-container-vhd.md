---
title: "błędy aaaTroubleshoot podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde

Może pojawić się błędy podczas próby toodelete kontem magazynu platformy Azure, kontenera lub wirtualnego dysku twardego (VHD) w hello [portalu Azure](https://portal.azure.com). Ten artykuł zawiera Rozwiązywanie problemów z wskazówki toohelp resolve hello problem we wdrożeniu usługi Azure Resource Manager.

Jeśli w tym artykule nie rozwiązania Azure problemu, odwiedź stronę hello forach platformy Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Problem można umieścić na tych fora lub too@AzureSupport w serwisie Twitter. Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na powitania [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptoms"></a>Objawy
### <a name="scenario-1"></a>Scenariusz 1
Podczas próby toodelete dysku VHD na koncie magazynu w ramach wdrożenia usługi Resource Manager pojawi się następujący komunikat o błędzie hello:

**Obiekt blob toodelete "vhds/BlobName.vhd" nie powiodło się. Błąd: Jest obecnie dzierżawę na powitania obiektów blob i identyfikator dzierżawy nie został określony w żądaniu hello.**

Ten problem może wystąpić, ponieważ maszyna wirtualna (VM) ma dzierżawę na powitania próbujesz toodelete wirtualnego dysku twardego.

### <a name="scenario-2"></a>Scenariusz 2
Podczas próby toodelete kontenera na koncie magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie hello:

**Nie można toodelete kontenera magazynu "VHD". Błąd: Jest obecnie dzierżawę na powitania kontenera i identyfikator dzierżawy nie został określony w żądaniu hello.**

Ten problem może wystąpić, ponieważ kontener hello ma wirtualnego dysku twardego, który jest zablokowany w stanie dzierżawy hello.

### <a name="scenario-3"></a>Scenariusz 3
Podczas próby toodelete konto magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie hello:

**Konto magazynu toodelete "StorageAccountName" nie powiodło się. Błąd: nie można usunąć konta magazynu hello powodu tooits artefakty są nadal używane.**

Ten problem może wystąpić, ponieważ konto magazynu hello zawiera wirtualny dysk twardy jest w stanie dzierżawy hello.

## <a name="solution"></a>Rozwiązanie 
tooresolve tych problemów, należy wskazać hello wirtualnego dysku twardego, który powoduje błąd hello i hello skojarzonego VM. Następnie odłącz hello wirtualnego dysku twardego z hello maszyny Wirtualnej (w przypadku dysków z danymi) lub usunąć hello maszynę Wirtualną, która używa hello wirtualnego dysku twardego (w przypadku dysków systemu operacyjnego). Usuwa dzierżawy hello hello wirtualnego dysku twardego i umożliwia jego toobe usunięte. 

toodo tego, użyj jednej z następujących metod hello:

### <a name="method-1---use-azure-storage-explorer"></a>Metoda 1 - użyj Eksploratora magazynu Azure

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Krok 1 Określ hello wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu hello

1. Podczas usuwania konta magazynu hello pojawi się okno dialogowe wiadomości, takie jak następujące hello: 

    ![Podczas usuwania konta magazynu hello komunikat o błędzie](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Sprawdź hello **adres URL dysku** konto magazynu hello tooidentify i hello wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu hello. W hello poniższy przykład, hello ciągu przed ". blob.core.windows.net" jest nazwa konta magazynu hello, a "SCCM2012-2015-08-28.vhd" hello, Nazwa wirtualnego dysku twardego.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Krok 2 Delete hello wirtualnego dysku twardego za pomocą Eksploratora usługi Storage platformy Azure

1. Pobierz i zainstaluj hello najnowszej wersji [Eksploratora usługi Storage Azure](http://storageexplorer.com/). To narzędzie jest aplikacją autonomiczną firmy Microsoft, który pozwala tooeasily pracy z danymi usługi Azure Storage w systemie Windows, system macOS i Linux.
2. Otwórz Eksploratora usługi Storage platformy Azure, wybierz opcję ![Ikona konta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) na pasku po lewej stronie powitania wybierz środowisku platformy Azure, a następnie zaloguj się.

3. Wybierz wszystkie subskrypcje lub hello subskrypcji, która zawiera hello konta magazynu, które chcesz toodelete.

    ![Dodaj subskrypcję](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Przejdź do konta magazynu toohello uzyskiwanej z hello dysku adres URL wcześniej, wybierz pozycję hello **kontenerów obiektów Blob** > **wirtualne dyski twarde** i wyszukaj hello wirtualnego dysku twardego, który uniemożliwia konta magazynu hello delete.
5. Jeśli zostanie znaleziony hello wirtualny dysk twardy, sprawdź hello **nazwę maszyny Wirtualnej** kolumny toofind hello maszynę Wirtualną, która używa tego wirtualnego dysku twardego.

    ![Sprawdź maszyny wirtualnej](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Usuwanie hello dzierżawy z hello wirtualnego dysku twardego za pomocą portalu Azure. Aby uzyskać więcej informacji, zobacz [Usuń hello dzierżawy z wirtualnego dysku twardego hello](#remove-the-lease-from-the-vhd). 

7. Przejdź toohello Eksploratora usługi Storage platformy Azure, kliknij prawym przyciskiem myszy hello wirtualnego dysku twardego, a następnie wybierz delete.

8. Usunięcie konta magazynu hello.

### <a name="method-2---use-azure-portal"></a>Metoda 2 - użyj portalu Azure 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>: Krok 1 hello wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu hello

1. Podczas usuwania konta magazynu hello pojawi się okno dialogowe wiadomości, takie jak następujące hello: 

    ![Podczas usuwania konta magazynu hello komunikat o błędzie](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Sprawdź hello **adres URL dysku** konto magazynu hello tooidentify i hello wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu hello. W hello poniższy przykład, hello ciągu przed ". blob.core.windows.net" jest nazwa konta magazynu hello, a "SCCM2012-2015-08-28.vhd" hello, Nazwa wirtualnego dysku twardego.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
3. W menu Centrum hello wybierz **wszystkie zasoby**. Przejdź toohello konta magazynu, a następnie wybierz **obiekty BLOB** > **wirtualne dyski twarde**.

    ![Zrzut ekranu przedstawiający portal hello, za pomocą hello konta magazynu i kontener "VHD" hello wyróżnione](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Zlokalizuj hello wirtualnego dysku twardego, który mamy uzyskany z adresu URL dysku hello wcześniej. Następnie określ, którego używa wirtualna hello wirtualnego dysku twardego. Zwykle można określić, które maszyna wirtualna przechowuje hello wirtualnego dysku twardego, sprawdzając nazwę hello wirtualnego dysku twardego:

Maszyna wirtualna w modelu programowania usługi Resource Manager

   * Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd
   * Dyski danych należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd

Maszynę Wirtualną w klasycznym modelu programowania

   * Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Dyski danych należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Krok 2: Usuń hello dzierżawy z hello wirtualnego dysku twardego

[Usuń hello dzierżawy z hello wirtualnego dysku twardego](#remove-the-lease-from-the-vhd), a następnie usunąć konto magazynu hello.

## <a name="what-is-a-lease"></a>Co to jest dzierżawa?
Dzierżawa jest blokady, które mogą być używane toocontrol dostępu tooa blob (na przykład dysk VHD). Gdy obiektu blob jest dzierżawiony, tylko hello właściciele hello dzierżawy mają dostęp do obiektów blob hello. Dzierżawa jest ważne dla hello z następujących powodów:

* Zapobiega uszkodzenie danych, jeśli wiele właścicieli spróbuj toowrite toohello tę samą część obiektu blob hello na powitania tym samym czasie.
* Obiekt blob hello uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).
* Konto magazynu hello uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).

### <a name="remove-hello-lease-from-hello-vhd"></a>Usuń hello dzierżawy z hello wirtualnego dysku twardego
Jeśli hello wirtualnego dysku twardego, dysk systemu operacyjnego, należy usunąć hello wirtualna tooremove hello dzierżawy:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na powitania **Centrum** menu, wybierz opcję **maszyn wirtualnych**.
3. Wybierz hello maszynę Wirtualną, która przechowuje dzierżawę na powitania wirtualnego dysku twardego.
4. Upewnij się, że nic nie jest aktywnie używających hello maszyny wirtualnej i czy użytkownik nie jest już konieczne hello maszyny wirtualnej.
5. U góry hello hello **szczegóły maszyny Wirtualnej** bloku, wybierz opcję **usunąć**, a następnie kliknij przycisk **tak** tooconfirm.
6. powinien zostać usunięty Hello maszyny Wirtualnej, ale hello wirtualnego dysku twardego mogą być przechowywane. Jednak hello wirtualnego dysku twardego nie powinni mieć dzierżawę na nim. Może upłynąć kilka minut, aż toobe dzierżawy hello wydane. zwolnieniu tooverify, który hello dzierżawy, przejdź zbyt**wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >  **wirtualne dyski twarde**. W hello **właściwości obiektu Blob** okienka, hello **stanu dzierżawy** wartość powinna być **odblokowany**.

Jeśli hello wirtualnego dysku twardego jest dysk z danymi, odłącz hello wirtualnego dysku twardego z hello wirtualna tooremove hello dzierżawy:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na powitania **Centrum** menu, wybierz opcję **maszyn wirtualnych**.
3. Wybierz hello maszynę Wirtualną, która przechowuje dzierżawę na powitania wirtualnego dysku twardego.
4. Wybierz **dysków** na powitania **szczegóły maszyny Wirtualnej** bloku.
5. Wybierz dysk danych hello, który przechowuje dzierżawę na powitania wirtualnego dysku twardego. Można określić, który wirtualny dysk twardy jest podłączony w hello dysku, sprawdzając adres URL hello hello wirtualnego dysku twardego.
6. Określ, z pewnością, że nic nie jest aktywnie używających hello dysku danych.
7. Kliknij przycisk **Detach** na powitania **dysku szczegóły** bloku.
8. dysk Hello powinny teraz można odłączyć od hello maszyny Wirtualnej, a hello wirtualnego dysku twardego nie może mieć dzierżawę na nim. Może upłynąć kilka minut, aż toobe dzierżawy hello wydane. została wydana tooverify, który hello dzierżawy, przejdź zbyt**wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >  **wirtualne dyski twarde**. W hello **właściwości obiektu Blob** okienka, hello **stanu dzierżawy** wartość powinna być **odblokowany**.

## <a name="next-steps"></a>Następne kroki
* [Usunięcie konta magazynu](storage-create-storage-account.md#delete-a-storage-account)
* [Jak toobreak hello zablokowany dzierżawy magazynu obiektów blob w Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
