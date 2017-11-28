---
title: Usuwanie klastra platformy Azure i jej zasobach | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak Aby całkowicie usunąć klastra usługi sieć szkieletowa, usunięcie grupy zasobów, zawierającą klaster lub selektywne usuwanie zasobów."
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="80031-103">Usuwanie klastra sieci szkieletowej usług na platformie Azure i zasobów, które są używane</span><span class="sxs-lookup"><span data-stu-id="80031-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="80031-104">Klastra usługi sieć szkieletowa składa się z wielu innych zasobów platformy Azure oprócz samego zasobu klastra.</span><span class="sxs-lookup"><span data-stu-id="80031-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="80031-105">Dlatego też, aby całkowicie usunąć klaster usługi Service Fabric, musisz również usunąć wszystkie zasoby, z których się składa.</span><span class="sxs-lookup"><span data-stu-id="80031-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="80031-106">Dostępne są dwie opcje: albo Usuń grupę zasobów, który znajduje się w klastrze (który usuwa zasób klastra i innych zasobów w grupie zasobów) lub usunięcie zasobu klastra, w szczególności i związany z zasobów (, ale nie innych zasobów w grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="80031-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="80031-107">Usuwanie zasobu klastra **nie** usunąć wszystkie zasoby, które klastra usługi sieć szkieletowa składa się z.</span><span class="sxs-lookup"><span data-stu-id="80031-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="80031-108">Usuń grupę zasobów całej (grupy zasobów), należącego do klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="80031-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="80031-109">To jest najprostszym sposobem, aby upewnić się, że należy usunąć wszystkie zasoby, które są skojarzone z klastrem, w tym grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="80031-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="80031-110">Można usunąć grupy zasobów, przy użyciu programu PowerShell lub za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="80031-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="80031-111">Jeśli grupa zasobów zawiera zasoby, które nie są związane z klastrem usługi sieć szkieletowa, można usunąć określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="80031-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="80031-112">Usuń grupę zasobów, przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80031-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="80031-113">Możesz także usunąć grupy zasobów, uruchamiając następujące polecenia cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80031-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="80031-114">Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="80031-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="80031-115">Jeśli nie zostało zrobione to przed, wykonaj czynności opisane w temacie [sposób instalowania i konfigurowania programu Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="80031-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="80031-116">Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS:</span><span class="sxs-lookup"><span data-stu-id="80031-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="80031-117">Zostanie wyświetlony monit o potwierdzenie usunięcia, jeśli nie używasz *-Force* opcji.</span><span class="sxs-lookup"><span data-stu-id="80031-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="80031-118">Na potwierdzenie zarządcy zasobów i wszystkie zasoby, które zawiera zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="80031-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="80031-119">Usuń grupę zasobów, w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80031-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="80031-120">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80031-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="80031-121">Przejdź do klastra usługi Service Fabric, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="80031-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="80031-122">Kliknij nazwę grupy zasobów na stronie essentials klastra.</span><span class="sxs-lookup"><span data-stu-id="80031-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="80031-123">Spowoduje to wyświetlenie **Essentials grupy zasobów** strony.</span><span class="sxs-lookup"><span data-stu-id="80031-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="80031-124">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="80031-124">Click **Delete**.</span></span>
6. <span data-ttu-id="80031-125">Postępuj zgodnie z instrukcjami na stronie Kończenie procesu usuwania grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="80031-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Usuń grupę zasobów][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="80031-127">Usuń zasób klastra i zasoby, które są używane, ale nie innych zasobów w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="80031-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="80031-128">Jeśli grupa zasobów zawiera tylko tych zasobów, które są powiązane z klastra sieci szkieletowej usług, które chcesz usunąć, następnie łatwiej można usunąć grupy zasobów całej.</span><span class="sxs-lookup"><span data-stu-id="80031-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="80031-129">Jeśli chcesz selektywnie usunąć jeden po drugim zasoby w grupie zasobów, należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="80031-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="80031-130">Jeśli wdrożono klastra za pomocą portalu lub przy użyciu jednego z szablonów usługi sieć szkieletowa Resource Manager z galerii szablonów z następujących dwóch tagów są oznakowane wszystkie zasoby używane przez klaster.</span><span class="sxs-lookup"><span data-stu-id="80031-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="80031-131">Można używać ich, aby zdecydować, które zasoby, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="80031-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="80031-132">***Tag #1:*** klucz = Nazwa_klastra, wartość = "Nazwa klastra"</span><span class="sxs-lookup"><span data-stu-id="80031-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="80031-133">***Tag #2:*** klucz = resourceName, wartość = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="80031-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="80031-134">Usuwanie określonych zasobów w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80031-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="80031-135">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80031-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="80031-136">Przejdź do klastra usługi Service Fabric, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="80031-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="80031-137">Przejdź do **wszystkie ustawienia** w bloku essentials.</span><span class="sxs-lookup"><span data-stu-id="80031-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="80031-138">Polecenie **tagi** w obszarze **zarządzanie zasobami** w bloku ustawienia.</span><span class="sxs-lookup"><span data-stu-id="80031-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="80031-139">Kliknij jeden z **tagi** w bloku tagów, aby uzyskać listę wszystkich zasobów z tym znacznikiem.</span><span class="sxs-lookup"><span data-stu-id="80031-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Tagi zasobów][ResourceTags]
6. <span data-ttu-id="80031-141">Po utworzeniu listy zasobów oznakowany, kliknij każdy z zasobów i usuń je.</span><span class="sxs-lookup"><span data-stu-id="80031-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Oznakowane zasobów][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="80031-143">Usuwanie zasobów przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80031-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="80031-144">Możesz usunąć zasoby po kolei, uruchamiając następujące polecenia cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80031-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="80031-145">Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="80031-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="80031-146">Jeśli nie zostało zrobione to przed, wykonaj czynności opisane w temacie [sposób instalowania i konfigurowania programu Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="80031-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="80031-147">Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS:</span><span class="sxs-lookup"><span data-stu-id="80031-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="80031-148">Dla każdego z zasobów chcesz usunąć, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="80031-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="80031-149">Aby usunąć zasobu klastra, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="80031-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="80031-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80031-150">Next steps</span></span>
<span data-ttu-id="80031-151">Przeczytaj następujące również informacje na temat uaktualniania klastra i partycjonowanie usług:</span><span class="sxs-lookup"><span data-stu-id="80031-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="80031-152">Więcej informacji na temat uaktualnienia klastra</span><span class="sxs-lookup"><span data-stu-id="80031-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="80031-153">Więcej informacji na temat partycjonowania usługi stanowej maksymalną skalę</span><span class="sxs-lookup"><span data-stu-id="80031-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
