---
title: informacje o wersji aaaStorSimple 8000 serii aktualizacji 4 | Dokumentacja firmy Microsoft
description: "Opis nowych funkcji hello, problemy i rozwiązania StorSimple 8000 serii Update 4."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Informacje o wersji StorSimple 8000 serii aktualizacji 4

## <a name="overview"></a>Omówienie

Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować problemy krytyczne Otwórz hello StorSimple 8000 serii Update 4. Zawierają one również listę aktualizacji oprogramowania StorSimple hello zawarte w tej wersji. 

Aktualizacja 4 może być zastosowane tooany StorSimple urządzenie z systemem zlecenia (GA) lub Update 0.1 za pomocą aktualizacji w wersji 3.1. Wersja urządzenia Hello skojarzony z aktualizacją Update 4 jest 6.3.9600.17820.

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Aktualizacja 4 ma oprogramowanie urządzenia, oprogramowania układowego należy LSI sterowników i oprogramowania układowego, oprogramowania układowego dysku, Storport i Spaceport, zabezpieczeń i inne aktualizacje systemu operacyjnego. Trwa około 4 godziny tooinstall tej aktualizacji. Aktualizacja oprogramowania układowego dysku jest destrukcyjne aktualizacji i powoduje przestój dla danego urządzenia. Zaleca się zastosować aktualizacji 4 tookeep aktualne urządzenia. 
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako te staną się dostępne wkrótce.

## <a name="whats-new-in-update-4"></a>Nowości w aktualizacji w wersji 4

Witaj następujące ulepszenia klucza i poprawki zostały wprowadzone w pakiecie Update 4.

* **Inteligentny automatycznego algorytmów odzyskiwanie miejsca** — aktualizacji 4, hello miejsca automatyczne odzyskiwanie algorytmy są odzyskiwanie miejsca hello rozszerzone tooadjust cykle hello oczekiwano odzyskać dostępnego miejsca w chmurze hello. 

* **Ulepszenia wydajności dla woluminów przypiętych lokalnie** — aktualizacji w wersji 4 ma wyższą wydajność hello woluminów przypiętych lokalnie w scenariuszach, w których wprowadzanie danych wysokiej (rozmiar danych można porównywać pod względem toovolume).

