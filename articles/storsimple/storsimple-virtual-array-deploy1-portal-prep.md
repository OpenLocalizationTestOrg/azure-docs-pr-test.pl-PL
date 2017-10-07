---
title: przedprodukcyjnym aaaPortal dla tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: Pierwszy samouczek toodeploy tablicy wirtualnego StorSimple obejmuje przygotowanie hello portalu Azure
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Wdrażanie tablicy wirtualne StorSimple — przygotowanie hello portalu Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Omówienie

Jest to hello pierwszego artykułu hello serii samouczków wdrożenia wymagane toocompletely wdrażania wirtualnego tablica jako serwera plików lub przy użyciu modelu Resource Manager powitania serwera iSCSI. W tym artykule opisano toocreate przygotowania hello i konfigurowanie programu Menedżer urządzeń StorSimple usługi wcześniejsze tooprovisioning wirtualnego tablicy. Ten artykuł zawiera również linki limit tooa konfiguracji listy kontrolnej, konfiguracji i wymagania wstępne dotyczące wdrażania.

Potrzebne administratora uprawnień toocomplete hello procesu instalacji i konfiguracji. Firma Microsoft zaleca przejrzenie listy kontrolnej konfiguracji wdrożenia hello przed rozpoczęciem. Przygotowanie portalu Hello ma mniej niż 10 minut.

informacje Hello opublikowane w tym artykule dotyczą wdrażania toohello tablice wirtualnego StorSimple w hello portalu Azure i Microsoft Azure dla instytucji rządowych chmury.

### <a name="get-started"></a>Rozpoczęcie pracy
przepływ pracy wdrożenia Hello składa się z przygotowanie hello portalu, udostępniania wirtualnego tablicy w środowisku zwirtualizowanym i zakończeniu hello instalacji. wprowadzenie do wdrażania tablicy wirtualnego StorSimple hello jako serwer plików lub serwera iSCSI tooget, należy toohello toorefer następujące tabelaryczne zasobów.

#### <a name="deployment-articles"></a>Wdrażania

toodeploy tablica wirtualnego StorSimple, zobacz następujące artykuły w określonej sekwencji hello toohello.

