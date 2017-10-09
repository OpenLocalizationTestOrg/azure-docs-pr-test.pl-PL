---
title: Biblioteka klienta elastycznej bazy danych aaaUsing Dapper | Dokumentacja firmy Microsoft
description: "Za pomocą biblioteki klienta elastycznej bazy danych z Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Korzystanie z biblioteki klienta elastycznej bazy danych z Dapper
Ten dokument jest przeznaczony dla deweloperów, które zależą od Dapper toobuild aplikacji, ale również mają tooembrace [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md) toocreate aplikacji, które implementuje wychodzący tooscale dzielenia na fragmenty ich warstwy danych.  Ten dokument przedstawia hello zmian w aplikacjach opartych na Dapper, które są niezbędne toointegrate z narzędzi elastycznej bazy danych. Skupiliśmy się na tworzenie hello elastycznej bazy danych niezależnych zarządzania i zależne od danych routingu z Dapper. 

**Przykładowy kod**: [narzędzi elastycznej bazy danych dla usługi Azure SQL Database — integracja Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Integrowanie **Dapper** i **DapperExtensions** z hello jest łatwe biblioteki klienta elastycznej bazy danych dla bazy danych SQL Azure. Aplikacje można użyć danych zależnych routingu przez zmianę hello tworzenia i otwierania nowych [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello toouse obiektów [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) wywoływać z hello [klienta Biblioteka](http://msdn.microsoft.com/library/azure/dn765902.aspx). Ogranicza to zmiany w Twojej aplikacji tooonly, gdzie utworzony i otworzyć nowe połączenia. 

## <a name="dapper-overview"></a>Dapper — omówienie
**Dapper** jest mapowania obiektów relacyjnych. Mapuje obiekty .NET z Twojej aplikacji tooa relacyjnej bazy danych (i na odwrót). Hello pierwsza część hello przykładowy kod przedstawia sposób integrowania biblioteki klienta elastycznej bazy danych hello z aplikacji opartych na Dapper. Witaj drugiej części hello przykładowy kod przedstawia sposób toointegrate podczas używania zarówno Dapper i DapperExtensions.  

funkcje mapowania Hello w Dapper udostępnia metody rozszerzenia na połączenia z bazą danych, które upraszczają przesyłanie instrukcje T-SQL do wykonania lub podczas badania hello bazy danych. Na przykład Dapper umożliwia łatwe toomap między obiekty .NET i hello parametry instrukcji SQL dla **Execute** wywołania lub tooconsume hello wyników zapytań SQL na obiekty .NET przy użyciu **zapytania**wywołania z Dapper. 

Korzystając z DapperExtensions, nie są już potrzebne instrukcje SQL hello tooprovide. Metody rozszerzenia, takie jak **GetList** lub **Wstaw** za pośrednictwem połączenia z bazą danych hello utworzyć hello tle hello instrukcje SQL.

Kolejną zaletą Dapper, a także DapperExtensions jest, że formanty aplikacji hello hello tworzenia hello połączenia z bazą danych. Dzięki temu interakcyjnie hello biblioteki klienta elastycznej bazy danych, która brokerzy przez połączenia na podstawie mapowania hello z shardlets toodatabases bazy danych.

Zobacz tooget hello Dapper zestawy [Dapper kropka net](http://www.nuget.org/packages/Dapper/). Witaj Dapper rozszerzeń, zobacz [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Krótki przegląd biblioteki klienta elastycznej bazy danych hello
Z biblioteki klienta elastycznej bazy danych hello, zdefiniuj partycje danych aplikacji o nazwie *shardlets* zamapowania ich toodatabases i identyfikację przez *klucze dzielenia na fragmenty*. Może mieć dowolną liczbę baz danych i rozpowszechniają shardlets z tych baz danych. Mapowanie Hello baz danych toohello wartości klucza dzielenia na fragmenty jest przechowywany przez mapy niezależnego fragmentu podał hello biblioteki interfejsów API. Ta funkcja jest wywoływana **zarządzania mapy niezależnego fragmentu**. Mapa niezależnego fragmentu Hello służy również jako hello brokera połączeń z bazą danych dla żądań zawierających klucz dzielenia na fragmenty. Ta funkcja jest określony tooas **danych zależnych routingu**.

![Mapy niezależnego fragmentu i danych zależnych routingu][1]

Menedżera map niezależnego fragmentu Hello chroni użytkowników z widoków niespójne w shardlet dane, które mogą wystąpić, gdy shardlet równoczesnych operacji zarządzania są wykonywane na powitania baz danych. toodo Witaj, niezależnych mapy brokera hello połączenia bazy danych dla aplikacji skompilowanej za pomocą biblioteki hello. Operacje zarządzania niezależnego fragmentu może mieć wpływ na powitania shardlet, umożliwia hello niezależnego fragmentu mapy funkcji tooautomatically kill połączenia z bazą danych. 

Zamiast przy użyciu połączenia toocreate tradycyjny sposób hello Dapper, potrzebujemy toouse hello [metody OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn824099.aspx). Dzięki temu wszystkie hello weryfikacji ma miejsce a połączenia są zarządzane prawidłowo, gdy wszystkie dane są przenoszone między fragmentów.

### <a name="requirements-for-dapper-integration"></a>Wymagania dotyczące integracji Dapper
Podczas pracy z biblioteki klienta elastycznej bazy danych hello i hello Dapper interfejsów API, chcemy hello tooretain następujące właściwości:

* **Skalowania**: Firma Microsoft ma tooadd lub usunąć bazy danych z warstwy danych hello podzielonej aplikacji hello odpowiednio do potrzeb pojemności hello aplikacji hello. 
* **Spójność**: ponieważ naszej aplikacji jest skalowana w poziomie przy użyciu dzielenia na fragmenty, potrzebujemy tooperform danych zależnych routingu. Dlatego chcemy toouse hello danych zależnych routingu możliwości hello toodo biblioteki. W szczególności chcemy tooretain hello weryfikacji i spójność gwarantuje podał połączeń, które są obsługiwane przez brokera za pośrednictwem Menedżera mapy niezależnego fragmentu hello w kolejności tooavoid uszkodzenie lub wyników zapytania niewłaściwy. Dzięki temu tooa tego połączenia, podane shardlet są odrzucone lub zatrzymana, jeśli (na przykład) hello shardlet jest obecnie przeniesionego tooa inny identyfikator niezależnego fragmentu przy użyciu interfejsów API podziału/Merge.
* **Mapowanie obiektu**: chcemy wygody hello tooretain mapowań hello dostarczonych przez Dapper tootranslate między klasami w aplikacji hello i hello podstawowej struktury bazy danych. 

Hello Poniższa sekcja zawiera wskazówki dotyczące tych wymagań aplikacji na podstawie **Dapper** i **DapperExtensions**.

## <a name="technical-guidance"></a>Wskazówki techniczne
### <a name="data-dependent-routing-with-dapper"></a>Zależne od, routing z Dapper danych
Z Dapper aplikacja hello jest zazwyczaj odpowiedzialny za tworzenie i otwieranie toohello połączeń hello podstawowej bazy danych. Określony typ T aplikacja hello, Dapper zwraca wyniki zapytania kolekcji .NET typu T. Dapper wykonuje mapowanie hello z obiektów wynikowych T-SQL hello toohello wierszy typu T. Podobnie Dapper mapuje obiekty .NET do wartości SQL lub parametrów dla instrukcji języka manipulacji danych. Dapper oferuje tę funkcję za pomocą metod rozszerzenia na powitania regularne [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) obiektu z powitania klienta SQL ADO .NET bibliotek. Hello połączenie SQL zwrócony przez hello interfejsy API elastycznego skalowania dla DDR są także regularne [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) obiektów. Dzięki temu nam rozszerzenia Dapper Użyj toodirectly za pośrednictwem hello zwrócone przez interfejs API DDR powitania klienta biblioteki, jak również jest proste połączenia klienta SQL.

Uwagi te umożliwiają połączeń bezpośrednich toouse przez biblioteki klienta elastycznej bazy danych hello obsługiwanych przez brokera dla Dapper.

W tym przykładzie kodu (od hello towarzyszące przykładowe) przedstawiono podejście hello gdzie hello dzielenia na fragmenty klucz jest dostarczany przez hello aplikacji toohello biblioteki toobroker hello połączenia toohello prawo niezależnego fragmentu.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Witaj wywołania toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) interfejsu API zastępuje hello domyślnego tworzenia i otwierania połączenia klienta SQL. Witaj [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) wywołania przyjmuje hello argumenty, które są wymagane dla danych zależnych routingu: 

* Witaj niezależnego fragmentu mapy tooaccess hello zależnych interfejsów routingu danych
* Witaj shardlet hello klucza tooidentify dzielenia na fragmenty
* Witaj poświadczeń (nazwy użytkownika i hasło) tooconnect toohello niezależnych

Obiekt mapy niezależnego fragmentu Hello tworzy niezależnych toohello połączenie, zawierający hello shardlet dla hello podany klucz dzielenia na fragmenty. interfejsów API klienta elastycznej bazy danych Hello tagu również hello tooimplement połączenia, który jego spójność gwarantuje. Od hello wywołać zbyt[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) zwraca regularne obiektu połączenia klienta SQL, hello kolejne wywołanie toohello **Execute** — metoda rozszerzenia z Dapper następujące hello Dapper standardowe praktyki.

Zapytania pracy znacznie Witaj sam sposób - pierwszym otwarciu hello połączenia za pomocą [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) z powitania klienta interfejsu API. Następnie można użyć hello standardowego rozszerzenia Dapper metody toomap hello wyników kwerendy SQL na obiekty .NET:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Należy pamiętać, że hello **przy użyciu** zablokować z zakresami połączenia DDR hello wszystkie operacje bazy danych w ramach hello bloku toohello jeden identyfikator niezależnego fragmentu tam tenantId1 jest przechowywana. Witaj zapytanie zwraca tylko blogi przechowywane na powitania bieżący identyfikator niezależnego fragmentu, ale hello te przechowywane na dowolnej liczbie fragmentów. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Zależne od, routing Dapper i DapperExtensions danych
Dapper pochodzi z ekosystemem dodatkowe rozszerzenia, które udostępniają dalsze zwiększenie wygody działania i abstrakcji z hello bazy danych podczas opracowywania aplikacji bazy danych. Przykładem jest DapperExtensions. 

W aplikacji przy użyciu DapperExtensions nie zmienia sposób połączenia bazy danych są tworzone i zarządzane. Nadal jest aplikacji hello odpowiedzialność tooopen połączeń, a regularne obiekty połączenia klienta SQL są oczekiwane przez metody rozszerzenia hello. Firma Microsoft może polegać na powitania [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) w sposób opisany powyżej. Jako hello następujące przykłady kodu Pokaż, hello jedyna różnica polega na to, że nie mamy już toowrite instrukcje hello T-SQL:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

A Oto przykładowy kod hello hello kwerendy: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Obsługa błędów przejściowych
Witaj Microsoft Patterns & rozwiązania zespołu opublikowanych hello [bloku aplikacji obsługi błędów przejściowych](http://msdn.microsoft.com/library/hh680934.aspx) deweloperzy aplikacji toohelp ograniczenia typowe warunki wystąpienia błędu przejściowego napotkała podczas uruchamiania w chmurze hello. Aby uzyskać więcej informacji, zobacz [Perseverance, klucz tajny wszystkie sukcesy: przy użyciu hello bloku aplikacji obsługi błędów przejściowych](http://msdn.microsoft.com/library/dn440719.aspx).

Przykładowy kod Hello polega na powitania błędu przejściowego biblioteki tooprotect przed błędów przejściowych. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** w hello powyższy kod jest zdefiniowany jako **SqlDatabaseTransientErrorDetectionStrategy** z liczbą ponowień równą 10 i 5 sekund oczekiwania czasu między kolejnymi próbami. Jeśli używane są transakcje, upewnij się, ponów próbę zakresu Przechodzi wstecz toohello rozpoczęciem powitalne transakcji w przypadku wystąpienia błędu przejściowego hello.

## <a name="limitations"></a>Ograniczenia
Witaj metod opisanych w tym dokumencie pociąga za sobą kilka ograniczeń:

* Witaj przykładowy kod dla tego dokumentu nie pokazują, jak schematu toomanage między fragmentów.
* Biorąc pod uwagę na żądanie, przyjęto założenie, że jego przetwarzanie bazy danych znajduje się w obrębie jednego niezależnego fragmentu określonej za pomocą klucza dzielenia na fragmenty hello dostarczonego przez Żądanie hello. Jednak to założenie nie zawsze przechowuje, na przykład, gdy nie jest możliwe toomake dostępne klucz dzielenia na fragmenty. tooaddress tego hello biblioteki klienta elastycznej bazy danych obejmuje hello [MultiShardQuery klasy](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). Klasa Hello implementuje abstrakcji połączenia, na potrzeby zapytań przez kilka fragmentów. Przy użyciu MultiShardQuery w połączeniu z Dapper wykracza poza zakres tego dokumentu hello.

## <a name="conclusion"></a>Podsumowanie
Aplikacji przy użyciu Dapper i DapperExtensions można łatwo korzystać z narzędzi elastycznej bazy danych dla bazy danych SQL Azure. Hello kroków opisanych w tym dokumencie, tych aplikacji można użyć narzędzia hello możliwości zależnych routingu przez zmianę hello tworzenia i otwierania nowych danych [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello toouse obiektów [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) wywołania biblioteki klienta elastycznej bazy danych hello. To ogranicza hello aplikacji zmiany wymagane toothose miejsca gdzie utworzony i otworzyć nowe połączenia. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
