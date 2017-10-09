---
title: "aaaAnalyzing klienta churn — przy użyciu usługi Machine Learning | Dokumentacja firmy Microsoft"
description: Analiza przypadku powstania zintegrowanego modelu do analizowania i oceniania przenoszenie klienta
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Analizowanie zmienności klientów przy użyciu usługi Azure Machine Learning
## <a name="overview"></a>Omówienie
Ten artykuł przedstawia wdrożenie odwołanie do projektu analizy przenoszenie klienta skompilowanego za pomocą usługi Azure Machine Learning. W tym artykule omówiono skojarzone ogólnego modeli całościowe rozwiązanie problemu hello z tworzeniem przemysłowych klienta. Możemy również Zmierz hello dokładność modeli, które są tworzone za pomocą uczenia maszynowego i możemy oceny instrukcjami w celu dalszego rozwijania.  

### <a name="acknowledgements"></a>Potwierdzeń
Tego eksperymentu został opracowany i przetestowane przez Serge Berger naukowca danych podmiot zabezpieczeń w firmie Microsoft i Roger Barga, wcześniej produktu programu Microsoft Azure Machine Learning. zespół Azure dokumentacji Hello gratefully uznaje ich wiedzy i Dziękujemy je do udostępniania tego oficjalny dokument.

