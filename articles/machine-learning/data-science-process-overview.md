---
title: "Omówienie procesu nauki danych zespołu aaaAzure | Dokumentacja firmy Microsoft"
description: "Zapewnia dane nauki metodologii toodeliver analizy predykcyjnej rozwiązań i inteligentnego aplikacji."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Omówienie procesu nauki danych zespołu

Hello zespołu danych nauki procesu (TDSP) jest elastyczne rozwiązania analizy predykcyjnej toodeliver metodologii nauki iteracyjne danych i aplikacji inteligentnego wydajnie. TDSP pomaga w zwiększeniu współpraca z zespołem i learning. Zawiera ona destylacji hello najlepszych rozwiązań i struktury firmy Microsoft i innych użytkowników w branży hello ułatwiających hello pomyślnego wykonania inicjatyw analizy danych. Celem Hello jest firm toohelp pełni osiągnięcia korzyści hello programu analytics.

Ten artykuł zawiera omówienie TDSP oraz jej główne składniki. Udostępniamy ogólny opis tutaj hello procesu, który może być zaimplementowany przy użyciu różnych narzędzi. Bardziej szczegółowy opis zadania projektu hello i role związane z cyklem życia hello procesu hello znajduje się w dodatkowych powiązanych tematach. Wskazówki dotyczące sposobu hello tooimplement TDSP korzystających z określonego zestawu narzędzi firmy Microsoft i infrastrukturę będziemy używać tooimplement hello TDSP naszymi zespołami jest również udostępniany.

## <a name="key-components-of-hello-tdsp"></a>Najważniejsze składniki hello TDSP

TDSP obejmuje hello następujące najważniejsze składniki:

- A **analizy danych w cyklu życia** definicji
- A **standaryzowane struktury projektu**
- **Infrastrukturę i zasoby** dla projektów analizy danych
- **Narzędzia** do wykonania projektu


## <a name="data-science-lifecycle"></a>Cykl życia analizy danych

Hello zespołu danych nauki procesu (TDSP) zawiera cykl życia toostructure hello rozwoju projektów analizy danych. cykl życia Hello opisano kroki hello, z toofinish start, która projektów wykonaj zazwyczaj, gdy są one wykonywane.

Jeśli używasz innej cykl życia analizy danych, takich jak [DM WYSOKĄ](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) lub procesu niestandardowych w organizacji, można nadal używać hello opartego na zadaniach TDSP w kontekście hello tych rozwoju cykle. Na wysokim poziomie te różne metody mają wiele wspólnych. 

Ten cykl życia zostało zaprojektowane dla projektów nauki danych, które są dostarczane jako część inteligentnego aplikacji. Te aplikacje wdrażanie machine learning lub analizy sztucznego modeli analizy predykcyjnej. Projekty nauki poznawcze danych lub projektów ad hoc analytics można również korzystać z tego procesu. W takich przypadkach niektóre hello opisane może nie być jednak potrzebna.    

cykl życia TDSP Hello składa się z pięciu główne etapy, które są wykonywane wielokrotnie powtarzane:

* **Opis biznesowa**
* **Uzyskiwanie danych i zrozumienie**
* **Modelowanie**
* **Wdrożenie**
* **Akceptacji klienta**

W tym miejscu jest wizualną reprezentację hello **cyklu życia procesu nauki danych zespołu**. 

