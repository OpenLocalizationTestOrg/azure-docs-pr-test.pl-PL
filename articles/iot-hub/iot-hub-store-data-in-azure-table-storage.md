---
title: "Zapisywania wiadomości Centrum IoT do magazynu danych Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu aplikacji Azure funkcji zapisywania wiadomości Centrum IoT z magazynu tabel Azure. Komunikaty Centrum IoT zawierają informacje, takie jak dane czujników, które są wysyłane z urządzenia IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Magazyn danych iot, przechowywania danych czujników iot"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="c31e0-105">Zapisz komunikaty Centrum IoT, które zawierają dane czujników w celu Twojego magazynu tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c31e0-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="c31e0-107">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="c31e0-107">What you learn</span></span>

<span data-ttu-id="c31e0-108">Jak utworzyć konto magazynu platformy Azure i aplikacji funkcji platformy Azure do przechowywania komunikatów Centrum IoT w Twoim magazynie w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c31e0-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c31e0-109">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="c31e0-109">What you do</span></span>

- <span data-ttu-id="c31e0-110">Utworzenie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c31e0-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="c31e0-111">Przygotuj połączenie Centrum IoT odczytywać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="c31e0-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="c31e0-112">Tworzenie i wdrażanie aplikacji funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c31e0-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c31e0-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="c31e0-113">What you need</span></span>

