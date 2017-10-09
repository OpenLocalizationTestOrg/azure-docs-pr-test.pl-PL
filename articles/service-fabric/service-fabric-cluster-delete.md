---
title: "aaaDelete Azure klastra i jego zasobów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, w jaki sposób usuwania toocompletely usługi sieć szkieletowa klastra albo usunięcie grupy zasobów hello zawierające hello klastra lub przez selektywne usuwanie zasobów."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="20186-103">Usuwanie klastra sieci szkieletowej usług Azure i hello zasobów, które są używane</span><span class="sxs-lookup"><span data-stu-id="20186-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="20186-104">Klastra usługi sieć szkieletowa składa się z wielu zasobów platformy Azure dodatkowo zasobu klastra toohello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="20186-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="20186-105">Dlatego toocompletely Usuwanie klastra sieci szkieletowej usług należy również toodelete hello wszystkie zasoby, które składa się z.</span><span class="sxs-lookup"><span data-stu-id="20186-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="20186-106">Dostępne są dwie opcje: albo grupa zasobów hello delete hello klastra (który usuwa hello zasobu klastra i innych zasobów w grupie zasobów hello) lub specjalnie usunąć zasobu klastra hello i związany z zasobów (ale nie innych zasoby w grupie zasobów hello).</span><span class="sxs-lookup"><span data-stu-id="20186-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="20186-107">Usuwanie zasobu klastra hello **nie** Usuń wszystkie hello inne zasoby, które klastra usługi sieć szkieletowa składa się z.</span><span class="sxs-lookup"><span data-stu-id="20186-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="20186-108">Usuń grupę zasobów całej hello (zarządcy zasobów), który hello klaster znajduje się w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="20186-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="20186-109">Jest to najprostszy tooensure sposób hello, aby usunąć wszystkie zasoby hello skojarzony z klastrem, w tym hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20186-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="20186-110">Można usunąć grupy zasobów hello przy użyciu programu PowerShell lub za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="20186-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="20186-111">Jeśli grupa zasobów zawiera zasoby, które nie są powiązane tooService klastra sieci szkieletowej, można usunąć określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="20186-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="20186-112">Usuń grupę zasobów hello przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20186-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="20186-113">Można również usunąć hello grupy zasobów, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="20186-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="20186-114">Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="20186-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="20186-115">Jeśli nie zostało zrobione to przed, wykonaj kroki hello opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="20186-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="20186-116">Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS hello:</span><span class="sxs-lookup"><span data-stu-id="20186-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="20186-117">Otrzymasz usunięcia hello tooconfirm monitu, jeśli nie używasz hello *-Force* opcji.</span><span class="sxs-lookup"><span data-stu-id="20186-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="20186-118">Na potwierdzenie hello zarządcy zasobów i zostaną usunięte wszystkie zasoby hello, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="20186-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="20186-119">Usuń grupę zasobów w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="20186-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="20186-120">Toohello logowania [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20186-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="20186-121">Przejdź toohello klastra sieci szkieletowej usług ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="20186-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="20186-122">Powitania kliknij nazwę grupy zasobów na stronie essentials klastra hello.</span><span class="sxs-lookup"><span data-stu-id="20186-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="20186-123">Spowoduje to wyświetlenie hello **Essentials grupy zasobów** strony.</span><span class="sxs-lookup"><span data-stu-id="20186-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="20186-124">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="20186-124">Click **Delete**.</span></span>
6. <span data-ttu-id="20186-125">Wykonaj instrukcje hello na usunięcie hello toocomplete strony tego hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20186-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Usuń grupę zasobów][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="20186-127">Usuń zasób klastra hello i hello zasoby, które są używane, ale nie innych zasobów w grupie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="20186-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="20186-128">Jeśli grupa zasobów zawiera tylko tych zasobów, które są powiązane toohello klastra sieci szkieletowej usług ma toodelete, a następnie jest łatwiejsze toodelete hello całej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20186-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="20186-129">Jeśli chcesz tooselectively delete hello zasobów jeden po drugim w grupie zasobów, następnie wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="20186-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="20186-130">Jeśli wdrożono klastra przy użyciu portalu hello lub jednego z szablonów usługi sieć szkieletowa Resource Manager hello z galerii szablonów hello wszystkie zasoby hello hello używa klastra są oznaczone tagiem hello następujące dwa tagi.</span><span class="sxs-lookup"><span data-stu-id="20186-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="20186-131">Można ich używać toodecide zasobów, do których chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="20186-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="20186-132">***Tag #1:*** klucz = Nazwa_klastra, wartość = "Nazwa klastra hello"</span><span class="sxs-lookup"><span data-stu-id="20186-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="20186-133">***Tag #2:*** klucz = resourceName, wartość = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="20186-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="20186-134">Usuń wybrane zasoby hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="20186-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="20186-135">Toohello logowania [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20186-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="20186-136">Przejdź toohello klastra sieci szkieletowej usług ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="20186-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="20186-137">Przejdź za**wszystkie ustawienia** na powitania essentials bloku.</span><span class="sxs-lookup"><span data-stu-id="20186-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="20186-138">Polecenie **tagi** w obszarze **zarządzanie zasobami** w bloku ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="20186-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="20186-139">Kliknij jeden z hello **tagi** w hello tagi bloku tooget listę wszystkich zasobów hello z tym znacznikiem.</span><span class="sxs-lookup"><span data-stu-id="20186-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Tagi zasobów][ResourceTags]
6. <span data-ttu-id="20186-141">Po utworzeniu listy hello oznakowanych zasobów, kliknij każdy z zasobów hello i usuń je.</span><span class="sxs-lookup"><span data-stu-id="20186-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Oznakowane zasobów][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="20186-143">Usuwanie zasobów hello przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20186-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="20186-144">Możesz usunąć zasoby powitania po kolei, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="20186-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="20186-145">Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="20186-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="20186-146">Jeśli nie zostało zrobione to przed, wykonaj kroki hello opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="20186-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="20186-147">Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS hello:</span><span class="sxs-lookup"><span data-stu-id="20186-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="20186-148">Dla każdego z zasobów hello mają toodelete, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="20186-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="20186-149">toodelete hello zasobu klastra, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="20186-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="20186-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20186-150">Next steps</span></span>
<span data-ttu-id="20186-151">Po tooalso hello odczytu więcej informacji na temat uaktualniania klastra i partycjonowania usługi:</span><span class="sxs-lookup"><span data-stu-id="20186-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="20186-152">Więcej informacji na temat uaktualnienia klastra</span><span class="sxs-lookup"><span data-stu-id="20186-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="20186-153">Więcej informacji na temat partycjonowania usługi stanowej maksymalną skalę</span><span class="sxs-lookup"><span data-stu-id="20186-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
