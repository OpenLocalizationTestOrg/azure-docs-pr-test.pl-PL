---
title: "Analiza zdarzeń sieci szkieletowej usług z pakietu OMS aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Analiza zdarzeń i wizualizacji z OMS

Operations Management Suite (OMS) to zbiór usług zarządzania, które pomagają w monitorowania i diagnostyki dla aplikacji i usług hostowanych w chmurze hello. Przeczytaj tooget bardziej szczegółowy przegląd OMS, jakie oferuje [co to jest OMS?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Analiza i hello obszarem roboczym pakietu OMS dziennika

Analiza dzienników zbiera dane z zarządzanych zasobów, włącznie z tabeli magazynu systemu Azure lub agenta i przechowuje ją w centralnym repozytorium. następnie można Hello dane, używana do analizy, alerty i wizualizacji lub dodatkowe eksportowanie. Analiza dzienników obsługuje zdarzeń, danych wydajności lub innych danych niestandardowych.

Po skonfigurowaniu OMS będzie mieć dostępu do określonych tooa *obszarem roboczym pakietu OMS*, z którym danych można wykonać zapytania lub wizualizowane w pulpitach nawigacyjnych.

Po odebraniu danych przez analizy dzienników, OMS ma kilka *rozwiązań do zarządzania* opakowaniach jednostkowych rozwiązań toomonitor przychodzących danych, dostosowane tooseveral scenariusze, które są. Obejmują one *usługi sieć szkieletowa Analytics* rozwiązania i *kontenery* rozwiązania, które są toodiagnostics Witaj dwie najbardziej znaczenie i monitorowania w przypadku używania klastrów sieci szkieletowej usług. Istnieje kilka innych oraz które warto eksploracji i OMS umożliwia również tworzenie hello rozwiązań niestandardowych, które można uzyskać więcej informacji [tutaj](../operations-management-suite/operations-management-suite-solutions.md). Każde rozwiązanie, wybierz polecenie toouse dla klastra zostanie skonfigurowany w hello tego samego obszarem roboczym pakietu OMS obok analizy dzienników. Obszary robocze umożliwiają niestandardowe pulpity nawigacyjne i wizualizację danych, a modyfikacji toohello dane, które mają toocollect, przetwarzanie i analizowanie.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Konfigurowanie obszar roboczy OMS z hello rozwiązania sieci szkieletowej usług

Zaleca się, że zawierają hello rozwiązania usługi w sieci szkieletowej w obszarze roboczym pakietu OMS, ponieważ zawiera on przydatne pulpitu nawigacyjnego który pokazuje hello różne kanały dzienników przychodzące z poziomu platformy i aplikacji hello i stanie tooquery hello sieci szkieletowej usług określonych dzienniki. W tym miejscu jest stosunkowo proste rozwiązania sieci szkieletowej usługi wygląd, z jednej aplikacji wdrożonych w klastrze hello:

![Rozwiązanie rz OMS](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Istnieją dwa sposoby tooprovision i skonfigurować obszar roboczy OMS za pomocą szablonu usługi Resource Manager lub bezpośrednio z portalu Azure Marketplace. Użyj była hello podczas wdrażania klastra i włączone hello później, jeśli masz już wdrożone w diagnostyce klastra.

### <a name="deploying-oms-using-a-resource-management-template"></a>Wdrażanie pakietu OMS przy użyciu szablonu zarządzanie zasobami

Dzieje się na etapie tworzenia klastra hello — podczas wdrażania klastra przy użyciu szablonu usługi Resource Manager, szablon hello mogą także tworzyć nowy obszar roboczy OMS, Dodaj hello tooit rozwiązania usługi w sieci szkieletowej i skonfiguruj go tooread danych z magazynu odpowiednie hello tabele.

>[!NOTE]
>Dla tego toowork Diagnostyka ma włączone hello Azure magazynu tabel tooexist dla OMS toobe / Log Analytics tooread informacji w z.

[W tym miejscu](https://azure.microsoft.com/resources/templates/service-fabric-oms/) jest przykładowy szablon, który można używać i modyfikować zgodnie z harmonogramem wymaganie, który przeprowadza powyżej akcje. W przypadku hello, że ma więcej Opcjonalność, istnieje kilka więcej szablonów, które zapewniają różne opcje w zależności od tego, gdzie w procesie hello może się konfigurowania obszarem roboczym pakietu OMS - znajduje się w temacie [szablonów usługi Service Fabric i OMS](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Wdrażanie pakietu OMS przy użyciu za pośrednictwem portalu Azure Marketplace

Jeśli wolisz tooadd obszarem roboczym pakietu OMS po wdrożeniu klastra, przejdź tooAzure Marketplace i poszukaj *"Analytics sieci szkieletowej usług"*. Powinien istnieć tylko jeden zasób pokazywany w kategorii "Monitorowania zarządzanie +" hello, pokazano poniżej:

![OMS rz Analytics w portalu Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Kliknięcie przycisku **Utwórz** pojawi się prośba o obszarem roboczym pakietu OMS. Kliknij przycisk **wybierz obszar roboczy** , a następnie **Utwórz nowy obszar roboczy**. Wypełnianie hello wymagane wpisy — hello tutaj jedynym wymaganiem jest hello subskrypcji hello klastra i hello obszarem roboczym pakietu OMS powinna być sieć szkieletowa usług hello takie same. Po sprawdzeniu poprawności wpisy obszar roboczy OMS zostanie wdrożona w ciągu kilku minut. Gdy zakończeniem wdrażania, tworzenie hello bloku rozwiązania sieci szkieletowej usług hello nadal pozostanie otwarte. Upewnij się, że hello tego samego obszaru roboczego pokazuje się w obszarze *obszarem roboczym pakietu OMS* i trafień **Utwórz** u dołu hello tooadd hello obszar roboczy toohello rozwiązania sieci szkieletowej usług.

## <a name="using-hello-oms-agent"></a>Przy użyciu hello Agent pakietu OMS

Zalecane jest toouse EventFlow i WAD jako rozwiązania agregacji, ponieważ umożliwiają one dla bardziej moduły toodiagnostics podejścia i monitorowania. Na przykład jeśli chcesz toochange Twoje dane wyjściowe z EventFlow, wymaga zmiany tooyour rzeczywiste Instrumentacja nie, po prostu prostą modyfikację tooyour pliku. Jeśli jednak zdecydować tooinvest za pomocą pakietu OMS i podejmowanie toocontinue wykorzystywać ich w celach analizy zdarzenia (nie ma toobe hello tylko Użyj platformy, ale raczej jego będzie co najmniej jeden z platform hello), firma Microsoft zaleca zapoznanie się skonfigurowanie hello [</C0>agentpakietuOMS<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> Należy też używać agent pakietu OMS hello w przypadku wdrażania klastra tooyour kontenerów, zgodnie z opisem poniżej.

w ten sposób proces Hello jest stosunkowo łatwa, ponieważ należy tooadd hello agenta zgodnie z zestawu skalowania maszyn wirtualnych szablonu usługi Resource Manager tooyour rozszerzenia, zapewnienie, że jest zainstalowany na każdym z węzłów. Przykładowy szablon usługi Resource Manager wdraża hello obszar roboczy OMS z hello rozwiązania sieci szkieletowej usług (jak powyżej), który dodaje hello agenta tooyour węzły znajdują się w przypadku klastrów [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) lub [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Zalety Hello tego są następujące hello:

* Bardziej rozbudowane dane po stronie liczników i metryki wydajności hello
* Łatwe tooconfigure danych zbieranych z hello klastra i wprowadzania zmian tooit bez ponownego wdrażania aplikacji lub hello klastra, ponieważ zmiany ustawień toohello hello agenta może odbywać się z obszarem roboczym pakietu OMS hello i będzie tylko Zresetuj hello agenta automatycznie. tooconfigure hello OMS agenta toopick się konkretnych licznikach wydajności, przejdź toohello obszaru roboczego **strona główna > Ustawienia > danych > liczników wydajności systemu Windows** i wybierz chcesz toosee zbieranych danych hello
* Dane zostaną wyświetlone szybciej niż o toobe przechowywane przed odbierany przez OMS / Log Analytics
* Monitorowanie kontenery jest znacznie łatwiejsze, ponieważ można wybrać dzienniki docker (stdout, stderr były umieszczane) i statystyka (metryki wydajności na poziomach kontenera i węzeł)

Witaj głównego tutaj to, że ponieważ jest agentem, zostanie ona wdrożona w klastrze z wszystkich aplikacji, zostanie wydajności toohello minimalnym wpływie niektórych aplikacji w klastrze hello.

## <a name="monitoring-containers"></a>Kontenery monitorowania

W przypadku wdrażania klastra sieci szkieletowej usług tooa kontenerów, zalecane jest hello klastra nie został skonfigurowany z agentem pakietu OMS hello i dodano tego rozwiązania kontenery hello tooyour OMS obszaru roboczego tooenable monitorowania i diagnostyki. Jakie rozwiązania wygląda w obszarze roboczym kontenery hello jest następujący:

![Pulpit nawigacyjny podstawowe OMS](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Hello agent umożliwia zbieranie hello kilka dzienników specyficzne dla kontenera, które mogą być wyszukiwane w OMS lub użyć toovisualized wskaźników wydajności. typy dziennika Hello, które są zbierane są:

* ContainerInventory: zawiera informacje o lokalizacji kontenera, nazwy i obrazów
* ContainerImageInventory: informacje o wdrożonej obrazów, w tym identyfikatory lub rozmiary
* ContainerLog: dzienniki błędu, dzienniki docker (stdout itp.) i innych pozycji
* ContainerServiceLog: docker demon poleceń, które zostały uruchomione
* O wydajności: liczniki wydajności w tym kontenerze procesora cpu, pamięć, ruch sieciowy na We/Wy dysku i metryki niestandardowe z hello obsługi maszyn

W tym artykule omówiono tooset wymagane kroki hello zapasowej kontenera monitorowania dla klastra. więcej informacji na temat rozwiązania kontenery w OMS, toolearn wyewidencjonowania ich [dokumentacji](../log-analytics/log-analytics-containers.md).

tooset się hello rozwiązania kontenera, w obszarze roboczym, upewnij się, że masz agent pakietu OMS hello wdrożone w węzłach klastra, wykonując kroki hello wymienionych powyżej. Gdy klaster hello jest gotowy, należy wdrożyć tooit kontenera. Opatrzone pamiętać, że hello po raz pierwszy obraz kontenera jest wdrożony tooa klastra, zajmuje kilka minut toodownload obraz powitania w zależności od rozmiaru.

W portalu Azure Marketplace, wyszukaj *kontenery* i Utwórz zasób kontenerów (w obszarze hello monitorowanie i zarządzanie kategorii).

![Dodawanie rozwiązania kontenerów](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

W kroku tworzenia hello żądania obszarem roboczym pakietu OMS. Wybierz hello, który został utworzony z wdrożeniem hello powyżej. Ten krok dodaje rozwiązania kontenery w obszarze roboczym pakietu OMS i jest automatyczne wykrywany przez agenta pakietu OMS hello wdrożone przez szablon hello. Hello agent rozpocznie się zbieranie danych na procesach kontenery hello hello klastra i mniej niż 15 minut lub tak, powinny pojawić się rozwiązania hello światła się za pomocą danych, tak jak obraz powitania pulpitu nawigacyjnego hello powyżej.


## <a name="next-steps"></a>Następne kroki

Eksploruj hello następujące narzędzia OMS i opcje toocustomize tooyour obszaru roboczego musi:

* W przypadku klastrów lokalnymi OMS oferuje bramy (do przodu serwer Proxy HTTP), które mogą być używane toosend tooOMS danych. Dowiedz się więcej o tym, że w [łączenia komputerów bez Internetu dostępu tooOMS za pomocą hello bramy OMS](../log-analytics/log-analytics-oms-gateway.md)
* Skonfiguruj OMS tooset się [automatycznego alerty](../log-analytics/log-analytics-alerts.md) tooaid w wykrywaniu i Diagnostyka
* Pobierz zapoznaniu się z hello [wyszukiwania i badania dziennika](../log-analytics/log-analytics-log-searches.md) funkcje dostępne w ramach analizy dzienników
