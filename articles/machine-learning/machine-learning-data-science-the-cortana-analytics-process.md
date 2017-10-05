---
title: "Co to jest proces nauki danych zespołu?  | Microsoft Docs"
description: "Proces nauki danych zespołu jest systematyczne metody tworzenia inteligentnego aplikacji, które wykorzystują zaawansowana analityka."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: TRUE
ms.openlocfilehash: d1ec602b2a69b0bd01bf7b43ef5fed9b8c2781c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-team-data-science-process-tdsp"></a>Co to jest zespołowe przetwarzanie danych dla celów naukowych?
[Zespołu danych nauki procesu (TDSP)](data-science-process-overview.md) dostarcza systematyczne rozwiązanie do tworzenia aplikacji inteligentnego umożliwiającą zespoły analityków danych do współpracy nad pełny cykl działania potrzebne, aby włączyć te aplikacje do produktów. TDSP przedstawiono sekwencję kroków, które zapewniają **wskazówki** na temat sposobu definiowania problem, Konfigurowanie narzędzi oraz środowiska wymaganego, analizy danych, kompilacji i oceny modeli predykcyjnych i następnie wdrażania modeli w aplikacjach dla przedsiębiorstw. 

Poniżej przedstawiono kroki **proces nauki danych zespołu**:  

