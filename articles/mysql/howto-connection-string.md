---
title: "Łączenie aplikacji bazy danych platformy Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera listę ciągów połączenia aktualnie obsługiwane dla aplikacji, aby połączyć się z bazą danych Azure dla programu MySQL, w tym ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python i Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="b4d1a-103">Jak połączyć aplikacje do bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="b4d1a-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="b4d1a-104">Ten dokument zawiera listę typów ciąg połączenia, które są obsługiwane przez bazę danych Azure dla programu MySQL, wraz z szablonów i przykłady.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="b4d1a-105">W ciągu połączenia może mieć różne parametry i inne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="b4d1a-106">Aby uzyskać certyfikat, zobacz [Konfigurowanie SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b4d1a-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="b4d1a-107">{your_host} = <servername>. mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="b4d1a-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="b4d1a-108">{your_user}@{servername} poprawnie = format identyfikatora użytkownika do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="b4d1a-109">Użycie tylko userID spowoduje niepowodzenia uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="b4d1a-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="b4d1a-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="b4d1a-111">W tym przykładzie nazwa serwera jest `myserver4demo`, nazwa bazy danych jest `wpdb`, nazwa użytkownika jest `WPAdmin`, a hasło to `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="b4d1a-112">Następnie powinien być ciąg połączenia:</span><span class="sxs-lookup"><span data-stu-id="b4d1a-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="b4d1a-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="b4d1a-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="b4d1a-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="b4d1a-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="b4d1a-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="b4d1a-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="b4d1a-116">PHP</span><span class="sxs-lookup"><span data-stu-id="b4d1a-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="b4d1a-117">Python</span><span class="sxs-lookup"><span data-stu-id="b4d1a-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="b4d1a-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="b4d1a-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="b4d1a-119">Pobierz szczegóły parametrów połączenia z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b4d1a-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="b4d1a-120">W [portalu Azure](https://portal.azure.com), przejdź do bazy danych Azure, aby serwer MySQL, a następnie kliknij przycisk **parametry połączenia** można pobrać listy ciągu dla swojego wystąpienia: ![okienko ciągów połączenia platformy Azure Portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="b4d1a-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="b4d1a-121">Ciąg zawiera szczegółowe informacje, takie jak sterownik, serwera i inne bazy danych parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="b4d1a-122">Zmodyfikuj te przykłady za pomocą własnych parametrów, takich jak nazwa bazy danych, hasło i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="b4d1a-123">Następnie można ten ciąg połączenia z serwerem z kodu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4d1a-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d1a-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4d1a-124">Next steps</span></span>
- <span data-ttu-id="b4d1a-125">Aby uzyskać więcej informacji na temat biblioteki połączeń, zobacz [pojęcia — bibliotek połączeń](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="b4d1a-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
