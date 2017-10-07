---
title: aaaBuild hiperskali aplikacji na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomaximize różnych usług Azure toouse hello wydajności aplikacji platformy ASP.NET na platformie Azure."
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
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="3c042-103">Tworzenie aplikacji sieci web w hiperskali na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3c042-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="3c042-104">Ten samouczek pokazuje, jak żądania tooscale limit aplikacji sieci web platformy ASP.NET w Azure toomaximize użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c042-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="3c042-105">Przed rozpoczęciem tego samouczka, upewnij się, że [hello wiersza polecenia platformy Azure jest instalowany](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3c042-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="3c042-106">Ponadto należy [programu Visual Studio](https://www.visualstudio.com/vs/) na komputerze lokalnym toorun hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="3c042-107">Krok 1 - Get przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="3c042-108">Ten krok służy do konfigurowania projektu programu ASP.NET lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="3c042-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="3c042-109">Repozytorium aplikacji hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="3c042-109">Clone hello application repository</span></span>

<span data-ttu-id="3c042-110">Witaj Otwórz terminal wiersza polecenia dowolnego i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="3c042-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="3c042-111">Następnie hello uruchom następujące polecenia tooclone hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="3c042-112">Uruchom hello przykładowej aplikacji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c042-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="3c042-113">Otwórz rozwiązanie hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c042-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="3c042-114">Typ `F5` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="3c042-115">Tej przykładowej aplikacji sieci web ASP.NET pochodzi z hello domyślny szablon i będzie się powtarzał użytkownika sesji i używa hello wyjściowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3c042-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="3c042-116">Spójrz na `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="3c042-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="3c042-117">Witaj `Index()` metoda dodaje część danych toohello sesji.</span><span class="sxs-lookup"><span data-stu-id="3c042-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="3c042-118">I hello `About()` i `Contact()` ich dane wyjściowe pamięci podręcznej metody.</span><span class="sxs-lookup"><span data-stu-id="3c042-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="3c042-119">Krok 2 — wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="3c042-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="3c042-120">W tym kroku możesz utworzyć aplikację sieci web platformy Azure i wdrażać tooit aplikacji ASP.NET z przykładowych.</span><span class="sxs-lookup"><span data-stu-id="3c042-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="3c042-121">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3c042-121">Create a resource group</span></span>   
<span data-ttu-id="3c042-122">Użyj [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) toocreate [grupy zasobów](../azure-resource-manager/resource-group-overview.md) w regionie Europy Zachodniej hello.</span><span class="sxs-lookup"><span data-stu-id="3c042-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="3c042-123">Grupa zasobów to, gdzie możesz umieścić wszystkie hello zasobów platformy Azure, które mają toomanage ze sobą, takie jak zaplecza hello aplikacji sieci web i wszystkie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3c042-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="3c042-124">toosee jakie możliwe wartości można użyć dla `---location`, użyj hello [appservice az listy lokalizacje](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) polecenia.</span><span class="sxs-lookup"><span data-stu-id="3c042-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="3c042-125">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3c042-125">Create an App Service plan</span></span>
<span data-ttu-id="3c042-126">Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c042-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="3c042-127">Plan usługi aplikacji jest jednostki skalowania, która może zawierać dowolną liczbę aplikacje mają tooscale w górę, lub limit razem w hello sam infrastruktury usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="3c042-128">Każdy plan jest również przypisany [warstwy cenowej](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="3c042-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="3c042-129">Wyższych warstw obejmują lepsze sprzętu i więcej funkcji, takich jak więcej wystąpień skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="3c042-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="3c042-130">W tym samouczku B1 jest hello minimalna warstwy, która umożliwia skalowanie w poziomie toothree wystąpień.</span><span class="sxs-lookup"><span data-stu-id="3c042-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="3c042-131">Aplikację można zawsze przeniesienie w górę lub w dół hello warstwy cenowej później, uruchamiając [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="3c042-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="3c042-132">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="3c042-132">Create a web app</span></span>
<span data-ttu-id="3c042-133">Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate aplikacji sieci web o unikatowej nazwie w `$appName`.</span><span class="sxs-lookup"><span data-stu-id="3c042-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="3c042-134">Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3c042-134">Set deployment credentials</span></span>
<span data-ttu-id="3c042-135">Użyj [az usługi aplikacji sieci web wdrożenia użytkownika zestaw](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset wdrożenia poziomie konta poświadczeń dla usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="3c042-136">Konfigurowanie wdrożenia Git</span><span class="sxs-lookup"><span data-stu-id="3c042-136">Configure Git deployment</span></span>
<span data-ttu-id="3c042-137">Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokalnego wdrożenia usługi Git.</span><span class="sxs-lookup"><span data-stu-id="3c042-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="3c042-138">To polecenie umożliwia skorzystanie z danych wyjściowych, która wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="3c042-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="3c042-139">Użyj hello zwrócił tooconfigure adresu URL programu Git zdalnego.</span><span class="sxs-lookup"><span data-stu-id="3c042-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="3c042-140">Witaj następujące polecenie używa hello poprzedzających przykład danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3c042-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="3c042-141">Wdrażanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-141">Deploy hello sample application</span></span>
<span data-ttu-id="3c042-142">Użytkownik jest teraz gotowy toodeploy przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="3c042-143">Uruchom polecenie `git push`.</span><span class="sxs-lookup"><span data-stu-id="3c042-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="3c042-144">Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="3c042-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="3c042-145">Przeglądaj tooAzure aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="3c042-145">Browse tooAzure web app</span></span>
<span data-ttu-id="3c042-146">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee aplikację działającą na platformie Azure, uruchom to polecenie.</span><span class="sxs-lookup"><span data-stu-id="3c042-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="3c042-147">Krok 3 — Połącz tooRedis</span><span class="sxs-lookup"><span data-stu-id="3c042-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="3c042-148">W tym kroku można skonfigurować pamięć podręczna Redis Azure jako aplikacja sieci web platformy Azure tooyour zewnętrznych, wspólnie przechowywane pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3c042-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="3c042-149">Redis toocache można szybko wykorzystywać dane wyjściowe strony.</span><span class="sxs-lookup"><span data-stu-id="3c042-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="3c042-150">Ponadto, gdy użytkownik skalowanie aplikacji sieci web później, Redis pomaga utrwalić sesje użytkowników na wielu wystąpień niezawodnie.</span><span class="sxs-lookup"><span data-stu-id="3c042-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="3c042-151">Tworzenie usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="3c042-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="3c042-152">Użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) pamięci podręcznej Redis Azure toocreate i Zapisz hello dane wyjściowe JSON.</span><span class="sxs-lookup"><span data-stu-id="3c042-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="3c042-153">Użyj unikatowej nazwy w `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="3c042-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="3c042-154">Skonfiguruj toouse aplikacji hello Redis</span><span class="sxs-lookup"><span data-stu-id="3c042-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="3c042-155">Format hello parametry połączenia dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3c042-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="3c042-156">drugi wiersz Hello powinien zapewnić wyjścia, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3c042-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="3c042-157">W programie Visual Studio, Utwórz plik konfiguracji sieci web w katalogu głównym projektu o nazwie `redis.config` i Wklej hello następującego kodu do niego.</span><span class="sxs-lookup"><span data-stu-id="3c042-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="3c042-158">W `value`, użyj parametrów połączenia hello z hello dane wyjściowe programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c042-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="3c042-159">Jeśli przyjrzymy się hello `.gitignore` plik w repozytorium Git, zobaczysz, że ten plik jest wyłączone z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="3c042-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="3c042-160">W ten sposób poufne informacje były bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="3c042-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="3c042-161">Otwórz `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="3c042-161">Open `Web.config`.</span></span> <span data-ttu-id="3c042-162">Powiadomienie hello `<appSettings file="redis.config">` element, który pobiera ustawienie hello utworzony w `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="3c042-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="3c042-163">Znajdź hello oznaczone jako sekcja zawierająca `<sessionState>` i `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="3c042-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="3c042-164">Usuń znaczniki komentarza w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="3c042-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="3c042-165">Ten kod wyszukuje ciąg połączenia Redis hello zdefiniowanego w `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="3c042-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="3c042-166">Teraz aplikacja korzysta z pamięci podręcznej Redis toomanage sesji i buforowania.</span><span class="sxs-lookup"><span data-stu-id="3c042-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="3c042-167">Typ `F5` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="3c042-168">Jeśli chcesz możesz pobrać Redis zarządzania klienta toovisualize hello danych zapisywanych teraz toohello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3c042-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="3c042-169">Konfigurowanie parametrów połączenia hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3c042-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="3c042-170">Dla twojej aplikacji toowork na platformie Azure, trzeba tooconfigure hello tych samych parametrach połączenia Redis w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="3c042-171">Ponieważ `redis.config` nie są przechowywane w kontroli źródła, nie jest wdrożony tooAzure po uruchomieniu wdrożenia usługi Git.</span><span class="sxs-lookup"><span data-stu-id="3c042-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="3c042-172">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello parametrów połączenia z hello sama nazwa (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="3c042-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="3c042-173">AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $connstring"--name $appName — myResourceGroup grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3c042-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="3c042-174">Należy pamiętać, że `$connstring` zawiera hello sformatowany ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="3c042-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="3c042-175">Należy ponownie wdrożyć tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="3c042-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="3c042-176">Użyj toopush polecenia Git tooAzure Twoje zmiany</span><span class="sxs-lookup"><span data-stu-id="3c042-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="3c042-177">Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="3c042-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="3c042-178">Przeglądaj toohello aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="3c042-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="3c042-179">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello zmiany wprowadzone w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="3c042-180">Krok 4 — wystąpień toomultiple skali</span><span class="sxs-lookup"><span data-stu-id="3c042-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="3c042-181">plan usługi aplikacji Hello jest hello jednostką skalowania dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="3c042-182">tooscale limit aplikacji sieci web, można skalować hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="3c042-183">Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale limit hello wystąpieniach toothree planu usługi aplikacji, która jest hello maksymalnej liczby dozwolonej przez hello B1 warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="3c042-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="3c042-184">Należy pamiętać, że B1 jest hello utworzenia hello wcześniej planu usługi aplikacji — warstwa wybraną warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="3c042-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="3c042-185">Krok 5 — skali geograficznie</span><span class="sxs-lookup"><span data-stu-id="3c042-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="3c042-186">Skalowanie geograficznie, możesz uruchomić aplikację w wielu regionach hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="3c042-187">Ten Instalator zrównoważenie obciążenia aplikacji dalsze oparte na lokalizacji geograficznej i zmniejsza czas odpowiedzi hello przez umieszczenie przeglądarek tooclient bliżej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="3c042-188">W tym kroku skalować ASP.NET web app tooa drugi regionu z [usługi Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="3c042-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="3c042-189">Na końcu hello hello krok będziesz mieć aplikację sieci web uruchomione w Europie zachodnie (już utworzone) i aplikacji sieci web uruchomionych w Azji Południowo-Wschodnia (jeszcze nie utworzono).</span><span class="sxs-lookup"><span data-stu-id="3c042-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="3c042-190">Obie aplikacje zostanie obsłużona z hello sam adres URL Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="3c042-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="3c042-191">Skalowanie w górę hello Europy aplikacji tooStandard warstwy</span><span class="sxs-lookup"><span data-stu-id="3c042-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="3c042-192">W usłudze App Service Integracja z usługą Azure Traffic Manager wymaga warstwy cenowej standardowa hello.</span><span class="sxs-lookup"><span data-stu-id="3c042-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="3c042-193">Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale się z tooS1 planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="3c042-194">Tworzenie profilu usługi Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="3c042-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="3c042-195">Użyj [Tworzenie profilu Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate Traffic Manager profilu i dodaj go tooyour grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3c042-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="3c042-196">Użyj unikatowej nazwy DNS w $dnsName.</span><span class="sxs-lookup"><span data-stu-id="3c042-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="3c042-197">`--routing-method Performance`Określa, że ten profil [kieruje użytkownika ruchu toohello najbliższy punkt końcowy](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="3c042-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="3c042-198">Pobierz identyfikator zasobu hello hello Europy aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="3c042-199">Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello identyfikator zasobu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3c042-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="3c042-200">Dodawanie punktu końcowego Menedżera ruchu hello Europy aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="3c042-201">Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour punktu końcowego profilu Menedżera ruchu i użycia hello identyfikator zasobu aplikacji sieci web jako hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="3c042-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="3c042-202">Pobierz adres URL punktu końcowego Menedżera ruchu hello</span><span class="sxs-lookup"><span data-stu-id="3c042-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="3c042-203">Profil Menedżera ruchu ma punkt końcowy tego istniejącej aplikacji sieci web punktów tooyour.</span><span class="sxs-lookup"><span data-stu-id="3c042-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="3c042-204">Użyj [Pokaż profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3c042-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="3c042-205">Kopiuj dane wyjściowe hello w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="3c042-205">Copy hello output into your browser.</span></span> <span data-ttu-id="3c042-206">Aplikacja sieci web powinno zostać wyświetlone ponownie.</span><span class="sxs-lookup"><span data-stu-id="3c042-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="3c042-207">Tworzenie pamięci podręcznej Azure Redis w Azji</span><span class="sxs-lookup"><span data-stu-id="3c042-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="3c042-208">Teraz możesz replikować regionu Azja południowo-wschodnia toohello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="3c042-209">toostart, użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate drugi pamięć podręczna Redis Azure w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="3c042-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="3c042-210">Ta pamięć podręczna musi toobe kolokowane z aplikacją w Azji.</span><span class="sxs-lookup"><span data-stu-id="3c042-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="3c042-211">`--name $cacheName-asia`zapewnia hello nazwę hello pamięci podręcznej hello pamięci podręcznej Europa Zachodnia, z hello `-asia` sufiks.</span><span class="sxs-lookup"><span data-stu-id="3c042-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="3c042-212">Tworzenie planu usługi App Service w Azji</span><span class="sxs-lookup"><span data-stu-id="3c042-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="3c042-213">Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate drugi usługi aplikacji plan hello regionu Azja południowo-wschodnia, przy użyciu hello S1 tej samej warstwie jako hello plan Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="3c042-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="3c042-214">Tworzenie aplikacji sieci web w Azji</span><span class="sxs-lookup"><span data-stu-id="3c042-214">Create a web app in Asia</span></span>
<span data-ttu-id="3c042-215">Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate drugi aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3c042-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="3c042-216">`--name $appName-asia`zapewnia hello nazwa hello aplikacji hello aplikacji Europa Zachodnia, z hello `-asia` sufiks.</span><span class="sxs-lookup"><span data-stu-id="3c042-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="3c042-217">Konfigurowanie parametrów połączenia powitania dla pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="3c042-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="3c042-218">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello sieci web aplikacji hello ciąg połączenia dla hello Azja południowo-wschodnia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3c042-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="3c042-219">AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $($redis.hostname): $($redis.sslPort), hasło = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False"--name $appName — Azja--myResourceGroup grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3c042-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="3c042-220">Konfiguruj wdrożenie Git dla aplikacji Azja hello.</span><span class="sxs-lookup"><span data-stu-id="3c042-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="3c042-221">Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokalnego wdrożenia Git dla aplikacji sieci web drugi hello.</span><span class="sxs-lookup"><span data-stu-id="3c042-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="3c042-222">To polecenie umożliwia skorzystanie z danych wyjściowych, która wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="3c042-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="3c042-223">Użyj hello zwrócił tooconfigure adres URL drugi Git dla lokalnego repozytorium zdalnego.</span><span class="sxs-lookup"><span data-stu-id="3c042-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="3c042-224">Witaj następujące polecenie używa hello poprzedzających przykład danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3c042-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="3c042-225">Wdrażanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-225">Deploy your sample application</span></span>
<span data-ttu-id="3c042-226">Uruchom `git push` toodeploy Twojego drugi zdalnego Git przykładowej aplikacji toohello.</span><span class="sxs-lookup"><span data-stu-id="3c042-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="3c042-227">Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="3c042-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="3c042-228">Przeglądaj toohello Azja aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-228">Browse toohello Asia app</span></span>
<span data-ttu-id="3c042-229">Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify, że aplikacja działa na żywo na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3c042-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="3c042-230">Pobierz identyfikator zasobu hello hello Azja aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="3c042-231">Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello identyfikator zasobu aplikacji sieci web w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="3c042-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="3c042-232">Dodawanie punktu końcowego Menedżera ruchu hello Azja aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c042-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="3c042-233">Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd drugi toohello punktu końcowego profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="3c042-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="3c042-234">Dodawanie aplikacji tooweb identyfikator regionu</span><span class="sxs-lookup"><span data-stu-id="3c042-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="3c042-235">Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd zmienną środowiskową określonego regionu.</span><span class="sxs-lookup"><span data-stu-id="3c042-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="3c042-236">Kod aplikacji już używa tego ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c042-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="3c042-237">Spójrz na `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="3c042-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="3c042-238">Zakończenie!</span><span class="sxs-lookup"><span data-stu-id="3c042-238">Complete!</span></span>

<span data-ttu-id="3c042-239">Teraz spróbuj tooaccess hello adres URL profilu Menedżera ruchu z przeglądarek w różnych regionach geograficznych.</span><span class="sxs-lookup"><span data-stu-id="3c042-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="3c042-240">Przeglądarka klienta z Europy powinny być widoczne "Europa Zachodnia ASP.NET" i "Azja południowo-wschodnia ASP.NET." powinny być widoczne w przeglądarce klienta z Azja</span><span class="sxs-lookup"><span data-stu-id="3c042-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="3c042-241">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="3c042-241">More resources</span></span>
