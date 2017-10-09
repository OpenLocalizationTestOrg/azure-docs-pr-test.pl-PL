---
title: "zmiany aaaTrack za pomocą usługi Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Witaj rozwiązania analizy dzienników śledzenia zmian pomaga zidentyfikować oprogramowanie i zmiany usługi systemu Windows w środowisku."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Śledzenie zmian w oprogramowaniu w Twoim środowisku z hello rozwiązaniu do śledzenia zmian

![Zmień symbol śledzenia](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Ten artykuł pomaga hello Użyj rozwiązania tooeasily analizy dzienników śledzenia zmian identyfikować zmiany w danym środowisku. Witaj rozwiązania śledzi zmiany tooWindows i oprogramowania w systemie Linux, pliki systemu Windows i kluczy rejestru usług systemu Windows i demonów systemu Linux. Identyfikowanie zmian konfiguracji może pomóc w określeniu problemy z działaniem.

Możesz zainstalować program hello tooupdate hello rozwiązania typu agenta, który został zainstalowany. Zmiany tooinstalled oprogramowania, usług systemu Windows i demonów systemu Linux na serwerach hello monitorowane są do odczytu. Następnie dane hello są wysyłane toohello analizy dzienników usługi w chmurze hello do przetwarzania. Logika jest stosowane toohello odebranych danych i usługi w chmurze hello rejestruje dane hello. Przy użyciu informacji hello na pulpicie nawigacyjnym hello śledzenia zmian, można łatwo Zobacz hello zmiany infrastruktury serwera.

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

* Musi mieć [Windows](log-analytics-windows-agents.md), [programu Operations Manager](log-analytics-om-agents.md), lub [Linux](log-analytics-linux-agents.md) agenta na każdym komputerze, na którym chcesz toomonitor zmiany.
* Dodaj hello śledzenia zmian rozwiązania tooyour obszar roboczy OMS z hello [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Można dodać hello rozwiązania przy użyciu informacji hello w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Jest wymagana żadna dalsza konfiguracja.

### <a name="configure-linux-files-tootrack"></a>Skonfiguruj tootrack plików systemu Linux
Użyj hello następujące kroki tooconfigure pliki tootrack na komputerach z systemem Linux.

1. W portalu OMS hello, kliknij przycisk **ustawienia** (symbol hello koło zębate).
2. Na powitania **ustawienia** kliknij przycisk **danych**, a następnie kliknij przycisk **Linux pliku śledzenia**.
3. W obszarze Linux śledzenia zmian plików wpisz pełną ścieżkę hello, w tym hello nazwy pliku hello, że mają tootrack, a następnie kliknij przycisk hello **Dodaj** symbolu. Na przykład: "/etc/*.conf"
4. Kliknij pozycję **Zapisz**.  

> [!NOTE]
> Linux pliku śledzenia ma dodatkowe możliwości, w tym katalogu śledzenia, recrusion za pośrednictwem katalogów i symboli wieloznacznych śledzenia.

### <a name="configure-windows-files-tootrack"></a>Skonfiguruj tootrack plików systemu Windows
Użyj następujących kroków tooconfigure pliki tootrack na komputerach z systemem Windows hello.

1. W portalu OMS hello, kliknij przycisk **ustawienia** (symbol hello koło zębate).
2. Na powitania **ustawienia** kliknij przycisk **danych**, a następnie kliknij przycisk **śledzenia plików systemu Windows**.
3. W obszarze śledzenia zmian plików systemu Windows wpisz pełną ścieżkę hello, w tym hello nazwy pliku hello, że mają tootrack, a następnie kliknij przycisk hello **Dodaj** symbolu. Na przykład: C:\Program Files (x86) \Internet Explorer\iexplore.exe lub C:\Windows\System32\drivers\etc\hosts.
4. Kliknij pozycję **Zapisz**.  
   ![Śledzenie zmian plików systemu Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Skonfiguruj tootrack kluczy rejestru systemu Windows
Użyj następującego tootrack klucze rejestru tooconfigure kroki na komputerach z systemem Windows hello.

1. W portalu OMS hello, kliknij przycisk **ustawienia** (symbol hello koło zębate).
2. Na powitania **ustawienia** kliknij przycisk **danych**, a następnie kliknij przycisk **śledzenia rejestru systemu Windows**.
3. W obszarze śledzenia zmian rejestru systemu Windows wpisz hello cały klucz, że chcesz tootrack, a następnie kliknij przycisk hello **Dodaj** symbolu.
4. Kliknij pozycję **Zapisz**.  
   ![Śledzenie zmian w rejestrze systemu Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Opis właściwości kolekcji plików systemu Linux
1. **Typ**
   * **Plik** (raport metadanych pliku — rozmiar, Data modyfikacji, skrót itp.)
   * **Katalog** (katalogu metadanych raportu — rozmiar, Data modyfikacji itp.)
2. **Łącza** (Obsługa systemu Linux łącza symbolicznego odwołuje się do tooother plików lub katalogów)
   * **Ignoruj** (łączy symbolicznych Ignoruj podczas recurions toonot obejmuje hello plików/katalogów, do których odwołuje się)
   * **Postępuj zgodnie z** (łączy symbolicznych hello wykonaj podczas rekursji tooalso obejmuje hello plików/katalogów, do których odwołuje się)
   * **Zarządzanie** (wykonaj łączy symbolicznych hello i zmień traktowania hello zwrócony zawartości)

   > [!NOTE]   
   > Witaj łącza "Manage", opcja nie jest zalecane. Pobieranie zawartości pliku nie jest obsługiwana.

3. **Recurse** (Recurse za pomocą poziomów folderu i śledzić wszystkie pliki spełniające instrukcji ścieżki hello)
4. **Sudo** (Włącz dostęp do plików lub katalogów, które wymagają uprawnień sudo)

### <a name="limitations"></a>Ograniczenia
Witaj w rozwiązaniu do śledzenia zmian nie obsługuje obecnie hello następujące elementy:

* Folderów (katalogów) dla systemu Windows plik śledzenia
* Rekursja plików śledzenia
* Symbole wieloznaczne śledzenia plików systemu Windows
* Zmienne ścieżek
* Systemy plików sieciowych
* Zawartość pliku

Inne ograniczenia:

* Witaj **maksymalny rozmiar pliku** kolumny i wartości są używane w hello bieżąca implementacja.
* W przypadku zebrania plików więcej niż 2500 w cyklu zbierania 30-minutowych hello, może wiązać ze spadkiem wydajności rozwiązania.
* Gdy ruch sieciowy jest wysoka, rejestruje zmiany może potrwać tooa maksymalnie toodisplay sześciu godzin.
* Jeśli zmodyfikujesz hello konfiguracji, gdy komputer jest wyłączony, hello komputera opublikować zmian pliku, które należały toohello poprzedniej konfiguracji.

## <a name="change-tracking-data-collection-details"></a>Zmień szczegóły kolekcji danych śledzenia
Śledzenie zmian zbiera dane spisu oprogramowania i metadanych usługi Windows hello agentów, które mają włączone.

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla śledzenia zmian.

| Platformy | Bezpośrednie agenta | Agent programu Operations Manager | Agent systemu Linux | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- | --- |
| System Windows i Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minut too50 minut w zależności od typu zmiany hello. Zobacz hello w poniższej tabeli, aby uzyskać więcej informacji. |


Witaj poniższej tabeli przedstawiono częstotliwość zbierania danych hello hello typy zmian.

| **Zmień typ** | **częstotliwość** | **Jest****agenta****wysyłania różnice, jeśli znaleziono?**  |
| --- | --- | --- |
| Rejestr systemu Windows | 50 minut | Nie |
| Plik systemu Windows | 30 minut | Tak. Jeśli nie została zmieniona w ciągu 24 godzin, jest wysyłane migawki. |
| Plik systemu Linux | 15 minut | Tak. Jeśli nie została zmieniona w ciągu 24 godzin, jest wysyłane migawki. |
| Usługi systemu Windows | 30 minut | Tak, co 30 minut, jeśli znaleziono zmian. Co 24 godziny migawki są wysyłane, niezależnie od zmian. Dlatego hello migawki są wysyłane nawet w przypadku, gdy nie wprowadzono żadnych zmian. |
| Demonów systemu Linux | 5 minut | Tak. Jeśli nie została zmieniona w ciągu 24 godzin, jest wysyłane migawki. |
| Oprogramowanie Windows | 30 minut | Tak, co 30 minut, jeśli znaleziono zmian. Co 24 godziny migawki są wysyłane, niezależnie od zmian. Dlatego hello migawki są wysyłane nawet w przypadku, gdy nie wprowadzono żadnych zmian. |
| Oprogramowania w systemie Linux | 5 minut | Tak. Jeśli nie została zmieniona w ciągu 24 godzin, jest wysyłane migawki. |

### <a name="registry-key-change-tracking"></a>Śledzenie zmian klucza rejestru

Analiza dzienników wykonuje rejestru systemu Windows, monitorowanie i śledzenie z hello rozwiązaniu do śledzenia zmian. Celem Hello monitorowania zmian tooregistry kluczy jest toopinpoint punkty rozszerzeń, gdzie można uaktywnić kodu innych firm i złośliwego oprogramowania. następujące Hello listy pokazuje hello domyślne klucze rejestru które są śledzone przez rozwiązanie hello i dlaczego każdego śledzone.

- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Monitory skrypty uruchamiane automatycznie.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Skrypty monitorów Uruchom przy zamykaniu.
- Klucz HKEY\_lokalnego\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Monitoruje klucze, które są ładowane przed hello użytkownik loguje tootheir konta systemu Windows. klucz Hello jest używany dla 32-bitowe programów na komputerach 64-bitowych.
- Klucz HKEY\_lokalnego\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed składników
    - Monitory zmienia ustawienia tooapplication.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Monitory wspólnej autostart wpisów, które przyłączanie się bezpośrednio do Eksploratora Windows i zwykle uruchamiania w procesie z Explorer.exe.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Monitory wspólnej autostart wpisów, które przyłączanie się bezpośrednio do Eksploratora Windows i zwykle uruchamiania w procesie z Explorer.exe.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Monitory wspólnej autostart wpisów, które przyłączanie się bezpośrednio do Eksploratora Windows i zwykle uruchamiania w procesie z Explorer.exe.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitory dla ikony nakładki obsługi rejestracji.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitory dla ikony nakładki rejestracji programu obsługi dla 32-bitowe programów na komputerach 64-bitowych.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser obiekty pomocnicze
    - Monitory nowych wtyczek obiektu pomocnika przeglądarki Internet Explorer. Używane tooaccess hello modelu DOM (Document Object) bieżącej strony i toocontrol nawigacji hello.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser obiekty pomocnicze
    - Monitory nowych wtyczek obiektu pomocnika przeglądarki Internet Explorer. Używane tooaccess hello modelu DOM (Document Object) hello bieżącej strony i toocontrol nawigacji dla 32-bitowe programów na komputerach 64-bitowych.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Monitory dla nowych rozszerzeń programu Internet Explorer, takie jak narzędzie niestandardowe menu i niestandardowe przyciski paska narzędzi.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Monitory dla nowych rozszerzeń programu Internet Explorer, takie jak narzędzie niestandardowe menu i przycisków paska narzędzi niestandardowych dla 32-bitowe programów na komputerach 64-bitowych.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Monitoruje hello 32-bitowe sterowniki skojarzone z wavemapper, wave1 i wave2 msacm.imaadpcm, .msadpcm, .msgsm610 i vidc. Podobne toohello [sterowniki] części hello systemu. Pliku INI.
- Klucz HKEY\_lokalnego\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Monitory hello 32-bitowe sterowniki są skojarzone z wavemapper, wave1 i wave2 msacm.imaadpcm, .msadpcm, .msgsm610 i vidc dla 32-bitowe programów na komputerach 64-bitowych. Podobne toohello [sterowniki] części hello systemu. Pliku INI.
- Klucz HKEY\_lokalnego\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitory hello listę znanych lub często używane systemowej biblioteki dll; Ten system uniemożliwia osób wykorzystania uprawnienia katalogu aplikacji słabe przez usunięcie koń trojański wersji systemowej biblioteki dll.
- Klucz HKEY\_lokalnego\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Lista hello monitoruje powiadomienia o zdarzeniach stanie tooreceive pakiety z usługi Winlogon, hello modelu obsługi interakcyjnego logowania dla systemu operacyjnego Windows hello.


## <a name="use-change-tracking"></a>Użyj śledzenie zmian
Po zainstalowaniu rozwiązania hello hello podsumowanie zmian można wyświetlić dla monitorowanych serwerów przy użyciu hello **śledzenia zmian** Kafelek na powitania **omówienie** strony w OMS.

![Obraz śledzenia zmian kafelka](./media/log-analytics-change-tracking/change-tracking-tile.png)

Można wyświetlić infrastruktury tooyour zmiany, a następnie przejście do szczegółów hello następujące kategorie:

* Zmiany według typu konfiguracji oprogramowania i usług systemu Windows
* Zmiany oprogramowania tooapplications i aktualizacje dla poszczególnych serwerów
* Całkowita liczba zmiany oprogramowania dla każdej aplikacji
* Pakietów systemu Linux
* Zmiany usług systemu Windows dla poszczególnych serwerów
* Zmiany demonów systemu Linux

![Obraz śledzenia zmian pulpitu nawigacyjnego](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![Obraz śledzenia zmian pulpitu nawigacyjnego](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>zmiany tooview dla dowolnego zmianę typu
1. Na powitania **omówienie** kliknij przycisk hello **śledzenia zmian** kafelka.
2. Na powitania **zmienić śledzenia** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z hello zmiany typu bloków, a następnie kliknij jedną tooview szczegółowe informacje o nim w hello **wyszukiwania dziennika** strony.
3. Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania. Można również filtrować według aspekty toonarrow hello wyników.

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane śledzenia zmian.
