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
# <a name="create-your-first-function-using-hello-azure-cli"></a>Utwórz swoją pierwszą funkcję przy użyciu hello wiersza polecenia platformy Azure

Ten samouczek szybkiego startu przedstawia procedury toocreate usługi Azure Functions toouse swoją pierwszą funkcję. Możesz użyć hello Azure CLI toocreate aplikacji funkcji, który jest hello bez serwera infrastruktury, który jest hostem funkcji. Witaj funkcja kodu jest wdrażany z repozytorium GitHub próbki.    

Możesz wykonać kroki hello za pomocą komputera Mac, systemu Windows lub Linux. 

## <a name="prerequisites"></a>Wymagania wstępne 

Przed uruchomieniem tego przykładu, musi mieć następujące hello:

+ Aktywne konto usługi [GitHub](https://github.com). 
+ Aktywna subskrypcja platformy Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje funkcji, bazy danych i konta magazynu, oraz zarządzania nimi.

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup`.  
Jeśli nie korzystasz z usługi Cloud Shell, musisz się najpierw zalogować za pomocą polecenia `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage

Funkcje używa toomaintain stan konta magazynu Azure i inne informacje dotyczące funkcji. Utwórz konto magazynu w grupie zasobów hello został utworzony za pomocą hello [Tworzenie konta magazynu az](/cli/azure/storage/account#create) polecenia.

Hello następujące polecenia, podstawić własną nazwę konta magazynu unikatowych której występuje hello `<storage_name>` symbolu zastępczego. Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Po utworzeniu konta magazynu hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

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

## <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

Funkcja aplikacji toohost hello wykonywanie funkcji są wymagane. Aplikacja funkcji Hello zapewnia środowisko niekorzystającą wykonywania kodu funkcji. Umożliwia ona grupowanie funkcji w ramach jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi. Tworzenie aplikacji funkcji przy użyciu hello [az functionapp utworzyć](/cli/azure/functionapp#create) polecenia. 

Hello następujące polecenia, Zastąp własną nazwą aplikacji unique — funkcja, której występuje hello `<app_name>` symbolu zastępczego i hello nazwy konta magazynu dla `<storage_name>`. Witaj `<app_name>` jest używany jako domyślnej domeny DNS dla aplikacji funkcja hello i tak nazwy hello hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Domyślnie aplikacja funkcji jest tworzony z hello zużycie hostingu planu, co oznacza, że zasoby są dodawane dynamicznie, co jest wymagane przez funkcji i płacisz tylko po uruchomieniu funkcji. Aby uzyskać więcej informacji, zobacz [plan hostingu poprawne hello wybierz](functions-scale.md). 

Po utworzeniu aplikacji funkcji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

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

Teraz, gdy masz aplikacji funkcji, można wdrożyć kod rzeczywista funkcja hello z repozytorium przykładowej GitHub hello.

## <a name="deploy-your-function-code"></a>Wdrażanie kodu funkcji  

Istnieje kilka sposobów toocreate funkcja kodu w nowej aplikacji funkcji. W tym temacie łączy tooa próbki repozytorium w usłudze GitHub. Jak wcześniej w hello następującego kodu Zastąp hello `<app_name>` symbolu zastępczego o nazwie hello hello funkcji aplikacji został utworzony. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Po wdrożeniu hello źródła została ustawiona, powitalne interfejsu wiersza polecenia Azure zawiera informacje o toohello podobnie poniższy przykład (usunąć dla czytelności wartości null):

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

## <a name="test-hello-function"></a>Funkcja hello testu

Funkcja cURL tootest hello wdrożona na komputerze Mac lub Linux lub przy użyciu Bash w systemie Windows. Wykonanie następującego polecenia cURL, zastępując hello hello `<app_name>` symbolu zastępczego o nazwie hello funkcji aplikacji. Dołącz ciągu zapytania hello `&name=<yourname>` toohello adresu URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Jeśli nie jest dostępne w wierszu polecenia cURL, wprowadź hello tego samego adresu URL hello adresu przeglądarki sieci web. Ponownie, Zastąp hello `<app_name>` symbolu zastępczego o nazwie hello funkcji aplikacji i Dołącz ciągu zapytania hello `&name=<yourname>` toohello adresu URL i wykonać hello żądania. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Inne przewodniki Szybki start w tej kolekcji bazują na tym przewodniku. Jeśli planujesz toocontinue toowork kolejne Przewodniki Szybki Start lub hello samouczki, czy nie wyczyścić zasoby hello utworzone w tym Szybki Start. Jeśli toocontinue nie jest planowane, użyj następującego polecenia toodelete hello wszystkie zasoby utworzone przez tego przewodnika Szybki Start:

```azurecli-interactive
az group delete --name myResourceGroup
```
Gdy pojawi się monit, wpisz `y`.

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
