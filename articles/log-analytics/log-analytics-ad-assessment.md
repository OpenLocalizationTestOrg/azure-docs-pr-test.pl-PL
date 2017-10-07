---
title: "aaaOptimize środowiskiem usługi Active Directory na platformie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Możesz użyć hello Active oceny katalogu rozwiązania tooassess hello ryzyka i kondycji środowisk serwera w regularnych odstępach czasu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Optymalizowanie środowiska usługi Active Directory z hello oceny usługi Active Directory rozwiązania analizy dzienników

![Symbol oceny usługi AD](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Możesz użyć hello Active oceny katalogu rozwiązania tooassess hello ryzyka i kondycji środowisk serwera w regularnych odstępach czasu. Ten artykuł pomaga zainstalować i używać rozwiązania hello, dzięki czemu można wykonać działania naprawcze potencjalnych problemów.

To rozwiązanie zapewnia priorytetową listą zaleceń tooyour określonego wdrożonego serwera infrastruktury. Hello zalecenia są podzielone na cztery fokus, zrozumiałą dla obszarów, które pomagają w szybkim hello ryzyka i podejmij akcję.

zalecenia Hello są oparte na powitania wiedzy i doświadczenia przez pracownicy firmy Microsoft z tysięcy wizyt klienta. Każde zalecenie znajdują się wskazówki dotyczące przyczyny problemu może być niezależnie od tego, tooyou i jak tooimplement hello sugerowane zmiany.

Można wybrać fokus obszarów, które są najważniejsze tooyour organizacji i śledzić postęp w kierunku uruchomionym środowiskiem ryzyka bezpłatne i działa prawidłowo.

Po dodaniu hello rozwiązania i ocenę jest zakończone, podsumowanie informacji o obszarach zainteresowań jest wyświetlany na powitania **oceny AD** pulpitu nawigacyjnego dla infrastruktury hello w danym środowisku. Witaj poniższych sekcjach opisano sposób toouse hello informacji na temat hello **oceny AD** pulpitu nawigacyjnego, gdzie można przeglądać i wykonaj zalecane akcje dotyczące infrastruktury serwera usługi Active Directory.

![Obraz kafelka oceny SQL](./media/log-analytics-ad-assessment/ad-tile.png)

![Obraz pulpitu nawigacyjnego oceny SQL](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

* Agenci musi być zainstalowany na kontrolery domeny, które są członkami toobe domeny hello obliczone.
* Witaj Active Directory oceny, rozwiązanie wymaga obsługiwanej wersji programu .NET Framework 4 (4.5.2 lub nowszej) zainstalowane na każdym komputerze, na którym agent pakietu OMS.
* Dodaj hello oceny usługi Active Directory rozwiązania tooyour obszar roboczy OMS z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).  Nie są wymagane żadne dalsze czynności konfiguracyjne.

  > [!NOTE]
  > Po dodaniu rozwiązania hello hello AdvisorAssessment.exe plik zostanie dodany tooservers z agentami. Dane konfiguracji jest do odczytu i następnie wysyłane toohello usługę w chmurze hello do przetwarzania. Logika jest stosowane toohello odebranych danych i usługi w chmurze hello rejestruje dane hello.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Szczegóły kolekcji danych w usłudze Active Directory oceny

Active Directory oceny zbiera dane z hello następujące źródła przy użyciu agentów hello, które mają włączone:

- Rejestr modułów zbierających dane
- Moduły zbierające LDAP
- .NET framework
- Dziennik zdarzeń modułów zbierających dane
- Usługa Active Directory interfejsy (ADSI)
- Windows PowerShell
- Moduły zbierające dane pliku
- Instrumentacja zarządzania Windows (WMI)
- Narzędzie DCDIAG interfejsu API
- Interfejs API usługi (NTFRS) replikacji plików
- Kod niestandardowy C#


Witaj poniższej tabeli przedstawiono metody zbierania danych dla agentów, czy Operations Manager (SCOM) jest wymagany i jak często dane są zbierane przez agenta.

| Platformy | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 dni |

## <a name="understanding-how-recommendations-are-prioritized"></a>Opis sposobu mają pierwszeństwo zalecenia
Każdy zalecenia otrzymuje wartość wagi, która identyfikuje hello względnego hello zalecenia. Wyświetlane są tylko zalecenia najważniejszych hello 10.

### <a name="how-weights-are-calculated"></a>Jak są obliczane wagi
Wagi są wartości zagregowanych oparte na trzech kluczowych czynników:

* Witaj *prawdopodobieństwo* czy problemu powoduje występowanie problemów. Większe prawdopodobieństwo oznacza większe ogólny wynik tooa rekomendację hello.
* Witaj *wpływ* wydania hello w Twojej organizacji, jeśli spowodować problem. Większy wpływ oznacza większe ogólny wynik tooa rekomendację hello.
* Witaj *nakładu* wymagane tooimplement hello zalecenia. Wyższy nakładu pracy oznacza tooa mniejszych ogólny wynik dla hello zalecenia.

Witaj wag każde zalecenie jest wyrażona jako procent hello łącznym wynikiem dostępne dla każdego obszaru fokus. Na przykład jeśli zalecenia w hello zabezpieczeń i zgodności fokus obszaru ma wynik % 5, wdrażanie tego zalecenia zwiększa z ogólną % wynik przez 5 zabezpieczeń i zgodności.

### <a name="focus-areas"></a>Obszarach zainteresowań
**Zabezpieczeń i zgodności** — w tym obszarze fokus zawiera zalecenia dotyczące potencjalnego zagrożenia bezpieczeństwa i naruszeń, zasad firmowych i wymagania techniczne, prawne i przepisami zgodności.

**Dostępność i ciągłość prowadzenia działalności biznesowej** — w tym obszarze fokus zawiera zalecenia dotyczące odporności infrastruktury i ochronę biznesowej, dostępności usług.

**Wydajność i skalowalność** — ten obszar fokus zawiera zalecenia dotyczące toohelp organizacji infrastruktury IT zwiększania, sprawdź, czy spełnia bieżące wymagania dotyczące wydajności środowiska informatycznego i jest w stanie toorespond toochanging wymaga infrastruktury.

**Uaktualniania, wdrażania i migracji** — toohelp zalecenia dotyczące uaktualniania zawiera ten obszar fokus, migrację i wdrażanie usługi Active Directory tooyour istniejącej infrastruktury.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Należy należy dążyć tooscore 100% w każdym obszarze fokus?
Niekoniecznie. zalecenia Hello są oparte na powitania wiedzy i doświadczeń zdobytych Microsoft inżynierowie między tysięcy wizyt klienta. Jednak nie infrastruktury serwerowe są hello takie same i szczegółowe zalecenia mogą być bardziej lub mniej istotne tooyou. Na przykład niektóre zalecenia dotyczące zabezpieczeń może być mniej istotne, jeśli maszyny wirtualne nie są uwidocznione toohello Internet. Kilka zaleceń dostępności może być mniej istotne dla usług, które umożliwiają zbieranie danych ad hoc — niski priorytet i raportowania. Problemy, które są ważne tooa dojrzałe firm może być mniej ważne tooa rozruchu. Może mają tooidentify obszarach zainteresowań, które są zebranych i przyjrzyj się jak zmienić wyniki wraz z upływem czasu.

Każdy zalecenie obejmuje wskazówek dotyczących Dlaczego ważne jest. Należy użyć tego tooevaluate wskazówki czy wdrażanie zalecenie hello jest odpowiednie dla Ciebie, charakter hello IT usługi i hello potrzeby biznesowe danej organizacji.

## <a name="use-assessment-focus-area-recommendations"></a>Użyj zaleceń obszaru fokus oceny
Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie hello. tooread więcej na temat instalowania rozwiązań, zobacz [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Po jego zainstalowaniu, można wyświetlić podsumowanie hello zalecenia za pomocą kafelka oceny hello na stronie Przegląd hello OMS.

Witaj w widoku Podsumowanie oceny zgodności dla Twojej infrastruktury, a następnie wejdź do zalecenia.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview zalecenia dotyczące fokus obszaru i podejmij akcję korekcyjną
1. Na powitania **omówienie** kliknij przycisk hello **oceny** kafelku infrastruktury serwera.
2. Na powitania **oceny** strony, przejrzyj hello informacje podsumowania w jednym z bloków obszaru fokus hello, a następnie kliknij jedną tooview zalecenia dla tego obszaru fokus.
3. Na dowolnym hello fokus obszaru stron można wyświetlić hello priorytety zalecenia dla danego środowiska. Kliknij zalecenie, w obszarze **dotyczy obiektów** tooview szczegółowych informacji o Dlaczego hello tworzone są zalecenia.  
    ![Obraz zalecenia oceny](./media/log-analytics-ad-assessment/ad-focus.png)
4. Należy wykonać działania naprawcze sugerowane w **sugerowanych akcji**. Gdy element hello został rozwiązany, nowsze rekordy oceny zalecane akcje zostały wykonane i zwiększy wynik zgodności. Poprawione elementy są wyświetlane jako **przekazany obiektów**.

## <a name="ignore-recommendations"></a>Ignoruj zalecenia
Jeśli masz zaleceń, które mają tooignore, można utworzyć plik tekstowy, który będzie używany przez OMS tooprevent zaleceń znajdujących się w wynikach oceny.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>zalecenia dotyczące tooidentify, które będzie ignorować
1. Zaloguj się w obszarze roboczym tooyour i Otwórz dziennik wyszukiwania. Użyj hello następujące zalecenia toolist zapytania, które nie powiodły się na komputerach w danym środowisku.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Poniżej przedstawiono zrzut ekranu przedstawiający hello dziennik wyszukiwania: ![nie powiodło się zalecenia](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Wybierz, które mają tooignore zalecenia. Użyjesz wartości hello RecommendationId w następnej procedurze hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate i użyj pliku tekstowego IgnoreRecommendations.txt
1. Utwórz plik o nazwie IgnoreRecommendations.txt.
2. Wklej lub wpisz każdego RecommendationId dla każde zalecenie ma tooignore analizy dzienników w osobnym wierszu, a następnie zapisz i zamknij plik hello.
3. Umieść plik hello w hello następującego folderu na każdym komputerze miejscu zalecenia tooignore OMS.
   * Na komputerach z usługą Microsoft Monitoring Agent (połączony bezpośrednio lub za pośrednictwem programu Operations Manager) - hello *SystemDrive*: \Program Files\Microsoft Agent\Agent monitorowania
   * Na serwerze zarządzania programu Operations Manager hello - *SystemDrive*: System Center 2012 R2\Operations Manager\Server \Program Files\Microsoft

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify, że zalecenia są ignorowane
Po uruchomieniu hello następnej zaplanowanej oceny domyślnie co 7 dni hello określony zalecenia są oznaczone *zignorowane* i nie będą wyświetlane na pulpicie nawigacyjnym oceny hello.

1. Możesz użyć powitania po toolist zapytania wyszukiwania dziennika wszystkie zalecenia hello ignorowane.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Jeśli później zdecydujesz, które mają toosee zignorowane zalecenia, Usuń wszystkie pliki IgnoreRecommendations.txt lub RecommendationIDs można usunąć z nich.

## <a name="ad-assessment-solutions-faq"></a>AD oceny rozwiązania — często zadawane pytania
*Częstotliwość oceny, czy działa?*

* Ocena Hello jest uruchamiane co 7 dni.

*Czy istnieje sposób tooconfigure częstotliwość oceny hello działa?*

* Nie w tej chwili.

*Jeśli inny serwer zostanie odnaleziony po rozwiązanie do oceny zostały dodane, zostanie on oceniane?*

* Tak, gdy okaże się, że jest oceniane z następnie, co 7 dni.

*Jeśli serwer jest likwidowany, gdy zostanie ono zostać usunięte z hello oceny?*

* Jeśli serwer nie przedstawi danych do 3 tygodni, zostanie ono usunięte.

*Co to jest nazwa hello procesu hello hello zbierania danych?*

* AdvisorAssessment.exe

*Jak długo trwa toobe dane zbierane?*

* Hello zbierania danych rzeczywistych na powitania serwera trwa około 1 godziny. Może trwać dłużej na serwerach, które mają wiele serwerów usługi Active Directory.

*Istnieje już tooconfigure sposób podczas zbierania danych?*

* Nie w tej chwili.

*Dlaczego są wyświetlane tylko zalecenia 10 pierwszych hello?*

* Zamiast daje utrudnione kompletnej zadań, zaleca się skupić się na najpierw adresowania hello priorytety zalecenia. Po adresu im dodatkowe zalecenia staną się dostępne. Jeśli wolisz toosee hello szczegółową listę, można wyświetlić wszystkie zalecenia za pomocą wyszukiwania dziennika.

*Istnieje już tooignore sposób zalecenia?*

* Tak, zobacz [zignorowanie zalecenia](#ignore-recommendations) powyższej sekcji.

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowych danych oceny usługi AD i zalecenia.
