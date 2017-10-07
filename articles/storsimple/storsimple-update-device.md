---
title: "aaaUpdate urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak toouse hello StorSimple aktualizacji funkcji tooinstall regularnych i obsługi trybu aktualizacje i poprawki."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Zaktualizuj urządzenia z serii StorSimple 8000
## <a name="overview"></a>Omówienie
Hello StorSimple aktualizacje funkcji pozwalają tooeasily aktualizowanie urządzenia StorSimple. W zależności od typu aktualizacji hello należy zastosować aktualizacje toohello urządzenia za pośrednictwem hello klasycznego portalu Azure lub za pośrednictwem interfejsu programu Windows PowerShell hello. W tym samouczku opisano typy aktualizacji hello i w jaki sposób tooinstall każdego z nich.

Można zastosować dwa typy aktualizacji urządzenia: 

* Regularne (lub tryb normalny) aktualizacji
* Aktualizacje trybu konserwacji

Możesz zainstalować regularne aktualizacje za pośrednictwem hello klasycznego portalu Azure lub programu Windows PowerShell; należy jednak używać aktualizacji trybu konserwacji tooinstall środowiska Windows PowerShell. 

Każdy typ aktualizacji jest opisane oddzielnie, poniżej.

### <a name="regular-updates"></a>Regularne aktualizacje
Regularne aktualizacje są Brak aktualizacji, które mogą być instalowane, gdy urządzenie hello jest w trybie normalnym. Aktualizacje te są stosowane przy użyciu hello Microsoft Update witryny sieci Web tooeach urządzenia kontrolera. 

> [!IMPORTANT]
> Tryb failover kontrolera mogą wystąpić podczas procesu aktualizacji hello. Jednak nie wpłynie to dostępność systemu lub operacji.
> 
> 

* Szczegółowe informacje dotyczące sposobu tooinstall regular aktualizacje za pośrednictwem hello klasycznego portalu Azure, zobacz [zainstalować regularne aktualizacje za pośrednictwem klasycznego portalu Azure hello](#install-regular-updates-via-the-azure-classic-portal).
* Można także zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple. Aby uzyskać więcej informacji, zobacz [zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Aktualizacje trybu konserwacji
Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, takie jak aktualizacje oprogramowania dysku. Te aktualizacje wymagają toobe urządzenia hello przełączyć w tryb konserwacji. Aby uzyskać więcej informacji, zobacz [krok 2: tryb konserwacji wprowadź](#step2). Nie można użyć hello Azure classic portal tooinstall obsługi trybu aktualizacji. Zamiast tego należy użyć programu Windows PowerShell dla urządzenia StorSimple. 

Aby uzyskać szczegółowe informacje na sposób aktualizowania tooinstall tryb konserwacji, zobacz [zainstalować obsługi trybu aktualizacje za pomocą programu Windows PowerShell dla StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Tryb konserwacji, aktualizacje należy zastosować oddzielnie tooeach kontrolera. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Zainstaluj regularne aktualizacje za pomocą hello klasycznego portalu Azure
Można użyć urządzenia StorSimple tooyour hello Azure classic portal tooapply aktualizacji.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Zainstaluj regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
Alternatywnie można użyć programu Windows PowerShell aktualizacji regularne (tryb normalny) tooapply StorSimple.

> [!IMPORTANT]
> Mimo że można zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple, zdecydowanie zaleca się zainstalowanie regularne aktualizacje za pośrednictwem hello klasycznego portalu Azure. Począwszy od aktualizacji 1, wstępne sprawdzanie jest wykonywane wcześniejsze tooinstalling aktualizacje z portalu hello. Kontrole wstępne będzie zastępują błędy i upewnij się, płynniejszy efekt. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Zainstaluj aktualizacje tryb konserwacji za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
Korzystając z programu Windows PowerShell dla urządzenia StorSimple tooyour StorSimple tooapply obsługi trybu aktualizacji. Wszystkie żądania We/Wy są wstrzymane w tym trybie. Usług takich jak trwałej pamięci (NVRAM) lub usługa klastrowania hello również zostały zatrzymane. Zarówno kontrolery są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb. Po zakończeniu pracy w tym trybie, wszystkie usługi hello wznowi i powinna być w dobrej kondycji. (Może to potrwać kilka minut).

Aktualizacje trybu konserwacji tooapply należy otrzymasz alert za pośrednictwem hello klasycznego portalu Azure, czy są aktualizacje, które muszą zostać zainstalowane. Ten alert zawiera instrukcje dotyczące używania środowiska Windows PowerShell dla StorSimple tooinstall hello aktualizacji. Po zaktualizowaniu urządzenia, użyj hello sam tryb tooRegular procedury toochange hello urządzenia. Aby uzyskać instrukcje, zobacz [krok 4: tryb konserwacji zakończenia](#step4).

> [!IMPORTANT]
> * Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, sprawdzając hello **stan sprzętu** na powitania **konserwacji** strony w hello klasycznego portalu Azure. Jeśli kontroler hello nie działa prawidłowo, skontaktuj się z Microsoft Support hello następnych kroków. Aby uzyskać więcej informacji Przejdź tooContact Support firmy Microsoft. 
> * Podczas pracy w trybie konserwacji, należy tooapply hello aktualizacji najpierw na jeden kontroler, a następnie na hello inny kontroler.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Krok 1: Łączenie toohello konsoli szeregowej<a name="step1">
Po pierwsze korzystanie z aplikacji, takich jak PuTTY tooaccess hello konsoli szeregowej. Witaj poniższej procedurze wyjaśniono, jak konsoli szeregowej toohello toouse PuTTY tooconnect.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Krok 2: Wprowadź trybu konserwacji<a name="step2">
Po podłączeniu konsoli toohello ustalić, czy są aktualizacje tooinstall, a następnie wprowadź tooinstall trybu konserwacji je.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Krok 3: Instalowanie aktualizacji<a name="step3">
Następnie zainstaluj aktualizacje.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Krok 4: Tryb obsługi zakończenia<a name="step4">
Na koniec wyjść z trybu konserwacji.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Instalowanie poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
W przeciwieństwie do aktualizacji dla programu Microsoft Azure StorSimple są zainstalowane poprawki z folderu udostępnionego. Podobnie jak w przypadku aktualizacji, istnieją dwa typy poprawki: 

* Regularne poprawki 
* Poprawki trybu konserwacji  

Witaj poniższe procedury wyjaśniają, jak toouse środowiska Windows PowerShell dla regularne tooinstall StorSimple i poprawki dla trybu konserwacji.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Co się stanie, resetowania urządzenia hello tooupdates Jeśli przeprowadzenie do ustawień fabrycznych?
Jeśli urządzenie jest ustawienia toofactory resetowania, wszystkie aktualizacje hello zostaną utracone. Po rejestracji i konfiguracji hello Resetowanie do ustawień fabrycznych urządzenia należy toomanually Zainstaluj aktualizacje za pośrednictwem hello klasycznego portalu Azure i/lub środowiska Windows PowerShell dla urządzenia StorSimple. Aby uzyskać więcej informacji na temat resetowania do ustawień fabrycznych, zobacz [przywrócić ustawienia domyślne toofactory urządzenia hello](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [środowiska Windows PowerShell dla StorSimple tooadminister urządzenia StorSimple](storsimple-windows-powershell-administration.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

