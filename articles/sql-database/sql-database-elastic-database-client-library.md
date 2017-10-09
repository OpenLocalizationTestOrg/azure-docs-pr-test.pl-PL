---
title: bazy danych chmury skalowalne aaaBuilding | Dokumentacja firmy Microsoft
description: "Tworzenie skalowalnych aplikacji .NET bazy danych za pomocą biblioteki klienta elastycznej bazy danych hello"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Tworzenie skalowalnych baz danych w chmurze
Skalowanie w poziomie baz danych można łatwo osiągnąć za pomocą funkcji i narzędzi skalowalne bazy danych SQL Azure. W szczególności można użyć hello **biblioteki klienta elastycznej bazy danych** toocreate i zarządzanie bazami danych skalowalnych w poziomie. Ta funkcja pozwala łatwo tworzyć aplikacje podzielonej przy użyciu setki —, a nawet tysiące — baz danych Azure SQL. [Zadania elastyczne](sql-database-elastic-jobs-powershell.md) mogą być następnie używane toohelp ułatwiają zarządzanie tych baz danych.

Biblioteka hello tooinstall, przejdź do zbyt[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Dokumentacja
1. [Wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md)
2. [Elastyczne funkcje bazy danych](sql-database-elastic-scale-introduction.md)
3. [Zarządzanie mapami fragmentów](sql-database-elastic-scale-shard-map-management.md)
4. [Migrowanie istniejących baz danych tooscale w poziomie](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Routing zależny od danych](sql-database-elastic-scale-data-dependent-routing.md)
6. [Wiele niezależnych zapytań](sql-database-elastic-scale-multishard-querying.md)
7. [Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych](sql-database-elastic-scale-add-a-shard.md)
8. [Aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Uaktualnij klienta biblioteki aplikacji](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Elastyczne zapytań — omówienie](sql-database-elastic-query-overview.md)
11. [Słownik narzędzi elastycznych baz danych](sql-database-elastic-scale-glossary.md)
12. [Biblioteka klienta usługi elastycznej bazy danych z programu Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Biblioteki klienta elastycznej bazy danych z Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Narzędzie do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Liczniki wydajności dla menedżera map fragmentów](sql-database-elastic-database-client-library.md) 
16. [Często zadawane pytania dotyczące narzędzi elastycznej bazy danych](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Możliwości klienta
Skalowanie w poziomie aplikacji przy użyciu *dzielenia na fragmenty* przedstawia problemy dotyczące zarówno hello developer, jak i hello administratora. powitania klienta biblioteki upraszcza zadania zarządzania hello, udostępniając narzędzia umożliwiające deweloperom zarówno i administratorom zarządzanie bazami danych skalowalnych w poziomie. W typowym przykładem istnieje wiele baz danych, nazywane "odłamków", toomanage. Klienci są wspólnie w hello tej samej bazy danych i jest jedną bazę danych na klienta (schemat pojedynczej dzierżawy). Biblioteka klienta Hello zawiera następujące funkcje:

- **Zarządzanie mapy niezależnego fragmentu**: specjalne bazy danych o nazwie "Menedżer mapy niezależnego fragmentu" hello jest tworzony. Zarządzanie mapy niezależnego fragmentu jest możliwość hello metadanych toomanage aplikacji o jego odłamków. Deweloperzy można używać baz danych to funkcja tooregister jako odłamków, opisano mapowania poszczególnych dzielenia na fragmenty kluczy lub baz danych toothose zakresami kluczy i Obsługa metadanych jako numer hello i tooreflect pojemność zmiany rozwoju środowisko kompozycji baz danych. Bez hello biblioteki klienta elastycznej bazy danych trzeba toospend mnóstwo czasu kod zarządzania hello podczas implementowania dzielenia na fragmenty. Aby uzyskać więcej informacji, zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).

- **Routing zależnych danych**: Wyobraź sobie żądanie do aplikacji hello. Oparte na wartości klucza dzielenia na fragmenty hello hello żądania, aplikacja hello musi hello toodetermine prawidłowa baza danych oparta na wartości klucza hello. Otwiera Żądanie hello tooprocess połączenia toohello bazy danych. Routing zależnych danych umożliwia określenie hello tooopen połączeń przy użyciu jednego wywołania łatwe do mapy niezależnego fragmentu hello aplikacji hello. Routing zależnych danych był inny obszar kodu infrastruktury, który jest teraz objęte funkcji biblioteki klienta elastycznej bazy danych hello. Aby uzyskać więcej informacji, zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md).
- **Wiele niezależnych kwerendy (MSQ)**: badania wielu niezależnych działa, gdy żądanie obejmuje odłamków kilka (lub wszystkie). Zapytanie wielu niezależnych wykonuje hello tego samego kodu T-SQL na wszystkich odłamków lub zbiór fragmentów. wyniki Hello hello uczestniczących odłamków są scalane w ogólnej zestawu, używając semantyki UNION ALL wyników. Witaj funkcji jako dostępne za pośrednictwem powitania klienta biblioteki obsługuje wiele zadań, takich jak: Zarządzanie połączeniami, zarządzanie wątkami, obsługa błędów i pośrednich wyników przetwarzania. MSQ można badać się toohundreds fragmentów. Aby uzyskać więcej informacji, zobacz [zapytań wielu niezależnych](sql-database-elastic-scale-multishard-querying.md).

Ogólnie rzecz biorąc klientów przy użyciu narzędzi elastycznej bazy danych można oczekiwać, że funkcje T-SQL tooget podczas przesyłania operacji niezależnych lokalnego jako min. niezależnych toocross operacje, które mają własne semantyki.

## <a name="next-steps"></a>Następne kroki
Spróbuj hello [Przykładowa aplikacja](sql-database-elastic-scale-get-started.md) który demonstruje powitania klienta funkcji. 

Biblioteka hello tooinstall, przejdź zbyt[elastycznej bazy danych klienta biblioteki](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Aby uzyskać instrukcje na temat używania narzędzia do scalania podziału hello, zobacz hello [Omówienie narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md).

[Biblioteki klienta elastycznej bazy danych jest teraz otworzyć pochodzenia!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Użyj [elastycznej zapytania](sql-database-elastic-query-overview.md).

Witaj biblioteki jest dostępny jako oprogramowanie typu open source na [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

