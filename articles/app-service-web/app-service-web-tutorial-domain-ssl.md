---
title: domeny niestandardowej aaaAdd i SSL tooan Azure web app | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooprepare platformy Azure w sieci web toogo aplikacji w środowisku produkcyjnym, dodając znakowaniu firmy. Mapa aplikacji sieci web tooyour (domena niestandardowych) nazwa domeny niestandardowej hello i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="24a16-104">Dodaj niestandardową domenę i protokołu SSL tooan aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="24a16-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="24a16-105">Ten samouczek pokazuje, jak tooquickly mapowania aplikacji sieci web Azure tooyour nazwy domeny niestandardowej i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="24a16-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="24a16-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="24a16-106">Before you begin</span></span>

<span data-ttu-id="24a16-107">Przed uruchomieniem tego przykładu należy zainstalować hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokalnie.</span><span class="sxs-lookup"><span data-stu-id="24a16-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="24a16-108">Należy również strony konfiguracji DNS toohello dostęp administracyjny do dostawcy odpowiedniej domeny.</span><span class="sxs-lookup"><span data-stu-id="24a16-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="24a16-109">Na przykład tooadd `www.contoso.com`, należy wpisy DNS może tooconfigure toobe dla `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="24a16-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="24a16-110">Ponadto należy się prawidłowe. Plik PFX _i_ jego hasło dla certyfikatu SSL hello ma tooupload i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="24a16-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="24a16-111">Ten certyfikat protokołu SSL należy toosecure skonfigurowanych hello domenę niestandardową nazwę.</span><span class="sxs-lookup"><span data-stu-id="24a16-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="24a16-112">W hello powyżej przykładzie, należy zabezpieczyć certyfikat SSL `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="24a16-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="24a16-113">Krok 1 — Tworzenie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="24a16-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="24a16-114">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="24a16-114">Log in tooAzure</span></span>

<span data-ttu-id="24a16-115">Mamy teraz będzie toouse hello Azure CLI 2.0 w zasobach hello toocreate okno terminalu potrzebne toohost naszej aplikacji Node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="24a16-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="24a16-116">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="24a16-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="24a16-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="24a16-117">Create a resource group</span></span>   
<span data-ttu-id="24a16-118">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="24a16-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="24a16-119">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="24a16-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="24a16-120">toosee jakie możliwe wartości można użyć dla `---location`, użyj hello `az appservice list-locations` polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24a16-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="24a16-121">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="24a16-121">Create an App Service plan</span></span>

<span data-ttu-id="24a16-122">Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="24a16-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="24a16-123">Witaj poniższy przykład tworzy plan usługi aplikacji o nazwie `myAppServicePlan` przy użyciu hello **podstawowe** warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="24a16-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="24a16-124">Tworzenie planu usług aplikacji az — nazwa myAppServicePlan — myResourceGroup grupy zasobów--sku B1</span><span class="sxs-lookup"><span data-stu-id="24a16-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="24a16-125">Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="24a16-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="24a16-126">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="24a16-126">Create a web app</span></span>

