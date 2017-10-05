---
title: "Konfigurowanie i uzyskiwać dostęp do dzienników serwera dla PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania i uzyskiwać dostęp do dzienników serwera w bazie danych Azure dla PostgreSQL przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="6be05-103">Konfigurowanie i uzyskać dostępu do dzienników serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6be05-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="6be05-104">Możesz pobrać PostgreSQL dzienniki błędów serwera przy użyciu interfejsu wiersza polecenia (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="6be05-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="6be05-105">Jednak dostęp do dzienników transakcji nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="6be05-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6be05-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6be05-106">Prerequisites</span></span>
<span data-ttu-id="6be05-107">Do wykonania kroków opisanych ten przewodnik, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="6be05-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="6be05-108">[PostgreSQL serwera bazy danych Azure](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6be05-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="6be05-109">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) narzędzia wiersza polecenia lub użyj powłoki chmury Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="6be05-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="6be05-110">Konfigurowanie rejestrowania w bazie danych Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6be05-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="6be05-111">Można skonfigurować serwera dostępu do dzienników kwerend i dzienników błędów.</span><span class="sxs-lookup"><span data-stu-id="6be05-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="6be05-112">Dzienniki błędów mogą zawierać informacje automatycznego próżni, połączenia i punkty kontrolne.</span><span class="sxs-lookup"><span data-stu-id="6be05-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="6be05-113">Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="6be05-113">Turn on logging</span></span>
2. <span data-ttu-id="6be05-114">Dziennik aktualizacji\_instrukcji i dziennika\_min\_czas trwania\_instrukcji, aby włączyć rejestrowanie zapytań</span><span class="sxs-lookup"><span data-stu-id="6be05-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="6be05-115">Okres przechowywania aktualizacji</span><span class="sxs-lookup"><span data-stu-id="6be05-115">Update retention period</span></span>

<span data-ttu-id="6be05-116">Aby uzyskać więcej informacji, zobacz [Dostosowywanie parametry konfiguracji serwera](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6be05-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="6be05-117">Lista dzienników bazy danych Azure PostgreSQL serwera</span><span class="sxs-lookup"><span data-stu-id="6be05-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="6be05-118">Aby wyświetlić pliki dziennika dostępne na serwerze, uruchom [az postgres dzienniki serwera listy](/cli/azure/postgres/server-logs#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6be05-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="6be05-119">Można wyświetlić listę plików dziennika dla serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**i bezpośrednie jego tekstu w pliku o nazwie **dziennika\_pliki\_lista.txt.**</span><span class="sxs-lookup"><span data-stu-id="6be05-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="6be05-120">Pobierz dzienniki lokalnie z serwera</span><span class="sxs-lookup"><span data-stu-id="6be05-120">Download logs locally from the server</span></span>
<span data-ttu-id="6be05-121">[Pobierz dzienniki serwera az postgres](/cli/azure/postgres/server-logs#download) polecenie umożliwia pobieranie osobnych plikach dziennika dla serwera.</span><span class="sxs-lookup"><span data-stu-id="6be05-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="6be05-122">W tym przykładzie pliki do pobrania określonego pliku dziennika dla serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup** do środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6be05-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="6be05-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6be05-123">Next steps</span></span>
- <span data-ttu-id="6be05-124">Aby dowiedzieć się więcej na temat dzienniki serwera, zobacz [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="6be05-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="6be05-125">Aby uzyskać więcej informacji na parametry serwera, zobacz [dostosować parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6be05-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
