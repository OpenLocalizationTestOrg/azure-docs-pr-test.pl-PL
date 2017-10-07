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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="ad027-103">Konfigurowanie protokołu SSL łączność w sieci toosecurely aplikacji połączyć tooAzure bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="ad027-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="ad027-104">Bazy danych platformy Azure dla programu MySQL obsługuje połączenie bazy danych Azure dla aplikacji tooclient serwera MySQL przy użyciu protokołu Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="ad027-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="ad027-105">Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="ad027-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="ad027-106">Krok 1: Uzyskiwanie certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="ad027-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="ad027-107">Pobierz hello toocommunicate potrzebnego certyfikatu za pośrednictwem protokołu SSL z bazy danych Azure, aby serwer MySQL z [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) i Zapisz tooyour pliku certyfikatu hello lokalnego dysku (z tego samouczka użyliśmy c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="ad027-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="ad027-108">**Programu Microsoft Internet Explorer oraz Microsoft Edge:** po zakończeniu pobierania hello, Zmień nazwę hello tooBaltimoreCyberTrustRoot.crt.pem certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ad027-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="ad027-109">Krok 2: Powiązanie SSL</span><span class="sxs-lookup"><span data-stu-id="ad027-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="ad027-110">Łączenie tooserver przy użyciu hello MySQL Workbench za pośrednictwem protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="ad027-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="ad027-111">Skonfiguruj tooconnect MySQL Workbench bezpiecznie za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="ad027-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="ad027-112">Przejdź toohello **SSL** kartę w hello MySQL Workbench na powitania dialogu instalacji nowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="ad027-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="ad027-113">Wprowadź lokalizację pliku hello hello **BaltimoreCyberTrustRoot.crt.pem** w hello **pliku urząd certyfikacji SSL:** pola.</span><span class="sxs-lookup"><span data-stu-id="ad027-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="ad027-114">![Zapisz niestandardowe kafelka](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="ad027-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="ad027-115">Łączenie tooserver przy użyciu interfejsu wiersza polecenia MySQL hello za pośrednictwem protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="ad027-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="ad027-116">Przy użyciu interfejsu wiersza polecenia MySQL hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ad027-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="ad027-117">Krok 3: Wymuszanie połączeń SSL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ad027-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="ad027-118">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ad027-118">Using Azure portal</span></span>
<span data-ttu-id="ad027-119">Przy użyciu hello portalu Azure, odwiedź witrynę Azure bazy danych MySQL serwer i kliknij przycisk **zabezpieczenia połączeń**.</span><span class="sxs-lookup"><span data-stu-id="ad027-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="ad027-120">Użyj tooenable przycisk przełączania hello lub wyłącz hello **połączenia SSL wymusić** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="ad027-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="ad027-121">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="ad027-121">Then click **Save**.</span></span> <span data-ttu-id="ad027-122">Firma Microsoft zaleca włączyć tooalways **połączenia SSL wymusić** ustawienie w celu zwiększenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="ad027-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="ad027-123">![Włącz ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="ad027-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="ad027-124">Korzystanie z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ad027-124">Using Azure CLI</span></span>
<span data-ttu-id="ad027-125">Można włączyć lub wyłączyć hello **wymuszania ssl** parametr przy użyciu wartości włączone lub wyłączone odpowiednio w wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad027-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="ad027-126">Krok 4: Sprawdź połączenia SSL</span><span class="sxs-lookup"><span data-stu-id="ad027-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="ad027-127">Wykonanie hello mysql **stan** tooverify polecenia, że nawiązano połączenie przy użyciu protokołu SSL serwera MySQL tooyour:</span><span class="sxs-lookup"><span data-stu-id="ad027-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="ad027-128">Potwierdź, że hello połączenie jest szyfrowane, przeglądając hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ad027-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="ad027-129">Powinny być widoczne: **SSL: szyfrowania używany jest algorytm SHA AES256**</span><span class="sxs-lookup"><span data-stu-id="ad027-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="ad027-130">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="ad027-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="ad027-131">PHP</span><span class="sxs-lookup"><span data-stu-id="ad027-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="ad027-132">Python</span><span class="sxs-lookup"><span data-stu-id="ad027-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="ad027-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad027-133">Next steps</span></span>
<span data-ttu-id="ad027-134">Przegląd różnych opcji łączności aplikacji po [biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ad027-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
