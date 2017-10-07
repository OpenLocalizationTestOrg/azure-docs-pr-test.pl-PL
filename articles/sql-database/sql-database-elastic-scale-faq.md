---
title: "aaaAzure SQL elastycznej skali — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące elastycznego skalowania bazy danych Azure SQL."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Często zadawane pytania dotyczące narzędzi elastycznej bazy danych
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Jak wypełnić hello dzielenia na fragmenty klucza dla informacji o schemacie hello posiadający pojedynczej dzierżawy na niezależnych i żaden klucz dzielenia na fragmenty?
Obiekt informacji schematu Hello jest tylko używane toosplit scalania scenariuszy. Jeśli aplikacja jest z założenia pojedynczej dzierżawy, nie jest wymagane narzędzie do scalania podziału hello i w związku z tym nie ma żadnego obiektu informacji o konieczności toopopulate hello schematu.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Zostały udostępnionych bazy danych i Menedżera Map niezależnego fragmentu mają już, jak zarejestrować tej nowej bazy danych jako niezależnych?
Zobacz  **[Dodawanie aplikacji tooan niezależnego fragmentu, za pomocą biblioteki klienta elastycznej bazy danych hello](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Ile koszt narzędzi elastycznej bazy danych?
Za pomocą biblioteki klienta elastycznej bazy danych hello nie wpływa negatywnie kosztów. Koszty są naliczane tylko w przypadku baz danych Azure SQL hello używanych fragmentów i hello Menedżera Map niezależnego fragmentu, a także role sieć web/proces roboczy hello udostępniania dla narzędzia do scalania podziału hello.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Dlaczego moje poświadczenia nie działają po dodaniu niezależnego fragmentu z innego serwera?
Nie należy używać poświadczeń w formie hello "identyfikator użytkownika =username@servername", po prostu użyć zamiast tego "Nazwa użytkownika = nazwa użytkownika".  Upewnij się również, że logowanie "nazwa_użytkownika" hello, ma uprawnienia na powitania niezależnego fragmentu.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>I wymagają toocreate Menedżera Map niezależnego fragmentu i wypełnić odłamków w każdym uruchomieniu aplikacje?
Nie — Witaj tworzenia hello Menedżera Map niezależnego fragmentu (na przykład  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) jest to jednorazowa operacja.  Aplikacja powinna używać wywołania hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  w momencie uruchamiania aplikacji.  Ma takich tylko jedno wywołanie dla domeny aplikacji.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>Pytania dotyczące korzystania z narzędzi elastycznej bazy danych, jak ich odpowiedzi uzyskać?
Sprawdź dotrzeć toous na powitania [forum usługi Azure SQL Database](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Gdy uzyskać połączenia z bazą danych przy użyciu klucza dzielenia na fragmenty, I może nadal danych zapytania dla innych dzielenia na fragmenty kluczy na powitania sam identyfikator niezależnego fragmentu.  To jest celowe?
Hello interfejsy API elastycznego skalowania umożliwiają połączenie toohello poprawną bazę danych, klucza dzielenia na fragmenty, ale nie zawiera klucza filtrowania dzielenia na fragmenty.  Dodaj **gdzie** klauzule tooyour zapytania toorestrict hello zakresu toohello podano klucz dzielenia na fragmenty, jeśli to konieczne.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Czy można użyć innej wersji bazy danych platformy Azure dla każdego niezależnego fragmentu w zestawu niezależnego fragmentu?
Tak, niezależnych jest jedna baza danych, a w związku z tym jednego niezależnego fragmentu może być wersji Premium innego być Standard edition. Ponadto hello wersji niezależnych można skalować w górę lub w dół wiele razy w ciągu okresu istnienia hello niezależnych hello.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Czy hello udostępnić narzędzia do scalania podziału (lub usunąć) bazy danych podczas operacji dzielenie i scalanie?
Nie. Aby uzyskać **podzielić** operacji, musi istnieć z odpowiedniego schematu hello hello docelowej bazy danych i być zarejestrowane przy użyciu hello Menedżera Map niezależnego fragmentu.  Aby uzyskać **scalania** operacje, musisz usunąć niezależnych hello hello niezależnego fragmentu Mapa menedżera, a następnie usunąć bazę danych hello.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

