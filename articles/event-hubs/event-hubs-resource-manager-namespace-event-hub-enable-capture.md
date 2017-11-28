---
title: "przestrzeń nazw usługi Azure Event Hubs i włączyć funkcję przechwytywania przy użyciu szablonu aaaCreate | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Azure Event Hubs z jednym centrum zdarzeń i włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="bd9bb-103">Tworzenie przestrzeni nazw usługi Event Hubs z centrum zdarzeń i włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd9bb-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="bd9bb-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą centra zdarzeń w przestrzeni nazw z wystąpieniem koncentratora jedno zdarzenie, a także umożliwia hello [funkcja przechwytywania](event-hubs-capture-overview.md) na powitania Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="bd9bb-105">Witaj artykule opisano sposób toodefine zasobów, do których są wdrażane i jak toodefine parametrów, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="bd9bb-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="bd9bb-107">Artykuł przedstawia sposób toospecify przechwytywania zdarzeń w obiektach blob magazynu Azure lub usługi Azure Data Lake Store oparte na powitania docelowym.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="bd9bb-108">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="bd9bb-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="bd9bb-109">Aby uzyskać więcej informacji na temat praktycznych rozwiązań i wzorców dotyczących konwencji nazewnictwa zasobów platformy Azure, zobacz [Azure Resources Naming Conventions (Konwencje nazewnictwa zasobów platformy Azure)][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="bd9bb-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="bd9bb-110">Dla szablonów pełną hello kliknij hello następującego łącza GitHub:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="bd9bb-111">[Centrum i włączyć funkcję przechwytywania tooStorage szablonu zdarzenia][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="bd9bb-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="bd9bb-112">[Centrum i włączyć funkcję przechwytywania tooAzure usługi Data Lake Store szablonu zdarzenia][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="bd9bb-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="bd9bb-113">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="bd9bb-114">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="bd9bb-114">What will you deploy?</span></span>

<span data-ttu-id="bd9bb-115">Ten szablon umożliwia wdrożenie przestrzeni nazw usługi Event Hubs z centrum zdarzeń oraz włączenie [funkcji przechwytywania usługi Event Hubs](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd9bb-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="bd9bb-116">[Centra zdarzeń](event-hubs-what-is-event-hubs.md) jest zdarzeniem przetwarzania używanej tooprovide zdarzenia i dane telemetryczne wejściowych tooAzure w bardzo dużej skali, z małymi opóźnieniami i wysoką niezawodnością.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="bd9bb-117">Zdarzenie koncentratory przechwytywania umożliwia tooautomatically należy dostarczyć hello przesyłanie strumieniowe danych w magazynie obiektów Blob tooAzure centra zdarzeń lub usługi Azure Data Lake Store, w ramach określonego rozmiaru czasowych lub wybrane.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="bd9bb-118">Kliknij powitania po tooenable przycisku przechwytywania centra zdarzeń do usługi Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="bd9bb-119">[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd9bb-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="bd9bb-120">Kliknij powitania po tooenable przycisku przechwytywania centra zdarzeń do usługi Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="bd9bb-121">[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd9bb-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bd9bb-122">Parametry</span><span class="sxs-lookup"><span data-stu-id="bd9bb-122">Parameters</span></span>

<span data-ttu-id="bd9bb-123">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="bd9bb-124">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="bd9bb-125">Należy zdefiniować parametr dla tych wartości, które różnią się na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="bd9bb-126">Definiuje parametry dla wartości, które zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="bd9bb-127">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="bd9bb-128">Szablon Hello definiuje hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="bd9bb-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="bd9bb-129">eventHubNamespaceName</span></span>

<span data-ttu-id="bd9bb-130">Nazwa Hello hello [przestrzeni nazw usługi Event Hubs](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="bd9bb-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="bd9bb-131">eventHubName</span></span>

<span data-ttu-id="bd9bb-132">Nazwa Hello hello Centrum zdarzeń utworzonych w hello [przestrzeni nazw usługi Event Hubs](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="bd9bb-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="bd9bb-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="bd9bb-133">messageRetentionInDays</span></span>

<span data-ttu-id="bd9bb-134">Witaj liczba dni wiadomości powitania tooretain w Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="bd9bb-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="bd9bb-135">partitionCount</span></span>

<span data-ttu-id="bd9bb-136">Liczba Hello toocreate partycji w Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-136">hello number of partitions toocreate in hello event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="bd9bb-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="bd9bb-137">captureEnabled</span></span>

<span data-ttu-id="bd9bb-138">Włącz przechwytywanie na powitania Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-138">Enable Capture on hello event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="bd9bb-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="bd9bb-139">captureEncodingFormat</span></span>

<span data-ttu-id="bd9bb-140">Określ dane zdarzeń hello tooserialize format kodowania Hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-140">hello encoding format you specify tooserialize hello event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="bd9bb-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="bd9bb-141">captureTime</span></span>

<span data-ttu-id="bd9bb-142">Interwał czasu Hello, w którym przechwytywania centra zdarzeń rozpoczyna się przechwytywanie danych hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="bd9bb-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="bd9bb-143">captureSize</span></span>
<span data-ttu-id="bd9bb-144">rozmiar interwału powitania jaką przechwytywania uruchamia przechwytywanie danych hello.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-144">hello size interval at which Capture starts capturing hello data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="bd9bb-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="bd9bb-145">captureNameFormat</span></span>

<span data-ttu-id="bd9bb-146">format nazwy Hello używane przez pliki Avro hello toowrite przechwytywania centrów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="bd9bb-147">Format nazwy funkcji przechwytywania musi zawierać pola `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` i `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="bd9bb-148">Mogą one być uporządkowane w dowolnej kolejności z ogranicznikami lub bez nich.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="bd9bb-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="bd9bb-149">apiVersion</span></span>

<span data-ttu-id="bd9bb-150">Wersja Hello interfejsu API hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="bd9bb-151">Użyj hello następujące parametry, jeżeli wybierz magazyn Azure jako lokalizacja docelowa.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="bd9bb-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="bd9bb-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="bd9bb-153">Przechwytywanie wymaga się, że konto usługi Azure Storage zasobów tooenable identyfikator Przechwytywanie tooyour żądanego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="bd9bb-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="bd9bb-154">blobContainerName</span></span>

<span data-ttu-id="bd9bb-155">Witaj kontenera obiektów blob, w którym toocapture danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="bd9bb-156">Użyj hello następujące parametry, jeżeli wybierzesz Azure Data Lake Store jako lokalizacja docelowa.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="bd9bb-157">Należy ustawić uprawnienia w ścieżce usługi Data Lake Store, w której ma zostać tooCapture hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="bd9bb-158">Zobacz uprawnienia tooset [w tym artykule](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="bd9bb-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="bd9bb-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bd9bb-159">subscriptionId</span></span>

<span data-ttu-id="bd9bb-160">Identyfikator subskrypcji dla przestrzeni nazw usługi Event Hubs hello i usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="bd9bb-161">Oba te zasoby muszą znajdować się pod hello tego samego identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="bd9bb-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="bd9bb-162">dataLakeAccountName</span></span>

<span data-ttu-id="bd9bb-163">nazwę usługi Azure Data Lake Store Hello hello przechwycić zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="bd9bb-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="bd9bb-164">dataLakeFolderPath</span></span>

<span data-ttu-id="bd9bb-165">Ścieżka folderu docelowego Hello hello przechwycić zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="bd9bb-166">Toodeploy zasobów usługi Azure Storage jako miejsce docelowe toocaptured zdarzenia</span><span class="sxs-lookup"><span data-stu-id="bd9bb-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="bd9bb-167">Tworzy nazw typu **EventHubs**, z Centrum zdarzeń jednej, a także umożliwia przechwytywanie tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="bd9bb-168">Toodeploy zasobów dla usługi Azure Data Lake Store jako miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="bd9bb-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="bd9bb-169">Tworzy nazw typu **EventHubs**, z Centrum zdarzeń jednej, a także umożliwia przechwytywanie tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bd9bb-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="bd9bb-170">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="bd9bb-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="bd9bb-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd9bb-171">PowerShell</span></span>

<span data-ttu-id="bd9bb-172">Wdrażanie sieci tooenable szablonu przechwytywania centra zdarzeń w magazynie Azure:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="bd9bb-173">Wdrażanie sieci tooenable szablonu przechwytywania centra zdarzeń do usługi Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="bd9bb-174">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bd9bb-174">Azure CLI</span></span>

<span data-ttu-id="bd9bb-175">Wybieranie usługi Azure Blob Storage jako lokalizacji docelowej:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="bd9bb-176">Wybieranie usługi Azure Data Lake Store jako lokalizacji docelowej:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="bd9bb-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd9bb-177">Next steps</span></span>

<span data-ttu-id="bd9bb-178">Można również skonfigurować przechwytywania centra zdarzeń za pomocą hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd9bb-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bd9bb-179">Aby uzyskać więcej informacji, zobacz [włączyć przechwytywania centra zdarzeń przy użyciu hello portalu Azure](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd9bb-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="bd9bb-180">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="bd9bb-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="bd9bb-181">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bd9bb-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="bd9bb-182">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="bd9bb-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="bd9bb-183">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="bd9bb-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
