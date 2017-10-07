---
title: "aaaClean i przygotowania danych do usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Tooprepare danych wstępnie procesu i wyczyść go do uczenia maszynowego."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Dane tooprepare zadania uczenia maszynowego rozszerzone
Przetwarzanie wstępne i czyszczenia danych są ważne zadania, które zwykle należy przeprowadzić przed zestawu danych można skutecznie uczenia maszynowego. Dane pierwotne jest często zakłócenia i zawodnych i może brakować wartości. Przy użyciu tych danych do modelowania może wygenerować błędne wyniki. Te zadania są częścią hello zespołu danych nauki procesu (TDSP) i zwykle wykonaj początkowej eksploracji toodiscover użyć zestawu danych i przetwarzanie wstępne hello planu wymagane. Aby uzyskać szczegółowe instrukcje dotyczące procesu TDSP hello, zobacz hello kroki opisane w hello [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Przetwarzanie wstępne i zadania oczyszczania, takich jak hello zadanie Eksploracja danych, może zostać przeprowadzona w różnych środowiskach, takich jak SQL lub Hive lub Azure Machine Learning Studio oraz z różnych narzędzi i języków, takich jak R lub Python, gdy dane znajdują się w zależności przechowywane i sposób formatowania. Ponieważ TDSP ma charakter iteracyjny charakter, te zadania może odbywać się w różnych kroków w przepływie pracy hello hello procesu.

W tym artykule przedstawiono różne pojęcia dotyczące przetwarzania danych i zadań, które można podjąć przed lub po pozyskaniu danych do usługi Azure Machine Learning.

Na przykład Eksploracja danych i przetwarzanie wstępne wykonywane w usłudze Azure Machine Learning studio, zobacz hello [wstępne przetworzenie danych w usłudze Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) wideo.

## <a name="why-pre-process-and-clean-data"></a>Dlaczego wstępnie przetworzyć i czyszczenia danych?
Rzeczywistych dane są zbierane z różnych źródeł i procesy i może zawierać nieprawidłowości lub uszkodzone dane obniżania jakości hello hello zestawu danych. Witaj typowych danych jakości problemów, które powstają są:

* **Niekompletne**: danych nie ma atrybutów lub zawierające brakujące wartości.
* **Zakłócenia**: dane zawierają rekordy błędne lub odstające.
* **Niespójne**: dane zawierają rekordy powodujące konflikt lub niezgodności.

Jakości danych jest wymagane w przypadku modeli predykcyjnych jakości. tooavoid "pamięci w pamięci out" i poprawy jakości danych i w związku z tym modelu wydajności, jest konieczne tooconduct danych kondycji ekranu toospot danych wystawia wczesne i podejmowanie decyzji o hello odpowiadającego przetwarzania danych i czyszczenie kroki.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Co to są niektóre ekrany kondycji typowych danych, które są wykorzystywane?
Sprawdzamy hello ogólnej jakości danych, sprawdzając:

* Witaj liczba **rekordów**.
* Witaj liczba **atrybuty** (lub **funkcje**).
* Atrybut Hello **typy danych** (nominalnego, numer porządkowy lub ciągłe).
* Witaj liczba **brakujące wartości**.
* **Składniowej** hello danych.
  * Jeśli dane hello TSV lub CSV, sprawdź, czy hello kolumny separatorów i separatory wierszy zawsze poprawnie oddzielnych kolumn i wierszy.
  * Jeśli hello danych jest w formacie HTML i XML, sprawdź, czy danych hello jest poprawnie sformułowany oparte na ich odpowiednich standardów.
  * Podczas analizowania może być również konieczne w kolejności tooextract strukturę informacje z częściową strukturą lub bez struktury danych.
* **Niespójne dane rekordów**. Sprawdź zakres wartości hello są dozwolone. np. Jeżeli dane hello GPA studentów, sprawdź, czy jest hello GPA Witaj wyznaczone zakresu, powiedz 0 ~ 4.

Po znalezieniu problemy z danymi, **przetwarzania czynności** są konieczne, który często pociąga za sobą czyszczenia brakujące wartości, normalizacji danych, dyskretyzacji, tooremove przetwarzania tekstu i/lub Zastąp osadzonych znaków, które mogą wpływać na Wyrównywanie danych mieszane typy danych wspólnych pól i inne.

**Usługa Azure Machine Learning zużywa danych tabelarycznych sformułowany**.  Jeśli dane hello jest już w formie tabelarycznej, przetwarzanie wstępne danych można wykonać bezpośrednio z usługi Azure Machine Learning w hello Machine Learning Studio.  Jeśli dane nie są w formie tabelarycznej, że jest on analizowanie kodu XML może być wymagane w kolejności tooconvert hello dane tootabular formularza.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Jakie są najważniejsze zadania hello przetwarzanie wstępne danych?
* **Czyszczenie danych**: wypełnić lub brakujące wartości, wykrywaniu i usuwaniu danych zakłócenia i wartości oddalonych.
* **Przekształcenia danych**: normalizacji danych tooreduce wymiarów i szumu.
* **Redukcja danych**: Przykładowe rekordów danych lub atrybutów w celu łatwiejszej obsługi danych.
* **Dyskretyzacji danych**: Convert ciągłego atrybuty atrybuty toocategorical dla łatwość użycia z niektórych machine learning metod.
* **Czyszczenie tekstu**: usunął osadzonych znaków, które mogą spowodować niespójność danych, np. kartach osadzone w pliku danych tabulatorem osadzonych nowe wiersze, które mogą być dzielone rekordów itp.

Poniższe rozdziały zawierają Hello szczegółowo opisano niektóre z tych kroków przetwarzania danych.

## <a name="how-toodeal-with-missing-values"></a>Jak toodeal z brakującymi wartości?
toodeal z brakującymi wartościami, najlepiej jest toofirst zidentyfikować hello Przyczyna dla hello brakuje wartości toobetter dojście hello problem. Typowe metody obsługi brakujące wartości są:

* **Usuwanie**: Usuń rekordy z brakującymi wartościami
* **Fikcyjny podstawienia**: Zamień brakujące wartości fikcyjnej wartości: np., *nieznany* dla kategorii lub równa 0 dla wartości liczbowe.
* **Oznacza podstawienia**: Jeśli hello brakujące dane liczbowe, Zamień hello brakujące wartości średniej hello.
* **Częste podstawienia**: hello brakujące dane są podzielone na kategorie, Zastąp hello Brak wartości elementu najczęstsze hello
* **Podstawienie regresji**: Użyj Brak tooreplace metody regresji wartości z wartościami uwzględniona.  

## <a name="how-toonormalize-data"></a>Jak toonormalize danych?
Tooa wartości liczbowe ponownie skaluje normalizacji danych określony zakres. Metody normalizacji popularnych danych obejmują:

* **Min i Max normalizacji**: liniowo przekształcenie zakres tooa danych hello, co oznacza od 0 do 1, gdy hello wartość minimalna jest skalowana too0 i too1 wartości maksymalnej.
* **Wynik Z normalizacji**: skalować dane na podstawie średnią i odchylenie standardowe: dzielenia hello różnica między hello danych i oznacza hello przez hello odchylenie standardowe.
* **Skalowanie dziesiętną**: skalowanie hello danych przez przenoszenie dziesiętnego hello hello wartości atrybutu.  

## <a name="how-toodiscretize-data"></a>Jak toodiscretize danych?
Dane można zdyskretyzować konwertując ciągłego wartości atrybutów toonominal lub interwałów. W ten sposób niektóre sposoby są następujące:

* **Szerokość równości Binning**: podział zakresu hello wszystkich możliwych wartości atrybutu N grup hello sam rozmiar i przypisz hello wartości, które wchodzą w pojemniku o numerze bin hello.
* **Wysokość równości Binning**: dzielenia zakresu hello wszystkich możliwych wartości atrybutu w grupach N, każdy z nich zawiera hello samą liczbę wystąpień, a następnie przypisywać hello wartości mieszczące się w pojemniku z hello bin numer.  

## <a name="how-tooreduce-data"></a>Jak tooreduce danych?
Istnieją różne metody tooreduce rozmiar danych łatwiejsze obsługi danych. W zależności od rozmiaru i hello domeny danych można zastosować hello następujące metody:

* **Zarejestruj próbkowania**: Przykładowe hello rekordów danych i wybierać tylko hello reprezentatywnego podzestawu z hello danych.
* **Atrybut próbkowania**: wybierać tylko podzestaw hello najważniejsze atrybuty hello danych.  
* **Agregacja**: podział danych hello grup i przechowywania hello numerów dla każdej grupy. Na przykład hello Przychód dzienny liczby łańcuch restauracji za pośrednictwem hello ostatnich lat 20 może być agregowany toomonthly przychodu tooreduce hello rozmiar danych hello.  

## <a name="how-tooclean-text-data"></a>Jak dane tekstowe tooclean?
**Pola tekstowe w danych tabelarycznych** może zawierać znaki, które wpływają na kolumny wyrównanie i/lub rekord granic. Np. osadzony karty w pliku tabulatorem niezgodność kolumny Przyczyna i osadzone znaki nowego wiersza Podziel rekordów wierszy. Nieprawidłowe kodowanie Obsługa podczas zapisu/odczytu tekstu tekstu prowadzi utraty tooinformation niezamierzonego wprowadzenia znaki niemożliwe do odczytania, np. wartości null i może również wpływają na tekst analizy. Zachować ostrożność podczas analizowania i edytowania mogą być wymagane w kolejności pól tekstowych tooclean dla prawidłowego wyrównania i/lub tooextract strukturę danych ze źródła danych bez struktury lub częściowo ustrukturyzowanych tekstu.

**Eksploracja danych** zapewnia wczesne wgląd w dane hello. Szereg problemów danych może być niepokrytego w tym kroku i odpowiednich metod może być zastosowane tooaddress tych problemów.  Jest ważne tooask pytania, takie jak co to jest źródło hello hello problemu i jak problem hello mogły zostać wprowadzone. Pomaga to również zdecydować o kroki przetwarzania danych hello tego toobe należy podjąć tooresolve je. rodzaj Hello szczegółowe informacje, że jeden zamierza tooderive hello danych można też nakładu pracy przetwarzania danych hello tooprioritize używane.

## <a name="references"></a>Dokumentacja
> *Wyszukiwania danych: Koncepcjach i technikach*, wydanie trzecie Morgan Kaufmann 2011 r. Jiawei Han, Micheline Kamber i Jian Pei
> 
> 

