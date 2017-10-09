---
title: "aaaManage zasobów przy użyciu interfejsu wiersza polecenia Azure hello | Dokumentacja firmy Microsoft"
description: "Użyj hello toomanage Azure interfejsu wiersza polecenia (CLI) Azure zasobów i grup"
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="a0bf0-103">Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów</span><span class="sxs-lookup"><span data-stu-id="a0bf0-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0bf0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a0bf0-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="a0bf0-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0bf0-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a0bf0-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0bf0-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a0bf0-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a0bf0-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="a0bf0-108">Witaj interfejsu wiersza polecenia platformy Azure (Azure CLI) jest jednym z kilku narzędzi można użyć toodeploy i zarządzanie zasobami za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="a0bf0-109">W tym artykule przedstawiono typowe sposoby toomanage Azure zasobów i grup zasobów za pomocą interfejsu wiersza polecenia Azure hello w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="a0bf0-110">Uzyskać informacji o używaniu hello CLI toodeploy zasobów, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="a0bf0-111">Ogólne dotyczące zasobów platformy Azure i Menedżer zasobów, odwiedź stronę hello [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0bf0-112">toomanage Azure zasoby z hello wiersza polecenia platformy Azure, należy za[zainstalować hello Azure CLI](../cli-install-nodejs.md), i [Zaloguj tooAzure](../xplat-cli-connect.md) przy użyciu hello `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="a0bf0-113">Utwórz hello się, że interfejs wiersza polecenia jest w trybie Menedżera zasobów (Uruchom `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="a0bf0-114">Po wykonaniu tych czynności możesz toogo gotowe.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="a0bf0-115">Pobieranie grup zasobów i zasoby</span><span class="sxs-lookup"><span data-stu-id="a0bf0-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="a0bf0-116">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="a0bf0-116">Resource groups</span></span>
<span data-ttu-id="a0bf0-117">tooget listę wszystkich grup zasobów w Twojej subskrypcji i ich lokalizacje, uruchom to polecenie.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="a0bf0-118">Zasoby</span><span class="sxs-lookup"><span data-stu-id="a0bf0-118">Resources</span></span>
 <span data-ttu-id="a0bf0-119">nazwy wszystkich zasobów w grupie, takie jak jeden z toolist *testRG*, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="a0bf0-120">tooview poszczególnych zasobów w ramach grupy hello, np. maszyna wirtualna o nazwie *MyUbuntuVM*, użyj polecenia takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="a0bf0-121">Powiadomienie hello **Microsoft.Compute/virtualMachines** parametru.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="a0bf0-122">Ten parametr wskazuje typ hello hello zasób, którego chcesz uzyskać informacje na.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bf0-123">Korzystając z hello **zasobów platformy azure** polecenia niż hello **listy** polecenia, należy określić hello interfejsu API w wersji hello zasobu z hello **-o** parametru.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="a0bf0-124">Jeśli nie wiesz o wersji interfejsu API hello, zapoznaj się hello pliku szablonu i znajdź pole apiVersion hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="a0bf0-125">Aby uzyskać więcej informacji o wersji interfejsu API w Menedżerze zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="a0bf0-126">Podczas wyświetlania szczegółowych informacji w zasobie, często jest przydatne toouse hello `--json` parametru.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="a0bf0-127">Ten parametr sprawia, że dane wyjściowe hello bardziej czytelny, ponieważ niektóre wartości są zagnieżdżone struktury lub kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="a0bf0-128">Witaj poniższym przykładzie pokazano zwracająca wyniki hello hello **Pokaż** polecenie jako dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="a0bf0-129">Jeśli chcesz, Zapisz toofile danych JSON hello przy użyciu hello &gt; pliku tooa wyjściowego hello toodirect znaków.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="a0bf0-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="a0bf0-131">Tagi</span><span class="sxs-lookup"><span data-stu-id="a0bf0-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="a0bf0-132">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="a0bf0-132">Manage resources</span></span>
<span data-ttu-id="a0bf0-133">tooadd zasobów, takich jak grupy zasobów tooa konta magazynu, uruchom polecenie podobne do:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="a0bf0-134">Ponadto toospecifying hello wersja interfejsu API hello zasobu z hello **-o** parametru, użyj hello **-p** parametru toopass w formacie JSON ciąg z każdego wymaganego lub dodatkowych właściwości.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="a0bf0-135">toodelete istniejącego zasobu, takie jak zasobu maszyny wirtualnej, należy użyć polecenia takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="a0bf0-136">toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello **przenoszenia zasobów platformy azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="a0bf0-137">powitania po przykładzie pokazano, jak toomove pamięci podręcznej Redis tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="a0bf0-138">W hello **-i** parametru zawierają identyfikator zasobu hello toomove listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="a0bf0-139">Kontrola dostępu tooresources</span><span class="sxs-lookup"><span data-stu-id="a0bf0-139">Control access tooresources</span></span>
<span data-ttu-id="a0bf0-140">Można użyć hello toocreate wiersza polecenia platformy Azure i zarządzanie zasobami tooAzure dostępu toocontrol zasad.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="a0bf0-141">Aby uzyskać ogólne informacje o definicji zasad i przypisywanie tooresources zasad, zobacz [używają zasad toomanage zasobów i kontroli dostępu](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="a0bf0-142">Na przykład zdefiniować następujące zasady toodeny hello wszystkie żądania, w którym lokalizacja nie jest zachodnie stany USA lub północno-środkowe Stany i zapisać go policy.json pliku definicji zasad toohello:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="a0bf0-143">Następnie uruchom hello **utworzenia definicji zasad** polecenia:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="a0bf0-144">To polecenie przedstawia dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="a0bf0-145">Utworzenie definicji zasad danych MyPolicy: PolicyName: dane MyPolicy: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="a0bf0-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="a0bf0-146">dane: PolicyType: danych niestandardowych: Nazwa wyświetlana: niezdefiniowana danych: Opis: niezdefiniowana danych: klasa PolicyRule: pole = lokalizacji, w = [westus, northcentralus], efekt = Odmów</span><span class="sxs-lookup"><span data-stu-id="a0bf0-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="a0bf0-147">tooassign zasad w zakresie hello ma, użyj hello **PolicyDefinitionId** zwrócony z hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="a0bf0-148">W hello poniższy przykład ten zakres jest hello subskrypcji, ale można określić zakres grupy tooresource lub pojedynczych zasobów:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="a0bf0-149">MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### utworzenia przypisania zasad Azure /</span><span class="sxs-lookup"><span data-stu-id="a0bf0-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="a0bf0-150">Można uzyskać, Zmień lub Usuń definicje zasad przy użyciu hello **Pokaż definicji zasad**, **zestaw definicji zasad**, i **usunąć definicji zasad** poleceń.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="a0bf0-151">Podobnie można uzyskać, zmienianie lub usuwanie przypisania zasady przy użyciu hello **Pokaż przypisania zasad**, **zestawie przypisania zasad**, i **Usuń przypisanie zasad** poleceń .</span><span class="sxs-lookup"><span data-stu-id="a0bf0-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="a0bf0-152">Eksportowanie grupy zasobów jako szablon</span><span class="sxs-lookup"><span data-stu-id="a0bf0-152">Export a resource group as a template</span></span>
<span data-ttu-id="a0bf0-153">W przypadku istniejącej grupy zasobów można wyświetlać hello szablonu usługi Resource Manager dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="a0bf0-154">Eksportowanie szablonu hello oferuje dwie korzyści:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="a0bf0-155">Można łatwo automatyzować przyszłych wdrożeń hello rozwiązania, ponieważ wszystkie infrastruktury hello jest zdefiniowany w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="a0bf0-156">Należy zaznajomić o składni szablonu analizując hello JSON, który reprezentuje rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="a0bf0-157">Przy użyciu hello wiersza polecenia platformy Azure, możesz wyeksportować szablon, który reprezentuje hello bieżący stan grupy zasobów, lub Pobierz szablon hello, które było używane dla konkretnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="a0bf0-158">**Eksportowanie szablonu powitania dla grupy zasobów** — jest to przydatne, gdy wprowadzone grupy zasobów tooa zmiany i konieczne tooretrieve hello reprezentacja JSON swojego bieżącego stanu.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="a0bf0-159">Jednak hello wygenerowanego szablonu zawiera tylko z minimalnej liczby parametrów i żadnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="a0bf0-160">Większość wartości hello w szablonie hello są zakodowane na stałe.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="a0bf0-161">Przed wdrożeniem hello wygenerowany szablonu, warto zapoznać się z tooconvert więcej wartości hello do parametrów, można dostosować hello wdrożenia dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="a0bf0-162">tooexport hello szablonu dla zasobu grupy tooa katalogiem lokalnym, uruchom hello `azure group export` polecenia, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="a0bf0-163">(Zastępuje katalog lokalny odpowiednie dla danego środowiska systemu operacyjnego).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="a0bf0-164">**Pobierz szablon powitania dla konkretnego wdrożenia** — jest to przydatne, gdy będziesz potrzebować tooview hello rzeczywiste szablon, który został toodeploy używane zasoby.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="a0bf0-165">Szablon Hello zawiera wszystkie parametry i zmienne zdefiniowane dla hello oryginalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="a0bf0-166">Jednak jeśli ktoś w organizacji grupę zasobów toohello zmiany poza definicji hello w szablonie hello, ten szablon nie zawiera bieżący stan hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="a0bf0-167">toodownload hello szablon używany do konkretnego wdrożenia tooa katalogiem lokalnym, uruchom hello `azure group deployment template download` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="a0bf0-168">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a0bf0-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="a0bf0-169">Eksportowanie szablonu jest w wersji zapoznawczej, a nie wszystkich typów zasobów nie obsługiwało eksportowania szablonu.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="a0bf0-170">Podczas próby tooexport szablonu, może zostać wyświetlony błąd informujący, że niektóre zasoby nie zostały wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="a0bf0-171">Jeśli to konieczne, ręcznie zdefiniować te zasoby do szablonu po pobraniu jej.</span><span class="sxs-lookup"><span data-stu-id="a0bf0-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a0bf0-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0bf0-172">Next steps</span></span>
* <span data-ttu-id="a0bf0-173">Szczegóły tooget operacje wdrażania i rozwiązywania problemów wdrożenia z hello wiersza polecenia platformy Azure, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="a0bf0-174">Toouse hello CLI tooset aplikacji lub skryptu tooaccess zasobów, zobacz [toocreate wiersza polecenia platformy Azure Użyj nazwy głównej usługi zasobów tooaccess](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="a0bf0-175">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a0bf0-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

