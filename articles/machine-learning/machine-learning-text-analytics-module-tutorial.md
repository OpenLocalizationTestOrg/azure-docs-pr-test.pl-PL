---
title: "aaaCreate modele analizy tekstu w usłudze Azure Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Jak analiza tekstu toocreate modeli w usłudze Azure Machine Learning Studio przy użyciu modułów przetwarzania wstępnego tekstu, N-g lub Tworzenie skrótu funkcji"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Tworzenie modeli analizy tekstu w usłudze Azure Machine Learning Studio
Można użyć usługi Azure Machine Learning toobuild i operacjonalizuj modele analizy tekstu. Te modele mogą ułatwić rozwiązywanie, na przykład problemy analizy dokumentu klasyfikacji i wskaźniki nastrojów klientów.

W eksperymencie analytics tekst ma zazwyczaj:

1. Czyszczenie i wstępnie Przetwórz tekst zestawu danych
2. Wyodrębnij wektory funkcji numerycznych z wstępnie przetworzonych tekstu
3. Train model klasyfikacji lub regresji
4. Wynik i weryfikacja modelu hello
5. Wdrażanie hello tooproduction modelu

Z tego samouczka, dowiesz się, te kroki jako możemy przeprowadzenie modelu analizy wskaźniki nastrojów klientów przy użyciu zestawu Amazon książki przeglądy danych (zobacz ten dokument research "Biographies, Bollywood, wysięgnik pola i mieszalni: dostosowanie domeny klasyfikacji wskaźniki nastrojów klientów" Blitzer Jan, oznacz Dredze i Fernando Pereira; Skojarzenie Linguistics obliczeniową (ACL), 2007.) Ten zestaw danych składa się z przeglądu wyniki (1-2 lub 4-5) i dowolnego tekstu. Witaj celem jest wynik przeglądu hello toopredict: Niski (1 - 2) lub high (4 – 5).

Można znaleźć eksperymenty omówione w tym samouczku w Cortana Intelligence Gallery:

