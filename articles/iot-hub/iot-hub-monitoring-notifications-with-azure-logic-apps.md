---
title: "zdalne monitorowanie aaaIoT i powiadomienia przy użyciu usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Logic Apps IoT temperatury monitorowania w Centrum IoT i automatycznie wysyłać skrzynki pocztowej tooyour powiadomienia e-mail dla wszelkich wykrytych nieprawidłowości."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: monitorowanie powiadomienia iot iot monitorowania temperatury iot
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="ab492-104">Zdalne monitorowanie IoT i powiadomienia przy użyciu usługi Azure Logic Apps łączenia z Centrum IoT i skrzynek pocztowych</span><span class="sxs-lookup"><span data-stu-id="ab492-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="ab492-106">Aplikacje logiki platformy Azure umożliwia procesów tooautomate jako serię kroków.</span><span class="sxs-lookup"><span data-stu-id="ab492-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="ab492-107">Aplikacja logiki mogą się łączyć przez różnych usług i protokołów.</span><span class="sxs-lookup"><span data-stu-id="ab492-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="ab492-108">Rozpoczyna się wyzwalacz takich jak "Po dodaniu konta" i następuje kombinacją akcji, jak "wysyła powiadomienie wypychane".</span><span class="sxs-lookup"><span data-stu-id="ab492-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="ab492-109">Ta funkcja umożliwia Logic Apps to idealne rozwiązanie IoT dla IoT monitorowania, takich jak pozostaje alert w celu wykrycia nieprawidłowości, między innymi scenariusze użycia.</span><span class="sxs-lookup"><span data-stu-id="ab492-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ab492-110">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="ab492-110">What you learn</span></span>

<span data-ttu-id="ab492-111">Dowiesz się, jak toocreate aplikacji logiki łączącej centrum IoT i skrzynki pocztowej temperatury monitorowania i powiadomień.</span><span class="sxs-lookup"><span data-stu-id="ab492-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="ab492-112">Gdy temperatury hello jest ponad 30 C, hello znaczniki aplikacji klienta `temperatureAlert = "true"` w wiadomości powitania wysyła tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ab492-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="ab492-113">wiadomości powitania wyzwalaczy hello toosend aplikacji logiki możesz wiadomość e-mail z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="ab492-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ab492-114">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="ab492-114">What you do</span></span>

* <span data-ttu-id="ab492-115">Utwórz przestrzeń nazw magistrali usług i Dodaj tooit kolejki.</span><span class="sxs-lookup"><span data-stu-id="ab492-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="ab492-116">Dodawanie punktu końcowego i routingu Centrum IoT tooyour reguły.</span><span class="sxs-lookup"><span data-stu-id="ab492-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="ab492-117">Tworzenie, konfigurowanie i testowanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ab492-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ab492-118">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="ab492-118">What you need</span></span>

