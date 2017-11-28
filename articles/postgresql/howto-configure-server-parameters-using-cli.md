---
title: "Parametry usługi hello aaaConfigure w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello usługi parametrów w bazie danych Azure przy użyciu PostgreSQL hello wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="1c8c1-103">Dostosuj parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1c8c1-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="1c8c1-104">Można wyświetlić listę, wyświetlić i zaktualizować parametry konfiguracji serwera Azure PostgreSQL przy użyciu hello interfejsu wiersza polecenia (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="1c8c1-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="1c8c1-105">Jednak tylko podzbiór aparatu konfiguracji są narażone na poziomie serwera i może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1c8c1-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1c8c1-106">Prerequisites</span></span>
<span data-ttu-id="1c8c1-107">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="1c8c1-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="1c8c1-108">Serwer i bazę danych [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="1c8c1-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="1c8c1-109">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="1c8c1-110">Lista parametrów konfiguracji serwera dla bazy danych Azure PostgreSQL serwera</span><span class="sxs-lookup"><span data-stu-id="1c8c1-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="1c8c1-111">Uruchom wszystkie parametry można modyfikować w serwerze i ich wartości toolist hello [az postgres serwera konfiguracji na liście](/cli/azure/postgres/server/configuration#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="1c8c1-112">Możesz wyświetlić listę hello parametry konfiguracji serwera dla serwera hello **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="1c8c1-113">Pokaż szczegóły parametru konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="1c8c1-113">Show server configuration parameter details</span></span>
<span data-ttu-id="1c8c1-114">Szczegóły tooshow parametr określoną konfigurację serwera, uruchom hello [az postgres serwera konfiguracji Pokaż](/cli/azure/postgres/server/configuration#show) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="1c8c1-115">W tym przykładzie przedstawiono szczegóły hello **dziennika\_min\_wiadomości** parametru konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w obszarze Grupa zasobów **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="1c8c1-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="1c8c1-116">Zmodyfikuj wartość parametru konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="1c8c1-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="1c8c1-117">Można również zmodyfikować wartość hello niektórych parametru konfiguracji serwera i spowoduje to zaktualizowanie hello podstawowej konfiguracji wartość hello PostgreSQL serwera aparatu.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="1c8c1-118">tooupdate hello konfiguracji Użyj hello [zestawu konfiguracji serwera postgres az](/cli/azure/postgres/server/configuration#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="1c8c1-119">tooupdate hello **dziennika\_min\_wiadomości** parametru konfiguracji serwera serwera **mypgserver 20170401.postgres.database.azure.com** wgrupiezasobów**myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="1c8c1-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="1c8c1-120">Jeśli tooreset hello wartość parametru konfiguracji, po prostu wybierz tooleave limit hello opcjonalne `--value` parametr, a usługa hello zastosuje hello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="1c8c1-121">W powyżej przykład jego wygląd:</span><span class="sxs-lookup"><span data-stu-id="1c8c1-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="1c8c1-122">Spowoduje to zresetowanie hello **dziennika\_min\_wiadomości** wartości domyślnej konfiguracji toohello **ostrzeżenie**.</span><span class="sxs-lookup"><span data-stu-id="1c8c1-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="1c8c1-123">Aby uzyskać szczegółowe informacje o konfiguracji serwera i dopuszczalne wartości, zobacz dokumentację PostgreSQL [konfiguracji serwera](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="1c8c1-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c8c1-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c8c1-124">Next steps</span></span>
- <span data-ttu-id="1c8c1-125">Zobacz dzienniki serwera tooconfigure i dostępu, [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="1c8c1-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
