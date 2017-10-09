---
title: "aaaLearn o skali maszyny wirtualnej ustawienie szablonów | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate minimalnej wielkości Ustaw szablon zestawy skalowania maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="d66f9-103">Więcej informacji na temat szablonów zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d66f9-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="d66f9-104">[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) są toodeploy doskonały sposób grup powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d66f9-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="d66f9-105">Ta seria samouczek pokazuje, jak toocreate minimalnej wielkości Ustaw szablon i jak toomodify toosuit ten szablon różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d66f9-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="d66f9-106">Wszystkie przykłady pochodzą od tego [repozytorium GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="d66f9-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="d66f9-107">Ten szablon jest zamierzone toobe proste.</span><span class="sxs-lookup"><span data-stu-id="d66f9-107">This template is intended toobe simple.</span></span> <span data-ttu-id="d66f9-108">Bardziej szczegółowy przykłady skali szablonów, zobacz hello [repozytorium GitHub szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) i Wyszukaj foldery zawierające ciąg hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="d66f9-109">Jeśli znasz już tworzenie szablonów, można pominąć toohello toosee sekcji "Następne kroki" jak toomodify tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="d66f9-110">Szablon hello przeglądu</span><span class="sxs-lookup"><span data-stu-id="d66f9-110">Review hello template</span></span>

