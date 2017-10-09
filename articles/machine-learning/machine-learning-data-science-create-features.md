---
title: "Inżynieria aaaFeature w nauce danych | Dokumentacja firmy Microsoft"
description: "Zawiera opis celów hello inżynierii funkcji oraz przykłady swoją rolę w procesie rozszerzenie danych hello uczenia maszynowego."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Inżynieria w nauce danych
W tym temacie opisano celów hello inżynierii funkcji oraz przykłady swoją rolę w procesie rozszerzenie danych hello uczenia maszynowego. Przykłady Hello używane tooillustrate tego procesu są pobierane z usługi Azure Machine Learning Studio. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach. To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Funkcja engineering prób tooincrease hello predykcyjnej możliwości algorytmów uczenia przez tworzenie funkcji z danych pierwotnych ułatwić hello uczenia procesu. Witaj, inżynieria i wybór funkcji ma jedną część hello TDSP opisane w hello [co to jest cyklu życia procesu nauki danych zespołu hello?](data-science-process-overview.md) Funkcja inżynieryjne i wyboru są części hello **opracowywania funkcji** krok hello TDSP. 

* **Inżynieria**: ten proces próbuje toocreate dodatkowe istotne cechy z istniejących funkcji hello hello danych pierwotnych i tooincrease hello predykcyjnej możliwości Algorytm uczenia hello.
* **Wybór funkcji**: tego procesu wybiera hello klucza podzbioru cech oryginalnych danych w wymiarach hello tooreduce próba hello szkolenia problemu.

Zwykle **Inżynieria** zostanie zastosowane pierwszy toogenerate funkcje dodatkowe, a następnie hello **funkcji wyboru** krokiem jest wykonywane tooeliminate nie ma znaczenia, nadmiarowe lub dużej skorelowane funkcje.

dane szkoleniowe Hello używane w uczeniu maszynowym wspomagają często wyodrębniania funkcji z hello nieprzetworzone dane zebrane. Przykład funkcji odtworzone w kontekście hello learning, jak obrazy hello tooclassify odręcznie znaków jest tworzenie nieco mapy gęstość utworzone na podstawie danych dystrybucji raw bit hello. Ta mapa można lokalizowania krawędzi hello znaków hello efektywniej niż po prostu bezpośrednio przy użyciu rozkładu raw hello.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Tworzenie funkcji z danych - Inżynieria
dane szkoleniowe Hello składa się z macierzy składa się z przykładami (rekordy lub obserwacji przechowywane w wierszach), z których każda ma zestaw funkcji (zmienne lub pól przechowywane w kolumnach). Funkcje Hello określony w projekcie doświadczenia hello są oczekiwane toocharacterize hello wzorce w danych hello. Mimo że wiele hello pierwotnych danych, pola, które mogą zostać bezpośrednio włączone w hello tootrain zestaw używany wybranej funkcji modelu, jest często przypadek hello toobe utworzone na podstawie funkcji hello w rozszerzonych toogenerate nieprzetworzone dane hello potrzebne dodatkowe funkcje (odtworzone) zestaw danych szkoleniowych.

Jakiego rodzaju funkcje należy utworzyć zestawu danych hello tooenhance podczas uczenia modelu? Odtworzone funkcji, które zwiększają szkolenia hello dostarczają informacji lepiej odróżniającą hello wzorce w danych hello. Oczekujemy hello nowe funkcje tooprovide dodatkowe informacje, które nie jest zestawem funkcji oryginalny lub istniejące hello wyraźnie przechwycony lub łatwo widoczna w. Jednak ten proces jest coś grafiki. Decyzje dźwięku i produktywności często wymagają doświadczenia z niektórych domen.

Podczas uruchamiania przy użyciu usługi Azure Machine Learning, jest najprostszym toograsp ten proces, konkretnie przy użyciu przykłady podane w hello Studio. Poniżej przedstawiono dwa przykłady:

