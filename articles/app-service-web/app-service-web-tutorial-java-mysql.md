---
title: aaaBuild aplikacji sieci web Java i MySQL na platformie Azure
description: "Dowiedz się, jak tooget aplikacji Java łączące usługi baza danych MySQL na platformie Azure toohello pracy usługi aplikacji Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="084ad-103">Tworzenie aplikacji sieci web Java i MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="084ad-104">Ten samouczek pokazuje, jak toocreate Java sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="084ad-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="084ad-105">Po zakończeniu, konieczne będzie [Spring rozruchu](https://projects.spring.io/spring-boot/) przechowywania danych w aplikacji [bazy danych Azure dla programu MySQL](https://docs.microsoft.com/azure/mysql/overview) systemem [aplikacji sieci Web usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="084ad-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Aplikacja Java w usługi aplikacji Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="084ad-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="084ad-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="084ad-108">Utwórz bazę danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="084ad-109">Połącz toohello aplikację przykładową bazę danych</span><span class="sxs-lookup"><span data-stu-id="084ad-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="084ad-110">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="084ad-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="084ad-111">Aktualizowanie i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="084ad-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="084ad-112">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="084ad-113">Monitorowanie aplikacji hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="084ad-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="084ad-114">Prerequisites</span></span>

1. [<span data-ttu-id="084ad-115">Pobierz i zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="084ad-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="084ad-116">Pobierz i zainstaluj hello Java 7 JDK lub nowszy</span><span class="sxs-lookup"><span data-stu-id="084ad-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="084ad-117">Pobierz, zainstaluj i uruchom MySQL</span><span class="sxs-lookup"><span data-stu-id="084ad-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="084ad-118">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="084ad-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="084ad-119">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="084ad-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="084ad-120">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="084ad-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="084ad-121">Przygotowywanie lokalnej MySQL</span><span class="sxs-lookup"><span data-stu-id="084ad-121">Prepare local MySQL</span></span> 

<span data-ttu-id="084ad-122">W tym kroku utworzysz bazę danych w lokalnym serwerze MySQL do użycia w przypadku testowania aplikacji hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="084ad-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="084ad-123">Połącz serwer tooMySQL</span><span class="sxs-lookup"><span data-stu-id="084ad-123">Connect tooMySQL server</span></span>

<span data-ttu-id="084ad-124">W oknie terminalu Połącz tooyour lokalny serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="084ad-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="084ad-125">Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="084ad-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="084ad-126">Jeśli zostanie wyświetlony monit o podanie hasła, wprowadź hasło hello hello `root` konta.</span><span class="sxs-lookup"><span data-stu-id="084ad-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="084ad-127">Jeśli nie pamiętasz hasła do konta głównego, zobacz [MySQL: jak tooReset hello hasła użytkownika Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="084ad-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="084ad-128">Jeśli polecenie zostanie wykonane pomyślnie, na serwerze MySQL już jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="084ad-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="084ad-129">Jeśli nie, upewnij się, że serwera lokalnego MySQL została uruchomiona z następujących hello [MySQL poinstalacyjne czynności](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="084ad-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="084ad-130">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="084ad-130">Create a database</span></span> 

<span data-ttu-id="084ad-131">W hello `mysql` należy utworzyć bazę danych i tabeli dla hello elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="084ad-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="084ad-132">Zakończyć połączenie z serwerem, wpisując `quit`.</span><span class="sxs-lookup"><span data-stu-id="084ad-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="084ad-133">Tworzenie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="084ad-133">Create and run hello sample app</span></span> 

<span data-ttu-id="084ad-134">W tym kroku sklonować przykładowej aplikacji rozruchu Spring, skonfiguruj ją toouse hello lokalnej bazy danych MySQL i uruchom go na komputerze.</span><span class="sxs-lookup"><span data-stu-id="084ad-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="084ad-135">Przykład Witaj klonowania</span><span class="sxs-lookup"><span data-stu-id="084ad-135">Clone hello sample</span></span>

<span data-ttu-id="084ad-136">Hello okno terminalu Przejdź tooa pracy katalogu i klonowania repozytorium przykładowej hello.</span><span class="sxs-lookup"><span data-stu-id="084ad-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="084ad-137">Skonfiguruj bazę danych MySQL hello hello aplikacji toouse</span><span class="sxs-lookup"><span data-stu-id="084ad-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="084ad-138">Aktualizacja hello `spring.datasource.password` i wartość w *spring-boot-mysql-todo/src/main/resources/application.properties* z hello tego samego hasła głównego używany tooopen hello MySQL wiersz:</span><span class="sxs-lookup"><span data-stu-id="084ad-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="084ad-139">Tworzenie i uruchamianie przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="084ad-139">Build and run hello sample</span></span>

<span data-ttu-id="084ad-140">Tworzenie i uruchamianie przykładowych hello przy użyciu otoki Maven hello zawarte w repozytorium hello:</span><span class="sxs-lookup"><span data-stu-id="084ad-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="084ad-141">Otwórz toosee toohttp://localhost:8080 Twojego przeglądarki w przykładowym hello w akcji.</span><span class="sxs-lookup"><span data-stu-id="084ad-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="084ad-142">Podczas dodawania listy toohello zadań, użyj hello SQL następujące polecenia w hello MySQL monitu tooview hello danych przechowywanych w MySQL.</span><span class="sxs-lookup"><span data-stu-id="084ad-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="084ad-143">Zatrzymywanie aplikacji hello za pomocą `Ctrl` + `C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="084ad-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="084ad-144">Utwórz bazę danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="084ad-145">W tym kroku utworzysz [bazy danych Azure dla programu MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) wystąpienia przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="084ad-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="084ad-146">Należy skonfigurować hello przykładowej aplikacji toouse tej bazy danych później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="084ad-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="084ad-147">Użyj hello Azure CLI 2.0 w zasobach hello toocreate okno terminalu potrzebne toohost aplikacji Java w usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="084ad-148">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="084ad-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="084ad-149">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="084ad-149">Create a resource group</span></span>

<span data-ttu-id="084ad-150">Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="084ad-151">Grupy zasobów platformy Azure jest kontenerem logicznym, w której wdrożone i zarządzane zasoby pokrewne, takie jak aplikacje sieci web, baz danych i konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="084ad-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="084ad-152">Witaj poniższy przykład tworzy grupę zasobów w regionie Europa Północna, Europa hello:</span><span class="sxs-lookup"><span data-stu-id="084ad-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="084ad-153">toosee hello możliwe wartości można użyć dla `--location`, użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="084ad-154">Utwórz serwer MySQL</span><span class="sxs-lookup"><span data-stu-id="084ad-154">Create a MySQL server</span></span>

<span data-ttu-id="084ad-155">Utwórz serwer bazy danych Azure dla programu MySQL (wersja zapoznawcza) z hello [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="084ad-156">Podstawić własną unikatową nazwę serwera MySQL, której występuje hello `<mysql_server_name>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="084ad-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="084ad-157">Ta nazwa jest częścią nazwy hosta serwera MySQL, `<mysql_server_name>.mysql.database.azure.com`, dlatego toobe potrzebuje globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="084ad-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="084ad-158">Zamienić `<admin_user>` i `<admin_password>` z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="084ad-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="084ad-159">Po utworzeniu serwer MySQL hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="084ad-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="084ad-160">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="084ad-160">Configure server firewall</span></span>

<span data-ttu-id="084ad-161">Tworzenie reguły zapory klienta MySQL serwera tooallow połączeń przy użyciu hello [az mysql reguły zapory serwera — Utwórz](/cli/azure/mysql/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="084ad-162">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza) nie obsługuje obecnie automatycznie połączenia z usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="084ad-163">Adresy IP na platformie Azure są przypisywane dynamicznie, jest lepsze tooenable wszystkie adresy IP dla teraz.</span><span class="sxs-lookup"><span data-stu-id="084ad-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="084ad-164">Jak usługa hello kontynuuje jej podgląd, lepiej metody zabezpieczania bazy danych zostanie włączona.</span><span class="sxs-lookup"><span data-stu-id="084ad-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="084ad-165">Skonfiguruj bazę danych MySQL na platformie Azure hello</span><span class="sxs-lookup"><span data-stu-id="084ad-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="084ad-166">W hello okno terminalu na komputerze nawiąż połączenie toohello serwer MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="084ad-167">Użyj wartości hello wcześniej określona dla `<admin_user>` i `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="084ad-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="084ad-168">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="084ad-168">Create a database</span></span> 

<span data-ttu-id="084ad-169">W hello `mysql` należy utworzyć bazę danych i tabeli dla hello elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="084ad-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="084ad-170">Utwórz użytkownika z uprawnieniami</span><span class="sxs-lookup"><span data-stu-id="084ad-170">Create a user with permissions</span></span>

<span data-ttu-id="084ad-171">Tworzenie użytkownika bazy danych i nadaj mu wszystkie uprawnienia w hello `tododb` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="084ad-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="084ad-172">Zastąp symbole zastępcze hello `<Javaapp_user>` i `<Javaapp_password>` z własnych unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="084ad-173">Zakończyć połączenie z serwerem, wpisując `quit`.</span><span class="sxs-lookup"><span data-stu-id="084ad-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="084ad-174">Wdrażanie hello próbki tooAzure usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="084ad-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="084ad-175">Tworzenie planu usługi aplikacji Azure z hello **wolne** przy użyciu hello warstwy cenowej [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="084ad-176">planu usług aplikacji Hello definiuje hello toohost fizyczne zasoby używane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="084ad-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="084ad-177">Wszystkie aplikacje przypisane planu usług aplikacji tooan udostępniania tych zasobów, umożliwiając koszt toosave odnośnie do hostowania wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="084ad-178">Jeśli hello plan jest gotowy, powitalne interfejsu wiersza polecenia Azure zawiera podobne dane wyjściowe toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="084ad-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="084ad-179">Tworzenie aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-179">Create an Azure Web app</span></span>

 <span data-ttu-id="084ad-180">Użyj hello [tworzenie aplikacji sieci Web az](/cli/azure/appservice/web#create) toocreate polecenia interfejsu wiersza polecenia definicję aplikacji sieci web w hello `myAppServicePlan` planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="084ad-181">definicję aplikacji sieci web Hello zapewnia tooaccess adres URL aplikacji przy użyciu i konfiguruje kilka opcji toodeploy Twojego tooAzure kodu.</span><span class="sxs-lookup"><span data-stu-id="084ad-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="084ad-182">SUBSTITUTE hello `<app_name>` symbol zastępczy własne unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="084ad-183">Ta nazwa jest część hello domyślna nazwa domeny dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="084ad-184">Przed udostępnieniem jej tooyour użytkowników, możesz mapować aplikacji sieci web toohello wpis nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="084ad-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="084ad-185">Podczas definiowania aplikacji sieci web hello jest gotowy, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="084ad-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="084ad-186">Konfigurowanie języka Java</span><span class="sxs-lookup"><span data-stu-id="084ad-186">Configure Java</span></span> 

<span data-ttu-id="084ad-187">Skonfigurować hello Java runtime wymagające aplikacji z hello [aktualizacja konfiguracji sieci web appservice az](/cli/azure/appservice/web/config#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="084ad-188">Witaj następujące polecenie konfiguruje toorun aplikacji sieci web hello na ostatnie JDK 8 Java i [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="084ad-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="084ad-189">Konfigurowanie bazy danych Azure SQL hello toouse aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="084ad-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="084ad-190">Przed uruchomieniem hello Przykładowa aplikacja, ustawienia aplikacji na powitania sieci web aplikacji toouse hello Azure baza danych MySQL utworzonej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="084ad-191">Te właściwości są uwidocznione toohello aplikacji sieci web jako zmienne środowiskowe i Zastąp wartości hello application.properties hello wewnątrz aplikacji sieci web spakowanych hello.</span><span class="sxs-lookup"><span data-stu-id="084ad-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="084ad-192">Ustawienia aplikacji przy użyciu [appsettings konfiguracji aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) w hello interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="084ad-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="084ad-193">Uzyskiwanie poświadczeń wdrożenia FTP</span><span class="sxs-lookup"><span data-stu-id="084ad-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="084ad-194">Można wdrożyć z appservice tooAzure aplikacji na różne sposoby, w tym FTP, lokalne Git GitHub, Visual Studio Team Services i BitBucket.</span><span class="sxs-lookup"><span data-stu-id="084ad-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="084ad-195">W tym przykładzie FTP toodeploy hello. Plik WAR utworzony wcześniej na tooAzure Twojego komputera lokalnego usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="084ad-196">toodetermine co toopass wzdłuż w ftp polecenia toohello aplikacji sieci Web, Użyj poświadczeń [az usługi aplikacji sieci web wdrożenia listy publikowania — profile](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) polecenia:</span><span class="sxs-lookup"><span data-stu-id="084ad-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="084ad-197">Przekaż aplikację hello za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="084ad-197">Upload hello app using FTP</span></span>

<span data-ttu-id="084ad-198">Użyj ulubionego hello toodeploy narzędzia FTP. Toohello pliku WAR */site/wwwroot/webapps* folderu na pobrane z hello adres serwera hello `URL` w hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="084ad-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="084ad-199">Usuń istniejący katalog domyślny (ROOT) aplikacji hello i Zastąp istniejące ROOT.war z hello hello. Wbudowane hello wcześniej w samouczku hello pliku WAR.</span><span class="sxs-lookup"><span data-stu-id="084ad-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="084ad-200">Przetestuj aplikację sieci web hello</span><span class="sxs-lookup"><span data-stu-id="084ad-200">Test hello web app</span></span>

<span data-ttu-id="084ad-201">Przeglądaj zbyt`http://<app_name>.azurewebsites.net/` i dodaj kilka zadań toohello listy.</span><span class="sxs-lookup"><span data-stu-id="084ad-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Aplikacja Java w usługi aplikacji Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="084ad-203">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="084ad-203">**Congratulations!**</span></span> <span data-ttu-id="084ad-204">Używasz aplikacji Java opartych na danych w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="084ad-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="084ad-205">Aktualizacja aplikacji hello i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="084ad-205">Update hello app and redeploy</span></span>

<span data-ttu-id="084ad-206">Zaktualizuj tooinclude aplikacji hello dodatkowe kolumny na liście todo powitania dla elementu hello dzień został utworzony.</span><span class="sxs-lookup"><span data-stu-id="084ad-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="084ad-207">Spring rozruchu obsługuje aktualizacji schematu bazy danych hello automatycznie jako zmianami modelu danych hello bez zmiany istniejącego rekordy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="084ad-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="084ad-208">W systemie lokalnym otwarcie *src/main/java/com/example/fabrikam/TodoItem.java* i dodaj następujące hello importuje toohello klasy:</span><span class="sxs-lookup"><span data-stu-id="084ad-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="084ad-209">Dodaj `String` właściwości `timeCreated` za*src/main/java/com/example/fabrikam/TodoItem.java*, inicjowanie go z sygnaturą czasową podczas tworzenia obiektu.</span><span class="sxs-lookup"><span data-stu-id="084ad-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="084ad-210">Dodaj metody pobierające/ustawiające hello nowe `timeCreated` właściwości podczas edytowania tego pliku.</span><span class="sxs-lookup"><span data-stu-id="084ad-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="084ad-211">Aktualizacja *src/main/java/com/example/fabrikam/TodoDemoController.java* o wiersz w hello `updateTodo` sygnatury czasowej hello tooset metody:</span><span class="sxs-lookup"><span data-stu-id="084ad-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="084ad-212">Dodaj obsługę nowego pola hello hello Thymeleaf szablonu.</span><span class="sxs-lookup"><span data-stu-id="084ad-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="084ad-213">Aktualizacja *src/main/resources/templates/index.html* z użyciem nowego nagłówka tabeli sygnatury czasowej hello i nową wartość hello toodisplay pola sygnatury czasowej hello w każdym wierszu danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="084ad-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="084ad-214">Odbuduj aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="084ad-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="084ad-215">Zaktualizowano hello FTP. WAR jako przed, usunięcie istniejących hello */wwwroot/webapps/katalogu głównego witryny* katalogu i *ROOT.war*, a następnie przekazać zaktualizowany hello. Plik WAR jako ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="084ad-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="084ad-216">Podczas odświeżania aplikacji hello **tworzony** kolumny jest teraz widoczne.</span><span class="sxs-lookup"><span data-stu-id="084ad-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="084ad-217">Po dodaniu nowego zadania aplikacji hello zostanie automatycznie wypełnić hello sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="084ad-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="084ad-218">Istniejących zadań pozostają bez zmian i korzystanie z aplikacji hello, mimo że hello podstawowy model danych został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="084ad-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Zaktualizowane o nową kolumnę aplikacji Java](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="084ad-220">Dzienniki diagnostyczne strumienia</span><span class="sxs-lookup"><span data-stu-id="084ad-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="084ad-221">Podczas wykonywania aplikacji Java w usłudze Azure App Service można uzyskać konsoli hello dzienniki przetwarzana potokowo bezpośrednio tooyour terminala.</span><span class="sxs-lookup"><span data-stu-id="084ad-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="084ad-222">W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="084ad-223">Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/appservice/web/log#tail) polecenia.</span><span class="sxs-lookup"><span data-stu-id="084ad-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="084ad-224">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-224">Manage your Azure web app</span></span>

<span data-ttu-id="084ad-225">Przejdź aplikacji sieci web hello toosee portalu Azure toohello, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="084ad-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="084ad-226">toodo, zaloguj się za[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="084ad-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="084ad-227">W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="084ad-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="084ad-229">Domyślnie bloku aplikacji sieci web zawiera hello **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="084ad-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="084ad-230">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="084ad-231">W tym miejscu mogą też wykonywać zadania zarządzania, takie jak zatrzymanie, start, ponowne uruchomienie i usuwania.</span><span class="sxs-lookup"><span data-stu-id="084ad-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="084ad-232">Hello karty po lewej stronie powitania bloku hello zawierają hello innej konfiguracji stron, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="084ad-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="084ad-234">Te karty w bloku hello zawierają hello wiele aplikacji sieci web tooyour można dodać funkcje.</span><span class="sxs-lookup"><span data-stu-id="084ad-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="084ad-235">powitania po liście oferuje kilka możliwości hello:</span><span class="sxs-lookup"><span data-stu-id="084ad-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="084ad-236">Mapowanie niestandardowej nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="084ad-236">Map a custom DNS name</span></span>
* <span data-ttu-id="084ad-237">Tworzenie powiązania niestandardowego certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="084ad-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="084ad-238">Konfigurowanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="084ad-238">Configure continuous deployment</span></span>
* <span data-ttu-id="084ad-239">Skalowanie w górę i w dół</span><span class="sxs-lookup"><span data-stu-id="084ad-239">Scale up and out</span></span>
* <span data-ttu-id="084ad-240">Dodawanie uwierzytelniania użytkownika</span><span class="sxs-lookup"><span data-stu-id="084ad-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="084ad-241">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="084ad-241">Clean up resources</span></span>

<span data-ttu-id="084ad-242">Jeśli nie potrzebujesz tych zasobów innym samouczek (zobacz [następne kroki](#next)), można je usunąć, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="084ad-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="084ad-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="084ad-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="084ad-244">Utwórz bazę danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="084ad-245">Połącz próbki toohello aplikacji Java MySQL</span><span class="sxs-lookup"><span data-stu-id="084ad-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="084ad-246">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="084ad-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="084ad-247">Aktualizowanie i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="084ad-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="084ad-248">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="084ad-249">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="084ad-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="084ad-250">Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="084ad-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="084ad-251">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="084ad-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
