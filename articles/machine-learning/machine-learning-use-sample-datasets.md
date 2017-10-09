---
title: "zestawy aaaUse hello przykładowych danych w usłudze Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Opisy hello zestawów danych używany w Przykładowe modele uwzględnione w usłudze Machine Learning Studio. Te przykładowych zestawów danych można użyć do eksperymentów."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Użyj hello przykładowych zestawów danych w usłudze Azure Machine Learning Studio
[top]: #machine-learning-sample-datasets

Po utworzeniu nowego obszaru roboczego w usłudze Azure Machine Learning szereg przykładowych zestawów danych i eksperymenty są domyślnie dołączone. Wiele z tych przykładowych zestawów danych są używane przez hello Przykładowe modele w hello [Azure Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/). Inne są dołączone jako przykłady różnych typów danych zwykle używanych w uczeniu maszynowym.

Niektóre z tych zestawów danych są dostępne w magazynie obiektów Blob Azure. Dla tych zestawów danych hello w poniższej tabeli zapewnia bezpośrednie połączenie. Te zestawy danych można użyć w eksperymentów, za pomocą hello [i zaimportuj dane] [ import-data] modułu.

pozostałe Hello tych przykładowych zestawów danych są dostępne w obszarze roboczym w obszarze **zapisane zestawów danych** w hello modułu palety toohello lewej kanwy eksperymentu hello podczas otwierania lub utworzyć nowy eksperyment w usłudze Machine Learning Studio.
Można użyć dowolnej z tych zestawów danych w eksperymencie własnych przeciągając tooyour kanwy eksperymentu.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Nazwa zestawu danych</th>
  <th align=left>Opis zestawu danych</th>
</tr>

<tr>
  <td valign=top>Dla dorosłych klasyfikacji binarnej dochodu spisu zestawu danych.</td>
  <td valign=top>
Podzbiór hello 1994 r. spisu bazy danych, przy użyciu osoby dorosłe pracy nad wieku hello 16 z indeksem skorygowaną dochodu > 100.<p> </p><b>Sposób użycia:</b> klasyfikowania osoby za pomocą toopredict demograficznych, czy osoba uzyskuje ponad 50 K rocznie.<p> </p><b>Powiązane Research:</b> Kohavi, R., Becker B., (1996). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Zestaw danych kodów lotnisku</td>
  <td valign=top>
Kody lotnisku Stanów Zjednoczonych.<p> </p>Ten zestaw danych zawiera jeden wiersz dla każdego lotnisku USA, zapewniając hello lotnisku identyfikator i nazwa wraz z hello lokalizacji miejscowość i województwo.
  </td>
</tr>

<tr>
  <td valign=top>Cen samochodów, data (Raw)</td>
  <td valign=top>
Informacje o samochodów przez producent i model, w tym ceny hello, funkcje, takie jak liczba hello cylindrów i MPG, a także oceny ryzyka ubezpieczenia.<p> </p>oceny ryzyka Hello jest początkowo skojarzony z automatycznego ceny i następnie dostosowana do rzeczywistego zagrożenia w procesie nazywanym tooactuaries jako symboling. Wartość + 3 wskazuje, że automatyczne hello jest ryzykowne i wartość -3 jego jest prawdopodobnie bezpieczne.<p> </p><b>Sposób użycia:</b> oceny ryzyka hello prognozowania przez funkcje za pomocą regresji lub multivariate klasyfikacji. <p> </p><b>Powiązane Research:</b> Schlimmer, J.C. (1987). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Zestaw danych UCI wynajem roweru</td>
  <td valign=top>
Dzierżawa roweru UCI zestawu danych, który bazuje na prawdziwe dane z Bikeshare kapitału firmy, która obsługuje sieci wynajem roweru w stanie Waszyngton kontrolera domeny.<p> </p>Witaj dataset zawiera jeden wiersz dla każdej godziny dziennie 2011 i 2012, łącznie 17,379 wierszy. zakres Hello co godzinę roweru dzierżawy jest z 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Obraz RGB rachunku bramy</td>
  <td valign=top>
Plik obrazu publicznie dostępnych przekonwertować tooCSV danych.<p> </p>Witaj kod do konwersji obraz powitania znajduje się w hello <strong>kolor podziału korzystania z klastra K-średnich</strong> strony szczegółów modelu.
  </td>
</tr>

<tr>
  <td valign=top>Krwi pobrania danych</td>
  <td valign=top>