* Przykład regresji [prognozowania hello liczby dzierżawy roweru](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) w nadzorowanym eksperymentu, gdzie są znane wartości docelowych hello
* Using przykład klasyfikacji wyszukiwania tekstu [Tworzenie skrótu funkcji](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Przykład 1: Dodawanie funkcji danych czasowych dla modelu regresji
Użyjmy hello eksperymentu "żądanie prognozowania rowerów" w sposób funkcji tooengineer toodemonstrate Azure Machine Learning Studio zadania regresji. Celem tego eksperymentu Hello jest toopredict hello popytu na powitania rowerów, czyli hello numer roweru dzierżawy w ramach określonej miesiąc/dzień/godziny. Witaj zestawu danych "dzierżawa roweru UCI zestawu danych" jest używany jako hello nieprzetworzone dane wejściowe. Ten zestaw danych jest oparty na prawdziwe dane z hello Bikeshare kapitału firmy, która obsługuje sieci wynajem roweru w stanie Waszyngton kontrolera domeny w hello Stanów Zjednoczonych. zestaw danych Hello reprezentuje hello liczbę roweru dzierżawy w ramach określoną godzinę dnia w latach hello i 2011 roku 2012 i zawiera 17379 wierszy i kolumn 17. zestaw funkcji raw Hello zawiera pogodą (knie temperatury/wilgotności szybkość) i typ hello hello dnia (świątecznych/dzień tygodnia). toopredict pola Hello jest "cnt", liczba reprezentuje hello roweru dzierżawy w ciągu godziny określonych i które zakresów może się wahać od 1 too977.

Celem hello konstruowania skuteczne funkcje dane szkoleniowe hello, cztery modele regresji utworzonym przy użyciu hello samego algorytmu, ale z czterech różnych szkolenia zestawami danych. reprezentuje zestaw danych Hello czterech hello tego samego nieprzetworzone dane wejściowe, ale z coraz więcej funkcji ustawiona. Te funkcje są podzielone na kategorie cztery:

1. A = pogody + świątecznych dzień tygodnia + weekendowe funkcje hello przewidywane dzień
2. B = liczba rowerów, które zostały dzierżawione w każdym hello ostatnich 12 godzin
3. C = Liczba rowerów, które zostały dzierżawione w każdym hello poprzednich dni 12 na powitania sam godzinę
4. D = liczba rowerów, które zostały dzierżawione w każdym hello poprzednich 12 tygodni na powitania sam godzinę i hello tego samego dnia

Oprócz A zestaw funkcji, które już istnieją w oryginalnej danych pierwotnych hello, hello innych trzy zestawy funkcji są tworzone za pomocą funkcji hello inżynierii procesu. Zestaw funkcji przechwytywania B bardzo ostatnie żądanie dla rowerów hello. Skonfigurować funkcji przechwytywania C hello żądanie dla rowerów o określonej godzinie. Funkcja ustawiona D przechwytywania żądanie dla rowerów w określonej godziny i dnia tygodnia hello. Hello cztery szkolenia zestawów danych każdy zawiera odpowiednio A zestaw funkcji, A + B, A + B + C i A + B + C + D.

W hello eksperymentu uczenia maszynowego Azure te cztery zestawy danych szkoleniowych są tworzone za pomocą czterech oddziałów z hello wstępnie przetworzonych wejściowego zestawu danych. Z wyjątkiem hello lewej większości gałęzi, każdy z tych gałęzi zawiera [wykonanie skryptu języka R](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) modułu, w którym zestaw funkcji pochodnych (funkcja ustawiona B, C i D), są odpowiednio skonstruowane i dołączany toohello zaimportowany zestaw danych. powitania po rysunku przedstawiono skrypt hello R używany zestaw funkcji toocreate B w drugim gałęzi po lewej stronie powitania.

![Tworzenie funkcji](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

hello w poniższej tabeli przedstawiono porównanie Hello wyniki wydajności hello hello cztery modele. Witaj najlepsze wyniki są wyświetlane przez funkcje A + B + C. Należy pamiętać, że hello zmniejsza szybkość błąd, gdy zestaw dodatkowych funkcji zostaną uwzględnione w danych szkoleniowych hello. Sprawdza naszych założenie, że zestaw funkcji hello B, C zapewniają dodatkowe istotne informacje dotyczące zadań regresji hello. Ale dodawania funkcji hello D prawdopodobnie nie tooprovide każde dodatkowe zmniejszenie hello współczynnik błędów.

![wynik porównania](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a>Przykład 2: Tworzenie funkcji wyszukiwania tekstu
Funkcja engineering jest powszechnie stosowane w tootext powiązanych zadań wyszukiwania, takich jak analiza dokumentu klasyfikacji i wskaźniki nastrojów klientów. Na przykład gdy chcemy tooclassify dokumentów na kilka kategorii typowe założeń jest możliwość hello word/fraz uwzględnione w jednym dokumencie kategorii toooccur mniej prawdopodobne w innej kategorii dokumentu. W innym słowa częstotliwość hello dystrybucji słowa/fraz hello jest możliwe toocharacterize innego dokumentu kategorii. W aplikacjach wyszukiwania tekstu ponieważ pojedynczych zawartość tekstową zwykle służą jako dane wejściowe hello, funkcja hello inżynierii procesu jest wymagane toocreate hello funkcje dotyczące częstotliwości word/frazy.

tooachieve to zadanie, technika o nazwie **Tworzenie skrótu funkcji** jest stosowane tooefficiently Włącz funkcje dowolnego tekstu do indeksów. Zamiast kojarzenie każdego tekstu funkcji (słowa/wyrażenia) tooa określonego indeksu, to funkcje — metoda stosowania funkcji toohello funkcji skrótu i używając ich wartości skrótu jako indeksy bezpośrednio.

W usłudze Azure Machine Learning [Tworzenie skrótu funkcji](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) moduł, który tworzy te word/frazy funkcje wygodny sposób. Poniższej ilustracji przedstawiono przykład za pomocą tego modułu. zestaw danych wejściowych Hello zawiera dwie kolumny: hello klasyfikacji książki z zakresu od 1 too5 i hello przeglądu rzeczywistej zawartości. Celem Hello to [Tworzenie skrótu funkcji](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) modułu jest tooretrieve licznych nowe funkcje, które Pokaż częstotliwość wystąpienie hello hello odpowiadającego wyrazy / wyrażenia s. w hello wybranej książki przeglądu. toouse ten moduł, potrzebujemy hello toocomplete następujące kroki:

* Najpierw wybierz hello kolumny, która zawiera tekst wejściowy hello ("Col2" w tym przykładzie).
* Po drugie, ustawić hello too8 "Hashing bitsize", czyli 2 ^ 8 = 256 funkcje zostaną utworzone. word Hello/faza cały tekst hello będzie indeksów skrótu too256. Parametr Hello "Hashing bitsize" zakresu od 1 too31. Witaj wyrazy wyrażenia są rzadziej toobe skrótu do hello sam indeksu, jeśli ustawieniem dla niego toobe większą liczbę.
* Trzecie Ustaw too2 parametr "N-gramów" hello. Częstotliwość wystąpienie hello unigrams (funkcja dla każdego pojedynczego wyrazu) i bigrams (funkcja dla każdej pary słów sąsiadujące) to pobiera z hello wejściowego tekstu. Hello parametr "N-gramów" może się wahać od 0 too10, wskazujący hello maksymalną liczbę toobe sekwencyjnych słowa objęte funkcją.  

![Moduł "funkcji Hashing"](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Witaj przedstawiony na poniższym rysunku co hello tych nowych funkcji przypominają.

![Przykład "funkcji Hashing"](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Podsumowanie
Funkcje odtworzone i wybranych zwiększenia efektywności hello hello szkolenia procesu, który próbuje tooextract hello najważniejsze informacje zawarte w danych hello. One również poprawić zasilania hello te modele tooclassify hello danych wejściowych dokładnie i wyniki toopredict odsetek więcej niezawodnie. Funkcja inżynieryjne i wyboru można także połączyć learning hello toomake więcej praktyce tractable. Robi to przez rozszerzanie i następnie zmniejszeniu liczby hello funkcje wymagane toocalibrate lub train model. Ze sobą matematycznie rzecz biorąc, model hello tootrain wybrane funkcje hello są minimalny zbiór zmienne niezależne, hello wzorce w danych hello wyjaśnienia, które następnie pomyślnie przewidywania wyników.

Należy pamiętać, że nie zawsze jest zawsze tooperform funkcji engineering lub funkcji wyboru cech. Określa, czy jest potrzebna, lub nie zależy od danych hello mają lub zbierane hello algorytmu, który mamy pobranie i hello cel hello eksperymentu.

