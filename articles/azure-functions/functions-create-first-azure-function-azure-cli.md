---
title: aaaCreate pierwszej funkcji z interfejsu wiersza polecenia Azure hello | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate platformy Azure pierwsze działać przez wykonanie niekorzystającą hello wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="07098-103">Utwórz swoją pierwszą funkcję przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="07098-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="07098-104">Ten samouczek szybkiego startu przedstawia procedury toocreate usługi Azure Functions toouse swoją pierwszą funkcję.</span><span class="sxs-lookup"><span data-stu-id="07098-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="07098-105">Możesz użyć hello Azure CLI toocreate aplikacji funkcji, który jest hello bez serwera infrastruktury, który jest hostem funkcji.</span><span class="sxs-lookup"><span data-stu-id="07098-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="07098-106">Witaj funkcja kodu jest wdrażany z repozytorium GitHub próbki.</span><span class="sxs-lookup"><span data-stu-id="07098-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="07098-107">Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="07098-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="07098-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07098-108">Prerequisites</span></span> 

<span data-ttu-id="07098-109">Przed uruchomieniem tego przykładu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="07098-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="07098-110">Aktywne konto usługi [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="07098-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="07098-111">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07098-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="07098-112">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="07098-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="07098-113">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="07098-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="07098-114">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07098-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="07098-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="07098-115">Create a resource group</span></span>

<span data-ttu-id="07098-116">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="07098-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="07098-117">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje funkcji, bazy danych i konta magazynu, oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="07098-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="07098-118">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="07098-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="07098-119">Jeśli nie korzystasz z usługi Cloud Shell, musisz się najpierw zalogować za pomocą polecenia `az login`.</span><span class="sxs-lookup"><span data-stu-id="07098-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="07098-120">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="07098-120">Create an Azure Storage account</span></span>

<span data-ttu-id="07098-121">Funkcje używa toomaintain stan konta magazynu Azure i inne informacje dotyczące funkcji.</span><span class="sxs-lookup"><span data-stu-id="07098-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="07098-122">Utwórz konto magazynu w grupie zasobów hello został utworzony za pomocą hello [Tworzenie konta magazynu az](/cli/azure/storage/account#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="07098-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="07098-123">Hello następujące polecenia, podstawić własną nazwę konta magazynu unikatowych której występuje hello `<storage_name>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="07098-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="07098-124">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="07098-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="07098-125">Po utworzeniu konta magazynu hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="07098-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="07098-126">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="07098-126">Create a function app</span></span>

<span data-ttu-id="07098-127">Funkcja aplikacji toohost hello wykonywanie funkcji są wymagane.</span><span class="sxs-lookup"><span data-stu-id="07098-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="07098-128">Aplikacja funkcji Hello zapewnia środowisko niekorzystającą wykonywania kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="07098-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="07098-129">Umożliwia ona grupowanie funkcji w ramach jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="07098-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="07098-130">Tworzenie aplikacji funkcji przy użyciu hello [az functionapp utworzyć](/cli/azure/functionapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="07098-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="07098-131">Hello następujące polecenia, Zastąp własną nazwą aplikacji unique — funkcja, której występuje hello `<app_name>` symbolu zastępczego i hello nazwy konta magazynu dla `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="07098-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="07098-132">Witaj `<app_name>` jest używany jako domyślnej domeny DNS dla aplikacji funkcja hello i tak nazwy hello hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="07098-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="07098-133">Domyślnie aplikacja funkcji jest tworzony z hello zużycie hostingu planu, co oznacza, że zasoby są dodawane dynamicznie, co jest wymagane przez funkcji i płacisz tylko po uruchomieniu funkcji.</span><span class="sxs-lookup"><span data-stu-id="07098-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="07098-134">Aby uzyskać więcej informacji, zobacz [plan hostingu poprawne hello wybierz](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="07098-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="07098-135">Po utworzeniu aplikacji funkcji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="07098-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="07098-136">Teraz, gdy masz aplikacji funkcji, można wdrożyć kod rzeczywista funkcja hello z repozytorium przykładowej GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="07098-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="07098-137">Wdrażanie kodu funkcji</span><span class="sxs-lookup"><span data-stu-id="07098-137">Deploy your function code</span></span>  

<span data-ttu-id="07098-138">Istnieje kilka sposobów toocreate funkcja kodu w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="07098-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="07098-139">W tym temacie łączy tooa próbki repozytorium w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="07098-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="07098-140">Jak wcześniej w hello następującego kodu Zastąp hello `<app_name>` symbolu zastępczego o nazwie hello hello funkcji aplikacji został utworzony.</span><span class="sxs-lookup"><span data-stu-id="07098-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="07098-141">Po wdrożeniu hello źródła została ustawiona, powitalne interfejsu wiersza polecenia Azure zawiera informacje o toohello podobnie poniższy przykład (usunąć dla czytelności wartości null):</span><span class="sxs-lookup"><span data-stu-id="07098-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="07098-142">Funkcja hello testu</span><span class="sxs-lookup"><span data-stu-id="07098-142">Test hello function</span></span>

<span data-ttu-id="07098-143">Funkcja cURL tootest hello wdrożona na komputerze Mac lub Linux lub przy użyciu Bash w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="07098-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="07098-144">Wykonanie następującego polecenia cURL, zastępując hello hello `<app_name>` symbolu zastępczego o nazwie hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07098-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="07098-145">Dołącz ciągu zapytania hello `&name=<yourname>` toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07098-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="07098-147">Jeśli nie jest dostępne w wierszu polecenia cURL, wprowadź hello tego samego adresu URL hello adresu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="07098-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="07098-148">Ponownie, Zastąp hello `<app_name>` symbolu zastępczego o nazwie hello funkcji aplikacji i Dołącz ciągu zapytania hello `&name=<yourname>` toohello adresu URL i wykonać hello żądania.</span><span class="sxs-lookup"><span data-stu-id="07098-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="07098-150">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="07098-150">Clean up resources</span></span>

<span data-ttu-id="07098-151">Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="07098-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="07098-152">Jeśli planujesz toocontinue toowork kolejne Przewodniki Szybki Start lub hello samouczki, czy nie wyczyścić zasoby hello utworzone w tym Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="07098-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="07098-153">Jeśli toocontinue nie jest planowane, użyj następującego polecenia toodelete hello wszystkie zasoby utworzone przez tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="07098-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="07098-154">Gdy pojawi się monit, wpisz `y`.</span><span class="sxs-lookup"><span data-stu-id="07098-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07098-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07098-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
