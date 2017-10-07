---
title: "toosecurely łączności SSL aaaConfigure połączyć tooAzure bazy danych MySQL | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące sposobu tooproperly konfigurowania Azure bazy danych MySQL i toocorrectly skojarzonych aplikacji używać połączeń SSL"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Konfigurowanie protokołu SSL łączność w sieci toosecurely aplikacji połączyć tooAzure bazy danych MySQL
Bazy danych platformy Azure dla programu MySQL obsługuje połączenie bazy danych Azure dla aplikacji tooclient serwera MySQL przy użyciu protokołu Secure Sockets Layer (SSL). Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.

## <a name="step-1-obtain-ssl-certificate"></a>Krok 1: Uzyskiwanie certyfikatu SSL
Pobierz hello toocommunicate potrzebnego certyfikatu za pośrednictwem protokołu SSL z bazy danych Azure, aby serwer MySQL z [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) i Zapisz tooyour pliku certyfikatu hello lokalnego dysku (z tego samouczka użyliśmy c:\ssl).
**Programu Microsoft Internet Explorer oraz Microsoft Edge:** po zakończeniu pobierania hello, Zmień nazwę hello tooBaltimoreCyberTrustRoot.crt.pem certyfikatu.

## <a name="step-2-bind-ssl"></a>Krok 2: Powiązanie SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Łączenie tooserver przy użyciu hello MySQL Workbench za pośrednictwem protokołu SSL
Skonfiguruj tooconnect MySQL Workbench bezpiecznie za pośrednictwem protokołu SSL. Przejdź toohello **SSL** kartę w hello MySQL Workbench na powitania dialogu instalacji nowego połączenia. Wprowadź lokalizację pliku hello hello **BaltimoreCyberTrustRoot.crt.pem** w hello **pliku urząd certyfikacji SSL:** pola.
![Zapisz niestandardowe kafelka](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Łączenie tooserver przy użyciu interfejsu wiersza polecenia MySQL hello za pośrednictwem protokołu SSL
Przy użyciu interfejsu wiersza polecenia MySQL hello, wykonaj następujące polecenie hello:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Krok 3: Wymuszanie połączeń SSL na platformie Azure 
### <a name="using-azure-portal"></a>Korzystanie z witryny Azure Portal
Przy użyciu hello portalu Azure, odwiedź witrynę Azure bazy danych MySQL serwer i kliknij przycisk **zabezpieczenia połączeń**. Użyj tooenable przycisk przełączania hello lub wyłącz hello **połączenia SSL wymusić** ustawienie. Następnie kliknij przycisk **Save** (Zapisz). Firma Microsoft zaleca włączyć tooalways **połączenia SSL wymusić** ustawienie w celu zwiększenia bezpieczeństwa.
![Włącz ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Korzystanie z interfejsu wiersza polecenia platformy Azure
Można włączyć lub wyłączyć hello **wymuszania ssl** parametr przy użyciu wartości włączone lub wyłączone odpowiednio w wiersza polecenia platformy Azure.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Krok 4: Sprawdź połączenia SSL
Wykonanie hello mysql **stan** tooverify polecenia, że nawiązano połączenie przy użyciu protokołu SSL serwera MySQL tooyour:
```dos
mysql> status
```
Potwierdź, że hello połączenie jest szyfrowane, przeglądając hello danych wyjściowych. Powinny być widoczne: **SSL: szyfrowania używany jest algorytm SHA AES256** 

## <a name="sample-code"></a>Przykładowy kod
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Następne kroki
Przegląd różnych opcji łączności aplikacji po [biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)
