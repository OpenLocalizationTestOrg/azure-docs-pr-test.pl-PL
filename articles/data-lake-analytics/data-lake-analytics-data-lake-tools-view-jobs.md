---
title: "aaaUse przeglądarki zadania i zadania dla zadań usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse przeglądarki zadania i zadania dla zadań usługi Azure Data Lake Analytics. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Użyj przeglądarki zadania i widoku zadania dla zadań usługi Azure Data lake Analytics
Witaj archiwa usługi Azure Data Lake Analytics przesłać zadania w [magazyn zapytań](#query-store). W tym artykule dowiesz się, jak toouse przeglądarki zadania i widoku zadania w narzędzia Azure Data Lake Tools dla Visual Studio toofind hello historycznych zadanie informacji. 

Domyślnie program hello usługi Data Lake Analytics archiwa hello zadania przez 30 dni. Konfigurując zasady wygasania hello dostosowane z hello portalu Azure można skonfigurować okres ważności Hello. Nie będzie możliwe tooaccess informacje o zadaniu powitania po wygaśnięciu. 

## <a name="prerequisites"></a>Wymagania wstępne
Zobacz [narzędzi Data Lake Tools dla Visual Studio wymagania wstępne](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Otwórz hello przeglądarki zadania
Dostęp hello przeglądarki zadania za pomocą **Eksploratora serwera > Azure > Data Lake Analytics > zadań** w programie Visual Studio.  Witaj przeglądarki zadania są dostępne magazynu zapytań hello konta usługi Data Lake Analytics. Przeglądarki zadania są magazynu zapytań na powitania po lewej, wyświetlane informacje podstawowe zadania, a następnie Wyświetl zadania na powitania prawo przedstawiający szczegółowe informacje o zadania.

## <a name="job-view"></a>Zadania widoku
Zadania widoku przedstawia hello szczegółowe informacje o zadaniu. tooopen zadania, kliknij dwukrotnie pozycję zadania w hello zadania przeglądarki lub otworzyć z menu usługi Data Lake hello, klikając widoku zadania. Powinny zostać wyświetlone okno dialogowe wypełniane przy użyciu adresu URL zadania hello.

![Data Lake Tools przeglądarki zadania programu Visual Studio](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

Zadania widoku zawiera:

* Podsumowanie zadania
  
    Odśwież hello widoku zadania toosee hello nowych informacji o uruchomionych zadań.
  
  * Stan zadania (wykres):
    
      Stan zadania zawiera opis etapów zadania hello:
    
      ![Fazy stan zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Przygotowanie: Przekaż chmury toohello skryptu, kompilowania i optymalizowanie przy użyciu usługi kompilacji hello skryptu hello.
    * W kolejce: Zadania są serwatki umieszczonych w kolejce, które czekają za mało zasobów lub zadania hello przekracza maksymalną równoczesnych zadań hello na ograniczenie konta. ustawienia priorytetu Hello określa hello sekwencji zadań w kolejce - hello mniejszą liczbę hello, wyższy priorytet hello hello.
    * Uruchomiona: zadanie hello rzeczywiście jest uruchomiona na koncie usługi Data Lake Analytics.
    * Finalizowanie: kończy zadanie hello (na przykład finalizowanie hello pliku).
      
      zadanie Hello może zakończyć się niepowodzeniem na każdym etapie. Na przykład błędy kompilacji hello Preparing fazy, błędy przekroczenia limitu czasu w fazie w kolejce hello i wykonywania błędów w fazie uruchamiania hello itp.
  * Podstawowe informacje
    
      Pokazuje informacje podstawowe zadania Hello w dolnej części hello hello panel Podsumowanie zadania.
    
      ![Fazy stan zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Wynik zadania: Powodzeniem lub niepowodzeniem. zadanie Hello może zakończyć się niepowodzeniem na każdym etapie.
    * Łączny czas trwania: Ścian czasu zegara (czas trwania) między przesyłanie czas i czas zakończenia.
    * Łączny czas obliczeniowe: hello sumę czas wykonywania każdego wierzchołka, można rozważyć się, że jej jako hello czasu hello zadania są wykonywane w tylko jednego wierzchołka. Toofind wierzchołków tooTotal można znaleźć więcej informacji na temat wierzchołka.
    * Czas przesyłania/rozpoczęcia/zakończenia: hello czas, kiedy hello usługi Data Lake Analytics otrzyma hello toorun przesyłanie/uruchamia zadanie zadania/zakończenia zadania hello pomyślnie lub nie.
    * Kompilacji/w kolejce/uruchomiona: Czas zegarowy spędzony w fazie Preparing/w kolejce/uruchomiony hello.
    * Konto: konto usługi Data Lake Analytics hello używane do uruchamiania zadania hello.
    * Autor: hello użytkownika, który przesłał zadanie hello, może to być konto tworzy prawdziwa osoba lub konta system.
    * Priorytet: priorytet hello hello zadania. Witaj hello niższą, wyższy priorytet hello hello. Wpływa tylko na powitania sekwencji zadań hello w kolejce hello. Ustawienie wyższy priorytet nie zastępują uruchomionych zadań.
    * Równoległość: hello zażądał maksymalną liczbę równoczesnych Azure danych Lake Analytics jednostek (ADLAUs), alias wierzchołków. Obecnie jednego wierzchołka jest równy tooone maszyny Wirtualnej z dwóch wirtualnego rdzeni i 6 GB pamięci RAM, ale można jej uaktualnić w przyszłości usługi Data Lake Analytics aktualizacji.
    * Bajtów w lewo: Bajtów wymagające toobe przetwarzane dopiero po zakończeniu zadania hello.
    * Odczyt/zapisanych bajtów: bajtów, które zostały odczytana/zapisana, od momentu uruchomienia zadania hello.
    * Łącznie wierzchołków: hello zadania został podzielony na wiele elementów pracy, każdy element pracy jest nazywany wierzchołka. Ta wartość opisuje, ile zadania hello elementów pracy składa się z. Należy rozważyć wierzchołek jako jednostka podstawowy proces alias Azure Data Lake Analytics jednostki (ADLAU), i wierzchołków mogą być uruchamiane w równoległości. 
    * Ukończono/uruchomiona/nie powiodło się: hello liczba wierzchołków zakończone lub uruchomiona/nie powiodła się. Wierzchołki może zakończyć się niepowodzeniem ze względu na błędy użytkowników tooboth kodu i systemu, ale system hello liczbę ponownych prób nie wierzchołków automatycznie kilka razy. Jeśli wierzchołków hello nadal nie powiodło się po ponowieniu próby, całą pracę hello zakończy się niepowodzeniem.
* Wykres zadania
  
    Skrypt U-SQL reprezentuje logiki hello przekształcania danych toooutput danych wejściowych. skrypt Hello jest kompilowane i optymalizowane plan wykonania fizycznego tooa w fazie Preparing hello. Wykres zadania jest plan wykonania fizycznego hello tooshow.  powitania po diagram przedstawia proces hello:
  
    ![Fazy stan zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Zadanie jest podzielony na wiele elementów pracy. Każdy element pracy jest nazywany wierzchołka. wierzchołki Hello są zgrupowane jako Super wierzchołków (alias etap) i wizualizowane jako wykres zadania. tabliczek zielony etap Hello wykresie zadania hello Pokaż hello etapach.
  
    Każdy wierzchołek w fazie wykonuje hello sam rodzaj pracy z różnych części hello same dane. Na przykład jeśli plik z jednego TB danych, a setki wierzchołków odczytywania z niego, każde z nich jest odczytu fragmentu. Te wierzchołków są pogrupowane w hello tego samego etapu i ten sam działają w różnych części tego samego pliku wejściowego.
  
  * <a name="state-information"></a>Etap informacji
    
      W szczególności etapie w plakietkę hello przedstawiono niektóre liczby.
    
      ![Wykres etap zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Wyodrębnij: Nazwa hello etapu, o nazwie za pomocą numeru i hello metody operacji.
    * 84 wierzchołków: hello łączna liczba wierzchołki na tym etapie. Rysunek Hello wskazuje, ile elementów pracy jest podzielona na tym etapie.
    * 12.90 s/wierzchołków: hello wierzchołków Średni czas wykonania dla tego etapu. Liczba ta jest obliczana na podstawie sumy (co czas wykonania wierzchołka) / (całkowita liczba wierzchołków). Co oznacza, że jeśli można przypisać wszystkich wierzchołków hello wykonywane w równoległości, hello całej operacji w 12.90 s. Oznacza to również, jeśli wszystkie hello w pracy tego etapu jest wykonywane szeregowo, hello koszt wyniesie #vertices * Średni czas.
    * 850,895 wierszy, zapisany: łączna liczba wierszy, zapisany na tym etapie.
    * R/W: ilość danych odczytu/Written na tym etapie w bajtach.
    * Kolory: Kolory hello etap tooindicate wierzchołków inny stan.
      
      * Zielony oznacza, że wierzchołków hello jest zakończyło się pomyślnie.
      * Kolor pomarańczowy wskazuje, że próba zostanie ponowiona hello wierzchołka. wierzchołków Hello ponowione nie powiodło się, ale próba zostanie ponowiona automatycznie i pomyślnie systemu hello i hello ogólną etap zakończyło się powodzeniem. Jeśli wierzchołków hello ponowione, ale nadal nie powiodło się, kolor hello włącza czerwony i hello całego zadania nie powiodło się.
      * Czerwony oznacza nie powiodło się, co oznacza, że niektóre wierzchołek ma została podjęta przez hello system kilka razy, ale nadal nie powiodło się. Ten scenariusz powoduje hello toofail całego zadania.
      * Niebieski oznacza, że niektóre wierzchołek jest uruchomiona.
      * Białe wskazuje hello oczekuje wierzchołka. wierzchołków Hello może być oczekiwanie toobe zaplanowane po udostępnieniu ADLAU lub może go oczekuje na dane wejściowe od czasu jej danych wejściowych może nie być gotowy.
      
      Więcej szczegółów można znaleźć na etapie hello, ustawiając kursor kursor myszy przez jednego stanu:
      
      ![Wykres etap szczegóły zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Wierzchołków: Opisuje hello wierzchołków uzyskać szczegółowe informacje, na przykład, ile wierzchołków łączną liczbę wierzchołków zostały ukończone, są nie powiodło się lub jest nadal uruchomiona/oczekiwanie itp.
  * Dane odczytane pod między/wewnątrz: pliki i dane są przechowywane w wielu stanowiskami w rozproszonym systemie plików. tutaj wartość Hello opisano, jak dużo danych został odczytany w hello tej samej pod lub granic pod.
  * Całkowity czas obliczeniowe: Suma hello co czas wykonywania wierzchołków w etapie hello, można rozważyć go jako czas hello zajmie, jeśli wszystkie działają na etapie hello są wykonywane w tylko jednego wierzchołka.
  * Dane i zapisywane odczytu wierszy: wskazuje, ile danych wierszy zostać odczytana/zapisana lub wymagają toobe odczytu.
  * Wierzchołka odczytywać błędów: w tym artykule opisano, jak wiele wierzchołków są nie powiodło się podczas odczytu danych.
  * Odrzuca wierzchołków zduplikowane: w przypadku wierzchołek działa zbyt wolno, hello systemu może planować wierzchołków wielu toorun hello sam element pracy. Wierzchołki reductant zostaną odrzucone po jednej wierzchołków hello pomyślnie. Zduplikowane wierzchołków odrzuca rekordy hello liczbę wierzchołków, które zostaną odrzucone jako powtórzeń na etapie hello.
  * Odwołania wierzchołków: hello wierzchołków powiodła się, ale uzyskać ponownie uruchomić później powodu toosome powodów. Na przykład jeśli podrzędne wierzchołków utraci pośrednich danych wejściowych, jest pytanie hello toorerun wierzchołków nadrzędnego.
  * Wierzchołków harmonogram wykonaniami: hello całkowity czas, który zaplanowano hello wierzchołków.
  * Dane wierzchołków średni/min/Max odczytane: hello średni/minimum/maksimum każdego wierzchołka odczytywać dane.
  * Czas trwania: hello czas zegarowy podejmowaną etap, należy toosee profilu tooload tej wartości.
  * Odtwarzanie zadania
    
      Data Lake Analytics uruchamia zadania i archiwa hello wierzchołków systemem informacji hello zadań, takich jak uruchomienia wierzchołków hello, zatrzymana, nie powiodło się i jak są zwalniane itp. Wszystkie informacje hello jest automatycznie rejestrowane w magazynie zapytań hello i przechowywane w profilu zadania. Możesz pobrać hello profilu zadania za pomocą "Załaduj profil" w widoku zadania i można wyświetlić hello odtwarzania zadania po pobraniu hello profilu zadania.
    
      Odtwarzanie zadania jest wizualizację epitome co się stało hello klastra. Pomaga obserwowanie postępu wykonywania zadania oraz wzrokowe wykrycie anomalii wydajności i wąskich gardeł w krótkim czasie (mniej niż 30s zwykle).
  * Ekran mapy interakcji zadania 
    
      Mapa cieplna zadania można określić za pomocą listy rozwijanej wyświetlanej hello wykresie zadania. 
    
      ![Ekran mapy sterty wykresu zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Przedstawia on hello Mapa cieplna we/wy, czas i przepływności zadania, za pomocą których można znaleźć gdzie zadania hello spędza w większości przypadków hello lub czy zadanie jest zadaniem granic We/Wy i tak dalej.
    
      ![Przykład mapy sterty wykresu zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Postęp: hello postęp wykonywania zadania, zobacz informacje w [przemieszczanie informacji](#stage-information).
    * Dane odczytana/zapisana: hello Mapa cieplna całkowita danych odczytana/zapisana na każdym etapie.
    * Godziny obliczeniowe: hello Mapa cieplna sum (co czas wykonania wierzchołka), można rozważyć to jak długo zajmie, jeśli wszystkie prace na etapie hello jest wykonywane z tylko 1 wierzchołka.
    * Średni czas wykonania węzła: hello Mapa cieplna sum (co czas wykonania wierzchołka) / (liczba wierzchołków). Co oznacza, jeżeli można przypisać wszystkich wierzchołków hello wykonywane w równoległości, etap całego hello zostaną wykonane, w tym przedziale czasu.
    * Przepływność wejścia/wyjścia: hello Mapa cieplna przepustowość operacji We/Wy każdego etapu, można potwierdzić, jeśli zadanie jest powiązane zadanie we/wy przez to.
* Operacji na metadanych
  
    Można wykonać operacji na metadanych za pomocą skryptu U-SQL, takich jak tworzenie bazy danych, drop table itd. Te operacje są wyświetlane w metadanych operacji po kompilacji. Może znaleźć potwierdzeń, Utwórz jednostki, w tym miejscu upuść jednostek.
  
    ![Azure Data Lake Analytics zadania widoku operacji na metadanych](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Historia stanu
  
    Hello historii stanu również wizualizacji w Podsumowanie zadania, ale można uzyskać więcej informacji w tym miejscu. Można znaleźć hello szczegółowe informacje, takie jak kiedy zadanie hello jest gotowa, kolejce uruchomienia, została zakończona. Również można znaleźć ile razy został skompilowany hello zadania (hello CcsAttempts: 1), gdy jest rzeczywiście hello zadania wysłane toohello klastra (hello szczegółów: wysyłki toocluster zadania) itp.
  
    ![Historia stanu usługi Azure Data Lake Analytics zadania widoku](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnostyka
  
    Narzędzie Hello automatycznie diagnozuje wykonywania zadania. W przypadku błędów lub problemów z wydajnością w zadaniach zostaną wysłane alerty. Należy pamiętać, należy toodownload profilu tooget pełne informacje w tym miejscu. 
  
    ![Diagnostyka Azure Data Lake Analytics zadania widoku](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Ostrzeżenia: Alertu zostaną wyświetlone tutaj z ostrzeżeniem kompilatora. Możesz kliknąć toohave link "x problemów" szczegółowe po wyświetleniu alertu hello.
  * Wierzchołków Uruchom za długa: Jeśli dowolny z wierzchołków przekroczyły limit czasu (np. 5 godzin), problemy zostaną znalezione w tym miejscu.
  * Użycie zasobów: Jeżeli równoległości więcej lub za mało są przydzielone niż konieczne, problemów będzie można znaleźć tutaj. Również kliknij toosee użycia zasobów więcej szczegółowych informacji i wykonać toofind scenariusze warunkowej lepsze alokacji zasobów (Aby uzyskać więcej informacji, zobacz w tym przewodniku).
  * Sprawdzanie pamięci: Jeśli dowolny z wierzchołków korzysta z więcej niż 5 GB pamięci, problemy zostaną znalezione w tym miejscu. Wykonanie zadania może pobrać przerwany przez system, gdy jest używana większa ilość pamięci niż ograniczenie systemu.

## <a name="job-detail"></a>Szczegóły zadania
Szczegóły zadania pokazuje hello szczegółowe informacje hello zadania, w tym skryptu, zasobów i widoku wykonania wierzchołka.

![Szczegóły zadania usługi Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Skrypt
  
    Witaj skryptu U-SQL zadania hello jest przechowywany w magazynie zapytań hello. Można wyświetlać hello oryginalny skrypt U-SQL i ponownie prześlij, jeśli to konieczne.
* Zasoby
  
    Można znaleźć hello: zadanie dane wyjściowe kompilacji przechowywane w magazynie zapytań hello przy użyciu zasobów. Na przykład można znaleźć "algebra.xml", które jest używane tooshow hello wykres zadania, zestawy hello, który został zarejestrowany, itp. w tym miejscu.
* Widoku wykonania wierzchołka
  
    Zawiera on wierzchołków szczegóły wykonywania. Witaj profilu zadania archiwa co dziennika wykonywania wierzchołków, takie jak łączna ilość danych odczytana/zapisana, runtime, stan itd. Za pomocą tego widoku można uzyskać więcej informacji na temat sposobu uruchomienia zadania. Aby uzyskać więcej informacji, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Następne kroki
* informacje diagnostyczne toolog, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* widoku wykonania wierzchołka toouse, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

