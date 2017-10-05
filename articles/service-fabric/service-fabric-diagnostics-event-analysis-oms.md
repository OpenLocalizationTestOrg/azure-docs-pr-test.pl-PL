---
title: "Analiza zdarzeń sieci szkieletowej usług Azure z usługą OMS | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wizualizacji i analizowania zdarzeń, monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure przy użyciu pakietu OMS."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 425c7a733a0a2383f01d2122e7155d3e3a9071be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Analiza zdarzeń i wizualizacji z OMS

Operations Management Suite (OMS) to zbiór usług zarządzania, które pomagają w monitorowania i diagnostyki dla aplikacji i usług hostowanych w chmurze. Aby uzyskać bardziej szczegółowy przegląd OMS, jakie oferuje, przeczytaj [co to jest OMS?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-the-oms-workspace"></a>Analiza dzienników i obszar roboczy OMS

Analiza dzienników zbiera dane z zarządzanych zasobów, włącznie z tabeli magazynu systemu Azure lub agenta i przechowuje ją w centralnym repozytorium. Dane można następnie używana do analizy, alerty i wizualizacji lub dodatkowe eksportowanie. Analiza dzienników obsługuje zdarzeń, danych wydajności lub innych danych niestandardowych.

Po skonfigurowaniu OMS mają dostęp do określonego *obszarem roboczym pakietu OMS*, z którym danych można wykonać zapytania lub wizualizowane w pulpitach nawigacyjnych.

Po odebraniu danych przez analizy dzienników, OMS ma kilka *rozwiązań do zarządzania* , które są opakowaniach jednostkowych rozwiązań do przychodzących danych, dostosować, tak aby kilka scenariuszy monitorowania. Obejmują one *usługi sieć szkieletowa Analytics* rozwiązania i *kontenery* rozwiązania, które są najbardziej odpowiednie dwóch te Diagnostyka i monitorowanie w przypadku używania klastrów sieci szkieletowej usług. Istnieje kilka innych oraz które warto eksploracji i OMS umożliwia również tworzenie rozwiązań niestandardowych, które można uzyskać więcej informacji [tutaj](../operations-management-suite/operations-management-suite-solutions.md). Każdego rozwiązania, które chcesz użyć dla klastra zostanie skonfigurowany w tym samym obszarze roboczym pakietu OMS, obok analizy dzienników. Obszary robocze umożliwiają dla niestandardowych pulpitów nawigacyjnych i wizualizacja danych i modyfikacji danych, które chcesz gromadzenie i przetwarzanie i analizowanie danych.

## <a name="setting-up-an-oms-workspace-with-the-service-fabric-solution"></a>Konfigurowanie obszar roboczy OMS z rozwiązaniem sieci szkieletowej usług

Zaleca się obejmuje rozwiązania usługi sieci szkieletowej w obszarze roboczym pakietu OMS, ponieważ zawiera przydatne pulpit nawigacyjny, który zawiera różne przychodzące kanały dzienników platformy i poziomie aplikacji i stanie do określonych dzienników w sieci szkieletowej usług zapytania. W tym miejscu jest stosunkowo proste rozwiązania sieci szkieletowej usługi wygląd, z jednej aplikacji wdrożonych w klastrze:

![Rozwiązanie rz OMS](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Istnieją dwa sposoby udostępniania i konfigurowania obszarem roboczym pakietu OMS za pomocą szablonu usługi Resource Manager lub bezpośrednio z portalu Azure Marketplace. Użyj pierwszej podczas wdrażania klastra, a drugie Jeśli masz już wdrożone w diagnostyce klastra włączone.

### <a name="deploying-oms-using-a-resource-management-template"></a>Wdrażanie pakietu OMS przy użyciu szablonu zarządzanie zasobami

Dzieje się na etapie tworzenia klastra — w przypadku wdrażania klastra przy użyciu szablonu usługi Resource Manager, szablon można również utworzyć nowy obszar roboczy OMS Dodaj rozwiązania sieci szkieletowej usług do niego i skonfiguruj go odczytać danych z tabel do przechowywania odpowiednie.

>[!NOTE]
>Aby to zrobić, musi być aktywne w kolejności dla tabel usługi Azure storage istnieć OMS diagnostyki / Log Analytics dostęp do informacji z.

[W tym miejscu](https://azure.microsoft.com/resources/templates/service-fabric-oms/) jest przykładowy szablon, który można używać i modyfikować zgodnie z harmonogramem wymaganie, który przeprowadza powyżej akcje. W przypadku, że ma więcej Opcjonalność, istnieje kilka więcej szablonów, które zapewniają różne opcje w zależności od tego, gdzie w procesie może być konfigurowania obszarem roboczym pakietu OMS - znajduje się w temacie [szablonów usługi Service Fabric i OMS](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Wdrażanie pakietu OMS przy użyciu za pośrednictwem portalu Azure Marketplace

Jeśli wolisz Dodaj obszar roboczy OMS po wdrożeniu klastra, przejdź do portalu Azure Marketplace i poszukaj *"Analytics sieci szkieletowej usług"*. Powinien istnieć tylko jeden zasób pokazywany w kategorii "Monitorowania zarządzanie +", pokazano poniżej:

![OMS rz Analytics w portalu Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Kliknięcie przycisku **Utwórz** pojawi się prośba o obszarem roboczym pakietu OMS. Kliknij przycisk **wybierz obszar roboczy** , a następnie **Utwórz nowy obszar roboczy**. Wypełnij odpowiednie wpisy — jedynym wymaganiem jest subskrypcji dla klastra sieci szkieletowej usług i obszarem roboczym pakietu OMS musi być taka sama. Po sprawdzeniu poprawności wpisy obszar roboczy OMS zostanie wdrożona w ciągu kilku minut. Gdy zakończeniem wdrażania, Tworzenie bloku rozwiązania sieci szkieletowej usług nadal pozostanie otwarte. Upewnij się, że tego samego obszaru roboczego zostaną wyświetlone w obszarze *obszarem roboczym pakietu OMS* i trafień **Utwórz** na dole, aby dodać rozwiązanie sieci szkieletowej usług do obszaru roboczego.

## <a name="using-the-oms-agent"></a>Za pomocą agenta pakietu OMS

Jest zalecane, aby użyć EventFlow i WAD jako rozwiązania agregacji, ponieważ pozwalają one na bardziej podejściu Diagnostyka i monitorowanie. Na przykład jeśli chcesz zmienić Twoje dane wyjściowe z EventFlow wymaga nie zmieniono Twojego rzeczywiste Instrumentacji tylko prostą modyfikację do pliku konfiguracji. Jeśli, można jednak podjąć decyzję o inwestycji w przy użyciu pakietu OMS i chcesz kontynuować z użyciem jej do analizy zdarzeń (musi być jedynym Użyj platformy, ale raczej jego będzie co najmniej jednej z platform), firma Microsoft zaleca zapoznanie się ustawienie [OMS ag Enterprise](../log-analytics/log-analytics-windows-agents.md). Należy też używać agent pakietu OMS podczas wdrażania kontenerów do klastra, zgodnie z opisem poniżej.

Proces w ten sposób jest stosunkowo łatwa, ponieważ należy dodać agenta jako skalowania maszyny wirtualnej ustawić rozszerzenia do szablonu usługi Resource Manager zapewnienie, że jest zainstalowany na każdym z węzłów. Przykładowy szablon Menedżera zasobów, która wdraża obszar roboczy OMS z rozwiązaniem sieci szkieletowej usług (jak powyżej) i dodanie agenta do węzły znajdują się w przypadku klastrów [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) lub [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Zalety tego są następujące:

* Bardziej rozbudowane dane po stronie liczników i metryki wydajności
* Łatwa do skonfigurowania danych zbieranych z klastra i go zmienić bez ponownego wdrażania aplikacji lub w klastrze, ponieważ zmiany ustawień agenta może odbywać się w obszarze roboczym pakietu OMS i będzie tylko agent automatycznie resetować. Aby skonfigurować agenta pakietu OMS do pobrania konkretnych licznikach wydajności, przejdź do obszaru roboczego **strona główna > Ustawienia > danych > liczników wydajności systemu Windows** i wybierz dane, które chcesz wyświetlić zebrane
* Dane zostaną wyświetlone szybciej niż musi być przechowywany przed odbierany przez OMS / Log Analytics
* Monitorowanie kontenery jest znacznie łatwiejsze, ponieważ można wybrać dzienniki docker (stdout, stderr były umieszczane) i statystyka (metryki wydajności na poziomach kontenera i węzeł)

Główne w tym miejscu to, że ponieważ jest agentem, zostanie ona wdrożona w klastrze z wszystkich aplikacji, zostanie niektórych minimalny wpływ na wydajność aplikacji w klastrze.

## <a name="monitoring-containers"></a>Kontenery monitorowania

Podczas wdrażania kontenerów do klastra usługi sieć szkieletowa, zaleca się, że klaster został skonfigurowany z agentem pakietu OMS i czy rozwiązania kontenery został dodany do obszaru roboczego OMS, aby włączyć monitorowanie i diagnostyki. Oto, jak wygląda rozwiązania kontenery w obszarze roboczym:

![Pulpit nawigacyjny podstawowe OMS](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Agent umożliwia zbieranie kilka dzienników specyficzne dla kontenera, które można wykonać zapytania w OMS, lub używany do wizualizowanego wskaźników. Typy dziennika, które są zbierane są:

* ContainerInventory: zawiera informacje o lokalizacji kontenera, nazwy i obrazów
* ContainerImageInventory: informacje o wdrożonej obrazów, w tym identyfikatory lub rozmiary
* ContainerLog: dzienniki błędu, dzienniki docker (stdout itp.) i innych pozycji
* ContainerServiceLog: docker demon poleceń, które zostały uruchomione
* O wydajności: liczniki wydajności w tym kontenerze procesora cpu, pamięć, ruch sieciowy na dysku We/Wy i metryki niestandardowe z maszyn hosta

W tym artykule opisano kroki wymagane do skonfigurowania kontenera monitorowania dla klastra. Aby dowiedzieć się więcej o rozwiązaniu kontenery w OMS, zapoznaj się ich [dokumentacji](../log-analytics/log-analytics-containers.md).

Aby skonfigurować rozwiązanie kontenera, w obszarze roboczym, upewnij się, że masz agent pakietu OMS wdrożone w węzłach klastra, wykonując kroki wymienione powyżej. Gdy klaster jest gotowy, należy wdrożyć kontener do niego. Przy tym pamiętać, że kontener jest wdrażany do klastra, po raz pierwszy go może zająć kilka minut pobranie obrazu w zależności od rozmiaru.

W portalu Azure Marketplace, wyszukaj *kontenery* i Utwórz zasób kontenerów (w obszarze monitorowanie i zarządzanie kategorii).

![Dodawanie rozwiązania kontenerów](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

W kroku tworzenia żądania obszarem roboczym pakietu OMS. Wybierz jedną, która została utworzona przy użyciu wdrażania powyżej. Ten krok dodaje rozwiązania kontenery w obszarze roboczym pakietu OMS i jest automatyczne wykrywany przez agenta pakietu OMS wdrożone przez szablon. Agent rozpocznie zbieranie danych o procesach kontenery w klastrze i mniej niż 15 minut, lub tak, powinien zostać wyświetlony światła się za pomocą danych, tak jak obraz powyżej pulpitu nawigacyjnego rozwiązania.


## <a name="next-steps"></a>Następne kroki

Zapoznaj się z następujących narzędzi OMS i opcji, aby dostosować obszar roboczy do potrzeb:

* W przypadku klastrów lokalnymi OMS oferuje bramy (do przodu serwer Proxy HTTP), która może służyć do wysyłania danych z usługą OMS. Dowiedz się więcej o tym, że w [łączenia komputerów bez dostępu do Internetu z usługą OMS przy użyciu bramy OMS](../log-analytics/log-analytics-oms-gateway.md)
* Skonfiguruj OMS, aby skonfigurować [automatycznego alerty](../log-analytics/log-analytics-alerts.md) do pomocy w wykrywaniu i Diagnostyka
* Pobierz zapoznaniu się z [wyszukiwania i badania dziennika](../log-analytics/log-analytics-log-searches.md) funkcje dostępne w ramach analizy dzienników