---
title: aaaIntegrating z Operations Management Suite (OMS) | Dokumentacja firmy Microsoft
description: "Ponadto toousing hello standardowe funkcje OMS, możesz też zintegrować ją z innymi tooprovide aplikacji i usług zarządzania środowiska hybrydowego zarządzania, środowiska unikatowy tooyour scenariusze zarządzania niestandardowe tooprovide lub tooprovide niestandardowego możliwości zarządzania dla klientów.  Ten artykuł zawiera omówienie różnych opcji dotyczących integracji z usługą OMS i łączy tooarticles udostępnia szczegółowe informacje techniczne."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Integracja z pakietem Operations Management Suite (OMS)
Operations Management Suite jest firmy Microsoft w chmurze IT rozwiązania do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze.  Ponadto toousing hello standardowe funkcje OMS, możesz też zintegrować ją z innymi tooprovide aplikacji i usług zarządzania środowiska hybrydowego zarządzania, środowiska unikatowy tooyour scenariusze zarządzania niestandardowe tooprovide lub tooprovide niestandardowego możliwości zarządzania dla klientów.  Ten artykuł zawiera omówienie różnych opcji dotyczących integracji z usługą OMS usług oraz linki tooarticles udostępnia szczegółowe informacje techniczne. 

## <a name="log-analytics"></a>Log Analytics
Dane zbierane przez analizy dzienników danych zarządzania znajduje się w repozytorium, która jest hostowana na platformie Azure.  Wszystkie dane przechowywane w repozytorium hello jest dostępna w wyszukiwaniach dziennika, które zapewniają szybki analizy w bardzo dużych ilości danych.  Wymagania w zakresie integracji może być toopopulate hello repozytorium i nowe dane, udostępniając analizy, tooextract danych lub w tooprovide repozytorium hello nowej wizualizacji lub toointegrate z innego narzędzia do zarządzania.

Każda część danych w repozytorium hello jest przechowywany jako rekord.  Podczas wypełniania hello repozytorium, należy zapewnić użytkownikom typu rekordu hello używającej rozwiązania oraz opis jego właściwości.  Podczas pobierania danych, należy te informacje o pracy z danych hello.

