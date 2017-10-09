---
title: Transakcje aaaDistributed dla baz danych w chmurze
description: "Omówienie transakcji elastycznej bazy danych z bazy danych Azure SQL"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Transakcje rozproszone w bazach danych w chmurze
Transakcji elastycznej bazy danych dla usługi Azure SQL Database (baza danych SQL) pozwalają transakcje toorun, obejmujące wiele baz danych w bazie danych SQL. Transakcji elastycznej bazy danych dla bazy danych SQL są dostępne dla aplikacji .NET przy użyciu ADO .NET oraz integrują się z hello znanych środowisko programowania przy użyciu hello [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) klasy. Biblioteka hello tooget, zobacz [.NET Framework 4.6.1 (Instalator internetowy)](https://www.microsoft.com/download/details.aspx?id=49981).

Lokalnie takiej sytuacji są zwykle wymagane systemem koordynatora transakcji rozproszonych (MSDTC). Ponieważ usługa MSDTC nie jest dostępna dla aplikacji platformy jako usługa na platformie Azure, transakcje rozproszone toocoordinate możliwości hello ma teraz bezpośrednio integrowane bazy danych SQL. Aplikacje mogą łączyć transakcje rozproszone toolaunch bazy danych SQL tooany i jednej z baz danych hello niewidocznie będzie koordynować z transakcji rozproszonych hello pokazane na powitania po rysunku. 

  ![Transakcje rozproszone w usłudze Azure SQL Database przy użyciu transakcji elastycznej bazy danych ][1]

## <a name="common-scenarios"></a>Typowe scenariusze
Transakcji elastycznej bazy danych dla bazy danych SQL. Włącz toodata atomic zmiany toomake aplikacji przechowywanych w wielu różnych baz danych SQL. Podgląd Hello koncentruje się na procesy programowanie po stronie klienta w C# i platformy .NET. Czynności po stronie serwera, za pomocą T-SQL jest zaplanowane na później.  
Następujące scenariusze hello cele transakcji elastycznej bazy danych:

* Bazy danych wielu aplikacji na platformie Azure: W tym scenariuszu danych jest pionowo podzielonym na partycje w kilku baz danych w bazie danych SQL tak, aby różne rodzaje danych znajdują się na różnych baz danych. Niektóre operacje wymagają toodata zmian, który jest przechowywany w dwóch lub więcej baz danych. Aplikacja Hello używa zmiany hello toocoordinate transakcji elastycznej bazy danych dla baz danych i upewnij się, niepodzielność.
* Aplikacje bazy danych podzielonej na platformie Azure: W tym scenariuszu hello warstwy danych użyto hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md) lub toohorizontally dzielenia na fragmenty samoobsługowego partycji hello danych przez wiele baz danych w bazie danych SQL. Jeden przypadek użycia poświęcone jest hello potrzeby tooperform atomic zmiany dla podzielonej aplikacji wielodostępnej podczas zmiany span dzierżaw. Traktować dla wystąpienia transfer z tooanother jednej dzierżawy, zarówno znajdującej się na różnych baz danych. Drugim przypadku jest wymagana pojemność tooaccommodate szczegółowych dzielenia na fragmenty dla dużych dzierżawy, który z kolei zwykle oznacza, że niektóre toostretch potrzeb operacji niepodzielnych w kilku bazy danych używane do hello sam dzierżawy. Trzeci zdarza się atomic tooreference danych, które są replikowane między bazami danych. Niepodzielne, transakcyjne, operacje na te wiersze można teraz koordynowane przez wiele baz danych za pomocą podglądu hello.
  Transakcji elastycznej bazy danych użyj dwufazowe tooensure transakcji niepodzielność dla baz danych. Należy dobrze dla transakcji, które obejmują mniej niż 100 baz danych w czasie w ramach jednej transakcji. Ograniczenia te nie są wymuszane, ale jeden oczekiwać wydajności i odsetka pomyślnych dla toosuffer transakcji elastycznej bazy danych po przekroczeniu tych limitów.

## <a name="installation-and-migration"></a>Instalacja i migracji
możliwości Hello transakcji elastycznej bazy danych w bazie danych SQL są realizowane za pośrednictwem aktualizacji bibliotek .NET toohello System.Data.dll i Biblioteka System.Transactions.dll. Witaj biblioteki DLL upewnij się że dwufazowe jest używana w miarę potrzeby niepodzielność tooensure. Zainstaluj toostart: tworzenie aplikacji przy użyciu transakcji elastycznej bazy danych, [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) lub nowszym. Podczas uruchamiania w starszej wersji hello platformy .NET Framework, transakcje zakończy się niepowodzeniem transakcji rozproszonych tooa toopromote i zostanie zgłoszony wyjątek.

