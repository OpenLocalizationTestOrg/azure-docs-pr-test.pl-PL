---
title: "aaaAssess aplikacji sieci szkieletowej usług za pomocą analizy dzienników przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą rozwiązania sieci szkieletowej usług hello w analizy dzienników przy użyciu hello Azure tooassess portalu hello ryzyka i kondycji sieci szkieletowej usług aplikacji, a także micro-services, węzły i klastry."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Oceń aplikacji usługi Service Fabric i micro-services z hello portalu Azure

> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Symbol sieci szkieletowej usług](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

W tym artykule opisano sposób hello toouse rozwiązania sieci szkieletowej usług w toohelp analizy dzienników identyfikowanie i rozwiązywanie problemów w klastrze usługi sieć szkieletowa usług.

Hello rozwiązania usługi Service Fabric korzysta z danych diagnostyki Azure z maszyn wirtualnych, sieci szkieletowej usług zbierać dane z tabel Azure WAD. Analizy dzienników następnie odczytuje zdarzenia framework sieci szkieletowej usług, w tym **niezawodnej zdarzeń usługi**, **zdarzenia aktora**, **zdarzenia operacyjne**, i **zdarzenia ETW niestandardowe**. Z pulpitu nawigacyjnego rozwiązania hello jesteś tooview stanie godne uwagi problemy i istotne zdarzenia w środowisku sieci szkieletowej usług.

wprowadzenie do rozwiązania hello tooget, należy tooconnect obszaru roboczego analizy dzienników tooa klastra sieci szkieletowej usług. Poniżej przedstawiono trzy tooconsider scenariusze:

1. Jeśli klaster sieci szkieletowej usług nie została wdrożona, wykonaj kroki hello w ***wdrażanie obszaru roboczego analizy dzienników tooa klastra sieci szkieletowej usług podłączony*** toodeploy nowego klastra i skonfigurowano tooreport tooLog Analytics.
2. Jeśli należy toocollect liczniki wydajności z toouse Twojego hostów innych rozwiązań pakietu OMS, takich jak zabezpieczeń w klastrze usługi sieć szkieletowa, wykonaj kroki hello w ***wdrażanie obszar roboczy analizy dzienników tooa klastra sieci szkieletowej usług połączone z rozszerzenia maszyny Wirtualnej zainstalowana.***
3. Jeśli została już wdrożona klastra sieci szkieletowej usług i chcesz tooconnect go tooLog Analytics, wykonaj kroki hello ***Dodawanie istniejącego konta magazynu tooLog Analytics.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Wdróż obszaru roboczego analizy dzienników tooa połączenia klastra sieci szkieletowej usług.
Ten szablon hello następujące:

1. Wdraża obszar roboczy analizy dzienników tooa klastra już połączona sieć szkieletowa usług Azure. Masz toocreate opcji hello nowy obszar roboczy podczas wdrażania szablonu hello lub nazwę wejściowej hello już istniejący obszar roboczy analizy dzienników.
2. Dodaje obszaru roboczego analizy dzienników toohello konto magazynu diagnostyki hello.
3. Umożliwia rozwiązanie sieci szkieletowej usług hello w obszarze roboczym analizy dzienników.

[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Po wybraniu hello wdrażanie przycisk powyżej, hello Azure otwarciu portalu wraz z parametrami, należy tooedit. Być toocreate się nową grupę zasobów możesz wpisać nazwę nowego obszaru roboczego analizy dzienników:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Zaakceptuj postanowienia prawne hello i kliknij przycisk **Utwórz** toostart hello wdrożenia. Po zakończeniu wdrażania hello powinni widzieć nowy obszar roboczy hello i utworzyć klaster i hello WADServiceFabric * zdarzeń, WADWindowsEventLogs i WADETWEvent tabele dodać:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Zainstalowane rozszerzenie maszyny Wirtualnej, należy wdrożyć obszaru roboczego analizy dzienników tooa połączenia klastra sieci szkieletowej usług.

Ten szablon hello następujące:

1. Wdraża obszar roboczy analizy dzienników tooa klastra już połączona sieć szkieletowa usług Azure. Można utworzyć nowego obszaru roboczego lub użyć istniejącego.
2. Dodaje obszaru roboczego analizy dzienników toohello hello diagnostycznych magazynu kont.
3. Umożliwia rozwiązanie sieci szkieletowej usług hello w obszarze roboczym analizy dzienników hello.
4. Instaluje rozszerzenia agent MMA hello w każdym skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa usług. Z zainstalowanym agentem MMA hello metryki wydajności mogą tooview nastąpi węzły.

[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Poniżej hello tego samego powyższe kroki, niezbędne parametry wejściowe hello i rozpocząć poza wdrożenia. Ponownie powinien zostać wyświetlony nowy obszar roboczy hello, klastra i tabele WAD wszystkie utworzone:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Wyświetlanie danych wydajności

tooview danych o wydajności z węzłów:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Uruchom program hello obszaru roboczego analizy dzienników z hello portalu Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Przejdź tooSettings w okienku po lewej stronie powitania i wybierz dane >> liczników wydajności systemu Windows >> "hello Dodaj wybrane liczniki wydajności": ![sieci szkieletowej usług](./media/log-analytics-service-fabric/7.png)
- W wyszukiwaniu dziennika należy użyć powitania po toodelve zapytania do kluczowych metryk dotyczących węzły:

    a. Porównaj hello średnie wykorzystanie procesora CPU przez wszystkie węzły w hello węzły, które występują problemy dotyczące ostatniego toosee godzinę i w odstępach czasu, jaki węzeł ma kolekcji:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Widok podobne wykresy liniowe dla ilość pamięci dostępna na każdym węźle z tej kwerendy:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview lista wszystkich węzłów, przedstawiający hello dokładną wartość średnia dla dostępna pamięć (MB) dla każdego węzła, skorzystaj z tej kwerendy:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. W przypadku hello mają toodrill w dół w określonym węźle, sprawdzając średniej godzinowej hello minimalne, maksymalne i percentyl 75 użycia procesora CPU, możesz teraz możliwe toodo to przez przy użyciu tej kwerendy (Zastąp pole komputera):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Przeczytaj więcej informacji na temat metryk wydajności w analizy dzienników hello [blogu Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Dodawanie istniejącego konta magazynu tooLog analityka

Ten szablon jest po prostu dodaje z istniejącego magazynu kont tooa nowy lub istniejący obszar roboczy analizy dzienników.

[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> Wybór grupy zasobów, jeśli pracujesz już istniejący obszar roboczy analizy dzienników wybierz "Użyj istniejącego" i wyszukaj hello grupę zasobów, zawierającą hello obszaru roboczego analizy dzienników. Utwórz nowy Jeśli jeden inaczej.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Po wdrożeniu tego szablonu można obszaru roboczego może toosee hello magazynu konto podłączone tooyour analizy dzienników. W tym wystąpieniu po dodaniu jednego więcej pamięci masowej konta toohello Exchange obszaru roboczego utworzone powyżej.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Wyświetl zdarzenia dotyczące sieci szkieletowej usług

Po zakończeniu wdrożenia hello i hello rozwiązania sieci szkieletowej usług została włączona w obszarze roboczym, wybierz hello **sieci szkieletowej usług** kafelka na pulpicie nawigacyjnym hello analizy dzienników portalu toolaunch hello sieci szkieletowej usług. pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli. Każda kolumna wymieniono top zdarzenia 10 hello przez liczbę dopasowanie, że kryteria kolumny hello określony przedział czasu. Możesz uruchomić wyszukiwanie dziennika, które zawiera listę całego hello klikając **zobaczyć wszystkie** u dołu prawo hello każdej kolumny lub przez kliknięcie nagłówka kolumny hello.

| **Zdarzenie sieci szkieletowej usług** | **Opis elementu** |
| --- | --- |
| Problemy godne uwagi |Wyświetlanie problemy, takie jak RunAsyncFailures RunAsynCancellations i rozwijane węzła. |
| Zdarzenia operacyjne |Godne zdarzenia operacyjne takich jak uaktualniania aplikacji i wdrożenia. |
| Zdarzenia niezawodne usługi |Zdarzenia zauważalne niezawodnej usługi takie Runasyncinvocations. |
| Zdarzenia aktora |Godne aktora zdarzenia generowane przez micro usług, takich jak wyjątki wyrzucane przez metodę aktora, aktora aktywacji i deactivations i tak dalej. |
| Zdarzenia aplikacji |Wszystkie niestandardowe ETW zdarzenia generowane przez aplikacje. |

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf3.png)

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf4.png)

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla sieci szkieletowej usług.

| Platformy | Bezpośrednie agenta | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minut |

> [!NOTE]
> Zakres hello tych zdarzeń w hello rozwiązania sieci szkieletowej usług można zmienić, klikając **dane oparte na ostatnich 7 dni** u góry hello hello pulpitu nawigacyjnego. Można również wyświetlać zdarzenia generowane w hello ostatnich siedmiu dni, w ciągu jednego dnia lub sześciu godzin. Umożliwia wybranie **niestandardowych** toospecify niestandardowy zakres dat.
>
>

## <a name="next-steps"></a>Następne kroki

* Użyj [wyszukiwania dziennika analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane zdarzeń usługi sieć szkieletowa usług.
