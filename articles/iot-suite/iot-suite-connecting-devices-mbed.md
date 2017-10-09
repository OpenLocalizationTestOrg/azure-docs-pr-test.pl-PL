---
title: "aaaConnect urządzenia za pomocą C na mbed | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconnect toohello urządzenia pakiet IoT Azure wstępnie zdalnego rozwiązanie monitorowania przy użyciu Aplikacja napisana w języku C działającej na urządzeniu mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="01b96-103">Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (mbed)</span><span class="sxs-lookup"><span data-stu-id="01b96-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="01b96-104">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="01b96-104">Scenario overview</span></span>
<span data-ttu-id="01b96-105">W tym scenariuszu, Utwórz urządzenie, które wysyła powitania po monitorowania zdalnego toohello telemetrii [wstępnie skonfigurowane rozwiązanie][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="01b96-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="01b96-106">Temperatura zewnętrzna</span><span class="sxs-lookup"><span data-stu-id="01b96-106">External temperature</span></span>
* <span data-ttu-id="01b96-107">Temperatura wewnętrzna</span><span class="sxs-lookup"><span data-stu-id="01b96-107">Internal temperature</span></span>
* <span data-ttu-id="01b96-108">Wilgotność</span><span class="sxs-lookup"><span data-stu-id="01b96-108">Humidity</span></span>

<span data-ttu-id="01b96-109">Dla uproszczenia kodu hello na urządzeniu hello generuje przykładowe wartości, ale firma Microsoft zachęca możesz tooextend hello próbki podłączania urządzenia tooyour rzeczywistych czujników i wysyła rzeczywistych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="01b96-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="01b96-110">urządzenie Hello jest również toomethods toorespond można wywołać z poziomu pulpitu nawigacyjnego rozwiązania hello i potrzebne wartości właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="01b96-111">toocomplete tego samouczka potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="01b96-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="01b96-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="01b96-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="01b96-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="01b96-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="01b96-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="01b96-114">Before you start</span></span>
<span data-ttu-id="01b96-115">Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="01b96-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="01b96-116">Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="01b96-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="01b96-117">urządzenie Hello Utwórz w tym samouczku wysyła dane wystąpienia tooan hello [monitorowania zdalnego] [ lnk-remote-monitoring] wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="01b96-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="01b96-118">Jeśli nie zostało już przydzielona hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie w konta platformy Azure, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="01b96-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="01b96-119">Na powitania <https://www.azureiotsuite.com/> kliknij przycisk  **+**  toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="01b96-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="01b96-120">Kliknij przycisk **wybierz** na powitania **monitorowania zdalnego** panelu toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="01b96-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="01b96-121">Na powitania **utworzyć zdalnego rozwiązanie monitorujące** wprowadź **Nazwa rozwiązania** wybranych przez użytkownika, wybierz hello **Region** toodeploy do, a następnie wybierz hello Azure toouse toowant subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01b96-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="01b96-122">Następnie kliknij pozycję **Utwórz rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="01b96-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="01b96-123">Poczekaj na zakończenie procesu udostępniania hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="01b96-124">rozwiązania Hello wstępnie skonfigurowane za pomocą usług Azure rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="01b96-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="01b96-125">Pamiętaj, że tooremove hello wstępnie skonfigurowane rozwiązanie z subskrypcji, gdy wszystko będzie gotowe z nim tooavoid opłaty niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="01b96-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="01b96-126">Wstępnie skonfigurowane rozwiązanie można całkowicie usunąć z subskrypcji, odwiedzając hello <https://www.azureiotsuite.com/> strony.</span><span class="sxs-lookup"><span data-stu-id="01b96-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="01b96-127">Po zakończeniu hello inicjowania obsługi administracyjnej proces hello zdalnego rozwiązanie monitorujące, kliknij przycisk **uruchamianie** pulpit nawigacyjny rozwiązania hello tooopen w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="01b96-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="01b96-129">Zapewnij urządzenia w hello zdalne monitorowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="01b96-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="01b96-130">Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="01b96-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="01b96-131">Należy tooknow hello urządzenia poświadczeń podczas tworzenia powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01b96-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="01b96-132">Jako rozwiązanie toohello wstępnie tooconnect urządzenia, jego musi identyfikacji tooIoT Centrum używając poprawnych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="01b96-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="01b96-133">Pulpit nawigacyjny rozwiązania hello może pobrać poświadczenia urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="01b96-134">Wprowadzono poświadczenia urządzeń hello w dalszej części tego samouczka aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="01b96-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="01b96-135">tooadd urządzenia tooyour zdalnego rozwiązanie monitorowania pełną hello następujące kroki na pulpicie nawigacyjnym rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="01b96-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="01b96-136">W hello lewym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **dodać urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="01b96-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Dodawanie urządzenia][1]
2. <span data-ttu-id="01b96-138">W hello **urządzenia niestandardowe** panelu, kliknij przycisk **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="01b96-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Dodawanie urządzenia niestandardowego][2]
3. <span data-ttu-id="01b96-140">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="01b96-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="01b96-141">Wprowadź identyfikator urządzenia, takie jak **mydevice**, kliknij przycisk **Sprawdź identyfikator** tooverify tej nazwie nie jest już w użyciu, a następnie kliknij **Utwórz** tooprovision hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="01b96-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Dodawanie identyfikatora urządzenia][3]
4. <span data-ttu-id="01b96-143">Należy skonfigurować urządzenie hello Uwaga poświadczeń (identyfikator urządzenia, nazwy hosta Centrum IoT i klucz urządzenia).</span><span class="sxs-lookup"><span data-stu-id="01b96-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="01b96-144">Aplikacja kliencka musi zdalne monitorowanie rozwiązania toohello tooconnect tych wartości.</span><span class="sxs-lookup"><span data-stu-id="01b96-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="01b96-145">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="01b96-145">Then click **Done**.</span></span>
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. <span data-ttu-id="01b96-147">Wybierz urządzenie na liście urządzeń hello na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="01b96-148">Następnie w hello **szczegóły urządzenia** panelu, kliknij przycisk **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="01b96-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="01b96-149">Witaj stan urządzenia jest teraz **systemem**.</span><span class="sxs-lookup"><span data-stu-id="01b96-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="01b96-150">rozwiązanie monitorowania zdalnego Hello teraz może odbierać dane telemetryczne z urządzenia i wywołania metod na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="01b96-151">Tworzenie i uruchamianie hello C przykładowe rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="01b96-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="01b96-152">Witaj poniższe instrukcje przedstawiają kroki hello podłączania [włączone mbed FRDM K64F Freescale] [ lnk-mbed-home] toohello urządzenie zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="01b96-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="01b96-153">Połącz hello mbed urządzenia tooyour sieci i komputerów</span><span class="sxs-lookup"><span data-stu-id="01b96-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="01b96-154">Połącz hello mbed urządzenia tooyour sieci przy użyciu kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="01b96-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="01b96-155">Ten krok jest niezbędny, ponieważ hello przykładowej aplikacji wymaga dostępu do Internetu.</span><span class="sxs-lookup"><span data-stu-id="01b96-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="01b96-156">Zobacz [wprowadzenie mbed] [ lnk-mbed-getstarted] tooconnect mbed urządzenia tooyour pulpitu komputera.</span><span class="sxs-lookup"><span data-stu-id="01b96-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="01b96-157">Jeśli komputer pulpitu systemu Windows, zobacz [konfigurację komputera] [ lnk-mbed-pcconnect] tooconfigure portu szeregowego dostępu tooyour mbed urządzenia.</span><span class="sxs-lookup"><span data-stu-id="01b96-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="01b96-158">Utwórz projekt mbed i zaimportować hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="01b96-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="01b96-159">Wykonaj te kroki tooadd niektórych przykładowy kod tooan mbed projekt.</span><span class="sxs-lookup"><span data-stu-id="01b96-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="01b96-160">Możesz zaimportować hello zdalnego monitorowania starter projektu, a następnie zmień hello projektu toouse hello protokołu MQTT zamiast hello protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="01b96-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="01b96-161">Obecnie należy toouse hello MQTT protokołu toouse hello funkcji zarządzania urządzeniami Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="01b96-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="01b96-162">W przeglądarce sieci web przejdź toohello mbed.org [deweloperskiej](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="01b96-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="01b96-163">Jeśli masz utworzonego konta, zobaczysz opcję toocreate konta (jest bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="01b96-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="01b96-164">W przeciwnym razie Zaloguj się przy użyciu poświadczeń konta.</span><span class="sxs-lookup"><span data-stu-id="01b96-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="01b96-165">Następnie kliknij przycisk **kompilatora** w hello prawym górnym rogu strony hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="01b96-166">Ta akcja powoduje toohello *obszaru roboczego* interfejsu.</span><span class="sxs-lookup"><span data-stu-id="01b96-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="01b96-167">Upewnij się, platforma sprzętowa hello używanego pojawia się w hello prawym górnym rogu okna hello, lub kliknij ikonę hello w tooselect prawym rogu hello platformy sprzętu.</span><span class="sxs-lookup"><span data-stu-id="01b96-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="01b96-168">Kliknij przycisk **importu** na powitania w menu głównym.</span><span class="sxs-lookup"><span data-stu-id="01b96-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="01b96-169">Następnie kliknij przycisk **kliknij tutaj tooimport z adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="01b96-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Uruchom workspace toombed importu][6]

