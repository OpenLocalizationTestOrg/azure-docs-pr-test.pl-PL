---
title: tooAzure aaaConnect SQL Data Warehouse | Dokumentacja firmy Microsoft
description: "Jak ciąg połączenia i nazwę serwera na powitania toofind dla Twojego tooAzure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>Połącz tooAzure SQL Data Warehouse
Ten artykuł ułatwia rozpoczęcie tooSQL podłączonego magazynu danych na powitania po raz pierwszy.

## <a name="find-your-server-name"></a>Znajdowanie nazwy serwera
Witaj pierwszy krok tooconnecting tooSQL uprzedniego uzyskania informacji o magazynie danych jak toofind nazwę serwera.  Na przykład nazwa serwera hello w hello poniższy przykład jest sample.database.windows.net. Nazwa FQDN serwera hello toofind:

1. Przejdź toohello [portalu Azure][Azure portal].
2. Kliknij pozycję **Bazy danych SQL**. 
3. Polecenie hello bazy danych, które mają tooconnect do.
4. Zlokalizuj hello pełną nazwę serwera.
   
    ![Pełna nazwa serwera][1]

## <a name="supported-drivers-and-connection-strings"></a>Obsługiwane sterowniki i parametry połączenia
Usługa Azure SQL Data Warehouse obsługuje sterowniki [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] i [JDBC][JDBC]. Kliknij jeden z hello poprzedzających sterowniki toofind hello najnowszej wersji i dokumentacji. tooautomatically Generowanie ciągu połączenia hello hello sterownika, którego używasz z hello Azure portalu, możesz kliknąć hello **Pokaż parametry połączenia bazy danych** z hello poprzedzających przykład.  Poniżej przedstawiono również przykłady parametrów połączenia dla każdego sterownika.

> [!NOTE]
> Rozważ ustawienie hello połączenia limitu czasu too300 sekund tooallow toosurvive Twojego połączenia krótkich okresów niedostępności.
> 
> 

### <a name="adonet-connection-string-example"></a>Przykład parametrów połączenia sterownika ADO.NET
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Przykład parametrów połączenia sterownika ODBC
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Przykład parametrów połączenia sterownika PHP
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Przykład parametrów połączenia sterownika JDBC
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Ustawienia połączenia
Usługa SQL Data Warehouse standaryzuje niektóre ustawienia podczas tworzenia połączenia i obiektu. Tych ustawień nie można zastąpić i obejmują one:

| Ustawienia bazy danych | Wartość |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ON |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ON |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Następne kroki
tooconnect i zapytania z programem Visual Studio, zobacz [zapytania z programem Visual Studio][Query with Visual Studio]. toolearn więcej informacji na temat opcji uwierzytelniania, zobacz [tooAzure uwierzytelniania SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


