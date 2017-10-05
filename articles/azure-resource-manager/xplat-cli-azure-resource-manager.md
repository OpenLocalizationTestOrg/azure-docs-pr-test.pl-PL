---
title: "Zarządzanie zasobami za pomocą wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Umożliwia zarządzanie zasobami platformy Azure i grup Azure interfejsu wiersza polecenia (CLI)"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="4f4ca-103">Użyj wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów</span><span class="sxs-lookup"><span data-stu-id="4f4ca-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f4ca-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4f4ca-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="4f4ca-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4f4ca-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="4f4ca-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f4ca-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="4f4ca-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4f4ca-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="4f4ca-108">Interfejs wiersza polecenia platformy Azure (Azure CLI) jest jednym z kilku narzędzi można użyć do wdrożenia i zarządzania zasobami za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="4f4ca-109">W tym artykule przedstawiono typowe sposoby zarządzania zasobami Azure i grup zasobów przy użyciu wiersza polecenia platformy Azure w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="4f4ca-110">Aby dowiedzieć się, jak wdrażanie zasobów za pomocą interfejsu wiersza polecenia, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="4f4ca-111">Ogólne dotyczące zasobów platformy Azure i Menedżer zasobów, odwiedź stronę [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4f4ca-112">Do zarządzania zasobami Azure z wiersza polecenia platformy Azure, musisz [instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md), i [logowanie do platformy Azure](../xplat-cli-connect.md) przy użyciu `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="4f4ca-113">Upewnij się, że interfejsu wiersza polecenia jest w trybie Menedżera zasobów (Uruchom `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="4f4ca-114">Po wykonaniu tych czynności możesz rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="4f4ca-115">Pobieranie grup zasobów i zasoby</span><span class="sxs-lookup"><span data-stu-id="4f4ca-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="4f4ca-116">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="4f4ca-116">Resource groups</span></span>
<span data-ttu-id="4f4ca-117">Aby uzyskać listę wszystkich grup zasobów w Twojej subskrypcji i ich lokalizacje, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="4f4ca-118">Zasoby</span><span class="sxs-lookup"><span data-stu-id="4f4ca-118">Resources</span></span>
 <span data-ttu-id="4f4ca-119">Aby wyświetlić listę wszystkich zasobów w grupie, takie jak jedną o nazwie *testRG*, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="4f4ca-120">Aby wyświetlić poszczególnych zasobów w grupie, takie jak maszyny Wirtualnej o nazwie *MyUbuntuVM*, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="4f4ca-121">Powiadomienie **Microsoft.Compute/virtualMachines** parametru.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="4f4ca-122">Ten parametr określa typ zasobu, którego chcesz uzyskać informacje na.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="4f4ca-123">Korzystając z **zasobów platformy azure** polecenia innych niż **listy** polecenia, należy określić wersję interfejsu API zasobu z **-o** parametru.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="4f4ca-124">Jeśli nie wiesz o wersji interfejsu API, zapoznaj się z pliku szablonu i znajdź pole apiVersion zasobu.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="4f4ca-125">Aby uzyskać więcej informacji o wersji interfejsu API w Menedżerze zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="4f4ca-126">Podczas wyświetlania szczegółowych informacji w zasobie, często jest przydatne do użycia `--json` parametru.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="4f4ca-127">Ten parametr sprawia, że dane wyjściowe bardziej czytelny, ponieważ niektóre wartości są zagnieżdżone struktury lub kolekcji.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="4f4ca-128">W poniższym przykładzie pokazano zwracania wyników z **Pokaż** polecenie jako dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="4f4ca-129">Jeśli chcesz, Zapisz dane JSON do pliku przy użyciu &gt; znak Przekieruj dane wyjściowe do pliku.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="4f4ca-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="4f4ca-131">Tagi</span><span class="sxs-lookup"><span data-stu-id="4f4ca-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="4f4ca-132">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="4f4ca-132">Manage resources</span></span>
<span data-ttu-id="4f4ca-133">Aby dodać zasobów, takich jak konta magazynu do grupy zasobów, uruchom polecenie podobne do:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="4f4ca-134">Oprócz określanie wersji interfejsu API zasobu z **-o** parametru, użyj **-p** parametr do przekazania w formacie JSON ciąg z każdego wymaganego lub dodatkowych właściwości.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="4f4ca-135">Aby usunąć istniejący zasób usługi takie jak zasobu maszyny wirtualnej, użyj polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="4f4ca-136">Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć **przenoszenia zasobów platformy azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="4f4ca-137">Poniższy przykład przedstawia sposób przenoszenia pamięci podręcznej Redis do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="4f4ca-138">W **-i** parametru, podaj jego rozdzielana przecinkami lista identyfikator zasobu można przenieść.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="4f4ca-139">Kontrolowanie dostępu do zasobów</span><span class="sxs-lookup"><span data-stu-id="4f4ca-139">Control access to resources</span></span>
<span data-ttu-id="4f4ca-140">Tworzenie zasad i zarządzania nimi na kontrolowanie dostępu do zasobów platformy Azure, można użyć wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="4f4ca-141">Aby uzyskać ogólne informacje o definicji zasad oraz przypisywania zasad do zasobów, zobacz [za pomocą zasad zarządzania zasobami i kontrola dostępu](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="4f4ca-142">Na przykład zdefiniować następujące zasady odrzucanie wszystkich żądań, w którym lokalizacja nie jest zachodnie stany USA lub północno-środkowe Stany i zapisać go w policy.json pliku definicji zasad:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="4f4ca-143">Następnie uruchom **utworzenia definicji zasad** polecenia:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="4f4ca-144">To polecenie przedstawia dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="4f4ca-145">Utworzenie definicji zasad danych MyPolicy: PolicyName: dane MyPolicy: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="4f4ca-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="4f4ca-146">dane: PolicyType: danych niestandardowych: Nazwa wyświetlana: niezdefiniowana danych: Opis: niezdefiniowana danych: klasa PolicyRule: pole = lokalizacji, w = [westus, northcentralus], efekt = Odmów</span><span class="sxs-lookup"><span data-stu-id="4f4ca-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="4f4ca-147">Aby przypisać zasad w zakresie ma, użyj **PolicyDefinitionId** zwrócone przez poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="4f4ca-148">W poniższym przykładzie ten zakres jest subskrypcji, ale można przejść do grupy zasobów lub pojedynczych zasobów:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="4f4ca-149">MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### utworzenia przypisania zasad Azure /</span><span class="sxs-lookup"><span data-stu-id="4f4ca-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="4f4ca-150">Można uzyskać, Zmień lub Usuń definicje zasad przy użyciu **Pokaż definicji zasad**, **zestaw definicji zasad**, i **usunąć definicji zasad** poleceń.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="4f4ca-151">Podobnie można uzyskać, zmienianie lub usuwanie przypisania zasady przy użyciu **Pokaż przypisania zasad**, **zestawie przypisania zasad**, i **Usuń przypisanie zasad** poleceń.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="4f4ca-152">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="4f4ca-152">Export a resource group as a template</span></span>
<span data-ttu-id="4f4ca-153">W przypadku istniejącej grupy zasobów można wyświetlać szablonu usługi Resource Manager dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="4f4ca-154">Eksportowanie szablonu oferuje dwie korzyści:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="4f4ca-155">Można łatwo automatyzować przyszłych wdrożeń rozwiązania, ponieważ cała infrastruktura jest zdefiniowany w szablonie.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="4f4ca-156">Należy zaznajomić się ze składnią szablonu analizując JSON, który reprezentuje rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="4f4ca-157">Przy użyciu wiersza polecenia platformy Azure, możesz wyeksportować szablon, który reprezentuje bieżący stan grupy zasobów, lub Pobierz szablon, który był używany dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="4f4ca-158">**Eksportowanie szablonu dla grupy zasobów** — jest to przydatne, gdy wprowadziło zmiany w grupie zasobów i musi pobrać reprezentacja JSON w jego bieżącym stanie.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="4f4ca-159">Jednak wygenerowanego szablonu zawiera tylko z minimalnej liczby parametrów i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="4f4ca-160">Większość wartości w szablonie są zakodowane na stałe.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="4f4ca-161">Przed wdrożeniem wygenerowanego szablonu, możesz przekonwertować więcej wartości parametrów, można dostosować wdrożenia dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="4f4ca-162">Aby wyeksportować szablon dla grupy zasobów w katalogu lokalnym, uruchom `azure group export` polecenia, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="4f4ca-163">(Zastępuje katalog lokalny odpowiednie dla danego środowiska systemu operacyjnego).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="4f4ca-164">**Pobierz szablon dla konkretnego wdrożenia** — jest to przydatne, gdy chcesz wyświetlić rzeczywiste szablon, który został użyty do wdrożenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="4f4ca-165">Szablon zawiera wszystkie parametry i zmienne zdefiniowane dla oryginalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="4f4ca-166">Jednak jeśli ktoś w organizacji wprowadzone zmiany w grupie zasobów poza definicją w szablonie, ten szablon nie zawiera bieżący stan grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="4f4ca-167">Aby pobrać szablon używany do konkretnego wdrożenia do katalogu lokalnego, uruchom `azure group deployment template download` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="4f4ca-168">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4f4ca-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="4f4ca-169">Eksportowanie szablonu jest w wersji zapoznawczej, a nie wszystkich typów zasobów nie obsługiwało eksportowania szablonu.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="4f4ca-170">Podczas próby eksportowania szablonu, może zostać wyświetlony błąd informujący, że niektóre zasoby nie zostały wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="4f4ca-171">Jeśli to konieczne, ręcznie zdefiniować te zasoby do szablonu po pobraniu jej.</span><span class="sxs-lookup"><span data-stu-id="4f4ca-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4f4ca-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f4ca-172">Next steps</span></span>
* <span data-ttu-id="4f4ca-173">Aby uzyskać szczegółowe informacje o operacji wdrażania i rozwiązywanie problemów z błędy wdrożenia przy użyciu wiersza polecenia platformy Azure, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="4f4ca-174">Jeśli chcesz użyć interfejsu wiersza polecenia do konfigurowania aplikacji lub skryptu dostęp do zasobów, zobacz [użyć wiersza polecenia platformy Azure można utworzyć nazwy głównej usługi dostępu do zasobów](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="4f4ca-175">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="4f4ca-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

