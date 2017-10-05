---
title: "Dodaj niestandardową domenę i protokołu SSL dla aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przygotować aplikacji sieci Azure web, aby przejść przez dodanie znakowaniu firmy produkcji. Mapa niestandardowa nazwa domeny (domena niestandardowych) do aplikacji sieci web i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL."
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="76660-104">Dodaj niestandardową domenę i protokołu SSL dla aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="76660-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="76660-105">Ten samouczek pokazuje, jak szybko zamapować niestandardowej nazwy domeny do aplikacji sieci web platformy Azure i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="76660-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="76660-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="76660-106">Before you begin</span></span>

<span data-ttu-id="76660-107">Przed uruchomieniem tego przykładu należy zainstalować [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokalnie.</span><span class="sxs-lookup"><span data-stu-id="76660-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="76660-108">Należy również dostęp administracyjny do strony Konfiguracja DNS dla dostawcy odpowiedniej domeny.</span><span class="sxs-lookup"><span data-stu-id="76660-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="76660-109">Na przykład, aby dodać `www.contoso.com`, musisz mieć możliwość konfigurowania wpisów DNS dla `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="76660-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="76660-110">Ponadto należy się prawidłowe. Plik PFX _i_ jego hasło dla certyfikatu SSL, aby przekazać i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="76660-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="76660-111">Należy skonfigurować ten certyfikat protokołu SSL do zabezpieczania nazwy domeny niestandardowej, która ma.</span><span class="sxs-lookup"><span data-stu-id="76660-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="76660-112">W powyższym przykładzie, należy zabezpieczyć certyfikat SSL `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="76660-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="76660-113">Krok 1 — Tworzenie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="76660-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="76660-114">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="76660-114">Log in to Azure</span></span>

<span data-ttu-id="76660-115">Teraz użyjemy interfejsu wiersza polecenia platformy Azure 2.0 w oknie terminalu do utworzenia zasobów wymaganych do hostowania tej aplikacji w języku Node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="76660-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="76660-116">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="76660-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="76660-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="76660-117">Create a resource group</span></span>   
<span data-ttu-id="76660-118">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="76660-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="76660-119">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="76660-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="76660-120">Aby sprawdzić, jakich wartości można użyć dla lokalizacji `---location`, użyj polecenia interfejsu wiersza polecenia platformy Azure `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="76660-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="76660-121">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="76660-121">Create an App Service plan</span></span>

<span data-ttu-id="76660-122">Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="76660-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="76660-123">Poniższy przykład tworzy plan usługi aplikacji o nazwie `myAppServicePlan` przy użyciu **podstawowe** warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="76660-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="76660-124">Tworzenie planu usług aplikacji az — nazwa myAppServicePlan — myResourceGroup grupy zasobów--sku B1</span><span class="sxs-lookup"><span data-stu-id="76660-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="76660-125">Po utworzeniu planu usługi aplikacji Azure CLI przedstawia informacje podobne do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="76660-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="76660-126">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="76660-126">Create a web app</span></span>

<span data-ttu-id="76660-127">Teraz, gdy został utworzony plan usługi App Service, utwórz aplikację sieci Web w ramach planu usługi App Service `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="76660-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="76660-128">Umożliwia aplikacji sieci web, możesz w przypadku hostingu miejsca, aby wdrożyć kod, a także zawiera adres URL do wyświetlania wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76660-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="76660-129">Użyj polecenia [az appservice web create](/cli/azure/appservice/web#create), aby utworzyć aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="76660-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="76660-130">W poniższym poleceniu zastąp z własnej nazwy unikatowy aplikacji, w której występuje `<app_name>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="76660-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="76660-131">Ta nazwa będzie służyć jako część domyślna nazwa domeny dla aplikacji sieci web, więc nazwa musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="76660-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="76660-132">Później możesz zamapować dowolny niestandardowy wpis DNS na aplikację sieci Web, zanim udostępnisz ją użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="76660-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="76660-133">Po utworzeniu aplikacji sieci Web interfejs wiersza polecenia platformy Azure wyświetli informacje podobne do następujących.</span><span class="sxs-lookup"><span data-stu-id="76660-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

<span data-ttu-id="76660-134">Z danych wyjściowych JSON `defaultHostName` wskazuje nazwę domeny domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76660-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="76660-135">W przeglądarce przejdź do tego adresu.</span><span class="sxs-lookup"><span data-stu-id="76660-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="76660-137">Krok 2 — Konfigurowanie mapowania DNS</span><span class="sxs-lookup"><span data-stu-id="76660-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="76660-138">W tym kroku należy dodać mapowanie z domeny niestandardowej nazwy domeny domyślnej aplikacji sieci web, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="76660-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="76660-139">Zazwyczaj jest wykonanie tego kroku w witryny sieci Web dostawcy domeny.</span><span class="sxs-lookup"><span data-stu-id="76660-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="76660-140">Witryny sieci Web co rejestratora domen różni się nieznacznie, dlatego należy skonsultować się Twój dostawca dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="76660-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="76660-141">W tym miejscu są jednak pewne ogólne wytyczne.</span><span class="sxs-lookup"><span data-stu-id="76660-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="76660-142">Przejdź do strony zarządzania DNS</span><span class="sxs-lookup"><span data-stu-id="76660-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="76660-143">Po pierwsze Zaloguj się do witryny sieci Web rejestratora domen.</span><span class="sxs-lookup"><span data-stu-id="76660-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="76660-144">Następnie można znaleźć strony zarządzania rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="76660-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="76660-145">Wyszukaj łącza lub obszarów witryny z etykietą **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="76660-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="76660-146">Często, można znaleźć link wyświetlanie informacji o koncie, a następnie sprawdzając takich jak łącze **mojej domeny**.</span><span class="sxs-lookup"><span data-stu-id="76660-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="76660-147">Po znalezieniu tej strony, poszukaj łącze umożliwiające dodawanie lub edytowanie rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="76660-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="76660-148">Może to być **pliku strefy** lub **rekordy DNS** łącza, lub **konfiguracji zaawansowanej** łącza.</span><span class="sxs-lookup"><span data-stu-id="76660-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="76660-149">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="76660-149">Create a CNAME record</span></span>

<span data-ttu-id="76660-150">Dodaj rekord CNAME mapujący nazwa żądanego poddomeny do aplikacji sieci web domyślna nazwa domeny (`<app_name>.azurewebsites.net`, gdzie `<app_name>` jest unikatowa nazwa aplikacji).</span><span class="sxs-lookup"><span data-stu-id="76660-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="76660-151">Dla `www.contoso.com` przykład utworzyć rekord CNAME, który mapuje `www` nazwy hosta do `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="76660-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="76660-152">Krok 3 — konfigurowanie domeny niestandardowej w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="76660-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="76660-153">Po zakończeniu konfigurowania mapowania nazwy hosta w witryny sieci Web dostawcy domeny, możesz przystąpić do konfigurowania domeny niestandardowej w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76660-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="76660-154">Użyj [dodać az usługi aplikacji sieci web config hostname](/cli/azure/appservice/web/config/hostname#add) polecenie, aby dodać tę konfigurację.</span><span class="sxs-lookup"><span data-stu-id="76660-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="76660-155">W poniższym poleceniu zastąp `<app_name>` z unikatowej nazwy aplikacji, a < your_custom_domain > o nazwie FQDN domen niestandardowych (np. `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="76660-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="76660-156">Domena niestandardowa teraz pełni jest mapowana do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76660-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="76660-157">W przeglądarce przejdź do nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="76660-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="76660-158">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="76660-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="76660-160">Krok 4 — wiązanie niestandardowe certyfikat SSL do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="76660-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="76660-161">Masz teraz aplikacji sieci web platformy Azure, wraz z nazwą domeny, w pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="76660-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="76660-162">Jednak jeśli przejdziesz do `https://<your_custom_domain>` teraz otrzymujesz błąd certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="76660-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="76660-164">Ten błąd występuje, ponieważ aplikacja sieci web nie ma jeszcze powiązanie certyfikatu SSL, który jest zgodny z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="76660-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="76660-165">Jednak nie występuje błąd, jeśli przejdziesz do `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="76660-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="76660-166">Jest to spowodowane aplikacji, a także wszystkie aplikacje w usłudze Azure App Service, jest zabezpieczony przy użyciu certyfikatu SSL dla `*.azurewebsites.net` domeny symbolu wieloznacznego domyślnie.</span><span class="sxs-lookup"><span data-stu-id="76660-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="76660-167">Aby uzyskać dostęp do aplikacji sieci web przez niestandardową nazwę domeny, należy powiązać certyfikat protokołu SSL dla domeny niestandardowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76660-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="76660-168">Wykona go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="76660-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="76660-169">Przekaż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="76660-169">Upload the SSL certificate</span></span>

<span data-ttu-id="76660-170">Przekaż certyfikat protokołu SSL dla domeny niestandardowej do aplikacji sieci web przy użyciu [az usługi aplikacji sieci web config ssl przekazywania](/cli/azure/appservice/web/config/ssl#upload) polecenia.</span><span class="sxs-lookup"><span data-stu-id="76660-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="76660-171">W poniższym poleceniu zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji, `<path_to_ptx_file>` ze ścieżką do sieci. Plik PFX i `<password>` z hasło do certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="76660-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="76660-172">Po przekazaniu certyfikat interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="76660-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="76660-173">Z danych wyjściowych JSON `thumbprint` przedstawia odcisku palca certyfikatu przekazane.</span><span class="sxs-lookup"><span data-stu-id="76660-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="76660-174">Skopiuj wartości na potrzeby kolejnego kroku.</span><span class="sxs-lookup"><span data-stu-id="76660-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="76660-175">Powiąż przekazany certyfikat SSL do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="76660-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="76660-176">Aplikacja sieci web ma teraz nazwę domeny niestandardowej, który ma i ma również certyfikat SSL, która zabezpiecza tej domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="76660-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="76660-177">Tylko celu pozostało Aby powiązać certyfikat z przekazane do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76660-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="76660-178">Można to zrobić przy użyciu [powiązania ssl konfiguracji sieci web appservice az](/cli/azure/appservice/web/config/ssl#bind) polecenia.</span><span class="sxs-lookup"><span data-stu-id="76660-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="76660-179">W poniższym poleceniu zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji i `<thumbprint-from-previous-output>` o odcisk palca certyfikatu, który można pobrać z poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="76660-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="76660-180">powiązania ssl sieci web config az appservice--name < nazwa_aplikacji >--myResourceGroup grupy zasobów — odcisk palca certyfikatu < odcisk palca z — poprzednie output > SNI ssl — typ</span><span class="sxs-lookup"><span data-stu-id="76660-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="76660-181">Gdy certyfikat jest powiązana z aplikacji sieci web, Azure CLI pokazuje informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="76660-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="76660-182">{"stanu dostępności": "Normal", "clientAffinityEnabled": ma wartość true, "clientCertEnabled": ma wartość FAŁSZ, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< nazwa_aplikacji >. azurewebsites.net", "enabled": true "enabledHostNames": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net", "< nazwa_aplikacji >. scm.azurewebsites.net"], "gatewaySiteName": null, "hostNameSslStates": [{"hostType": "Standardowy", "name": "< nazwa_aplikacji >. azurewebsites.net", "sslState": "Wyłączone", "odcisk palca": null, "toUpdate": wartość null, "wirtualnego adresu IP": null}, {"hostType": "Repository", "name": "< nazwa_aplikacji >. scm.azurewebsites.net", "sslState": "Wyłączone" "odcisk palca": null, "toUpdate": null, "wirtualnego adresu IP": wartości null}, {"hostType": "Standardowy", "name": "www.contoso.com", "sslState": "SniEnabled", "odcisk palca": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "wirtualnego adresu IP": wartości null}], "nazwy hostów": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net"], "hostNamesDisabled": ma wartość FAŁSZ, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < nazwa_aplikacji >", "isDefaultContainer": null "typu": "Aplikacja sieci Web", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "Lokalizacja": "Europa Zachodnia", "maxNumberOfWorkers": null, "Mikrousługi": "false", "Nazwa": "< nazwa_aplikacji >" "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "< nazwa_aplikacji >", "zastrzeżone": false "w grupie zasobów": "myResourceGroup", "scmSiteAlsoStopped": ma wartość FAŁSZ, "serverFarmId": "/ subskrypcji/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/dostawców/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "stan": "Uruchomiona", "suspendedTill": null "tagi": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal"}</span><span class="sxs-lookup"><span data-stu-id="76660-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="76660-183">W przeglądarce przejdź do punktu końcowego protokołu HTTPS z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="76660-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="76660-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="76660-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="76660-186">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="76660-186">More resources</span></span>

<span data-ttu-id="76660-187">[Kupowanie i konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="76660-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
