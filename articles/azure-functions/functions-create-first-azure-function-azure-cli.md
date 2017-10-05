---
title: Tworzenie pierwszej funkcji z poziomu interfejsu wiersza polecenia platformy Azure | Microsoft Docs
description: "Dowiedz się, jak utworzyć pierwszą funkcję platformy Azure do wykonywania bezserwerowego z poziomu interfejsu wiersza polecenia platformy Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 8bd3e4bb7423db44c48b04f25edcf1074e6ea0bd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="24778-103">Tworzenie pierwszej funkcji z poziomu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="24778-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="24778-104">W tym samouczku szybkiego startu omówiono tworzenie pierwszej funkcji przy użyciu usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="24778-104">This quickstart tutorial walks through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="24778-105">Za pomocą interfejsu wiersza polecenia platformy Azure zostanie utworzona aplikacja funkcji, która jest bezserwerową infrastrukturą hostującą funkcję.</span><span class="sxs-lookup"><span data-stu-id="24778-105">You use the Azure CLI to create a function app, which is the serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="24778-106">Sam kod funkcji jest wdrażany z repozytorium przykładów GitHub.</span><span class="sxs-lookup"><span data-stu-id="24778-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="24778-107">Poniższe kroki możesz wykonać przy użyciu komputera z systemem Mac, Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="24778-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="24778-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24778-108">Prerequisites</span></span> 

<span data-ttu-id="24778-109">Przed uruchomieniem tego przykładu należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="24778-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="24778-110">Aktywne konto usługi [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="24778-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="24778-111">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24778-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="24778-112">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="24778-112">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="24778-113">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="24778-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="24778-114">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24778-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="24778-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="24778-115">Create a resource group</span></span>

<span data-ttu-id="24778-116">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="24778-116">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="24778-117">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje funkcji, bazy danych i konta magazynu, oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="24778-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="24778-118">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="24778-118">The following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="24778-119">Jeśli nie korzystasz z usługi Cloud Shell, musisz się najpierw zalogować za pomocą polecenia `az login`.</span><span class="sxs-lookup"><span data-stu-id="24778-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="24778-120">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="24778-120">Create an Azure Storage account</span></span>