Po instalacji można transakcji rozproszonych hello interfejsów API w System.Transactions z tooSQL połączenia bazy danych. Jeśli masz istniejące aplikacje usługi MSDTC za pomocą tych interfejsów API, po zainstalowaniu hello 4.6.1 po prostu odbudować istniejące aplikacje dla .NET 4.6 Framework. Projektów skierowania .NET 4.6, zostanie automatycznie korzystają z bibliotek DLL hello zaktualizowane z nowej wersji Framework hello i wywołania interfejsu API transakcji rozproszonych w połączeniu z tooSQL połączeń, które teraz powiedzie się bazy danych.

Należy pamiętać, że transakcji elastycznej bazy danych nie wymagają instalowania usługi MSDTC. Zamiast tego transakcji elastycznej bazy danych są zarządzane bezpośrednio przez i w obrębie bazy danych SQL. To znacznie upraszcza scenariusze chmury, ponieważ wdrożenie usługi MSDTC nie jest konieczne toouse rozproszonych transakcje z bazy danych SQL. 4 z sekcji wyjaśniono szczegółowo w sposób toodeploy transakcji elastycznej bazy danych i hello wymagane .NET framework wraz z tooAzure aplikacji w chmurze.

## <a name="development-experience"></a>Środowisko programistyczne
### <a name="multi-database-applications"></a>Aplikacje wielu baz danych
Witaj następujący przykładowy kod używa hello znanych środowisko programowania z .NET System.Transactions. Witaj klasy elementu TransactionScope ustanawia transakcja otoczenia w .NET. ("Transakcja otoczenia" jest taki, który znajduje się w bieżącym wątku hello). Wszystkie połączenia otwarty w hello TransactionScope uczestniczyć w hello transakcji. Jeśli udział różnych baz danych, transakcji hello jest automatycznie z podwyższonym poziomem uprawnień tooa distributed transaction. Witaj wyniku transakcji hello jest kontrolowany przez ustawienie tooindicate toocomplete zakresu hello na zatwierdzenie.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Aplikacje baz danych podzielonej
Transakcji elastycznej bazy danych dla bazy danych SQL obsługuje również koordynowanie transakcji rozproszonych, gdy używana jest metoda OpenConnectionForKey hello hello elastycznej bazy danych klienta biblioteki tooopen połączeń skalowanej danych warstwy. Należy wziąć pod uwagę przypadkach, gdy muszą spójności transakcyjnej tooguarantee zmiany na kilka różnych dzielenia na fragmenty wartości klucza. Hosting wartości klucza różnych dzielenia na fragmenty hello odłamków toohello połączenia jest przeprowadzana przy użyciu OpenConnectionForKey. W przypadku ogólnych hello hello połączenia może być odłamków toodifferent tak, aby zapewnienie transakcyjne gwarancje wymaga transakcji rozproszonej. powitania po przykładowy kod przedstawia tej metody. Przyjęto założenie, że zmienna o nazwie shardmap jest używane toorepresent niezależnego fragmentu mapowania z biblioteki klienta elastycznej bazy danych hello:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Instalacja środowiska .NET dla usługi w chmurze Azure
Platforma Azure udostępnia kilka ofert toohost aplikacji .NET. Porównanie różnych ofert hello jest dostępna w [porównanie usługi Azure App Service, usługi w chmurze i maszyn wirtualnych](../app-service-web/choose-web-site-cloud-service-vm.md). Witaj system operacyjny gościa oferty hello jest mniejszy niż .NET 4.6.1 wymagane dla transakcji elastycznej, należy najpierw too4.6.1 systemu operacyjnego gościa hello tooupgrade. 

