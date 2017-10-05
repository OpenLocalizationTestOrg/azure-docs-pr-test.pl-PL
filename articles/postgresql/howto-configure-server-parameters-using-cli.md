---
title: "Skonfiguruj parametry usługi w bazie danych Azure dla PostgreSQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak skonfigurować parametry usługi w bazie danych Azure dla PostgreSQL przy użyciu wiersza polecenia wiersza polecenia platformy Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="2f066-103">Dostosuj parametry konfiguracji serwera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2f066-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="2f066-104">Można wyświetlić listę, wyświetlić i zaktualizować parametry konfiguracji serwera Azure PostgreSQL przy użyciu interfejsu wiersza polecenia (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="2f066-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="2f066-105">Jednak tylko podzbiór aparatu konfiguracji są narażone na poziomie serwera i może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="2f066-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2f066-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f066-106">Prerequisites</span></span>
<span data-ttu-id="2f066-107">Do wykonania kroków opisanych ten przewodnik, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="2f066-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="2f066-108">Serwer i bazę danych [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2f066-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="2f066-109">Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) narzędzia wiersza polecenia lub użyć powłoki chmury Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="2f066-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="2f066-110">Lista parametrów konfiguracji serwera dla bazy danych Azure PostgreSQL serwera</span><span class="sxs-lookup"><span data-stu-id="2f066-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="2f066-111">Aby wyświetlić listę wszystkich parametrów można modyfikować w serwerze i ich wartości, należy uruchomić [az postgres serwera konfiguracji na liście](/cli/azure/postgres/server/configuration#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2f066-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="2f066-112">Można wyświetlić parametry konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="2f066-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="2f066-113">Pokaż szczegóły parametru konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="2f066-113">Show server configuration parameter details</span></span>
<span data-ttu-id="2f066-114">Aby wyświetlić szczegółowe informacje dotyczące parametru określoną konfigurację serwera, uruchom [az postgres serwera konfiguracji Pokaż](/cli/azure/postgres/server/configuration#show) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2f066-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="2f066-115">W tym przykładzie przedstawiono szczegóły **dziennika\_min\_wiadomości** parametru konfiguracji serwera dla serwera **mypgserver 20170401.postgres.database.azure.com** w obszarze Grupa zasobów **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="2f066-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="2f066-116">Zmodyfikuj wartość parametru konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="2f066-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="2f066-117">Można również zmodyfikować wartość niektórych parametru konfiguracji serwera i spowoduje to zaktualizowanie odpowiednia wartość konfiguracji dla aparatu serwera PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f066-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="2f066-118">Aby zaktualizować Użyj konfiguracji [zestawu konfiguracji serwera postgres az](/cli/azure/postgres/server/configuration#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2f066-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="2f066-119">Aby zaktualizować **dziennika\_min\_wiadomości** parametru konfiguracji serwera serwera **mypgserver 20170401.postgres.database.azure.com** w grupie zasobów **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="2f066-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="2f066-120">Jeśli chcesz zresetować wartość parametru konfiguracji, po prostu chcesz Opuść opcjonalny `--value` parametr i usługi będą stosowane wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="2f066-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="2f066-121">W powyżej przykład jego wygląd:</span><span class="sxs-lookup"><span data-stu-id="2f066-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="2f066-122">Spowoduje to zresetowanie **dziennika\_min\_wiadomości** konfiguracji przy użyciu wartości domyślnej **ostrzeżenie**.</span><span class="sxs-lookup"><span data-stu-id="2f066-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="2f066-123">Aby uzyskać szczegółowe informacje o konfiguracji serwera i dopuszczalne wartości, zobacz dokumentację PostgreSQL [konfiguracji serwera](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="2f066-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f066-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f066-124">Next steps</span></span>
- <span data-ttu-id="2f066-125">Aby skonfigurować i uzyskać dostępu do dzienników serwera, zobacz [dzienniki serwera w bazie danych PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="2f066-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
