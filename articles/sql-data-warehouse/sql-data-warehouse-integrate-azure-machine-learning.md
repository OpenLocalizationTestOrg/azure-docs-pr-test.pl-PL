---
title: "aaaUse usługi Azure Machine Learning z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Samouczek korzystania z usługi Azure Machine Learning z usługą Azure SQL Data Warehouse w celu opracowywania rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Użyj usługi Azure Machine Learning z usługą Magazyn danych SQL
Usługa Azure Machine Learning to usługa analizy predykcyjnej w pełni zarządzana, użyj modeli predykcyjnych toocreate względem danych w magazynie danych SQL, a następnie opublikować jako gotowe do użycia usług sieci web. Można dowiedzieć się hello podstaw analizy predykcyjnej i uczenia maszynowego, odczytując [tooMachine wprowadzenie Learning na platformie Azure][Introduction tooMachine Learning on Azure].  Można następnie dowiesz się, jak toocreate, uczenia, wynik i przetestowania modelu uczenia maszynowego przy użyciu hello [tworzenie eksperymentu samouczek][Create experiment tutorial].

W tym artykule przedstawiono sposób hello toodo po użyciu hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Odczytywanie danych z programu toocreate bazy danych, szkolenia i score model predykcyjny
* Zapisu bazy danych tooyour danych

## <a name="read-data-from-sql-data-warehouse"></a>Odczyt danych z magazynu danych SQL
Firma Microsoft będzie odczytywać dane z tabeli produktu w bazie danych AdventureWorksDW hello.

### <a name="step-1"></a>Krok 1
Uruchom nowy eksperyment, klikając + nowy u dołu okna Machine Learning Studio hello hello wybierz EKSPERYMENTU, a następnie wybierz, pusty eksperymentu. Wybierz hello domyślne nazwy u góry hello hello kanwy eksperymentu i zmień jego nazwę na toosomething opisowy, na przykład Prognozowanie cen roweru.

### <a name="step-2"></a>Krok 2
Poszukaj moduł czytnika hello w palecie hello zestawów danych i moduły powitania po lewej stronie kanwy eksperymentu hello. Przeciągnij hello modułu toohello eksperymentu w obszarze roboczym.
![][drag_reader]

### <a name="step-3"></a>Krok 3
Wybierz moduł czytnika hello i wypełnij hello w okienku właściwości.

1. Wybierz bazę danych SQL Azure jako hello źródła danych.
2. Nazwa serwera bazy danych: Nazwa serwera hello typu. Można użyć hello [portalu Azure] [ Azure portal] toofind to.

![][server_name]

1. Nazwa bazy danych: Nazwa typu hello bazy danych na serwerze hello właśnie zostało określone.
2. Nazwa konta użytkownika serwera: nazwa użytkownika hello typu konta, które ma uprawnienia dostępu do bazy danych hello.
3. Hasło konta użytkownika serwera: Podaj hasło hello hello określone konto użytkownika.
4. Dowolny certyfikat serwera Zaakceptuj: użyć tej opcji (mniej bezpieczna opcja), jeśli tooskip recenzowania hello certyfikatu witryny, przed przeczytaniem danych.
5. Zapytanie bazy danych: wprowadź instrukcję SQL opisujący hello dane, które mają tooread. W takim przypadku firma Microsoft będzie odczytywać dane z tabel produktu za pomocą hello następującego zapytania.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Krok 4
1. Uruchom eksperyment hello klikając przycisk Uruchom obszarze kanwy eksperymentu hello.
2. Po zakończeniu eksperymentu hello moduł czytnika hello będzie miał tooindicate zielony znacznik wyboru, która została pomyślnie ukończona. Zwróć uwagę, również hello bieżący stan w prawym górnym rogu hello zakończone.

![][run]

1. toosee hello importowanych danych, kliknij port wyjściowy hello u dołu hello hello samochodów zestawu danych i wybierz wizualizacja.

## <a name="create-train-and-score-a-model"></a>Tworzenie, uczenie i score model
Teraz można używać tego elementu dataset do:

* Tworzenie modelu: przetwarzanie danych i zdefiniować funkcji
* Train hello model: Wybieranie i stosowanie algorytmu uczenia
* Oceny i testowania hello modelu: przewidywanie nowych cen rowerów

![][model]

więcej informacji na temat sposobu toocreate, uczenia, generowanie wyników i testowanie hello Użyj modelu uczenia maszynowego toolearn [tworzenie eksperymentu samouczek][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Zapis tooAzure danych magazynu danych SQL
Firma Microsoft będzie zapisywać tabeli tooProductPriceForecast zestaw wyników hello w bazie danych AdventureWorksDW hello.

### <a name="step-1"></a>Krok 1
Poszukaj hello moduł zapisu w palecie hello zestawów danych i moduły powitania po lewej stronie kanwy eksperymentu hello. Przeciągnij hello modułu toohello eksperymentu w obszarze roboczym.

![][drag_writer]

### <a name="step-2"></a>Krok 2
Wybierz moduł zapisywania hello i wypełnij hello w okienku właściwości.

1. Wybierz bazę danych SQL Azure jako hello miejsce docelowe danych.
2. Nazwa serwera bazy danych: Nazwa serwera hello typu. Można użyć hello [portalu Azure] [ Azure portal] toofind to.
3. Nazwa bazy danych: Nazwa typu hello bazy danych na serwerze hello właśnie zostało określone.
4. Nazwa konta użytkownika serwera: nazwa użytkownika hello typu konta, które ma uprawnienia do zapisu dla hello bazy danych.
5. Hasło konta użytkownika serwera: Podaj hasło hello hello określone konto użytkownika.
6. Zaakceptuj wszystkie certyfikatu serwera (niebezpieczne): Wybierz tę opcję, jeśli nie chcesz tooview hello certyfikatu.
7. Rozdzielana przecinkami lista kolumn toobe zapisane: Podaj listę hello zestawu danych lub wynik kolumn, które mają toooutput.
8. Nazwa tabeli danych: Określ nazwę hello hello danych tabeli.
9. Rozdzielana przecinkami lista kolumn elementu datatable: Określ toouse nazwy kolumny hello hello nowej tabeli. Witaj nazwy kolumny może różnić się od hello widocznych w zestawie hello źródła danych, ale musi zawierać taką samą liczbę kolumn w tym miejscu zdefiniowane dla tabeli wyjściowej hello hello.
10. Liczba wierszy, zapisany dla operacji SQL Azure: można skonfigurować hello liczby wierszy, które są zapisywane tooa bazy danych SQL w ramach jednej operacji.

![][writer_properties]

### <a name="step-3"></a>Krok 3
1. Uruchom eksperyment hello klikając przycisk Uruchom obszarze kanwy eksperymentu hello.
2. Po zakończeniu eksperymentu hello wszystkie moduły będą mieć tooindicate zielony znacznik wyboru, które zostały ukończone pomyślnie.

## <a name="next-steps"></a>Następne kroki
Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
