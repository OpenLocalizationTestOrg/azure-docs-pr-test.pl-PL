---
title: "dzienniki serwera dostępu i aaaConfigure PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak dostępu i tooconfigure hello do dzienników serwera w bazie danych Azure dla PostgreSQL przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="50751-103">Konfigurowanie i uzyskać dostępu do dzienników serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="50751-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="50751-104">Możesz pobrać hello PostgreSQL dzienników błędów serwera przy użyciu hello interfejsu wiersza polecenia (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="50751-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="50751-105">Dzienniki tootransaction dostępu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="50751-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="50751-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="50751-106">Prerequisites</span></span>
<span data-ttu-id="50751-107">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="50751-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="50751-108">[PostgreSQL serwera bazy danych Azure](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="50751-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="50751-109">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="50751-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="50751-110">Konfigurowanie rejestrowania w bazie danych Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="50751-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="50751-111">Można skonfigurować powitania serwera tooaccess zapytania dzienników i dzienników błędów.</span><span class="sxs-lookup"><span data-stu-id="50751-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="50751-112">Dzienniki błędów mogą zawierać informacje automatycznego próżni, połączenia i punkty kontrolne.</span><span class="sxs-lookup"><span data-stu-id="50751-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="50751-113">Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="50751-113">Turn on logging</span></span>
2. <span data-ttu-id="50751-114">Dziennik aktualizacji\_instrukcji i dziennika\_min\_czas trwania\_rejestrowanie zapytań tooenable — instrukcja</span><span class="sxs-lookup"><span data-stu-id="50751-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="50751-115">Okres przechowywania aktualizacji</span><span class="sxs-lookup"><span data-stu-id="50751-115">Update retention period</span></span>

<span data-ttu-id="50751-116">Aby uzyskać więcej informacji, zobacz [Dostosowywanie parametry konfiguracji serwera](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="50751-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="50751-117">Lista dzienników bazy danych Azure PostgreSQL serwera</span><span class="sxs-lookup"><span data-stu-id="50751-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="50751-118">pliki dziennika dostępne hello toolist dla serwera, uruchom hello [az postgres dzienniki serwera listy](/cli/azure/postgres/server-logs#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="50751-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="50751-119">Możesz wyświetlić listę plików dziennika powitania serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**i bezpośrednie jego tekstu tooa plik o nazwie **dziennika\_pliki\_lista.txt.**</span><span class="sxs-lookup"><span data-stu-id="50751-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="50751-120">Pobierz dzienniki lokalnie z serwera hello</span><span class="sxs-lookup"><span data-stu-id="50751-120">Download logs locally from hello server</span></span>
<span data-ttu-id="50751-121">Witaj [Pobierz dzienniki serwera az postgres](/cli/azure/postgres/server-logs#download) polecenie umożliwia toodownload osobnych plikach dziennika dla serwera.</span><span class="sxs-lookup"><span data-stu-id="50751-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="50751-122">W tym przykładzie pliki do pobrania hello pliku dziennika określonego serwera hello **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup** tooyour lokalnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="50751-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="50751-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="50751-123">Next steps</span></span>
- <span data-ttu-id="50751-124">toolearn więcej informacji na temat dzienniki serwera, zobacz [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="50751-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="50751-125">Aby uzyskać więcej informacji na parametry serwera, zobacz [dostosować parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="50751-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