1. <span data-ttu-id="01b96-171">W oknie podręcznym hello, wprowadź łącze hello hello przykładowy kod https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, a następnie kliknij przycisk **importu**.</span><span class="sxs-lookup"><span data-stu-id="01b96-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importuj roboczym toombed kod przykładowy][7]

1. <span data-ttu-id="01b96-173">W oknie kompilatora mbed hello widać, że importowanie tego projektu również importuje bibliotek różnych.</span><span class="sxs-lookup"><span data-stu-id="01b96-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="01b96-174">Niektóre są dostarczane i obsługiwane przez zespół Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), a inne są dostępne w katalogu bibliotek mbed hello bibliotek innych firm.</span><span class="sxs-lookup"><span data-stu-id="01b96-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Widok projektu mbed][8]

1. <span data-ttu-id="01b96-176">W hello **obszaru roboczego programu**, powitania kliknij prawym przyciskiem myszy **Centrum iothub\_amqp\_transportu** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="01b96-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="01b96-177">W hello **obszaru roboczego programu**, powitania kliknij prawym przyciskiem myszy **azure\_amqp\_c** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="01b96-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="01b96-178">Powitania kliknij prawym przyciskiem myszy **remote_monitoring** projektu w hello **obszaru roboczego programu**, wybierz pozycję **biblioteki importu**, a następnie wybierz pozycję **z adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="01b96-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Uruchom obszaru roboczego Biblioteka importu toombed][6]

