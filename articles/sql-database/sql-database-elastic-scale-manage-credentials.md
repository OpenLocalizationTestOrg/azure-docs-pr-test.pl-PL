---
title: "poświadczenia aaaManaging biblioteki klienta elastycznej bazy danych hello | Dokumentacja firmy Microsoft"
description: "Jak tooset hello odpowiedni poziom poświadczeń administratora tooread tylko dla elastycznej bazy danych aplikacji"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess
Witaj [biblioteki klienta elastycznej bazy danych](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) używa trzech różnych rodzajów hello tooaccess poświadczenia [menedżera map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md). W zależności od potrzeby hello za pomocą poświadczeń hello hello najniższa możliwy dostęp.

* **Poświadczenia zarządzania**: do tworzenia lub manipulowanie menedżera map niezależnego fragmentu. (Zobacz hello [słownik](sql-database-elastic-scale-glossary.md).) 
* **Dostęp do poświadczeń**: tooaccess niezależnych istniejącego mapowania Menedżera tooobtain informacje o liczbie fragmentów.
* **Poświadczenia połączenia**: tooconnect tooshards. 

Zobacz też [Zarządzanie bazami danych i logowaniami w bazie danych SQL Azure](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Informacji o poświadczeniach zarządzania
Zarządzanie poświadczenia są używane toocreate [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) obiektu dla aplikacji, które manipulowania niezależnego fragmentu mapowania. (Na przykład, zobacz [Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych](sql-database-elastic-scale-add-a-shard.md) i [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md)) użytkownika hello biblioteki klienta elastycznej skali hello tworzy hello SQL użytkowników i kont logowania SQL i upewnia się, każdy jest przyznaje uprawnienia odczytu/zapisu hello na powitania globalne niezależnego fragmentu mapy bazy danych i wszystkie również niezależnego fragmentu bazy danych.. Te poświadczenia są używane toomaintain hello globalne niezależnego fragmentu mapowania i map niezależnych lokalne powitania podczas zmiany toohello niezależnego fragmentu mapy. Na przykład użyć hello zarządzania poświadczenia toocreate hello niezależnego fragmentu mapy menedżera obiektu (za pomocą [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

Zmienna Hello **smmAdminConnectionString** jest ciąg połączenia, który zawiera hello zarządzania poświadczeniami. Hello identyfikator użytkownika i hasło zawiera odczytu/zapisu dostępu tooboth niezależnego fragmentu mapy do bazy danych i poszczególnych fragmentów. Parametry połączenia zarządzania Hello również baza hello serwera nazwę i bazy danych nazwa tooidentify hello globalne niezależnych mapy. Poniżej przedstawiono typowe parametry, w tym celu:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Nie używaj wartości w postaci hello "username@server" — zamiast tego użyć wartości "nazwa_użytkownika" hello.  Jest to spowodowane poświadczeń, należy skontaktować się przed zarówno hello niezależnego fragmentu mapy manager w bazie danych, jak i poszczególnych fragmentów, które mogą znajdować się na różnych serwerach.

## <a name="access-credentials"></a>Poświadczenia dostępu
Podczas tworzenia niezależnych Menedżera mapy w aplikacji, która nie administrować niezależnego fragmentu mapy, Użyj poświadczeń z uprawnieniami tylko do odczytu na mapie globalne niezależnych hello. Witaj informacje o pobrane z mapy globalne niezależnych hello te poświadczenia są używane do [routingu zależne od danych](sql-database-elastic-scale-data-dependent-routing.md) i niezależnych hello toopopulate mapowanie pamięci podręcznej na powitania klienta. Witaj poświadczenia są dostarczane za pośrednictwem hello sam call wzorzec zbyt**GetSqlShardMapManager** zgodnie z powyższym: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Należy zwrócić uwagę użycie hello hello **smmReadOnlyConnectionString** tooreflect hello Użyj innych poświadczeń dla tego dostępu dla **bez uprawnień administratora** użytkowników: te poświadczenia nie powinien zawierać zapisu uprawnienia dotyczące hello globalne niezależnych mapy. 

## <a name="connection-credentials"></a>Poświadczenia połączenia
Dodatkowe poświadczenia są wymagane w przypadku korzystania z hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) tooaccess metody niezależnych, skojarzone z kluczem dzielenia na fragmenty. Te poświadczenia potrzebne uprawnienia tooprovide dostęp tylko do odczytu toohello lokalnego niezależnych mapy tabel znajdującej się na powitania niezależnego fragmentu. Jest to wymagane tooperform sprawdzania poprawności połączenia zależne od danych routingu na powitania niezależnego fragmentu. Następujący fragment kodu umożliwia dostęp do danych w kontekście hello zależnych routingu danych: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

W tym przykładzie **smmUserConnectionString** zawiera parametry połączenia hello hello poświadczeń użytkownika. Dla bazy danych SQL Azure w tym miejscu jest ciąg połączenia typowe dla poświadczeń użytkownika: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Podobnie jak w przypadku poświadczeń administratora hello, nie wartości w postaci hello "username@server". Zamiast tego można użyć "nazwa_użytkownika".  Należy również zauważyć, że parametry połączenia hello nie zawiera nazwę serwera i nazwę bazy danych. Jest to spowodowane tym hello **OpenConnectionForKey** wywołania spowoduje automatyczne kierowanie toohello połączenia hello poprawny identyfikator niezależnego fragmentu oparte na kluczu hello. W związku z tym hello nazwy bazy danych i serwera nie są dostarczane. 

## <a name="see-also"></a>Zobacz też
[Zarządzanie bazami danych i nazwami logowania w usłudze Azure SQL Database](sql-database-manage-logins.md)

[Zabezpieczanie bazy danych SQL](sql-database-security-overview.md)

[Wprowadzenie zadania elastycznej bazy danych](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