| **#** | **W tym kroku** | **Aby to zrobić...** | **I korzystać z tych dokumentów.** |
| --- | --- | --- | --- |
| 1. |**Konfigurowanie hello portalu Azure** |Tworzenie i konfigurowanie programu Menedżer urządzeń StorSimple usługi wcześniejsze tooprovisioning tablicą wirtualne StorSimple. |[Przygotowanie hello portalu](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Zainicjuj obsługę hello wirtualnego tablicy** |Dla funkcji Hyper-V udostępniania i połączyć tooa tablicy wirtualnego StorSimple na komputerze hosta z funkcją Hyper-V w systemie Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2. <br></br> <br></br> VMware udostępniania i połączyć tooa tablicy wirtualnego StorSimple na komputerze hosta z systemem VMware ESXi 5.5 lub nowszym.<br></br> |[Udostępnianie wirtualnych tablicy w funkcji Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Udostępnianie wirtualnych tablicy w środowisku programu VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Konfigurowanie hello wirtualnego tablicy** |Dla serwera plików wykonywania początkowej konfiguracji, zarejestruj StorSimple serwera plików, a następnie przeprowadzić konfigurację urządzenia hello. Można następnie udostępnić udziałów SMB. <br></br> <br></br> Dla serwera iSCSI wykonywania początkowej konfiguracji, Zarejestruj serwer iSCSI StorSimple i przeprowadzić konfigurację urządzenia hello. Następnie można alokować woluminy iSCSI. |[Konfigurowanie wirtualnego tablicy jako serwer plików](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Konfigurowanie wirtualnego tablicy jako serwer iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Można teraz rozpocząć tooset się hello portalu Azure.

## <a name="configuration-checklist"></a>Lista kontrolna dotycząca konfiguracji

Lista kontrolna dotycząca konfiguracji Hello opisano informacje hello toocollect potrzebne przed skonfigurowaniem oprogramowania hello na tablica wirtualne StorSimple. Przygotowanie tych informacji wcześniejsze pomaga czasu usprawnienia hello proces wdrażania urządzenia StorSimple hello w danym środowisku. Zależności od tego, czy tablica wirtualne StorSimple jest wdrożona jako serwera plików lub serwera iSCSI, potrzebujesz jednego z następującej listy kontrolne hello.

* Pobierz hello [StorSimple wirtualnego tablicy plików serwera Lista kontrolna dotycząca konfiguracji](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Pobierz hello [iSCSI tablicy wirtualnego StorSimple Lista kontrolna dotycząca konfiguracji serwera](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Wymagania wstępne

W tym miejscu możesz znaleźć wymagania wstępne dotyczące hello konfiguracji usługi Menedżer urządzeń StorSimple, tablicy wirtualnego StorSimple i hello sieci centrum danych.

### <a name="for-hello-storsimple-device-manager-service"></a>Dla hello usługi Menedżer StorSimple urządzenia

Przed rozpoczęciem upewnij się, że:

* Masz konto Microsoft z poświadczeniami dostępu.
* Masz konto magazynu platformy Microsoft Azure z poświadczeniami dostępu.
* Subskrypcja platformy Microsoft Azure powinno być włączone dla usługi Menedżer StorSimple urządzenia.

### <a name="for-hello-storsimple-virtual-array"></a>Dla hello tablicy wirtualnego StorSimple

Przed wdrożeniem wirtualnego tablicy, upewnij się, że:

* Używany system dostępu tooa hosta funkcji Hyper-V w systemie Windows Server 2008 R2 lub nowszym i VMware (ESXi 5.5 lub nowszego), które mogą być używane tooa inicjowania obsługi administracyjnej urządzeniu.
* system hosta Hello jest możliwe toodedicate hello następujących zasobów tooprovision tablica wirtualnego:
  
  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM. Jeśli planujesz tooconfigure hello wirtualnego tablicy jako serwer plików, 8 GB obsługuje 2 milionów plików. Należy 16 GB pamięci RAM toosupport 2-4 miliony plików.
  * Jeden interfejs sieciowy.
  * Dysk wirtualny 500 GB danych systemu.

### <a name="for-hello-datacenter-network"></a>Witaj sieci centrum danych

Przed rozpoczęciem upewnij się, że:

* Witaj sieci w centrum danych jest skonfigurowany zgodnie z harmonogramem hello wymagań sieciowych dla urządzenia StorSimple. Aby uzyskać więcej informacji, zobacz hello [wymagania systemowe tablicy wirtualnego StorSimple](storsimple-ova-system-requirements.md).
* Tablica wirtualnego StorSimple ma dedykowany 5 MB/s przepustowości połączenia z Internetem (lub więcej) dostępne przez cały czas. Przepustowość nie powinien być współużytkowany z innych aplikacji.

## <a name="step-by-step-preparation"></a>Krok przygotowania

Na użytek hello następujące instrukcje krok po kroku tooprepare portalem hello usługi Menedżer StorSimple urządzenia.

## <a name="step-1-create-a-new-service"></a>Krok 1. Tworzenie nowej usługi

Jedno wystąpienie usługi Menedżer StorSimple urządzenia hello można zarządzać wiele tablic wirtualne StorSimple. Wykonaj następujące kroki toocreate wystąpienie usługi Menedżer StorSimple urządzenia hello hello. Jeśli masz istniejące toomanage usługi Menedżer StorSimple urządzenia z macierzami wirtualnego, Pomiń ten krok i przejdź za[krok 2: Pobierz klucz rejestracji usługi hello](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Jeśli nie włączono hello automatyczne tworzenie konta magazynu z usługą, konieczne będzie toocreate co najmniej jedno konto magazynu, po pomyślnym utworzeniu usługi.
> 
> * Jeśli nie utworzono automatycznie konta magazynu, należy przejść za[Konfigurowanie nowego konta magazynu dla usługi hello](#optional-step-configure-a-new-storage-account-for-the-service) szczegółowe informacje.
> * Jeśli włączono automatyczne tworzenie konta magazynu hello Przejdź zbyt[krok 2: Pobierz klucz rejestracji usługi hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Krok 2: Pobieranie klucza rejestracji usługi hello

Po skonfigurowaniu i uruchomieniu hello usługi Menedżer StorSimple urządzenia należy klucz rejestracji usługi hello tooget. Ten klucz jest używane tooregister i połączenia z usługą hello urządzenia StorSimple.

Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Witaj klucz rejestracji usługi jest używane tooregister hello wszystkie urządzenia StorSimple Menedżera urządzeń, które wymagają tooregister przy użyciu usługi Menedżer StorSimple urządzenia.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Krok 3: Pobierz hello wirtualnego tablicy obrazu

Po klucz rejestracji usługi hello, konieczne będzie toodownload hello odpowiednie tablicy wirtualnego obrazu tooprovision wirtualnego tablicy w systemie hosta. obrazy wirtualnego tablicy Hello są zależne od systemu operacyjnego, można pobrać ze strony Szybki Start hello w hello portalu Azure.

> [!IMPORTANT]
> oprogramowanie Hello hello tablicy wirtualnego StorSimple można używać tylko z hello usługi Menedżer StorSimple urządzenia.
> 
> 

Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>Obraz wirtualnego tablicy hello tooget

1. Zaloguj się na powitania [portalu Azure](https://portal.azure.com/). 
2. W portalu Azure hello, kliknij przycisk **Przeglądaj > menedżerów urządzenia StorSimple**.
3. Wybierz istniejącą usługę Menedżer StorSimple urządzenia. W hello **Menedżera urządzeń StorSimple** bloku, kliknij przycisk **Szybki Start**. 
4. Kliknij przycisk hello łącze odpowiednie toohello obrazu, które mają toodownload z hello Microsoft Download Center. pliki obrazów Hello są około 4.8 GB.
   
   * VHDX dla funkcji Hyper-V w systemie Windows Server 2012 lub nowszym
   * Wirtualnego dysku twardego funkcji Hyper-v w systemie Windows Server 2008 R2 lub nowszym
   * VMDK VMWare ESXi 5.5 lub nowszy
5. Pobierz i Rozpakuj hello pliku tooa dysku lokalnego, co Zanotuj którym znajduje się plik rozpakowane hello.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Krok opcjonalny: Konfigurowanie nowego konta magazynu dla usługi hello

Ten krok jest opcjonalny i należy wykonać tylko wtedy, gdy nie włączono hello automatyczne tworzenie konta magazynu z usługą.

Jeśli potrzebujesz konta magazynu Azure w innym regionie toocreate, zobacz [jak toocreate konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) instrukcje krok po kroku.

Wykonaj następujące kroki w hello hello [portalu Azure](https://ms.portal.azure.com/) na powitania Menedżera urządzeń StorSimple usługi strony tooadd istniejącego konta magazynu Microsoft Azure.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd poświadczeń konta magazynu, który ma hello tej samej subskrypcji platformy Azure jako hello usługa Menedżera urządzeń

1. Przejdź tooyour usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie. Spowoduje to otwarcie hello **omówienie** bloku.
2. Wybierz **poświadczeń konta magazynu** w hello **konfiguracji** sekcji.
3. Kliknij pozycję **Dodaj**.
4. W hello **dodawania konta magazynu** bloku hello następujące:
   
    1. Aby uzyskać **subskrypcji**, wybierz pozycję **bieżącego**.
   
    2. Podaj nazwę hello konta magazynu Azure.
   
    3. Wybierz **włączyć** toocreate bezpiecznego kanału komunikacji sieciowej między chmury urządzenia i hello StorSimple. Wybierz **wyłączyć** tylko wtedy, gdy pracujesz w chmurze prywatnej.
   
    4. Kliknij pozycję **Dodaj**. Użytkownik jest powiadamiany po pomyślnym utworzeniu konta magazynu hello.<br></br>
   
     ![Dodawanie istniejących poświadczeń dla konta magazynu](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Następny krok

Witaj następnym krokiem jest tooprovision maszyny wirtualnej do macierzy wirtualne StorSimple. W zależności od systemu operacyjnego hosta, zobacz hello szczegółowe instrukcje w:

* [Zapewnij tablicą wirtualnego StorSimple w funkcji Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Zapewnij tablicą wirtualnego StorSimple w środowisku programu VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

