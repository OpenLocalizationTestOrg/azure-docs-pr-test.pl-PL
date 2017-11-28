---
title: "dane o czasie aaaReal wizualizacji danych czujnika z Centrum Azure IoT — aplikacji sieci Web | Dokumentacja firmy Microsoft"
description: "Funkcja hello aplikacje sieci Web Microsoft Azure App Service toovisualize temperatury i wilgotności danych, który został zebrany z czujnika hello i wysyłany tooyour Centrum Iot."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "wizualizację danych czasu rzeczywistego, wizualizacji danych na żywo czujnik wizualizacji danych"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="6a255-104">Wizualizacja danych czujnika w czasie rzeczywistym z Centrum Azure IoT za pomocą funkcji Web Apps hello Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6a255-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="6a255-106">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="6a255-106">What you learn</span></span>

<span data-ttu-id="6a255-107">Z tego samouczka dowiesz się, jak danych czujnika w czasie rzeczywistym toovisualize Centrum IoT odbieranych przez uruchomienie aplikacji sieci web, który znajduje się w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6a255-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="6a255-108">Jeśli chcesz tootry toovisualize hello danych w Centrum IoT przy użyciu usługi Power BI, zobacz [danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum IoT Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6a255-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6a255-109">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="6a255-109">What you do</span></span>

- <span data-ttu-id="6a255-110">Tworzenie aplikacji sieci web w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6a255-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="6a255-111">Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="6a255-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="6a255-112">Skonfiguruj hello danych czujnika tooread aplikacji sieci web z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6a255-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="6a255-113">Przekaż toobe aplikacji sieci web, na użytek hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6a255-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="6a255-114">Otwórz hello web toosee w czasie rzeczywistym temperatury i wilgotności danych aplikacji z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6a255-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6a255-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="6a255-115">What you need</span></span>

- <span data-ttu-id="6a255-116">[Urządzenie jest skonfigurowane](iot-hub-raspberry-pi-kit-node-get-started.md), która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="6a255-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="6a255-117">Aktywną subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6a255-117">An active Azure subscription</span></span>
  - <span data-ttu-id="6a255-118">Centrum Iot w ramach Twojej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6a255-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="6a255-119">Aplikacji klienckiej, która wysyła Centrum Iot tooyour wiadomości</span><span class="sxs-lookup"><span data-stu-id="6a255-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="6a255-120">Pobierz narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="6a255-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="6a255-121">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6a255-121">Create a web app</span></span>

1. <span data-ttu-id="6a255-122">W hello [portalu Azure](https://ms.portal.azure.com/), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="6a255-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="6a255-123">Wprowadź nazwę unikatową zadania upewnij się, hello subskrypcji, określ grupę zasobów i lokalizację, wybierz opcję **toodashboard numeru Pin**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6a255-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="6a255-124">Zaleca się, że wybrano hello tej samej lokalizacji co dla Twojej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a255-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="6a255-125">W ten sposób mogą korzystać z szybkość przetwarzania i zmniejsza koszt hello transferu danych.</span><span class="sxs-lookup"><span data-stu-id="6a255-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Tworzenie aplikacji sieci Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="6a255-127">Skonfiguruj hello dane tooread aplikacji sieci web z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="6a255-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="6a255-128">Otwórz aplikację sieci web hello, po prostu aprowizowanej.</span><span class="sxs-lookup"><span data-stu-id="6a255-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="6a255-129">Kliknij przycisk **ustawienia aplikacji**, a następnie w obszarze **ustawień aplikacji**, Dodaj następujące pary klucz wartość hello:</span><span class="sxs-lookup"><span data-stu-id="6a255-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="6a255-130">Klucz</span><span class="sxs-lookup"><span data-stu-id="6a255-130">Key</span></span>                                   | <span data-ttu-id="6a255-131">Wartość</span><span class="sxs-lookup"><span data-stu-id="6a255-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="6a255-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="6a255-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="6a255-133">Uzyskane z Centrum iothub explorer</span><span class="sxs-lookup"><span data-stu-id="6a255-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="6a255-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="6a255-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="6a255-135">Nazwa Hello grupy konsumentów hello dodanie tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="6a255-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Dodawanie aplikacji sieci web tooyour ustawienia z pary klucz wartość](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="6a255-137">Kliknij przycisk **ustawienia aplikacji**w obszarze **ustawienia ogólne**, Przełącz hello **sieci Web sockets** , a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6a255-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Przełącz hello opcja gniazda sieci Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="6a255-139">Przekaż toobe aplikacji sieci web, na użytek hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="6a255-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="6a255-140">W witrynie GitHub wprowadziliśmy dostępności aplikacji sieci web, który wyświetla danych czujnika w czasie rzeczywistym z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6a255-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="6a255-141">Toodo wystarczy skonfigurować toowork aplikacji sieci web hello z repozytorium Git, Pobierz hello aplikacji sieci web z usługi GitHub i przekaż go po tooAzure dla toohost aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="6a255-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="6a255-142">W aplikacji sieci web hello, kliknij przycisk **opcje wdrażania** > **wybierz źródło** > **lokalnego repozytorium Git**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a255-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Konfigurowanie sieci web aplikacji wdrożenia toouse hello lokalnego repozytorium Git](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="6a255-144">Kliknij przycisk **poświadczenia wdrażania**, Utwórz użytkownika nazwę i hasło toouse tooconnect toohello repozytorium Git na platformie Azure, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6a255-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="6a255-145">Kliknij przycisk **omówienie**i zanotuj wartość hello **adres url klonowania Git**.</span><span class="sxs-lookup"><span data-stu-id="6a255-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Pobierz adres URL klonowania Git hello aplikacji sieci web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="6a255-147">Otwórz okno terminalu na komputerze lokalnym lub polecenie.</span><span class="sxs-lookup"><span data-stu-id="6a255-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="6a255-148">Pobierz aplikację sieci web hello z usługi GitHub i przekaż go tooAzure dla toohost aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="6a255-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="6a255-149">toodo tak, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="6a255-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="6a255-150">\<Adres URL klonowania Git\> jest adres URL repozytorium Git hello na powitania hello **omówienie** strony hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6a255-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="6a255-151">Otwórz hello web toosee w czasie rzeczywistym temperatury i wilgotności danych aplikacji z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="6a255-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="6a255-152">Na powitania **omówienie** strony aplikacji sieci web, kliknij przycisk aplikacji hello tooopen hello adres URL w sieci web.</span><span class="sxs-lookup"><span data-stu-id="6a255-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Pobieranie adresu URL hello aplikacji sieci web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="6a255-154">Witaj w czasie rzeczywistym temperatury i wilgotności danych powinny być widoczne z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6a255-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Wyświetlanie w czasie rzeczywistym temperatury i wilgotności strony aplikacji sieci Web](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="6a255-156">Upewnij się, że hello Przykładowa aplikacja jest uruchomiona na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="6a255-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="6a255-157">Nie otrzymasz pusty wykres, może się odwoływać samouczki toohello w obszarze [skonfigurować na twoim urządzeniu](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a255-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a255-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a255-158">Next steps</span></span>
<span data-ttu-id="6a255-159">Pomyślnie zastosowano danych czujnika w czasie rzeczywistym toovisualize aplikacji sieci web z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6a255-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="6a255-160">Alternatywna metoda toovisualize danych z Centrum IoT Azure, zobacz [danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6a255-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