<span data-ttu-id="24a16-127">Teraz, utworzono plan usługi aplikacji, należy utworzyć aplikację sieci web w obrębie hello `myAppServicePlan` planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24a16-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="24a16-128">Hello daje aplikacji sieci web użytkownik w przypadku hostingu toodeploy miejsca kodu, a także zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24a16-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="24a16-129">Użyj hello [utworzyć az appservice web](/cli/azure/appservice/web#create) aplikacji sieci web hello toocreate polecenia.</span><span class="sxs-lookup"><span data-stu-id="24a16-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="24a16-130">W poleceniu hello poniżej, podstawić własną unikatowej nazwy aplikacji której występuje hello `<app_name>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="24a16-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="24a16-131">Ta nazwa będzie służyć jako część hello hello domyślna nazwa domeny dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="24a16-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="24a16-132">Później można mapować żadnych niestandardowych aplikacji sieci web toohello wpis DNS przed udostępnieniem jej tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="24a16-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="24a16-133">Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="24a16-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="24a16-134">Z danych wyjściowych JSON, hello `defaultHostName` wskazuje nazwę domeny domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="24a16-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="24a16-135">W przeglądarce Przejdź toothis adres.</span><span class="sxs-lookup"><span data-stu-id="24a16-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="24a16-137">Krok 2 — Konfigurowanie mapowania DNS</span><span class="sxs-lookup"><span data-stu-id="24a16-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="24a16-138">W tym kroku, Dodaj mapowanie z domeny niestandardowej tooyour aplikacji sieci web domyślna nazwa domeny `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="24a16-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="24a16-139">Zazwyczaj jest wykonanie tego kroku w witryny sieci Web dostawcy domeny.</span><span class="sxs-lookup"><span data-stu-id="24a16-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="24a16-140">Witryny sieci Web co rejestratora domen różni się nieznacznie, dlatego należy skonsultować się Twój dostawca dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="24a16-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="24a16-141">W tym miejscu są jednak pewne ogólne wytyczne.</span><span class="sxs-lookup"><span data-stu-id="24a16-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="24a16-142">Przejdź do strony zarządzania tootooDNS</span><span class="sxs-lookup"><span data-stu-id="24a16-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="24a16-143">Po pierwsze Zaloguj rejestratora domen tooyour witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="24a16-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="24a16-144">Następnie odnaleźć hello strony Zarządzanie rekordami DNS.</span><span class="sxs-lookup"><span data-stu-id="24a16-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="24a16-145">Wyszukaj łącza lub obszarów witryny hello etykietą **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="24a16-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="24a16-146">Często, można znaleźć łącza hello wyświetlanie informacji o koncie, a następnie sprawdzając takich jak łącze **mojej domeny**.</span><span class="sxs-lookup"><span data-stu-id="24a16-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="24a16-147">Po znalezieniu tej strony, poszukaj łącze umożliwiające dodawanie lub edytowanie rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="24a16-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="24a16-148">Może to być **pliku strefy** lub **rekordy DNS** łącza, lub **konfiguracji zaawansowanej** łącza.</span><span class="sxs-lookup"><span data-stu-id="24a16-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="24a16-149">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="24a16-149">Create a CNAME record</span></span>

<span data-ttu-id="24a16-150">Dodaj rekord CNAME mapujący hello poddomeny odpowiednią nazwę tooyour aplikacji sieci web domyślna nazwa domeny (`<app_name>.azurewebsites.net`, gdzie `<app_name>` jest unikatowa nazwa aplikacji).</span><span class="sxs-lookup"><span data-stu-id="24a16-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="24a16-151">Dla hello `www.contoso.com` przykład utworzyć rekord CNAME, który mapuje hello `www` hostname zbyt`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="24a16-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="24a16-152">Krok 3 — konfigurowanie domeny niestandardowej hello na aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="24a16-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="24a16-153">Po zakończeniu konfigurowania mapowania nazwy hosta hello w witryny sieci Web dostawcy domeny, możesz teraz gotowy tooconfigure hello niestandardową domenę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="24a16-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="24a16-154">Użyj hello [dodać az usługi aplikacji sieci web config hostname](/cli/azure/appservice/web/config/hostname#add) polecenia tooadd tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="24a16-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="24a16-155">W poleceniu hello poniżej, Zastąp `<app_name>` z unikatowej nazwy aplikacji, a < your_custom_domain > z hello pełną niestandardowej nazwy domeny (np. `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="24a16-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="24a16-156">domeny niestandardowej Hello jest teraz pełni zamapowanych tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="24a16-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="24a16-157">W przeglądarce Przejdź toohello niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="24a16-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="24a16-158">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="24a16-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="24a16-160">Krok 4 — wiązanie niestandardowej aplikacji sieci web tooyour certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="24a16-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="24a16-161">Masz teraz aplikacji sieci web platformy Azure, z nazwą domeny hello w hello na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="24a16-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="24a16-162">Jednak w przypadku przejścia toohello `https://<your_custom_domain>` teraz otrzymujesz błąd certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="24a16-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="24a16-164">Ten błąd występuje, ponieważ aplikacja sieci web nie ma jeszcze powiązanie certyfikatu SSL, który jest zgodny z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="24a16-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="24a16-165">Jednak nie występuje błąd, jeśli użytkownik przejdzie zbyt`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="24a16-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="24a16-166">Jest to spowodowane aplikacji, a także wszystkie aplikacje w usłudze Azure App Service, są chronione za hello certyfikat protokołu SSL dla hello `*.azurewebsites.net` domeny symbolu wieloznacznego domyślnie.</span><span class="sxs-lookup"><span data-stu-id="24a16-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="24a16-167">W kolejności tooaccess aplikacji sieci web przez niestandardową nazwę domeny, wymagany jest certyfikat SSL hello toobind dla aplikacji sieci web toohello domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="24a16-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="24a16-168">Wykona go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="24a16-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="24a16-169">Przekaż certyfikat SSL hello</span><span class="sxs-lookup"><span data-stu-id="24a16-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="24a16-170">Przekaż hello certyfikat SSL dla aplikacji sieci web tooyour domeny niestandardowej przy użyciu hello [az usługi aplikacji sieci web config ssl przekazywania](/cli/azure/appservice/web/config/ssl#upload) polecenia.</span><span class="sxs-lookup"><span data-stu-id="24a16-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="24a16-171">W poleceniu hello poniżej, Zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji, `<path_to_ptx_file>` z hello tooyour ścieżki. Plik PFX i `<password>` z hasło do certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="24a16-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="24a16-172">Po przekazaniu certyfikatu hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="24a16-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="24a16-173">Z danych wyjściowych JSON, hello `thumbprint` przedstawia odcisku palca certyfikatu przekazane.</span><span class="sxs-lookup"><span data-stu-id="24a16-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="24a16-174">Skopiuj wartości na potrzeby hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="24a16-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="24a16-175">Witaj BIND przekazać aplikacji sieci web toohello certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="24a16-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="24a16-176">Aplikacja sieci web ma teraz nazwę domeny niestandardowej hello i ma również certyfikat SSL, która zabezpiecza tej domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="24a16-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="24a16-177">Witaj tylko element toodo po lewej stronie jest toobind hello przekazano certyfikat toohello aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="24a16-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="24a16-178">Można to zrobić przy użyciu hello [powiązania ssl konfiguracji sieci web appservice az](/cli/azure/appservice/web/config/ssl#bind) polecenia.</span><span class="sxs-lookup"><span data-stu-id="24a16-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="24a16-179">W poleceniu hello poniżej, Zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji i `<thumbprint-from-previous-output>` z hello odcisk palca certyfikatu, który można pobrać z hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="24a16-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="24a16-180">powiązania ssl sieci web config az appservice--name < nazwa_aplikacji >--myResourceGroup grupy zasobów — odcisk palca certyfikatu < odcisk palca z — poprzednie output > SNI ssl — typ</span><span class="sxs-lookup"><span data-stu-id="24a16-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="24a16-181">Gdy certyfikat hello jest powiązane tooyour aplikacji sieci web, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="24a16-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="24a16-182">{"stanu dostępności": "Normal", "clientAffinityEnabled": ma wartość true, "clientCertEnabled": ma wartość FAŁSZ, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< nazwa_aplikacji >. azurewebsites.net", "enabled": true "enabledHostNames": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net", "< nazwa_aplikacji >. scm.azurewebsites.net"], "gatewaySiteName": null, "hostNameSslStates": [{"hostType": "Standardowy", "name": "< nazwa_aplikacji >. azurewebsites.net", "sslState": "Wyłączone", "odcisk palca": null, "toUpdate": wartość null, "wirtualnego adresu IP": null}, {"hostType": "Repository", "name": "< nazwa_aplikacji >. scm.azurewebsites.net", "sslState": "Wyłączone" "odcisk palca": null, "toUpdate": null, "wirtualnego adresu IP": wartości null}, {"hostType": "Standardowy", "name": "www.contoso.com", "sslState": "SniEnabled", "odcisk palca": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "wirtualnego adresu IP": wartości null}], "nazwy hostów": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net"], "hostNamesDisabled": ma wartość FAŁSZ, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < nazwa_aplikacji >", "isDefaultContainer": null "typu": "Aplikacja sieci Web", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "Lokalizacja": "Europa Zachodnia", "maxNumberOfWorkers": null, "Mikrousługi": "false", "Nazwa": "< nazwa_aplikacji >" "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "< nazwa_aplikacji >", "zastrzeżone": false "w grupie zasobów": "myResourceGroup", "scmSiteAlsoStopped": ma wartość FAŁSZ, "serverFarmId": "/ subskrypcji/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/dostawców/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "stan": "Uruchomiona", "suspendedTill": null "tagi": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal"}</span><span class="sxs-lookup"><span data-stu-id="24a16-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="24a16-183">W przeglądarce Przejdź tooHTTPS punkt końcowy z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="24a16-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="24a16-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="24a16-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="24a16-186">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="24a16-186">More resources</span></span>

<span data-ttu-id="24a16-187">[Kupowanie i konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="24a16-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
