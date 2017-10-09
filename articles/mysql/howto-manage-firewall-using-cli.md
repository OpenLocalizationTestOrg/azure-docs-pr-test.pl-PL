---
title: "aaaCreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="40456-103">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="40456-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="40456-104">Reguły zapory poziomu serwera włączyć tooan dostępu toomanage administratorów bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="40456-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="40456-105">Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, można utworzyć, zaktualizować, Usuń, listy i Pokaż toomanage reguł zapory serwera.</span><span class="sxs-lookup"><span data-stu-id="40456-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="40456-106">Omówienie bazy danych Azure dla zapór MySQL, zobacz [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="40456-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40456-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40456-107">Prerequisites</span></span>
* [<span data-ttu-id="40456-108">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="40456-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="40456-109">Zainstaluj Azure Python SDK dla usługi MySQL i PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="40456-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="40456-110">Zainstaluj składnik Azure CLI hello usług PostgreSQL i MySQL</span><span class="sxs-lookup"><span data-stu-id="40456-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="40456-111">Tworzenie serwera usługi Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="40456-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="40456-112">Polecenia reguły zapory:</span><span class="sxs-lookup"><span data-stu-id="40456-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="40456-113">Witaj **az mysql reguły zapory serwera-** używane jest polecenie z wiersza polecenia platformy Azure toocreate, usunąć listy, wyświetlanie i aktualizowanie reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="40456-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="40456-114">Polecenia:</span><span class="sxs-lookup"><span data-stu-id="40456-114">Commands:</span></span>
- <span data-ttu-id="40456-115">**Utwórz**: Tworzenie reguły zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="40456-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="40456-116">**Usuń**: Usuń regułę zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="40456-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="40456-117">**Lista** : lista reguł zapory serwera Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="40456-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="40456-118">**Pokaż** : Pokaż szczegóły powitania serwera Azure MySQL reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="40456-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="40456-119">**Zaktualizuj**: aktualizowanie reguły zapory serwera Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="40456-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="40456-120">TooAzure logowania i listy bazy danych Azure, serwerów MySQL</span><span class="sxs-lookup"><span data-stu-id="40456-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="40456-121">Bezpieczne łączenie wiersza polecenia platformy Azure z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40456-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="40456-122">Użyj hello **logowania az** to polecenie toodo.</span><span class="sxs-lookup"><span data-stu-id="40456-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="40456-123">Uruchom następujące polecenie z wiersza polecenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="40456-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="40456-124">Toouse kodu, w następnym kroku hello będzie danych wyjściowych tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="40456-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="40456-125">Użyj strony hello tooopen przeglądarki sieci web [https://aka.ms/devicelogin](https://aka.ms/devicelogin) i wprowadź kod hello.</span><span class="sxs-lookup"><span data-stu-id="40456-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="40456-126">W wierszu hello Zaloguj się przy użyciu poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40456-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="40456-127">Logowanie jest autoryzowany, w konsoli hello są drukowane listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="40456-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="40456-128">Skopiuj identyfikator hello hello potrzeby subskrypcji tooset hello bieżącej subskrypcji toobe używane przenoszenie do przodu.</span><span class="sxs-lookup"><span data-stu-id="40456-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="40456-129">Lista hello baz danych Azure, serwerów MySQL dla Twojej subskrypcji i grupie zasobów, w razie wątpliwości hello nazw.</span><span class="sxs-lookup"><span data-stu-id="40456-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="40456-130">Należy pamiętać, atrybut nazwy hello w hello wyświetlania, która będzie używana toospecify toowork serwera MySQL, które na.</span><span class="sxs-lookup"><span data-stu-id="40456-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="40456-131">Jeśli to konieczne, potwierdź hello szczegóły dla tego serwera toousing hello nazwa atrybutu tooconfirm nazwa jest prawidłowa:</span><span class="sxs-lookup"><span data-stu-id="40456-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="40456-132">Lista reguł zapory na Azure bazy danych MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="40456-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="40456-133">Przy użyciu hello nazwę serwera i nazwa grupy zasobów hello, listy hello istniejących reguł zapory serwera na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="40456-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="40456-134">Zwróć uwagę, ten atrybut nazwy serwera hello jest określona w hello **— serwer** przełącznika i nie hello **— nazwa** przełącznika.</span><span class="sxs-lookup"><span data-stu-id="40456-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="40456-135">dane wyjściowe Hello znajduje się lista hello reguły formatowania żadnego domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="40456-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="40456-136">Można użyć przełącznika hello **--tabeli wyników** dla bardziej czytelnym formacie tabeli jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="40456-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="40456-137">Tworzenie reguły zapory na Azure bazy danych MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="40456-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="40456-138">Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, Utwórz nową regułę zapory na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="40456-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="40456-139">Podaj nazwę reguły hello hello ustawiony początkowy adres IP i końcowemu adresowi IP dla hello toocover reguły dostępu tooallow adresów zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="40456-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="40456-140">Dla pojedynczej adresów IP toobe zezwolenie na dostęp, podaj hello tego samego adresu, jak hello Start adresów IP i końcowemu adresowi IP, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="40456-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="40456-141">Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały utworzone, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="40456-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="40456-142">W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="40456-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="40456-143">Aktualizuj reguły zapory w bazie danych Azure MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="40456-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="40456-144">Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, zaktualizuj istniejącą regułę zapory na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="40456-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="40456-145">Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe i hello start adresów IP i końcowy IP atrybutów tooupdate.</span><span class="sxs-lookup"><span data-stu-id="40456-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="40456-146">Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="40456-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="40456-147">W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="40456-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="40456-148">Jeśli reguły zapory hello nie istnieje, zostanie utworzony przez polecenie aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="40456-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="40456-149">Pokaż szczegóły reguły zapory w bazie danych systemu Azure dla serwera MySQL</span><span class="sxs-lookup"><span data-stu-id="40456-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="40456-150">Przy użyciu nazwy serwera Azure MySQL hello i nazwa grupy zasobów hello, zawierają hello istniejących zapory reguły szczegóły z serwera hello.</span><span class="sxs-lookup"><span data-stu-id="40456-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="40456-151">Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="40456-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="40456-152">Na sukces dane wyjściowe polecenia hello znajduje się lista szczegółów hello hello reguły zapory, który został określony, domyślnie w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="40456-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="40456-153">W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="40456-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="40456-154">Usuwanie reguły zapory w bazie danych Azure MySQL serwera</span><span class="sxs-lookup"><span data-stu-id="40456-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="40456-155">Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, usuń istniejącą regułę zapory z powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="40456-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="40456-156">Podaj nazwę hello hello istniejącej reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="40456-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="40456-157">Na sukces nie ma żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="40456-157">Upon success, there is no output.</span></span> <span data-ttu-id="40456-158">W przypadku awarii zostanie zwrócony tekst komunikatu o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="40456-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40456-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40456-159">Next steps</span></span>
- <span data-ttu-id="40456-160">Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="40456-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="40456-161">Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="40456-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
