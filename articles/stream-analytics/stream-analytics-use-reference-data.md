---
title: "aaaUse tabele danych i wyszukiwania odwołań w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Użycie danych referencyjnych w kwerendzie analiza strumienia"
keywords: "Tabela odnośnika, dane referencyjne"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Przy użyciu tabel danych lub wyszukiwanie odwołań w Stream Analytics strumienia wejściowego
Dane referencyjne (znanej także jako tabela odnośnika) jest ograniczone zestawu danych, który jest statyczny lub spowalniając zmianę charakteru, użyty tooperform wyszukiwania lub toocorrelate ze strumienia danych. Użycie toomake danych referencyjnych w zadania usługi analiza strumienia Azure będą zwykle używać [dołączenia danych odwołania](https://msdn.microsoft.com/library/azure/dn949258.aspx) w zapytaniu. Stream Analytics korzysta z magazynu obiektów Blob platformy Azure jako hello warstwy magazynu danych referencyjnych i z odwołaniem do fabryki danych Azure dane mogą być tooAzure przekształcone i/lub skopiowane magazynu obiektów Blob, do użycia jako dane referencyjne z [dowolną liczbę oparte na chmurze i magazyny danych lokalnymi](../data-factory/data-factory-data-movement-activities.md). Sekwencja obiektów blob (zdefiniowany w konfiguracji wejściowych hello) rosnąco hello Data/Godzina podana w nazwie obiektu blob hello ma formę danych referencyjnych. On **tylko** obsługuje dodawanie toohello koniec sekwencji hello przy użyciu daty/godziny **większa** niż określona w hello ostatniego obiektów blob w sekwencji hello hello.

Analiza strumienia ma **limit 100 MB dla obiekt blob** , ale zadania można przetwarzać wielu obiektów blob odwołania przy użyciu hello **wzorzec ścieżki** właściwości.


## <a name="configuring-reference-data"></a>Konfigurowanie danych referencyjnych
tooconfigure danych odwołania, należy najpierw toocreate danych wejściowych typu **danych referencyjnych**. Witaj w poniższej tabeli opisano każdej właściwości, że konieczne będzie tooprovide podczas tworzenia wejściowych danych referencyjnych hello z jego opisem:


<table>
<tbody>
<tr>
<td>Nazwa właściwości</td>
<td>Opis</td>
</tr>
<tr>
<td>Alias wejściowy</td>
<td>Przyjazna nazwa, który będzie używany w tooreference zapytania zadania hello wejściowego.</td>
</tr>
<tr>
<td>Konto magazynu</td>
<td>Nazwa Hello hello konta magazynu, gdzie znajdują się obiektów blob. Jeśli jest on hello tej samej subskrypcji co Twoje zadania usługi analiza strumienia, możesz wybrać je z listy rozwijanej hello.</td>
</tr>
<tr>
<td>Klucz konta magazynu</td>
<td>klucz tajny Hello skojarzone z kontem magazynu hello. Pobiera to wypełnione automatycznie, jeśli konto magazynu hello hello tej samej subskrypcji co zadania usługi analiza strumienia.</td>
</tr>
<tr>
<td>Kontener magazynu</td>
<td>Kontenery umożliwiają logiczne grupowanie dla obiektów blob przechowywanych w hello usługi obiektów Blob Microsoft Azure. Podczas przekazywania toohello obiektu blob usługi obiektów Blob, należy określić kontener dla tego obiektu blob.</td>
</tr>
<tr>
<td>Wzorzec ścieżki</td>
<td>użyta ścieżka Hello toolocate obiektów blob w określonym kontenerze hello. W ścieżce hello można wybrać jeden lub więcej wystąpień hello następujące zmienne 2 toospecify:<BR>{date} {time}<BR>Przykład 1: products/{date}/{time}/product-list.csv<BR>Przykład 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Format daty [opcjonalnie]</td>
<td>{Date} użycie w hello wzorzec ścieżki, określony format daty hello, w którym są zorganizowane obiektów blob można wybrać z rozwijanej hello obsługiwanych formatów.<BR>Przykład: RRRR/MM/DD/MM/DD/RRRR, itp.</td>
</tr>
<tr>
<td>Format czasu [opcjonalnie]</td>
<td>{Time} użycie w hello wzorzec ścieżki, określonej można wybrać format czasu hello, w którym są zorganizowane obiektów blob z rozwijanej hello obsługiwanych formatów.<BR>Przykład: HH gg/mm lub HH mm</td>
</tr>
<tr>
<td>Format serializacji zdarzeń</td>
<td>Czy na pewno zapytania mogły działać hello oczekiwaniami, Stream Analytics toomake musi tooknow format serializacji używany w przypadku przychodzących strumieni danych. Dla danych referencyjnych hello obsługiwane formaty to CSV i JSON.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Generowanie danych referencyjnych zgodnie z harmonogramem
Jeśli dane odwołanie jest wolno zmieniającego zestawu danych, określając wzorzec ścieżki w konfiguracji wejściowych hello przy użyciu hello {date} i {time} tokenów podstawienia jest włączona obsługa odświeżania danych referencyjnych. Analiza strumienia przejmuje definicji danych odwołania hello zaktualizowane opartych na ten wzorzec ścieżki. Na przykład wzorzec `sample/{date}/{time}/products.csv` z datą o postaci **"RRRR-MM-DD"** i format czasu **"HH mm"** nakazuje toopick Stream Analytics się obiektów blob hello zaktualizowane `sample/2015-04-16/17-30/products.csv` na 5:30 będzie kwietnia 16, strefę czasową UTC 2015.

> [!NOTE]
> Obecnie zadania usługi analiza strumienia poszukaj hello blob odświeżania tylko wtedy, gdy czas komputera hello przesuwa czasu toohello zakodowane w hello nazwa obiektu blob. Na przykład zadanie hello będzie szukać `sample/2015-04-16/17-30/products.csv` jak to możliwe, ale nie wcześniej niż 5:30 będzie 16 kwietnia 2015 UTC czasu strefy. Będzie on *nigdy nie* wyszukiwania dla obiektu blob z wcześniejszych niż hello ostatnią odnalezionej zakodowanego czasu.
> 
> Na przykład Po hello zostanie znaleziony hello blob `sample/2015-04-16/17-30/products.csv` będzie ignorował wszystkie pliki z datą zakodowanego starszych niż 5:30 będzie 16 kwietnia 2015 r. tak więc jeśli późne odbieranych `sample/2015-04-16/17-25/products.csv` obiektu blob jest tworzony w hello same zadania hello kontenera nie będzie używać.
> 
> Podobnie jeśli `sample/2015-04-16/17-30/products.csv` dostarczać tylko godzinie 10:03 16 kwietnia 2015 r., ale nie obiektów blob z wcześniejszą datę znajduje się w kontenerze hello, hello zadania będą używać tego pliku, zaczynając od 10:03 PM 16 kwietnia 2015 i użyj hello poprzednie dane odwołanie do tego czasu.
> 
> Toothis wyjątku jest zadanie hello wymaga toore przetwarzania danych w czasie lub po pierwszym uruchomieniu zadanie hello. Podczas uruchamiania zadania hello czasu szuka hello blob najnowszych utworzonej przed zadania hello określono godzinę rozpoczęcia. Jest to realizowane tooensure, że ma **niepustym** odwołania zestawu danych podczas uruchamiania zadania hello. Jeśli nie można odnaleźć jednego, zadanie hello Wyświetla powitania po diagnostycznych: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Fabryka danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) mogą być używane tooorchestrate hello zadanie tworzenia hello zaktualizowane obiekty BLOB wymagany przez definicje danych odwołania tooupdate Stream Analytics. Fabryka danych jest usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych. Fabryka danych obsługuje [łączenie tooa dużą liczbę oparte na chmurze i lokalnych magazynów danych](../data-factory/data-factory-data-movement-activities.md) i łatwe przenoszenie danych zgodnie z ustalonym harmonogramem, który określisz. Aby uzyskać więcej informacji oraz wskazówki krok po kroku dotyczące jak tooset się fabryki danych w potoku danych referencyjnych toogenerate dla usługi analiza strumienia, który odświeża na wstępnie zdefiniowany harmonogram, zapoznaj się z tym [próbki GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Porady dotyczące odświeżania danych odwołania
1. Zastępowanie obiektów blob danych odwołania nie spowoduje, że obiekt blob hello tooreload Stream Analytics, a w niektórych przypadkach może spowodować hello toofail zadania. dane referencyjne toochange sposób jest tooadd nowego obiektu blob przy użyciu tego samego wzorca kontenera i ścieżki zdefiniowane w danych wejściowych zadania hello hello i używanie daty/godziny, zalecane Hello **większa** niż określona w hello ostatniego obiektów blob w sekwencji hello hello.
2. Obiekty BLOB danych odwołania są **nie** określona przez czas "Ostatniej modyfikacji" hello blob, ale tylko przez hello godzina i data podana w nazwie obiektu blob hello przy użyciu hello {date} i {time} podstawienia.
3. W kilku przypadkach zadania musi wrócić do poprzedniej strony w czasie, w związku z tym obiekty BLOB danych odwołania może nie być zmieniane ani usuwane w.

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
Już zostały wprowadzone tooStream Analytics — zarządzaną usługę służącą do analizy danych z Internetu rzeczy hello przesyłanych strumieniowo. toolearn więcej informacji na temat tej usługi, zobacz:

* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