[Przewidywanie książki przeglądów](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Przewidywanie przeglądami Book - eksperyment predykcyjny](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Krok 1: Clean i wstępnie Przetwórz tekst zestawu danych
Zaczniemy eksperymentu hello przez podzielenie hello Przejrzyj wyniki w kategorii zasobników niski i wysoki tooformulate hello problem dwuklasowych klasyfikacji. Używamy [edytowanie metadanych](https://msdn.microsoft.com/library/azure/dn905986.aspx) i [wartości kategorii grupy](https://msdn.microsoft.com/library/azure/dn906014.aspx) modułów.

![Tworzenie etykiety](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Następnie możemy czyszczenia hello tekstu przy użyciu [wstępnie Przetwórz tekst](https://msdn.microsoft.com/library/azure/mt762915.aspx) modułu. czyszczenie Hello zmniejsza szumu hello w zestawie danych hello, pomocy Znajdź hello najważniejszych funkcjach i zwiększyć hello dokładność hello ostatecznego modelu. Usuwamy odrzucanych - popularnych wyrazów, takie jak "" lub "-" i cyfry, znaki specjalne zduplikowanych znaków, adresy e-mail i adresów URL. Możemy również przekonwertować toolowercase tekst hello, lemmatize hello słowa, a także wykryć granice zdania, które następnie są wskazywane przez "|||" symboli w tekście wstępnie przetworzonych.

![Przetwarzanie wstępne tekstu](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Co zrobić, jeśli chcesz toouse niestandardowej listy odrzucanych? Można przekazać go jako dane wejściowe opcjonalne. Można również użyć niestandardowej C# składni wyrażeń regularnych tooreplace podciągów i usunąć słowa przez część mowy: rzeczowniki poleceń i określeniem.

Po zakończeniu przetwarzania wstępnego hello możemy podzielić danych hello pociągu i testowania zestawów.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Krok 2: Wyodrębniania wstępnie przetworzonych tekst wektory funkcji numerycznych
toobuild modelu dla danych tekstowych, zazwyczaj mają tooconvert dowolnego tekstu do funkcji numerycznych wektory. W tym przykładzie używamy [wyodrębnić funkcji N-gramów z tekstu](https://msdn.microsoft.com/library/azure/mt762916.aspx) format toosuch danych modułu tootransform hello tekstu. Ten moduł ma kolumnę rozdzielone odstępem słów i oblicza słownika wyrazy lub N-gramów wyrazy, które pojawiają się w zestawie danych. Następnie liczy zlicza, ile razy każdego programu word, lub N-gramów, pojawi się we wszystkich rekordach i tworzy wektory funkcji w porównaniu. W tym samouczku możemy ustawić N-gramów too2 rozmiar, tak, aby nasze wektory funkcji to pojedyncze wyrazy i kombinacje dwóch kolejnych wyrazów.

![Wyodrębnij N-gramów](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Trwa stosowanie TF * IDF (określenie częstotliwości odwrotny dokumentu częstotliwość), waga tooN gram liczby. Takie podejście dodaje wagi słowa, które często pojawiają się w jednym rekordzie, ale są rzadko między hello cały zestaw danych. Inne opcje obejmują TF, binary oraz wykresów o wadze.

Takie funkcje tekstu często mają wysokie wymiary. Na przykład jeśli Twoje Boże ma 100 000 unikatowych słów, obszaru funkcji miałyby wymiary 100 000 lub więcej Jeśli N-g są używane. Moduł wyodrębnić funkcji N-gramów Hello zapewnia zestaw opcji tooreduce hello wymiary. Możesz wybrać tooexclude słowa, które są istotne wartość toohave krótki lub długi lub zbyt nietypowych lub zbyt częste. W tym samouczku Wyłączamy N-gramów występujące w mniej niż 5 rekordów lub więcej niż 80% rekordów.

Również można używać funkcji tooselect wybór tylko funkcje, które są najbardziej hello skorelowane z docelowym prognozowania. Używamy chi funkcja wyboru tooselect 1000 funkcje. Słownictwa hello wybranego słowa lub N-gramów można wyświetlić, klikając hello wyjściowego prawo wyodrębniania N-gramów modułu.

Jako toousing o innym podejściu wyodrębnić N-gramów funkcji można użyć funkcji wyznaczania wartości skrótu modułu. Pamiętaj jednak, że [Tworzenie skrótu funkcji](https://msdn.microsoft.com/library/azure/dn906018.aspx) nie ma możliwości wyboru funkcji kompilacji lub TF * IDF o wadze.

## <a name="step-3-train-classification-or-regression-model"></a>Krok 3: Train model klasyfikacji lub regresji
Teraz hello tekst został przekształcone toonumeric funkcji kolumn. zestaw danych Hello nadal zawiera kolumnach typu ciąg z poprzednich etapów, więc używamy Wybieranie kolumn w zestawie danych tooexclude je.

Następnie użyj [Regresja logistyczna Two-Class](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict celem: wynik przeglądu wysoki lub niski. W tym momencie problem regularne klasyfikacji została przekształcona hello tekst analityka problemu. Można użyć hello narzędzi dostępnych w usłudze Azure Machine Learning tooimprove hello modelu. Na przykład możesz eksperymentować toofind klasyfikatory różne wyniki jak dokładny przekazać lub użyj hyperparameter dostrajanie tooimprove hello dokładności.

![Pociągu i wynik](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Krok 4: Wynik i weryfikacja modelu hello
Jak można sprawdzić hello uczonego modelu? Firma Microsoft wynik go przed hello zestawu danych testowych i ocenić hello dokładności. Jednak hello model pokazaliśmy słownictwa hello N-g i ich wagi z zestawu danych szkoleniowych hello. W związku z tym powinniśmy skorzystać w tym słownictwa i wagi tych podczas wyodrębniania funkcji z danych testowych jako przeciwieństwie słownictwa hello toocreating od nowa. W związku z tym firma Microsoft Dodaj toohello modułu wyodrębnić funkcji N-gramów oceniania gałęzi hello eksperymentu, Połącz hello słownika danych wyjściowych z gałęzi szkolenia i ustaw tryb słownictwa hello tylko tooread. Możemy również wyłączyć hello filtrowania N-gramów przez częstotliwość ustawienie hello wystąpienia too1 minimalna i maksymalna too100% i Wyłącz hello wybór funkcji.

Po hello kolumny tekstowej w teście, którego dane zostały przekształcone toonumeric funkcji kolumn, Wyłączamy ciąg hello w gałęzi szkolenia, takich jak kolumny z poprzednich etapach. Następnie użyj się prognoz toomake modułu Score Model i dokładność hello tooevaluate modułu Evaluate Model.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Krok 5: Wdrożenie hello tooproduction modelu
Hello model jest już prawie gotowe toobe wdrożone tooproduction. Po wdrożeniu jako usługi sieci web go przyjmuje ciąg tekstowy dowolnych jako dane wejściowe, a zwracany prediction "high" lub "low". Używa hello rozpoznane N-gramów słownictwa tootransform hello tekst toofeatures i uczony Regresja logistyczna toomake modelu prognozowania z tych funkcji. 

tooset się eksperyment predykcyjny hello, firma Microsoft najpierw zapisz słownictwa N-gramów hello jako zestawu danych i hello uczenia modelu Regresja logistyczna gałęzi szkolenia hello hello eksperymentu. Następnie możemy zapisać eksperymentu hello przy użyciu toocreate "Zapisz jako" wykresu eksperymentu dla eksperyment predykcyjny. Możemy usunąć hello podziału danych modułu i hello szkolenia oddziału z hello eksperymentu. Następnie połączymy hello wcześniej zapisany N-gramów słownictwa i modelu tooExtract N-gramów funkcje i moduły Score Model, odpowiednio. Możemy również usunąć hello modułu Evaluate Model.

Firma Microsoft wybierz kolumny do wstawienia w module zestawu danych przed wstępnie Przetwórz tekst modułu tooremove hello etykiety kolumn i usuń zaznaczenie opcji "Dołącz wynik kolumny toodataset" w Module wynik. W ten sposób usługa sieci web hello nie żąda etykiety hello próbuje toopredict i funkcje wejściowych hello w odpowiedzi nie są wyświetlane.

![Eksperyment predykcyjny](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Mamy teraz eksperymentu, które mogą być publikowane jako usługę sieci web i wywoływane przy użyciu żądanie odpowiedź lub wsadowe wykonywanie interfejsów API.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o modułów analytics tekst z [dokumentacji MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

