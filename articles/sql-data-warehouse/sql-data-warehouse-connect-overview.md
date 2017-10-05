---
title: "Nawiązywanie połączenia z usługą Azure SQL Data Warehouse | Microsoft Docs"
description: "Jak znaleźć nazwę serwera i parametry połączenia dla usługi Azure SQL Data Warehouse"
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
ms.openlocfilehash: 72c2b404e66611da421eca0dc30aa71e18c6d120
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="a997c-103">Nawiązywanie połączenia z usługą Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a997c-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a997c-104">W tym artykule opisano, jak nawiązać połączenie z usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a997c-104">This article helps you get connected to SQL Data Warehouse for the first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="a997c-105">Znajdowanie nazwy serwera</span><span class="sxs-lookup"><span data-stu-id="a997c-105">Find your server name</span></span>
<span data-ttu-id="a997c-106">Pierwszym krokiem do nawiązania połączenia z usługą SQL Data Warehouse jest wiedza, jak znaleźć nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="a997c-106">The first step to connecting to SQL Data Warehouse is knowing how to find your server name.</span></span>  <span data-ttu-id="a997c-107">Na przykład w poniższym przykładzie nazwa serwera to sample.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="a997c-107">For example, the server name in the following example is sample.database.windows.net.</span></span> <span data-ttu-id="a997c-108">Aby znaleźć w pełni kwalifikowaną nazwę serwera:</span><span class="sxs-lookup"><span data-stu-id="a997c-108">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="a997c-109">Przejdź do witryny [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a997c-109">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a997c-110">Kliknij pozycję **Bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="a997c-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="a997c-111">Kliknij bazę danych, z którą chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="a997c-111">Click on the database you want to connect to.</span></span>
4. <span data-ttu-id="a997c-112">Znajdź pełną nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="a997c-112">Locate the full server name.</span></span>
   
    ![Pełna nazwa serwera][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="a997c-114">Obsługiwane sterowniki i parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="a997c-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="a997c-115">Usługa Azure SQL Data Warehouse obsługuje sterowniki [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] i [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="a997c-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="a997c-116">Kliknij jeden z powyższych sterowników, aby znaleźć najnowszą wersję i dokumentację.</span><span class="sxs-lookup"><span data-stu-id="a997c-116">Click on one of the preceding drivers to find the latest version and documentation.</span></span> <span data-ttu-id="a997c-117">Aby automatycznie wygenerować parametry połączenia dla używanego sterownika z poziomu witryny Azure Portal, można kliknąć pozycję **Pokaż parametry połączenia bazy danych** z poprzedniego przykładu.</span><span class="sxs-lookup"><span data-stu-id="a997c-117">To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.</span></span>  <span data-ttu-id="a997c-118">Poniżej przedstawiono również przykłady parametrów połączenia dla każdego sterownika.</span><span class="sxs-lookup"><span data-stu-id="a997c-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="a997c-119">Rozważ ustawienie limitu czasu połączenia na wartość 300 sekund, aby połączenie nie zostało zakończone mimo krótkich okresów niedostępności.</span><span class="sxs-lookup"><span data-stu-id="a997c-119">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="a997c-120">Przykład parametrów połączenia sterownika ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a997c-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="a997c-121">Przykład parametrów połączenia sterownika ODBC</span><span class="sxs-lookup"><span data-stu-id="a997c-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="a997c-122">Przykład parametrów połączenia sterownika PHP</span><span class="sxs-lookup"><span data-stu-id="a997c-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="a997c-123">Przykład parametrów połączenia sterownika JDBC</span><span class="sxs-lookup"><span data-stu-id="a997c-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="a997c-124">Ustawienia połączenia</span><span class="sxs-lookup"><span data-stu-id="a997c-124">Connection settings</span></span>
<span data-ttu-id="a997c-125">Usługa SQL Data Warehouse standaryzuje niektóre ustawienia podczas tworzenia połączenia i obiektu.</span><span class="sxs-lookup"><span data-stu-id="a997c-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="a997c-126">Tych ustawień nie można zastąpić i obejmują one:</span><span class="sxs-lookup"><span data-stu-id="a997c-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="a997c-127">Ustawienia bazy danych</span><span class="sxs-lookup"><span data-stu-id="a997c-127">Database Setting</span></span> | <span data-ttu-id="a997c-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="a997c-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="a997c-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="a997c-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="a997c-130">ON</span><span class="sxs-lookup"><span data-stu-id="a997c-130">ON</span></span> |
| <span data-ttu-id="a997c-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="a997c-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="a997c-132">ON</span><span class="sxs-lookup"><span data-stu-id="a997c-132">ON</span></span> |
| <span data-ttu-id="a997c-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="a997c-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="a997c-134">mdy</span><span class="sxs-lookup"><span data-stu-id="a997c-134">mdy</span></span> |
| <span data-ttu-id="a997c-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="a997c-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="a997c-136">7</span><span class="sxs-lookup"><span data-stu-id="a997c-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a997c-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a997c-137">Next steps</span></span>
<span data-ttu-id="a997c-138">Aby nawiązać połączenie i rozpocząć tworzenie zapytań przy użyciu programu Visual Studio, zobacz artykuł [Query with Visual Studio][Query with Visual Studio] (Wykonywanie zapytań przy użyciu programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="a997c-138">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="a997c-139">Aby dowiedzieć się więcej na temat opcji uwierzytelniania, zobacz [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse] (Uwierzytelnianie w usłudze Azure SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="a997c-139">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

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