* **Przywracania oparte na Heatmap** — hello starszych wersjach po odzyskiwania awaryjnego (DR), dane hello została przywrócona z chmury hello na podstawie wzorców dostępu hello, co spowoduje niską wydajność. 

    Nowa funkcja jest zaimplementowana w aktualizacji 4 czy śledzi często używanych danych toocreate heatmap podczas urządzenie hello jest użycie wcześniejszego tooDR (najczęściej używanych fragmentów danych mają wysokie cieplna używane mniejsze fragmenty ma cieplna niski). Po odzyskiwania po awarii używa StorSimple hello heatmap tooautomatically przywracania i rehydrate hello danych z chmury hello. 

    Wszystkie przywraca hello są teraz heatmap na podstawie operacji przywracania. Aby uzyskać więcej informacji na jak heatmap tooquery i Anuluj na podstawie zadań przywracania i preparaty nawadniające Przejdź zbyt[programu Windows PowerShell dla StorSimple dokumentacji poleceń cmdlet](https://technet.microsoft.com/library/dn688168.aspx).

* **Narzędzie diagnostyczne StorSimple** — w aktualizacji 4 diagnostyki StorSimple, jest narzędzie wydane tooallow dla łatwe diagnozowanie i rozwiązywanie problemów związanych kondycja składnika toosystem, sieci, wydajności i sprzętu. To narzędzie jest uruchamiane za pomocą hello środowiska Windows PowerShell dla urządzenia StorSimple. Aby uzyskać więcej informacji, przejdź zbyt[Rozwiązywanie problemów przy użyciu narzędzia diagnostycznego StorSimple](storsimple-8000-diagnostics.md).

* **Oparty na interfejsie użytkownika narzędzia migracji StorSimple** -toothis poprzednich wersji, migrację danych z serii 5000 7000 wymagane hello użytkowników tooexecute część przepływu pracy migracja hello przy użyciu hello Azure PowerShell interfejsu. W tej wersji łatwy w obsłudze migracji StorSimple oparty na interfejsie użytkownika narzędzia jest udostępniana do obsługi toofacilitate hello samego migracji przepływu pracy. To narzędzie może pozwalają również hello konsolidacji zasobników odzyskiwania. 

* **Zmiany dotyczące FIPS** — w tej wersji i jego nowszych wersjach, FIPS jest włączone domyślnie na wszystkich urządzeń z serii StorSimple 8000 powitania dla obu hello kont w chmurze publicznej systemu Azure i Microsoft Azure dla instytucji rządowych.

* **Aktualizuj zmiany** — w tej wersji tooupdate powiązanych usterek Naprawiono błędy.

* **Alert w przypadku awarii dysku** — w tej wersji dodano jest nowy alert z ostrzeżeniem hello użytkownika o zbliżającym się awarii dysku. Jeśli wystąpi ten alert, skontaktuj się z Microsoft Support tooship dysk zastępczy. Aby uzyskać więcej informacji, przejdź zbyt[alerty sprzętu na urządzeniu StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Zmiany zastępczego kontrolera** — polecenie cmdlet umożliwia hello użytkownika tooquery hello stan procesu wymiany kontrolera hello jest dodawany w tej wersji. Aby uzyskać więcej informacji, przejdź toohello [status zastąpienia kontrolera tooquery polecenia cmdlet](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemy rozwiązane w ramach aktualizacji w wersji 4

Witaj Poniższa tabela zawiera podsumowanie problemów, które zostały usunięte w pakiecie Update 4.    

| Nie | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Tryb failover |W hello starszej wersji, po hello w tryb failover, został problem związany toocleanup obserwowane na powitania klienta lokacji. Tego problemu w tej wersji. |Tak |Tak |
| 2 |Woluminów przypiętych lokalnie |W poprzedniej wersji hello wystąpił problem toorelated operacji tworzenia woluminu dla woluminów przypiętych lokalnie, które umożliwiałyby błędy tworzenia woluminu. Ten problem został spowodowany głównego i stałym w tej wersji. |Tak |Nie |
| 3 |Pakiet pomocy technicznej |W poprzedniej wersji wystąpiły problemy pokrewne tooSupport pakiet, który spowoduje powstanie wyjątku System.OutOfMemory lub inne błędy uniemożliwiające tworzenia pakietu obsługi. Te błędy są ustalone w tej wersji. |Tak |Tak |
| 4 |Monitorowanie |W poprzedniej wersji wystąpił problem związany wykresów toomonitoring dla woluminów przypiętych lokalnie gdzie zużycie był wyświetlany w EB. Ten problem zostanie rozwiązany w tej wersji. |Tak |Tak |
| 5 |Migracja |W poprzedniej wersji znaleziono kilka problemów powiązanych toohello niezawodności migracji z urządzeń z serii too8000 serii 5000 7000. Te problemy rozwiązano w tej wersji. |Tak |Tak |
| 6 |Aktualizacja |W poprzednich wersjach, jeśli wystąpił błąd aktualizacji, kontrolerów hello przejdzie do trybu odzyskiwania i dlatego nie można kontynuować aktualizacji hello hello użytkownika, a musi toocontact Support firmy Microsoft. <br> To zachowanie zostało zmienione w tej wersji. Jeśli użytkownik hello ma Niepowodzenie aktualizacji po obu kontrolerów hello są uruchomione hello tej samej wersji (aktualizacja 4), powitalne kontrolerów nie przechodzą w trybie odzyskiwania. Użytkownik hello napotka tego błędu, firma Microsoft zaleca czy czekać bit, a następnie ponów próbę aktualizacji hello. Ponów próbę Hello może się powieść. Jeśli hello ponownych prób nie powiedzie się, a następnie należy skontaktować się z Microsoft Support. |Tak |Tak |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Znane problemy w pakiecie Update 4 z poprzednich wersji

Nie występują nowe znane problemy w pakiecie Update 4. Listę problemów przenoszone tooUpdate 4 z poprzednich wersji, przejdź zbyt[wersji Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Magistrali Serial attached SCSI (SAS) kontrolera aktualizacje w pakiecie Update 4

Ta wersja zawiera kontroler SAS i LSI aktualizacje sterowników i oprogramowania układowego. Aby uzyskać więcej informacji na temat tooinstall tych aktualizacji, zobacz temat [zainstalować aktualizacji w wersji 4](storsimple-install-update-4.md) na urządzeniu StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Urządzenie wirtualne aktualizacji w pakiecie Update 4

Ta aktualizacja nie może być zastosowane toohello urządzenia chmury StorSimple (znanej także jako hello urządzenia wirtualnego). Nowe urządzenia wirtualnego należy utworzyć toobe. 

## <a name="next-step"></a>Następny krok

Dowiedz się, jak za[zainstalować aktualizacji w wersji 4](storsimple-install-update-4.md) na urządzeniu StorSimple.