![Przepływ pracy centralnych zasad dostępu](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

Proces jest **iteracyjne**: opis nowych i istniejących lub ulepszenia w modelu rozwoju i wymaga konieczności wprowadzania zmian wcześniej wykonywane w sekwencji kroki. Istniejące rozwoju organizacji i planowania procesów projektu są **łatwo dostosować** do pracy z sekwencją zdefiniowane TDSP kroków. 

Kroki w procesie są diagramu i połączone w [ścieżka szkoleniowa dotycząca TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i opisane poniżej.  

## <a name="preparation-steps"></a>Procedura przygotowująca
## <a name="p1-plan-the-analytics-project"></a>P1. Planowanie projektu analityka
Uruchom projekt analytics, definiując problemów i celów biznesowych. Są one określone w zakresie **wymagania biznesowe**. Głównym celem tego etapu jest do identyfikowania zmiennych klucza business (Prognoza lub prawdopodobieństwo kolejności fałszywych, na przykład), które wymaga analizy do przewidzenia, aby spełnić te wymagania. Dodatkowe planowanie następnie zazwyczaj konieczne jest opracowanie zrozumienia **źródeł danych** potrzebne do adresu cele projektu z perspektywy analitycznych. Nie jest rzadko, na przykład, aby dowiedzieć się, że istniejące systemy należy zbierać i rejestrować dodatkowych typów danych w celu rozwiązania problemu i osiągnięcia celów projektu. Aby uzyskać instrukcje, zobacz [Planowanie środowiska procesu nauki danych zespołu](machine-learning-data-science-plan-your-environment.md) i [scenariusze zaawansowana analityka w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Konfigurowanie środowiska analizy
Środowisko analytics procesu nauki danych zespołu obejmuje kilka składników: 

* **obszary robocze danych** w przypadku, gdy dane są przygotowywane do analizy i modelowania, 
* **infrastruktura przetwarzania** przetwarzanie wstępne, badać i modelowania danych
* **infrastrukturze środowiska uruchomieniowego** operacjonalizuj modele analitycznych i uruchomić inteligentnego klienta aplikacji, które wykorzystują modeli.  

Infrastruktura analytics, który należy skonfigurować często jest częścią środowisku, w którym jest niezależne od podstawowej systemów operacyjnych. Ale zwykle wykorzystuje dane z wielu systemów w przedsiębiorstwie, a także ze źródeł zewnętrznych w firmie. Infrastruktura analytics może być całkowicie opartej na chmurze, lub instalacji lokalnej lub hybrydowej obu. Opcjach, zobacz temat [Konfigurowanie środowisk nauki danych do użycia w procesie nauki danych zespołu](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Kroki Analytics:
## <a name="1-ingest-data-into-the-analytical-environment"></a>1. Pozyskiwania danych w środowisku analitycznych
Pierwszym krokiem jest wprowadzenie odpowiednich danych z różnych źródeł, albo z lub z poza firmę, w środowiskach analitycznego przetwarzania danych. **Format** w źródle danych może się różnić od formatu wymaganego przez miejsce docelowe. Dlatego niektóre przekształcania danych może także wymagać można przeprowadzić za pomocą narzędzi wprowadzanie. Opcjach, zobacz temat [ładowanie danych do środowiska magazynu dla analityka](machine-learning-data-science-ingest-data.md)

Oprócz początkowej wprowadzanie danych wiele aplikacji inteligentnego są wymagane do odświeżania danych regularnie jako część procesu uczenia trwającą. Można to zrobić, konfigurując **potoku danych** lub przepływ pracy. To jest częścią iteracyjne część procesu, który obejmuje ponowne utworzenie i ponownej oceny modeli analitycznych używanych przez aplikację inteligentnego wdrażania rozwiązania. Zobacz na przykład [przenoszenia danych z lokalnego programu SQL server SQL Azure z fabryką danych Azure](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Eksplorowanie i wstępne przetwarzanie danych
Następnym krokiem jest uzyskanie lepiej zrozumieć dane przez badanie jego **podsumowania statystyk** , relacje i przy użyciu techniki takie **wizualizacji**. Dotyczy to również gdzie problemy z **jakości danych** i integralności, takich jak brakujące wartości, niezgodności typu danych i relacje niespójne dane są obsługiwane. Przetwarzania wstępnego przekształceń są używane do wyczyścić nieprzetworzone dane przed dalszej analizy i modelowania może mieć miejsce. Aby uzyskać opis, zobacz [uczenia maszynowego zadania, aby przygotować dane dla rozszerzonego](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Tworzenie funkcji
Analityków danych, we współpracy z ekspertami domeny, musisz określić funkcje, które przechwytywania istotne właściwości zestawu danych i które najlepiej użyć do prognozowania zmienne klucza business zidentyfikowanego w trakcie planowania. Te nowe funkcje mogą pochodzić z istniejących danych i może wymagać dodatkowych danych, które mają być zbierane. Ten proces jest nazywany **Inżynieria** i jest jeden z kluczy kroków tworzenia systemu skuteczne analizy predykcyjnej. Ten krok wymaga creative kombinację doświadczenia z domeny i szczegółowych danych uzyskane w kroku Eksploracja danych. Aby uzyskać instrukcje, zobacz [Inżynieria w procesie nauki danych zespołu](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Tworzenie modeli predykcyjnych
Analityków danych kompilacji analitycznych modeli na potrzeby prognozowania klucza zmienne identyfikowana na podstawie wymagań biznesowych zdefiniowane w kroku przy użyciu danych, która została wyczyszczona i featurized planowania. Machine learning systemów obsługi wielu **modelowania algorytmów** dotyczą różnych przypadków. Aby uzyskać instrukcje, zobacz [Wybieranie algorytmów w zespół usługi Azure Machine Learning](machine-learning-algorithm-choice.md).

Analityków danych, musisz wybrać modelu najbardziej odpowiednie dla swojego zadania prognozowania i nie jest rzadko wyniki z wielu modeli muszą być łączone w celu uzyskania najlepszych wyników. Dane wejściowe dla modelowania jest zwykle losowo podzielone na trzy części:

* szkoleniowy zestaw danych 
* Sprawdzanie poprawności zestawu danych 
* zestaw danych testowych 

Modele są tworzone przy użyciu **szkoleniowy zestaw danych**. Optymalne kombinację modeli (z parametrami dopasowane) wybrano uruchamiając modeli i pomiaru błędy prognozowania **zestawu danych sprawdzania poprawności**. Na koniec **zestawu danych do testowania** służy do oceny wydajności wybrany model na niezależne danych, który nie był używany do nauczenia albo do sprawdzania modelu.  Aby uzyskać procedury, zobacz [jak do oceny wydajności modelu w usłudze Azure Machine Learning](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Wdrażanie i używanie modeli
Gdy mamy zestaw modeli, które również wykonywać może być **operationalized** korzystać z innych aplikacji. W zależności od wymagań biznesowych prognoz zostały wprowadzone w **czasu rzeczywistego** lub na **partii** podstawy. Aby operationalized, musi być widoczne z modeli **otworzyć Interfejs API** łatwe wykorzystanie z różnych aplikacji takich online witryny sieci Web, arkusze kalkulacyjne, pulpity nawigacyjne lub aplikacje biznesowe i wewnętrznej bazy danych. Zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Podsumowanie i następne kroki
[Proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ma formę sekwencji kroków iterowane który **zawierają wskazówki** zadań wymagane na potrzeby tworzenia aplikacji inteligentnego zaawansowana analityka. Każdy krok zawiera także szczegółowe informacje dotyczące sposobu używania różnych technologiach firmy Microsoft, aby wykonać zadania opisane. 

Gdy TDSP nie określają określonych rodzajów **dokumentacji** artefaktów, jest najlepszym rozwiązaniem dokumentu wyniki Eksploracja danych, modelowania i oceny i zapisać stosowne kodu tak, aby analiza można powtórzyć na żądanie. Dzięki temu również ponownemu pracy analytics podczas pracy z innych aplikacji obejmujących podobnych danych i zadań prognozowania.

Pełne end-to-end wskazówki, które pokazują wszystkie kroki procesu **określonych scenariuszy** podawane są również. Zobacz, na przykład:

* [Proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Używania platformy Spark w usłudze Azure HD.mdnsight nauki danych](machine-learning-data-science-spark-overview.md)
* [Skalowalna nauki danych w usłudze Azure Data Lake: wskazówki end-to-end](machine-learning-data-science-process-data-lake-walkthrough.md)

