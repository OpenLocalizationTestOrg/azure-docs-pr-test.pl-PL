---
title: "Szablony aaaLink dla wdrożenia usługi Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse połączone szablonów w toocreate szablonu usługi Azure Resource Manager rozwiązania moduły szablonu. Pokazuje, jak toopass wartości parametrów, określ plik parametrów i tworzone dynamicznie adresów URL."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="7c6f0-104">Korzystanie z szablonów połączonych w przypadku wdrażania zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c6f0-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="7c6f0-105">Z jednego szablonu usługi Azure Resource Manager, możesz połączyć tooanother szablonu, który pozwala toodecompose wdrożenia do zestawu docelowego, specyficzne dla celu szablonów.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="7c6f0-106">Tak jak w przypadku decomposing aplikację na kilku kod klasy, dekompozycji zapewnia korzyści w zakresie testowania, ponownemu i czytelność.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="7c6f0-107">Należy przekazać parametry szablonu połączonego tooa szablonu głównego, a te parametry można zamapować bezpośrednio, tooparameters lub zmiennych w hello wywoływania szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="7c6f0-108">Szablon połączonego Hello można również przekazać szablonu źródła zmiennej toohello wstecz dane wyjściowe, włączanie wymiany danych dwukierunkowej między szablonami.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="7c6f0-109">Łączenie tooa szablonu</span><span class="sxs-lookup"><span data-stu-id="7c6f0-109">Linking tooa template</span></span>
<span data-ttu-id="7c6f0-110">Możesz utworzyć łącza między dwa szablony przez dodanie do zasobu wdrożenia w szablonie głównym hello toohello punktów połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="7c6f0-111">Ustaw hello **templateLink** toohello właściwość URI hello połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="7c6f0-112">Można podać wartości parametrów szablonu połączonego hello, bezpośrednio w szablonie lub w pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="7c6f0-113">Witaj poniższym przykładzie użyto hello **parametry** toospecify właściwości bezpośrednio wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="7c6f0-114">Podobnie jak inne typy zasobów można ustawić zależności między hello połączonego szablonu i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="7c6f0-115">W związku z tym inne zasoby potrzebują wartość wyjściowa szablonu połączonego hello, można upewnij się, że wdrożeniu szablonu połączonego hello przed ich.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="7c6f0-116">Lub, gdy szablon połączonego hello opiera się na inne zasoby, można upewnij się, że inne zasoby są wdrażane przed hello połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="7c6f0-117">Można pobrać wartości z połączonych szablonu z hello składni:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="7c6f0-118">Hello usługi Resource Manager musi być możliwe tooaccess hello połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="7c6f0-119">Nie można określić plik lokalny lub plik, który jest dostępny tylko w sieci lokalnej hello połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="7c6f0-120">Możesz udostępniać wartość identyfikatora URI, która zawiera jedną **http** lub **https**.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="7c6f0-121">Jedną z opcji jest tooplace szablonu połączonego konta magazynu, i użyj hello identyfikatora URI dla tego elementu, takie jak pokazano na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="7c6f0-122">Mimo że hello połączonego szablonu musi być dostępny zewnętrznie, nie musi toobe publicznego toohello ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="7c6f0-123">Można dodać konta magazynu prywatnego tooa szablonu, który jest właścicielem konta magazynu hello tooonly dostępny.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="7c6f0-124">Następnie można utworzyć dostępu tooenable tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="7c6f0-125">Możesz dodać tego SAS tokenu toohello URI hello połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="7c6f0-126">Aby uzyskać instrukcje na temat ustawiania szablonu na koncie magazynu i generowania tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md) lub [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7c6f0-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="7c6f0-127">Witaj poniższy przykład przedstawia szablonu nadrzędnego szablonu tooanother łącza.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="7c6f0-128">Witaj połączony jest uzyskiwany z tokenu sygnatury dostępu Współdzielonego, który jest przekazywana jako parametr.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="7c6f0-129">Mimo że hello token jest przekazywany jako bezpieczny ciąg, hello URI szablonu połączonego hello, w tym hello tokenu sygnatury dostępu Współdzielonego, są rejestrowane w hello operacje wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="7c6f0-130">narażenia toolimit, ustawienia okresu ważności tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="7c6f0-131">Menedżer zasobów obsługuje każdego połączonego szablonu jako osobne wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="7c6f0-132">W historii wdrożenia hello hello grupy zasobów można zobaczyć oddzielnych wdrożeń hello nadrzędny i zagnieżdżone szablony.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![historia wdrażania](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="7c6f0-134">Łączenie pliku parametrów tooa</span><span class="sxs-lookup"><span data-stu-id="7c6f0-134">Linking tooa parameter file</span></span>
<span data-ttu-id="7c6f0-135">Witaj następnym przykładzie użyto hello **parametersLink** pliku parametrów tooa toolink właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="7c6f0-136">Hello URI wartość hello parametru połączonego pliku nie może być lokalny plik i musi zawierać albo **http** lub **https**.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="7c6f0-137">plik parametrów Hello może być również ograniczony tooaccess za pośrednictwem tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="7c6f0-138">Za pomocą szablonów toolink zmiennych</span><span class="sxs-lookup"><span data-stu-id="7c6f0-138">Using variables toolink templates</span></span>
<span data-ttu-id="7c6f0-139">Witaj poprzednich przykładach pokazano zakodowanych wartości adresu URL dla hello szablon łączy.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="7c6f0-140">Takie podejście może działać w przypadku prostego szablonu, ale nie działa w przypadku pracy z dużym zestawem moduły szablonów.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="7c6f0-141">Zamiast tego można utworzyć zmienną statyczną, przechowującym bazowy adres URL dla szablonu głównego hello, a następnie dynamicznie utworzyć adresów URL dla szablonów hello połączone z tym podstawowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="7c6f0-142">Możesz z łatwością przenoszenia lub rozwidlenia szablonu hello ponieważ wystarczy zmienna statyczna hello toochange w szablonie głównym hello jest Hello zaletą tej metody.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="7c6f0-143">Szablon głównego Hello przekazuje hello prawidłowe identyfikatory URI w całym hello rozłożone szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="7c6f0-144">Witaj poniższy przykład przedstawia sposób toouse podstawowej toocreate adres URL dwa adresy URL dla połączonych szablonów (**sharedTemplateUrl** i **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="7c6f0-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="7c6f0-145">Można również użyć [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello podstawowego adresu URL dla bieżącego szablonu hello i używać tego adresu URL hello tooget innych szablonów w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="7c6f0-146">Ta metoda jest przydatna, jeśli zmieni się lokalizację szablonu (być może z powodu tooversioning) lub ma tooavoid twardych kodowania adresów URL w pliku szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="7c6f0-147">Pełny przykład</span><span class="sxs-lookup"><span data-stu-id="7c6f0-147">Complete example</span></span>
<span data-ttu-id="7c6f0-148">następujące szablony przykład Hello Pokaż tooillustrate szablonów połączonych w układzie uproszczony kilka pojęć hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="7c6f0-149">Zakłada się, że szablony hello dodano toohello tego samego kontenera na koncie magazynu o dostępie jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="7c6f0-150">Szablon połączonego Hello przekazuje szablonie głównym wstecz toohello wartości w hello **generuje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="7c6f0-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="7c6f0-151">Witaj **parent.json** plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-151">hello **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="7c6f0-152">Witaj **helloworld.json** plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-152">hello **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="7c6f0-153">W programie PowerShell możesz uzyskać token dla kontenera hello i wdrażać hello szablonów:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="7c6f0-154">W programie Azure CLI 2.0 uzyskać token dla kontenera hello i wdrażanie szablonów hello z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7c6f0-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="7c6f0-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c6f0-155">Next steps</span></span>
* <span data-ttu-id="7c6f0-156">toolearn o hello określające kolejność wdrażania hello zasobów, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="7c6f0-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="7c6f0-157">toolearn toodefine jeden zasób, ale utworzenia wielu wystąpień, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="7c6f0-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

