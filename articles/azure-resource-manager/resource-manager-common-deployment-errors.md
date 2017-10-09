---
title: "typowe błędy wdrożenia usługi Azure aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooresolve typowe błędy podczas wdrażania tooAzure zasobów przy użyciu usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Błąd wdrażania, wdrożenia usługi azure wdrażanie tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="66518-104">Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66518-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="66518-105">W tym temacie opisano, jak może rozwiązać niektóre typowe mogą wystąpić błędy wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="66518-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="66518-106">w tym temacie opisano następujące kody błędów Hello:</span><span class="sxs-lookup"><span data-stu-id="66518-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="66518-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="66518-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="66518-108">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="66518-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="66518-109">Element BadRequest</span><span class="sxs-lookup"><span data-stu-id="66518-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="66518-110">Niepowodzenia wdrożenia</span><span class="sxs-lookup"><span data-stu-id="66518-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="66518-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="66518-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="66518-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="66518-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="66518-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="66518-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="66518-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="66518-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="66518-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="66518-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="66518-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="66518-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="66518-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="66518-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="66518-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="66518-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="66518-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="66518-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="66518-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="66518-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="66518-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="66518-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="66518-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="66518-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="66518-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="66518-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="66518-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="66518-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="66518-125">Niepowodzenia wdrożenia</span><span class="sxs-lookup"><span data-stu-id="66518-125">DeploymentFailed</span></span>

<span data-ttu-id="66518-126">Ten kod błędu wskazuje błąd ogólnego wdrożenia, ale nie jest to kod błędu hello należy toostart rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="66518-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="66518-127">Kod błędu Hello, która faktycznie pomaga rozwiązać problem hello jest zwykle jeden poziom w dół tego błędu.</span><span class="sxs-lookup"><span data-stu-id="66518-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="66518-128">Na przykład hello poniższy obraz przedstawia hello **RequestDisallowedByPolicy** kodu błędu, który podlega hello Błąd wdrażania.</span><span class="sxs-lookup"><span data-stu-id="66518-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![Pokaż kod błędu:](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="66518-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="66518-130">SkuNotAvailable</span></span>

