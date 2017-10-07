---
title: "aaaManage obliczeniowe zasilania w usłudze Azure SQL Data Warehouse (omówienie) | Dokumentacja firmy Microsoft"
description: "Wydajność skalowania możliwości w usłudze Azure SQL Data Warehouse. Skalowanie w poziomie przez dostosowanie wartości dwu lub wstrzymywać i wznawiać koszty toosave zasobów obliczeniowych."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (omówienie)
> [!div class="op_single_selector"]
> * [Omówienie](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

Architektura Hello usługi SQL Data Warehouse oddziela magazynu i zasobów obliczeniowych, dzięki czemu każdy tooscale niezależnie. W związku z tym obliczeń może być skalowana toomeet wymagań dotyczących wydajności niezależne od hello ilości danych. Fizyczne konsekwencją tej architektury jest to, że [rozliczeń] [ billed] dla zasobów obliczeniowych i magazynu jest oddzielona. 

Ten przegląd zawiera opis sposobu skalowania współpracuje z magazynu danych SQL i jak tooutilize Witaj, wstrzymywanie, wznawianie i możliwości skalowania usługi SQL Data Warehouse. Zapoznaj się hello [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] toolearn strony jak jednostek dwu i wydajności są powiązane. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Jak obliczeń operacje zarządzania działają w usłudze SQL Data Warehouse
Architektura Hello magazynu danych SQL składa się z węzłem sterowania, węzły obliczeniowe i hello rozmieszczenie 60 dystrybucje warstwy magazynu. 

Podczas normalnej sesji aktywnych w usłudze SQL Data Warehouse węzła głównego systemu zarządza hello metadanych i zawiera Optymalizator zapytań rozproszonych hello. Poniżej tego węzła głównego są węzłów obliczeniowych i warstwą magazynu. 400 DWU system ma jednego węzła głównego, czterech węzłów obliczeniowych i hello magazynu, składającego się z 60 dystrybucji. 

Przejście skali lub wstrzymać działania systemu hello najpierw Kasuje wszystkie zapytania przychodzące i wycofa następnie tooensure transakcji spójne. Dla operacji skalowania skalowanie będzie miało miejsce tylko po zakończeniu tego transakcyjne wycofywania. Dla operacji skalowania w górę przepisy systemu hello hello bardzo odpowiednią liczbę węzłów obliczeniowych, a następnie rozpoczyna podłączenie warstwy magazynu toohello węzły obliczeniowe hello. Dla operacji dół hello niepotrzebnych węzły są wydawane, a pozostałe węzły obliczeniowe hello Przyłącz się ponownie toohello odpowiedniej liczby dystrybucji. Dla operacji Wstrzymaj obliczeniowe wszystkie węzły są wydawane i systemu zostaną poddane różnych tooleave operacji metadanych systemu końcowego stabilna.

| DWU  | \#węzły obliczeniowe | \#dystrybucji na węzeł |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

Witaj trzy podstawowe funkcje zarządzania obliczeniowe są:

1. Wstrzymaj
2. Resume
3. Skalowanie

Każda z tych operacji może potrwać kilka minut toocomplete. Jeśli jesteś skalowanie/wstrzymywanie/wznawianie automatycznie, może być tooimplement tooensure logiki to pewność, że operacje zostały zakończone przed kontynuowaniem innej akcji. 

Sprawdzanie stanu bazy danych hello za pośrednictwem różnych punktów końcowych pozwoli toocorrectly automatyzacji implementacji takich operacji. Hello portal zapewni powiadomienie po zakończeniu operacji i hello bazy danych bieżący stan, ale nie jest możliwe programowe sprawdzania stanu. 

>  [!NOTE]
>
>  Funkcja zarządzania nie istnieje we wszystkich punktów końcowych obliczeń.
>
>  

|              | Wstrzymanie/wznowienie | Skalowanie | Sprawdź stan bazy danych |
| ------------ | ------------ | ----- | -------------------- |
| Azure Portal | Tak          | Tak   | **Nie**               |
| PowerShell   | Tak          | Tak   | Tak                  |
| Interfejs API REST     | Tak          | Tak   | Tak                  |
| T-SQL        | **Nie**       | Tak   | Tak                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Skalowanie możliwości obliczeniowych

Wydajność w usłudze SQL Data Warehouse jest mierzony w [jednostki (jednostek dwu) magazynu danych] [ data warehouse units (DWUs)] czyli abstracted miary zasoby obliczeniowe, takie jak procesor CPU, pamięci i we/wy przepustowości. Użytkownik, który chce tooscale wydajność ich systemu to zrobić za pośrednictwem różnych środków, takich jak za pośrednictwem portalu hello, T-SQL i interfejsów API REST. 

### <a name="how-do-i-scale-compute"></a>Jak skalować obliczeń?
Moc obliczeniową odbywa się SQL Data Warehouse, zmieniając ustawienie wartości DWU hello. Zwiększa wydajność [liniowo] [ linearly] jak dodać więcej DWU dla niektórych operacji.  Firma Microsoft oferuje ofert DWU, zapewniający, że gdy system skalować w górę lub w dół znacznie zmienić wydajność. 

tooadjust jednostek dwu służy jednej z tych poszczególnych metod.

* [Skala obliczeniowe zasilania z portalu Azure][Scale compute power with Azure portal]
* [Skala obliczeniowe zasilania przy użyciu programu PowerShell][Scale compute power with PowerShell]
* [Moc obliczeniową skali z interfejsów API REST][Scale compute power with REST APIs]
* [Skala obliczeniowe zasilania przy użyciu języka TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Liczbę jednostek dwu należy używać?

toounderstand jest jakie idealna wartość DWU, spróbuj skalowanie w górę i w dół oraz Uruchom kilka zapytań po załadowaniu danych. Ponieważ skalowanie odbywa się szybko, możesz wypróbować różne poziomy wydajności w ciągu godziny lub mniej. 

> [!Note] 
> Magazyn danych SQL jest zaprojektowana tooprocess dużych ilości danych. toosee true możliwości skalowania, zwłaszcza na większą liczbę jednostek dwu, ma toouse dużych zestawów danych, które zbliża się lub przekracza 1 TB.

Zalecenia dotyczące znajdowania hello DWU najlepsze dla obciążenia:

1. Dla magazynu danych na programowanie rozpocząć wybierając mniejszą wydajnością DWU.  Dobry punkt wyjścia jest DW400 lub DW200.
2. Monitorowanie wydajności aplikacji, obserwowania hello liczby jednostek dwu wybrany porównanych toohello wydajności, które należy obserwować.
3. Określ, ile szybciej lub wolniej wydajności powinny mieć możesz tooreach hello optymalny poziom wydajności dla wymagań przejmując skali liniowej.
4. Zwiększ lub Zmniejsz liczbę hello jednostek dwu w proporcji toohow znacznie szybciej lub wolniej ma tooperform Twojego obciążenia. 
5. Kontynuuj, wprowadzić zmiany, aż do uzyskania optymalnej wydajności poziom dla potrzeb biznesowych.

> [!NOTE]
>
> Wydajność zapytań tylko zwiększa się wraz z paralelizacja więcej jeśli hello pracy może zostać podzielony między węzły obliczeń. Jeśli okaże się, że skalowanie nie zmienia się na wydajność, można znaleźć na naszych dostrajanie toocheck artykuły, czy dane jest nierównomiernie dystrybuowane lub jeśli udostępniono dużą ilość ruchu danych wydajności. 

### <a name="when-should-i-scale-dwus"></a>Kiedy skalować liczbę jednostek dwu?
Skalowanie jednostek dwu zmienia powitania po ważne scenariusze:

1. Liniowo Zmiana wydajności systemu hello skanowania, agregacji i CTAS — instrukcje
2. Zwiększenie liczby hello czytelników i zapisywania podczas ładowania przy użyciu programu PolyBase
3. Maksymalna liczba równoczesnych zapytań i gniazda współbieżności

Zalecenia dotyczące kiedy tooscale jednostek dwu:

1. Przed wykonaniem operacji ładowania i przekształcania dużej ilości danych, skalowanie w górę liczbę jednostek dwu tak, aby szybciej Twoje dane są dostępne.
2. W godzinach szczytu skalowanie tooaccommodate większej liczby równoczesnych zapytań. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Wstrzymaj obliczeń
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause bazy danych, użyj jednej z tych poszczególnych metod.

* [Wstrzymaj obliczeń z portalu Azure][Pause compute with Azure portal]
* [Wstrzymaj obliczeń przy użyciu programu PowerShell][Pause compute with PowerShell]
* [Wstrzymaj obliczeń z interfejsów API REST][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Wznów obliczeń
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume bazy danych, użyj jednej z tych poszczególnych metod.

* [Wznów obliczeń z portalu Azure][Resume compute with Azure portal]
* [Wznów obliczeń przy użyciu programu PowerShell][Resume compute with PowerShell]
* [Wznów obliczeń z interfejsów API REST][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Sprawdź stan bazy danych 

tooresume bazy danych, użyj jednej z tych poszczególnych metod.

- [Sprawdź stan bazy danych z T-SQL][Check database state with T-SQL]
- [Sprawdź stan bazy danych przy użyciu programu PowerShell][Check database state with PowerShell]
- [Sprawdź stan bazy danych z interfejsów API REST][Check database state with REST APIs]

## <a name="permissions"></a>Uprawnienia

Skalowania hello bazy danych wymaga uprawnień hello opisanego w [ALTER DATABASE][ALTER DATABASE].  Wstrzymywanie i wznawianie wymagają hello [Współautor bazy danych SQL] [ SQL DB Contributor] uprawnienia, w szczególności Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Następne kroki
Zapoznaj się następujące artykuły toohelp pojęciami niektóre dodatkowe wydajności toohello:

* [Zarządzanie obciążenia i współbieżność][Workload and concurrency management]
* [Omówienie projektowania tabeli][Table design overview]
* [Dystrybucja tabeli][Table distribution]
* [Indeksowanie tabeli][Table indexing]
* [Partycjonowanie tabel][Table partitioning]
* [Statystyk tabeli][Table statistics]
* [Najlepsze praktyki][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
