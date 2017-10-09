---
title: "aaaHow rozproszonych danych działa w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dane są przesyłane Massively Parallel przetwarzania (MPP) i hello opcje dystrybucji tabel w usłudze Azure SQL Data Warehouse i Parallel Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Rozproszone danych i tabele rozproszone na ogromną skalę równoległego przetwarzania (MPP)
Dowiedz się, jak dane użytkownika są przesyłane w Azure SQL Data Warehouse i Parallel Data Warehouse, które są systemy Massively Parallel przetwarzania (MPP) firmy Microsoft. Projektowanie sieci toouse magazynu danych danych rozproszonych skutecznie pomaga możesz tooachieve hello przetwarzania zapytań zalet hello architektura MPP. Kilka decyzji projektowych bazy danych może mieć znaczący wpływ na poprawę wydajności zapytań.  

> [!NOTE]
> Usługa Azure SQL Data Warehouse i Parallel Data Warehouse hello Użyj tego samego masowego przetwarzania równoległego (MPP) projektu, ale mają kilka różnic ze względu na powitania podstawowej platformy. Usługa SQL Data Warehouse to platforma jako usługa (PaaS), która działa na platformie Azure. Parallel Data Warehouse jest uruchamiane na Analytics Platform System (punktach dostępu) czyli lokalnego urządzenia z systemem Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>Co to jest rozproszonej danych?
Magazyn danych SQL i Parallel Data Warehouse danych rozproszonych odwołuje się toouser dane, które są przechowywane w wielu lokalizacjach w hello MPP systemu. Każdą z tych lokalizacji działa jako niezależnie od magazynu i jednostki przetwarzania, która obsługuje kwerendy w jego części hello danych. Dane rozproszone są podstawowych toorunning zapytania w równoległych tooachieve wysoką wydajność zapytań.

danych toodistribute hurtowni danych hello przypisuje każdego wiersza w lokalizacji tooone rozproszonych tabeli użytkownika.  Można rozpowszechniać tabel z metody dystrybucji mieszania lub metody okrężnego. Metoda dystrybucji Hello jest określona w instrukcji CREATE TABLE hello. 

## <a name="hash-distributed-tables"></a>Tabele rozproszonych wyznaczania wartości skrótu
powitania po diagram ilustruje, jak Pełna (z systemem innym niż rozproszonych tabeli) pobiera przechowywane jako tabelę rozpowszechniane skrót. Funkcja deterministyczne przypisuje dystrybucji tooone toobelong każdego wiersza. W definicji tabeli hello jednej z kolumn hello jest wyznaczona jako hello dystrybucji kolumna. Funkcja wyznaczania wartości skrótu Hello używa wartości hello w tooassign kolumny dystrybucji hello dystrybucji tooa każdego wiersza.

Brak wyboru hello kolumny dystrybucji, takie jak odrębności, Pochylenie danych i hello typów kwerend w systemie hello zagadnienia związane z wydajnością.

![Tabela rozproszone](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "tabeli rozproszonych")  

* Każdy wiersz należy tooone dystrybucji.  
* Algorytm wyznaczania wartości skrótu deterministyczne przypisuje dystrybucji tooone każdego wiersza.  
* Hello liczba wierszy tabeli w dystrybucji zależy, jak to przedstawiono różne rozmiary hello tabel.

## <a name="round-robin-distributed-tables"></a>Tabele rozproszonej okrężnego
Tabela rozproszona okrężnego dystrybuuje wiersze hello przez przypisanie każdego wiersza tooa dystrybucji sekwencyjnie. Jest szybkie tooload dane do tabeli okrężnego, ale wydajność kwerend może przebiegać wolniej.  Sprzęganie tabeli okrężnego zwykle wymaga losowego grupowania hello wierszy tooenable hello zapytania tooproduce wynik dokładny czas.

## <a name="distributed-storage-locations-are-called-distributions"></a>Lokalizacje magazynu rozproszone są nazywane dystrybucji
Każda lokalizacja rozproszonej jest nazywany dystrybucji. Po uruchomieniu zapytania równolegle każdej dystrybucji wykonuje zapytanie SQL na jego część hello danych. Usługa SQL Data Warehouse używa zapytania hello toorun bazy danych SQL. Parallel Data Warehouse używa zapytania hello toorun programu SQL Server. Ten projekt architektury nieudostępnianych jednostkach jest podstawowych tooachieving skalowalnego w poziomie przetwarzania równoległego.

