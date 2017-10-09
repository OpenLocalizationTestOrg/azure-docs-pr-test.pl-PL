---
title: "rozwiązanie do zarządzania w OMS aaaBuild | Dokumentacja firmy Microsoft"
description: "Rozwiązania do zarządzania rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać obszar roboczy OMS tootheir klientów.  Ten artykuł zawiera szczegóły dotyczące tworzenia toobe rozwiązań zarządzania używane we własnym środowisku lub wprowadzone dostępne tooyour klientów."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Projektowanie i kompilowanie rozwiązania do zarządzania w Operations Management Suite (OMS) (wersja zapoznawcza)
> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.

[Rozwiązania do zarządzania](operations-management-suite-solutions.md) rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać obszar roboczy OMS tootheir klientów.  Ten artykuł przedstawia toodesign podstawowy proces i utworzenie rozwiązania do zarządzania, które jest odpowiednie dla najbardziej typowych wymagań.  W przypadku nowych rozwiązań do zarządzania toobuilding można skorzystać z tego procesu jako punkt początkowy i korzystać z założenia hello bardziej złożonych rozwiązań zgodnie z wymaganiami rozwijać.

## <a name="what-is-a-management-solution"></a>Co to jest rozwiązaniem do zarządzania?

Rozwiązania do zarządzania zawiera OMS i zasobów platformy Azure, które współpracują ze sobą tooachieve scenariusza monitorowania.  Są one zaimplementowane jako [szablony zarządzania zasobami](../azure-resource-manager/resource-manager-template-walkthrough.md) zawierające szczegóły dotyczące tooinstall i konfigurowanie ich zasobów zawartych w niej rozwiązania hello jest zainstalowany.