<span data-ttu-id="66518-131">W przypadku wdrażania zasobów (zazwyczaj maszyny wirtualnej), może zostać wyświetlony powitania po błąd kodu i komunikatu o błędzie:</span><span class="sxs-lookup"><span data-stu-id="66518-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="66518-132">Ten błąd jest wyświetlany, gdy zasób hello SKU wybrano (takich jak rozmiar maszyny Wirtualnej) nie jest dostępny dla lokalizacji hello, wybrana przez Ciebie.</span><span class="sxs-lookup"><span data-stu-id="66518-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="66518-133">tooresolve ten problem, należy toodetermine jednostki SKU dostępnych w danym regionie.</span><span class="sxs-lookup"><span data-stu-id="66518-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="66518-134">Możesz użyć programu PowerShell, hello portal lub toofind operacji REST dostępne jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="66518-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="66518-135">Dla programu PowerShell, użyj [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) i Filtruj według lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="66518-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="66518-136">Musi mieć hello najnowszej wersji programu PowerShell dla tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="66518-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="66518-137">Witaj wyniki obejmują listę jednostek SKU dla lokalizacji hello i zastosowanie jakiekolwiek ograniczenia dotyczące tej wersji produktu.</span><span class="sxs-lookup"><span data-stu-id="66518-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="66518-138">Witaj toouse [portal](https://portal.azure.com), zaloguj się w portalu toohello i Dodaj zasób za pośrednictwem interfejsu hello.</span><span class="sxs-lookup"><span data-stu-id="66518-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="66518-139">Podczas określania wartości hello, zobacz hello dostępne jednostki SKU dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="66518-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="66518-140">Nie trzeba toocomplete hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="66518-140">You do not need toocomplete hello deployment.</span></span>

    ![dostępne jednostki SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="66518-142">Witaj toouse interfejsu API REST dla maszyn wirtualnych, Wyślij hello następujące żądania:</span><span class="sxs-lookup"><span data-stu-id="66518-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="66518-143">Zwraca dostępne jednostki SKU i regiony w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="66518-143">It returns available SKUs and regions in hello following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="66518-144">Jeśli toofind odpowiedniej jednostki SKU w tym regionie lub alternatywne region, który spełnia potrzeby biznesowe, przesłać [żądania SKU](https://aka.ms/skurestriction) tooAzure pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="66518-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="66518-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="66518-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="66518-146">Jeśli ten błąd jest wyświetlany, używasz subskrypcji, która nie jest dozwolone tooaccess dowolnych usług Azure innego niż Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66518-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="66518-147">Ten typ subskrypcji mogą wystąpić podczas musi tooaccess hello klasycznego portalu, ale nie są dozwolone toodeploy zasobów.</span><span class="sxs-lookup"><span data-stu-id="66518-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="66518-148">tooresolve ten problem, należy użyć subskrypcji, które ma uprawnienie toodeploy zasobów.</span><span class="sxs-lookup"><span data-stu-id="66518-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="66518-149">tooview dostępnych subskrypcji przy użyciu programu PowerShell, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="66518-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="66518-150">I tooset hello bieżącej subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="66518-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="66518-151">tooview dostępnych subskrypcji Azure CLI 2.0, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="66518-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="66518-152">I tooset hello bieżącej subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="66518-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="66518-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="66518-153">InvalidTemplate</span></span>
<span data-ttu-id="66518-154">Ten błąd może wynikać z kilku różnych typów błędów.</span><span class="sxs-lookup"><span data-stu-id="66518-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="66518-155">Błąd składni</span><span class="sxs-lookup"><span data-stu-id="66518-155">Syntax error</span></span>

   <span data-ttu-id="66518-156">Jeśli zostanie wyświetlony komunikat o błędzie wskazuje hello szablonu nie powiodła się weryfikacja, mogą mieć problem składni w szablonie.</span><span class="sxs-lookup"><span data-stu-id="66518-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="66518-157">Ten błąd jest łatwe toomake, ponieważ wyrażenia szablonu mogą być skomplikowanych.</span><span class="sxs-lookup"><span data-stu-id="66518-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="66518-158">Na przykład hello następującego przypisania nazwy dla konta magazynu zawiera jeden zestaw nawiasów, trzy funkcje trzy zestawy nawiasów, jeden zestaw apostrofy i jedną właściwość:</span><span class="sxs-lookup"><span data-stu-id="66518-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="66518-159">Jeśli nie zostanie określona hello Składnia dopasowania, hello szablon tworzy wartość, która różni się od masz zamiar.</span><span class="sxs-lookup"><span data-stu-id="66518-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="66518-160">Po otrzymaniu tego typu błędu, należy dokładnie przejrzeć hello składni wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="66518-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="66518-161">Należy wziąć pod uwagę przy użyciu edytora JSON, takich jak [programu Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) lub [Visual Studio Code](resource-manager-vs-code.md), który może zostać wyświetlone ostrzeżenie dotyczące błędy składniowe.</span><span class="sxs-lookup"><span data-stu-id="66518-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="66518-162">Niepoprawne segmentu długości</span><span class="sxs-lookup"><span data-stu-id="66518-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="66518-163">Inny błąd nieprawidłowego szablonu występuje, gdy hello Nazwa zasobu nie jest w poprawnym formacie hello.</span><span class="sxs-lookup"><span data-stu-id="66518-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="66518-164">Zasób poziomu głównego musi mieć jeden mniej segment nazwy hello niż hello typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="66518-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="66518-165">Każdy z segmentów odróżnia się kreską ułamkową.</span><span class="sxs-lookup"><span data-stu-id="66518-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="66518-166">W hello poniższy przykład, typ hello ma dwa segmenty i nazwa hello ma jeden segment, tak aby zawierała **prawidłową nazwę**.</span><span class="sxs-lookup"><span data-stu-id="66518-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="66518-167">Ale hello w następnym przykładzie **Nieprawidłowa nazwa** ponieważ ma ona hello samą liczbę segmentów jak hello typu.</span><span class="sxs-lookup"><span data-stu-id="66518-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="66518-168">Zasoby podrzędne hello typem i nazwą mieć hello samą liczbę segmentów.</span><span class="sxs-lookup"><span data-stu-id="66518-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="66518-169">Liczba segmentów ma sens, ponieważ hello pełną nazwę i typ podrzędny hello obejmuje hello nadrzędnego nazwę i typ.</span><span class="sxs-lookup"><span data-stu-id="66518-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="66518-170">W związku z tym hello Pełna nazwa nadal ma jeden segment mniej niż pełny typ hello.</span><span class="sxs-lookup"><span data-stu-id="66518-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="66518-171">Pobieranie segmentów hello prawo może być trudnych z typami Menedżera zasobów, które są stosowane przez dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="66518-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="66518-172">Na przykład stosowania witryny sieci web zasobu blokady tooa wymaga typu z czterech segmentów.</span><span class="sxs-lookup"><span data-stu-id="66518-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="66518-173">W związku z tym nazwa hello jest trzy segmenty:</span><span class="sxs-lookup"><span data-stu-id="66518-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="66518-174">Indeks kopiowania nie jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="66518-174">Copy index is not expected</span></span>

   <span data-ttu-id="66518-175">To wystąpią **InvalidTemplate** Błąd stosowania hello **kopiowania** elementu tooa część hello szablon, który nie obsługuje tego elementu.</span><span class="sxs-lookup"><span data-stu-id="66518-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="66518-176">Można stosować tylko typ zasobu tooa hello kopiowania elementu.</span><span class="sxs-lookup"><span data-stu-id="66518-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="66518-177">Nie można zastosować właściwości tooa kopiowania w ramach typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="66518-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="66518-178">Na przykład zastosować maszyny wirtualnej tooa kopiowania, ale nie można zastosować dysków toohello systemu operacyjnego dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="66518-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="66518-179">W niektórych przypadkach można przekonwertować podrzędnych zasobów tooa nadrzędnej zasobów toocreate pętlę kopiowania.</span><span class="sxs-lookup"><span data-stu-id="66518-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="66518-180">Aby uzyskać więcej informacji o używaniu kopiowania, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="66518-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="66518-181">Parametr jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="66518-181">Parameter is not valid</span></span>

   <span data-ttu-id="66518-182">Jeśli szablon hello Określa dozwolone wartości parametru, a następnie podaj wartość, która nie jest jednym z tych wartości, zostanie wyświetlony komunikat toohello podobne, następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="66518-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="66518-183">Sprawdź hello dozwolone wartości w szablonie hello i podaj jeden podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="66518-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="66518-184">Wykryto zależność cykliczną</span><span class="sxs-lookup"><span data-stu-id="66518-184">Circular dependency detected</span></span>

   <span data-ttu-id="66518-185">Ten błąd jest wyświetlany, gdy zasoby są zależne od siebie nawzajem w sposób uniemożliwiający wdrożenia hello uruchamianiu.</span><span class="sxs-lookup"><span data-stu-id="66518-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="66518-186">Kombinacja zależnościami sprawia, że dwa lub więcej zasobów, poczekaj, aż inne zasoby, które są również oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="66518-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="66518-187">Na przykład zasób1 zależy od resource3 zasób2 zależy od zasób1 i resource3 zależy od zasób2.</span><span class="sxs-lookup"><span data-stu-id="66518-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="66518-188">Zazwyczaj można rozwiązać ten problem, usuwając zbędne zależności.</span><span class="sxs-lookup"><span data-stu-id="66518-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="66518-189">NotFound i ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="66518-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="66518-190">Jeśli szablon zawiera nazwę hello zasobu, którego nie można rozwiązać, komunikat o błędzie podobny do:</span><span class="sxs-lookup"><span data-stu-id="66518-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="66518-191">Jeśli próbujesz hello toodeploy Brak zasobów w szablonie hello, sprawdź, czy potrzebujesz tooadd zależności.</span><span class="sxs-lookup"><span data-stu-id="66518-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="66518-192">Menedżer zasobów optymalizuje wdrożenia przez utworzenie zasobów równoległe, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="66518-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="66518-193">Jeśli jeden zasób należy wdrożyć po inny zasób, należy toouse hello **dependsOn** element toocreate Twojego szablonu w zależności od hello innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="66518-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="66518-194">Na przykład w przypadku wdrażania aplikacji sieci web, musi istnieć hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66518-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="66518-195">Jeśli nie określono tej aplikacji sieci web hello jest zależna od hello planu usługi aplikacji, usługi Resource Manager tworzy oba zasoby w hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="66518-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="66518-196">Pojawi się komunikat o błędzie informujący tego hello, którego nie można odnaleźć zasobu planu usługi aplikacji, ponieważ nie istnieje jeszcze podczas próby tooset właściwość hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="66518-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="66518-197">Ustawiając hello zależności w aplikacji sieci web hello zapobiec wystąpieniu tego błędu.</span><span class="sxs-lookup"><span data-stu-id="66518-197">You prevent this error by setting hello dependency in hello web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="66518-198">Aby sugestie dotyczące rozwiązywania problemów z błędami zależności, zobacz [Sprawdź wdrożenia sekwencji](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="66518-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="66518-199">Gdy hello zasób istnieje w innej grupie zasobów niż hello jedną wdrażane na również wyświetlenie tego błędu.</span><span class="sxs-lookup"><span data-stu-id="66518-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="66518-200">W takim przypadku należy użyć hello [funkcja resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello pełni kwalifikowana nazwa zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="66518-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="66518-201">Jeśli próba toouse hello [odwołania](resource-group-template-functions-resource.md#reference) lub [listKeys](resource-group-template-functions-resource.md#listkeys) funkcje z zasobów, których nie można rozpoznać, zostanie wyświetlony następujący błąd hello:</span><span class="sxs-lookup"><span data-stu-id="66518-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="66518-202">Wyszukaj wyrażenie, które zawiera hello **odwołania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="66518-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="66518-203">Sprawdź, czy wartości parametrów hello są poprawne.</span><span class="sxs-lookup"><span data-stu-id="66518-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="66518-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="66518-204">ParentResourceNotFound</span></span>

<span data-ttu-id="66518-205">Gdy jeden zasób jest zasobem nadrzędnej tooanother, zasobu nadrzędnego hello musi istnieć przed utworzeniem hello zasobu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="66518-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="66518-206">Jeśli go jeszcze nie istnieje, zostanie wyświetlony hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="66518-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="66518-207">Nazwa Hello hello podrzędnych zasobu zawiera nazwę nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="66518-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="66518-208">Na przykład można zdefiniować jako bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="66518-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="66518-209">Jednak jeśli nie określisz zależność od zasobu nadrzędnego hello, zasobu podrzędnego hello może wdrożony przed hello nadrzędną.</span><span class="sxs-lookup"><span data-stu-id="66518-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="66518-210">tooresolve ten błąd, obejmują zależności.</span><span class="sxs-lookup"><span data-stu-id="66518-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="66518-211">StorageAccountAlreadyExists i StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="66518-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="66518-212">W przypadku kont magazynu należy podać nazwę zasobu hello, która jest unikatowa w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66518-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="66518-213">Jeśli nie zapewnia unikatową nazwę, komunikat o błędzie takich jak:</span><span class="sxs-lookup"><span data-stu-id="66518-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="66518-214">Można utworzyć unikatowej nazwy przez łączenie z wynikiem hello hello Konwencja nazewnictwa [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji.</span><span class="sxs-lookup"><span data-stu-id="66518-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="66518-215">W przypadku wdrożenia konto magazynu z hello sam nazwę istniejącego konta magazynu w ramach subskrypcji, ale Podaj inną lokalizację, komunikat o błędzie wskazuje konta magazynu hello istnieje już w innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="66518-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="66518-216">Usuń istniejące konto magazynu hello, lub podaj hello tej samej lokalizacji, ponieważ hello istniejącego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="66518-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="66518-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="66518-217">AccountNameInvalid</span></span>
<span data-ttu-id="66518-218">Zobacz hello **AccountNameInvalid** wystąpił błąd podczas próby toogive nazwę, która zawiera konta magazynu zabronione znaki.</span><span class="sxs-lookup"><span data-stu-id="66518-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="66518-219">Nazwy konta magazynu musi należeć do zakresu od 3 do 24 znaków i korzystać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="66518-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="66518-220">Witaj [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcja zwraca 13 znaków.</span><span class="sxs-lookup"><span data-stu-id="66518-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="66518-221">Jeśli łączenie toohello prefiks **uniqueString** wyniku, podaj prefiks, który jest 11 znaków lub mniej.</span><span class="sxs-lookup"><span data-stu-id="66518-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="66518-222">Element BadRequest</span><span class="sxs-lookup"><span data-stu-id="66518-222">BadRequest</span></span>

<span data-ttu-id="66518-223">Stan element BadRequest mogą wystąpić, gdy zawierają nieprawidłową wartość dla właściwości.</span><span class="sxs-lookup"><span data-stu-id="66518-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="66518-224">Na przykład, jeśli podasz niepoprawną wartość jednostki SKU dla konta magazynu hello wdrożenie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="66518-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="66518-225">toodetermine prawidłowe wartości dla właściwości, obejrzyj hello [interfejsu API REST](/rest/api) dla typu zasobu hello jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="66518-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="66518-226">NoRegisteredProviderFound i MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="66518-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="66518-227">Podczas wdrażania zasobu, mogą otrzymywać hello następującego kodu błędu i komunikatów:</span><span class="sxs-lookup"><span data-stu-id="66518-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="66518-228">Lub może zostać wyświetlony komunikat podobny:</span><span class="sxs-lookup"><span data-stu-id="66518-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="66518-229">Te błędy dla jednego z trzech powodów:</span><span class="sxs-lookup"><span data-stu-id="66518-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="66518-230">Dostawca zasobów Hello nie została zarejestrowana dla Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="66518-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="66518-231">Wersja interfejsu API nie jest obsługiwana dla typu zasobu hello</span><span class="sxs-lookup"><span data-stu-id="66518-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="66518-232">Lokalizacja nie jest obsługiwana dla typu zasobu hello</span><span class="sxs-lookup"><span data-stu-id="66518-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="66518-233">komunikat o błędzie Hello powinien zapewnić sugestie dotyczące hello obsługiwane lokalizacje i wersje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="66518-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="66518-234">Możesz zmienić tooone Twojego szablonu z hello sugerowane wartości.</span><span class="sxs-lookup"><span data-stu-id="66518-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="66518-235">Większość dostawców są rejestrowane automatycznie przez hello Azure portalu lub hello interfejsu wiersza polecenia, którego używasz, ale nie wszystkich.</span><span class="sxs-lookup"><span data-stu-id="66518-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="66518-236">Jeśli nie używasz dostawcy określonego zasobu przed, może być konieczne tooregister tego dostawcę.</span><span class="sxs-lookup"><span data-stu-id="66518-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="66518-237">Użytkownik może dowiedzieć się więcej o dostawców zasobów za pomocą programu PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66518-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="66518-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="66518-238">**Portal**</span></span>

<span data-ttu-id="66518-239">Możesz wyświetlić hello stanu rejestracji i zarejestrować przestrzeń nazw dostawcy zasobów za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="66518-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="66518-240">Dla Twojej subskrypcji, wybierz **dostawców zasobów**.</span><span class="sxs-lookup"><span data-stu-id="66518-240">For your subscription, select **Resource providers**.</span></span>

   ![Wybierz dostawców zasobów](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="66518-242">Spójrz na powitania listę dostawców zasobów i w razie potrzeby wybierz hello **zarejestrować** dostawcy zasobów hello tooregister łącza typu hello próbujesz toodeploy.</span><span class="sxs-lookup"><span data-stu-id="66518-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![Lista dostawców zasobów](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="66518-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="66518-244">**PowerShell**</span></span>

<span data-ttu-id="66518-245">toosee stan rejestracji, użyj **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="66518-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="66518-246">Użyj tooregister dostawcy, **AzureRmResourceProvider rejestru** i podaj nazwę hello dostawcy zasobów hello mają tooregister.</span><span class="sxs-lookup"><span data-stu-id="66518-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="66518-247">tooget hello obsługiwane lokalizacje dla określonego typu zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="66518-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="66518-248">Witaj tooget obsługiwane wersje interfejsu API dla określonego typu zasobu, użyj:</span><span class="sxs-lookup"><span data-stu-id="66518-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="66518-249">**Interfejs wiersza polecenia platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="66518-249">**Azure CLI**</span></span>

<span data-ttu-id="66518-250">toosee, czy dostawca hello jest zarejestrowany, użyj hello `azure provider list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66518-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="66518-251">tooregister dostawcy zasobów, użyj hello `azure provider register` polecenia, a następnie określ hello *przestrzeni nazw* tooregister.</span><span class="sxs-lookup"><span data-stu-id="66518-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="66518-252">Użyj toosee hello obsługiwane lokalizacje i wersje interfejsu API dla typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="66518-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="66518-253">QuotaExceeded i OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="66518-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="66518-254">Problemy mogą wystąpić podczas wdrażania przekracza limit przydziału, który może być według grupy zasobów, subskrypcje, konta i innych zakresów.</span><span class="sxs-lookup"><span data-stu-id="66518-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="66518-255">Na przykład dana subskrypcja może być skonfigurowany toolimit hello liczba rdzeni dla regionu.</span><span class="sxs-lookup"><span data-stu-id="66518-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="66518-256">Jeśli toodeploy maszynę wirtualną o większej liczby rdzeni niż dozwolona kwota hello, wystąpi błąd, który określania hello została przekroczona.</span><span class="sxs-lookup"><span data-stu-id="66518-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="66518-257">Przydział pełne informacje, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="66518-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="66518-258">tooexamine przydziały swoją subskrypcję dla rdzeni, możesz użyć hello `azure vm list-usage` w hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66518-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="66518-259">Witaj poniższy przykład przedstawia ten limit przydziału rdzeni hello bezpłatne konto próbne jest 4:</span><span class="sxs-lookup"><span data-stu-id="66518-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="66518-260">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="66518-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="66518-261">Jeśli wdrożono szablon, który tworzy więcej niż cztery rdzenie hello regionu zachodnie stany USA, można uzyskać Błąd wdrażania, która wygląda jak:</span><span class="sxs-lookup"><span data-stu-id="66518-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="66518-262">W programie PowerShell, możesz użyć hello **Get-AzureRmVMUsage** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66518-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="66518-263">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="66518-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="66518-264">W takich przypadkach możesz Przejdź toohello portalu i pliku limitu przydziału dla regionu hello, do którego będzie toodeploy tooraise problem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="66518-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="66518-265">Należy pamiętać, grup zasobów, limitu przydziału hello jest dla poszczególnych regionów, nie dla całej subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="66518-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="66518-266">Jeśli potrzebujesz toodeploy 30 rdzeni zachodnie stany USA, masz tooask dla 30 rdzeni Resource Manager zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="66518-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="66518-267">Jeśli potrzebujesz toodeploy 30 rdzeni w jednym z toowhich regionów hello masz dostęp, należy poprosić dla 30 rdzeni Resource Manager we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="66518-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="66518-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="66518-268">InvalidContentLink</span></span>
<span data-ttu-id="66518-269">Gdy pojawi się komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="66518-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="66518-270">Prawdopodobnie podjęto toolink tooa zagnieżdżonych szablon, który nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="66518-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="66518-271">Sprawdź hello przewidzianych hello zagnieżdżony szablon identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="66518-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="66518-272">Jeśli szablon hello istnieje na koncie magazynu, upewnij się, że hello identyfikatora URI jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="66518-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="66518-273">Może być konieczne toopass tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="66518-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="66518-274">Aby uzyskać więcej informacji, zobacz [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md) (Używanie szablonów połączonych w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="66518-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="66518-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="66518-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="66518-276">Ten błąd jest wyświetlany, gdy Twoja subskrypcja obejmuje uniemożliwiający akcji próbujesz tooperform podczas wdrażania zasad zasobów.</span><span class="sxs-lookup"><span data-stu-id="66518-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="66518-277">W komunikacie o błędzie hello Wyszukaj identyfikator zasad hello.</span><span class="sxs-lookup"><span data-stu-id="66518-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="66518-278">W **PowerShell**, podaj identyfikator zasad jako hello **identyfikator** parametru tooretrieve szczegóły hello zasad zablokowane wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="66518-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="66518-279">W **interfejsu wiersza polecenia Azure**, podaj nazwę hello hello definicji zasad:</span><span class="sxs-lookup"><span data-stu-id="66518-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="66518-280">Aby uzyskać więcej informacji zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="66518-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="66518-281">RequestDisallowedByPolicy error (Błąd RequestDisallowedByPolicy)</span><span class="sxs-lookup"><span data-stu-id="66518-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="66518-282">[Korzystanie z zasobów toomanage zasad i kontrola dostępu](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="66518-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="66518-283">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="66518-283">Authorization failed</span></span>
<span data-ttu-id="66518-284">Ponieważ hello konta lub głównej próby toodeploy hello zasobów usługi nie ma dostępu tooperform tych czynności może zostać wyświetlony błąd podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="66518-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="66518-285">Usługa Azure Active Directory umożliwia toocontrol Twojego administratora, tożsamości, które mają dostęp do zasobów, jakie precyzyjną precyzji.</span><span class="sxs-lookup"><span data-stu-id="66518-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="66518-286">Na przykład jeśli konto jest przypisaną rolę czytelnika toohello, nie jesteś toocreate stanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="66518-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="66518-287">W takim przypadku zostanie wyświetlony komunikat o błędzie wskazujący, że autoryzacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="66518-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="66518-288">Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach, zobacz [kontroli dostępu](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="66518-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="66518-289">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="66518-289">Next steps</span></span>
* <span data-ttu-id="66518-290">toolearn o inspekcji akcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="66518-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="66518-291">toolearn o błędach hello toodetermine akcje podczas wdrażania, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="66518-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