1. <span data-ttu-id="01b96-180">W oknie podręcznym hello, wprowadź łącze hello hello MQTT transportu biblioteki https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transportu / kliknięcie **importu**.</span><span class="sxs-lookup"><span data-stu-id="01b96-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importuj obszaru roboczego Biblioteka toombed][12]

1. <span data-ttu-id="01b96-182">Powtórz hello poprzedniego kroku tooadd hello MQTT biblioteki z https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="01b96-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="01b96-183">Obszar roboczy teraz wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="01b96-183">Your workspace now looks like hello following:</span></span>

    ![Wyświetl obszar roboczy mbed][13]

1. <span data-ttu-id="01b96-185">Otwórz hello zdalnego\_monitoring\remote_monitoring.c plików i Zastąp hello istniejących `#include` instrukcji z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="01b96-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="01b96-186">Usuń wszystkie hello pozostałych kodu w hello zdalnego\_monitoring\remote\_monitoring.c pliku.</span><span class="sxs-lookup"><span data-stu-id="01b96-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="01b96-187">Tworzenie i uruchamianie przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="01b96-187">Build and run hello sample</span></span>

<span data-ttu-id="01b96-188">Dodaj kod tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="01b96-189">Dodaj **głównego** funkcji z następujący kod na końcu hello hello zdalnego\_monitoring.c pliku tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji:</span><span class="sxs-lookup"><span data-stu-id="01b96-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="01b96-190">Kliknij przycisk **skompilować** toobuild hello program.</span><span class="sxs-lookup"><span data-stu-id="01b96-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="01b96-191">Można bezpiecznie zignorować ostrzeżenia, ale jeśli kompilacji hello generuje błędy, usuń je przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="01b96-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="01b96-192">Jeśli hello kompilacja zakończy się pomyślnie, witryny sieci Web hello mbed kompilatora generuje plik bin o nazwie hello projektu i pobiera go tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="01b96-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="01b96-193">Kopiuj hello bin pliku toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="01b96-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="01b96-194">Zapisywanie hello bin pliku toohello urządzenia powoduje hello toorestart urządzenia i uruchom program hello zawarte w pliku bin hello.</span><span class="sxs-lookup"><span data-stu-id="01b96-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="01b96-195">Można ręcznie uruchomić ponownie hello program w dowolnym momencie naciśnięcie przycisku resetowania hello na powitania mbed urządzenia.</span><span class="sxs-lookup"><span data-stu-id="01b96-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="01b96-196">Podłącz urządzenie toohello za pomocą aplikacji klienckiej SSH, takiego jak PuTTY.</span><span class="sxs-lookup"><span data-stu-id="01b96-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="01b96-197">Można określić hello portu szeregowego, używanych przez urządzenia, sprawdzając Menedżera urządzeń z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="01b96-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="01b96-198">W programu PuTTY, kliknij przycisk hello **Serial** typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="01b96-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="01b96-199">zwykle łączy urządzenie Hello na 9600 transmisji, dlatego należy wprowadzić 9600 w hello **szybkości** pole.</span><span class="sxs-lookup"><span data-stu-id="01b96-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="01b96-200">Następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="01b96-200">Then click **Open**.</span></span>

1. <span data-ttu-id="01b96-201">Hello program rozpoczyna wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="01b96-201">hello program starts executing.</span></span> <span data-ttu-id="01b96-202">Jeśli hello program nie zostanie uruchomiony automatycznie po połączeniu, może być tooreset hello tablicy (naciśnij klawisze CTRL + Break lub tablicy hello naciśnij przycisk reset).</span><span class="sxs-lookup"><span data-stu-id="01b96-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