Podzbiór danych z hello krwi dawcy bazy danych hello transfuzji krwi Service Center Hsin Chu Miasto, Tajwan.<p> </p>Dane dawcy obejmują hello miesięcy od czasu ostatniego pobrania), a częstotliwość lub hello całkowitą liczbę pobrań, czas od ostatniego pobrania, a ilość krwi przekazywana.<p> </p><b>Sposób użycia:</b> hello celem jest toopredict za pośrednictwem klasyfikacji, czy dawcy hello przekazywana krwi marca 2007, gdzie 1 oznacza dawcy okresie docelowy hello i 0 z systemem innym niż dawcy. <p> </p><b>Powiązane Research:</b> Yeh I.C., (2008). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki <p> </p>Yeh,-Cheng, Yang, króla-Jang i notatki, Tao-Ming "odnajdywania wiedzy w tryb RFM modelu przy użyciu sekwencji Bernoulliego" systemów ekspertów z aplikacjami, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Przeglądy książki z Amazon</td>
  <td valign=top>
Przeglądy książek w Amazon, pobranych z witryny sieci Web amazon.com hello przez pracowników naukowo-badawczych University Pennsylvania (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">wskaźniki nastrojów klientów</a>). Zobacz dokument research Witaj, "Biographies, Bollywood, wysięgnik pola i mieszalni: dostosowanie domeny klasyfikacji wskaźniki nastrojów klientów" Blitzer Jan, oznacz Dredze i Fernando Pereira; Skojarzenie Linguistics obliczeniową (ACL), 2007.<p> </p>Witaj oryginalnego zestawu danych ma przeglądami 975K o klasyfikacji, 1, 2, 3, 4 i 5. przeglądy Hello napisanych w języku angielskim i pochodzą z hello okresie 1997 2007. Ten zestaw danych został przeglądami too10K próbkowany w dół.
  </td>
</tr>

<tr>
  <td valign=top>Dane raka piersi</td>
  <td valign=top>
Jeden z trzech zestawów związanych z raka danych, udostępnione przez Instytut Oncology, który pojawia się często w machine learning materiały hello. Łączy informacje diagnostyczne z funkcjami z analizy laboratorium hodowlami około 300.<p> </p><b>Sposób użycia:</b> klasyfikowania typu hello raka, oparte na atrybutach 9, niektóre z nich liniowej i niektóre są podzielone na kategorie. <p> </p><b>Powiązane Research:</b> O.L. Wohlberg, W.H., ulicy, W.N. i Mangasarian, (1995). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Funkcje raka piersi <td valign=top>
Hello dataset zawiera informacje regionów podejrzane 102K (kandydatów) obrazów rentgenowskie każdego opisanego przez funkcje 117. Funkcje Hello są unikatowe i ich znaczenie nie została ujawniona przez hello twórców zestawu danych (opieki zdrowotnej Siemens). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Informacje o raka piersi</td>
  <td valign=top>
zestaw danych Hello zawiera dodatkowe informacje dla każdego podejrzanego obszaru rentgenowskie obrazu. Każdy przykład zawiera informacje (np. etykiety, pacjenta identyfikator, współrzędnych poprawki względną toohello całego obrazu) o hello jej numer wiersza w zestawie danych funkcji raka piersi hello. Każdy pacjenta ma wiele przykładów. Dla pacjentów, którzy mają raka Oto kilka przykładów dodatnią, a inne ujemna. Dla pacjentów, którzy nie mają raka wszystkie przykłady jest ujemna. Witaj dataset zawiera przykłady 102K. ukierunkowane Hello zestawu danych, 0,6% punktów hello jest dodatnia, hello rest jest ujemna. opieka zdrowotna Siemens nastąpiła dostępne Hello zestawu danych.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Etykiety Appetency CRM udostępnionych</td>
  <td valign=top>
Etykiety z hello 2009 Pucharze KDD klienta relacji prognozowania challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Etykiety przenoszenie CRM udostępnionych</td>
  <td valign=top>
Etykiety z hello 2009 Pucharze KDD klienta relacji prognozowania challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>CRM zestawu danych udostępnionych</td>
  <td valign=top>
Te dane pochodzą z hello 2009 Pucharze KDD klienta relacji prognozowania challenge (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>zestaw danych Hello zawiera 50K klientów z hello firmy telekomunikacyjnych francuski pomarańczowy. Każdy klient ma 230 funkcje anonimowe, 190, które są numeryczne i 40 są podzielone na kategorie. Funkcje Hello są bardzo rozrzedzone.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Etykiety grup CRM udostępnionych</td>
  <td valign=top>
Etykiety z hello 2009 Pucharze KDD klienta relacji prognozowania challenge (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Dane wydajności regresji energii</td>
  <td valign=top>
Zbiór profilów symulowane energii, na podstawie 12 innego budynku kształtów. budynków Hello są zróżnicowane przez 8 funkcje, takie jak szyb obszarze hello szyb obszaru dystrybucji i orientacji.<p> </p><b>Sposób użycia:</b> Użyj klasyfikacji lub regresji toopredict hello-zapotrzebowania na energię klasyfikacja na podstawie jako jedną z dwóch wartości rzeczywistych odpowiedzi. Klasa wielu klasyfikacji jest round toohello zmiennej odpowiedzi hello najbliższej liczby całkowitej. <p> </p><b>Powiązane Research:</b> Xifara, A. & Tsanas, A. (2012). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Transmitowane opóźnienia danych</td>
  <td valign=top>
Transmitowane pasażerów na czas dane wydajności z hello TranStats zbierania danych dotyczących hello stany USA Stanowych (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">na czas</a>).<p> </p>zestaw danych Hello obejmuje hello okresie kwietnia — październik 2013. Przed przekazaniem tooAzure Machine Learning Studio, zestaw danych hello przetworzono w następujący sposób:<ul><li>Hello zestaw danych został toocover filtrowane tylko hello 70 zajętej lotniskach w kontynentalnym hello stany USA</li><li>Anulowano lotach zostały oznaczone jako opóźniony o więcej niż 15 minut.</li><li>Kierunku lotach zostały odfiltrowane.</li><li>Witaj następujące kolumny wybrano: rok, miesiąc, DayofMonth, DayOfWeek, operatora, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, anulowane</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Na czas osiągów (Raw)</td>
  <td valign=top>
Rejestruje samolotowy transmitowane odbiorów i odejście na terenie Stanów Zjednoczonych z października 2011.<p> </p><b>Sposób użycia:</b> prognozowania transmitowane opóźnienia. <p> </p><b>Powiązane Research:</b> z działu transportu USA <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Dane generowane lasu</td>
  <td valign=top>
Zawiera dane pogodzie, takich jak indeksy temperatury i wilgotności i knie szybkość, z obszaru północno-wschodniej Portugalii, w połączeniu z rekordów pożarów lasów.<p> </p><b>Sposób użycia:</b> jest to zadanie trudne regresji, który celem hello toopredict hello kiedyś obszaru pożarów lasów. <p> </p><b>Powiązane Research:</b> Cortez, P. & Morais, A. (2008). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki <p> </p>[Cortez i Morais, 2007] Str. Cortez i A. Morais. TooPredict metody wyszukiwania danych przy użyciu danych meteorologicznych pożarów lasów. W J. Neves, M. F. Santos i J. Machado Eds., nowe tendencji sztucznego analizy, postępowania hello 13 EPIA 2007 — portugalski konferencji na sztucznego analizy grudnia, Guimarães, Portugalia str. 512-523, 2007. APPIA, ISBN 13 978-989-95618-0-9. Dostępne pod adresem: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Niemiecki karty kredytowej UCI zestawu danych</td>
  <td valign=top>
Witaj Statlog UCI (karta kredytowa niemiecki) zestawu danych (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + niemiecki + środki + danych</a>), przy użyciu pliku german.data hello.<p> </p>zestaw danych Hello klasyfikuje osób opisanego przez zestaw atrybutów jako niski lub wysokiego ryzyka. Każdy przykład reprezentuje osoby. Istnieją funkcje 20, zarówno numeryczne i podzielone na kategorie i etykietę binarne (wartość ryzyko kredytowe hello). Środki wysokiego ryzyka zapisów etykiety = 2, środki niskiego ryzyka zapisów etykiety = 1. Koszt Hello misclassifying jest przykład niskiego ryzyka tak dużych to 1, misclassifying przykład wysokiego ryzyka, jako niski koszt hello jest 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>ZAUFANI filmu tytułów</td>
  <td valign=top>
Witaj zestaw danych zawiera informacje na temat filmów, które zostały sklasyfikowane w serwisie Twitter tweetów: ZAUFANI filmu identyfikator, nazwę filmu genre i roku produkcji. W hello dataset są filmy 17K. Hello zestawu danych została wprowadzona w dokumencie hello "S. Dooms T. De Pessemier i L. Martens. MovieTweetings: filmu klasyfikacji zestawu danych zbieranych z serwisem Twitter. Workshop na Crowdsourcing i ludzkich obliczanie systemów polecania CrowdRec na RecSys 2013".
  </td>
</tr>

<tr>
  <td valign=top>Iris dwie klasy danych</td>
  <td valign=top>
Jest to prawdopodobnie hello w hello wzorzec rozpoznawania materiały znaną toobe bazy danych. zestaw danych Hello jest stosunkowo mały, zawierający 50 przykłady pomiarów Motyw Płatek z trzech iris odmian.<p> </p><b>Sposób użycia:</b> prognozowania hello iris typu z hello pomiarów.  <p> </p><b>Powiązane Research:</b> Fishera, R.A. (1988). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Tweetów film</td>
  <td valign=top>
zestaw danych Hello jest rozszerzona wersja hello Tweetings filmu dataset. Witaj dataset zawiera 170K Klasyfikacje filmów wyodrębniony z dobrze tweetów w serwisie Twitter. Każde wystąpienie reprezentuje tweet i jest krotka: identyfikator użytkownika, ZAUFANI filmu ID, klasyfikacji, sygnatura czasowa, numer Ulubione tweet i liczba retweets to tweet. Hello zestawu danych została udostępniona przez A. powiedział, S. Dooms, B. Loni i D. Tikk dla polecania systemów wyzwanie 2014.
  </td>
</tr>

<tr>
  <td valign=top>Dane MPG dotyczące różnych samochodów</td>
  <td valign=top>
Ten zestaw danych jest nieco zmodyfikowaną wersję zestawu danych hello udostępniane przez bibliotekę StatLib hello Carnegie Mellon University. zestaw danych Hello został użyty w hello 1983 American statystyczne specyfikacji skojarzenia.<p> </p>dane Hello Wyświetla zużycie paliwa dla różnych samochodów w milach na galon, wraz z informacjami o takich hello liczbę cylindrów, aparat przemieszczenie moc, całkowitej wagi i przyspieszenie.<p> </p><b>Sposób użycia:</b> prognozowania zużycie paliwa na podstawie 3 wielowartościowego atrybutów dyskretnych i 5 atrybutów ciągłych. <p> </p><b>Powiązane Research:</b> StatLib Carnegie Mellon University (1993). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr>
  <td valign=top>Klasyfikacji binarnej cukrzyca Indian Pima zestawu danych</td>
  <td valign=top>
Podzbiór danych z bazy danych National Institute cukrzyca i przewodu i choroby nerek hello. Hello zestaw danych został filtrowane toofocus na żeńskiego pacjentów dziedzictwa indyjskiego Pima. dane Hello obejmują medyczne dane, takie jak glukozy i inulinowego poziomy, a także lifestyle czynników.<p> </p><b>Sposób użycia:</b> prognozowania, czy temat hello ma cukrzyca (klasyfikacji binarnej). <p> </p><b>Powiązane Research:</b> Sigillito, V. (1990). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml "</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki </td>
</tr>

<tr>
  <td valign=top>Dane klienta restauracji</td>
  <td valign=top>
Zestaw metadane dotyczące klientów, w tym demograficznymi i preferencje.<p> </p><b>Sposób użycia:</b> używają tego zestawu danych, w połączeniu z hello innych dwóch restauracji zestawów danych, tootrain i przetestowania systemu polecania. <p> </p><b>Powiązane Research:</b> Bache, K. i Lichman, M. (2013). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki.
  </td>
</tr>

<tr>
  <td valign=top>Dane funkcji restauracji</td>
  <td valign=top>
Zestaw metadane dotyczące restauracji i ich funkcje, takie jak typ żywności, lokali stylu i lokalizacji.<p> </p><b>Sposób użycia:</b> używają tego zestawu danych, w połączeniu z hello innych dwóch restauracji zestawów danych, tootrain i przetestowania systemu polecania. <p> </p><b>Powiązane Research:</b> Bache, K. i Lichman, M. (2013). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki.
  </td>
</tr>

<tr>
  <td valign=top>Klasyfikacje restauracji</td>
  <td valign=top>
Zawiera klasyfikacji podanej przez użytkowników toorestaurants w skali od 0 too2.<p> </p><b>Sposób użycia:</b> używają tego zestawu danych, w połączeniu z hello innych dwóch restauracji zestawów danych, tootrain i przetestowania systemu polecania. <p> </p><b>Powiązane Research:</b> Bache, K. i Lichman, M. (2013). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki.
  </td>
</tr>

<tr>
  <td valign=top>Stali Annealing wielu klasy dataset</td>
  <td valign=top>
Ten zestaw danych zawiera szereg rekordy z stali termiczne odprężanie prób z atrybutami fizycznych hello (szerokość, grubość, typ (cewka, Arkusz itp.) co hello stali typów.<p> </p><b>Sposób użycia:</b> dwa atrybuty klasy liczbowych; twardości lub siły przewidzieć. Może również analizować korelacji między atrybutami.<p> </p>Stali wykonaj standardowego zestawu, zdefiniowany przez SAE i innych organizacji. Szukasz określonej "klasy" (zmienna klasy hello), a wartości hello toounderstand wymagane. <p> </p><b>Powiązane Research:</b> szterlinga, D. & Buntine, W. (NA). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University Kalifornijskiej, szkoły informacji i informatyki <p> </p>Klasy toosteel przydatny przewodnik można znaleźć tutaj: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Teleskopu danych</td>
  <td valign=top>
Rejestruje wysokiej energii gamma cząstki seria wraz z hałas w tle, zarówno symulowane za pomocą Monte Carlo procesu.<p> </p>Celem Hello symulacji hello został tooimprove dokładność hello na podstawie podstaw atmosferycznych Cherenkov gamma teleskopy, za pomocą metod statystycznych toodifferentiate między hello żądany sygnał (promieniowania Cherenkov natryski) i (hadronic szumu tła Natryski inicjowane przez promienie cosmic w atmosferze górna hello).<p> </p>Witaj dane zostały toocreate wstępnie przetworzone wydłużonym klaster z hello długiej osi jest zorientowany hello aparatu center. właściwości Hello tego elipsy (często nazywane parametry Hillas) są hello obrazu parametrów, które mogą być używane dla dyskryminacji.<p> </p><b>Sposób użycia:</b> prognozowania, czy obraz przyjęcie reprezentuje szumu sygnał lub w tle.<p> </p><b>Uwagi:</b> proste klasyfikacji dokładność nie jest zrozumiały dla tych danych, ponieważ klasyfikacji zdarzeń tła jako sygnału jest większa niż klasyfikowania zdarzenie sygnału jako tło. Porównanie różnych klasyfikatory hello ROC wykres powinien być używany. Witaj prawdopodobieństwo akceptowania zdarzeń tła jako sygnału musi być poniżej jednego powitania po progi: 0,01, 0,02, 0,05, 0,1 lub 0,2.<p> </p>Należy również zauważyć, że jest zgłosił hello liczba zdarzeń tła (h, natryski hadronic), w rzeczywiste pomiary hello h lub szumu klasy stanowi hello większość zdarzeń. <p> </p><b>Powiązane Research:</b> Bock, R.K. (1995). UCI Machine Learning repozytorium <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, urząd certyfikacji: University z Kalifornijskiej, szkoły informacji </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Pogody zestawu danych</td>
  <td valign=top>
Co godzinę uwag lądowej pogody NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">scalane dane z 201304 too201310</a>).<p> </p>Witaj pogody danych obejmuje uwagi z lotniska pogody stacje, obejmujące hello okresie kwietnia — październik 2013. Przed przekazaniem tooAzure Machine Learning Studio, zestaw danych hello przetworzono w następujący sposób:<ul><li>Identyfikatory pogody stacji zostały lotnisku zamapowanych toocorresponding identyfikatorów</li><li>Stacje pogody nie są skojarzone z 70 lotniskach zajętej hello zostały odfiltrowane.</li><li>kolumnę dat Hello podzielono na osobne kolumny rok, miesiąc i dzień</li><li>Witaj następujące kolumny wybrano: AirportID, rok, miesiąc, dzień, czas, strefy czasowej, SkyCondition, widoczność, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, Prędkość wiatru, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, wysokościomierza</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 zestawu danych</td>
  <td valign=top>
Danych jest określana na podstawie Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) oparte na artykuły każdej S & P 500 firmy przechowywanych danych XML.<p> </p>Przed przekazaniem tooAzure Machine Learning Studio, zestaw danych hello przetworzono w następujący sposób:<ul><li>Wyodrębnienie zawartości tekstowej dla każdej firmy</li><li>Usunięcie formatowania stron typu wiki</li><li>Usuń znaki inne niż alfanumeryczne</li><li>Konwertuj wszystkie toolowercase tekstu</li><li>Kategorie znane firmy zostały dodane</li></ul><p> </p>Należy pamiętać, że w niektórych firmach artykuł nie można odnaleźć, więc hello liczba rekordów jest mniej niż 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
Hello zestaw danych zawiera dane klientów i wskazówek dotyczących ich odpowiedzi tooa bezpośredniego kampanii. Każdy wiersz reprezentuje klienta. Witaj zestaw danych zawiera funkcje 9 o demograficznymi użytkownika oraz zachowania i 3 kolumny etykiety (odwiedź konwersji oraz wydatków).  Odwiedź stronę to kolumna typu binary, który oznacza, że klient odwiedzi po hello kampanię marketingową konwersji oznacza, że klient zakupiono produkt i spędzają na wielkość hello, który był poświęcony na.  zestaw danych Hello została udostępniona przez Hillstrom Kevina dla MineThatData E-Mail analizy danych wyszukiwania żądania i.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Funkcje przykłady testu w hello Reuters RCV1 V2 wiadomości w zestawie danych. Witaj dataset zawiera artykuły 781K wraz z ich identyfikatorów (pierwsza kolumna hello zestawu danych). Każdego artykułu jest stokenizowana stopworded i zakończonej. zestaw danych Hello została udostępniona przez Dominika. D. Nowak.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Funkcje przykładów szkoleniowych w hello Reuters RCV1 V2 wiadomości w zestawie danych. Witaj dataset zawiera artykuły 23K wraz z ich identyfikatorów (pierwsza kolumna hello zestawu danych). Każdego artykułu jest stokenizowana stopworded i zakończonej. zestaw danych Hello została udostępniona przez Dominika. D. Nowak.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Zestaw danych z hello 1999 Pucharze KDD wiedzy odnajdywania i danych wyszukiwania narzędzia konkurencji (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>zestaw danych Hello została pobrana i przechowywane w magazynie obiektów Blob platformy Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) i obejmuje zarówno uczenie i testowanie zestawów danych. zestaw danych szkoleniowych Hello ma około 126K wierszy i kolumn 43, w tym hello etykiety. Trzy kolumny są częścią hello etykiety informacji i 40 kolumn, składające się z funkcje numeryczne i ciągu/podzielone na kategorie, dostępnych do uczenia modelu hello. dane testowe Hello ma około 22,5 K testowania przykładów z kolumnami hello 43 sam jak hello danych szkoleniowych.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1 v2.topics.qrels.csv</a></td>
  <td valign=top>
Przypisania tematu dla artykuły w hello Reuters RCV1 V2 wiadomości w zestawie danych. Tematy tooseveral można przypisać artykuł wiadomości. format Hello każdy wiersz jest "&lt;nazwa tematu&gt; &lt;identyfikator dokumentu&gt; 1". zestaw danych Hello zawiera przypisania tematu 2.6M. zestaw danych Hello została udostępniona przez Dominika. D. Nowak.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Te dane pochodzą z hello wyzwanie oceny wydajności uczniów 2010 Pucharze KDD (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">oceny wydajności uczniowie</a>). Witaj danych używany jest zestaw szkoleniowy hello Algebra_2008_2009 (Stamper, J., Niculescu-Mizil, S. A., Ritter, Gordon, G.J. & Koedinger, K.R. (2010). Algebraiczną I 2008 2009. Żądanie zestawu danych z KDD Pucharze 2010 edukacyjnych danych wyszukiwania żądania. Znajdź go w <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> lub <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>zestaw danych Hello została pobrana i przechowywane w magazynie obiektów Blob platformy Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) i zawiera pliki dziennika z studenta Korepetycje systemu. cechy Hello podany identyfikator problemu i jego krótki opis ID studenta, timestamp, oraz liczbę prób uczniów hello przed rozwiązywania problemu hello w hello prawym przyciskiem myszy sposób. Witaj oryginalnego zestawu danych zawiera rekordy 8,9 M; Ten zestaw danych został próbkowany dół toohello pierwsze 100 KB wierszy. Hello dataset zawiera 23 tabulatorem kolumny z różnych typów: liczbowe podzielone na kategorie i sygnatura czasowa.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