![Cykl życia TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Witaj cele, zadania i artefakty dokumentacji dla każdego etapu cyklu hello w TDSP są opisane w hello [cyklu życia procesu nauki danych zespołu](data-science-process-lifecycle.md) tematu. Te zadania i artefakty są skojarzone z rolami projektu:

- Architekt rozwiązań
- Menedżer projektu
- Analityk danych
- Lider projektu 

Witaj następujący diagram zawiera widoku siatki zadań hello (na niebiesko) i artefakty (na zielono) związane z poszczególnymi etapami cyklu hello (na osi poziomej hello) dla tych ról (na osi pionowej hello). 

![TDSP-role i zadania](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Struktura standardowych projektu

Wszystkie projekty mają strukturę katalogu i użyj szablonów dokumentów projektu o ułatwia hello zespołu członków toofind informacji na temat projektów. Cały kod i dokumenty są przechowywane w systemie kontroli wersji (VC) jak Git, TFS lub Podwersją tooenable współpraca z zespołem. Śledzenia zadań i funkcje w projekcie agile systemu, takich jak Jira śledzenia, Rally, Visual Studio Team Services umożliwia śledzenie bliżej hello kodu dla poszczególnych funkcji. Takie śledzenia umożliwia również tooobtain zespołów lepiej Szacowanie kosztów. TDSP zaleca utworzenie oddzielnych repozytorium dla każdego projektu na powitania VC przechowywania wersji, bezpieczeństwo informacji i współpracy. Hello znormalizowany strukturę dla wszystkich projektów pomaga kompilacji instytucjonalnych wiedzy na powitania organizacji.

Udostępniamy szablony hello struktury folderów i wymagane dokumenty w standardowych lokalizacjach. Ta struktura folderów organizuje hello pliki zawierające kod Eksploracja danych i wyodrębniania funkcji i który zarejestrować iteracji modelu. Te szablony ułatwiają zespołu członków toounderstand pracy przez innych użytkowników i tooadd nowe elementy członkowskie tooteams. Jest łatwy tooview i zaktualizuj szablony dokumentów w formacie markdown. Za pomocą listy kontrolne tooprovide szablony ważne pytania dla każdego tooinsure projektu, aby hello problem jest dobrze zdefiniowany i że materiałów spełniały jakości hello oczekiwano. Przykłady:

- problem biznesowy hello toodocument karty projektu i zakres hello projektu
- Struktura hello toodocument raporty danych oraz statystyki realizacji hello nieprzetworzone dane
- Witaj toodocument raporty modelu pochodzi funkcji
- Model metryki wydajności, takich jak krzywych ROC lub MSE


![TDSP katalogów](./media/data-science-process-overview/tdsp-dir-structure.png)

Struktura katalogów Hello można sklonować z [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infrastrukturę i zasoby danych nauki projektów

TDSP zawiera zalecenia dotyczące zarządzania udostępnionego analytics i infrastruktury magazynu, takich jak:

- systemy plików chmury do przechowywania zestawów danych 
- bazy danych
- klastry danych big data (Hadoop lub Spark) 
- Machine learning usługi. 

Witaj analizy i magazynu infrastruktury może być w chmurze hello lub lokalnie. Jest to, gdzie są przechowywane nieprzetworzone i przetwarzanie zestawów danych. Ta infrastruktura włącza analizę odtworzenia. Również pozwala uniknąć duplikowania, co może prowadzić tooinconsistencies i koszty infrastrukturalne niepotrzebne. Narzędzia są dostarczane tooprovision hello zasobów udostępnionych, śledzić je, a następnie poczekanie każdego tooconnect członek zespołu bezpiecznie toothose zasobów. Możliwe jest również dobrym rozwiązaniem ma członków projektu utworzyć środowisko spójny obliczeniowej. Członkowie zespołu różnych można replikować i zweryfikować eksperymentów.

Oto przykład zespołu działa na wielu projektów i udostępniania różnych składników infrastruktury analytics chmury.

![TDSP infrastruktury](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Narzędzia i narzędzia umożliwiające wykonanie projektu

Wprowadzenie do procesów w większości organizacji jest trudne. Narzędzia pod warunkiem, że proces nauki danych hello tooimplement i cyklem życia pomocy niższe tooand bariery hello wzrost spójności hello przyjęcia. TDSP zapewnia początkowego zestawu narzędzi i skryptów toojump start przyjęcia TDSP w zespole. Pomaga również zautomatyzować niektóre typowe zadania hello w cyklu życia analizy danych hello takich jak Eksploracja danych i modelowanie linii bazowej. Brak dobrze zdefiniowanej strukturze podane dla użytkowników indywidualnych toocontribute udostępnionych z narzędzi do ich zespołu udostępnionego kodu repozytorium. Następnie można użyć tych zasobów przez inne projekty, w ramach hello zespół lub organizacja hello. TDSP również plany wkładów hello tooenable całej Wspólnoty toohello narzędzi. narzędzia TDSP Hello można sklonować z [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Następne kroki

[W procesie nauki danych zespołu: Ról i zadań](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) przedstawiono hello klucza personelu ról i ich skojarzonych zadań dla zespołu nauki danych, która normalizuje w tym procesie. 
