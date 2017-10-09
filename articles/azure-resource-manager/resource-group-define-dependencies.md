---
title: "kolejność wdrożenia aaaSet zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wdrożenia tooset jednego zasobu jako zależny od innego zasobu podczas wdrażania tooensure zasobów w odpowiedniej kolejności hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="324a5-103">Zdefiniuj kolejność hello wdrażania zasobów w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="324a5-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="324a5-104">Dla danego zasobu może być inne zasoby, które muszą istnieć przed wdrożeniem hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="324a5-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="324a5-105">Na przykład serwer SQL musi istnieć przed podjęciem próby wykonania toodeploy bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="324a5-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="324a5-106">Należy zdefiniować tę relację oznaczając jednego zasobu jako zależne hello innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="324a5-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="324a5-107">Definiowanie zależności z hello **dependsOn** elementu, lub za pomocą hello **odwołania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="324a5-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="324a5-108">Menedżer zasobów ocenia hello zależności między zasobami i wdraża je w porządku zależnych.</span><span class="sxs-lookup"><span data-stu-id="324a5-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="324a5-109">Jeśli zasoby nie są zależne od siebie, Menedżer zasobów wdraża je równolegle.</span><span class="sxs-lookup"><span data-stu-id="324a5-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="324a5-110">Wystarczy toodefine zależności zasobów, które są wdrażane w hello tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="324a5-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="324a5-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="324a5-111">dependsOn</span></span>
<span data-ttu-id="324a5-112">W szablonie hello dependsOn element umożliwia toodefine jeden zasób, w zależności od jednego lub więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="324a5-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="324a5-113">Wartość może być rozdzielana przecinkami lista nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="324a5-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="324a5-114">Witaj poniższy przykład przedstawia zestaw skali maszyny wirtualnej, która zależy od usługi równoważenia obciążenia, sieć wirtualną i pętli, które tworzy wiele kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="324a5-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="324a5-115">Poniższy przykład hello te inne zasoby nie są wyświetlane, ale powinny tooexist w innym miejscu w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="324a5-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="324a5-116">Zawiera zależność hello poprzedzających przykład, hello zasobów, które są tworzone przez pętlę kopiowania o nazwie **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="324a5-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="324a5-117">Na przykład zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="324a5-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="324a5-118">Podczas definiowania zależności, mogą obejmować hello zasobów dostawcy przestrzeń nazw i zasobów typu tooavoid niejednoznaczności.</span><span class="sxs-lookup"><span data-stu-id="324a5-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="324a5-119">Na przykład tooclarify, które usługa równoważenia obciążenia i sieć wirtualna, która może być hello nazwy takie same jak inne zasoby, hello Użyj następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="324a5-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="324a5-120">Może być odchylona toouse dependsOn toomap relacje między zasobami, jest ważne toounderstand Dlaczego podczas jej wykonywania.</span><span class="sxs-lookup"><span data-stu-id="324a5-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="324a5-121">Na przykład toodocument jak zasoby są połączone ze sobą, dependsOn nie jest hello podejście.</span><span class="sxs-lookup"><span data-stu-id="324a5-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="324a5-122">Nie można wykonać zapytania, które zasoby zostały zdefiniowane w elemencie dependsOn powitania po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="324a5-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="324a5-123">Za pomocą dependsOn, możesz potencjalnie wpływ czas wdrażania, ponieważ Menedżer zasobów nie wdraża równoległych dwa zasoby, które mają zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="324a5-124">Zamiast tego użyj toodocument relacje między zasobami, [łączenia zasobów](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="324a5-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="324a5-125">Zasoby podrzędne</span><span class="sxs-lookup"><span data-stu-id="324a5-125">Child resources</span></span>
<span data-ttu-id="324a5-126">Właściwość zasobów Hello pozwala toospecify podrzędne zasoby, które są powiązane toohello zasobów definiowanego.</span><span class="sxs-lookup"><span data-stu-id="324a5-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="324a5-127">Zasoby podrzędne może być tylko zdefiniowanych głębokości pięciu poziomów.</span><span class="sxs-lookup"><span data-stu-id="324a5-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="324a5-128">Należy utworzyć toonote niejawne zależności nie będący między zasobu podrzędnego i zasobu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="324a5-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="324a5-129">Jeśli konieczne hello wdrożyć po zasobu nadrzędnego hello toobe zasobów podrzędnych, musi jawnie określać tej zależności z hello dependsOn właściwości.</span><span class="sxs-lookup"><span data-stu-id="324a5-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="324a5-130">Każdy zasób nadrzędnego akceptuje tylko niektóre typy zasobów jako zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="324a5-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="324a5-131">zaakceptowane Hello typów zasobów są określone w hello [schematu szablonu](https://github.com/Azure/azure-resource-manager-schemas) hello zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="324a5-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="324a5-132">Witaj Nazwa typu zasobu podrzędnego obejmuje hello Nazwa typu zasobu nadrzędnego hello, takich jak **Microsoft.Web/sites/config** i **Microsoft.Web/sites/extensions** są zasobami podrzędnymi zarówno hello  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="324a5-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="324a5-133">Witaj poniższy przykład przedstawia programu SQL server i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="324a5-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="324a5-134">Zwróć uwagę, zdefiniowania jawne zależności między hello SQL database i programu SQL server, nawet jeśli hello bazy danych jest elementem podrzędnym powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="324a5-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="324a5-135">Odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="324a5-135">reference function</span></span>
<span data-ttu-id="324a5-136">Witaj [odwołania funkcji](resource-group-template-functions-resource.md#reference) umożliwia tooderive wyrażenie jego wartość z innych pary nazw i wartości JSON lub zasobów środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="324a5-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="324a5-137">Wyrażenia odwołania niejawnie deklaruje, że jeden zasób jest zależny od innego.</span><span class="sxs-lookup"><span data-stu-id="324a5-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="324a5-138">format Ogólne Hello jest:</span><span class="sxs-lookup"><span data-stu-id="324a5-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="324a5-139">W hello poniższy przykład punktu końcowego usługi CDN jawnie zależy od hello profilu CDN i niejawnie zależy od aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="324a5-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="324a5-140">Można używać tego elementu albo hello zależności toospecify element dependsOn, ale nie ma potrzeby toouse zarówno dla hello tego samego zasobu zależnego.</span><span class="sxs-lookup"><span data-stu-id="324a5-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="324a5-141">Jeśli to możliwe, należy użyć tooavoid niejawne odwołanie Dodawanie niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="324a5-142">toolearn więcej, zobacz [odwołania funkcja](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="324a5-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="324a5-143">Zalecenia dotyczące ustawiania zależności</span><span class="sxs-lookup"><span data-stu-id="324a5-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="324a5-144">Podczas podejmowania decyzji o jakie tooset zależności, użyj hello następujące wytyczne:</span><span class="sxs-lookup"><span data-stu-id="324a5-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="324a5-145">Jak to możliwe, należy ustawić jako kilka zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="324a5-146">Ustaw zasobu podrzędnego jako zależy od jego zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="324a5-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="324a5-147">Użyj hello **odwołania** funkcji tooset niejawne zależności między zasobami, które wymagają tooshare właściwości.</span><span class="sxs-lookup"><span data-stu-id="324a5-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="324a5-148">Nie dodawaj jawne zależności (**dependsOn**) podczas niejawnego zależności został już zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="324a5-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="324a5-149">Takie podejście zmniejsza ryzyko hello niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="324a5-150">Ustaw zależność zasobu nie może być **utworzony** bez funkcji z innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="324a5-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="324a5-151">Nie należy ustawiać zależność, jeśli zasoby hello komunikować się tylko po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="324a5-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="324a5-152">Let zależności cascade bez jawnie ich ustawienia.</span><span class="sxs-lookup"><span data-stu-id="324a5-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="324a5-153">Na przykład maszyny wirtualnej zależy od interfejsu sieci wirtualnej, a interfejs sieci wirtualnej hello jest zależna od sieci wirtualnej i publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="324a5-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="324a5-154">W związku z tym hello maszyny wirtualnej jest wdrożone po wszystkich trzech zasoby, ale nie ustawiaj jawnie hello maszyny wirtualnej jako zależne od wszystkich trzech zasobów.</span><span class="sxs-lookup"><span data-stu-id="324a5-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="324a5-155">Takie podejście wyjaśnia, kolejność zależności hello i umożliwia łatwiejsze szablonu hello toochange później.</span><span class="sxs-lookup"><span data-stu-id="324a5-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="324a5-156">Jeśli wartość można określić przed wdrożeniem, spróbuj wdrażanie zasobów hello bez zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="324a5-157">Na przykład jeśli wartość konfiguracji musi hello nazwę innego zasobu, może być konieczne nie zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="324a5-158">W tych wskazówkach nie zawsze działa, ponieważ niektóre zasoby Sprawdź istnienie hello hello innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="324a5-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="324a5-159">Jeśli wystąpi błąd, należy dodać zależności.</span><span class="sxs-lookup"><span data-stu-id="324a5-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="324a5-160">Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu.</span><span class="sxs-lookup"><span data-stu-id="324a5-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="324a5-161">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że istnieje zależność cykliczną, ocenić toosee Twojego szablonu, czy wszystkie zależności nie są wymagane i może zostać usunięta.</span><span class="sxs-lookup"><span data-stu-id="324a5-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="324a5-162">Jeśli usuwanie zależności nie działa, można uniknąć zależności cykliczne przez przeniesienie niektórych operacji wdrażania do zasobów podrzędne, które są wdrażane po hello zasoby, które mają hello zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="324a5-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="324a5-163">Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się toohello innych właściwości.</span><span class="sxs-lookup"><span data-stu-id="324a5-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="324a5-164">Można je wdrożyć w hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="324a5-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="324a5-165">vm1</span><span class="sxs-lookup"><span data-stu-id="324a5-165">vm1</span></span>
2. <span data-ttu-id="324a5-166">maszyny vm2</span><span class="sxs-lookup"><span data-stu-id="324a5-166">vm2</span></span>
3. <span data-ttu-id="324a5-167">Rozszerzenie na vm1 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="324a5-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="324a5-168">rozszerzenie Hello ustawia wartości vm1, który otrzymuje od maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="324a5-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="324a5-169">Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="324a5-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="324a5-170">rozszerzenie Hello ustawia wartości maszyny vm2, który otrzymuje od vm1.</span><span class="sxs-lookup"><span data-stu-id="324a5-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="324a5-171">Uzyskać informacje o ocenie hello kolejność wdrażania i rozwiązywaniu problemów z błędami zależności, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="324a5-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="324a5-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="324a5-172">Next steps</span></span>
* <span data-ttu-id="324a5-173">toolearn dotyczące rozwiązywania problemów z zależności podczas wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="324a5-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="324a5-174">toolearn o tworzeniu szablonów usługi Azure Resource Manager, zobacz [tworzenia szablonów](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="324a5-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="324a5-175">Aby uzyskać listę dostępnych funkcji hello w szablonie, zobacz [szablonu funkcji](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="324a5-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

