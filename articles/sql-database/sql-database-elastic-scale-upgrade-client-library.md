---
title: aaaUpgrade toohello najnowsze biblioteki klienta elastycznej bazy danych | Dokumentacja firmy Microsoft
description: "Uaktualnianie aplikacji i bibliotek przy użyciu narzędzia Nuget"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Uaktualnienie aplikacji toouse hello najnowsze elastycznej bazy danych biblioteki klienta
Nowe wersje hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md) są dostępne za pośrednictwem interfejsu Menedżera NuGetPackage hello NuGetand w programie Visual Studio. Uaktualnień obsługę nowych funkcji biblioteki klienta hello oraz zawierać poprawki.

**Do najnowszej wersji hello:** Przejdź zbyt[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Odbuduj aplikacji przy użyciu nowej biblioteki hello, a także zmienić istniejące metadanych Menedżera Map niezależnego fragmentu przechowywane w Twojej bazy danych SQL Azure toosupport nowe funkcje.

Te kroki są wykonywane w kolejności gwarantuje, że starsze wersje biblioteki klienta hello nie są już dostępne w danym środowisku po zaktualizowaniu obiektów metadanych, co oznacza, że po uaktualnieniu nie można utworzyć obiektów stara wersja metadanych.   

## <a name="upgrade-steps"></a>Kroki uaktualniania
**1. Uaktualnienie aplikacji.** W Visual Studio, pobierania i odwołanie powitania klienta biblioteki najnowszym do wszystkich projektów programowanie korzystających z biblioteki hello; następnie ponownie skompilować i wdrożyć. 

* W rozwiązaniu programu Visual Studio wybierz **narzędzia** --> **Menedżera pakietów NuGet** -->  **Zarządzaj pakietami NuGet dla rozwiązania**. 
* (Visual Studio 2013) W lewym panelu hello, wybierz **aktualizacje**, a następnie wybierz hello **aktualizacji** przycisk na powitania pakietu **Azure SQL Database elastyczne skalowanie klienta Library** wyświetlonym w hello okno.
* (Visual Studio 2015) Ustaw pole filtru hello zbyt**uaktualnienia dostępne**. Wybierz hello tooupdate pakietu, a następnie kliknij przycisk hello **aktualizacji** przycisku.
* (Visual Studio 2017) U góry okna dialogowego hello hello, wybierz **aktualizacje**. Wybierz hello tooupdate pakietu, a następnie kliknij przycisk hello **aktualizacji** przycisku.
* Tworzenie i wdrażanie. 

**2. Uaktualnij skryptów.** Jeśli używasz **PowerShell** skrypty odłamków toomanage [pobrać nową wersję biblioteki hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) i skopiować go do katalogu hello, z którego wykonywanie skryptów. 

**3. Uaktualnij usługę podziału scalania.** Jeśli używasz hello elastycznej bazy danych narzędzia do scalania podziału tooreorganize podzielony na niezależne fragmenty danych, [pobrać i zainstalować najnowszą wersję narzędzia hello hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Szczegółowe kroki uaktualnienia można znaleźć usługi hello [tutaj](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Uaktualnienie bazy danych Menedżera Map niezależnego fragmentu**. Uaktualnij metadanych hello Obsługa map niezależnego fragmentu w bazie danych SQL Azure.  Istnieją dwa sposoby, można to zrobić, za pomocą programu PowerShell lub C#. Poniżej przedstawiono obie opcje.

***Opcja 1: Metadane aktualizacji przy użyciu programu PowerShell***

1. Pobierz hello najnowsza wersja narzędzia wiersza polecenia programu NuGet z [tutaj](http://nuget.org/nuget.exe) i Zapisz tooa folderu. 
2. Otwórz wiersz polecenia, przejdź toohello tym samym folderze, a problem hello polecenia:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Przejdź podfolder toohello zawierający hello nowej biblioteki DLL wersji klienta po prostu pobrany, na przykład:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Pobierz skryptlet uaktualnienia hello elastycznej bazy danych klienta z hello [Centrum skryptów](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), i zapisz go na powitania tego samego folderu zawierającego hello biblioteki DLL.
5. Z tego folderu Uruchom ".\upgrade.ps1 programu PowerShell" w wierszu polecenia hello i postępuj zgodnie z monitami hello.

***Opcja 2: Uaktualnienie metadanych za pomocą języka C#***

Można również utworzyć aplikację programu Visual Studio, która otwiera ShardMapManager Twojego, przechodzi przez wszystkie odłamków i przeprowadza uaktualnienie metadanych hello przez wywołanie metody hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) i [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) jak w poniższym przykładzie: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Techniki metadane uaktualnienia można zastosować wiele razy bez problemów. Na przykład jeśli starsza wersja klienta tworzy przypadkowo niezależnych po zaktualizowaniu już, można uruchomić uaktualnienia ponownie we wszystkich tooensure odłamków tego hello najnowszej wersji metadanych jest obecny w całej infrastrukturze. 

**Uwaga:** nowych wersji biblioteki klienta hello opublikowane do daty kontynuować toowork we wcześniejszych wersjach hello niezależnego fragmentu Mapa menedżera metadanych dla bazy danych SQL Azure i na odwrót.   Jednak zaletą tootake niektóre nowe funkcje hello hello najnowszego klienta metadanych musi toobe uaktualniony.   Należy pamiętać o tym, czy metadane uaktualnienia nie wpłynie na wszystkie dane użytkownika lub dane specyficzne dla aplikacji, tylko obiekty tworzone i używane przez hello Menedżera Map niezależnego fragmentu.  A aplikacje nadal toooperate za pośrednictwem hello sekwencji uaktualniania opisany powyżej. 

## <a name="elastic-database-client-version-history"></a>Historia wersji klienta elastycznej bazy danych
Historii wersji, przejdź zbyt[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