- <span data-ttu-id="c31e0-114">[Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md) , aby pokrywał się następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="c31e0-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="c31e0-115">Aktywną subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c31e0-115">An active Azure subscription</span></span>
  - <span data-ttu-id="c31e0-116">Centrum IoT w ramach Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c31e0-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="c31e0-117">Działającej aplikacji, która wysyła komunikaty do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c31e0-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="c31e0-118">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c31e0-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="c31e0-119">W [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **magazynu** > **konta magazynu**  >   **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="c31e0-120">Wprowadź informacje niezbędne do konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="c31e0-120">Enter the necessary information for the storage account:</span></span>

   ![Utwórz konto magazynu w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="c31e0-122">**Nazwa**: Nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c31e0-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="c31e0-123">Nazwa musi być unikatowa w skali globalnej.</span><span class="sxs-lookup"><span data-stu-id="c31e0-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="c31e0-124">**Grupa zasobów**: Użyj tej samej grupie zasobów, która używa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="c31e0-125">**Przypnij do pulpitu nawigacyjnego**: wybierz tę opcję, aby mieć łatwy dostęp do centrum IoT Hub z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31e0-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="c31e0-126">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="c31e0-127">Przygotowanie połączenia Centrum IoT odczytywać wiadomości</span><span class="sxs-lookup"><span data-stu-id="c31e0-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="c31e0-128">Centrum IoT przedstawia punktu końcowego zgodnych z Centrum zdarzeń wbudowanych umożliwia aplikacjom odczytywanie wiadomości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="c31e0-129">W tym samym czasie aplikacji umożliwia odczytywanie danych z Centrum IoT grup odbiorców.</span><span class="sxs-lookup"><span data-stu-id="c31e0-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="c31e0-130">Przed utworzeniem aplikacji funkcji platformy Azure można odczytać danych z Centrum IoT, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c31e0-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="c31e0-131">Pobierz ciąg połączenia punktu końcowego Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="c31e0-132">Utwórz grupy odbiorców Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="c31e0-133">Pobierz ciąg połączenia punktu końcowego Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c31e0-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="c31e0-134">Otwórz Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="c31e0-135">Na **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="c31e0-136">W prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="c31e0-137">W **właściwości** okienka, należy zwrócić uwagę na następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c31e0-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="c31e0-138">Punkt końcowy zgodnych z Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c31e0-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="c31e0-139">Nazwa zgodnych z Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c31e0-139">Event hub-compatible name</span></span>

   ![Pobierz ciąg połączenia punktu końcowego Centrum IoT w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="c31e0-141">W **Centrum IoT** okienku w obszarze **ustawienia**, kliknij przycisk **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="c31e0-142">Kliknij przycisk **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="c31e0-143">Uwaga **klucz podstawowy** wartość.</span><span class="sxs-lookup"><span data-stu-id="c31e0-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="c31e0-144">Utworzenie punktu końcowego Centrum IoT parametry połączenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c31e0-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="c31e0-145">Zastąp `<Event Hub-compatible endpoint>` i `<Primary key>` wartościami, których wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="c31e0-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="c31e0-146">Tworzenie grupy odbiorców Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c31e0-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="c31e0-147">Otwórz Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="c31e0-148">W **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="c31e0-149">W prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="c31e0-150">W **właściwości** okienku w obszarze **grupy konsumentów**, wprowadź nazwę, a następnie zanotuj jego.</span><span class="sxs-lookup"><span data-stu-id="c31e0-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="c31e0-151">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="c31e0-152">Tworzenie i wdrażanie aplikacji Azure — funkcja</span><span class="sxs-lookup"><span data-stu-id="c31e0-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="c31e0-153">W [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **obliczeniowe** > **aplikacji funkcji**  >   **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="c31e0-154">Wprowadź informacje niezbędne do funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c31e0-154">Enter the necessary information for the function app.</span></span>

   ![Tworzenie aplikacji funkcji w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="c31e0-156">**Nazwa aplikacji**: Nazwa aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="c31e0-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="c31e0-157">Nazwa musi być unikatowa w skali globalnej.</span><span class="sxs-lookup"><span data-stu-id="c31e0-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="c31e0-158">**Grupa zasobów**: Użyj tej samej grupie zasobów, która używa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="c31e0-159">**Konto magazynu**: utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c31e0-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="c31e0-160">**Przypnij do pulpitu nawigacyjnego**: Zaznacz tę opcję, by mieć łatwy dostęp do aplikacji funkcji z poziomu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31e0-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="c31e0-161">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-161">Click **Create**.</span></span>

4. <span data-ttu-id="c31e0-162">Po utworzeniu aplikacji funkcji, można go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="c31e0-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="c31e0-163">W funkcji aplikacji Utwórz nową funkcję, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c31e0-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="c31e0-164">a.</span><span class="sxs-lookup"><span data-stu-id="c31e0-164">a.</span></span> <span data-ttu-id="c31e0-165">Kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-165">Click **New Function**.</span></span>

   <span data-ttu-id="c31e0-166">b.</span><span class="sxs-lookup"><span data-stu-id="c31e0-166">b.</span></span> <span data-ttu-id="c31e0-167">Wybierz **JavaScript** dla **języka**, i **przetwarzania danych** dla **scenariusza**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="c31e0-168">c.</span><span class="sxs-lookup"><span data-stu-id="c31e0-168">c.</span></span> <span data-ttu-id="c31e0-169">Kliknij przycisk **tworzenia tej funkcji**, a następnie kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="c31e0-170">d.</span><span class="sxs-lookup"><span data-stu-id="c31e0-170">d.</span></span> <span data-ttu-id="c31e0-171">Wybierz **JavaScript** dla języka, i **przetwarzania danych** dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c31e0-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="c31e0-172">e.</span><span class="sxs-lookup"><span data-stu-id="c31e0-172">e.</span></span> <span data-ttu-id="c31e0-173">Kliknij przycisk **EventHubTrigger JavaScript** szablonu.</span><span class="sxs-lookup"><span data-stu-id="c31e0-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="c31e0-174">f.</span><span class="sxs-lookup"><span data-stu-id="c31e0-174">f.</span></span> <span data-ttu-id="c31e0-175">Wprowadź informacje niezbędne do szablonu.</span><span class="sxs-lookup"><span data-stu-id="c31e0-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="c31e0-176">**Nazwa funkcji**: Nazwa funkcji.</span><span class="sxs-lookup"><span data-stu-id="c31e0-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="c31e0-177">**Nazwa Centrum zdarzeń**: Nazwa zgodnych z Centrum zdarzeń zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c31e0-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="c31e0-178">**Połączenia Centrum zdarzeń**: Aby dodać parametry połączenia utworzonego punktu końcowego Centrum IoT kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="c31e0-179">g.</span><span class="sxs-lookup"><span data-stu-id="c31e0-179">g.</span></span> <span data-ttu-id="c31e0-180">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-180">Click **Create**.</span></span>

6. <span data-ttu-id="c31e0-181">Dane wyjściowe funkcji należy skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c31e0-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="c31e0-182">a.</span><span class="sxs-lookup"><span data-stu-id="c31e0-182">a.</span></span> <span data-ttu-id="c31e0-183">Kliknij przycisk **integracji** > **nowych danych wyjściowych** > **magazynu tabel Azure** > **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Dodawanie magazynu tabel do funkcji aplikacji w portalu Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="c31e0-185">b.</span><span class="sxs-lookup"><span data-stu-id="c31e0-185">b.</span></span> <span data-ttu-id="c31e0-186">Wprowadź niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="c31e0-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="c31e0-187">**Nazwa parametru tabeli**: Użyj `outputTable`, który będzie używany w funkcji platformy Azure kod.</span><span class="sxs-lookup"><span data-stu-id="c31e0-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="c31e0-188">**Nazwa tabeli**: Użyj `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="c31e0-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="c31e0-189">**Konta połączenia z magazynem**: kliknij **nowy**, a następnie wybierz lub wprowadź konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c31e0-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="c31e0-190">Jeśli konto magazynu nie jest wyświetlany, zobacz [wymagania dotyczące konta magazynu](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="c31e0-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="c31e0-191">c.</span><span class="sxs-lookup"><span data-stu-id="c31e0-191">c.</span></span> <span data-ttu-id="c31e0-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-192">Click **Save**.</span></span>

7. <span data-ttu-id="c31e0-193">W obszarze **wyzwalaczy**, kliknij przycisk **Azure Event Hub (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="c31e0-194">W obszarze **grupy odbiorców Centrum zdarzeń**, wprowadź nazwę grupy odbiorców, który zostanie utworzony, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="c31e0-195">Kliknij funkcję utworzony po lewej stronie, a następnie kliknij przycisk **Wyświetl pliki** po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="c31e0-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="c31e0-196">Zastąp kod w `index.js` następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c31e0-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="c31e0-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-197">Click **Save**.</span></span>

<span data-ttu-id="c31e0-198">Utworzona aplikacja funkcji.</span><span class="sxs-lookup"><span data-stu-id="c31e0-198">You have now created the function app.</span></span> <span data-ttu-id="c31e0-199">Przechowuje wiadomości, które otrzymuje Centrum IoT w Twoim magazynie w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c31e0-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c31e0-200">Można użyć **Uruchom** przycisk, aby przetestować aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="c31e0-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="c31e0-201">Po kliknięciu **Uruchom**, wiadomości testowej są wysyłane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="c31e0-202">Otrzymanie komunikatu powinno spowodować aplikacji funkcja start, a następnie Zapisz komunikat do magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="c31e0-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="c31e0-203">**Dzienniki** okienko rejestruje szczegółowe informacje o procesie.</span><span class="sxs-lookup"><span data-stu-id="c31e0-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="c31e0-204">Sprawdź wiadomość w Twoim magazynie w tabeli</span><span class="sxs-lookup"><span data-stu-id="c31e0-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="c31e0-205">Uruchom przykładową aplikację na urządzeniu do wysyłania komunikatów do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c31e0-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="c31e0-206">[Pobieranie i instalowanie Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="c31e0-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="c31e0-207">Otwórz Eksploratora usługi Storage, kliknij pozycję **Dodaj konto Azure** > **Zaloguj**, a następnie zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c31e0-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="c31e0-208">Kliknij subskrypcję platformy Azure > **kont magazynu** > Twoje konto magazynu > **tabel** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="c31e0-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="c31e0-209">Powinny pojawić się komunikaty wysyłane z urządzenia do Centrum IoT zalogowany `deviceData` tabeli.</span><span class="sxs-lookup"><span data-stu-id="c31e0-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c31e0-210">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c31e0-210">Next steps</span></span>

<span data-ttu-id="c31e0-211">Pomyślnie utworzono Twoje konto usługi Azure storage i Azure funkcji aplikacji, która przechowuje komunikaty odbieranych przez Centrum IoT w Twoim magazynie w tabeli.</span><span class="sxs-lookup"><span data-stu-id="c31e0-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
