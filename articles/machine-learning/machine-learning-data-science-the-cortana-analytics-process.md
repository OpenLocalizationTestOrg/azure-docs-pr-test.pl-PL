---
title: "aaaWhat jest proces nauki danych zespołu?  | Microsoft Docs"
description: "Hello proces nauki danych zespołu jest systematyczne metody tworzenia inteligentnego aplikacji, które wykorzystują zaawansowana analityka."
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
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Co to jest hello zespołu danych nauki procesu (TDSP)?
Witaj [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md) dostarcza systematyczne rozwiązanie toobuilding inteligentnego aplikacji, które umożliwia zespoły danych służące toocollaborate skutecznie przez hello pełny cykl życiowy działania potrzebne tooturn te aplikacje do produktów. Witaj TDSP przedstawiono sekwencję kroków, które zapewniają **wskazówki** w sposób toodefine hello problem, skonfiguruj narzędzia hello oraz środowiska wymaganego, analizy danych, kompilacji i ocenić modeli predykcyjnych, a następnie Wdróż te modele w aplikacje przedsiębiorstwa. 

Poniżej przedstawiono kroki hello **proces nauki danych zespołu**:  

![Przepływ pracy centralnych zasad dostępu](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

proces Hello jest **iteracyjne**: hello zrozumienia nowych i istniejących lub ulepszenia w modelu hello rozwoju i wymaga konieczności wprowadzania zmian wcześniej wypełniane hello sekwencji kroki. Istniejące rozwoju organizacji i planowania procesów projektu są **łatwo dostosować** toowork z hello zdefiniowane TDSP sekwencji kroków. 

Witaj kroki w procesie hello są diagramu i połączone w hello [ścieżka szkoleniowa dotycząca TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i opisane poniżej.  

## <a name="preparation-steps"></a>Procedura przygotowująca
## <a name="p1-plan-hello-analytics-project"></a>P1. Planowanie projektu analytics hello
Uruchom projekt analytics, definiując problemów i celów biznesowych. Są one określone w zakresie **wymagania biznesowe**. Głównym celem tego etapu jest tooidentify hello klucza business zmiennych (sprzedaży prognozy lub hello prawdopodobieństwo kolejności fałszywych, na przykład) hello toosatisfy toopredict na potrzeby analizy tych wymagań. Dodatkowe planowanie jest zwykle niezbędne toodevelop zrozumienia hello **źródeł danych** potrzebne tooaddress hello celami hello projektu z perspektywy analitycznych. Nie jest nietypowa sytuacja, na przykład toofind czy istniejącymi systemami muszą toocollect i dziennika dodatkowe rodzaje danych tooaddress hello problem i osiągnięcia celów projektu hello. Aby uzyskać instrukcje, zobacz [Planowanie środowiska do hello proces nauki danych Team](machine-learning-data-science-plan-your-environment.md) i [scenariusze zaawansowana analityka w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Konfigurowanie środowiska analizy
Środowisko analytics hello zespołu w procesie nauki danych obejmuje kilka składników: 

* **obszary robocze danych** w przypadku, gdy dane hello są przygotowywane do analizy i modelowania, 
* **infrastruktura przetwarzania** przetwarzanie wstępne, badać i modelowania danych hello
* **infrastrukturze środowiska uruchomieniowego** toooperationalize hello modeli analitycznych i uruchom powitania klienta inteligentnego aplikacji, które wykorzystują hello modeli.  

Hello analytics infrastrukturę, która wymaga instalacji toobe często jest częścią środowisku, w którym jest niezależne od podstawowej systemów operacyjnych. Ale zwykle wykorzystuje dane z wielu systemów w przedsiębiorstwie hello, a także ze źródeł zewnętrznych toohello firmy. Witaj analytics infrastruktury może być całkowicie opartej na chmurze lub instalacji lokalnej lub hybrydowej z Witaj dwie. Opcjach, zobacz temat [Konfigurowanie środowisk nauki danych do użycia w hello proces nauki danych zespołu](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Kroki Analytics:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Pozyskiwania danych w środowisku analitycznych hello
pierwszym krokiem Hello jest toobring hello odpowiednie dane z różnych źródeł, albo z wewnątrz lub Enterprise poza hello, w środowiskach analitycznego przetwarzania danych hello. Witaj **format** z hello danych w źródle może różnić się od formatu hello wymaganych przez docelowy hello. Dlatego niektórych transformacji danych może być konieczne toobe programach hello wprowadzanie narzędzi. Opcjach, zobacz temat [ładowanie danych do środowiska magazynu dla analityka](machine-learning-data-science-ingest-data.md)

W dodanie toohello początkowej wprowadzanie danych wiele aplikacji inteligentnego są wymagane toorefresh hello danych regularnie jako część procesu trwającą learning. Można to zrobić, konfigurując **potoku danych** lub przepływ pracy. To jest częścią hello iteracyjne część hello procesu, który obejmuje ponowne utworzenie i ponownej oceny hello modeli analitycznych używanych przez aplikację inteligentnego hello wdrażanie rozwiązania hello. Zobacz na przykład [przenoszenia danych z lokalnego tooSQL serwera SQL Azure z fabryką danych Azure](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Eksplorowanie i wstępne przetwarzanie danych
Witaj następnym krokiem jest tooobtain lepiej zrozumieć dane hello polega badaniu jego **podsumowania statystyk** , relacje i przy użyciu technik, takich **wizualizacji**. Dotyczy to również gdzie problemy z **jakości danych** i integralności, takich jak brakujące wartości, niezgodności typu danych i relacje niespójne dane są obsługiwane. Transformacje przetwarzania wstępnego są używane tooclean się hello nieprzetworzone dane przed dalszej analizy i modelowania może mieć miejsce. Aby uzyskać opis, zobacz [tooprepare danych do uczenia maszynowego rozszerzone zadań](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Tworzenie funkcji
Analityków danych, we współpracy z ekspertami domeny, musisz określić hello funkcji przechwytywania hello istotne właściwości zestawu danych hello oraz że najlepiej można zmienne klucza business hello używane toopredict rozpoznane podczas planowania. Te nowe funkcje mogą pochodzić z istniejącymi danymi lub mogą wymagać toobe dodatkowe dane zbierane. Ten proces jest nazywany **Inżynieria** i jest jednym z hello klucza kroki tworzenia systemu skuteczne analizy predykcyjnej. Ten krok wymaga creative kombinację insights wiedzę i hello domeny uzyskane w kroku Eksploracja danych hello. Aby uzyskać instrukcje, zobacz [Inżynieria w hello proces nauki danych zespołu](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Tworzenie modeli predykcyjnych
Analityków danych utworzyć analitycznych modele toopredict hello klucza zmienne identyfikowana na podstawie wymagań biznesowych hello zdefiniowane w kroku przy użyciu danych, która została wyczyszczona i featurized planowania hello. Machine learning systemów obsługi wielu **modelowania algorytmów** , które są stosowane tooa szerokiej gamy przypadków. Aby uzyskać instrukcje, zobacz [jak toochoose algorytmów uczenia maszynowego Azure zespołu](machine-learning-algorithm-choice.md).

Analityków danych, musisz wybrać hello modelu najbardziej odpowiednie dla swojego zadania prognozowania i nie jest rzadko, że wyniki z wielu modeli muszą łączyć toobe tooobtain hello najlepsze wyniki. Witaj danych wejściowych modelowania jest zwykle podzielone losowo na trzy części:

* szkoleniowy zestaw danych 
* Sprawdzanie poprawności zestawu danych 
* zestaw danych testowych 

modele Hello są tworzone przy użyciu hello **szkoleniowy zestaw danych**. Hello optymalne modeli (z parametrami dopasowane) zostanie wybrana kombinacja uruchamiając hello modeli i pomiaru błędów prognozowania hello hello **zestawu danych sprawdzania poprawności**. Na koniec hello **zestawu danych do testowania** jest używane tooevaluate hello wydajności modelu hello wybrany na niezależne danych, które nie były używane tootrain lub sprawdzania poprawności modelu hello.  Aby uzyskać procedury, zobacz [jak tooevaluate modelu wydajności w usłudze Azure Machine Learning](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Wdrażanie i używanie modeli
Gdy mamy zestaw modeli, które również wykonywać może być **operationalized** dla tooconsume inne aplikacje. W zależności od wymagań biznesowych hello, prognoz zostały wprowadzone w **czasu rzeczywistego** lub na **partii** podstawy. toobe operationalized, modele hello mają toobe narażony na **otworzyć Interfejs API** łatwe wykorzystanie z różnych aplikacji takich online witryny sieci Web, arkusze kalkulacyjne, pulpity nawigacyjne lub aplikacje biznesowe i wewnętrznej bazy danych. Zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Podsumowanie i następne kroki
Hello [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ma formę sekwencję powtórzyć kroki który **zawierają wskazówki** zadań hello toouse wymagane zaawansowane analizy toobuild inteligentnego aplikacji. Każdy krok zawiera także szczegółowe informacje o toouse różnych zadań hello toocomplete technologii Microsoft opisu. 

Gdy TDSP nie określają określonych rodzajów **dokumentacji** artefaktów, jest najlepszym rozwiązaniem toodocument hello wyniki hello Eksploracja danych, modelowania i oceny i toosave hello stosowne kodu, który hello analizy można powtórzyć, gdy jest to wymagane. Umożliwia to także ponownemu hello analytics działa podczas pracy z innych aplikacji obejmujących podobnych danych i zadań prognozowania.

Pełne end-to-end wskazówki, które pokazują wszystkie kroki procesu hello hello **określonych scenariuszy** podawane są również. Zobacz, na przykład:

* [Hello proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Hello proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Używania platformy Spark w usłudze Azure HD.mdnsight nauki danych](machine-learning-data-science-spark-overview.md)
* [Skalowalna nauki danych w usłudze Azure Data Lake: wskazówki end-to-end](machine-learning-data-science-process-data-lake-walkthrough.md)

