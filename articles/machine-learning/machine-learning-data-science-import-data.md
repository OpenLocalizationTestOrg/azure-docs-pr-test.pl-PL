---
title: "aaaImport danych do usługi Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Jak tooimport dane do usługi Azure Machine Learning Studio z różnych źródeł danych. Dowiedz się, jakie typy danych i formatów danych są obsługiwane."
keywords: "Importowanie danych, formatu danych, typy danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importowanie danych szkoleniowych do usługi Azure Machine Learning Studio z różnych źródeł danych
toouse własnych danych w usłudze Machine Learning Studio toodevelop i train rozwiązania analizy predykcyjnej można wykonywać następujące czynności: 

* przekazywanie danych z **pliku lokalnego** wyprzedzenia czasu z toocreate Twojego dysku twardego modułu zestawu danych, w obszarze roboczym
* dostęp do danych z jednego z kilku **źródeł danych w trybie online** eksperymentu jest uruchomiona przy użyciu hello [i zaimportuj dane] [ import-data] modułu 
* Użyj danych z innej usługi Azure Machine learning **eksperymentu** zapisane jako zestawu danych
* Użyj danych z lokalnego **bazy danych programu SQL Server**

Każdą z tych opcji jest opisany w tematach hello menu hello poniżej. Tych tematach opisano, jak tooimport danych na podstawie tych danych różnych źródeł toouse w usłudze Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Wiele przykładowych zestawów danych są dostępne w usłudze Machine Learning Studio używanej dla danych szkoleniowych. Aby uzyskać informacje o tych, zobacz [Użyj hello przykładowych zestawów danych w usłudze Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).
> 
> 

W tym temacie wprowadzające również omówiono sposób tooget danych gotowe do użycia w usłudze Machine Learning Studio oraz opis, które formaty danych i typy danych są obsługiwane. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Przygotowanie danych do użycia w usłudze Azure Machine Learning Studio
Usługa Machine Learning Studio jest zaprojektowana toowork prostokątne lub tabelarycznym danych, takich jak dane tekstowe, rozdzielany lub strukturę danych z bazy danych, chociaż w niektórych sytuacjach może być używany nieregularnych danych.

Najlepiej danych jest stosunkowo czysty. Oznacza to, że należy tootake nad problemy, takie jak parametry bez cudzysłowów przed przekazaniem hello dane do eksperymentu.

Jednak Brak modułów dostępnych w usłudze Machine Learning Studio umożliwiające niektórych manipulacji danymi w ramach eksperymentu. W zależności od algorytmów uczenia maszynowego hello należy używać, może być konieczne toodecide jak będzie obsługiwać danych strukturalnych problemy, takie jak brak wartości i rozrzedzone danych, a moduły, które mogą pomóc, z których. Szukaj w hello **transformacji danych** części palety modułów hello modułów, które wykonują te funkcje.

W dowolnym momencie w eksperymencie można wyświetlać lub pobrania danych hello jest generowany przez moduł, klikając hello port wyjściowy. W zależności od modułu hello mogą być pobierania różne opcje dostępne lub możliwe toovisualize hello danych może być przeglądarki sieci web w usłudze Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Dane formaty i typy danych obsługiwane
Można je zaimportować do eksperymentu wiele typów danych, w zależności od tego, jaki mechanizm można używać danych tooimport i której pochodzi od:

* Zwykły tekst (txt)
* Wartości rozdzielanych przecinkami (CSV) z nagłówkiem (.csv) lub bez (. nh.csv)
* Tabulatorem tabulatorami (TSV z nagłówkiem (.tsv) lub bez) (. nh.tsv)
* Plik programu Excel
* Tabeli platformy Azure
* Tabelę programu hive
* Tabela bazy danych SQL
* Wartości OData
* Dane SVMLight (.svmlight) (zobacz hello [definicji SVMLight](http://svmlight.joachims.org/) dla informacji o formacie)
* Atrybut danych relacji File Format (ARFF) (.arff) (zobacz hello [definicji ARFF](http://weka.wikispaces.com/ARFF) dla informacji o formacie)
* Plik zip (.zip)
* Plik obiektu lub obszar roboczy R (. RData)

W przypadku importowania danych w formacie, takich jak ARFF zawierający metadane, Machine Learning Studio korzysta z tej pozycji hello toodefine metadanych i typu danych każdej kolumny.

Po zaimportowaniu danych, takich jak format TSV lub CSV, który nie zawiera metadanych usługi Machine Learning Studio wnioskuje hello typ danych dla każdej kolumny przez hello dane próbkowania. Jeśli dane hello również nie ma nagłówki kolumn, Machine Learning Studio udostępnia domyślne nazwy.

Można jawnie określ lub zmień hello nagłówki i typy danych kolumn za pomocą hello [edytowanie metadanych][edit-metadata].

następujące Hello **typy danych** są rozpoznawane przez Machine Learning Studio:

* Ciąg
* Liczba całkowita
* O podwójnej precyzji
* Wartość logiczna
* Data i godzina
* Zakres czasu

Usługa Machine Learning Studio używa typu danych wewnętrznych o nazwie ***tabeli danych*** toopass danych między modułami. Można jawnie przekonwertować danych w formacie tabeli danych przy użyciu hello [przekonwertować tooDataset] [ convert-to-dataset] modułu.

Każdy moduł akceptującego formatów innych niż tabela danych przekonwertuje hello danych tooData tabeli dyskretnie przed przekazaniem go toohello następnego modułu.

Jeśli to konieczne, możesz przekonwertować format tabeli danych do woluminu CSV, TSV, ARFF lub format SVMLight przy użyciu innych modułów konwersji.
Szukaj w hello **konwersje Format danych** części palety modułów hello modułów, które wykonują te funkcje.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
