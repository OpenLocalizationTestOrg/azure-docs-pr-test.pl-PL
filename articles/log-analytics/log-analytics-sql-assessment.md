---
title: "aaaOptimize środowiskiem programu SQL Server na platformie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Z usługi Analiza dzienników Azure możesz użyć hello oceny SQL tooassess rozwiązania hello ryzyka i kondycji środowisk programu SQL server w regularnych odstępach czasu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Optymalizuj środowisko programu SQL Server z hello oceny SQL rozwiązania analizy dzienników

![Symbol oceny SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Możesz użyć hello oceny SQL tooassess rozwiązania hello ryzyka i kondycji środowisk serwera w regularnych odstępach czasu. Ten artykuł pomoże Ci zainstalować rozwiązanie hello tak, aby można podjąć działania naprawcze potencjalnych problemów.

To rozwiązanie zapewnia priorytetową listą zaleceń tooyour określonego wdrożonego serwera infrastruktury. Hello zalecenia są podzielone na sześć fokus, zrozumiałą dla obszarów, które pomagają w szybkim hello ryzyka i podejmowanie działań naprawczych.

Witaj zalecenia są oparte na powitania wiedzy i doświadczenia przez pracownicy firmy Microsoft z tysięcy wizyt klienta. Każde zalecenie znajdują się wskazówki dotyczące przyczyny problemu może być niezależnie od tego, tooyou i jak tooimplement hello sugerowane zmiany.

Można wybrać fokus obszarów, które są najważniejsze tooyour organizacji i śledzić postęp w kierunku uruchomionym środowiskiem ryzyka bezpłatne i działa prawidłowo.

Po dodaniu hello rozwiązania i ocenę jest zakończone, podsumowanie informacji o obszarach zainteresowań jest wyświetlany na powitania **oceny SQL** pulpitu nawigacyjnego dla infrastruktury hello w danym środowisku. Witaj poniższych sekcjach opisano sposób toouse hello informacji na temat hello **oceny SQL** pulpitu nawigacyjnego, gdzie można przeglądać i wykonaj zalecane akcje dotyczące infrastruktury serwera SQL.

![Obraz kafelka oceny SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![Obraz pulpitu nawigacyjnego oceny SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Ocena SQL współpracuje z wszystkich aktualnie obsługiwanych wersjach programu SQL Server dla hello wersje Standard, Developer i Enterprise.

Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

* Agenci musi być zainstalowany na serwerach, które mają zainstalowany program SQL Server.
* Witaj rozwiązanie do oceny SQL wymaga obsługiwanej wersji programu .NET Framework 4 zainstalowane na każdym komputerze, na którym agent pakietu OMS.
* W rozwiązaniu hello tooinstall kolejności użytkownik hello musi być administratorem lub współautora toohello subskrypcji platformy Azure przy użyciu hello portalu Azure. Ponadto hello użytkownik musi być członkiem hello OMS obszaru roboczego współautora lub administrator roli w portalu OMS hello.
* Jeśli agent programu Operations Manager hello z SQL do oceny, konieczne będzie toouse konta programu Operations Manager Run-As. Zobacz [konta programu Operations Manager, Uruchom jako dla OMS](#operations-manager-run-as-accounts-for-oms) poniżej Aby uzyskać więcej informacji.

  > [!NOTE]
  > Hello MMA agent nie obsługuje programu Operations Manager Run-As kont.
  >
  >
* Dodaj tooyour rozwiązania oceny SQL hello obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Nie są wymagane żadne dalsze czynności konfiguracyjne.

> [!NOTE]
> Po dodaniu rozwiązania hello hello AdvisorAssessment.exe plik zostanie dodany tooservers z agentami. Dane konfiguracji jest do odczytu i następnie wysyłane toohello usługę w chmurze hello do przetwarzania. Logika jest stosowane toohello odebranych danych i usługi w chmurze hello rejestruje dane hello.

## <a name="sql-assessment-data-collection-details"></a>Szczegóły pobierania danych SQL do oceny
Ocena SQL służy do zbierania danych usługi WMI, dane rejestru dane dotyczące wydajności i wyników widoku dynamicznego zarządzania programu SQL Server za pomocą hello agentów, które mają włączone.

Witaj poniższej tabeli przedstawiono metody zbierania danych dla agentów, czy Operations Manager (SCOM) jest wymagany i jak często dane są zbierane przez agenta.

| Platformy | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 dni |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Uruchom jako konta programu Operations Manager dla OMS
Analiza dzienników w OMS używa hello agenta programu Operations Manager i toocollect grupy zarządzania i wysyłać dane toohello usługę. Kompilacje OMS na pakiety administracyjne dla obciążeń tooprovide wartość — Dodawanie usług. Pakiety administracyjne toorun uprawnienia specyficznego dla obciążenia w innym kontekście zabezpieczeń, takie jak konto domeny wymaga poszczególnych obciążeń. Potrzebujesz informacji o poświadczeniach tooprovide przez skonfigurowanie konta Operations Manager uruchom jako.

Użyj hello następujące informacje tooset hello programu Operations Manager konto Uruchom jako w celu oceny SQL.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Ustaw hello konta Uruchom jako w celu oceny SQL
 Jeśli korzystasz już z hello pakiet administracyjny programu SQL Server, należy użyć tego konta Uruchom jako.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>Witaj tooconfigure konta Uruchom jako SQL w konsoli operacje hello
> [!NOTE]
> Jeśli używasz hello OMS bezpośrednio agenta, a nie hello agenta programu SCOM, pakiet administracyjny hello zawsze działa w kontekście zabezpieczeń hello hello lokalnego konta systemowego. Pomiń kroki 1 – 5 poniżej i uruchom hello albo próbki T-SQL lub programu Powershell określającego NT AUTHORITY\SYSTEM jako hello nazwy użytkownika.
>
>

1. W programie Operations Manager, otwórz konsolę operacje hello, a następnie kliknij przycisk **administracji**.
2. W obszarze **Konfiguracja Uruchom jako**, kliknij przycisk **profile**i Otwórz **OMS SQL oceny profilu Uruchom jako**.
3. Na powitania **konta Uruchom jako** kliknij przycisk **Dodaj**.
4. Wybierz konto systemu Windows uruchom jako, które zawiera poświadczenia hello wymagane dla programu SQL Server, lub kliknij przycisk **nowy** toocreate jeden.

   > [!NOTE]
   > Witaj typ konta Uruchom jako musi być systemu Windows. Witaj konta Uruchom jako musi być również częścią lokalnej grupy administratorów na wszystkich serwerach systemu Windows obsługującego wystąpienia programu SQL Server.
   >
   >
5. Kliknij pozycję **Zapisz**.
6. Modyfikuj, a następnie wykonaj hello następujące przykładowe T-SQL w każdej wystąpienie programu SQL Server toogrant minimalne uprawnienia wymagane tooRun tooperform jako konto programu SQL do oceny. Jednak nie toodo to konieczne, jeśli konto Uruchom jako jest już częścią roli serwera sysadmin hello na wystąpienia programu SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>Witaj tooconfigure SQL Uruchom jako konta przy użyciu programu Windows PowerShell
Otwórz okno programu PowerShell i uruchom hello następującego skryptu po zaktualizowaniu z informacjami:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Opis sposobu mają pierwszeństwo zalecenia
Każdy zalecenia otrzymuje wartość wagi, która identyfikuje hello względnego hello zalecenia. Wyświetlane są tylko hello 10 najważniejszych zalecenia.

### <a name="how-weights-are-calculated"></a>Jak są obliczane wagi
Wagi są wartości zagregowanych oparte na trzech kluczowych czynników:

* Witaj *prawdopodobieństwo* czy problemu może powodować problemy. Większe prawdopodobieństwo oznacza większe ogólny wynik tooa rekomendację hello.
* Witaj *wpływ* wydania hello w Twojej organizacji, jeśli spowodować problem. Większy wpływ oznacza większe ogólny wynik tooa rekomendację hello.
* Witaj *nakładu* wymagane tooimplement hello zalecenia. Wyższy nakładu pracy oznacza tooa mniejszych ogólny wynik dla hello zalecenia.

Witaj wag każde zalecenie jest wyrażona jako procent hello łącznym wynikiem dostępne dla każdego obszaru fokus. Na przykład jeśli zalecenia w hello zabezpieczeń i zgodności fokus obszaru ma wynik % 5, wdrażanie tego zalecenia spowoduje zwiększenie ogólnej % wynik przez 5 zabezpieczeń i zgodności.

### <a name="focus-areas"></a>Obszarach zainteresowań
**Zabezpieczeń i zgodności** — w tym obszarze fokus zawiera zalecenia dotyczące potencjalnego zagrożenia bezpieczeństwa i naruszeń, zasad firmowych i wymagania techniczne, prawne i przepisami zgodności.

**Dostępność i ciągłość prowadzenia działalności biznesowej** — w tym obszarze fokus zawiera zalecenia dotyczące odporności infrastruktury i ochronę biznesowej, dostępności usług.

**Wydajność i skalowalność** — ten obszar fokus zawiera zalecenia dotyczące toohelp organizacji infrastruktury IT zwiększania, sprawdź, czy spełnia bieżące wymagania dotyczące wydajności środowiska informatycznego i jest w stanie toorespond toochanging wymaga infrastruktury.

**Uaktualniania, wdrażania i migracji** — toohelp zalecenia dotyczące uaktualniania zawiera ten obszar fokus, migrację i wdrażanie programu SQL Server tooyour istniejącej infrastruktury.

**Operacje i monitorowanie** — w tym obszarze fokus zawiera zalecenia dotyczące usprawnienia toohelp operacji IT, zaimplementować program prewencyjnej konserwacji i zmaksymalizować wydajność.

**Zarządzanie zmianami i konfiguracją** — w tym obszarze fokus zawiera zalecenia dotyczące toohelp Chroń bieżącą działalność, upewnij się, że zmiany negatywnie nie mają wpływ na infrastrukturę, ustal procedury sterowania zmianami i tootrack i inspekcji konfiguracje systemu.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Należy należy dążyć tooscore 100% w każdym obszarze fokus?
Niekoniecznie. zalecenia Hello są oparte na powitania wiedzy i doświadczeń zdobytych Microsoft inżynierowie między tysięcy wizyt klienta. Jednak nie infrastruktury serwerowe są hello takie same i szczegółowe zalecenia mogą być bardziej lub mniej istotne tooyou. Na przykład niektóre zalecenia dotyczące zabezpieczeń może być mniej istotne, jeśli maszyny wirtualne nie są uwidocznione toohello Internet. Kilka zaleceń dostępności może być mniej istotne dla usług, które umożliwiają zbieranie danych ad hoc — niski priorytet i raportowania. Problemy, które są ważne tooa dojrzałe firm może być mniej ważne tooa rozruchu. Może mają tooidentify obszarach zainteresowań, które są zebranych i przyjrzyj się jak zmienić wyniki wraz z upływem czasu.

Każdy zalecenie obejmuje wskazówek dotyczących Dlaczego ważne jest. Należy użyć tego tooevaluate wskazówki czy wdrażanie zalecenie hello jest odpowiednie dla Ciebie, charakter hello IT usługi i hello potrzeby biznesowe danej organizacji.

## <a name="use-assessment-focus-area-recommendations"></a>Użyj zaleceń obszaru fokus oceny
Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie hello. tooread więcej na temat instalowania rozwiązań, zobacz [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Po jego zainstalowaniu, można wyświetlić podsumowanie hello zalecenia za pomocą kafelka oceny SQL hello na stronie Przegląd hello OMS.

Witaj w widoku Podsumowanie oceny zgodności dla Twojej infrastruktury, a następnie wejdź do zalecenia.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview zalecenia dotyczące fokus obszaru i podejmij akcję korekcyjną
1. Na powitania **omówienie** kliknij przycisk hello **oceny SQL** kafelka.
2. Na powitania **oceny SQL** strony, przejrzyj hello informacje podsumowania w jednym z bloków obszaru fokus hello, a następnie kliknij jedną tooview zalecenia dla tego obszaru fokus.
3. Na dowolnym hello fokus obszaru stron można wyświetlić hello priorytety zalecenia dla danego środowiska. Kliknij zalecenie, w obszarze **dotyczy obiektów** tooview szczegółowych informacji o Dlaczego hello tworzone są zalecenia.  
    ![Obraz zalecenia oceny SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. Należy wykonać działania naprawcze sugerowane w **sugerowanych akcji**. Gdy element hello został rozwiązany, ocen nowsze zarejestruje które zalecane akcje zostały pobrane i zwiększa wynik zgodności. Poprawione elementy są wyświetlane jako **przekazany obiektów**.

## <a name="ignore-recommendations"></a>Ignoruj zalecenia
Jeśli masz zaleceń, które mają tooignore, można utworzyć plik tekstowy, który będzie używany przez OMS tooprevent zaleceń znajdujących się w wynikach oceny.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>zalecenia dotyczące tooidentify, które będzie ignorować
1. Zaloguj się w obszarze roboczym tooyour i Otwórz dziennik wyszukiwania. Użyj hello następujące zalecenia toolist zapytania, które nie powiodły się na komputerach w danym środowisku.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Poniżej przedstawiono zrzut ekranu przedstawiający hello dziennik wyszukiwania: ![nie powiodło się zalecenia](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Wybierz, które mają tooignore zalecenia. Użyjesz wartości hello RecommendationId w następnej procedurze hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate i użyj pliku tekstowego IgnoreRecommendations.txt
1. Utwórz plik o nazwie IgnoreRecommendations.txt.
2. Wklej lub wpisz każdego RecommendationId dla każde zalecenie ma tooignore OMS w osobnym wierszu, a następnie zapisz i zamknij plik hello.
3. Umieść plik hello w hello następującego folderu na każdym komputerze miejscu zalecenia tooignore OMS.
   * Na komputerach z usługą Microsoft Monitoring Agent (połączony bezpośrednio lub za pośrednictwem programu Operations Manager) - hello *SystemDrive*: \Program Files\Microsoft Agent\Agent monitorowania
   * Na serwerze zarządzania programu Operations Manager hello - *SystemDrive*: System Center 2012 R2\Operations Manager\Server \Program Files\Microsoft

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify, że zalecenia są ignorowane
1. Po uruchomieniu hello następnej zaplanowanej oceny domyślnie co 7 dni hello określone zalecenia są oznaczone ignorowany i nie będą wyświetlane na pulpicie nawigacyjnym oceny hello.
2. Możesz użyć powitania po toolist zapytania wyszukiwania dziennika wszystkie zalecenia hello ignorowane.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Jeśli później zdecydujesz, które mają toosee zignorowane zalecenia, Usuń wszystkie pliki IgnoreRecommendations.txt lub RecommendationIDs można usunąć z nich.

## <a name="sql-assessment-solution-faq"></a>Rozwiązanie do oceny SQL — często zadawane pytania
*Częstotliwość oceny, czy działa?*

* Ocena Hello jest uruchamiane co 7 dni.

*Czy istnieje sposób tooconfigure częstotliwość oceny hello działa?*

* Nie w tej chwili.

*Jeśli inny serwer zostanie odnaleziony po hello rozwiązanie SQL do oceny zostały dodane, zostanie on oceniane?*

* Tak, gdy okaże się, że jest oceniane z następnie, co 7 dni.

*Jeśli serwer jest likwidowany, gdy zostanie ono zostać usunięte z hello oceny?*

* Jeśli serwer nie przedstawi danych do 3 tygodni, zostanie ono usunięte.

*Co to jest nazwa hello procesu hello hello zbierania danych?*

* AdvisorAssessment.exe

*Jak długo trwa toobe dane zbierane?*

* Hello zbierania danych rzeczywistych na powitania serwera trwa około 1 godziny. Może trwać dłużej na serwerach, które mają wiele wystąpień programu SQL lub bazy danych.

*Jakiego typu dane są zbierane?*

* zbierane są następujące typy danych Hello:
  * USŁUGI WMI
  * Rejestru
  * Liczniki wydajności
  * SQL dynamicznych widoków zarządzania (DMV).

*Istnieje już tooconfigure sposób podczas zbierania danych?*

* Nie w tej chwili.

*Dlaczego ma tooconfigure konto Uruchom jako?*

* Dla programu SQL Server są uruchamiane niewielkiej liczby zapytania SQL. Aby je toorun, konto Uruchom jako z tooSQL uprawnienia VIEW SERVER STATE musi być używany.  Ponadto w kolejności tooquery WMI, wymagane są poświadczenia administratora lokalnego.

*Dlaczego są wyświetlane tylko zalecenia 10 pierwszych hello?*

* Zamiast daje utrudnione kompletnej zadań, zaleca się skupić się na najpierw adresowania hello priorytety zalecenia. Po adresu im dodatkowe zalecenia staną się dostępne. Jeśli wolisz toosee hello szczegółową listę, można wyświetlić wszystkie zalecenia w wyszukiwaniu hello OMS dziennika.

*Istnieje już tooignore sposób zalecenia?*

* Tak, zobacz [zignorowanie zalecenia](#ignore-recommendations) powyższej sekcji.

## <a name="next-steps"></a>Następne kroki
* [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowych danych SQL do oceny i zalecenia.
