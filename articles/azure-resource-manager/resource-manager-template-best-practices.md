---
title: "aaaBest wskazówki dotyczące tworzenia szablonów usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Wytyczne dotyczące uproszczenia szablonów usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="95f50-103">Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95f50-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="95f50-104">Niniejsze wytyczne ułatwia tworzenie szablonów usługi Azure Resource Manager, które są toouse niezawodnych i prostych.</span><span class="sxs-lookup"><span data-stu-id="95f50-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="95f50-105">wskazówki Hello są tylko sugestie.</span><span class="sxs-lookup"><span data-stu-id="95f50-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="95f50-106">Nie są one wymagania, oprócz wskazanych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="95f50-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="95f50-107">Scenariusz może wymagać zmiany jednego hello podejścia lub przykłady.</span><span class="sxs-lookup"><span data-stu-id="95f50-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="95f50-108">Nazwy zasobów</span><span class="sxs-lookup"><span data-stu-id="95f50-108">Resource names</span></span>
<span data-ttu-id="95f50-109">Ogólnie rzecz biorąc pracować z trzech rodzajów nazw zasobów w Menedżerze zasobów:</span><span class="sxs-lookup"><span data-stu-id="95f50-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="95f50-110">Nazwy zasobów, które muszą być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="95f50-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="95f50-111">Nazwy zasobów, które nie są wymagane toobe unikatowy, ale możesz wybrać tooprovide nazwę, która może pomóc w identyfikacji zasobu na podstawie kontekstu.</span><span class="sxs-lookup"><span data-stu-id="95f50-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="95f50-112">Nazwy zasobów, które mogą być ogólne.</span><span class="sxs-lookup"><span data-stu-id="95f50-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="95f50-113">Aby uzyskać informacje o ograniczeniach nazw zasobów, zobacz [konwencje nazewnictwa dla zasobów platformy Azure zalecane](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="95f50-114">Nazwy zasobów unikatowy</span><span class="sxs-lookup"><span data-stu-id="95f50-114">Unique resource names</span></span>
<span data-ttu-id="95f50-115">Musisz podać nazwę zasobu unikatowy dla dowolnego typu zasobu, która zawiera punkt końcowy dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="95f50-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="95f50-116">Niektóre typowe typy zasobów, które wymagają unikatową nazwę obejmują:</span><span class="sxs-lookup"><span data-stu-id="95f50-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="95f50-117">Usługa Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="95f50-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="95f50-118">Funkcje aplikacji internetowych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="95f50-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="95f50-119">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="95f50-119">SQL Server</span></span>
* <span data-ttu-id="95f50-120">W usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="95f50-120">Azure Key Vault</span></span>
* <span data-ttu-id="95f50-121">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="95f50-121">Azure Redis Cache</span></span>
* <span data-ttu-id="95f50-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="95f50-122">Azure Batch</span></span>
* <span data-ttu-id="95f50-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="95f50-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="95f50-124">Azure Search</span><span class="sxs-lookup"><span data-stu-id="95f50-124">Azure Search</span></span>
* <span data-ttu-id="95f50-125">Usługa Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="95f50-125">Azure HDInsight</span></span>

<span data-ttu-id="95f50-126"><sup>1</sup> nazwy konta magazynu musi być także małe litery, 24 znaków lub mniej, a nie ma żadnych łączników.</span><span class="sxs-lookup"><span data-stu-id="95f50-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="95f50-127">Jeśli podasz nazwę zasobu parametr, Podaj unikatową nazwę podczas wdrażania zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="95f50-128">Opcjonalnie można utworzyć zmiennej, która używa hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate nazwę funkcji.</span><span class="sxs-lookup"><span data-stu-id="95f50-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="95f50-129">Możesz również mają tooadd prefiks lub sufiks toohello **uniqueString** wynik.</span><span class="sxs-lookup"><span data-stu-id="95f50-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="95f50-130">Modyfikowanie hello unikatową nazwę może pomóc więcej łatwo zidentyfikować hello typu zasobu na podstawie nazwy hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="95f50-131">Na przykład można wygenerować unikatowej nazwy dla konta magazynu przy użyciu następującej zmiennej hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="95f50-132">Nazwy zasobów do identyfikacji</span><span class="sxs-lookup"><span data-stu-id="95f50-132">Resource names for identification</span></span>
<span data-ttu-id="95f50-133">Niektóre typy zasobów może być tooname, ale ich nazwy nie mają toobe unikatowy.</span><span class="sxs-lookup"><span data-stu-id="95f50-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="95f50-134">W przypadku tych typów zasobów można Podaj nazwę, która identyfikuje zarówno hello zasobów kontekst, jak i hello typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="95f50-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="95f50-135">Wprowadź opisową nazwę, która pomaga w identyfikacji zasobów hello na liście zasobów.</span><span class="sxs-lookup"><span data-stu-id="95f50-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="95f50-136">Jeśli potrzebujesz toouse inną nazwę zasobu dla różnych wdrożeń można użyć parametru hello nazwy:</span><span class="sxs-lookup"><span data-stu-id="95f50-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="95f50-137">Jeśli nie potrzebują toopass w nazwie podczas wdrażania, można użyć zmiennej:</span><span class="sxs-lookup"><span data-stu-id="95f50-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="95f50-138">Można także użyć wartości stałe:</span><span class="sxs-lookup"><span data-stu-id="95f50-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="95f50-139">Nazwy zasobów ogólnych</span><span class="sxs-lookup"><span data-stu-id="95f50-139">Generic resource names</span></span>
<span data-ttu-id="95f50-140">Dla typów zasobów, które przede wszystkim uzyskują dostęp za pomocą innego zasobu można użyć nazwy ogólnej, który jest ustalony w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="95f50-141">Na przykład można ustawić nazwę standardowego, ogólne reguły zapory na serwerze SQL server:</span><span class="sxs-lookup"><span data-stu-id="95f50-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="95f50-142">Parametry</span><span class="sxs-lookup"><span data-stu-id="95f50-142">Parameters</span></span>
<span data-ttu-id="95f50-143">Witaj następujące informacje mogą być pomocne podczas pracy z parametrów:</span><span class="sxs-lookup"><span data-stu-id="95f50-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="95f50-144">Zminimalizować korzystanie z parametrów.</span><span class="sxs-lookup"><span data-stu-id="95f50-144">Minimize your use of parameters.</span></span> <span data-ttu-id="95f50-145">Jeśli to możliwe, należy użyć zmiennej lub wartość literału.</span><span class="sxs-lookup"><span data-stu-id="95f50-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="95f50-146">Parametry tylko dla tych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="95f50-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="95f50-147">Ustawienia, które mają toouse zmian zgodnie z tooenvironment (jednostka SKU, rozmiar, pojemności).</span><span class="sxs-lookup"><span data-stu-id="95f50-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="95f50-148">Nazwy zasobów ma toospecify ułatwiający identyfikację.</span><span class="sxs-lookup"><span data-stu-id="95f50-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="95f50-149">Wartości użycie często toocomplete inne zadania (takie jak nazwa użytkownika administratora).</span><span class="sxs-lookup"><span data-stu-id="95f50-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="95f50-150">Klucze tajne (takie jak hasła).</span><span class="sxs-lookup"><span data-stu-id="95f50-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="95f50-151">numer Hello lub tablicy toouse wartości podczas tworzenia wielu wystąpień typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="95f50-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="95f50-152">Użyj formatu camelcase dla nazw parametrów.</span><span class="sxs-lookup"><span data-stu-id="95f50-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="95f50-153">Podaj opis każdego parametru w metadanych hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="95f50-154">Zdefiniuj wartości domyślne parametrów (z wyjątkiem hasła i klucze SSH):</span><span class="sxs-lookup"><span data-stu-id="95f50-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="95f50-155">Użyj **SecureString** dla wszystkich hasła i klucze tajne:</span><span class="sxs-lookup"><span data-stu-id="95f50-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="95f50-156">Jeśli to możliwe, nie używaj lokalizacji toospecify parametru.</span><span class="sxs-lookup"><span data-stu-id="95f50-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="95f50-157">Zamiast tego należy użyć hello **lokalizacji** właściwości hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="95f50-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="95f50-158">Za pomocą hello **resourceGroup () .location** wyrażenie dla wszystkich zasobów, zasobów w szablonie hello są wdrażane w tej samej lokalizacji co grupa zasobów hello hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="95f50-159">Jeśli typ zasobu jest obsługiwana w ograniczonej liczby miejsc, można toospecify bezpośrednio w szablonie hello prawidłową lokalizację.</span><span class="sxs-lookup"><span data-stu-id="95f50-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="95f50-160">Jeśli musisz użyć **lokalizacji** parametru udostępniać tę wartość parametru możliwie zasoby, które są prawdopodobnie toobe w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="95f50-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="95f50-161">Pozwala to zmniejszyć hello liczba użytkownicy są proszeni tooprovide informacji o lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="95f50-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="95f50-162">Unikaj używania parametr lub zmienna hello wersji interfejsu API dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="95f50-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="95f50-163">Właściwości zasobów i wartości może się różnić przez numer wersji.</span><span class="sxs-lookup"><span data-stu-id="95f50-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="95f50-164">Gdy wersja interfejsu API hello ustawiono tooa parametr lub zmienna IntelliSense w edytorze kodu nie może określić hello poprawny schemat.</span><span class="sxs-lookup"><span data-stu-id="95f50-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="95f50-165">Zamiast tego należy trwale kodować hello wersja interfejsu API w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="95f50-166">Zmienne</span><span class="sxs-lookup"><span data-stu-id="95f50-166">Variables</span></span>
<span data-ttu-id="95f50-167">Witaj następujące informacje mogą być pomocne podczas pracy ze zmiennymi:</span><span class="sxs-lookup"><span data-stu-id="95f50-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="95f50-168">Użyj zmienne dla wartości, należy toouse więcej niż raz w szablonie.</span><span class="sxs-lookup"><span data-stu-id="95f50-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="95f50-169">Jeśli wartość jest używana tylko raz, wartość ustalony sprawia, że Twoje tooread łatwiejsze szablonu.</span><span class="sxs-lookup"><span data-stu-id="95f50-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="95f50-170">Nie można użyć hello [odwołania](resource-group-template-functions-resource.md#reference) funkcji w hello **zmienne** sekcji hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="95f50-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="95f50-171">Witaj **odwołania** funkcja pochodzi wartość stanu środowiska uruchomieniowego hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="95f50-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="95f50-172">Jednak zmienne są rozpoznawane podczas początkowej analizy szablonu hello hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="95f50-173">Tworzenia wartości, które wymagają hello **odwołania** funkcji bezpośrednio w hello **zasobów** lub **generuje** sekcji hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="95f50-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="95f50-174">Obejmują zmienne dla nazw zasobów, które muszą być unikatowe, zgodnie z opisem w [nazw zasobów](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="95f50-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="95f50-175">Zmienne można grupować w obiektów złożonych.</span><span class="sxs-lookup"><span data-stu-id="95f50-175">You can group variables into complex objects.</span></span> <span data-ttu-id="95f50-176">Użyj hello **variable.subentry** format tooreference wartości z obiektu złożonego.</span><span class="sxs-lookup"><span data-stu-id="95f50-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="95f50-177">Grupowania zmiennych może ułatwić śledzenie powiązanych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="95f50-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="95f50-178">Zwiększa czytelność hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="95f50-178">It also improves readability of hello template.</span></span> <span data-ttu-id="95f50-179">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="95f50-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="95f50-180">Obiekt złożony nie może zawierać wyrażenia, który odwołuje się do wartości z obiektu złożonego.</span><span class="sxs-lookup"><span data-stu-id="95f50-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="95f50-181">W tym celu zdefiniowane osobnej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="95f50-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="95f50-182">Przykłady zaawansowanych za pomocą obiektu złożonego jako zmiennych, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="95f50-183">Zasoby</span><span class="sxs-lookup"><span data-stu-id="95f50-183">Resources</span></span>
<span data-ttu-id="95f50-184">Hello następujące informacje mogą być przydatne podczas pracy z zasobami:</span><span class="sxs-lookup"><span data-stu-id="95f50-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="95f50-185">toohelp innych uczestników zrozumienie przeznaczenia hello hello zasobu, należy określić **komentarze** dla każdego zasobu w szablonie hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="95f50-186">Można użyć znaczników tooadd metadanych tooresources.</span><span class="sxs-lookup"><span data-stu-id="95f50-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="95f50-187">Użyj metadanych tooadd informacji o zasobach.</span><span class="sxs-lookup"><span data-stu-id="95f50-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="95f50-188">Na przykład można dodać szczegółów rozliczeń toorecord metadanych dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="95f50-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="95f50-189">Aby uzyskać więcej informacji, zobacz [używanie tagów tooorganize zasobów platformy Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="95f50-190">Jeśli używasz *publiczny punkt końcowy* w szablonie (np. Azure Blob magazynu publiczny punkt końcowy), *czy nie kodowane* hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="95f50-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="95f50-191">Użyj hello **odwołania** toodynamically funkcja pobrać hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="95f50-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="95f50-192">Można użyć tego podejścia toodeploy hello szablonu toodifferent publicznej przestrzeni nazw środowiskach bez ręcznej zmiany punktu końcowego hello w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="95f50-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="95f50-193">Ustaw toohello wersji interfejsu API hello tej samej wersji, używanego dla konta magazynu hello w szablonie:</span><span class="sxs-lookup"><span data-stu-id="95f50-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="95f50-194">Jeśli konto magazynu hello jest wdrażana w hello tego samego szablonu, który tworzysz, nie trzeba przestrzeń nazw dostawcy hello toospecify odwołanie hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="95f50-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="95f50-195">Jest to hello uproszczony składni:</span><span class="sxs-lookup"><span data-stu-id="95f50-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="95f50-196">Jeśli masz inne wartości w szablonie, które są skonfigurowane toouse publicznej przestrzeni nazw, zmień wartości tych tooreflect hello sam **odwołania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="95f50-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="95f50-197">Na przykład można ustawić hello **storageUri** właściwości profilu diagnostyki maszyny wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="95f50-198">Możesz także odwoływać się do istniejącego konta magazynu, który znajduje się w innej grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="95f50-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="95f50-199">Przypisz publicznego maszyny wirtualnej tooa adresy IP tylko wtedy, gdy aplikacja wymaga on.</span><span class="sxs-lookup"><span data-stu-id="95f50-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="95f50-200">tooconnect tooa maszyny wirtualnej (VM) do debugowania lub zarządzania lub celów administracyjnych, użyj reguły NAT ruchu przychodzącego, Brama sieci wirtualnej lub jumpbox.</span><span class="sxs-lookup"><span data-stu-id="95f50-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="95f50-201">Aby uzyskać więcej informacji o podłączaniu toovirtual maszyny zobacz:</span><span class="sxs-lookup"><span data-stu-id="95f50-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="95f50-202">Uruchamianie maszyn wirtualnych dla architektury N-warstwowa na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="95f50-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="95f50-203">Konfigurowanie dostępu do usługi WinRM dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95f50-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="95f50-204">Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="95f50-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="95f50-205">Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="95f50-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="95f50-206">Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej systemu Linux przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95f50-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="95f50-207">Witaj **domainNameLabel** właściwości dla publicznych adresów IP muszą być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="95f50-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="95f50-208">Witaj **domainNameLabel** wartość musi mieć długość od 3 do 63 znaków i reguły hello określonego przez tego wyrażenia regularnego: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="95f50-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="95f50-209">Ponieważ hello **uniqueString** funkcja generuje ciąg, który jest 13 znaków hello **dnsPrefixString** parametr jest ograniczona too50 znaków:</span><span class="sxs-lookup"><span data-stu-id="95f50-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="95f50-210">Po dodaniu hasła tooa niestandardowe rozszerzenie skryptu Użyj hello **commandToExecute** właściwości w hello **protectedSettings** właściwości:</span><span class="sxs-lookup"><span data-stu-id="95f50-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="95f50-211">tooensure, że hasła są szyfrowane, gdy są one przekazywane jako parametry tooVMs i rozszerzenia, użyj hello **protectedSettings** właściwości hello odpowiednich rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="95f50-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="95f50-212">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="95f50-212">Outputs</span></span>
<span data-ttu-id="95f50-213">Jeśli używasz publiczne adresy IP szablonu toocreate obejmują **generuje** sekcja, która zwraca szczegóły hello adresu IP i hello pełną nazwę domeny (FQDN).</span><span class="sxs-lookup"><span data-stu-id="95f50-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="95f50-214">Po wdrożeniu można użyć danych wyjściowych wartości tooeasily pobranie szczegółów dotyczących publicznych adresów IP i nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="95f50-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="95f50-215">Podając odniesienie hello zasobów, użyj wersji hello interfejsu API użytą toocreate go:</span><span class="sxs-lookup"><span data-stu-id="95f50-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="95f50-216">Jednego szablonu, a zagnieżdżone szablony</span><span class="sxs-lookup"><span data-stu-id="95f50-216">Single template vs. nested templates</span></span>
<span data-ttu-id="95f50-217">toodeploy rozwiązania, można użyć jednego szablonu lub szablonu głównego z wielu szablonów zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="95f50-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="95f50-218">Zagnieżdżone szablony są wspólne dla bardziej zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="95f50-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="95f50-219">Przy użyciu zapewnia szablon zagnieżdżony, tekst hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="95f50-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="95f50-220">Można podzielić rozwiązania do elementów docelowych.</span><span class="sxs-lookup"><span data-stu-id="95f50-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="95f50-221">Zagnieżdżone szablony z różnych szablonów głównego można użyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="95f50-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="95f50-222">Jeśli wybierzesz toouse zagnieżdżone szablony hello następujące wytyczne może pomóc normalizacji projektu szablonu.</span><span class="sxs-lookup"><span data-stu-id="95f50-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="95f50-223">Niniejsze wytyczne dotyczą [wzorce projektowania szablonów usługi Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="95f50-224">Zaleca się projekt, który ma hello następujące szablony:</span><span class="sxs-lookup"><span data-stu-id="95f50-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="95f50-225">**Główny szablon** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="95f50-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="95f50-226">Na użytek hello parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="95f50-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="95f50-227">**Udostępnione zasoby szablonu**.</span><span class="sxs-lookup"><span data-stu-id="95f50-227">**Shared resources template**.</span></span> <span data-ttu-id="95f50-228">Użyj toodeploy udostępnionych zasobów korzystających z innych zasobów (na przykład wirtualnych sieci i dostępność zestawy).</span><span class="sxs-lookup"><span data-stu-id="95f50-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="95f50-229">Użyj hello **dependsOn** tooensure wyrażenia, że ten szablon jest wdrażany przed innych szablonów.</span><span class="sxs-lookup"><span data-stu-id="95f50-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="95f50-230">**Opcjonalne zasoby szablonu**.</span><span class="sxs-lookup"><span data-stu-id="95f50-230">**Optional resources template**.</span></span> <span data-ttu-id="95f50-231">Użyj tooconditionally wdrażanie zasobów na podstawie parametru (na przykład jumpbox).</span><span class="sxs-lookup"><span data-stu-id="95f50-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="95f50-232">**Szablon elementu członkowskiego zasobów**.</span><span class="sxs-lookup"><span data-stu-id="95f50-232">**Member resources template**.</span></span> <span data-ttu-id="95f50-233">Każdy typ wystąpienie w warstwie aplikacji ma własny konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="95f50-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="95f50-234">W ramach warstwy można zdefiniować typy innego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="95f50-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="95f50-235">(Na przykład hello pierwsze wystąpienie jest tworzony klaster, i dodatkowe wystąpienia są dodawane toohello istniejącego klastra) Każdy typ wystąpienia ma własny szablon wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="95f50-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="95f50-236">**Skrypty**.</span><span class="sxs-lookup"><span data-stu-id="95f50-236">**Scripts**.</span></span> <span data-ttu-id="95f50-237">Powszechnie wielokrotnego użytku skrypty są stosowane do każdego wystąpienia typu (na przykład, inicjowanie i formatowanie dodatkowe dyski).</span><span class="sxs-lookup"><span data-stu-id="95f50-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="95f50-238">Niestandardowych skryptów utworzonych w celu dostosowania określonych są różne, na podstawie hello wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="95f50-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Szablon zagnieżdżony](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="95f50-240">Aby uzyskać więcej informacji, zobacz [używać szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="95f50-241">Warunkowo link toonested szablonów</span><span class="sxs-lookup"><span data-stu-id="95f50-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="95f50-242">Można użyć parametru tooconditionally łącze toonested szablonów.</span><span class="sxs-lookup"><span data-stu-id="95f50-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="95f50-243">Parametr Hello staje się częścią hello identyfikatora URI dla szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="95f50-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="95f50-244">Format szablonu</span><span class="sxs-lookup"><span data-stu-id="95f50-244">Template format</span></span>
<span data-ttu-id="95f50-245">Toopass dobrym rozwiązaniem jest szablonu przez moduł weryfikacji JSON.</span><span class="sxs-lookup"><span data-stu-id="95f50-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="95f50-246">Moduł weryfikacji ułatwia Usuń nadmiarowe przecinkami, nawiasy i nawiasy, które może spowodować wystąpienie błędu podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="95f50-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="95f50-247">Spróbuj [JSONLint](http://jsonlint.com/) lub pakiet linter dla Ulubione edycji środowiska (Sublime tekstu Visual Studio Code, Atom, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="95f50-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="95f50-248">Istnieje również tooformat dobrze czy kod JSON w celu zwiększenia czytelności.</span><span class="sxs-lookup"><span data-stu-id="95f50-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="95f50-249">Pakiet programu formatującego JSON można użyć dla Edytora lokalnych.</span><span class="sxs-lookup"><span data-stu-id="95f50-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="95f50-250">W programie Visual Studio, tooformat hello dokumentu, naciśnij klawisz **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="95f50-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="95f50-251">W programie Visual Studio Code, naciśnij klawisz **Alt + Shift + F**.</span><span class="sxs-lookup"><span data-stu-id="95f50-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="95f50-252">Edytor lokalnych nie formatuje hello dokumentu, można użyć [online program formatujący](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="95f50-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95f50-253">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95f50-253">Next steps</span></span>
* <span data-ttu-id="95f50-254">Aby uzyskać wskazówki dotyczące projektowania rozwiązania dla maszyn wirtualnych, zobacz [Uruchom Maszynę wirtualną systemu Windows na platformie Azure](../guidance/guidance-compute-single-vm.md) i [Uruchom Maszynę wirtualną systemu Linux na platformie Azure](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="95f50-255">Aby uzyskać instrukcje na temat konfigurowania konta magazynu, zobacz [Lista kontrolna wydajności i skalowalności magazynu Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="95f50-256">toolearn dotyczące wykorzystania tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise: ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="95f50-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

