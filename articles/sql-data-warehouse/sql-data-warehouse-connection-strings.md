---
title: "aaaDrivers dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Parametry połączenia i sterowniki dla magazynu danych SQL"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 5c91f423-b550-4734-8094-c7f2c418ac8d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: a808839a8cfc49c2d7b16038c88ffb39a9f97825
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="drivers-for-azure-sql-data-warehouse"></a><span data-ttu-id="46300-103">Sterowniki dla magazynu danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="46300-103">Drivers for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="46300-104">Możesz połączyć tooSQL hurtowni danych takich jak z kilku różnych aplikacji protokołów [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP] [ PHP] i [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="46300-104">You can connect tooSQL Data Warehouse with several different application protocols such as, [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] and [JDBC][JDBC].</span></span> <span data-ttu-id="46300-105">Poniżej przedstawiono kilka przykładów ciągi połączenia dla każdego protokołu.</span><span class="sxs-lookup"><span data-stu-id="46300-105">Below are some examples of connections strings for each protocol.</span></span>  <span data-ttu-id="46300-106">Umożliwia także hello toobuild portalu Azure w ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="46300-106">You can also use hello Azure portal toobuild your connection string.</span></span>  <span data-ttu-id="46300-107">toobuild ciągu połączenia za pomocą hello portalu Azure Przejdź tooyour bloku bazy danych, w obszarze *Essentials* kliknij *Pokaż parametry połączenia bazy danych*.</span><span class="sxs-lookup"><span data-stu-id="46300-107">toobuild your connection string using hello Azure portal, navigate tooyour database blade, under *Essentials* click on *Show database connection strings*.</span></span>

## <a name="sample-adonet-connection-string"></a><span data-ttu-id="46300-108">Parametry połączenia ADO.NET próbki</span><span class="sxs-lookup"><span data-stu-id="46300-108">Sample ADO.NET connection string</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

## <a name="sample-odbc-connection-string"></a><span data-ttu-id="46300-109">Ciąg połączenia ODBC próbki</span><span class="sxs-lookup"><span data-stu-id="46300-109">Sample ODBC connection string</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

## <a name="sample-php-connection-string"></a><span data-ttu-id="46300-110">Parametry połączenia PHP próbki</span><span class="sxs-lookup"><span data-stu-id="46300-110">Sample PHP connection string</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

## <a name="sample-jdbc-connection-string"></a><span data-ttu-id="46300-111">Parametry połączenia JDBC próbki</span><span class="sxs-lookup"><span data-stu-id="46300-111">Sample JDBC connection string</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

> [!NOTE]
> <span data-ttu-id="46300-112">Rozważ ustawienie hello połączenia too300 liczba sekund limitu czasu w kolejności tooallow hello połączenia toosurvive krótkich okresach niedostępności.</span><span class="sxs-lookup"><span data-stu-id="46300-112">Consider setting hello connection timeout too300 seconds in order tooallow hello connection toosurvive short periods of  unavailability.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="46300-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="46300-113">Next steps</span></span>
<span data-ttu-id="46300-114">toostart badania magazynu danych z programu Visual Studio i innych aplikacji, zobacz [zapytania z programem Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="46300-114">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!--Image references-->

<!--Azure.com references-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx

<!--Other references-->
