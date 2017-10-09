---
title: "aaaOptimize środowiskiem programu System Center Operations Manager na platformie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Możesz użyć hello systemu Center Operations Manager oceny tooassess rozwiązania hello ryzyka i kondycji środowisk serwera w regularnych odstępach czasu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Optymalizuj środowisko z hello rozwiązań System Center Operations Manager oceny (wersja zapoznawcza)

![System Center Operations Manager oceny symbol](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Możesz użyć hello systemu Center Operations Manager oceny tooassess rozwiązania hello ryzyka i kondycji środowisk serwera programu System Center Operations Manager w regularnych odstępach czasu. Ten artykuł pomaga zainstalować, skonfigurować i używać rozwiązania hello, dzięki czemu można wykonać działania naprawcze potencjalnych problemów.

To rozwiązanie zapewnia priorytetową listą zaleceń tooyour określonego wdrożonego serwera infrastruktury. Hello zalecenia są podzielone na cztery fokus, zrozumiałą dla obszarów, które pomagają w szybkim hello ryzyka i podejmowanie działań naprawczych.

Witaj zalecenia są oparte na powitania wiedzy i doświadczenia przez pracownicy firmy Microsoft z tysięcy wizyt klienta. Każde zalecenie znajdują się wskazówki dotyczące przyczyny problemu może być niezależnie od tego, tooyou i jak tooimplement hello sugerowane zmiany.

Można wybrać fokus obszarów, które są najważniejsze tooyour organizacji i śledzić postęp w kierunku uruchomionym środowiskiem ryzyka bezpłatne i działa prawidłowo.

Po dodaniu hello rozwiązania i ocenę jest zakończone, podsumowanie informacji o obszarach zainteresowań jest wyświetlany na powitania **System Center Operations Manager oceny** pulpitu nawigacyjnego dla infrastruktury. Witaj poniższych sekcjach opisano sposób toouse hello informacji na temat hello **System Center Operations Manager oceny** pulpitu nawigacyjnego, gdzie można przeglądać i wykonaj zalecane działania infrastruktury programu SCOM.

![Kafelek rozwiązania programu System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![Pulpit nawigacyjny programu System Center Operations Manager oceny](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania

rozwiązanie Hello współpracuje z programu Microsoft System Operations Manager 2012 R2 i 2012 z dodatkiem SP1.

Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

 - Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie hello. Zainstaluj hello rozwiązanie z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) lub wykonując instrukcje hello w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

 - Po dodaniu obszar roboczy toohello rozwiązania hello, hello System Center Operations Manager oceny kafelka na pulpicie nawigacyjnym hello wyświetla komunikat wymagana dodatkowa konfiguracja hello. Kliknij Kafelek hello i wykonaj kroki konfiguracji hello wymienione na stronie powitania

 ![Kafelka pulpitu nawigacyjnego programu System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Konfiguracja hello System Center Operations Manager może odbywać się za pośrednictwem skryptu hello wykonując kroki hello wspomnianego hello strony konfiguracji rozwiązania hello w OMS.

 Zamiast tego oceny hello tooconfigure za pośrednictwem konsoli programu SCOM, hello wykonaj poniższe kroki opisane w temacie hello sam kolejności
1. [Ustaw konto Uruchom jako hello System Center Operations Manager oceny](#operations-manager-run-as-accounts-for-oms)  
2. [Skonfiguruj regułę System Center Operations Manager oceny hello](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Szczegóły danych oceny System Center Operations Manager w kolekcji

Hello oceny programu System Center Operations Manager umożliwia zbieranie danych usługi WMI, rejestru danych, danych dziennika zdarzeń, danych programu Operations Manager za pomocą środowiska Windows PowerShell, zapytania SQL, moduł zbierający informacje o pliku przy użyciu serwera hello, która została włączona.

Witaj poniższej tabeli przedstawiono metody kolekcji danych System Center Operations Manager oceny i jak często dane są zbierane przez agenta.

| Platformy | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | 7 dni |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Uruchom jako konta programu Operations Manager dla OMS

Kompilacje OMS od pakietów administracyjnych dla obciążeń tooprovide wartość — Dodawanie usług. Pakiety administracyjne toorun uprawnienia specyficznego dla obciążenia w innym kontekście zabezpieczeń, takie jak konto domeny wymaga poszczególnych obciążeń. Skonfiguruj Operations Manager uruchom jako konta tooprovide informacji o poświadczeniach.

Użyj następujących informacji tooset hello konto Uruchom jako programu Operations Manager dla System Center Operations Manager oceny hello.

### <a name="set-hello-run-as-account"></a>Zestaw hello konta Uruchom jako

1. W hello konsola programu Operations Manager, przejdź do pozycji toohello **administracji** kartę.
2. W obszarze hello **Konfiguracja Uruchom jako**, kliknij przycisk **kont**.
3. Utwórz konto Uruchom jako, po za pomocą Kreatora tworzenia konta systemu Windows hello hello. toouse konta Hello jest hello jedną zidentyfikowane i posiadające wszystkie wymagania wstępne hello poniżej:

    >[!NOTE]
    Hello konta Uruchom jako musi spełniać następujące wymagania:
    - Element członkowski konta domeny hello lokalnej grupy Administratorzy na wszystkich serwerach w środowisku hello (wszystkie operacje menedżera ról — Serwer zarządzania, bazy danych programu Operations Manager, Magazyn danych raportowania, konsoli sieci Web, bramy)
    - Rola administratora menedżera operacji dla grupy zarządzania hello oceniane
    - Wykonanie hello [skryptu](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant szczegółowe uprawnienia toohello konta w wystąpieniu programu SQL używane przez program Operations Manager.
      Uwaga: Jeśli to konto ma już uprawnienia administratora systemu, następnie przejdź hello wykonywanie skryptu.

4. W obszarze **zabezpieczenia dystrybucji**, wybierz pozycję **bezpieczniejsze**.
5. Określ serwer zarządzania hello, które jest dystrybuowane hello konta.
3. Przejdź wstecz toohello Konfiguracja Uruchom jako, a następnie kliknij przycisk **profile**.
4. Wyszukaj hello *SCOM oceny profilu*.
5. Nazwa profilu Hello powinny być: *programu Microsoft System Center Advisor SCOM oceny profilu Uruchom jako*.
6. Kliknij prawym przyciskiem myszy i zaktualizuj jego właściwości i dodać hello ostatnio utworzone konto Uruchom jako utworzonego w kroku 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL skryptu toogrant szczegółowe uprawnienia toohello konta Uruchom jako

Wykonanie powitania po SQL skryptu toogrant wymagane uprawnienia toohello konta Uruchom jako na powitania wystąpienia serwera SQL używane przez program Operations Manager.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Skonfiguruj regułę oceny hello

System Center Operations Manager oceny rozwiązania pakiet administracyjny zawiera reguły o nazwie Hello *Microsoft System Center Advisor SCOM oceny Uruchom oceny reguły*. Ta reguła jest odpowiedzialna za uruchamianie hello oceny wydajności. tooenable hello reguły i skonfigurować częstotliwość hello, użyj poniższych procedur hello.

Domyślnie program hello Microsoft System Center Advisor SCOM oceny Uruchom oceny reguły jest wyłączona. oceny hello toorun, należy włączyć regułę hello na serwerze zarządzania. Użyj hello następujące kroki.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Włącz regułę powitania serwera zarządzania określonymi

1. W hello **tworzenie** obszaru roboczego w konsoli programu Operations Manager hello, wyszukaj regułę hello *Microsoft System Center Advisor SCOM oceny Uruchom oceny reguły* w hello **reguły** okienka.
2. W wynikach wyszukiwania hello, wybierz hello zawierającej tekst hello *typu: serwer zarządzania*.
3. Kliknij prawym przyciskiem myszy hello reguły, a następnie kliknij przycisk **zastępuje** > **dla konkretnego obiektu klasy: serwer zarządzania**.
4.  Na liście serwerów zarządzania dostępnych hello wybierz serwer zarządzania hello, gdzie reguła hello powinno być ono uruchomione.
5.  Upewnij się, zmień wartość zastępcza zbyt**True** dla hello **włączone** wartość parametru.  
    ![zastąpienie parametru](./media/log-analytics-scom-assessment/rule.png)

Nadal w tym oknie można skonfigurować częstotliwość hello hello uruchomić przy użyciu hello następnej procedury.

#### <a name="configure-hello-run-frequency"></a>Skonfiguruj częstotliwość uruchamiania hello

Ocena Hello jest skonfigurowany toorun co 10 080 minut (lub siedem dni), hello domyślny interwał. Można zastąpić wartość minimalna tooa wartość hello 1440 minut (lub jeden dzień). wartość Hello reprezentuje hello minimalny czas przerwy między oszacowanie działa. Interwał powitania toooverride, użyj hello kroki opisane poniżej.

1. W hello **tworzenie** obszaru roboczego w konsoli programu Operations Manager hello, wyszukaj regułę hello *Microsoft System Center Advisor SCOM oceny Uruchom oceny reguły* w hello **reguły** okienka.
2. W wynikach wyszukiwania hello, wybierz hello zawierającej tekst hello *typu: serwer zarządzania*.
3. Kliknij prawym przyciskiem myszy hello reguły, a następnie kliknij przycisk **hello zastąpienie reguły** > **dla wszystkich obiektów klasy: serwer zarządzania**.
4. Zmień hello **interwał** tooyour wartość parametru Żądana wartość interwału. W poniższym przykładzie hello hello wartość jest ustawiana too1440 minut (jeden dzień).  
    ![Parametr interwał](./media/log-analytics-scom-assessment/interval.png)  
    Jeśli wartość hello ustawiono tooless od 1440 minut, hello reguła jest uruchamiana w odstępach czasu w ciągu jednego dnia. W tym przykładzie reguły hello ignoruje wartość interwału hello i jest uruchamiany z częstotliwością jeden dzień.


## <a name="understanding-how-recommendations-are-prioritized"></a>Opis sposobu mają pierwszeństwo zalecenia

Każdy zalecenia otrzymuje wartość wagi, która identyfikuje hello względnego hello zalecenia. Wyświetlane są tylko zalecenia najważniejszych hello 10.

### <a name="how-weights-are-calculated"></a>Jak są obliczane wagi

Wagi są wartości zagregowanych oparte na trzech kluczowych czynników:

- Witaj *prawdopodobieństwo* czy problemu może powodować problemy. Większe prawdopodobieństwo oznacza większe ogólny wynik tooa rekomendację hello.
- Witaj *wpływ* wydania hello w Twojej organizacji, jeśli spowodować problem. Większy wpływ oznacza większe ogólny wynik tooa rekomendację hello.
- Witaj *nakładu* wymagane tooimplement hello zalecenia. Wyższy nakładu pracy oznacza tooa mniejszych ogólny wynik dla hello zalecenia.

Witaj wag każde zalecenie jest wyrażona jako procent hello łącznym wynikiem dostępne dla każdego obszaru fokus. Na przykład jeśli zalecenia w hello obszaru fokus dostępność i ciągłość prowadzenia działalności biznesowej ma wynik % 5, wdrażanie tego zalecenia zwiększa z ogólną % wynik przez 5 dostępność i ciągłość prowadzenia działalności biznesowej.

### <a name="focus-areas"></a>Obszarach zainteresowań

**Dostępność i ciągłość prowadzenia działalności biznesowej** — w tym obszarze fokus zawiera zalecenia dotyczące odporności infrastruktury i ochronę biznesowej, dostępności usług.

**Wydajność i skalowalność** — ten obszar fokus zawiera zalecenia dotyczące toohelp organizacji infrastruktury IT zwiększania, sprawdź, czy spełnia bieżące wymagania dotyczące wydajności środowiska informatycznego i jest w stanie toorespond toochanging wymaga infrastruktury.

**Uaktualnienie, migrację i wdrażanie** — toohelp zalecenia dotyczące uaktualniania zawiera ten obszar fokus, migrację i wdrażanie programu SQL Server tooyour istniejącej infrastruktury.

**Operacje i monitorowanie** — w tym obszarze fokus zawiera zalecenia dotyczące usprawnienia toohelp operacji IT, zaimplementować program prewencyjnej konserwacji i zmaksymalizować wydajność.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Należy należy dążyć tooscore 100% w każdym obszarze fokus?

Niekoniecznie. zalecenia Hello są oparte na powitania wiedzy i doświadczeń zdobytych Microsoft inżynierowie między tysięcy wizyt klienta. Jednak nie infrastruktury serwerowe są hello takie same i szczegółowe zalecenia mogą być bardziej lub mniej istotne tooyou. Na przykład niektóre zalecenia dotyczące zabezpieczeń może być mniej istotne, jeśli maszyny wirtualne nie są uwidocznione toohello Internet. Kilka zaleceń dostępności może być mniej istotne dla usług, które umożliwiają zbieranie danych ad hoc — niski priorytet i raportowania. Problemy, które są ważne tooa dojrzałe firm może być mniej ważne tooa rozruchu. Może mają tooidentify obszarach zainteresowań, które są zebranych i przyjrzyj się jak zmienić wyniki wraz z upływem czasu.

Każdy zalecenie obejmuje wskazówek dotyczących Dlaczego ważne jest. Za pomocą tego tooevaluate wskazówki czy wdrażanie zalecenie hello jest odpowiednie dla Ciebie, charakter hello IT usługi i hello potrzeby biznesowe danej organizacji.

## <a name="use-assessment-focus-area-recommendations"></a>Użyj zaleceń obszaru fokus oceny

Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie hello. tooread więcej na temat instalowania rozwiązań, zobacz [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Po jego zainstalowaniu, można wyświetlić podsumowanie hello zalecenia za pomocą kafelka System Center Operations Manager oceny hello na stronie Przegląd hello OMS.

Witaj w widoku Podsumowanie oceny zgodności dla Twojej infrastruktury, a następnie wejdź do zalecenia.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview zalecenia dotyczące fokus obszaru i podejmij akcję korekcyjną

1. Na powitania **omówienie** kliknij przycisk hello **System Center Operations Manager oceny** kafelka.
2. Na powitania **System Center Operations Manager oceny** strony, przejrzyj hello informacje podsumowania w jednym z bloków obszaru fokus hello, a następnie kliknij jedną tooview zalecenia dla tego obszaru fokus.
3. Na dowolnym hello fokus obszaru stron można wyświetlić hello priorytety zalecenia dla danego środowiska. Kliknij zalecenie, w obszarze **dotyczy obiektów** tooview szczegółowych informacji o Dlaczego hello tworzone są zalecenia.  
    ![obszar fokus](./media/log-analytics-scom-assessment/focus-area.png)
4. Należy wykonać działania naprawcze sugerowane w **sugerowanych akcji**. Gdy element hello został rozwiązany, ocen nowsze zarejestruje które zalecane akcje zostały pobrane i zwiększa wynik zgodności. Poprawione elementy są wyświetlane jako **przekazany obiektów**.

## <a name="ignore-recommendations"></a>Ignoruj zalecenia

Jeśli masz zaleceń, które mają tooignore, można utworzyć pliku tekstowego, który korzysta z pakietu OMS tooprevent zaleceń znajdujących się w wynikach oceny.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>tooidentify zaleceń, które mają tooignore

1. Zaloguj się w obszarze roboczym tooyour i Otwórz dziennik wyszukiwania. Użyj hello następujące zalecenia toolist zapytania, które nie powiodły się na komputerach w danym środowisku.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Poniżej przedstawiono zrzut ekranu przedstawiający hello dziennik wyszukiwania:  
    ![przeszukiwanie dzienników](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Wybierz, które mają tooignore zalecenia. Użyjesz wartości hello RecommendationId w następnej procedurze hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate i użyj pliku tekstowego IgnoreRecommendations.txt

1. Utwórz plik o nazwie IgnoreRecommendations.txt.
2. Wklej lub wpisz każdego RecommendationId dla każde zalecenie ma tooignore OMS w osobnym wierszu, a następnie zapisz i zamknij plik hello.
3. Umieść plik hello w hello następującego folderu na każdym komputerze miejscu zalecenia tooignore OMS.
4. Na serwerze zarządzania programu Operations Manager hello - *SystemDrive*: System Center 2012 R2\Operations Manager\Server \Program Files\Microsoft.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify, że zalecenia są ignorowane

1. Po uruchomieniu hello następnej zaplanowanej oceny domyślnie co siedem dni hello określone zalecenia są oznaczone ignorowany i nie będą wyświetlane na pulpicie nawigacyjnym oceny hello.
2. Możesz użyć powitania po toolist zapytania wyszukiwania dziennika wszystkie zalecenia hello ignorowane.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Jeśli później zdecydujesz, które mają toosee zignorowane zalecenia, Usuń wszystkie pliki IgnoreRecommendations.txt lub RecommendationIDs można usunąć z nich.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>System Center Operations Manager oceny rozwiązania — często zadawane pytania

*Po dodaniu obszar roboczy OMS toomy hello oceny rozwiązania. Nie widzę hello zalecenia. Dlaczego nie?* Po dodaniu hello rozwiązania, użyj hello następujące zalecenia hello widoku czynności na pulpicie nawigacyjnym OMS hello.  

- [Ustaw konto Uruchom jako hello System Center Operations Manager oceny](#operations-manager-run-as-accounts-for-oms)  
- [Skonfiguruj regułę System Center Operations Manager oceny hello](#configure-the-assessment-rule)


*Czy istnieje sposób tooconfigure częstotliwość oceny hello działa?* Tak. Zobacz [hello skonfiguruj częstotliwość uruchamiania](#configure-the-run-frequency).

*Jeśli inny serwer zostanie odnaleziony po rozwiązań System Center Operations Manager oceny hello zostały dodane, zostanie on oceniane?* Tak, po odnajdywaniu, ocenia się od — domyślnie co siedem dni.

*Co to jest nazwa hello procesu hello hello zbierania danych?* AdvisorAssessment.exe

*Gdzie jest uruchamiany proces AdvisorAssessment.exe hello?* AdvisorAssessment.exe uruchamiana hello usługi kondycji serwera zarządzania hello, gdzie reguła oceny hello jest włączona. Za pomocą tego procesu, odnajdywania całego środowiska odbywa się za pośrednictwem zdalne zbieranie danych.

*Jak długo trwa zbierania danych?* Zbieranie danych na serwerze hello trwa około jednej godziny. Może trwać dłużej w środowiskach mających wiele wystąpień programu Operations Manager lub baz danych.

*Co zrobić, jeśli ustawić interwał hello tooless oceny powitania od 1440 minut?*  oceny hello jest wstępnie skonfigurowane toorun maksymalnie raz dziennie. Jeśli zastąpić wartość tooa wartość interwału hello mniej niż 1440 minut, następnie oceny hello używa 1440 minut jako wartość interwału hello.

*Jak tooknow, jeśli występują błędy wstępnych?* Nie widzisz wyniki oceny hello został uruchomiony, następnie jest prawdopodobne, że niektóre wymagania wstępne hello w celu oceny hello nie powiodło się. Można wykonać zapytania: `Type=Operation Solution=SCOMAssessment` i `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` hello toosee wyszukiwania dziennika nie powiodło się wymagania wstępne.

*Brak `Failed tooconnect toohello SQL Instance (….).` komunikat wstępnych błędy. Co to jest problem hello?* AdvisorAssessment.exe, proces hello, która gromadzi dane, jest uruchamiana hello usługi kondycji serwera zarządzania hello. W ramach oceny hello proces hello prób toohello tooconnect programu SQL Server, gdzie bazy danych programu Operations Manager hello jest obecny. Ten błąd może wystąpić, gdy wystąpienie programu SQL Server toohello połączenia hello zablokować reguł zapory.

*Jakiego typu dane są zbierane?*  hello następujące typy danych są zbierane: danych programu Operations Manager — dane usługi WMI — rejestru danych — dane w dzienniku zdarzeń — za pośrednictwem plików, zapytania SQL i programu Windows PowerShell moduł zbierający informacje o.

*Dlaczego ma tooconfigure konto Uruchom jako?* W przypadku serwera programu Operations Manager są uruchamiane różne zapytania SQL. Aby je toorun, należy użyć konto Uruchom jako z niezbędne uprawnienia. Ponadto poświadczenia administratora lokalnego są wymagane tooquery WMI.

*Dlaczego są wyświetlane tylko zalecenia 10 pierwszych hello?* Zamiast daje wyczerpująca, utrudnione listę zadań, zaleca się skupić się na najpierw adresowania hello priorytety zalecenia. Po adresu im dodatkowe zalecenia staną się dostępne. Jeśli wolisz toosee hello szczegółową listę, można wyświetlić wszystkie zalecenia za pomocą wyszukiwania dziennika.

*Istnieje już tooignore sposób zalecenia?* Tak, zobacz hello [zignorowanie zalecenia](#Ignore-recommendations).


## <a name="next-steps"></a>Następne kroki

- [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowych danych System Center Operations Manager oceny i zalecenia.
