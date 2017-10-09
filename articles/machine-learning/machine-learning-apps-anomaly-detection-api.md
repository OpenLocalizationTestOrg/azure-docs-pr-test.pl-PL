---
title: aaaAzure Machine Learning anomalii wykrywania API | Dokumentacja firmy Microsoft
description: "Interfejs API wykrywania anomalii to przykład skompilowanej za pomocą programu Microsoft Azure Machine Learning wykrycia anomalii w czasie danych serii za pomocą wartości liczbowe, które są równomiernie rozłożone w czasie."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>Wykrywanie anomalii interfejsu API uczenia maszynowego
## <a name="overview"></a>Omówienie
[Interfejs API wykrywania anomalii](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) przykład skompilowanej za pomocą usługi Azure Machine Learning, która wykrywa anomalii w czasie danych serii za pomocą wartości liczbowe, które są równomiernie rozłożone w czasie.

Ten interfejs API może wykryć hello następujące typy nietypowe wzorce w danych w serii. czas:

* **Dodatnie i ujemne trendów**: na przykład po monitorowanie wykorzystania pamięci w przypadku komputerów trendów może być przydatne jako może być świadczy o przeciek pamięci
* **Zmiany zakresu dynamicznego hello wartości**: na przykład podczas monitorowania hello wyjątków zgłaszanych przez usługi w chmurze, zmiany wprowadzone w hello dynamicznego zakresu wartości może wskazywać niestabilności hello kondycji usługi hello i
* **Wzrósł i DIP**: na przykład w przypadku monitorowania hello liczba niepowodzeń logowania w usłudze lub liczbę wyewidencjonowań w witrynie handlu elektronicznego, nagłego lub DIP może wskazywać nietypowe zachowanie.

Te machine learning detektory śledzić takie zmiany wartości przez raport i czas zmiany zachodzące w ich wartości jako wyniki anomalii. Nie wymaga strojenia próg ad hoc i ich wyniki mogą być używane toocontrol false dodatniej stawki. wykrywania anomalii Hello interfejsu API jest przydatne w kilku scenariuszach, takich jak monitorowanie poprzez śledzenie wskaźników KPI w czasie, użycie usługi monitorowania przy użyciu metryk, takich jak liczbę wyszukiwań, liczby kliknięć, monitorowanie wydajności za pośrednictwem liczników, jak pliki pamięci, Procesora, odczytuje, itp. w czasie.

Oferta wykrywania anomalii Hello jest dostarczany z tooget przydatnych narzędzi, który został uruchomiony.