<span data-ttu-id="24778-121">Usługa Functions przechowuje informacje o stanie i inne informacje dotyczące funkcji za pomocą konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="24778-121">Functions uses an Azure Storage account to maintain state and other information about your functions.</span></span> <span data-ttu-id="24778-122">Utwórz konto magazynu w utworzonej grupie zasobów przy użyciu polecenia [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="24778-122">Create a storage account in the resource group you created by using the [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="24778-123">W poniższym poleceniu w miejsce symbolu zastępczego `<storage_name>` wstaw swoją własną unikatową w skali globalnej nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="24778-123">In the following command, substitute your own globally unique storage account name where you see the `<storage_name>` placeholder.</span></span> <span data-ttu-id="24778-124">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="24778-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="24778-125">Po utworzeniu konta magazynu w interfejsie wiersza polecenia platformy Azure zostanie wyświetlona informacja podobna do następującej:</span><span class="sxs-lookup"><span data-stu-id="24778-125">After the storage account has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="24778-126">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="24778-126">Create a function app</span></span>

<span data-ttu-id="24778-127">Do obsługi wykonywania funkcji potrzebna jest aplikacja funkcji.</span><span class="sxs-lookup"><span data-stu-id="24778-127">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="24778-128">Aplikacja funkcji zapewnia środowisko do bezserwerowego wykonywania kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="24778-128">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="24778-129">Umożliwia ona grupowanie funkcji w ramach jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="24778-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="24778-130">Utwórz aplikację funkcji przy użyciu polecenia [az functionapp create](/cli/azure/functionapp#create).</span><span class="sxs-lookup"><span data-stu-id="24778-130">Create a function app by using the [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="24778-131">W poniższym poleceniu w miejsce symbolu zastępczego `<app_name>` wstaw swoją własną unikatową w skali globalnej nazwę aplikacji funkcji, a w miejsce symbolu zastępczego `<storage_name>` wstaw nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="24778-131">In the following command, substitute your own unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="24778-132">Nazwa `<app_name>` jest używana jako domyślna domena DNS aplikacji funkcji, więc nazwa ta musi być unikatowa wśród wszystkich aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="24778-132">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="24778-133">Domyślnie aplikacja funkcji jest tworzona z planem hostingu Zużycie, co oznacza, że zasoby są dodawane dynamicznie zgodnie z wymaganiami funkcji, a opłaty są naliczane tylko wtedy, gdy funkcje są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="24778-133">By default, a function app is created with the Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="24778-134">Aby uzyskać więcej informacji, zobacz [Wybieranie odpowiedniego planu hostingu](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="24778-134">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="24778-135">Po utworzeniu aplikacji funkcji interfejs wiersza polecenia platformy Azure wyświetli informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="24778-135">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="24778-136">Teraz, gdy masz już aplikację funkcji, możesz wdrożyć właściwy kod funkcji z repozytorium przykładów GitHub.</span><span class="sxs-lookup"><span data-stu-id="24778-136">Now that you have a function app, you can deploy the actual function code from the GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="24778-137">Wdrażanie kodu funkcji</span><span class="sxs-lookup"><span data-stu-id="24778-137">Deploy your function code</span></span>  

<span data-ttu-id="24778-138">Istnieje kilka sposobów tworzenia kodu funkcji w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="24778-138">There are several ways to create your function code in your new function app.</span></span> <span data-ttu-id="24778-139">Ten temat jest połączony z repozytorium przykładów w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="24778-139">This topic connects to a sample repository in GitHub.</span></span> <span data-ttu-id="24778-140">Tak jak poprzednio, w poniższym kodzie w miejsce symbolu zastępczego `<app_name>` wstaw nazwę utworzonej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="24778-140">As before, in the following code replace the `<app_name>` placeholder with the name of the function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="24778-141">Po ustawieniu źródła wdrożenia w interfejsie wiersza polecenia platformy Azure zostanie wyświetlona informacja podobna do następującej (wartości null zostały usunięte, aby poprawić czytelność):</span><span class="sxs-lookup"><span data-stu-id="24778-141">After the deployment source been set, the Azure CLI shows information similar to the following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-the-function"></a><span data-ttu-id="24778-142">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="24778-142">Test the function</span></span>

<span data-ttu-id="24778-143">Przetestuj wdrożoną funkcję za pomocą programu cURL na komputerze Mac lub komputerze z systemem Linux bądź za pomocą powłoki Bash na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="24778-143">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="24778-144">Uruchom następujące polecenie programu cURL, wstawiając w miejsce symbolu zastępczego `<app_name>` nazwę aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="24778-144">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="24778-145">Dołącz ciąg zapytania `&name=<yourname>` do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="24778-145">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="24778-147">Jeśli w wierszu polecenia nie jest dostępny program cURL, wprowadź ten sam adres URL w pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="24778-147">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="24778-148">W miejsce symbolu zastępczego `<app_name>` wstaw nazwę aplikacji funkcji i dołącz ciąg zapytania `&name=<yourname>` do adresu URL, a następnie wykonaj żądanie.</span><span class="sxs-lookup"><span data-stu-id="24778-148">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="24778-150">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="24778-150">Clean up resources</span></span>

<span data-ttu-id="24778-151">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="24778-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="24778-152">Jeśli planujesz kontynuować pracę z kolejnymi przewodnikami Szybki start lub samouczkami, nie usuwaj zasobów utworzonych w tym przewodniku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="24778-152">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="24778-153">Jeśli nie planujesz kontynuować pracy, użyj poniższego polecenia, aby usunąć wszystkie zasoby utworzone w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="24778-153">If you do not plan to continue, use the following command to delete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="24778-154">Gdy pojawi się monit, wpisz `y`.</span><span class="sxs-lookup"><span data-stu-id="24778-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24778-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24778-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