Witaj strategii podstawowa jest toostart rozwiązania do zarządzania przez utworzenie hello pojedynczych składników w środowisku platformy Azure.  Po utworzeniu funkcji hello działa prawidłowo, następnie można uruchomić je do pakowania [plik rozwiązania zarządzania](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Projektowanie własnego rozwiązania
najbardziej typowe wzorzec Hello rozwiązania do zarządzania jest wyświetlana w powitania po diagramu.  Witaj różnych składników, w tym wzorcu omówiono hello poniżej.

![Omówienie rozwiązania OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Źródła danych
Witaj pierwszy krok w projektowaniu rozwiązania jest określenie hello dane, które wymagają z repozytorium analizy dzienników hello.  Te dane mogą być zbierane przez [źródła danych](../log-analytics/log-analytics-data-sources.md) lub [inne rozwiązanie](operations-management-suite-solutions.md), lub rozwiązanie może być konieczne tooprovide hello procesu toocollect go.

Istnieją różne sposoby źródeł danych, które mogą być zbierane w repozytorium analizy dzienników hello zgodnie z opisem w [źródeł danych w analizy dzienników](../log-analytics/log-analytics-data-sources.md).  Obejmuje zdarzenia w dzienniku zdarzeń systemu Windows hello, lub generowane przez Syslog dodatkowo tooperformance liczniki dla klientów z systemami Windows i Linux.  Można także gromadzić dane z zasobów platformy Azure, zebrane przez Azure Monitor.  

Jeśli potrzebujesz danych, który nie jest dostępny za pośrednictwem żadnego hello dostępnych źródeł danych, a następnie można użyć hello [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md) co pozwala repozytorium analizy dzienników toohello toowrite danych za pomocą dowolnego klienta, który można wywołać REST INTERFEJS API.  Witaj najczęściej oznacza zbierania danych niestandardowych w rozwiązaniu do zarządzania jest toocreate [runbook automatyzacji Azure](../automation/automation-runbook-types.md) który zbiera dane hello wymaganych zasobów platformy Azure lub zewnętrznego i używa hello toowrite interfejsu API modułów zbierających dane toohello repozytorium.  

### <a name="log-searches"></a>Dziennik wyszukiwania
[Zaloguj się wyszukiwanie](../log-analytics/log-analytics-log-searches.md) są używane tooextract i analizowanie danych hello analizy dzienników repozytorium.  Są one używane przez widoki i alertach w dodanie tooallowing hello użytkownika tooperform ad hoc analizy danych w repozytorium hello.  

Należy zdefiniować żadnych zapytań, które prawdopodobnie będą pomocne toohello użytkownika, nawet jeśli nie są one używane przez wszystkie widoki lub alerty.  W portalu hello będą dostępne toothem jako zapisane wyszukiwania i mogą również obejmować je w [części wizualizacji listy kwerend](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) w widoku niestandardowym.

### <a name="alerts"></a>Alerty
[Alerty w analizy dzienników](../log-analytics/log-analytics-alerts.md) identyfikowanie problemów za pomocą [dziennika wyszukiwania](#log-searches) danych hello w repozytorium hello.  One powiadomienia użytkownika hello albo automatycznie uruchomić akcję w odpowiedzi. Określić różnych warunków alertów dla aplikacji i umieścić odpowiednie reguły alertów w pliku rozwiązania.

Jeśli hello problem można rozwiązać potencjalnie z zautomatyzowanego procesu, następnie zwykle utworzysz element runbook w automatyzacji Azure tooperform rozwiązywanie tego problemu.  Najbardziej Azure usługi można zarządzać za pomocą [poleceń cmdlet](/powershell/azure/overview) runbook hello, które będą korzystać z tooperform takich funkcji.

Jeśli rozwiązanie wymaga funkcji zewnętrznych w odpowiedzi tooan alert, a następnie można użyć [odpowiedzi elementu webhook](../log-analytics/log-analytics-alerts-actions.md).  Dzięki temu można toocall zewnętrznej usługi sieci web wysyła informacje z hello alert.

### <a name="views"></a>Widoki
Widoki analizy dzienników są używane toovisualize danych z repozytorium analizy dzienników hello.  Każde rozwiązanie zazwyczaj będzie zawierać pojedynczy widok o [Kafelek](../log-analytics/log-analytics-view-designer-tiles.md) która jest wyświetlana na głównym pulpicie nawigacyjnym hello użytkownika.  Widok Hello może zawierać dowolną liczbę [części wizualizacji](../log-analytics/log-analytics-view-designer-parts.md) tooprovide różne wizualizacje hello zebranych danych toohello użytkownika.

Możesz [Tworzenie niestandardowych widoków przy użyciu projektanta widoków hello](../log-analytics/log-analytics-view-designer.md) który później można wyeksportować do uwzględnienia w pliku rozwiązania.  


## <a name="create-solution-file"></a>Utwórz plik rozwiązania
Po skonfigurowaniu i przetestowane hello składników, które będą częścią rozwiązania, możesz [utworzyć plik rozwiązania](operations-management-suite-solutions-solution-file.md).  Wdroży składniki rozwiązania hello w [szablonu usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) zawierającą [zasobów rozwiązania](operations-management-suite-solutions-solution-file.md#solution-resource) z toohello relacje innych zasobów w hello pliku.  


## <a name="test-your-solution"></a>Testowanie rozwiązania
Podczas tworzenia rozwiązania, będzie konieczne tooinstall i przetestować go w obszarze roboczym.  Można to zrobić przy użyciu dowolnej z dostępnych metod hello zbyt[testowania i zainstalowanie szablonów usługi Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publikowanie rozwiązania
Po wprowadzeniu i przetestowane rozwiązanie można tworzyć toocustomers dostępne za pośrednictwem albo hello następujące źródła.

- **Szablony szybkiego startu usługi Azure**.  [Szablony szybkiego startu usługi Azure](https://azure.microsoft.com/resources/templates/) jest zestaw szablonów usługi Resource Manager zamieszczone przez społeczność hello za pośrednictwem usługi GitHub.  Można udostępnić rozwiązania przez następujące informacje w hello [przewodnik wkład](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Witaj [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) pozwala toodistribute i sprzedawać rozwiązania tooother deweloperów, niezależnym dostawcom oprogramowania i specjalistów IT.  Aby dowiedzieć się jak toopublish tooAzure Twojego rozwiązania Marketplace w [jak toopublish i zarządzanie nimi oferty w portalu Azure Marketplace hello](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Utwórz plik rozwiązania](operations-management-suite-solutions-solution-file.md) rozwiązania do zarządzania.
* Szczegóły dotyczące hello [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Wyszukiwanie [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates) przykłady różnych szablonów usługi Resource Manager.