* Witaj [aplikacji sieci web](http://anomalydetection-aml.azurewebsites.net/) pomaga ocenić i wizualizacja wyników hello wykrywania anomalii interfejsów API na podstawie danych.

> [!NOTE]
> Spróbuj **rozwiązania IT anomalii Insights** obsługiwane przez [tego interfejsu API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)
> 
> tooget tooyour subskrypcji platformy Azure wdrożyć to rozwiązanie tooend <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **zacznij tutaj >**</a>
> 
>

## <a name="api-deployment"></a>Wdrażania interfejsu API
W kolejności toouse hello interfejsu API należy ją wdrożyć tooyour subskrypcji platformy Azure, w którym będzie obsługiwana jako usługi sieci web uczenie maszynowe Azure.  Można to zrobić z hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  To spowoduje wdrożenie dwóch usług sieci Web uczenie maszynowe Azure (i ich powiązane zasoby) tooyour subskrypcji platformy Azure — jeden dla wykrywania anomalii z wykrywaniem sezonowości i bez wykrywania sezonowości.  Po zakończeniu wdrażania hello będzie możliwe toomanage swoje interfejsy API z hello [usług sieci web uczenie maszynowe Azure](https://services.azureml.net/webservices/) strony.  Na tej stronie można będzie można toofind stanie lokalizacji punktu końcowego, klucze interfejsu API, a także przykładowy kod do wywoływania interfejsu API hello.  Bardziej szczegółowe informacje są dostępne [tutaj](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Skalowanie hello interfejsu API
Domyślnie wdrożenia mają bezpłatne i testowania plan rozliczeniowy obejmującej 1000 transakcji miesięcznie i obliczeń 2 godziny/miesiąc.  Można uaktualnić tooanother plan zgodnie z potrzebami.  Nie są dostępne informacje o cenach hello różnych planów [tutaj](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) w obszarze "Cennik produkcji interfejsu API sieci Web".

## <a name="managing-aml-plans"></a>Zarządzanie AML plany 
Możesz zarządzać planu rozliczeniowego [tutaj](https://services.azureml.net/plans/).  Nazwa planu Hello będzie opierać się na powitania Nazwa grupy zasobów, wybrana podczas wdrażania hello interfejsu API, a także ciąg, który jest unikatowy tooyour subskrypcji.  Instrukcje dotyczące sposobu tooupgrade planu są dostępne [tutaj](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) w sekcji "Zarządzanie planami rozliczeń" hello.

## <a name="api-definition"></a>Definicja interfejsu API
Witaj usługi sieci web udostępnia interfejs API opartego na interfejsie REST za pośrednictwem protokołu HTTPS, które mogą być używane w różnych sposobów, łącznie z sieci web lub aplikacji mobilnej, R, Python, Excel, itp.  Wyślij usługi toothis czasu serii danych za pośrednictwem wywołania interfejsu API REST i uruchomieniu kombinację hello trzy typy anomalii opisane poniżej.

## <a name="calling-hello-api"></a>Wywołanie interfejsu API hello
W kolejności toocall hello interfejsu API konieczne będzie tooknow hello punktu końcowego lokalizacji i klucz interfejsu API.  Oba te, wraz z przykładowy kod wywołujący interfejs API hello, są dostępne z hello [usług sieci web uczenie maszynowe Azure](https://services.azureml.net/webservices/) strony.  Przejdź toohello żądanego interfejsu API, a następnie kliknij przycisk toofind kartę "Consume" hello je.  Należy pamiętać, że można wywołać interfejsu API hello jako interfejsu API programu Swagger (tj. z parametru adresu URL hello `format=swagger`) lub jako nie - interfejsu API programu Swagger (tzn. bez hello `format` parametr adresu URL).  Witaj przykładowy kod w formacie hello struktury Swagger.  Poniżej jest przykładowe żądanie i odpowiedź w formacie bez struktury Swagger.  Te przykłady są toohello sezonowości endpoint.  punkt końcowy z systemem innym niż sezonowości Hello jest podobne.

### <a name="sample-request-body"></a>Treść żądania próbki
Żądanie hello zawiera dwa obiekty: `Inputs` i `GlobalParameters`.  W żądaniu przykład hello poniżej, niektóre parametry są wysyłane jawnie a inni nie (Przewiń w dół pełną listę parametrów dla każdego punktu końcowego).  Parametry, które nie są wysyłane jawnie w żądaniu hello użyje wartości domyślnych hello podane poniżej.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Przykładowa odpowiedź
Należy zauważyć, że w kolejności toosee hello `ColumnNames` pole musi zawierać `details=true` jako parametr adresu URL w żądaniu.  Zobacz poniższych tabelach hello znaczenie hello za każde z tych pól.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>Wynik interfejsu API
Hello API wynik jest używane do uruchamiania wykrywania anomalii w danych serii-okresach czasu. Witaj interfejsu API przeprowadza liczbą czujników anomalii na powitania danych i zwraca wyniki anomalii. Witaj na poniższej ilustracji przedstawiono przykład anomalii powitalne tego interfejsu API wynik może wykryć. Ta szeregów czasowych ma 2 różne zmiany na poziomie, a nagłego 3. kropki Hello red Pokaż razem hello, na które hello zmiany poziomu zostanie wykryte, podczas punktów hello czarny Pokaż nagłego hello wykryto.
![Wynik interfejsu API][1]

### <a name="detectors"></a>Detektory
wykrywanie anomalii Hello interfejs API obsługuje detektory w 3 szerokie kategorie. Szczegółowe informacje o określonych parametrów wejściowych i wyjściowych dla każdego detektora znajdują się w hello w poniższej tabeli.

| Wykrywacz kategorii | Wykrywanie | Opis | Parametry wejściowe | dane wyjściowe |
| --- | --- | --- | --- | --- |
| Detektory kolekcji |Wykrywanie TSpike |Wykrywanie wzrostów i oparte na powitania daleko, których wartości pochodzą z Kwartyle pierwszy i trzeci DIP |*tspikedetector.sensitivity:* przyjmuje wartość całkowitą zakresu hello 1-10, domyślne: 3; Wyższe wartości będzie przechwytywać więcej wartości skrajne, dzięki czemu mniej poufne |TSpike: wartości binarne — "1" w przypadku wykrycia kolekcji/dip, "0" w inny sposób |
| Detektory kolekcji | Wykrywanie ZSpike |Wykrywania impulsy i DIP oparte na jak daleko hello punktów danych są od ich średniej |*zspikedetector.sensitivity:* zająć domyślne 1-10, liczbę całkowitą z zakresu hello: 3; Wyższe wartości będzie przechwytywać więcej wartości skrajne, dzięki czemu mniej poufne |ZSpike: wartości binarne — "1" w przypadku wykrycia kolekcji/dip, "0" w inny sposób | |
| Wykrywanie powolnego Trend |Wykrywanie powolnego Trend |Wykrywanie powolnego trend dodatnią zgodnie z harmonogramem hello czułości zestawu |*trenddetector.sensitivity:* próg na wynik detektora (domyślne: 3,25, 3,25 – 5 jest tooselect uzasadnione zakres od; hello wyższej hello mniej liter) |tscore: liczbą zmiennoprzecinkową reprezentujący wynik anomalii na tendencji |
| Detektory zmiany poziomu | Poziom dwukierunkowego wykrywanie zmian |Wykrywanie zarówno w górę i zmień poziom w dół zgodnie z harmonogramem hello ustawić czułość |*bileveldetector.sensitivity:* próg na wynik detektora (domyślne: 3,25, 3,25 – 5 jest tooselect uzasadnione zakres od; hello wyższej hello mniej liter) |rpscore: liczba zmiennoprzecinkowa reprezentująca wynik anomalii w górę i w dół zmiany poziomu | |

### <a name="parameters"></a>Parametry
Bardziej szczegółowe informacje dotyczące tych parametrów wejściowych jest wymienione w poniższej tabeli hello:

| Parametry wejściowe | Opis | Ustawienie domyślne | Typ | Prawidłowy zakres | Sugerowany zakres |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Historia (w # punktów danych) używane do obliczeń wynik anomalii |500 |Liczba całkowita |10-2000 |Zależne od szeregu czasowego |
| detectors.spikesdips | Określa, czy toodetect tylko wzrósł, tylko DIP i/lub |Zarówno |Wyliczenie |Oba nagłego, DIP |Zarówno |
| bileveldetector.sensitivity |Czułość na poziomie dwukierunkowego zmienić detektora. |3.25 |O podwójnej precyzji |Brak |3,25-5 (mniejsze wartości oznaczają więcej liter) |
| trenddetector.sensitivity |Czułość dla detektora trend dodatnią. |3.25 |O podwójnej precyzji |Brak |3,25-5 (mniejsze wartości oznaczają więcej liter) |
| tspikedetector.sensitivity |Czułość dla detektora TSpike |3 |Liczba całkowita |1-10 |3 – 5 (mniejsze wartości oznaczają więcej liter) |
| zspikedetector.sensitivity |Czułość dla detektora ZSpike |3 |Liczba całkowita |1-10 |3 – 5 (mniejsze wartości oznaczają więcej liter) |
| postprocess.tailRows |Liczba hello najnowsze dane punktów toobe przechowywane w wynikach dane wyjściowe hello |0 |Liczba całkowita |0 (Zachowaj wszystkie punkty danych), lub określ liczbę punktów tookeep w wynikach |Nie dotyczy |

### <a name="output"></a>Dane wyjściowe
Hello interfejsu API uruchamia wszystkie detektory na podstawie czasu serii danych i zwraca wyniki anomalii i wskaźniki kolekcji binarne dla każdego punktu w czasie. w poniższej tabeli Hello przedstawiono dane wyjściowe z hello interfejsu API. 

| dane wyjściowe | Opis |
| --- | --- |
| Time |Sygnatury czasowe z danych pierwotnych lub dane zagregowane (i/lub) kalkulacyjne Jeśli agregacji (i/lub) brakuje przypisywania danych jest stosowany. |
| Dane |Wartości od danych pierwotnych lub dane zagregowane (i/lub) kalkulacyjne w przypadku agregacji (i/lub) brakuje zastosowano przypisywania danych |
| TSpike |Wskaźnik binarny tooindicate czy kolekcji są wykrywane przez wykrywacz TSpike |
| ZSpike |Wskaźnik binarny tooindicate czy kolekcji są wykrywane przez wykrywacz ZSpike |
| rpscore |Przestawne numer anomalii reprezentująca wynik na zmiany poziomu dwukierunkowych |
| rpalert |wartość 1/0 wskazującą, czy istnieje poziom dwukierunkowego zmienić anomalii oparte na hello czułości wejściowych |
| tscore |Przestawne numer anomalii reprezentująca wynik na dodatnią tendencji |
| talert |wartość 1/0 wskazującą jest anomalii trend dodatnią, oparte na hello czułości wejściowych |

## <a name="scorewithseasonality-api"></a>ScoreWithSeasonality interfejsu API
Hello ScoreWithSeasonality interfejsu API jest używane do uruchamiania wykrywania anomalii w szeregu czasowego, mające okresach wzorce. Ten interfejs API jest przydatne toodetect odchylenia okresach wzorce.  
Witaj poniższej ilustracji przedstawiono przykład nieprawidłowości wykryte w serii okresach czasu. szeregów czasowych Hello ma jeden kolekcji (hello 1 czarna kropka), DIP dwóch (2 czarna kropka hello i jeden na końcu hello) i jeden zmiany poziomu (czerwoną kropkę). Należy pamiętać, że oba hello dip w środku hello hello szeregów czasowych i zmiany poziomu hello są discernable tylko po usunięciu z serii hello okresach składników.
![Sezonowości interfejsu API][2]

### <a name="detectors"></a>Detektory
detektory Hello w punkcie końcowym sezonowości hello są podobne toohello te punktu końcowego z systemem innym niż sezonowości hello, ale nieco różne nazwy parametrów (wymienione poniżej).

### <a name="parameters"></a>Parametry

Bardziej szczegółowe informacje dotyczące tych parametrów wejściowych jest wymienione w poniższej tabeli hello:

| Parametry wejściowe | Opis | Ustawienie domyślne | Typ | Prawidłowy zakres | Sugerowany zakres |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Interwał agregacji w sekundach do agregowania danych wejściowych szeregów czasowych |0 (nie agregacji jest wykonywane) |Liczba całkowita |0: w przeciwnym razie Pomiń agregacji, > 0 |dzień too1 5 minut, zależne od szeregu czasowego |
| preprocess.aggregationFunc |Funkcja używana do agregowania danych do hello określony AggregationInterval |Średnia |Wyliczenie |Średnia, sum, długość |Nie dotyczy |
| preprocess.replaceMissing |Brak danych tooimpute użyte wartości |lkv (Ostatnia znana wartość) |Wyliczenie |zero, lkv, średnia |Nie dotyczy |
| detectors.historyWindow |Historia (w # punktów danych) używane do obliczeń wynik anomalii |500 |Liczba całkowita |10-2000 |Zależne od szeregu czasowego |
| detectors.spikesdips | Określa, czy toodetect tylko wzrósł, tylko DIP i/lub |Zarówno |Wyliczenie |Oba nagłego, DIP |Zarówno |
| bileveldetector.sensitivity |Czułość na poziomie dwukierunkowego zmienić detektora. |3.25 |O podwójnej precyzji |Brak |3,25-5 (mniejsze wartości oznaczają więcej liter) |
| postrenddetector.sensitivity |Czułość dla detektora trend dodatnią. |3.25 |O podwójnej precyzji |Brak |3,25-5 (mniejsze wartości oznaczają więcej liter) |
| negtrenddetector.sensitivity |Czułość dla detektora trend ujemna. |3.25 |O podwójnej precyzji |Brak |3,25-5 (mniejsze wartości oznaczają więcej liter) |
| tspikedetector.sensitivity |Czułość dla detektora TSpike |3 |Liczba całkowita |1-10 |3 – 5 (mniejsze wartości oznaczają więcej liter) |
| zspikedetector.sensitivity |Czułość dla detektora ZSpike |3 |Liczba całkowita |1-10 |3 – 5 (mniejsze wartości oznaczają więcej liter) |
| seasonality.enable |Czy analizy sezonowości toobe odbywa się |Wartość true |Wartość logiczna |wartość true, false |Zależne od szeregu czasowego |
| seasonality.numSeasonality |Maksymalna liczba cykli okresowe toobe wykryto |1 |Liczba całkowita |1, 2 |1-2 |
| seasonality.transform |Czy okresach trend części należy usunąć przed zastosowaniem wykrywania anomalii (i) |deseason |Wyliczenie |Brak, deseason deseasontrend |Nie dotyczy |
| postprocess.tailRows |Liczba hello najnowsze dane punktów toobe przechowywane w wynikach dane wyjściowe hello |0 |Liczba całkowita |0 (Zachowaj wszystkie punkty danych), lub określ liczbę punktów tookeep w wynikach |Nie dotyczy |

### <a name="output"></a>Dane wyjściowe
Hello interfejsu API uruchamia wszystkie detektory na podstawie czasu serii danych i zwraca wyniki anomalii i wskaźniki kolekcji binarne dla każdego punktu w czasie. w poniższej tabeli Hello przedstawiono dane wyjściowe z hello interfejsu API. 

| dane wyjściowe | Opis |
| --- | --- |
| Time |Sygnatury czasowe z danych pierwotnych lub dane zagregowane (i/lub) kalkulacyjne Jeśli agregacji (i/lub) brakuje przypisywania danych jest stosowany. |
| OriginalData |Wartości od danych pierwotnych lub dane zagregowane (i/lub) kalkulacyjne w przypadku agregacji (i/lub) brakuje zastosowano przypisywania danych |
| ProcessedData |Jedną z następujących hello: <ul><li>Sezonowo szeregów czasowych, jeśli wykryto znaczących sezonowości deseason opcji;</li><li>sezonowo dostosowane i Beztrendowy szeregów czasowych, jeśli wykryto znaczących sezonowości i wybrana opcja deseasontrend</li><li>w przeciwnym razie jest to hello taki sam jak OriginalData</li> |
| TSpike |Wskaźnik binarny tooindicate czy kolekcji są wykrywane przez wykrywacz TSpike |
| ZSpike |Wskaźnik binarny tooindicate czy kolekcji są wykrywane przez wykrywacz ZSpike |
| BiLevelChangeScore |Przestawne numer anomalii reprezentująca wynik na zmiany poziomu |
| BiLevelChangeAlert |1/0 wartość wskazującą jest anomalii zmiany poziomu, oparte na hello czułości wejściowych |
| PosTrendScore |Przestawne numer anomalii reprezentująca wynik na dodatnią tendencji |
| PosTrendAlert |wartość 1/0 wskazującą jest anomalii trend dodatnią, oparte na hello czułości wejściowych |
| NegTrendScore |Przestawne numer anomalii reprezentująca wynik na ujemnej tendencji |
| NegTrendAlert |wartość 1/0 wskazującą jest anomalii trend ujemna, oparte na hello czułości wejściowych |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

