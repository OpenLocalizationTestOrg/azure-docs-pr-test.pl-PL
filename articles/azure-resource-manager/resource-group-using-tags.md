---
title: "aaaTag Azure do zasobów organizacji logicznego | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak tooapply znaczniki tooorganize Azure zasoby dotyczące rozliczeń i zarządzania nimi."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="df158-103">Użyj tagów tooorganize zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="df158-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="df158-104">Można stosować tylko tooresources tagi, która obsługuje operacje usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="df158-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="df158-105">Jeśli utworzono maszyny wirtualnej, sieci wirtualnej lub konta magazynu za pośrednictwem hello klasycznego modelu wdrażania (takie jak za pomocą hello klasyczny portal Azure), nie można zastosować zasobów toothat tagu.</span><span class="sxs-lookup"><span data-stu-id="df158-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="df158-106">toosupport znakowanie, należy ponownie wdrożyć tych zasobów za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="df158-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="df158-107">Inne zasoby obsługują znakowanie.</span><span class="sxs-lookup"><span data-stu-id="df158-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="df158-108">Zasady spójności tag</span><span class="sxs-lookup"><span data-stu-id="df158-108">Policies for tag consistency</span></span>

<span data-ttu-id="df158-109">Standardowe reguły toocreate zasad zasobów można użyć dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="df158-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="df158-110">Można utworzyć zasad, które upewnij się, że zasoby są oznaczane hello odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="df158-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="df158-111">Aby uzyskać więcej informacji, zobacz [stosowania zasad zasobów dla tagów](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="df158-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="df158-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df158-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="df158-113">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="df158-113">Azure CLI</span></span>

<span data-ttu-id="df158-114">toosee hello znaczników dla *grupy zasobów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="df158-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="df158-115">Czy skrypt zwraca hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="df158-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="df158-116">toosee hello znaczników dla *zasób, który ma identyfikator określonego zasobu*, użyj:</span><span class="sxs-lookup"><span data-stu-id="df158-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="df158-117">Lub toosee hello znaczników dla *zasób, który ma nazwę, typ i zasobów do określonej grupy*, użyj:</span><span class="sxs-lookup"><span data-stu-id="df158-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="df158-118">Użyj tooget grupy zasobów, które mają konkretnego znacznika `az group list`:</span><span class="sxs-lookup"><span data-stu-id="df158-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="df158-119">tooget wszystkie zasoby hello, które mają określony tag i wartości, używają `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="df158-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="df158-120">Zawsze należy zastosować tagi tooa zasób lub grupa zasobów, należy zastąpić znaczników hello na tym zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="df158-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="df158-121">W związku z tym należy użyć innego podejścia opartego na czy hello zasób lub grupa zasobów ma znaczników.</span><span class="sxs-lookup"><span data-stu-id="df158-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="df158-122">tooadd znaczniki tooa *grupy zasobów bez znaczników*, użyj:</span><span class="sxs-lookup"><span data-stu-id="df158-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="df158-123">tooadd znaczniki tooa *zasobu bez znaczników*, użyj:</span><span class="sxs-lookup"><span data-stu-id="df158-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="df158-124">tooadd tagi tooa zasób, który ma już tagów, pobrać znaczników hello, sformatuj ponownie tę wartość i zastosuj je ponownie hello istniejących i nowych znaczników:</span><span class="sxs-lookup"><span data-stu-id="df158-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="df158-125">tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *nie zachować istniejące znaczniki zasobów hello*, użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="df158-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="df158-126">tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *zachować istniejące znaczniki zasobów*, użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="df158-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="df158-127">Szablony</span><span class="sxs-lookup"><span data-stu-id="df158-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="df158-128">Portal</span><span class="sxs-lookup"><span data-stu-id="df158-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="df158-129">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="df158-129">REST API</span></span>
<span data-ttu-id="df158-130">Witaj portalu Azure i programu PowerShell Użyj hello [interfejsu REST API usługi Resource Manager](https://docs.microsoft.com/rest/api/resources/) tle hello.</span><span class="sxs-lookup"><span data-stu-id="df158-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="df158-131">Toointegrate znakowanie do innego środowiska, należy tagów można uzyskać za pomocą **UZYSKAĆ** na hello identyfikator i aktualizacji hello zestawu zasobów tagów za pomocą **poprawka** wywołania.</span><span class="sxs-lookup"><span data-stu-id="df158-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="df158-132">Znaczniki i rozliczeń</span><span class="sxs-lookup"><span data-stu-id="df158-132">Tags and billing</span></span>
<span data-ttu-id="df158-133">Toogroup tagów można użyć danych rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="df158-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="df158-134">Na przykład jeśli używasz wielu maszyn wirtualnych w różnych organizacjach użycie hello tagi toogroup przez Centrum kosztów.</span><span class="sxs-lookup"><span data-stu-id="df158-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="df158-135">Umożliwia także koszty toocategorize tagi przez środowisko uruchomieniowe, takich jak hello rozliczeń użycia dla maszyn wirtualnych w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="df158-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="df158-136">Można pobrać informacji na temat tagów za pośrednictwem hello [użycia zasobów platformy Azure i interfejsów API RateCard](../billing/billing-usage-rate-card-overview.md) lub pliku wartości rozdzielanych przecinkami (CSV) użycia hello.</span><span class="sxs-lookup"><span data-stu-id="df158-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="df158-137">Pobieranie pliku użycia hello z hello [portalu konta usługi Azure](https://account.windowsazure.com/) lub [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df158-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="df158-138">Aby uzyskać więcej informacji o dostęp programistyczny toobilling informacji, zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df158-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="df158-139">Dla operacji interfejsu API REST, zobacz [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="df158-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="df158-140">Po pobraniu hello użycia woluminów CSV dla usług, które obsługują tagów z rozliczeniami hello znaczniki są wyświetlane w hello **tagi** kolumny.</span><span class="sxs-lookup"><span data-stu-id="df158-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="df158-141">Aby uzyskać więcej informacji, zobacz [zrozumieć rachunku platformy Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="df158-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Zobacz tagów w rozliczeń](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="df158-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df158-143">Next steps</span></span>
* <span data-ttu-id="df158-144">Za pomocą niestandardowych zasad można stosować ograniczenia i konwencje w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="df158-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="df158-145">Zasady, które należy zdefiniować może wymagać, że wszystkie zasoby mają wartość określony tag.</span><span class="sxs-lookup"><span data-stu-id="df158-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="df158-146">Aby uzyskać więcej informacji, zobacz [używają zasad toomanage zasobów i kontroli dostępu](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="df158-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="df158-147">Aby toousing wprowadzenie programu Azure PowerShell podczas wdrażania zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="df158-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="df158-148">Do wprowadzenia toousing hello Azure CLI podczas wdrażania zasobów, zobacz [hello Using Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="df158-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="df158-149">Wprowadzenie toousing hello portalu, zobacz [Using hello Azure toomanage portalu zasobów platformy Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df158-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="df158-150">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="df158-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

