---
title: "Ustawić kolejność wdrażania zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu ustawiania jeden zasób zależny od innego zasobu podczas wdrażania, aby upewnić się, że zasoby są wdrażane w odpowiedniej kolejności."
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
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="b14fc-103">Zdefiniuj kolejność wdrażania zasobów w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b14fc-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="b14fc-104">Dla danego zasobu może być inne zasoby, które muszą istnieć przed wdrożeniem zasobu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="b14fc-105">Na przykład serwer SQL musi istnieć przed podjęciem próby wdrożenia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b14fc-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="b14fc-106">Ta relacja należy zdefiniować oznaczając jednego zasobu jako zależny od innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="b14fc-107">Definiowanie zależności z **dependsOn** elementu, lub za pomocą **odwołania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="b14fc-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="b14fc-108">Menedżer zasobów ocenia zależności między zasobami i wdraża je w porządku zależnych.</span><span class="sxs-lookup"><span data-stu-id="b14fc-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="b14fc-109">Jeśli zasoby nie są zależne od siebie, Menedżer zasobów wdraża je równolegle.</span><span class="sxs-lookup"><span data-stu-id="b14fc-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="b14fc-110">Wystarczy Definiowanie zależności dla zasobów, które zostały wdrożone w tym samym szablonie.</span><span class="sxs-lookup"><span data-stu-id="b14fc-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="b14fc-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="b14fc-111">dependsOn</span></span>
<span data-ttu-id="b14fc-112">W szablonie dependsOn element umożliwia zdefiniowanie jednego zasobu jako zależną na jeden lub więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="b14fc-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="b14fc-113">Wartość może być rozdzielana przecinkami lista nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="b14fc-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="b14fc-114">W poniższym przykładzie przedstawiono zestaw skali maszyny wirtualnej, która zależy od usługi równoważenia obciążenia, sieć wirtualną i pętli, które tworzy wiele kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="b14fc-115">Te inne zasoby nie są wyświetlane w poniższym przykładzie, ale musi istnieć w innym miejscu w szablonie.</span><span class="sxs-lookup"><span data-stu-id="b14fc-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

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