<span data-ttu-id="d66f9-111">Użyj GitHub tooreview naszych minimalnej wielkości Ustaw szablon, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d66f9-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="d66f9-112">W tym samouczku omówione różnicowego hello (`git diff master minimum-viable-scale-set`) toocreate hello minimalnej wielkości Ustaw szablon element przez element.</span><span class="sxs-lookup"><span data-stu-id="d66f9-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="d66f9-113">Zdefiniuj $schema i contentVersion</span><span class="sxs-lookup"><span data-stu-id="d66f9-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="d66f9-114">Najpierw należy zdefiniować `$schema` i `contentVersion` hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="d66f9-115">Witaj `$schema` element definiuje hello wersji języka szablonu hello i jest używany dla programu Visual Studio wyróżnianie składni i podobne funkcje sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="d66f9-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="d66f9-116">Witaj `contentVersion` element nie jest używany przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="d66f9-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="d66f9-117">Zamiast tego należy go pomaga śledzić hello wersji szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="d66f9-118">Zdefiniuj parametry</span><span class="sxs-lookup"><span data-stu-id="d66f9-118">Define parameters</span></span>
<span data-ttu-id="d66f9-119">Następnie należy zdefiniować dwa parametry `adminUsername` i `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="d66f9-120">Parametry są podane w czasie hello wdrożenia wartości.</span><span class="sxs-lookup"><span data-stu-id="d66f9-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="d66f9-121">Hello `adminUsername` parametr jest po prostu `string` typu, ale ponieważ `adminPassword` jest klucz tajny, zapewniamy im typu `securestring`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="d66f9-122">Później te parametry są przekazywane do hello skali zestawu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d66f9-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="d66f9-123">Definiowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="d66f9-123">Define variables</span></span>
<span data-ttu-id="d66f9-124">Szablony Menedżera zasobów pozwalają również zdefiniować toobe zmienne używane w dalszej części hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="d66f9-125">Naszym przykładzie nie używa żadnych zmiennych, więc mamy już puste hello obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="d66f9-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="d66f9-126">Definiowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="d66f9-126">Define resources</span></span>
<span data-ttu-id="d66f9-127">Następnie jest sekcja zasobów hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="d66f9-128">W tym miejscu możesz zdefiniować elementy faktycznie toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d66f9-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="d66f9-129">W odróżnieniu od `parameters` i `variables` (które są obiektów JSON), `resources` znajduje się lista JSON obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="d66f9-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="d66f9-130">Wszystkie zasoby wymagają `type`, `name`, `apiVersion`, i `location` właściwości.</span><span class="sxs-lookup"><span data-stu-id="d66f9-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="d66f9-131">W tym przykładzie pierwszy zasób ma typ `Microsft.Network/virtualNetwork`, nazwa `myVnet`i apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="d66f9-132">(toofind hello najnowszą wersją interfejsu API dla typu zasobu, zobacz hello [dokumentacji interfejsu API REST Azure](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="d66f9-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="d66f9-133">Określ lokalizację</span><span class="sxs-lookup"><span data-stu-id="d66f9-133">Specify location</span></span>
<span data-ttu-id="d66f9-134">używamy lokalizacji hello toospecify hello sieci wirtualnej, [funkcji szablonu usługi Resource Manager](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="d66f9-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="d66f9-135">Ta funkcja musi być ujęta w cudzysłowy i nawiasy kwadratowe następująco: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="d66f9-136">W takim przypadku stosujemy hello `resourceGroup` funkcji.</span><span class="sxs-lookup"><span data-stu-id="d66f9-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="d66f9-137">Go przyjmuje żadnych argumentów i zwraca obiekt JSON z metadanymi o hello grupy zasobów, który jest wdrażany tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d66f9-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="d66f9-138">Grupa zasobów Hello jest ustawione przez użytkownika hello w czasie hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d66f9-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="d66f9-139">Firma Microsoft, a następnie indeks do tego obiektu JSON `.location` tooget hello lokalizacji z obiektu JSON hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="d66f9-140">Określ właściwości sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d66f9-140">Specify virtual network properties</span></span>
<span data-ttu-id="d66f9-141">Każdy zasób usługi Resource Manager ma własną `properties` sekcji konfiguracji toohello określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="d66f9-142">W takim przypadku określono tej sieci wirtualnej hello powinny mieć jedną podsieć przy użyciu hello zakresu prywatnych adresów IP `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="d66f9-143">Zestaw skali zawsze znajduje się w obrębie jednej podsieci.</span><span class="sxs-lookup"><span data-stu-id="d66f9-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="d66f9-144">Nie może występować w podsieci.</span><span class="sxs-lookup"><span data-stu-id="d66f9-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="d66f9-145">Dodaj listę dependsOn</span><span class="sxs-lookup"><span data-stu-id="d66f9-145">Add dependsOn list</span></span>
<span data-ttu-id="d66f9-146">Ponadto wymagane toohello `type`, `name`, `apiVersion`, i `location` właściwości, każdy zasób może mieć opcjonalny `dependsOn` lista ciągów.</span><span class="sxs-lookup"><span data-stu-id="d66f9-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="d66f9-147">Określa tej listy, która innych zasobów z tego wdrożenia musi zakończyć się przed wdrożeniem tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="d66f9-148">W takim przypadku istnieje tylko jeden element na liście hello hello sieci wirtualnej z poprzedniego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="d66f9-149">Możemy określić tę zależność, ponieważ hello zestawu skalowania wymaga hello tooexist sieci przed utworzeniem żadnej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d66f9-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="d66f9-150">W ten sposób hello zestaw skali można nadać tych maszyn wirtualnych prywatnych adresów IP z zakresu adresów IP hello wcześniej określona we właściwościach sieci hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="d66f9-151">format Hello każdego ciągu na liście dependsOn hello jest `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="d66f9-152">Użyj hello sam `type` i `name` wcześniej używane w definicji zasobu hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d66f9-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="d66f9-153">Określ właściwości zestawu skali</span><span class="sxs-lookup"><span data-stu-id="d66f9-153">Specify scale set properties</span></span>
<span data-ttu-id="d66f9-154">Zestawy skalowania ma wiele właściwości dostosowywania maszyn wirtualnych hello w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="d66f9-155">Aby uzyskać pełną listę tych właściwości, zobacz hello [dokumentacja interfejsu API REST zestawu skalowania](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="d66f9-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="d66f9-156">W tym samouczku będziemy ustawi tylko kilka właściwości często używane.</span><span class="sxs-lookup"><span data-stu-id="d66f9-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="d66f9-157">Rozmiar maszyny Wirtualnej i pojemności</span><span class="sxs-lookup"><span data-stu-id="d66f9-157">Supply VM size and capacity</span></span>
<span data-ttu-id="d66f9-158">skali Hello Ustaw tooknow potrzeb, jaki rozmiar toocreate maszyny Wirtualnej ("Nazwa jednostki sku") i jak wiele takich maszyn wirtualnych toocreate ("pojemność jednostki sku").</span><span class="sxs-lookup"><span data-stu-id="d66f9-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="d66f9-159">toosee rozmiarów maszyn wirtualnych, które są dostępne, zobacz hello [dokumentacji rozmiarów maszyn wirtualnych](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="d66f9-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="d66f9-160">Wybierz typ aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d66f9-160">Choose type of updates</span></span>
<span data-ttu-id="d66f9-161">zestaw skali Hello musi także tooknow sposób aktualizowania toohandle na powitania zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="d66f9-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="d66f9-162">Obecnie dostępne są dwie opcje `Manual` i `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="d66f9-163">Aby uzyskać więcej informacji na powitania różnice między dwoma hello, zobacz dokumentację hello [tooupgrade skali konfiguracji](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="d66f9-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="d66f9-164">Wybierz system operacyjny maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d66f9-164">Choose VM operating system</span></span>
<span data-ttu-id="d66f9-165">Witaj zestawu skalowania tooknow potrzeb tooput jakiego systemu operacyjnego na maszynach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="d66f9-166">W tym miejscu utworzymy hello maszyn wirtualnych z obrazem 16.04 LTS Ubuntu pełni poprawioną.</span><span class="sxs-lookup"><span data-stu-id="d66f9-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="d66f9-167">Określ element computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="d66f9-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="d66f9-168">zestaw skali Hello wdraża wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d66f9-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="d66f9-169">Zamiast określania nazwy maszyny Wirtualnej, jest określona `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="d66f9-170">Hello zestaw skali dołącza prefiks toohello indeksu dla każdej maszyny Wirtualnej, więc nazw maszyn wirtualnych jest formularz hello `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="d66f9-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="d66f9-171">W następujących fragment hello używamy parametry hello z przed tooset hello administratora użytkownika i hasło dla wszystkich maszyn wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="d66f9-172">Firma Microsoft to zrobić z hello `parameters` funkcji szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="d66f9-173">Ta funkcja przyjmuje ciąg, który określa, które tooand toorefer parametru generuje hello wartości tego parametru.</span><span class="sxs-lookup"><span data-stu-id="d66f9-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="d66f9-174">Określ konfigurację sieci maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d66f9-174">Specify VM network configuration</span></span>
<span data-ttu-id="d66f9-175">Na koniec potrzebujemy konfiguracji sieci hello toospecify dla maszyn wirtualnych hello w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="d66f9-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="d66f9-176">W takim przypadku tylko potrzebujemy toospecify hello identyfikator podsieci hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d66f9-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="d66f9-177">Ta wartość informuje zestawu skali hello tooput hello interfejsów sieciowych w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="d66f9-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="d66f9-178">Możesz uzyskać identyfikator hello hello sieci wirtualnych zawierających hello podsieci przy użyciu hello `resourceId` funkcji szablonu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="d66f9-179">Ta funkcja przyjmuje hello typem i nazwą zasobu i zwraca hello pełny identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="d66f9-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="d66f9-180">Ten identyfikator ma hello formularza:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="d66f9-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="d66f9-181">Jednak hello identyfikator hello sieci wirtualnej nie jest wystarczająco.</span><span class="sxs-lookup"><span data-stu-id="d66f9-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="d66f9-182">Należy określić hello określonej podsieci, która hello zestawu skalowania maszyn wirtualnych powinny być w.</span><span class="sxs-lookup"><span data-stu-id="d66f9-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="d66f9-183">toodo, łączenie `/subnets/mySubnet` toohello identyfikator hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d66f9-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="d66f9-184">wynik Hello jest identyfikator hello w pełni kwalifikowana hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="d66f9-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="d66f9-185">Czy to łączenia z hello `concat` funkcji, która przyjmuje w szeregu ciągi i zwraca ich łączenie.</span><span class="sxs-lookup"><span data-stu-id="d66f9-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="d66f9-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d66f9-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
