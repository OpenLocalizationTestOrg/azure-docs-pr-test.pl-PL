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
ms.date: 09/15/2017
ms.openlocfilehash: c9fe0a892bd5e81d2b33987b6ca55ec753550a01
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a>Jak połączyć aplikacje do bazy danych Azure dla programu MySQL
Ten temat zawiera listę typów ciąg połączenia, które są obsługiwane przez bazę danych Azure dla programu MySQL, wraz z szablonów i przykłady. W ciągu połączenia może mieć różne parametry i ustawienia.

- Aby uzyskać certyfikat, zobacz [Konfigurowanie SSL](./howto-configure-ssl.md).
- {your_host} = <servername>. mysql.database.azure.com
- {your_user}@{servername} poprawnie = format identyfikatora użytkownika do uwierzytelniania.  Jeśli używasz tylko identyfikator userID, uwierzytelnianie nie powiedzie się.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

W tym przykładzie nazwa serwera jest `myserver4demo`, nazwa bazy danych jest `wpdb`, nazwa użytkownika jest `WPAdmin`, a hasło to `mypassword!2`. W związku z tym powinien być ciąg połączenia:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a>Pobierz szczegóły parametrów połączenia z portalu Azure
W [portalu Azure](https://portal.azure.com), przejdź do bazy danych Azure, aby serwer MySQL, a następnie kliknij przycisk **parametry połączenia** można pobrać listy ciągu dla swojego wystąpienia: ![okienko ciągów połączenia platformy Azure Portal](./media/howto-connection-strings/connection-strings-on-portal.png)

Ciąg zawiera szczegółowe informacje, takie jak sterownik, serwera i inne bazy danych parametry połączenia. Zmodyfikuj te przykłady własne parametry, takie jak nazwa bazy danych, hasło i tak dalej. Następnie można ten ciąg połączenia z serwerem z kodu i aplikacji.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat biblioteki połączeń, zobacz [pojęcia — bibliotek połączeń](./concepts-connection-libraries.md).