<span data-ttu-id="b14fc-116">W powyższym przykładzie zależności znajduje się na zasoby, które są tworzone przez pętlę kopiowania o nazwie **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="b14fc-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="b14fc-117">Na przykład zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b14fc-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="b14fc-118">Podczas definiowania zależności, mogą obejmować przestrzeń nazw dostawcy zasobów i typu zasobu, aby uniknąć niejednoznaczności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="b14fc-119">Na przykład aby wyjaśnić, usługi równoważenia obciążenia i sieci wirtualnej, która może mieć tej samej nazwy jak inne zasoby, użyj następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="b14fc-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="b14fc-120">Gdy może żądać na potrzeby mapowania relacje między zasobami dependsOn, ważne jest zrozumienie, dlaczego podczas jej wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b14fc-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="b14fc-121">Na przykład do dokumentów, jak zasoby są połączone ze sobą, dependsOn nie jest to prawy rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="b14fc-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="b14fc-122">Nie można wykonać zapytania, które zasoby zostały zdefiniowane w elemencie dependsOn po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="b14fc-123">Za pomocą dependsOn, możesz potencjalnie wpływ czas wdrażania, ponieważ Menedżer zasobów nie wdraża równoległych dwa zasoby, które mają zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="b14fc-124">Relacje między zasobami dokumentu, zamiast tego użyć [łączenia zasobów](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="b14fc-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="b14fc-125">Zasoby podrzędne</span><span class="sxs-lookup"><span data-stu-id="b14fc-125">Child resources</span></span>
<span data-ttu-id="b14fc-126">Właściwość zasobów pozwala określ zasoby podrzędne, które odnoszą się do zasobu został określony.</span><span class="sxs-lookup"><span data-stu-id="b14fc-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="b14fc-127">Zasoby podrzędne może być tylko zdefiniowanych głębokości pięciu poziomów.</span><span class="sxs-lookup"><span data-stu-id="b14fc-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="b14fc-128">Należy pamiętać nie utworzono niejawne zależności między zasobu podrzędnego i zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="b14fc-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="b14fc-129">Jeśli potrzebujesz zasobu podrzędnego do wdrożenia po zasobu nadrzędnego musi jawnie określać tej zależności z właściwością dependsOn.</span><span class="sxs-lookup"><span data-stu-id="b14fc-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="b14fc-130">Każdy zasób nadrzędnego akceptuje tylko niektóre typy zasobów jako zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="b14fc-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="b14fc-131">Typy zasobów akceptowane są określone w [schematu szablonu](https://github.com/Azure/azure-resource-manager-schemas) zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="b14fc-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="b14fc-132">Nazwa typu zasobu podrzędnego zawiera nazwę typu zasobu nadrzędnego, takich jak **Microsoft.Web/sites/config** i **Microsoft.Web/sites/extensions** są oba zasoby podrzędne o **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="b14fc-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="b14fc-133">W poniższym przykładzie pokazano, SQL server i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b14fc-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="b14fc-134">Zwróć uwagę zdefiniowania jawne zależności między bazy danych SQL i programu SQL server, nawet, jeśli baza danych jest elementem podrzędnym serwera.</span><span class="sxs-lookup"><span data-stu-id="b14fc-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="b14fc-135">Odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="b14fc-135">reference function</span></span>
<span data-ttu-id="b14fc-136">[Odwołania funkcja](resource-group-template-functions-resource.md#reference) umożliwia wyrażenie ma być wartość z innych pary nazw i wartości JSON lub zasobów środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="b14fc-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="b14fc-137">Wyrażenia odwołania niejawnie deklaruje, że jeden zasób jest zależny od innego.</span><span class="sxs-lookup"><span data-stu-id="b14fc-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="b14fc-138">Ogólny format to:</span><span class="sxs-lookup"><span data-stu-id="b14fc-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="b14fc-139">W poniższym przykładzie punktu końcowego usługi CDN jawnie zależy od profilu CDN i niejawnie zależy od aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b14fc-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="b14fc-140">Aby określić zależności można użyć tego elementu lub dependsOn element, ale nie trzeba używać obu zasobów zależnych.</span><span class="sxs-lookup"><span data-stu-id="b14fc-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="b14fc-141">Jeśli to możliwe, użyj niejawne odwołanie, aby uniknąć, dodawanie niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="b14fc-142">Aby dowiedzieć się więcej, zobacz [odwołania funkcja](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="b14fc-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="b14fc-143">Zalecenia dotyczące ustawiania zależności</span><span class="sxs-lookup"><span data-stu-id="b14fc-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="b14fc-144">Podczas podejmowania decyzji o zależności, które można ustawić, skorzystaj z poniższych wskazówek:</span><span class="sxs-lookup"><span data-stu-id="b14fc-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="b14fc-145">Jak to możliwe, należy ustawić jako kilka zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="b14fc-146">Ustaw zasobu podrzędnego jako zależy od jego zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="b14fc-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="b14fc-147">Użyj **odwołania** funkcji, aby ustawić niejawne zależności między zasobami, które należy udostępnić właściwości.</span><span class="sxs-lookup"><span data-stu-id="b14fc-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="b14fc-148">Nie dodawaj jawne zależności (**dependsOn**) podczas niejawnego zależności został już zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="b14fc-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="b14fc-149">Takie podejście zmniejsza ryzyko niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="b14fc-150">Ustaw zależność zasobu nie może być **utworzony** bez funkcji z innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="b14fc-151">Nie należy ustawiać zależność, jeśli zasoby komunikować się tylko po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="b14fc-152">Let zależności cascade bez jawnie ich ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b14fc-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="b14fc-153">Na przykład na komputerze wirtualnym zależy od interfejsu sieci wirtualnej, a interfejs sieci wirtualnej jest zależny od sieci wirtualnej i publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="b14fc-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="b14fc-154">W związku z tym maszyny wirtualnej jest wdrożone po wszystkich trzech zasoby, ale nie ustawiaj jawnie maszynę wirtualną jako zależne od wszystkich trzech zasobów.</span><span class="sxs-lookup"><span data-stu-id="b14fc-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="b14fc-155">Takie podejście wyjaśnia, kolejność zależności i ułatwia później zmienić szablonu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="b14fc-156">Jeśli wartość można określić przed wdrożeniem, spróbuj wdrażanie zasobu bez zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="b14fc-157">Na przykład jeśli wartość konfiguracji wymaga innego zasobu, może być konieczne nie zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="b14fc-158">W tych wskazówkach nie zawsze działa, ponieważ niektóre zasoby sprawdzenia istnienia innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="b14fc-159">Jeśli wystąpi błąd, należy dodać zależności.</span><span class="sxs-lookup"><span data-stu-id="b14fc-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="b14fc-160">Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu.</span><span class="sxs-lookup"><span data-stu-id="b14fc-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="b14fc-161">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że istnieje zależność cykliczną, ocenić szablonu czy wszelkie zależności nie są wymagane i mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="b14fc-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="b14fc-162">Jeśli usuwanie zależności nie działa, można uniknąć zależności cykliczne przez przeniesienie niektórych operacji rozmieszczania w zasoby podrzędne, które są wdrażane po zasoby, które mają zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="b14fc-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="b14fc-163">Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się do innych właściwości.</span><span class="sxs-lookup"><span data-stu-id="b14fc-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="b14fc-164">Można je wdrożyć w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="b14fc-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="b14fc-165">vm1</span><span class="sxs-lookup"><span data-stu-id="b14fc-165">vm1</span></span>
2. <span data-ttu-id="b14fc-166">maszyny vm2</span><span class="sxs-lookup"><span data-stu-id="b14fc-166">vm2</span></span>
3. <span data-ttu-id="b14fc-167">Rozszerzenie na vm1 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="b14fc-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="b14fc-168">Rozszerzenie ustawia wartości vm1, który otrzymuje od maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="b14fc-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="b14fc-169">Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="b14fc-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="b14fc-170">Rozszerzenie ustawia wartości maszyny vm2, który otrzymuje od vm1.</span><span class="sxs-lookup"><span data-stu-id="b14fc-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="b14fc-171">Informacje o ocenie kolejność wdrażania i rozwiązywaniu problemów z błędami zależności, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b14fc-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14fc-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b14fc-172">Next steps</span></span>
* <span data-ttu-id="b14fc-173">Aby uzyskać informacje dotyczące rozwiązywania problemów zależności podczas wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b14fc-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b14fc-174">Aby dowiedzieć się więcej na temat tworzenia szablonów usługi Azure Resource Manager, zobacz [tworzenia szablonów](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b14fc-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="b14fc-175">Aby uzyskać listę dostępnych funkcji w szablonie, zobacz [szablonu funkcji](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b14fc-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

