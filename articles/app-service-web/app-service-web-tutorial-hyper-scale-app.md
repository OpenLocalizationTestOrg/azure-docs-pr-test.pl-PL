---
title: Tworzenie aplikacji hiperskali na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać różnych usług platformy Azure w celu zwiększenia wydajności aplikacji platformy ASP.NET na platformie Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="ce6c5-103">Tworzenie aplikacji sieci web w hiperskali na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="ce6c5-104">W tym samouczku przedstawiono sposób skalowanie aplikacji sieci web platformy ASP.NET na platformie Azure, aby zmaksymalizować żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="ce6c5-105">Przed rozpoczęciem tego samouczka, upewnij się, że [wiersza polecenia platformy Azure jest instalowany](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="ce6c5-106">Ponadto należy [programu Visual Studio](https://www.visualstudio.com/vs/) na komputerze lokalnym, aby uruchomić przykładową aplikację.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="ce6c5-107">Krok 1 - Get przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="ce6c5-108">Ten krok służy do konfigurowania lokalnego projektu programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="ce6c5-109">Klonuj repozytorium aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-109">Clone the application repository</span></span>

<span data-ttu-id="ce6c5-110">Otwórz wybrany terminal wiersza polecenia dowolnego i `CD` do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="ce6c5-111">Następnie uruchom następujące polecenia, można sklonować przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="ce6c5-112">Uruchom przykładową aplikację w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce6c5-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="ce6c5-113">Otwórz rozwiązanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="ce6c5-114">Typ `F5` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="ce6c5-115">Tej przykładowej aplikacji sieci web ASP.NET pochodzi z domyślnego szablonu i będzie się powtarzał użytkownika sesji i używa pamięci podręcznej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="ce6c5-116">Spójrz na `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="ce6c5-117">`Index()` Metoda dodaje element danych do sesji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="ce6c5-118">I `About()` i `Contact()` ich dane wyjściowe pamięci podręcznej metody.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="ce6c5-119">Krok 2 — wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="ce6c5-120">W tym kroku możesz utworzyć aplikację sieci web platformy Azure i wdrażać przykładowej aplikacji ASP.NET do niego.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="ce6c5-121">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="ce6c5-121">Create a resource group</span></span>   
<span data-ttu-id="ce6c5-122">Użyj [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) utworzyć [grupy zasobów](../azure-resource-manager/resource-group-overview.md) w regionie, Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="ce6c5-123">Grupa zasobów to, gdzie umieścić wszystkie zasoby platformy Azure, które mają być zarządzane, takie jak zaplecza aplikacji sieci web i wszystkie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="ce6c5-124">Aby sprawdzić, jakie możliwe wartości można użyć dla `---location`, użyj [appservice az listy lokalizacje](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="ce6c5-125">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="ce6c5-125">Create an App Service plan</span></span>
<span data-ttu-id="ce6c5-126">Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) można utworzyć "B1" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="ce6c5-127">Plan usługi aplikacji jest jednostki skalowania, która może zawierać dowolną liczbę aplikacji, które chcesz skalować w górę lub się ze sobą za pośrednictwem tej samej infrastruktury usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="ce6c5-128">Każdy plan jest również przypisany [warstwy cenowej](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="ce6c5-129">Wyższych warstw obejmują lepsze sprzętu i więcej funkcji, takich jak więcej wystąpień skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="ce6c5-130">W tym samouczku B1 jest minimalna warstwę, która umożliwia skalowanie w poziomie do wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="ce6c5-131">Zawsze przejściem aplikację w górę lub w dół warstwy cenowej później, uruchamiając [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="ce6c5-132">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="ce6c5-132">Create a web app</span></span>
<span data-ttu-id="ce6c5-133">Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) do utworzenia aplikacji sieci web o unikatowej nazwie w `$appName`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="ce6c5-134">Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ce6c5-134">Set deployment credentials</span></span>
<span data-ttu-id="ce6c5-135">Użyj [az usługi aplikacji sieci web wdrożenia użytkownika zestaw](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) można ustawić poświadczenia wdrażania na poziomie konta usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="ce6c5-136">Konfigurowanie wdrożenia Git</span><span class="sxs-lookup"><span data-stu-id="ce6c5-136">Configure Git deployment</span></span>
<span data-ttu-id="ce6c5-137">Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) do konfigurowania lokalnego wdrożenia usługi Git.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="ce6c5-138">To polecenie umożliwia wyjścia, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ce6c5-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="ce6c5-139">Umożliwia skonfigurowanie programu Git zdalnego zwrócony adres URL.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="ce6c5-140">Polecenie używa w poprzednim przykładzie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="ce6c5-141">Wdrażanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-141">Deploy the sample application</span></span>
<span data-ttu-id="ce6c5-142">Teraz można przystąpić do wdrażania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="ce6c5-143">Uruchom polecenie `git push`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="ce6c5-144">Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="ce6c5-145">Przejdź do aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-145">Browse to Azure web app</span></span>
<span data-ttu-id="ce6c5-146">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Aby wyświetlić aplikację działającą na platformie Azure, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="ce6c5-147">Krok 3 — nawiązać połączenia z pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="ce6c5-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="ce6c5-148">W tym kroku możesz skonfigurować pamięć podręczna Redis Azure jako zewnętrznych, wspólnie przechowywane pamięci podręcznej do aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="ce6c5-149">Może szybko korzystać z pamięci podręcznej Redis do buforowania danych wyjściowych strony.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="ce6c5-150">Ponadto, gdy użytkownik skalowanie aplikacji sieci web później, Redis pomaga utrwalić sesje użytkowników na wielu wystąpień niezawodnie.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="ce6c5-151">Tworzenie usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ce6c5-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="ce6c5-152">Użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) Tworzenie pamięci podręcznej Redis Azure i zapisać w formacie JSON dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="ce6c5-153">Użyj unikatowej nazwy w `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="ce6c5-154">Konfigurowanie aplikacji do korzystania z pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="ce6c5-154">Configure the application to use Redis</span></span>
<span data-ttu-id="ce6c5-155">Format ciągu połączenia dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="ce6c5-156">Drugi wiersz powinien zapewnić wyjścia, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ce6c5-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="ce6c5-157">W programie Visual Studio, Utwórz plik konfiguracji sieci web w katalogu głównym projektu o nazwie `redis.config` i wklej następujący kod do niego.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="ce6c5-158">W `value`, użyj parametrów połączenia z danych wyjściowych programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="ce6c5-159">Jeśli przyjrzymy się `.gitignore` plik w repozytorium Git, zobaczysz, że ten plik jest wyłączone z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="ce6c5-160">W ten sposób poufne informacje były bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="ce6c5-161">Otwórz `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-161">Open `Web.config`.</span></span> <span data-ttu-id="ce6c5-162">Powiadomienie `<appSettings file="redis.config">` element, który pobiera ustawienie utworzony w `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="ce6c5-163">Znajdź sekcję komentarze, która obejmuje `<sessionState>` i `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="ce6c5-164">Usuń znaczniki komentarza w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="ce6c5-165">Ten kod wyszukuje ciąg połączenia Redis zdefiniowanego w `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="ce6c5-166">Teraz aplikacja używa Redis do zarządzania sesjami i buforowania.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="ce6c5-167">Typ `F5` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-167">Type `F5` to run the application.</span></span> <span data-ttu-id="ce6c5-168">Jeśli chcesz możesz pobrać klienta zarządzania Redis do wizualizacji danych, które są teraz zapisywane w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="ce6c5-169">Konfigurowanie parametrów połączenia na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="ce6c5-170">Aby aplikacja działa na platformie Azure należy skonfigurować te same parametry połączenia Redis w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="ce6c5-171">Ponieważ `redis.config` nie są przechowywane w kontroli źródła, nie są wdrażane na platformie Azure, po uruchomieniu wdrożenia usługi Git.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="ce6c5-172">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) Aby dodać parametry połączenia o tej samej nazwie (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="ce6c5-173">AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $connstring"--name $appName — myResourceGroup grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="ce6c5-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="ce6c5-174">Należy pamiętać, że `$connstring` zawiera ciąg sformatowany połączenia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="ce6c5-175">Należy ponownie wdrożyć aplikację na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="ce6c5-176">Wypchnij zmiany na platformie Azure przy użyciu poleceń Git</span><span class="sxs-lookup"><span data-stu-id="ce6c5-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="ce6c5-177">Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="ce6c5-178">Przejdź do aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ce6c5-178">Browse to the Azure web app</span></span>
<span data-ttu-id="ce6c5-179">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) w celu wyświetlenia zmian na żywo na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="ce6c5-180">Krok 4 — Skaluj do wielu wystąpień</span><span class="sxs-lookup"><span data-stu-id="ce6c5-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="ce6c5-181">Plan usługi aplikacji jest jednostką skalowania dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="ce6c5-182">Do skalowania aplikacji sieci web, skalowanie planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="ce6c5-183">Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) do skalowania w poziomie plan usługi aplikacji do wystąpienia, który jest maksymalną liczbę dozwoloną przez warstwę cenową B1.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="ce6c5-184">Należy pamiętać, że B1 jest warstwę cenową wybraną podczas tworzenia planu usługi aplikacji wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="ce6c5-185">Krok 5 — skali geograficznie</span><span class="sxs-lookup"><span data-stu-id="ce6c5-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="ce6c5-186">Skalowanie geograficznie, możesz uruchomić aplikację w wielu regionach chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="ce6c5-187">Ten Instalator zrównoważenie obciążenia aplikacji dalsze oparte na lokalizacji geograficznej i zmniejsza czas odpowiedzi, umieszczając aplikację bliżej do przeglądarki klienta.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="ce6c5-188">W tym kroku można skalować aplikacji sieci web ASP.NET w regionie drugi z [usługi Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="ce6c5-189">Po zakończeniu tego kroku będziesz mieć aplikację sieci web uruchomione w Europie zachodnie (już utworzone) i aplikacji sieci web uruchomionych w Azji Południowo-Wschodnia (jeszcze nie utworzono).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="ce6c5-190">Obie aplikacje zostanie wyświetlona z tego samego adresu URL Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="ce6c5-191">Skalowanie w górę Europy aplikacji w warstwie Standard</span><span class="sxs-lookup"><span data-stu-id="ce6c5-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="ce6c5-192">W usłudze App Service Integracja z usługą Azure Traffic Manager wymaga warstwy cenowej standardowa.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="ce6c5-193">Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) na skalowanie w górę aby S1 plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="ce6c5-194">Tworzenie profilu usługi Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ce6c5-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="ce6c5-195">Użyj [Tworzenie profilu Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) do tworzenia profilu usługi Traffic Manager i dodać go do tej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="ce6c5-196">Użyj unikatowej nazwy DNS w $dnsName.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="ce6c5-197">`--routing-method Performance`Określa, że ten profil [kieruje ruchem użytkownika do najbliższego punktu końcowego](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="ce6c5-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="ce6c5-198">Pobierz identyfikator zasobu aplikacji Europy</span><span class="sxs-lookup"><span data-stu-id="ce6c5-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="ce6c5-199">Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) można uzyskać Identyfikatora zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="ce6c5-200">Dodawanie punktu końcowego Menedżera ruchu dla Europy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="ce6c5-201">Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) Dodawanie punktu końcowego profilu Menedżera ruchu i użycie identyfikator zasobu aplikacji sieci web jako element docelowy.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="ce6c5-202">Pobierz adres URL punktu końcowego Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="ce6c5-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="ce6c5-203">Profil Menedżera ruchu ma teraz punktu końcowego, który wskazuje istniejącą aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="ce6c5-204">Użyj [Pokaż profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) można pobrać adresu URL.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="ce6c5-205">Skopiuj dane wyjściowe w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-205">Copy the output into your browser.</span></span> <span data-ttu-id="ce6c5-206">Aplikacja sieci web powinno zostać wyświetlone ponownie.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="ce6c5-207">Tworzenie pamięci podręcznej Azure Redis w Azji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="ce6c5-208">Teraz Replikowanie aplikacji sieci web platformy Azure dla regionu Azja południowo-wschodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="ce6c5-209">Aby rozpocząć, należy użyć [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) utworzyć drugi pamięć podręczna Redis Azure w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="ce6c5-210">Ta pamięć podręczna musi być wspólnie przechowywane z aplikacją w Azji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="ce6c5-211">`--name $cacheName-asia`zawiera nazwę pamięci podręcznej Europa Zachodnia pamięci podręcznej z `-asia` sufiks.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="ce6c5-212">Tworzenie planu usługi App Service w Azji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="ce6c5-213">Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) można utworzyć planu usługi aplikacji — druga regionu Azja południowo-wschodnia, przy użyciu tej samej warstwie S1 jako plan Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="ce6c5-214">Tworzenie aplikacji sieci web w Azji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-214">Create a web app in Asia</span></span>
<span data-ttu-id="ce6c5-215">Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) utworzyć drugi aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="ce6c5-216">`--name $appName-asia`zawiera nazwę aplikacji Europa Zachodnia aplikacji z `-asia` sufiks.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="ce6c5-217">Konfigurowanie parametrów połączenia dla pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="ce6c5-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="ce6c5-218">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) można dodać do aplikacji sieci web, ciąg połączenia dla pamięci podręcznej Azja południowo-wschodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="ce6c5-219">AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $($redis.hostname): $($redis.sslPort), hasło = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False"--name $appName — Azja--myResourceGroup grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="ce6c5-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="ce6c5-220">Konfiguruj wdrożenie Git dla aplikacji Azji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="ce6c5-221">Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) do skonfigurowania lokalnego wdrożenia Git dla drugiego aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="ce6c5-222">To polecenie umożliwia wyjścia, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ce6c5-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="ce6c5-223">Umożliwia skonfigurowanie zdalnego dla lokalnego repozytorium Git drugi zwrócony adres URL.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="ce6c5-224">Polecenie używa w poprzednim przykładzie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="ce6c5-225">Wdrażanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-225">Deploy your sample application</span></span>
<span data-ttu-id="ce6c5-226">Uruchom `git push` Aby wdrożyć aplikację przykładową, do drugiego zdalny narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="ce6c5-227">Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="ce6c5-228">Przejdź do aplikacji Azja</span><span class="sxs-lookup"><span data-stu-id="ce6c5-228">Browse to the Asia app</span></span>
<span data-ttu-id="ce6c5-229">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Aby sprawdzić, czy aplikacja działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="ce6c5-230">Pobierz identyfikator zasobu aplikacji Azja</span><span class="sxs-lookup"><span data-stu-id="ce6c5-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="ce6c5-231">Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) można uzyskać Identyfikatora zasobów aplikacji sieci web w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="ce6c5-232">Dodawanie punktu końcowego Menedżera ruchu, Azja aplikacji</span><span class="sxs-lookup"><span data-stu-id="ce6c5-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="ce6c5-233">Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) można dodać drugiego punktu końcowego profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="ce6c5-234">Dodaj identyfikator regionu do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ce6c5-234">Add region identifier to web apps</span></span>
<span data-ttu-id="ce6c5-235">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) można dodać zmienną środowiskową określonego regionu.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="ce6c5-236">Kod aplikacji już używa tego ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="ce6c5-237">Spójrz na `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="ce6c5-238">Zakończenie!</span><span class="sxs-lookup"><span data-stu-id="ce6c5-238">Complete!</span></span>

<span data-ttu-id="ce6c5-239">Teraz spróbuj uzyskać dostęp adres URL profilu Menedżera ruchu z przeglądarek w różnych regionach geograficznych.</span><span class="sxs-lookup"><span data-stu-id="ce6c5-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="ce6c5-240">Przeglądarka klienta z Europy powinny być widoczne "Europa Zachodnia ASP.NET" i "Azja południowo-wschodnia ASP.NET." powinny być widoczne w przeglądarce klienta z Azja</span><span class="sxs-lookup"><span data-stu-id="ce6c5-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="ce6c5-241">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="ce6c5-241">More resources</span></span>