### <a name="can-i-view-hello-distributions"></a>Czy można wyświetlić hello dystrybucji?
Każdy dystrybucji ma identyfikator dystrybucji i jest widoczny w widokach systemu, które odnoszą się tooSQL magazynu danych i Parallel Data Warehouse. Można użyć hello dystrybucji identyfikator tootroubleshoot kwerendy wydajności i innych problemów. Lista hello widoków systemowych, zobacz hello [widoku systemu MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Różnica między dystrybucji i węzeł obliczeniowy
Dystrybucji to podstawowa jednostka hello do przechowywania danych rozproszonych i przetwarzania zapytania równoległe. Dystrybucje są zgrupowane w węzłach obliczeniowych. Każdy węzeł obliczeniowy śledzi dystrybucje jeden lub więcej.  

* Analytics Platform System używa węzły obliczeniowe jako główny składnik możliwości sprzętu hello architektury i skalowalnego w poziomie. Zawsze używa osiem dystrybucje na węźle obliczeń, jak pokazano na diagramie hello rozpowszechniane skrót tabel. Witaj liczba węzłów obliczeniowych i w związku z tym hello liczba dystrybucji, jest określany przez hello liczba węzłów obliczeniowych, zakupu hello urządzenia. Jeśli kupisz ośmiu węzłów obliczeniowych, na przykład get dystrybucje 64 (8 węzłów x 8 dystrybucje/węźle obliczeń). 
* Magazyn danych SQL ma stała liczba 60 dystrybucji i elastyczne liczba węzłów obliczeniowych. węzły obliczeniowe Hello są implementowane przy użyciu zasobów obliczeniowych i magazynu systemu Azure. zgodnie z toohello wewnętrznej bazy danych usługi Obciążenie i mocy obliczeniowej hello (jednostek dwu) określone dla magazynu danych hello, można zmienić Hello liczba węzłów obliczeniowych. Po zmianie hello liczba węzłów obliczeniowych hello liczba dystrybucji na węźle obliczeń jest również zmian. 

### <a name="can-i-view-hello-compute-nodes"></a>Czy można wyświetlić węzły obliczeniowe hello?
Każdy węzeł obliczeniowy ma identyfikator węzła i jest widoczny w widokach systemu, które odnoszą się tooSQL magazynu danych i Parallel Data Warehouse.  Widać hello węźle obliczeń, wyszukując hello node_id kolumny w widokach systemu, których nazwy zaczynają się od sys.pdw_nodes. Lista hello widoków systemowych, zobacz hello [widoku systemu MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Zreplikowane tabele
Tabela, który jest replikowany ma pełni przechowywać kopię tabeli hello w każdym węźle obliczeń. Replikowanie tabeli usuwa hello potrzeby tootransfer danych między węzłami obliczeniowymi przed join lub agregacji. Zreplikowane tabele są tylko wykonalne małe tabele z powodu hello pełne tabeli hello toostore wymagane dodatkowe miejsce do magazynowania w każdym węźle obliczeń.  

Witaj Poniższy diagram przedstawia zreplikowanej tabeli, który jest przechowywany w każdym węźle obliczeń. Dla usługi SQL Data Warehouse zreplikowanej tabeli hello jest bazy danych dystrybucji tooa całkowicie skopiowane na każdym węźle obliczeniowym. Dla Parallel Data Warehouse hello zreplikowanej tabeli są przechowywane na wszystkich dyskach przypisane toohello węźle obliczeń.  Ta strategia dysku jest implementowane za pomocą grup plików programu SQL Server.  

![Tabela zreplikowane](media/sql-data-warehouse-distributed-data/replicated-table.png "zreplikowane tabeli") 

## <a name="next-steps"></a>Następne kroki
tabele toouse rozproszonych skutecznie, zobacz [Dystrybucja tabel w usłudze SQL Data Warehouse](sql-data-warehouse-tables-distribute.md)  

