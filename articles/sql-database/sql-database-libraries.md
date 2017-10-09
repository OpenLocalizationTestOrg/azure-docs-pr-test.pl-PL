---
title: biblioteki aaaConnection bazy danych SQL | Dokumentacja firmy Microsoft
description: "Zawiera łącza do pobrania modułów, które umożliwiają połączenie tooSQL serwera i bazy danych SQL z szerokiej gamy klienta języków programowania. Moduły Hello są wydawane przez społeczność hello lub przez firmę Microsoft."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: genemi
ms.assetid: 13d899d3-cf46-4e4d-8919-cf4b41ca836d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: genemi
ms.openlocfilehash: 6ea77670276ad3304c7531f7ffd8f7dffd31af46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Łączność bibliotek i platform dla programu Microsoft SQL Server

Zapoznaj się z naszym [pobierania samouczków dotyczących](http://aka.ms/sqldev) tooquickly wprowadzenie do programowania języków, takich jak C#, Java, Node.js, PHP i Python i kompilowania aplikacji za pomocą programu SQL Server w systemie Linux lub Windows lub platformy Docker na macOS.

Hello w poniższej tabeli wymieniono łączności biblioteki lub *sterowniki* czy aplikacje klienckie mogą używać z różnych języków tooconnect tooand użytkowania programu Microsoft SQL Server, uruchamiane lokalnie lub w chmurze hello, w systemie Linux, Windows lub Docker i również tooAzure bazy danych SQL i magazyn danych SQL Azure. 

| Język | Platforma | Dodatkowe zasoby | Do pobrania | Wprowadzenie |
| :-- | :-- | :-- | :-- | :-- |
| C# | System macOS Windows, Linux, | [Microsoft ADO.NET dla programu SQL Server](https://docs.microsoft.com/sql/connect/ado-net/microsoft-ado-net-for-sql-server) | [Pobieranie](https://www.microsoft.com/net/download/) | [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | System macOS Windows, Linux, | [Sterownik JDBC firmy Microsoft dla programu SQL Server](http://msdn.microsoft.com/library/mt484311.aspx) | [Pobieranie](https://go.microsoft.com/fwlink/?linkid=852460) |  [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | System macOS Windows, Linux,| [Sterownik PHP SQL dla programu SQL Server](http://msdn.microsoft.com/library/dn865013.aspx) | System operacyjny: <br/> \*[Systemu Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \*[Systemu Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \*[macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | System macOS Windows, Linux, | [Sterownik programu node.js dla programu SQL Server](http://msdn.microsoft.com/library/mt652093.aspx) | [Instalowanie](https://msdn.microsoft.com/library/mt652094.aspx) |  [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | System macOS Windows, Linux, | [Sterownik SQL Python](http://msdn.microsoft.com/library/mt652092.aspx) | Zainstaluj opcje: <br/> \*[pymssql](https://msdn.microsoft.com/library/mt694094.aspx) <br/> \*[pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | System macOS Windows, Linux, | [Sterownik dopisków fonetycznych dla programu SQL Server](http://msdn.microsoft.com/library/mt691981.aspx) | [Instalowanie](https://msdn.microsoft.com/library/mt711041.aspx) | [Rozpoczęcie pracy](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | System macOS Windows, Linux, | [Sterownik ODBC firmy Microsoft dla programu SQL Server](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [Pobieranie](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

Witaj w poniższej tabeli przedstawiono kilka przykładów struktur relacyjne mapowania ORM (Object) i struktur sieci web, co aplikacje klienckie można użyć programu Microsoft SQL Server, uruchamiane lokalnie lub w chmurze hello, w systemie Linux, Windows lub Docker i również tooAzure bazy danych SQL i Magazyn danych Azure SQL. 

| Język | Platforma | ORM(s) |
| :-- | :-- | :-- |
| C# | System macOS Windows, Linux, | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Program Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/index) |
| Java | System macOS Windows, Linux, |[Hibernacji ORM](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | System macOS Windows, Linux, | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | System macOS Windows, Linux, |[Django](https://www.djangoproject.com/) |
| Ruby | System macOS Windows, Linux, | [Ruby na szyny](http://rubyonrails.org/) |

## <a name="related-links"></a>Powiązane linki
- [SQL Server sterowniki](http://msdn.microsoft.com/library/mt654049.aspx) do łączenia za pośrednictwem aplikacji klienckich
- [Połącz tooSQL bazy danych przy użyciu programu .NET (C#)](sql-database-connect-query-dotnet.md)
- [Połącz tooSQL bazy danych za pomocą języka PHP](sql-database-connect-query-php.md)
- [Połącz tooSQL bazy danych przy użyciu środowiska Node.js](sql-database-connect-query-nodejs.md)
- [Łączenie tooSQL bazy danych przy użyciu języka Java](sql-database-connect-query-java.md)
- [Łączenie tooSQL bazy danych przy użyciu języka Python](sql-database-connect-query-python.md)
- [Łączenie tooSQL bazy danych przy użyciu Ruby](sql-database-connect-query-ruby.md)
