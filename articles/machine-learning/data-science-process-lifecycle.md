---
title: "aaaAzure zespołu danych nauki procesu w cyklu życia | Dokumentacja firmy Microsoft"
description: "Wymagane czynności tooexecute projektów analizy danych."
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
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Zespół proces analizy danych w cyklu życia

Witaj zespołu danych nauki procesu (TDSP) zawiera zalecane cyklu życia używania toostructure projektów analizy danych. cykl życia Hello opisano kroki hello, z toofinish start, która projektów wykonaj zazwyczaj, gdy są one wykonywane. Jeśli używasz innej cykl życia analizy danych, takich jak [DM WYSOKĄ](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) lub procesu niestandardowych w organizacji, można nadal używać hello opartego na zadaniach TDSP z te cykle rozwoju. 

Dla danych nauki projektów, które są przeznaczone tooship jako część inteligentnego aplikacji został zaprojektowany tego cyklu. Te aplikacje wdrażanie machine learning lub analizy sztucznego modeli analizy predykcyjnej. Poznawcze danych nauki i projektów ad hoc analytics można również korzystać z tego procesu. W takich przypadkach niektóre opisane może nie być jednak potrzebna.    

W tym miejscu jest wizualną reprezentację hello **cyklu życia procesu nauki danych zespołu**. 