![Wypełnianie hello OMS repozytorium](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Wypełnij hello repozytorium analizy dzienników
Istnieje wiele metod wypełniania hello OMS repozytorium.  Witaj używanej metody zależy od czynników, takich jak którym znajduje się hello źródła danych, format hello hello danych i które należy toosupport klientów.  Gdy dane są przechowywane w repozytorium hello, nie ma różnicy jak został zebrany.

Witaj poniższych sekcjach opisano różne opcje hello podczas wypełniania hello OMS repozytorium.

#### <a name="connected-sources-and-data-sources"></a>Połączonych źródeł i źródła danych
Połączone źródła są hello lokalizacji, gdzie można pobrać danych dla repozytorium OMS hello.  Źródła danych i rozwiązania należy uruchomić na połączonych źródeł i zdefiniuj hello określone dane, które są zbierane.  Jeśli aplikacja zapisuje dane tooone tych źródeł danych, następnie można zebrać go przez skonfigurowanie hello źródła danych.  Na przykład jeśli aplikacja tworzy zdarzenia dziennika systemowego, następnie one mogą być zbierane przez źródło danych dziennika systemowego hello na agenta systemu Linux.

* [Źródła danych w analizy dzienników](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Rozwiązania
Rozwiązania rozszerzyć możliwości hello OMS.  Rozwiązanie może zbierać dane ze źródła połączonych hello lub go na rekordy już zebrane w repozytorium hello może wykonywać analizy.  Każdego z rozwiązań firmy Microsoft ma poszczególnych artykuł, zapewniająca szczegóły hello hello danych, które zbiera.

* [Rozwiązania w analizy dzienników](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>Moduł zbierający dane HTTP interfejsu API
Witaj interfejsu API modułów zbierających dane dziennika Analytics HTTP jest interfejs API REST umożliwiający tooadd JSON danych toohello analizy dzienników repozytorium.  Jeśli masz aplikację, która nie zapewnia danych za pomocą jednego z hello innych źródeł danych lub rozwiązania, można wykorzystać ten interfejs API.  Może być używane toopopulate hello repozytorium za pomocą dowolnego klienta, który można wywołać interfejsu API hello i nie polega na harmonogram zbierania hello źródła danych lub rozwiązania.

* [Moduł zbierający dane HTTP analizy dziennika interfejsu API](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Pobieranie danych z hello repozytorium analizy dzienników
Istnieje wiele metod pobierania danych z repozytorium OMS hello.  Może dane tooretrieve użytkowników przy użyciu konsoli OMS hello i udostępnia je z różnych typów wizualizacji i analizy.  Można również pobierać dane hello z procesu zewnętrznego, takich jak innego rozwiązania do zarządzania.

#### <a name="log-searches"></a>Dziennik wyszukiwania
Wszystkie dane przechowywane w repozytorium OMS hello jest dostępna za pośrednictwem dziennik wyszukiwania.  Użytkownicy mogą wykonać własne analizy ad hoc w konsoli OMS hello lub Utwórz pulpit nawigacyjny wizualizacji wyszukiwania określonego dziennika.  Rozwiązania może zawierać niestandardowe widoki z wizualizacjami opartymi na wstępnie zdefiniowane wyszukiwania.  Hello interfejs API dziennika wyszukiwania tooaccess danych można użyć w repozytorium OMS hello z zewnętrznego narzędzia zarządzania lub aplikacji.  

* [Dziennik wyszukiwania analizy dzienników](../log-analytics/log-analytics-log-searches.md)
* [Analiza dzienników dziennika wyszukiwania interfejsu API REST](../log-analytics/log-analytics-log-search-api.md)
* [Polecenia cmdlet analizy dzienników](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Widoki niestandardowe
Hello Widok projektanta pozwala toocreate niestandardowe widoki w konsoli OMS hello zapewniające użytkowników za pomocą wizualizacji i analiza danych hello w rozwiązaniu.  Każdy widok zawiera kafelka wyświetlany na stronie głównej hello hello konsoli i dowolną liczbę części wizualizacji, które są oparte na wyszukiwanie dziennika, zdefiniowane przez użytkownika.

* [Projektant widoków analizy dzienników](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Analiza dzienników można automatycznie eksportować dane z repozytorium OMS hello do usługi Power BI, można wykorzystać jej wizualizacje i narzędzia do analizy.  Wykonuje tego eksportu zgodnie z harmonogramem, więc hello dane są przechowywane w górę toodate. 

* [Eksportuj tooPower danych analizy dzienników analizy Biznesowej](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automatyzacja
OMS można zautomatyzować procesy tooreact toocollected danych lub tooperform innych funkcji zarządzania.  Może zbierać dane z aplikacji i wstawić je do repozytorium OMS hello, lub mogą zautomatyzować hello naprawianie znany problem w znaleziono w repozytorium hello toodata odpowiedzi. 

![Automatyzacja](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Elementy Runbook
Elementy Runbook automatyzacji Azure uruchomić przepływy pracy i skrypty programu PowerShell w hello chmury Azure.  Można używać ich toomanage zasobów platformy Azure lub innych zasobów, które są dostępne z chmury hello.  Elementy Runbook można również uruchomić w lokalnym centrum danych przy użyciu hybrydowego procesu roboczego elementu Runbook.  Można uruchomić element runbook z hello portalu Azure lub procesów zewnętrznych przy użyciu metod, takich jak Środowisko PowerShell lub hello automatyzacji interfejsu API.

* [Uruchamianie elementu runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md)
* [Polecenia cmdlet usługi automatyzacja systemu Azure](https://msdn.microsoft.com/library/dn690262.aspx)
* [Automatyzacja interfejsu API REST](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automatyzacja .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Alerty
Reguły alertów automatycznego uruchamiania zgodnie z harmonogramem tooa wyszukiwania dziennika.  Jeśli wyniki hello odpowiada określonym można uruchomić element runbook automatyzacji Azure i Wywołaj element webhook, który można uruchomić procesu zewnętrznego kryteria hello wynikowy alertu.  Oba te odpowiedzi mogą obejmować szczegóły alertu hello, włącznie z danymi hello zwracane w hello dziennik wyszukiwania.

* [Alerty w analizy dzienników](../log-analytics/log-analytics-alerts.md)
* [Interfejs API dziennika analizy alertu](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Kopii zapasowych i odzyskiwania lokacji
Azure Site Recovery i kopii zapasowych zapewnić usługi ochrony danych przedsiębiorstwa i zapewnienia dostępności hello serwerów i aplikacji.  Można wykorzystać te tooperform usług takich scenariuszy jako udostępnia usługi tworzenia kopii zapasowej dla aplikacji lub inicjowanie trybu failover maszyny wirtualnej.

* [Polecenia cmdlet tworzenia kopii zapasowej systemu Azure](https://msdn.microsoft.com/library/mt619253.aspx)
* [Usługi Azure Site Recovery interfejsu API REST](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Polecenia cmdlet programu Azure Site Recovery](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Niestandardowe rozwiązania
W obszarze roboczym lub w obszarze roboczym klienta, umożliwiająca Hermetyzowanie integracji logikę do toorun niestandardowego rozwiązania.  Rozwiązanie może zawierać dowolne metod integracji hello w tym artykule w tooprovide zasobów tooother dodanie scenariusza pełnego zarządzania.  zasoby Hello w rozwiązaniu hello są umieszczane w taki sposób, że po usunięciu hello rozwiązania, wszystkie zasoby hello, utworzonych przez siebie są usuwane z obszarem roboczym pakietu OMS hello i subskrypcji platformy Azure.

Na przykład rozwiązania można dołączyć automatyzacji elementu runbook toogather i przetwarzanie danych i wypełnij hello repozytorium analizy dzienników przy użyciu interfejsu API modułów zbierających dane HTTP hello.  Mogą również obejmować widok niestandardowy, który umożliwia wyświetlanie i analizuje dane zbierane hello.  

* Tworzenie niestandardowych rozwiązań (wkrótce)    

## <a name="next-steps"></a>Następne kroki
* Odwołanie hello [OMS SDK](operations-management-suite-sdk.md) Aby uzyskać informacje techniczne na temat automatyzacji usługi OMS.  