> [!NOTE]
> Witaj dane używane na potrzeby tego eksperymentu nie jest publicznie dostępna. Na przykład jak toobuild usługi machine learning model analizy zmian, zobacz: [handlowej churn — szablonu modelu](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>Hello problem z tworzeniem klienta
Przedsiębiorstwa powitania klienta rynku i we wszystkich sektorach przedsiębiorstwa mają toodeal z zmian. Czasami zmian jest nadmierne i wpływ decyzji dotyczących zasad. tradycyjne rozwiązania Hello jest toopredict churners większego ukierunkowania wysokiej i rozwiąż potrzeb za pośrednictwem usługi Konsjerż, kampanii, lub przez zastosowanie zwolnień specjalne. Te metody mogą się różnić z branży tooindustry i nawet tooanother klastra określonego użytkownika, w ramach jednego industry (na przykład telekomunikacyjnych).

współczynnik wspólnej Hello jest firm potrzeby toominimize tych działań przechowywania specjalne klienta. W związku z tym metodologię fizyczne można tooscore wszystkich klientów z hello prawdopodobieństwo zmian i adresów hello pierwszych N z nich. Witaj najlepszych klientów może hello najbardziej dochodowe te; na przykład w bardziej zaawansowanych scenariuszy, funkcja zysku jest zastosować podczas hello wybór kandydatów specjalne zwolnienia. Jednak te zagadnienia są tylko część strategii kompleksowe hello zajmujących się ilość danych churn. Przedsiębiorstwa mają również tootake do konta ryzyka (i tolerancji ryzyka skojarzone) hello poziomu i koszt hello interwencji i segmentacji odbiorców wiarygodne.  

## <a name="industry-outlook-and-approaches"></a>Outlook branżowych i metod
Zaawansowane obsługi zmian jest znak dojrzałe branżowych. przykład klasycznego Witaj jest hello telekomunikacyjnych branży, w których subskrybentów są przełącznika toofrequently znane z tooanother jednego dostawcę. To dobrowolny zmian jest podstawowym. Ponadto dostawców współdzielenia znaczących wiedzy o *churn — sterowniki*, które są elementami hello tooswitch klientów tego dysku.

Na przykład wybór słuchawki lub urządzenia jest dobrze znanego sterownika z postęp dokonany w firmie telefon komórkowy hello. W związku z tym popularnych zasad jest cena hello toosubsidize słuchawki dla nowych subskrybentów i ładowania tooexisting pełną cenę klientów do uaktualnienia. W przeszłości te zasady spowodowało toocustomers skaczące z jednego dostawcę tooanother tooget nowy rabat, który z kolei ma monit toorefine dostawców strategii.

Wysoka zmienności słuchawki oferty jest czynnik, który bardzo szybko unieważnia modeli zmian, które są oparte na bieżących słuchawki modeli. Ponadto telefonów nie są tylko telekomunikacyjnych urządzenia; są one również instrukcje sposób (rozważ hello iPhone), a te zmienne społecznościowych predykcyjne są poza zakresem hello regularne telekomunikacyjnych zestawów danych.

Witaj wynikiem modelowania jest, czy po prostu, eliminując znane przyczyny przenoszenia nie można opracować dźwięku zasad. W rzeczywistości jest strategii ciągłego modelowania klasycznych modeli, które określenie zmienne podzielone na kategorie (takie jak drzewa decyzyjne), w tym **obowiązkowe**.

Za pomocą zestawów danych big Data na klientach, organizacje wykonywania analizy danych big data (w szczególności wykrywania zmian na podstawie danych big Data) jako problem toohello podejście skuteczne. Można znaleźć więcej informacji na temat hello danych big data podejście toohello problemu postęp dokonany w hello zaleceń w sekcji ETL.  

## <a name="methodology-toomodel-customer-churn"></a>Postęp dokonany w metodologii toomodel klienta
Typowe rozwiązywania problemów procesu toosolve klienta zmian jest opisany w wartości 1-3:  

1. Model ryzyka umożliwia tooconsider wpływ akcje prawdopodobieństwo i ryzyka.
2. Model interwencji umożliwia tooconsider jak poziom hello interwencji mogą wpłynąć na powitania prawdopodobieństwo zmian i hello ilość wartość okresu istnienia klienta (CLV).
3. Analiza pozwalają tooa analizy jakościowej eskalowane tooa aktywnego kampanię marketingową przeznaczonego dla oferty optymalne toodeliver powitania klienta segmentów.  

![][1]

Takie podejście do przodu wyglądającej jest hello najlepsze sposób tootreat zmian, ale ma złożoność: mamy toodevelop wiele modeli archetype i śledzenia zależności między modelami hello. Hello interakcji między modelami można hermetyzowany, jak pokazano w powitania po diagramu:  

![][2]

*Rysunek 4: Unified archetype wiele modeli*  

Interakcji między modelami hello jest kluczem, jeśli mamy toodeliver przechowywania toocustomer kompleksowe rozwiązanie. Każdy model powoduje spadek niekoniecznie wraz z upływem czasu; w związku z tym architektura hello jest niejawne pętli (podobne archetype toohello ustawione przez standard wyszukiwania danych hello WYSOKĄ DM, [***3***]).  

Witaj ogólną cykl ryzyka decyzji obrotu segmentacji/rozkładu jest nadal uogólniony struktury, która jest zastosowanie toomany problemów biznesowych. Przenoszenie analizy jest po prostu przedstawiciela silne tej grupy problemów, ponieważ wskazuje wszystkie cech hello o problemie biznesowych, który nie zezwala na uproszczone rozwiązanie predykcyjne. Witaj społecznościowych aspektów hello nowoczesnych podejście toochurn nie są szczególnie wyróżnione w hello podejście, ale aspekty społecznościowych hello są hermetyzowane w archetype modelowania hello, jakie byłyby każdy model.  

W tym miejscu interesujące dodanie jest analizy danych big data. Współczesnych telekomunikacyjnych i detaliczne firmach zbierania wyczerpujący dane o swoich klientów i firma Microsoft może łatwo przewidywany jest tym hello wymagane dla wielu modelu łączności staną się typowe trendu, podane pojawiających się trendy, takie jak hello Internetu rzeczy i Powszechna urządzeń, które Zezwalaj inteligentnych rozwiązań biznesowych tooemploy w wielu warstw.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Implementowanie hello modelowania archetype w usłudze Machine Learning Studio
Podana hello problem, który właśnie opisano, co to jest hello najlepsze sposób tooimplement zintegrowanego modelowania i oceniania rozwiązania? W tej sekcji przedstawiono sposób możemy zrobić to za pomocą usługi Azure Machine Learning Studio.  

podejście wiele modeli Hello jest koniecznością podczas projektowania globalne archetype dla zmian. Nawet hello oceniania (predykcyjnej) część podejścia hello powinna być wiele modeli.  

Witaj Poniższy diagram przedstawia prototypu hello utworzony, która jest stosowana w czterech oceniania algorytmy przenoszenie toopredict Machine Learning Studio. Powodem Hello wiele modeli podejście jest nie tylko toocreate zespół klasyfikatora tooincrease dokładności, ale także tooprotect przed uwierzytelniając dopasowywania i tooimprove przetestowanego funkcji wyboru cech.  

![][3]

*Rysunek 5: Prototyp przenoszenie modelowania podejście*  

Witaj poniższe sekcje zawierają szczegółowe informacje o prototypu hello oceniania modelu wprowadzonym za pomocą usługi Machine Learning Studio.  

### <a name="data-selection-and-preparation"></a>Wybór danych i przygotowanie
dane Hello używane toobuild hello modeli i wynik klientów zostały pobrane z rozwiązania pionowy CRM, z hello danych zaciemniona tooprotect — ochrona prywatności klientów. Hello danych zawiera informacje o subskrypcjach 8000 w USA hello i składa się z trzech źródeł: Inicjowanie obsługi danych (metadane subskrypcji), dane o aktywności (użycie hello system) i danych obsługi klienta. Witaj danych nie zawiera dowolnego rodzaju działalności powiązane informacje o klientach hello; na przykład nie zawiera wyników lojalność metadanych lub faktury.  

Dla uproszczenia ETL i procesy czyszczenia danych są poza zakresem, ponieważ przyjęto założenie, że przygotowanie danych ma już zostały wykonane w innych miejscach.   

Wybieranie funkcji do modelowania jest oparta na wstępne istotności oceniania hello zestawu zmienne predykcyjne, zawarte w hello procesu, który korzysta z modułu losowe lasu hello. Dla implementacji hello w usłudze Machine Learning Studio firma Microsoft obliczona średnia hello, mediana i zakresy dla funkcji reprezentatywny. Na przykład dodawać wartości zagregowanych danych jakościowe hello, takie jak wartości minimalną i maksymalną dla działań użytkownika.    

Możemy również przechwycono danych czasowych informacje dotyczące hello ostatnich sześciu miesięcy. Przeanalizowaliśmy danych przez jeden rok i możemy ustanowić czy nawet wtedy, gdy było trendów statystycznie istotne, hello wpływa na przenoszenie będzie znacznie mniejsza po upływie sześciu miesięcy.  

punkt najważniejszych Hello jest tym hello całego procesu, w tym ETL, wybór funkcji i modelowania został wdrożony w usłudze Machine Learning Studio, korzystanie ze źródeł danych na platformie Microsoft Azure.   

Witaj poniższych diagramach przedstawiono hello dane, które zostało użyte.  

![][4]

*Rysunek 6: Fragment źródła danych (zaciemniona)*  

![][5]

*Rysunek 7: Funkcje wyodrębnione ze źródła danych*
 

> Zauważ, że te dane są prywatne i dlatego nie może być współużytkowana hello modelu i danych.
> Jednak dla podobnych modelu przy użyciu dostępnych publicznie danych, zobacz ten przykład eksperymentu w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco churn klienta —](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> więcej informacji na temat implementacji zmian modelu analizy przy użyciu pakietu Cortana Intelligence Suite toolearn, zalecamy również [ten film](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) przez Tok Hyong Wee starszy Menedżer programu. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Algorytmy używane w hello prototypu
My używamy hello następujące cztery algorytmów uczenia maszynowego prototypu hello toobuild (Brak dostosowanych):  

1. Regresja logistyczna (LR)
2. Drzewo decyzyjne boosted (BT)
3. Perceptron uśrednionej (AP)
4. Obsługa wektor maszyny (SVM)  

Witaj poniższym diagramie przedstawiono część powierzchni projektowej eksperymentu hello, co oznacza sekwencji hello, w których hello modele zostały utworzone:  

![][6]  

*Rysunek 8: Tworzenie modeli w usłudze Machine Learning Studio*  

### <a name="scoring-methods"></a>Metod oceniania
Modele hello czterech możemy oceniane przy użyciu zestawu danych oznaczonych szkolenia.  

Przesłaliśmy również hello oceniania zestawu danych tooa porównywalne model tworzony przy użyciu wersji pulpitu hello 12 analizatora Enterprise sygnatury dostępu Współdzielonego. Firma Microsoft mierzy hello dokładności modelu sygnatur dostępu Współdzielonego hello i wszystkie cztery modele usługi Machine Learning Studio.  

## <a name="results"></a>Wyniki
W tej sekcji możemy przedstawić uzyskanych danych o dokładności hello hello modeli, opartych na powitania oceniania zestawu danych.  

### <a name="accuracy-and-precision-of-scoring"></a>Dokładność i precyzja oceniania
Ogólnie rzecz biorąc implementacja hello uczenia maszynowego Azure jest za SAS dokładności o około 10 – 15% (obszar w obszarze krzywej lub AUC).  

Metryka najważniejszych hello w zmian jest jednak częstotliwość błędów klasyfikacji hello: oznacza to, z churners pierwszych N hello jako przewidywane przez hello klasyfikatora, który z nich rzeczywiście została **nie** churn — i jeszcze odebrane szczególnego traktowania? hello Poniższy diagram porównuje to częstotliwość błędów klasyfikacji dla wszystkich modeli hello:  

![][7]

*Rysunek 9: Passau prototypu obszarze krzywej*

### <a name="using-auc-toocompare-results"></a>Przy użyciu AUC toocompare wyników
Obszar w krzywej (AUC) jest metrykę, która reprezentuje globalne miara *odrębność* między dystrybucje hello wyników dla tych grup dodatnie i ujemne. Jest podobne wykres toohello tradycyjnych cech Operator odbiornika (ROC), ale jedną istotną różnicą jest tym Metryka AUC hello nie wymaga toochoose wartość progową. Zamiast tego należy podsumowanie wyników hello za pośrednictwem **wszystkie** możliwe opcje. Z kolei hello tradycyjnych ROC wykres pokazuje szybkość dodatnią hello na osi pionowej hello i false szybkość hello na osi poziomej hello dodatnią, a próg klasyfikacji hello zmienia się.   

AUC jest zazwyczaj używany jako środek do wartości dla różnych algorytmów (lub w innych systemach) ponieważ zezwala ona na porównaniu za pomocą ich wartości AUC toobe modeli. To podejście popularnych w branży, takie jak meteorologia i biosciences. W związku z tym AUC reprezentuje popularne narzędzia do oceny wydajności klasyfikatora.  

### <a name="comparing-misclassification-rates"></a>Porównywanie stawki błędu klasyfikacji
Firma Microsoft porównywane szybkości błędną klasyfikację hello na powitania dataset w za pomocą danych CRM hello około 8000 subskrypcji.  

* Częstotliwość błędów klasyfikacji SAS Hello to 10 – 15%.
* Współczynnik błędów klasyfikacji Machine Learning Studio Hello został 15-20% dla hello churners pierwsze 200 300.  

W branży telekomunikacyjnych hello jest ważne tooaddress tylko do klientów, którzy mają hello najwyższy toochurn ryzyka, oferując im usługi Konsjerż lub innych szczególnego traktowania. W tym zakresie implementacji usługi Machine Learning Studio hello osiąga wyników blokowego hello modelu sygnatur dostępu Współdzielonego.  

Przez hello sam token, dokładność ma większe znaczenie niż precyzja ponieważ przeważnie Dbamy o poprawnie klasyfikacji potencjalnych churners.  

Witaj poniższych diagramu z Wikipedia zebrano relacji hello grafiki barwnym, łatwe do zrozumienia:  

![][8]

*Rysunek 10: Zależności między dokładność i dokładność*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Dokładność i precyzja wyników dla modelu drzewa decyzyjnego boosted
Hello raw hello Wyświetla wykres po wynikiem oceniania przy użyciu prototypu uczenia maszynowego hello hello boosted decyzji drzewa modelu, które odbywa się hello toobe najdokładniejszych między cztery modele hello:  

![][9]

*Rysunek 11: Właściwości modelu drzewa decyzyjnego Boosted*

## <a name="performance-comparison"></a>Porównanie wydajności
Firma Microsoft porównywana szybkość hello jaką danych został oceniane przy użyciu modeli Machine Learning Studio hello i porównywanie modelu utworzone za pomocą wersji pulpitu hello 12.1 analizatora Enterprise SAS.  

Witaj w poniższej tabeli znajduje się podsumowanie wydajności hello algorytmów hello:  

*Tabela 1. Algorytmów hello ogólnej wydajności (dokładność)*

| LR | BT | Interfejs API | SVM |
| --- | --- | --- | --- |
| Model średni |Witaj najlepsze modelu |Gorszych wynikach w przypadku |Model średni |

modele Hello hostowanych w usłudze Machine Learning Studio outperformed SAS przez 15-25% do szybkości wykonywania, ale dokładność został przede wszystkim od par.  

## <a name="discussion-and-recommendations"></a>Omówienie i zalecenia
W branży telekomunikacyjnych hello, kilka rozwiązań pojawiło się tooanalyze churn — w tym:  

* Pochodzi metryki czterech podstawowych kategorii:
  * **Jednostka (na przykład subskrypcji)**. Udostępnić podstawowe informacje o subskrypcji hello i/lub klienta, który podlega hello zmian.
  * **Działanie**. Uzyskaj wszystkie informacje możliwe użycie toohello powiązane jednostki, na przykład hello numer logowania.
  * **Dział obsługi klienta**. Zebrać informacje z tooindicate dzienniki pomocy technicznej klienta, czy subskrypcja hello ma problemy lub interakcji z klienta obsługuje.
  * **Dane konkurencyjnych i biznesowych**. Uzyskiwać możliwe informacji na temat powitania klienta (na przykład może być niedostępna lub twardych tootrack).
* Zaznacz pole wyboru funkcji toodrive znaczenie. Oznacza to modelu drzewa decyzyjnego hello boosted jest zawsze obietnicy podejście.  

Witaj użyj kategorii tworzy wrażenie hello który prostą *deterministyczne* podejścia, opartego na indeksy sformatowany na czynniki uzasadnione według kategorii, powinny wystarczyć klientów tooidentify narażone na przenoszenie. Niestety Chociaż to pojęcie jest prawdopodobnie wiarygodne, jest FAŁSZ opis. Przyczyna Hello jest przenoszenie jest efekt danych czasowych oraz czynniki hello przyczyniające się toochurn znajdują się zwykle w stan przejściowy. Co skutkuje klienta tooconsider pozostawienie dzisiaj mogą się różnić jutro i oczywiście będzie inny sześciu miesięcy od teraz. W związku z tym *prawdopodobieństwa* modelu jest to konieczne.  

To ważne obserwacji jest często pomijane w firmie zwykle preferuje tooanalytics podejście zorientowane na analizy biznesowej, przede wszystkim, ponieważ jest łatwiejsze sprzedaży i dopuszcza prostego automatyzacji.  

Jednak promise hello samoobsługi analizy przy użyciu usługi Machine Learning Studio jest hello czterech kategorii informacji klasyfikowanych przez oddział lub dział cenne źródło uczenia maszynowego o zmian.  

Kolejna możliwość atrakcyjnych dostępne w usłudze Azure Machine Learning jest tooadd możliwości hello repozytorium toohello niestandardowego modułu wstępnie zdefiniowanych modułów, które są już dostępne. Ta funkcja zasadniczo tworzy tooselect możliwości bibliotek i tworzenia szablonów dla pionowego rynkach. Jest ważne różnicą uczenie maszynowe Azure w miejscu rynku hello.  

Mamy nadzieję toocontinue, w tym temacie w hello toobig przyszłych, szczególnie powiązanych danych w module analiz.
  

## <a name="conclusion"></a>Podsumowanie
W tym dokumencie opisano za pośrednictwem metody tootackling hello powszechny problem z tworzeniem klienta przy użyciu ogólnych framework. Firma Microsoft traktowane jako prototyp oceniania modeli i zaimplementowana przy użyciu usługi Azure Machine Learning. Na koniec mamy ocenić hello niezawodność i wydajność rozwiązania prototypu hello z uwzględnieniem toocomparable algorytmy SAS.  

**Aby uzyskać więcej informacji:**  

Czy w tym dokumencie pomóc? Daj nam swoją opinię. Powiedz nam w skali od 1 (niska) too5 (znakomity), jak oceniasz w tym dokumencie i dlaczego należy przyznanymi go tej klasyfikacji? Na przykład:  

* Są możesz klasyfikacji go wysokiej toohaving dobre przykłady, zrzuty ekranu znakomity, wyczyść zapisywania, lub kolejny powód?
* Są możesz klasyfikacji go niski przykłady toopoor, zrzuty ekranu rozmytego lub jasne zapisywania?  

Ta opinia pomoże nam poprawić jakość hello oficjalne dokumenty, które wydania.   

[Wyślij opinię](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Dokumentacja
[1] analizy predykcyjnej: poza hello prognoz, W. McKnight, zarządzanie informacji lipca i sierpnia 2011 r. p.18 20.  

[2] Wikipedia artykuł: [dokładność i dokładność](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [WYSOKĄ DM 1.0: Przewodnik wyszukiwania danych krok po kroku](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [Marketing danych big Data: efektywniej kontaktować się z klientami i dysk wartość](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Telco churn — szablonu modelu](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) w [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Dodatek
![][10]

*Rysunek 12: Migawki prezentacji na prototypie zmian*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
