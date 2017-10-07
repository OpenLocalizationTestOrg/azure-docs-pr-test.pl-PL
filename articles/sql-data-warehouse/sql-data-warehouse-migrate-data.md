---
title: aaaMigrate tooSQL Twojej danych hurtowni danych | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące migrowania tooAzure Twojego danych usługi SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Migrowanie danych
Można przenieść dane z różnych źródeł do magazynu danych SQL przy użyciu różnych narzędzi.  Kopiuj ADF, SSIS i może bcp wszystkie można tooachieve używanych w tym celu. Jednak miarę wzrostu hello ilości danych możesz pomyśleć o podziału hello proces migracji danych do kroków. Dzięki temu hello toooptimize okazji każdego kroku zarówno wydajności i odporności tooensure migracji smooth danych.

W tym artykule omówiono najpierw scenariusze migracji prostego powitania ADF kopiowania, SSIS i bcp. Następnie wygląda bardziej szczegółowe w sposób mogą być optymalizowane hello migracji.

## <a name="azure-data-factory-adf-copy"></a>Azure kopiowania fabryki danych (ADF)
[Kopiuj ADF] [ ADF Copy] jest częścią [fabryki danych Azure][Azure Data Factory]. Można użyć tooexport ADF kopiowania plików tooflat danych znajdującej się w magazynie lokalnym plików prostych tooremote przechowywany w magazynie obiektów blob platformy Azure lub bezpośrednio do usługi SQL Data Warehouse.

Jeśli danych rozpoczyna się w płaskiej plików, a następnie należy najpierw tootransfer go tooAzure obiektu blob magazynu przed zainicjowaniem obciążenia go do usługi SQL Data Warehouse. Po hello dane są przesyłane do magazynu obiektów blob platformy Azure można wybrać toouse [kopiowania ADF] [ ADF Copy] ponownie toopush hello danych do usługi SQL Data Warehouse.

Aparat PolyBase zapewnia również opcję wysokiej wydajności dla ładowania danych hello. Która jednak oznaczają za pomocą dwóch narzędzi, zamiast jednego. Jeśli konieczne hello najlepszą wydajność, użyj programu PolyBase. Jeśli w środowisku jednego narzędzia (co hello danych nie jest bardzo dużej) ADF jest odpowiedź.


> 
> 

HEAD za pośrednictwem toohello poniższego artykułu dla niektórych Wielkiej [przykłady ADF][ADF samples].

## <a name="integration-services"></a>Usługi integracji
Integration Services (SSIS) to wydajny i elastyczny wyodrębniania, przekształcania i ładowania (ETL) Narzędzie obsługującego złożone przepływy pracy, przekształcania danych i kilka opcji ładowania danych. Użyj SSIS toosimply transferu danych tooAzure lub w ramach szerszych migracji.

> [!NOTE]
> SSIS można wyeksportować tooUTF-8 bez hello znacznika kolejności bajtów w pliku hello. tooconfigure, to należy najpierw użyć hello utworzona kolumna danych znakowych hello tooconvert składnika w hello danych przepływu toouse hello 65001 UTF-8 stronę kodową. Po konwersji kolumny hello zapisu hello danych toohello pliku prostego docelowej karty sprawdzeniu, czy 65001 została również wybrana jako strona kodowa hello hello pliku.
> 
> 

SSIS łączy tooSQL hurtowni danych, tak samo, jak może zostać nawiązane tooa wdrożenie programu SQL Server. Jednak połączenia należy toobe za pomocą Menedżera połączenia ADO.NET. Również należy zadbać hello tooconfigure "Jeśli jest dostępna, użyj zostanie wstawiania zbiorczego" ustawienie toomaximize przepływności. Zobacz toohello [ADO.NET docelowy adapter] [ ADO.NET destination adapter] toolearn artykułu więcej informacji na temat tej właściwości

> [!NOTE]
> Łączenie tooAzure SQL Data Warehouse przy użyciu OLEDB nie jest obsługiwane.
> 
> 

Ponadto istnieje możliwość hello pakietu może zakończyć się niepowodzeniem ze względu na problemy z toothrottling lub sieci. Projekt pakietów, ich można wznawiać na powitania punktu awarii, bez ponawianie pracy, który zakończył się przed awarią hello.

