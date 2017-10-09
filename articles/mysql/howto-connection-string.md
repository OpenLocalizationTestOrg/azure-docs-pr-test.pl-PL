---
title: aaaConnect tooAzure aplikacji bazy danych dla programu MySQL | Dokumentacja firmy Microsoft
description: "Ten dokument zawiera listę hello aktualnie obsługiwane parametry połączenia dla tooconnect aplikacje z bazą danych Azure dla programu MySQL, w tym ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python i Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Jak tooconnect tooAzure aplikacji bazy danych MySQL
Ten dokument zawiera listę hello połączenia ciąg typów, które są obsługiwane przez bazę danych Azure dla programu MySQL, wraz z szablonów i przykłady. W ciągu połączenia może mieć różne parametry i inne ustawienia.

- tooobtain hello certyfikatu, zobacz [jak tooconfigure SSL](./howto-configure-ssl.md).
- {your_host} = <servername>. mysql.database.azure.com
- {your_user}@{servername} poprawnie = format identyfikatora użytkownika do uwierzytelniania.  Użycie tylko hello userID spowoduje hello toofail uwierzytelniania.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

W tym przykładzie nazwa serwera hello jest `myserver4demo`, nazwa bazy danych jest `wpdb`, nazwa użytkownika jest `WPAdmin`, a hasło to `mypassword!2`. Następnie należy hello parametry połączenia:

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

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Pobierz szczegóły parametrów połączenia hello z hello portalu Azure
W hello [portalu Azure](https://portal.azure.com), przejdź tooyour Azure bazy danych MySQL serwera, a następnie kliknij przycisk **parametry połączenia** tooget ciągu listy wystąpienia: ![okienko ciągów połączenia hello hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)

ciąg Hello zawiera szczegółowe informacje, takie jak sterownik hello, serwera i inne parametry połączenia bazy danych. Zmodyfikuj te przykłady za pomocą własnych parametrów, takich jak nazwa bazy danych, hasło i tak dalej. Następnie można użyć tego ciągu tooconnect toohello serwera z kodu i aplikacji.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat biblioteki połączeń, zobacz [pojęcia — bibliotek połączeń](./concepts-connection-libraries.md).