![Cykl życia TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

cykl życia TDSP Hello składa się pięć etapów głównych, które są wykonywane wielokrotnie powtarzane. Należą do nich:

* **Opis biznesowa**
* **Uzyskiwanie danych i zrozumienie**
* **Modelowanie**
* **Wdrożenie**
* **Akceptacji klienta**

Na każdym etapie firma Microsoft udostępnia hello następujących informacji:

* **Cele**: hello określonych celów.
* **Jak toodo on**: hello określonych zadań opisanych i wskazówki dotyczące ich wykonanie.
* **Artefakty**: hello materiały dostarczane i hello obsługę je.


## <a name="1-business-understanding"></a>1. Poznawanie firmy

### <a name="goals"></a>Cele
* Hello **klucza zmienne** są określone, które są tooserve jako hello **modelu obiektów docelowych** których powiązane metryki są używane i określić Powodzenie hello hello projektu.
* Witaj odpowiednich **źródeł danych** są identyfikowane czy hello business ma tooobtain potrzeb tooor dostępu.

### <a name="how-toodo-it"></a>Jak toodo go
Istnieją dwa główne zadania zostały omówione w tym etapie: 

* **Zdefiniuj cele**: Praca z klientów i innych uczestników toounderstand i zidentyfikować problemy biznesowe hello. Sformułować pytania definiujące hello cele biznesowe i że celem może być techniki analizy danych.
* **Źródła danych**: Znajdź hello istotne dane, które pomaga w odpowiedzi na pytania hello, definiujące hello celami hello projektu.

#### <a name="11-define-objectives"></a>1.1 zdefiniuj cele

1. Głównym celem tego etapu jest kluczem hello tooidentify **zmienne firm** wymagane przez analizy hello toopredict. Te zmienne są hello określonego tooas **modelu obiektów docelowych** i metryki hello skojarzonych z nimi są używane toodetermine hello Powodzenie hello projektu. Dwa przykłady takich elementów docelowych to sprzedaży prognozy lub hello prawdopodobieństwo kolejności jest fałszywe.

2. Zdefiniuj hello **projektu cele** pytania i uściślenie "ostrych" pytania odpowiednich i specyficznych i jednoznaczna. Nauki danych proces hello przy użyciu nazwy i numery tooanswer takie pytania. Aby uzyskać więcej informacji na zadawanie pytań sharp, zobacz [jak toodo nauki danych](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blogu. Dane nauki / machine learning to najczęściej używanymi tooanswer pięć typów pytania:
 
   * Ile lub ile? (Regresja)
   * Kategorii? (Klasyfikacja)
   * Grupę? (klastrowania)
   * Jest to nieco dziwne? (wykrywanie anomalii)
   * Należy podjąć, która opcja? (zalecane)

    Określ, które z tych pytań są zapytaniem i jak odpowiadający osiągnięcia celów biznesowych.

3. Zdefiniuj hello **projektu zespołowego** określając hello role i obowiązki związane z jego elementów członkowskich. Opracuj plan wysokiego poziomu punktu kontrolnego, który możesz przejść na wykrywane więcej informacji.  

4. **Zdefiniowanie kryteriów sukcesu**. Na przykład: osiągnięcia klienta dokładności prognozy pochodząca z X % końca hello ten projekt 3-miesięczna tak, aby oferujemy przenoszenie tooreduce promocji. metryki Hello musi być **INTELIGENTNE**: 
   * **S**bierz określone 
   * **M**easurable
   * **A**chievable 
   * **R**elevant 
   * **T**powiązane z edytora ime 

#### <a name="12-identify-data-sources"></a>1.2 zidentyfikować źródeł danych
Zidentyfikuj źródeł danych, które zawierają przykłady znanych sharp tooyour odpowiedzi na pytania. Wyszukaj hello następujące dane:

* Dane, które są **odpowiednie** toohello pytanie. Czy mamy miary docelowej hello i funkcje, które są powiązane toohello docelowego?
* Dane, które są **dokładne miary** funkcji naszych modelu docelowego i hello zainteresowań.

Nie jest nietypowa sytuacja, na przykład toofind czy istniejącymi systemami muszą toocollect i dziennika dodatkowe rodzaje danych tooaddress hello problem i osiągnięcia celów projektu hello. W takim przypadku możesz mają toolook dla zewnętrznych źródeł danych lub zaktualizować systemy toocollect nowych danych.

### <a name="artifacts"></a>Artefakty
Poniżej przedstawiono materiałów hello na tym etapie:

* [**Karty dokumentu**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): standardowy szablon znajduje się w hello definicji struktury projektu TDSP. To jest dokument życia, który jest aktualizowane w całej hello projektu, jak zostały wprowadzone nowe funkcje odnajdywania i zmiany wymagań biznesowych. klucz Hello jest tooiterate po tego dokumentu, dodawanie w czasie wykonywania procesu odnajdywania hello więcej szczegółów. Zachowaj powitania klienta oraz innych zainteresowanych osób zajmujących wprowadzania zmian hello i dokładniej informują hello powody hello toothem zmiany.  
* [**Źródła danych**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): jest hello **źródeł danych pierwotnych** sekcji hello **definicje danych** raport, który znajduje się w projekcie TDSP hello **danych raportu**  folderu. Określa hello oryginalnego i lokalizacje docelowe dla hello nieprzetworzone dane. W późniejszym etapie należy wypełnić dodatkowe szczegóły, takie jak skrypty toomove hello danych tooyour analityczne środowiska.  
* [**Słowniki danych**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): ten dokument zawiera opisy hello dane dostarczone przez powitania klienta. Opisy te zawierają informacje o schemacie hello (typy danych, informacji na temat reguł sprawdzania poprawności, jeśli istnieje) i hello diagramy jednostki relacji, jeśli jest dostępna.


## <a name="2-data-acquisition-and-understanding"></a>2. Pozyskiwanie danych i ich analiza

### <a name="goals"></a>Cele
* Czyste, wysokiej jakości zestawu danych, których relacji toohello docelowych zmiennych są zrozumiałe który znajdują się w środowisku odpowiednie analytics hello toomodel gotowe.
* Architektura rozwiązania, hello danych potoku toorefresh i wynik danych regularnie został opracowany.

### <a name="how-toodo-it"></a>Jak toodo go
Istnieją trzy główne zadania zostały omówione w tym etapie:

* **Pozyskiwania danych hello** do środowiska analityczne hello docelowej.
* **Eksplorowanie danych hello** toodetermine Jeśli jakości danych hello jest odpowiednie tooanswer hello pytanie. 
* **Konfigurowanie potoku danych** tooscore new lub regularnie odświeżania danych.

#### <a name="21-ingest-hello-data"></a>2.1 pozyskiwania danych hello
Konfigurowanie hello procesu toomove hello danych z lokalizacji źródłowej toohello docelowych lokalizacji, gdzie operacji analizy, takich jak szkolenia i toobe wykonywane są operacje przewidywania dla. Szczegółowe informacje techniczne i opcji na toodo to z różnych usług danych Azure, zobacz temat [ładowanie danych do magazynu środowisk analizy](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 Eksplorowanie danych hello
Przed uczenia modeli, należy toodevelop dźwięku zrozumienia hello danych. Zestawy danych rzeczywistych są często naprawienie lub brakuje wartości lub ma hosta inne niezgodności. Podsumowanie danych i wizualizacji można jakości hello tooaudit używanych danych i informacje hello potrzebne tooprocess hello danych z przed jest gotowa do modelowania. Ten proces jest często iteracji.

TDSP zapewnia automatyczne narzędzie o nazwie [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp wizualizacji danych hello i przygotowania danych Raporty podsumowujące. Firma Microsoft zaleca, począwszy od IDEAR pierwszy tooexplore hello danych toohelp zrozumienia początkowe dane z interaktywnie nie kodowania, a następnie wpisz niestandardowy kod Eksploracja danych i wizualizacji. Aby uzyskać wskazówki dotyczące czyszczenia danych hello, zobacz [tooprepare danych do uczenia maszynowego rozszerzone zadań](machine-learning-data-science-prepare-data.md).  

Po zakończeniu hello jakości danych hello oczyszczone hello następnym krokiem jest toobetter zrozumieć wzorce hello, które są związane z hello danych, które pomagają wybrać i utworzyć odpowiedni model predykcyjny docelowego. Poszukaj dowód jak hello połączonych danych jest toohello docelowym i czy brak wystarczających danych toomove do przodu z hello następne kroki modelowania. Ponownie ten proces jest często iteracji. Toofind nowych źródeł danych może być konieczne z bardziej trafna lub więcej danych tooaugment hello dataset początkowo objęci hello poprzedniego etapu.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 Konfigurowanie potoku danych
Ponadto toohello początkowej wprowadzanie i czyszczenie hello danych, zazwyczaj należy tooset procesu tooscore nowych danych lub odświeżanie danych hello regularnie jako część procesu trwającą learning. Można to zrobić, konfigurując potoku danych lub przepływ pracy. Oto [przykład](machine-learning-data-science-move-sql-azure-adf.md) jak tooset się potok wraz z [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/). 

Na tym etapie zaprojektowano w potoku danych hello architektury rozwiązania. potoku Hello jest również opracowany równolegle z hello następujące etapy hello danych nauki projektu. potoku Hello może być oparta na partii lub przesyłania strumieniowego/real-jednorazowej lub hybrydowego, w zależności od firmy wymaga i hello ograniczenia istniejących systemów w których jest integrowana tego rozwiązania. 

### <a name="artifacts"></a>Artefakty
Witaj poniżej przedstawiono materiałów hello na tym etapie.

* [**Raport jakości danych**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): Ten raport zawiera relacje między każdego atrybutu i docelowy, zmienna Klasyfikacja hello itp. dane podsumowania [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) narzędzie jako część TDSP mogą szybko generować Ten raport w żadnych tabelarycznym zestawu danych, takich jak plik CSV lub relacyjne tabeli. 
* **Architektura rozwiązania**: może to być diagramu lub opis danych potoku używany toorun oceniania lub prognoz na nowe dane po skonstruowaniu modelu. Zawiera ona także tooretrain potoku hello modelu na podstawie nowych danych. dokument Hello jest przechowywany w hello [projektu](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) katalogu, korzystając z szablonu struktury katalogu TDSP hello.
* **Punkt kontrolny decyzji**: przed rozpoczęciem inżynieryjne wszystkich funkcji i konstruowania modelu należy można obliczyć ponownie toodetermine projektu hello czy oczekiwaną wartość hello jest wystarczające toocontinue pursing go. Możesz, na przykład być gotowe tooproceed, toocollect potrzeby większej ilości danych lub Porzuć hello projektu jako hello danych nie istnieje tooanswer hello pytanie.


## <a name="3-modeling"></a>3. Modelowanie

### <a name="goals"></a>Cele
* Funkcje optymalne danych modelu uczenia maszynowego hello.
* Szczegółowy ML model przewiduje docelowy hello najbardziej dokładnie.
* Model uczenia Maszynowego, który nadaje się do produkcji.

### <a name="how-toodo-it"></a>Jak toodo go
Istnieją trzy główne zadania zostały omówione w tym etapie:

* **Inżynieria**: Tworzenie funkcji danych z hello nieprzetworzone dane toofacilitate modelu szkolenia.
* **Model uczenia**: znaleźć hello modelu to pytanie hello odpowiedzi najdokładniej porównując ich metryki sukcesu.
* Określa, czy model jest **odpowiednie do produkcji**.

#### <a name="31-feature-engineering"></a>3.1 Inżynieria
Funkcja engineering obejmuje dołączania, agregacji i przekształcenie toocreate zmienne pierwotne hello funkcji używanych w hello analizy. Chcąc wgląd w przyczyn nadmiernego modelu, należy toounderstand jak funkcje są inne pokrewne tooeach i jak algorytmów uczenia maszynowego hello są toouse tych funkcji. Ten krok wymaga creative kombinację doświadczenia z domeny i informacje uzyskane w kroku Eksploracja danych hello. To działanie znajdowania i tym informacyjny zmienne unikając zbyt wiele zmiennych niepowiązanych. Zmienne informacyjny poprawy naszych wyników; zmienne niepowiązanych wprowadzić powstanie niepotrzebnego szumu hello modelu. Należy również toogenerate te funkcje wszelkie nowe dane uzyskane podczas oceniania. Tak generowania hello tych funkcji można tylko zależą od danych, który jest dostępny w czasie hello oceniania. Techniczne wskazówki dotyczące funkcji zespołu inżynieryjnego, korzystając z różnych technologii danych Azure, zobacz [Inżynieria w hello proces nauki danych](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 modelu szkolenia
W zależności od typu zapytania, które próbujesz odpowiedzi Brak dostępnych wiele algorytmów modelowania. Aby uzyskać wskazówki dotyczące wybierania algorytmów hello, zobacz [jak toochoose algorytmów uczenia maszynowego Azure Microsoft](machine-learning-algorithm-choice.md). Chociaż ten artykuł jest przeznaczony dla usługi Azure Machine Learning, hello wskazówki zapewnia jest przydatne w przypadku maszyn uczenia projektów. 

proces Hello szkolenia modelu obejmuje hello następujące kroki: 

* **Dane wejściowe hello podziału** losowo do modelowania szkoleniowy zestaw danych i testowego zestawu danych.
* **Tworzenie modeli hello** przy użyciu hello szkoleniowy zestaw danych.
* **Ocena** (szkolenia i testowego zestawu danych) szereg konkurencyjnych maszyny algorytmów wraz z hello uczenia skojarzone dostrajanie parametrów (znany jako parametr odchylenia) adresowana udzielenie odpowiedzi na pytanie hello płynących z hello bieżące dane.
* **Określić rozwiązania "Najważniejsze" hello** tooanswer hello pytanie, porównując metryki sukcesu hello między alternatywne metody.

> [!NOTE]
> **Uniknąć wycieków**: wycieku danych może być spowodowana przez włączenie hello danych z poza hello szkolenia zestaw danych umożliwia modelu lub algorytmu uczenia maszynowego toomake nierealistycznie dobrej prognoz. Wyciek jest typową przyczyną Dlaczego analityków danych uzyskać nerwowe otrzymują oni predykcyjnej wyniki, które wydają się zbyt dobrej toobe wartość true. Te zależności można toodetect twardych. wyciek tooavoid często wymaga iteracja między kompilowania zestawu danych analizy, tworzenie modelu i oceny hello dokładności. 
> 
> 

Firma Microsoft udostępnia [narzędzie automatycznego modelowania i raportowania](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) z TDSP stanie toorun przez wiele algorytmów i parametr wachlarzy tooproduce modelu linii bazowej. Tworzy linię bazową modelowania podsumowania wydajności każdego modelu wraz z kombinacją parametrów zmiennej znaczenie w tym raporcie. Ten proces ma charakter iteracyjny również, jak można dysku dalsze engineering funkcji. 

### <a name="artifacts"></a>Artefakty
Artefakty Hello utworzone na tym etapie obejmują:

* [**Zestawy funkcji**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): funkcje hello utworzonych dla modelowania hello są opisane w hello **zestawy funkcji** sekcji hello **definicji danych** raportu. Zawiera wskaźniki toohello kodu toogenerate hello funkcje i opis na jak funkcja hello został wygenerowany.
* [**Model raportu**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): dla każdego modelu, który zostanie podjęta próba, standard, jest generowany na podstawie szablonu raportu, który zawiera szczegóły dotyczące każdego doświadczenia.
* **Decyzja punktu kontrolnego**: oceny, czy hello model wykonuje również za mało toodeploy on tooa systemu produkcji. Niektóre tooask ważne pytania są:
  * Hello modelu odpowiedzi hello pytanie bez obaw wystarczające podane dane testowe hello? 
  * Spróbuj użyć dowolnego alternatywnych metod: gromadzenie dodatkowych danych, czy więcej engineering funkcji lub wypróbować inne algorytmy?


## <a name="4-deployment"></a>4. Wdrożenie

### <a name="goal"></a>Cel
* Modele z potokiem danych są tooa wdrożone w środowisku produkcyjnym lub środowiska przypominającej środowisko produkcyjne dla użytkowników końcowych. 

### <a name="how-toodo-it"></a>Jak toodo go
zadania główne Hello zostały omówione w tym etapie:

* **Operacjonalizuj modelu hello**: Wdrażanie hello modelu i potoku tooa lub środowiska przypominającej środowisko produkcyjne korzystania z aplikacji.

#### <a name="41-operationalize-a-model"></a>4.1 operacjonalizacji modelu
Po utworzeniu zestaw modeli, które również wykonywać, może być operationalized dla tooconsume inne aplikacje. W zależności od wymagań biznesowych hello prognoz są wykonywane w czasie rzeczywistym lub na podstawie partii. toobe operationalized, modele hello mają toobe widoczne z interfejsem API otwarty łatwo jest używane z różnych aplikacji, takich jak witryny sieci Web w trybie online, arkusze kalkulacyjne, pulpity nawigacyjne lub aplikacje biznesowe i wewnętrznej bazy danych. Przykłady operationalization modelu z usługą sieci web uczenie maszynowe Azure można znaleźć [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md). Jest również najważniejsze dane telemetryczne toobuild praktyki i monitorowanie na hello modelu produkcji i hello toohelp potoku wdrożyć dane o stanie systemu kolejnych raportowania i rozwiązywania problemów.  

### <a name="artifacts"></a>Artefakty
* Pulpit nawigacyjny stanu z systemu metryki kondycji i klucza.
* Raport końcowy modelowania z szczegóły wdrożenia.
* Dokument architektury rozwiązania final.

## <a name="5-customer-acceptance"></a>5. Akceptacja klienta

### <a name="goal"></a>Cel
* **Finalizuj elementów dostarczanych projektu hello**: Sprawdź, czy hello potoku, hello modelu i ich wdrażania w środowisku produkcyjnym są spełniającą cele klienta.

### <a name="how-toodo-it"></a>Jak toodo go
Istnieją dwa główne zadania zostały omówione w tym etapie:

* **System sprawdzania poprawności**: Potwierdź modelu hello wdrożone i potoku spełniają potrzeb klientów.
* **Projekt ręcznie wyłączyć**: toohello jednostki, która jest toorun hello system w środowisku produkcyjnym.

powitania klienta należy zweryfikować, czy hello system spełnia ich potrzeb biznesowych i odpowiedzi hello hello pytania z dopuszczalnych dokładność toodeploy hello systemu tooproduction do użytku przez ich aplikacji klienckiej. Cała dokumentacja hello sfinalizowana, a sprawdzone. Ręcznie wyłączyć odpowiedzialny za operacje jednostki toohello projektu hello jest ukończona. Ta jednostka można na przykład IT lub zespołu nauki danych klienta albo agent powitania klienta, który odpowiada za uruchamianie systemu hello w środowisku produkcyjnym. 

### <a name="artifacts"></a>Artefakty
Hello artefaktu głównego wygenerowane w tym ostatnim krokiem jest hello **zakończenia raportu z projektu dla klienta**. Jest hello raport techniczne zawierający wszystkie szczegóły projektu hello tego toolearn przydatne informacje i stosować hello system. [Zakończenia raportu](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) szablonu jest zapewniana przez TDSP, która może być używany jako jest lub dostosować dla określonego klienta. 

## <a name="summary"></a>Podsumowanie
Witaj [cyklu życia procesu nauki danych zespołu](http://aka.ms/datascienceprocess) zgodnie z modelem jest odpowiednio sekwencję powtórzyć kroki, które zawierają wskazówki dotyczące zadań hello toouse modeli predykcyjnych. Modele te można wdrożyć w środowisku toobe wykorzystywana toobuild inteligentnego aplikacje produkcyjne. Celem Hello tego cyklu procesu jest toomove toocontinue danych nauki projektu do przodu do punktu końcowego wyczyść zaangażowania. Mimo że jest spełniony, że nauki danych jest procesem badania i odnajdywania, jest w stanie tooclearly komunikują się te zadania tooyour zespołu i klientów przy użyciu zestawu jasno określone artefaktów pomagające pracownikom standardowych szablonów uniknąć niezrozumienia i zwiększyć prawdopodobieństwo hello pomyślne zakończenie dane złożone nauki projektu.

## <a name="next-steps"></a>Następne kroki
Pełne end-to-end wskazówki, które pokazują wszystkie kroki procesu hello hello **określonych scenariuszy** podawane są również. Wymieniono i połączone z opisami miniatur w hello [wskazówki dotyczące procesu nauki danych zespołu](data-science-process-walkthroughs.md) tematu.

