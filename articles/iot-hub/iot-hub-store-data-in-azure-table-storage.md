---
title: "aaaSave Centrum IoT wiadomości magazynu danych tooAzure | Dokumentacja firmy Microsoft"
description: "Użyj toosave aplikacji Azure — funkcja Twoje tooyour wiadomości Centrum IoT magazynu tabel platformy Azure. wiadomości powitania od centrum IoT zawierają informacje, takie jak dane czujników, które są wysyłane z urządzenia IoT."
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
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="4acdb-105">Zapisz komunikaty Centrum IoT, które zawierają magazynu tabel Azure tooyour danych czujnika</span><span class="sxs-lookup"><span data-stu-id="4acdb-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="4acdb-107">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="4acdb-107">What you learn</span></span>

<span data-ttu-id="4acdb-108">Dowiedz się, jak komunikaty Centrum IoT toostore aplikacji w Twoim magazynie w tabeli funkcji toocreate konta magazynu platformy Azure i platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4acdb-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="4acdb-109">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="4acdb-109">What you do</span></span>

- <span data-ttu-id="4acdb-110">Utworzenie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4acdb-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="4acdb-111">Przygotuj Centrum IoT połączenia tooread wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4acdb-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="4acdb-112">Tworzenie i wdrażanie aplikacji funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4acdb-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4acdb-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="4acdb-113">What you need</span></span>

