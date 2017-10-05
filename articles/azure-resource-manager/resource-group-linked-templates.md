---
title: "Link szablonów dla wdrożenia usługi Azure | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące używania szablonów połączonych w szablonie usługi Azure Resource Manager tworzenie rozwiązań moduły szablonu. Pokazuje, jak można przekazać wartości parametrów, określ plik parametrów i dynamicznie utworzone adresy URL."
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
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="fecc3-104">Korzystanie z szablonów połączonych w przypadku wdrażania zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fecc3-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="fecc3-105">Z jednego szablonu usługi Azure Resource Manager, można połączyć z innego szablonu, który umożliwia dekompozycji wdrożenia do zestawu z celem, szablony specyficzne dla celu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="fecc3-106">Tak jak w przypadku decomposing aplikację na kilku kod klasy, dekompozycji zapewnia korzyści w zakresie testowania, ponownemu i czytelność.</span><span class="sxs-lookup"><span data-stu-id="fecc3-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="fecc3-107">Można przekazać do połączonego szablonu parametry z głównym szablonu, a tych parametrów można bezpośrednio mapowania parametrów i zmiennych w szablonie wywoływania.</span><span class="sxs-lookup"><span data-stu-id="fecc3-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="fecc3-108">Połączone szablonu można również przekazać do zmiennej dane wyjściowe do szablonu źródła włączenie wymiany danych dwukierunkowej między szablonami.</span><span class="sxs-lookup"><span data-stu-id="fecc3-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="fecc3-109">Łączenie z szablonu</span><span class="sxs-lookup"><span data-stu-id="fecc3-109">Linking to a template</span></span>
<span data-ttu-id="fecc3-110">Możesz utworzyć łącza między dwa szablony, dodając zasobu wdrożenia w szablonie głównym wskazujące połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="fecc3-111">Możesz ustawić **templateLink** właściwości do identyfikatora URI połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="fecc3-112">Można podać wartości parametrów szablonu połączone, bezpośrednio w szablonie lub w pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="fecc3-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="fecc3-113">W poniższym przykładzie użyto **parametry** właściwości w celu określenia wartości parametru bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="fecc3-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

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

<span data-ttu-id="fecc3-114">Podobnie jak inne typy zasobów można ustawić zależności między połączonego szablonu i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="fecc3-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="fecc3-115">W związku z tym inne zasoby potrzebują wartość wyjściowa szablonu połączone, można upewnij się, że połączonego szablonu jest wdrożyć przed ich.</span><span class="sxs-lookup"><span data-stu-id="fecc3-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="fecc3-116">Lub, gdy szablon połączonego opiera się na inne zasoby, można upewnij się, że inne zasoby są wdrażane przed połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="fecc3-117">Można pobrać wartości z połączonych szablonu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="fecc3-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="fecc3-118">Usługa Resource Manager musi mieć możliwość dostępu do połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="fecc3-119">Nie można określić plik lokalny lub plik, który jest dostępny tylko w sieci lokalnej połączonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="fecc3-120">Możesz udostępniać wartość identyfikatora URI, która zawiera jedną **http** lub **https**.</span><span class="sxs-lookup"><span data-stu-id="fecc3-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="fecc3-121">Jedną z opcji jest umieszczenie szablonu połączonego na koncie magazynu i użyj identyfikatora URI dla tego elementu, tak jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="fecc3-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="fecc3-122">Mimo że połączonego szablonu musi być dostępny zewnętrznie, nie trzeba być ogólnie dostępne publicznie.</span><span class="sxs-lookup"><span data-stu-id="fecc3-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="fecc3-123">Możesz dodać do szablonu na konto magazynu prywatnego, który jest dostępny tylko dla właściciela konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="fecc3-124">Następnie można utworzyć token sygnatury dostępu Współdzielonego dostępu współdzielonego, aby umożliwić dostęp podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fecc3-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="fecc3-125">Identyfikator URI dla połączonych szablonu należy dodać tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="fecc3-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="fecc3-126">Aby uzyskać instrukcje na temat ustawiania szablonu na koncie magazynu i generowania tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md) lub [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fecc3-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="fecc3-127">W poniższym przykładzie przedstawiono szablonu nadrzędnego, który stanowi łącze do innego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="fecc3-128">Połączony jest uzyskiwany z tokenu sygnatury dostępu Współdzielonego, który jest przekazywana jako parametr.</span><span class="sxs-lookup"><span data-stu-id="fecc3-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="fecc3-129">Nawet jeśli token jest przekazywany jako bezpieczny ciąg, identyfikator URI szablonu połączone, wraz z tokenem sygnatury dostępu Współdzielonego są rejestrowane w operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fecc3-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="fecc3-130">W celu ograniczenia narażenia, ustawienia okresu ważności tokenu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="fecc3-131">Menedżer zasobów obsługuje każdego połączonego szablonu jako osobne wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fecc3-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="fecc3-132">W historii wdrożenia dla grupy zasobów zobacz temat oddzielnych wdrożeń nadrzędny i zagnieżdżone szablony.</span><span class="sxs-lookup"><span data-stu-id="fecc3-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![historia wdrażania](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="fecc3-134">Łączenie z pliku parametrów</span><span class="sxs-lookup"><span data-stu-id="fecc3-134">Linking to a parameter file</span></span>
<span data-ttu-id="fecc3-135">W następnym przykładzie użyto **parametersLink** właściwości, aby utworzyć link do pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="fecc3-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

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

