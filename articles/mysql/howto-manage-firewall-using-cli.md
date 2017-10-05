---
title: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="02a5f-103">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="02a5f-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="02a5f-104">Reguły zapory poziomu serwera umożliwiają administratorom zarządzanie dostępem do bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="02a5f-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="02a5f-105">Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, możesz utworzyć, zaktualizować, Usuń listę i Pokaż reguły zapory do zarządzania serwerem.</span><span class="sxs-lookup"><span data-stu-id="02a5f-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="02a5f-106">Omówienie bazy danych Azure dla zapór MySQL, zobacz [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="02a5f-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02a5f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="02a5f-107">Prerequisites</span></span>
* [<span data-ttu-id="02a5f-108">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="02a5f-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="02a5f-109">Zainstaluj Azure Python SDK dla usługi MySQL i PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="02a5f-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="02a5f-110">Zainstaluj składnik wiersza polecenia platformy Azure dla usług PostgreSQL i MySQL</span><span class="sxs-lookup"><span data-stu-id="02a5f-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="02a5f-111">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="02a5f-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="02a5f-112">Polecenia reguły zapory:</span><span class="sxs-lookup"><span data-stu-id="02a5f-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="02a5f-113">**Az mysql reguły zapory serwera-** polecenie służy do tworzenia, usuwania, listy, Pokaż i zaktualizować reguł zapory z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a5f-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="02a5f-114">Polecenia:</span><span class="sxs-lookup"><span data-stu-id="02a5f-114">Commands:</span></span>
- <span data-ttu-id="02a5f-115">**Utwórz**: Tworzenie reguły zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="02a5f-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a5f-116">**Usuń**: Usuń regułę zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="02a5f-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a5f-117">**Lista** : lista reguł zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="02a5f-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="02a5f-118">**Pokaż** : Pokaż szczegóły serwera Azure MySQL reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="02a5f-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a5f-119">**Zaktualizuj**: aktualizowanie reguły zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="02a5f-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="02a5f-120">Logowanie do platformy Azure i listy Azure bazy danych dla serwerów MySQL</span><span class="sxs-lookup"><span data-stu-id="02a5f-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="02a5f-121">Bezpieczne łączenie wiersza polecenia platformy Azure z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a5f-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="02a5f-122">Użyj **logowania az** polecenie, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="02a5f-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="02a5f-123">W wierszu polecenia uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="02a5f-124">To polecenie zwróci kod, którego należy użyć w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="02a5f-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="02a5f-125">W przeglądarce sieci Web otwórz stronę [https://aka.ms/devicelogin](https://aka.ms/devicelogin) i wprowadź kod.</span><span class="sxs-lookup"><span data-stu-id="02a5f-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="02a5f-126">Po wyświetleniu monitu zaloguj się przy użyciu swoich poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a5f-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="02a5f-127">Autoryzowany logowanie listę subskrypcji będą wypisywane w konsoli.</span><span class="sxs-lookup"><span data-stu-id="02a5f-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="02a5f-128">Skopiuj identyfikator żądanego subskrypcji można ustawić bieżącej subskrypcji do użycia przenoszenie do przodu.</span><span class="sxs-lookup"><span data-stu-id="02a5f-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="02a5f-129">Lista baz danych Azure, serwerów MySQL dla Twojej subskrypcji i grupie zasobów, jeśli nie wiesz o nazwach.</span><span class="sxs-lookup"><span data-stu-id="02a5f-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="02a5f-130">Należy pamiętać, atrybut nazwy na liście, która będzie używana do określenia, który serwer MySQL do pracy w.</span><span class="sxs-lookup"><span data-stu-id="02a5f-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="02a5f-131">Jeśli to konieczne, Potwierdź szczegóły dla tego serwera, aby upewnić się, czy nazwa jest prawidłowa przy użyciu atrybutu name:</span><span class="sxs-lookup"><span data-stu-id="02a5f-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a5f-132">Lista reguł zapory na Azure bazy danych MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="02a5f-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="02a5f-133">Przy użyciu nazwy serwera i nazwa grupy zasobów, Wyświetl listę istniejących reguł zapory serwera na serwerze.</span><span class="sxs-lookup"><span data-stu-id="02a5f-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="02a5f-134">Należy zauważyć, że nazwa serwera jest określony w **--server** przełącznika i nie **— nazwa** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="02a5f-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="02a5f-135">Dane wyjściowe wyświetli listę reguł, jeśli istnieje domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="02a5f-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="02a5f-136">Można użyć przełącznika **--tabeli wyników** dla bardziej czytelnym formacie tabeli jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="02a5f-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a5f-137">Tworzenie reguły zapory na Azure bazy danych MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="02a5f-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a5f-138">Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, Utwórz nową regułę zapory na serwerze.</span><span class="sxs-lookup"><span data-stu-id="02a5f-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="02a5f-139">Podaj nazwę reguły, ustawiony początkowy adres IP i końcowemu adresowi IP reguły, aby pokryć zakres adresów IP zezwolić na dostęp.</span><span class="sxs-lookup"><span data-stu-id="02a5f-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="02a5f-140">Dla pojedynczej adresu IP zezwolić na dostęp Podaj ten sam adres Start IP i End IP, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="02a5f-141">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały utworzone, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="02a5f-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="02a5f-142">W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a5f-143">Aktualizuj reguły zapory w bazie danych Azure MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="02a5f-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="02a5f-144">Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, zaktualizuj istniejącą regułę zapory na serwerze.</span><span class="sxs-lookup"><span data-stu-id="02a5f-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="02a5f-145">Podaj nazwę istniejącej reguły zapory jako dane wejściowe i uruchom atrybutów IP adresów IP i końcowy do aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="02a5f-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="02a5f-146">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="02a5f-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="02a5f-147">W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="02a5f-148">Jeśli reguły zapory nie istnieje, zostanie utworzony za pomocą polecenia aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="02a5f-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a5f-149">Pokaż szczegóły reguły zapory w bazie danych systemu Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="02a5f-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a5f-150">Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, Pokaż szczegóły reguły z serwera istniejącą zapory.</span><span class="sxs-lookup"><span data-stu-id="02a5f-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="02a5f-151">Podaj nazwę istniejącej reguły zapory jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="02a5f-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="02a5f-152">Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, który został określony, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="02a5f-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="02a5f-153">W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a5f-154">Usuwanie reguły zapory w bazie danych Azure MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="02a5f-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a5f-155">Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, usuń istniejącą regułę zapory z serwera.</span><span class="sxs-lookup"><span data-stu-id="02a5f-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="02a5f-156">Podaj nazwę istniejącej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="02a5f-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="02a5f-157">Na sukces nie ma żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="02a5f-157">Upon success, there is no output.</span></span> <span data-ttu-id="02a5f-158">W przypadku awarii zostanie zwrócony tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="02a5f-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02a5f-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02a5f-159">Next steps</span></span>
- <span data-ttu-id="02a5f-160">Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="02a5f-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="02a5f-161">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="02a5f-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