- <span data-ttu-id="4acdb-114">[Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="4acdb-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="4acdb-115">Aktywną subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4acdb-115">An active Azure subscription</span></span>
  - <span data-ttu-id="4acdb-116">Centrum IoT w ramach Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4acdb-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="4acdb-117">Uruchomionych aplikacji, która wysyła Centrum IoT tooyour wiadomości</span><span class="sxs-lookup"><span data-stu-id="4acdb-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="4acdb-118">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4acdb-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="4acdb-119">W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **magazynu** > **konta magazynu**  >   **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="4acdb-120">Wprowadź niezbędne informacje powitania dla konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="4acdb-120">Enter hello necessary information for hello storage account:</span></span>

   ![Utwórz konto magazynu w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="4acdb-122">**Nazwa**: Nazwa hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="4acdb-123">Nazwa Hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="4acdb-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="4acdb-124">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="4acdb-125">**Numer PIN toodashboard**: Wybierz tę opcję, Centrum IoT tooyour łatwy dostęp z hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4acdb-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="4acdb-126">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="4acdb-127">Przygotowanie Centrum IoT komunikaty tooread połączenia.</span><span class="sxs-lookup"><span data-stu-id="4acdb-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="4acdb-128">Centrum IoT udostępnia wbudowane punktu końcowego Centrum zgodnego tooenable aplikacji tooread IoT Centrum komunikaty o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="4acdb-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="4acdb-129">W tym samym czasie aplikacje używają danych tooread grupy konsumentów z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="4acdb-130">Przed utworzeniem tooread dane aplikacji Azure funkcji z Centrum IoT hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4acdb-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="4acdb-131">Pobierz ciąg połączenia hello punktu końcowego Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="4acdb-132">Utwórz grupy odbiorców Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="4acdb-133">Pobierz ciąg połączenia hello punktu końcowego Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="4acdb-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="4acdb-134">Otwórz Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="4acdb-135">Na powitania **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="4acdb-136">W hello prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="4acdb-137">W hello **właściwości** okienka, hello Uwaga następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="4acdb-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="4acdb-138">Punkt końcowy zgodnych z Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4acdb-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="4acdb-139">Nazwa zgodnych z Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4acdb-139">Event hub-compatible name</span></span>

   ![Pobierz ciąg połączenia hello punktu końcowego Centrum IoT w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="4acdb-141">W hello **Centrum IoT** okienku w obszarze **ustawienia**, kliknij przycisk **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="4acdb-142">Kliknij przycisk **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="4acdb-143">Uwaga hello **klucz podstawowy** wartość.</span><span class="sxs-lookup"><span data-stu-id="4acdb-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="4acdb-144">Utwórz hello parametry połączenia punktu końcowego Centrum IoT w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4acdb-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="4acdb-145">Zastąp `<Event Hub-compatible endpoint>` i `<Primary key>` wartościami hello zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4acdb-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="4acdb-146">Tworzenie grupy odbiorców Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="4acdb-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="4acdb-147">Otwórz Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="4acdb-148">W hello **Centrum IoT** okienku w obszarze **wiadomości**, kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="4acdb-149">W hello prawym okienku w obszarze **wbudowane punkty końcowe**, kliknij przycisk **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="4acdb-150">W hello **właściwości** okienku w obszarze **grupy konsumentów**, wprowadź nazwę, a następnie zanotuj jego.</span><span class="sxs-lookup"><span data-stu-id="4acdb-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="4acdb-151">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="4acdb-152">Tworzenie i wdrażanie aplikacji Azure — funkcja</span><span class="sxs-lookup"><span data-stu-id="4acdb-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="4acdb-153">W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **obliczeniowe** > **aplikacji funkcji**  >   **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="4acdb-154">Wprowadź niezbędne informacje hello hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-154">Enter hello necessary information for hello function app.</span></span>

   ![Tworzenie aplikacji funkcji w hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="4acdb-156">**Nazwa aplikacji**: Nazwa hello hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="4acdb-157">Nazwa Hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="4acdb-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="4acdb-158">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4acdb-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="4acdb-159">**Konto magazynu**: hello utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="4acdb-160">**Numer PIN toodashboard**: Zaznacz tę opcję dla aplikacji funkcja toohello łatwy dostęp z poziomu pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="4acdb-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="4acdb-161">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-161">Click **Create**.</span></span>

4. <span data-ttu-id="4acdb-162">Po utworzeniu hello funkcji aplikacji, można go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="4acdb-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="4acdb-163">W aplikacji funkcji hello Utwórz nową funkcję, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4acdb-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="4acdb-164">a.</span><span class="sxs-lookup"><span data-stu-id="4acdb-164">a.</span></span> <span data-ttu-id="4acdb-165">Kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-165">Click **New Function**.</span></span>

   <span data-ttu-id="4acdb-166">b.</span><span class="sxs-lookup"><span data-stu-id="4acdb-166">b.</span></span> <span data-ttu-id="4acdb-167">Wybierz **JavaScript** dla **języka**, i **przetwarzania danych** dla **scenariusza**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="4acdb-168">c.</span><span class="sxs-lookup"><span data-stu-id="4acdb-168">c.</span></span> <span data-ttu-id="4acdb-169">Kliknij przycisk **tworzenia tej funkcji**, a następnie kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="4acdb-170">d.</span><span class="sxs-lookup"><span data-stu-id="4acdb-170">d.</span></span> <span data-ttu-id="4acdb-171">Wybierz **JavaScript** dla języka hello i **przetwarzania danych** hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="4acdb-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="4acdb-172">e.</span><span class="sxs-lookup"><span data-stu-id="4acdb-172">e.</span></span> <span data-ttu-id="4acdb-173">Kliknij przycisk hello **EventHubTrigger JavaScript** szablonu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="4acdb-174">f.</span><span class="sxs-lookup"><span data-stu-id="4acdb-174">f.</span></span> <span data-ttu-id="4acdb-175">Wprowadź niezbędne informacje hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="4acdb-176">**Nazwa funkcji**: Nazwa hello hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="4acdb-177">**Nazwa Centrum zdarzeń**: Nazwa zgodnych z Centrum zdarzeń hello zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4acdb-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="4acdb-178">**Połączenia Centrum zdarzeń**: parametry połączenia hello tooadd hello punktu końcowego Centrum IoT utworzony, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="4acdb-179">g.</span><span class="sxs-lookup"><span data-stu-id="4acdb-179">g.</span></span> <span data-ttu-id="4acdb-180">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-180">Click **Create**.</span></span>

6. <span data-ttu-id="4acdb-181">Skonfiguruj wyjścia funkcji hello, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4acdb-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="4acdb-182">a.</span><span class="sxs-lookup"><span data-stu-id="4acdb-182">a.</span></span> <span data-ttu-id="4acdb-183">Kliknij przycisk **integracji** > **nowych danych wyjściowych** > **magazynu tabel Azure** > **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Dodatek tabeli magazynu tooyour funkcji aplikacji hello portalu Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="4acdb-185">b.</span><span class="sxs-lookup"><span data-stu-id="4acdb-185">b.</span></span> <span data-ttu-id="4acdb-186">Wprowadź niezbędne informacje hello.</span><span class="sxs-lookup"><span data-stu-id="4acdb-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="4acdb-187">**Nazwa parametru tabeli**: Użyj `outputTable`, który będzie używany w hello Azure kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="4acdb-188">**Nazwa tabeli**: Użyj `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="4acdb-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="4acdb-189">**Konta połączenia z magazynem**: kliknij **nowy**, a następnie wybierz lub wprowadź konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="4acdb-190">Jeśli konto magazynu hello nie jest wyświetlany, zobacz [wymagania dotyczące konta magazynu](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="4acdb-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="4acdb-191">c.</span><span class="sxs-lookup"><span data-stu-id="4acdb-191">c.</span></span> <span data-ttu-id="4acdb-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-192">Click **Save**.</span></span>

7. <span data-ttu-id="4acdb-193">W obszarze **wyzwalaczy**, kliknij przycisk **Azure Event Hub (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="4acdb-194">W obszarze **grupy odbiorców Centrum zdarzeń**, wprowadź nazwę grupy odbiorców hello utworzone, a następnie kliknij przycisk hello **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="4acdb-195">Kliknij przycisk Funkcja powitania po utworzeniu na powitania po lewej, a następnie kliknij przycisk **Wyświetl pliki** na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="4acdb-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="4acdb-196">Zastąp kod hello w `index.js` hello następujący:</span><span class="sxs-lookup"><span data-stu-id="4acdb-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="4acdb-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-197">Click **Save**.</span></span>

<span data-ttu-id="4acdb-198">Utworzona hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-198">You have now created hello function app.</span></span> <span data-ttu-id="4acdb-199">Przechowuje wiadomości, które otrzymuje Centrum IoT w Twoim magazynie w tabeli.</span><span class="sxs-lookup"><span data-stu-id="4acdb-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="4acdb-200">Można użyć hello **Uruchom** przycisk tootest hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4acdb-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="4acdb-201">Po kliknięciu **Uruchom**, tooyour Centrum IoT jest wysłać wiadomości testowej hello.</span><span class="sxs-lookup"><span data-stu-id="4acdb-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="4acdb-202">Hello nadejście wiadomości powitania powinien wyzwolenia hello funkcji aplikacji toostart, a następnie zapisz magazynu tabel tooyour wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="4acdb-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="4acdb-203">Witaj **dzienniki** okienko rejestruje szczegóły hello hello procesu.</span><span class="sxs-lookup"><span data-stu-id="4acdb-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="4acdb-204">Sprawdź wiadomość w Twoim magazynie w tabeli</span><span class="sxs-lookup"><span data-stu-id="4acdb-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="4acdb-205">Uruchom hello przykładowej aplikacji w Centrum IoT tooyour wiadomości toosend urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4acdb-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="4acdb-206">[Pobieranie i instalowanie Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4acdb-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="4acdb-207">Otwórz Eksploratora usługi Storage, kliknij pozycję **Dodaj konto usługi Azure** > **Zaloguj**, a następnie zaloguj tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4acdb-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="4acdb-208">Kliknij subskrypcję platformy Azure > **kont magazynu** > Twoje konto magazynu > **tabel** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="4acdb-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="4acdb-209">Powinny pojawić się komunikaty wysyłane z Centrum IoT tooyour urządzenia zarejestrowane w hello `deviceData` tabeli.</span><span class="sxs-lookup"><span data-stu-id="4acdb-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4acdb-210">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4acdb-210">Next steps</span></span>

<span data-ttu-id="4acdb-211">Pomyślnie utworzono Twoje konto usługi Azure storage i Azure funkcji aplikacji, która przechowuje komunikaty odbieranych przez Centrum IoT w Twoim magazynie w tabeli.</span><span class="sxs-lookup"><span data-stu-id="4acdb-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