Usługi aplikacji Azure uaktualnia gościa toohello systemu operacyjnego nie są obecnie obsługiwane. Maszyn wirtualnych platformy Azure, wystarczy zalogować się do hello maszyny Wirtualnej i uruchom Instalatora hello hello najnowsze .NET Framework. Usługi w chmurze Azure należy tooinclude instalacji hello nowszą wersją .NET na powitania uruchamianie zadania wdrożenia. Witaj pojęcia i kroki opisano w [zainstalować .NET dla roli usługi chmury](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Należy pamiętać, że hello Instalatora dla platformy .NET 4.6.1 może wymagać więcej magazyn tymczasowy podczas hello uruchamianie procesu na usług w chmurze Azure niż hello Instalator programu .NET 4.6. tooensure instalacja zakończyła się pomyślnie, należy tooincrease tymczasowego magazynu dla usługi w chmurze platformy Azure w pliku ServiceDefinition.csdef w sekcji LocalResources hello i ustawienia środowiska hello uruchomienia zadania, jak pokazano poniżej hello przykład:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transakcje na wielu serwerach
Transakcji elastycznej bazy danych są obsługiwane na różnych serwerach logicznych w bazie danych SQL Azure. Gdy transakcje przekraczają granice serwer logiczny, serwerów hello muszą najpierw toobe wprowadzona w relacji wzajemnego komunikacji. Po ustanowieniu relacji komunikacji hello wszystkie bazy danych w żadnym powitalne dwa serwery mogą uczestniczyć w elastycznej transakcje z bazy danych z hello inny serwer. O transakcjach więcej niż dwa serwery logiczne relację komunikacji wymaga toobe w miejscu dla każdej pary serwerów logicznych.

Użyj hello następującego środowiska PowerShell polecenia cmdlet toomanage komunikacji między serwerami relacje dla transakcji elastycznej bazy danych:

* **Nowy AzureRmSqlServerCommunicationLink**: Użyj tego polecenia cmdlet toocreate nowej relacji komunikacji między dwoma serwerami logicznych w bazie danych SQL Azure. Relacja Hello jest symetrycznego, co oznacza, że oba serwery mogą inicjować transakcji z hello inny serwer.
* **Get-AzureRmSqlServerCommunicationLink**: Użyj tego polecenia cmdlet tooretrieve istniejącą komunikację relacji i ich właściwości.
* **Usuń AzureRmSqlServerCommunicationLink**: Użyj tego polecenia cmdlet tooremove istniejącej relacji komunikacji. 

## <a name="monitoring-transaction-status"></a>Monitorowanie stanu transakcji
Użyj dynamicznych widoków zarządzania (widoków DMV) w bazy danych SQL toomonitor stan i postęp transakcji trwającą elastycznej bazy danych. Wszystkie widoków DMV tootransactions powiązane są odpowiednie dla transakcji rozproszonych w bazie danych SQL. Listę można znaleźć hello odpowiedniego z widoków DMV tutaj: [powiązane dynamicznych widoków zarządzania transakcji i funkcji (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Tych widoków DMV jest szczególnie przydatna:

* **sys.DM\_tran\_active\_transakcji**: Wyświetla listę obecnie aktywnych transakcji i ich stan. Witaj kolumny UOW (jednostka pracy) może zidentyfikować hello podrzędnego innej transakcji, które należy toohello sama transakcja rozproszona. Tę samą wartość UOW hello wszystkie transakcje hello przenoszenia jednej transakcji rozproszonej. Zobacz hello [dokumentacji DMV](https://msdn.microsoft.com/library/ms174302.aspx) więcej szczegółów.
* **sys.DM\_tran\_bazy danych\_transakcji**: udostępnia dodatkowe informacje o transakcji, takich jak umieszczania hello transakcji w dzienniku hello. Zobacz hello [dokumentacji DMV](https://msdn.microsoft.com/library/ms186957.aspx) więcej szczegółów.
* **sys.DM\_tran\_blokad**: zawiera informacje o hello blokad, które są obecnie przechowywane w bieżących transakcji. Zobacz hello [dokumentacji DMV](https://msdn.microsoft.com/library/ms190345.aspx) więcej szczegółów.

## <a name="limitations"></a>Ograniczenia
Witaj obecnie następujące ograniczenia mają zastosowanie tooelastic transakcji bazy danych w bazie danych SQL:

* Obsługiwane są tylko transakcje dla baz danych w bazie danych SQL. Inne [X / Otwórz XA](https://en.wikipedia.org/wiki/X/Open_XA) dostawców zasobów i baz danych poza bazy danych SQL nie może brać udziału w transakcji elastycznej bazy danych. Oznacza to, że transakcji elastycznej bazy danych nie można rozciągnąć na lokalnie serwer SQL i baz danych SQL Azure. Transakcje rozproszone lokalnie nadal toouse usługi MSDTC. 
* Tylko koordynowane klienta transakcje z aplikacji .NET są obsługiwane. Obsługa po stronie serwera T-SQL, takich jak rozpocząć transakcji ROZPROSZONYCH jest planowane, ale nie jest jeszcze dostępna. 
* Transakcje w usługach WCF nie są obsługiwane. Na przykład masz metody usługi WCF, która wykonuje transakcji. Otaczający wywołanie hello w zakresie transakcji nie powiedzie się jako [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Następne kroki
Odpowiedzi na pytania, proszę dotrzeć toous na powitania [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je toohello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