Aby uzyskać więcej informacji, zapoznaj się hello [dokumentacji SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
Narzędzie bcp jest narzędziem wiersza polecenia, które jest przeznaczone do pliku prostego importowania i eksportowania danych. Niektóre przekształcania może odbywać się podczas eksportowania danych. przekształcenia proste tooperform Użyj tooselect zapytania i przekształcania danych hello. Po wyeksportowane, plików prostych hello, następnie mogą być ładowane bezpośrednio do hello docelowej hello magazyn danych SQL z bazy danych.

> [!NOTE]
> Często jest dobrym rozwiązaniem hello tooencapsulate, transformacje używane podczas danych eksportu w widoku w systemie źródłowym hello. Dzięki temu logika hello jest zachowywana, a proces hello jest powtarzalne.
> 
> 

Zalety programu bcp są następujące:

* Prostota. polecenia BCP są proste toobuild i wykonania
* Proces ładowania jej ponownie uruchomić. Raz wyeksportowanego hello obciążenia mogą być wykonywane dowolną liczbę razy

Ograniczenia programu bcp są:

* Narzędzie bcp działa tylko tabelaryczne plików prostych. Nie działa z plikami, takie jak xml lub JSON
* Funkcje przekształcania danych są ograniczone toohello eksportu tylko przemieszczanie i proste charakteru
* BCP nie został dostosowany toobe niezawodne, podczas ładowania danych za pośrednictwem hello internet. Niestabilności sieci może spowodować błąd ładowania.
* Narzędzie bcp zależy od schematu hello są obecne w hello docelowej bazy danych poprzednich toohello obciążenia

Aby uzyskać więcej informacji, zobacz [Użyj narzędzia bcp tooload danych do usługi SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Optymalizacja migracji danych
Proces migracji danych SQLDW mogą skutecznie podzielone na trzy osobne kroki:

1. Eksport źródła danych
2. Transfer danych tooAzure
3. Ładowanie do hello docelowej SQLDW bazy danych

Każdy krok można osobno zoptymalizowane toocreate proces migracji niezawodny, będzie można ponownie uruchomić systemu i elastyczne, które pozwala zmaksymalizować wydajność w każdym kroku.

## <a name="optimizing-data-load"></a>Optymalizacja ładowania danych
Spojrzenie na ich w kolejności odwrotnej do chwili; Witaj najszybszy sposób tooload danych odbywa się za pośrednictwem programu PolyBase. Optymalizacja dla proces ładowania PolyBase umieszcza wymagania wstępne w poprzednich krokach, jest najlepszym toounderstand, to hello góry. Są to:

1. Kodowanie plików danych
2. Format plików danych
3. Lokalizacja plików danych

### <a name="encoding"></a>Encoding
Program PolyBase wymaga toobe pliki danych UTF-8 lub UTF-16FE. 



### <a name="format-of-data-files"></a>Format plików danych
Program PolyBase ma terminatora stałym wiersza \n lub nowym wierszem. Pliki danych muszą być zgodne toothis standard. Nie ma ograniczeń terminatory parametry lub kolumny.

Konieczne będzie toodefine każdej kolumny w pliku hello jako część tabeli zewnętrznej w PolyBase. Upewnij się, że wymagane są wszystkie kolumny wyeksportowany i typy hello zgodność standardów toohello wymagane.

Można ponownie znaleźć toohello [migracji schemat] artykułu dla szczegółów na obsługiwane typy danych.

### <a name="location-of-data-files"></a>Lokalizacja plików danych
Usługa SQL Data Warehouse używany wyłącznie danych tooload PolyBase z magazynu obiektów Blob Azure. W rezultacie dane hello musi najpierw przeniesiono do magazynu obiektów blob.

## <a name="optimizing-data-transfer"></a>Optymalizacja transferu danych
Jeden z elementów najwolniejsze hello migracji danych jest hello transferu hello tooAzure danych. Nie tylko przepustowość sieci może być problemem, ale również niezawodność sieci może poważnie utrudniać postępu. Domyślnie migracja tooAzure danych znajduje się nad hello internet tak hello prawdopodobieństwo wystąpienia, prawdopodobnie rozsądnych błędów transferu. Jednak te błędy mogą wymagać toobe dane wysyłane ponownie w całości lub częściowo.

Na szczęście masz kilka opcji tooimprove hello szybkość i odporności tego procesu:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Może być za pomocą tooconsider [ExpressRoute] [ ExpressRoute] toospeed się hello transferu. [ExpressRoute] [ ExpressRoute] zapewnia o tooAzure ustanowionym połączeniu prywatnej tak hello połączenia nie został przekroczony hello publicznej sieci internet. W żadnym wypadku nie jest to krok obowiązkowe. Jednak go może zwiększyć przepustowość podczas wypychania danych tooAzure z lokalnymi lub wspólnej lokalizacji.

Witaj korzyści wynikające ze stosowania [ExpressRoute] [ ExpressRoute] są:

1. Zwiększenie niezawodności
2. Szybsze sieci
3. Mniejsze opóźnienia sieci
4. wyższy poziom zabezpieczeń sieci

[ExpressRoute] [ ExpressRoute] jest przydatne w przypadku różnych scenariuszach; hello nie tylko migracji.

Chcesz spróbować? Więcej informacji oraz sprawdź ceny odwiedź hello [dokumentacja usługi ExpressRoute][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Azure importu i eksportu usługi
Hello Azure importowania i eksportowania usługa jest z procesu transferu danych, przeznaczony dla dużych (GB ++) toomassive (TB ++) transferów danych na platformie Azure. Obejmuje ona zapisywanie toodisks Twojego danych i wysyłania ich tooan centrum danych Azure. zawartość dysku Hello zostaną następnie załadowane na obiektach blob magazynu Azure w Twoim imieniu.

Ogólny widok procesu eksportu importowania hello jest następujący:

1. Konfigurowanie usługi Azure Blob Storage kontenera tooreceive hello danych
2. Eksportuj toolocal magazynu danych
3. Skopiuj hello danych too3.5 CAL SATA II/III dysków twardych za pomocą hello [narzędzie importu/eksportu Azure]
4. Utwórz zadanie importu za pomocą hello Azure importu i eksportu usługi, zapewniając hello pliki dziennika utworzone przez hello [narzędzie importu/eksportu Azure]
5. Wyślij centrum danych Azure nominalnym hello dysków
6. Twoje dane są przekazanych tooyour kontenera magazynu obiektów Blob Azure
7. Ładowanie danych hello do SQLDW przy użyciu programu PolyBase

### <a name="azcopyazcopy-utility"></a>[Narzędzie AZCopy][Narzędzie AZCopy] narzędzia
Witaj [Narzędzie AZCopy][Narzędzie AZCopy] narzędzie to doskonałe narzędzie do pobierania danych przesyłanych w obiektach blob magazynu Azure. Jest on przeznaczony dla małych (MB ++) toovery duże (GB ++) transferów danych. [Narzędzie AZCopy] również została zaprojektowana tooprovide dobrej przepływności odporne podczas przesyłania danych tooAzure i dlatego jest doskonałym wyborem kroku przeniesienie danych hello. Raz przeniesione, można załadować danych hello przy użyciu programu PolyBase do usługi SQL Data Warehouse. Narzędzia AZCopy można również zastosować w pakietów SSIS za pomocą zadania "Wykonania procesu".

toouse AZCopy, najpierw należy toodownload a go zainstalować. Brak [wersji produkcyjnej] [ production version] i [wersji zapoznawczej] [ preview version] dostępne.

tooupload pliku z systemu plików, które mają być polecenia takie jak hello jedną poniżej:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Podsumowanie procesu może być:

1. Konfigurowanie magazynu Azure blob kontenera tooreceive hello danych
2. Eksportuj toolocal magazynu danych
3. Dane w kontenerze magazynu obiektów Blob Azure hello AZCopy
4. Ładowanie danych hello do usługi SQL Data Warehouse przy użyciu programu PolyBase

Pełna dokumentacja: [Narzędzie AZCopy][Narzędzie AZCopy].

## <a name="optimizing-data-export"></a>Optymalizowanie eksportowanie danych
Ponadto tooensuring czy eksportu hello spełnia wymogi toohello określone przez aparat PolyBase można również można wyszukiwać eksportu hello toooptimize hello danych tooimprove hello procesu dalsze.



### <a name="data-compression"></a>Kompresja danych
Program PolyBase mogą odczytywać dane skompresowane gzip. Jeśli jesteś stanie toocompress pliki toogzip danych, a następnie użytkownik zostanie zminimalizowane hello ilość danych przekazywanej hello sieci.

### <a name="multiple-files"></a>Wiele plików
Podzielenie dużych tabel do wielu plików nie tylko pomaga tooimprove wyeksportować szybkości, ale także z transfer re-startability i hello ogólne możliwości zarządzania danych hello raz w magazynie obiektów blob Azure hello. Jeden z hello jest wiele funkcji nieuprzywilejowany PolyBase czy odczytuje wszystkie pliki hello znajduje się w folderze i traktować go jako jedna tabela. Dlatego jest dobrym rozwiązaniem tooisolate hello plików dla każdej tabeli do własnego folderu.

Aparat PolyBase obsługuje również funkcją znana jako "Przechodzenie folderu cykliczne". Tej funkcji można używać toofurther zwiększenia hello organizacji tooimprove Twojego wyeksportowanych danych z danych zarządzania.

toolearn więcej informacji na temat ładowanie danych przy użyciu programu PolyBase, zobacz [Użyj programu PolyBase tooload danych do usługi SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat migracji, zobacz [migracji tooSQL Twojego rozwiązania magazynu danych][Migrate your solution tooSQL Data Warehouse].
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[Narzędzie AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