<span data-ttu-id="fecc3-136">Wartość identyfikatora URI dla pliku połączonego parametru nie może być lokalny plik i musi zawierać albo **http** lub **https**.</span><span class="sxs-lookup"><span data-stu-id="fecc3-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="fecc3-137">Można też maksymalnie dostęp za pośrednictwem tokenu sygnatury dostępu Współdzielonego pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="fecc3-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="fecc3-138">Użycie zmiennych połączenia szablonów</span><span class="sxs-lookup"><span data-stu-id="fecc3-138">Using variables to link templates</span></span>
<span data-ttu-id="fecc3-139">W poprzednich przykładach pokazano zakodowanych wartości adresu URL dla łączy szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="fecc3-140">Takie podejście może działać w przypadku prostego szablonu, ale nie działa w przypadku pracy z dużym zestawem moduły szablonów.</span><span class="sxs-lookup"><span data-stu-id="fecc3-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="fecc3-141">Zamiast tego można utworzyć zmienną statyczną, przechowującym bazowy adres URL dla szablonu głównego, a następnie dynamicznie utworzyć adresów URL dla szablonów połączonych z tym podstawowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fecc3-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="fecc3-142">Zaletą tej metody jest można łatwo przenosić lub rozwidlania szablonu, ponieważ musisz zmienić zmienna statyczna w szablonie głównym.</span><span class="sxs-lookup"><span data-stu-id="fecc3-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="fecc3-143">Główny szablon przekazuje prawidłowe identyfikatory URI w szablonie rozłożone.</span><span class="sxs-lookup"><span data-stu-id="fecc3-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="fecc3-144">Poniższy przykład przedstawia sposób Użyj podstawowego adresu URL, aby utworzyć dwa adresy URL dla szablonów połączonych (**sharedTemplateUrl** i **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="fecc3-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="fecc3-145">Można również użyć [deployment()](resource-group-template-functions-deployment.md#deployment) uzyskać podstawowy adres URL dla bieżącego szablonu i używać, aby uzyskać adres URL dla innych szablonów w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fecc3-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="fecc3-146">Ta metoda jest przydatna, jeśli zmieni się lokalizację szablonu (być może z powodu versioning) lub aby uniknąć twardego kodowania adresów URL w pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="fecc3-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="fecc3-147">Pełny przykład</span><span class="sxs-lookup"><span data-stu-id="fecc3-147">Complete example</span></span>
<span data-ttu-id="fecc3-148">Następujące szablony przykład Pokaż uproszczony rozmieszczenie szablonów połączonych aby zilustrować niektóre pojęcia w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="fecc3-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="fecc3-149">Przyjęto założenie, że szablony zostały dodane do tego samego kontenera na koncie magazynu o dostępie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="fecc3-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="fecc3-150">Szablon połączonego przekazuje wartość z powrotem na główny szablonu w **generuje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="fecc3-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="fecc3-151">**Parent.json** plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="fecc3-151">The **parent.json** file consists of:</span></span>

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

<span data-ttu-id="fecc3-152">**Helloworld.json** plik zawiera:</span><span class="sxs-lookup"><span data-stu-id="fecc3-152">The **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="fecc3-153">W programie PowerShell możesz uzyskać token dla kontenera i wdrażać szablonów:</span><span class="sxs-lookup"><span data-stu-id="fecc3-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="fecc3-154">W programie Azure CLI 2.0 uzyskać token dla kontenera i wdrażanie szablonów z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="fecc3-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fecc3-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fecc3-155">Next steps</span></span>
* <span data-ttu-id="fecc3-156">Aby dowiedzieć się więcej na temat definiowania kolejność wdrażania zasobów, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="fecc3-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="fecc3-157">Aby dowiedzieć się, jak zdefiniować jeden zasób, ale utworzenia wielu wystąpień, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="fecc3-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