* <span data-ttu-id="ab492-119">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="ab492-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="ab492-120">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab492-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="ab492-121">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ab492-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="ab492-122">Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ab492-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="ab492-123">Utwórz przestrzeń nazw magistrali usług i Dodaj tooit kolejki</span><span class="sxs-lookup"><span data-stu-id="ab492-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="ab492-124">Utwórz przestrzeń nazw magistrali usług</span><span class="sxs-lookup"><span data-stu-id="ab492-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="ab492-125">Na powitania [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **integracji przedsiębiorstwa** > **usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="ab492-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="ab492-126">Podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ab492-126">Provide hello following information:</span></span>

   <span data-ttu-id="ab492-127">**Nazwa**: Nazwa hello hello service Bus.</span><span class="sxs-lookup"><span data-stu-id="ab492-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="ab492-128">**Warstwa cenowa**: kliknij **podstawowe** > **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="ab492-129">Warstwa podstawowa Hello jest wystarczająca dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ab492-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="ab492-130">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ab492-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="ab492-131">**Lokalizacja**: Użyj hello sam lokalizacji, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ab492-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="ab492-132">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-132">Click **Create**.</span></span>

   ![Utwórz przestrzeń nazw magistrali usług w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="ab492-134">Dodaj kolejką usługi service bus</span><span class="sxs-lookup"><span data-stu-id="ab492-134">Add a service bus queue</span></span>

1. <span data-ttu-id="ab492-135">Otwórz hello przestrzeń nazw magistrali usług, a następnie kliknij przycisk **+ kolejki**.</span><span class="sxs-lookup"><span data-stu-id="ab492-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="ab492-136">Wprowadź nazwę kolejki hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="ab492-137">Otwórz hello kolejką usługi service bus, a następnie kliknij przycisk **zasady dostępu współużytkowanego** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ab492-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="ab492-138">Wprowadź nazwę zasady hello wyboru **Zarządzaj**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Dodaj kolejką usługi service bus w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="ab492-140">Dodawanie punktu końcowego i routingu Centrum IoT tooyour reguły</span><span class="sxs-lookup"><span data-stu-id="ab492-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="ab492-141">Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="ab492-141">Add an endpoint</span></span>

1. <span data-ttu-id="ab492-142">Otwórz Centrum IoT, kliknij punkty końcowe > + Dodaj.</span><span class="sxs-lookup"><span data-stu-id="ab492-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="ab492-143">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ab492-143">Enter hello following information:</span></span>

   <span data-ttu-id="ab492-144">**Nazwa**: hello Nazwa punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="ab492-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="ab492-145">**Typ punktu końcowego**: Wybierz **kolejką usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="ab492-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="ab492-146">**Przestrzeń nazw magistrali usług**: Wybierz nazw hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ab492-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="ab492-147">**Kolejki usługi Service Bus**: kolejki hello wybierz utworzony.</span><span class="sxs-lookup"><span data-stu-id="ab492-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="ab492-148">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab492-148">Click **OK**.</span></span>

   ![Dodawanie punktu końcowego Centrum IoT tooyour w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="ab492-150">Dodaj regułę routingu</span><span class="sxs-lookup"><span data-stu-id="ab492-150">Add a routing rule</span></span>

1. <span data-ttu-id="ab492-151">W Centrum IoT kliknij **tras** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ab492-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="ab492-152">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ab492-152">Enter hello following information:</span></span>

   <span data-ttu-id="ab492-153">**Nazwa**: hello nazwa hello reguły routingu.</span><span class="sxs-lookup"><span data-stu-id="ab492-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="ab492-154">**Źródło danych**: Wybierz **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="ab492-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="ab492-155">**Punkt końcowy**: Wybierz hello punkt końcowy został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ab492-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="ab492-156">**Długość ciągu zapytania**: wprowadź `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="ab492-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="ab492-157">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-157">Click **Save**.</span></span>

   ![Dodaj regułę routingu w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="ab492-159">Tworzenie i konfigurowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ab492-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="ab492-160">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ab492-160">Create a logic app</span></span>

1. <span data-ttu-id="ab492-161">W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **integracji przedsiębiorstwa** > **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="ab492-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="ab492-162">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ab492-162">Enter hello following information:</span></span>

   <span data-ttu-id="ab492-163">**Nazwa**: Nazwa hello hello logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab492-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="ab492-164">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ab492-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="ab492-165">**Lokalizacja**: Użyj hello sam lokalizacji, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ab492-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="ab492-166">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="ab492-167">Skonfiguruj aplikację logiki hello</span><span class="sxs-lookup"><span data-stu-id="ab492-167">Configure hello logic app</span></span>

1. <span data-ttu-id="ab492-168">Otwórz aplikację logiki hello otwartym w hello projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ab492-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="ab492-169">W hello projektanta aplikacji logiki, kliknij przycisk **pustą aplikację logiki**.</span><span class="sxs-lookup"><span data-stu-id="ab492-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Uruchom z aplikacji logiki pusty w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="ab492-171">Kliknij przycisk **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="ab492-171">Click **Service Bus**.</span></span>

   ![Wybierz opcję tworzenia aplikacji logiki w portalu Azure hello toostart usługi Service Bus](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="ab492-173">Kliknij przycisk **usługi Service Bus — nadejściu jedną lub więcej wiadomości w kolejce (automatycznie uzupełniać)**.</span><span class="sxs-lookup"><span data-stu-id="ab492-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="ab492-174">Utwórz połączenia magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="ab492-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="ab492-175">Wprowadź nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="ab492-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="ab492-176">Kliknij przestrzeń nazw magistrali usług hello > hello zasad magistrali usługi > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Tworzenie połączenia magistrali usługi aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="ab492-178">Kliknij przycisk **Kontynuuj** po utworzeniu połączenia magistrali usługi hello.</span><span class="sxs-lookup"><span data-stu-id="ab492-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="ab492-179">Wybierz kolejki hello, który został utworzony i wprowadź `175` dla **maksymalna liczba komunikatów**</span><span class="sxs-lookup"><span data-stu-id="ab492-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Określ liczbę maksymalną wiadomość hello połączenia magistrali usługi hello w aplikacji logiki](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="ab492-181">Kliknij przycisk Zapisz, przycisk toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="ab492-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="ab492-182">Utwórz połączenie usługi SMTP.</span><span class="sxs-lookup"><span data-stu-id="ab492-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="ab492-183">Kliknij przycisk **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="ab492-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="ab492-184">Typ `SMTP`, kliknij przycisk hello **SMTP** usług w wyniku wyszukiwania hello, a następnie kliknij przycisk **SMTP — Wyślij wiadomość E-mail**.</span><span class="sxs-lookup"><span data-stu-id="ab492-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Tworzenie połączenia protokołu SMTP w aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="ab492-186">Wprowadź informacje hello SMTP skrzynki pocztowej, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Wprowadź informacje o połączeniu SMTP w aplikacji logiki w hello portalu Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="ab492-188">Pobierz informacje hello SMTP dla [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), i [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="ab492-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="ab492-189">Wprowadź adres e-mail dla **z** i **do**, i `High temperature detected` dla **podmiotu** i **treści**.</span><span class="sxs-lookup"><span data-stu-id="ab492-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="ab492-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ab492-190">Click **Save**.</span></span>

<span data-ttu-id="ab492-191">Aplikacja logiki Hello jest w stanie podczas zapisywania.</span><span class="sxs-lookup"><span data-stu-id="ab492-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="ab492-192">Przetestuj aplikację logiki hello</span><span class="sxs-lookup"><span data-stu-id="ab492-192">Test hello logic app</span></span>

1. <span data-ttu-id="ab492-193">Uruchomić aplikacji klienckiej hello wdrażanego urządzenia tooyour w [tooAzure ESP8266 połączenia Centrum IoT](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab492-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="ab492-194">Zwiększ temperatury środowiska hello wokół toobe Sensor tag hello powyżej 30 C. Na przykład jasny świecy wokół Twojej Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="ab492-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="ab492-195">Otrzymasz wiadomość e-mail z powiadomieniem wysyłanych przez aplikację logiki hello.</span><span class="sxs-lookup"><span data-stu-id="ab492-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab492-196">Usługodawca poczty e-mail może być konieczne jest użytkownik, który wysyła wiadomości e-mail hello toomake tożsamość nadawcy hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="ab492-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab492-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab492-197">Next steps</span></span>

<span data-ttu-id="ab492-198">Pomyślnie utworzono aplikację logiki, która łączy Centrum IoT i skrzynki pocztowej temperatury monitorowania i powiadomień.</span><span class="sxs-lookup"><span data-stu-id="ab492-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
