---
title: "Podłącz urządzenie za pomocą C na mbed | Dokumentacja firmy Microsoft"
description: "Opisuje sposób podłącz urządzenie do wstępnie pakiet IoT Azure zdalnego monitorowania rozwiązania przy użyciu Aplikacja napisana w języku C działającej na urządzeniu mbed."
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="c16f0-103">Podłącz urządzenie do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania (mbed)</span><span class="sxs-lookup"><span data-stu-id="c16f0-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="c16f0-104">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="c16f0-104">Scenario overview</span></span>
<span data-ttu-id="c16f0-105">W tym scenariuszu utworzysz urządzenie, które wysyła następujące dane telemetryczne do [wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="c16f0-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="c16f0-106">Temperatura zewnętrzna</span><span class="sxs-lookup"><span data-stu-id="c16f0-106">External temperature</span></span>
* <span data-ttu-id="c16f0-107">Temperatura wewnętrzna</span><span class="sxs-lookup"><span data-stu-id="c16f0-107">Internal temperature</span></span>
* <span data-ttu-id="c16f0-108">Wilgotność</span><span class="sxs-lookup"><span data-stu-id="c16f0-108">Humidity</span></span>

<span data-ttu-id="c16f0-109">Dla uproszczenia kod na urządzeniu generuje przykładowe wartości, ale zachęcamy do rozszerzenia przykładu przez podłączenie rzeczywistych czujników do urządzenia i wysyłanie rzeczywistych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="c16f0-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="c16f0-110">Urządzenie potrafi także odpowiadać na metody wywołane z poziomu pulpitu nawigacyjnego rozwiązania i wartości żądanych właściwości ustawione na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="c16f0-111">Do wykonania kroków tego samouczka jest potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c16f0-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="c16f0-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c16f0-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c16f0-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="c16f0-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c16f0-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c16f0-114">Before you start</span></span>
<span data-ttu-id="c16f0-115">Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="c16f0-116">Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="c16f0-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="c16f0-117">Urządzenie, które utworzysz w ramach tego samouczka, będzie wysyłać dane do wystąpienia wstępnie skonfigurowanego rozwiązania do [monitorowania zdalnego][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="c16f0-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="c16f0-118">Jeśli jeszcze nie przeprowadzono aprowizacji wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego na Twoim koncie platformy Azure, wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="c16f0-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="c16f0-119">Na stronie <https://www.azureiotsuite.com/> kliknij pozycję **+**, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="c16f0-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="c16f0-120">Kliknij pozycję **Wybierz** w panelu **Monitorowanie zdalne**, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="c16f0-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="c16f0-121">Na stronie **Tworzenie rozwiązania do monitorowania zdalnego** w polu **Nazwa rozwiązania** wprowadź wybraną nazwę rozwiązania, w polu **Region** wybierz region, w którym chcesz przeprowadzić wdrożenie, a następnie wybierz subskrypcję platformy Azure, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="c16f0-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="c16f0-122">Następnie kliknij pozycję **Utwórz rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="c16f0-123">Zaczekaj na ukończenie procesu aprowizowania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="c16f0-124">Wstępnie skonfigurowane rozwiązania korzystają z płatnych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c16f0-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="c16f0-125">Pamiętaj o usunięciu wstępnie skonfigurowanego rozwiązania ze swojej subskrypcji po zakończeniu pracy z nim, aby uniknąć wszelkich zbędnych opłat.</span><span class="sxs-lookup"><span data-stu-id="c16f0-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="c16f0-126">Możesz całkowicie usunąć wstępnie skonfigurowane rozwiązanie ze swojej subskrypcji, odwiedzając stronę <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="c16f0-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="c16f0-127">Po zakończeniu procesu aprowizowania rozwiązania do monitorowania zdalnego kliknij pozycję **Uruchom**, aby otworzyć pulpit nawigacyjny rozwiązania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c16f0-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="c16f0-129">Aprowizowanie urządzenia w ramach rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="c16f0-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="c16f0-130">Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="c16f0-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="c16f0-131">Podczas tworzenia aplikacji klienckiej musisz znać poświadczenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c16f0-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="c16f0-132">Aby urządzenie mogło nawiązać połączenie ze wstępnie skonfigurowanym rozwiązaniem, musi ono zidentyfikować się względem usługi IoT Hub za pomocą prawidłowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c16f0-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="c16f0-133">Poświadczenia urządzenia możesz pobrać z pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="c16f0-134">W dalszej części tego samouczka podasz te poświadczenia urządzenia w Twojej aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="c16f0-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="c16f0-135">Aby dodać urządzenie do swojego rozwiązania do monitorowania zdalnego, wykonaj poniższe kroki na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="c16f0-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="c16f0-136">W lewym dolnym rogu pulpitu nawigacyjnego kliknij pozycję **Dodaj urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Dodawanie urządzenia][1]
2. <span data-ttu-id="c16f0-138">W panelu **Urządzenie niestandardowe** kliknij pozycję **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Dodawanie urządzenia niestandardowego][2]
3. <span data-ttu-id="c16f0-140">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="c16f0-141">Wprowadź identyfikator urządzenia, na przykład **moje_urządzenie**, kliknij pozycję **Sprawdź identyfikator**, aby sprawdzić, czy dana nazwa nie jest już używana, a następnie kliknij pozycję **Utwórz**, aby przeprowadzić aprowizację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c16f0-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Dodawanie identyfikatora urządzenia][3]
4. <span data-ttu-id="c16f0-143">Zanotuj poświadczenia urządzenia (identyfikator urządzenia, nazwę hosta usługi IoT Hub i klucz urządzenia).</span><span class="sxs-lookup"><span data-stu-id="c16f0-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="c16f0-144">Twoja aplikacja kliencka potrzebuje tych wartości, aby mogła nawiązać połączenie z rozwiązaniem do monitorowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="c16f0-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="c16f0-145">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-145">Then click **Done**.</span></span>
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. <span data-ttu-id="c16f0-147">Wybierz urządzenie na liście urządzeń na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="c16f0-148">Następnie w panelu **Szczegóły urządzenia** kliknij pozycję **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="c16f0-149">Stan Twojego urządzenia to teraz **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="c16f0-150">Rozwiązanie do monitorowania zdalnego może teraz odbierać dane telemetryczne z Twojego urządzenia i wywoływać metody na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="c16f0-151">Skompilować i uruchomić przykładowe rozwiązanie C</span><span class="sxs-lookup"><span data-stu-id="c16f0-151">Build and run the C sample solution</span></span>

<span data-ttu-id="c16f0-152">Poniższe instrukcje przedstawiają kroki wymagane do połączenia [włączone mbed FRDM K64F Freescale] [ lnk-mbed-home] urządzenia zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c16f0-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="c16f0-153">Podłącz urządzenie mbed do komputera w sieci i pulpitu</span><span class="sxs-lookup"><span data-stu-id="c16f0-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="c16f0-154">Podłącz urządzenie mbed do sieci przy użyciu kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="c16f0-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="c16f0-155">Ten krok jest niezbędny, ponieważ przykładowej aplikacji wymaga dostępu do Internetu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="c16f0-156">Zobacz [wprowadzenie mbed] [ lnk-mbed-getstarted] Podłącz urządzenie mbed do komputera.</span><span class="sxs-lookup"><span data-stu-id="c16f0-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="c16f0-157">Jeśli komputer pulpitu systemu Windows, zobacz [konfigurację komputera] [ lnk-mbed-pcconnect] do konfigurowania portu szeregowego dostęp do Twojego urządzenia mbed.</span><span class="sxs-lookup"><span data-stu-id="c16f0-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="c16f0-158">Utwórz projekt mbed i zaimportować przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="c16f0-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="c16f0-159">Wykonaj następujące kroki, aby dodać do projektu mbed niektórych przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="c16f0-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="c16f0-160">Możesz zaimportować zdalnego monitorowania projektu starter, a następnie zmień projektu do korzystania z protokołu MQTT zamiast protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="c16f0-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="c16f0-161">Obecnie należy użyć protokołu MQTT do używania funkcji zarządzania urządzeniami Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c16f0-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="c16f0-162">W przeglądarce sieci web, przejdź do mbed.org [deweloperskiej](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="c16f0-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="c16f0-163">Jeśli masz utworzonego konta, zobaczysz opcję, aby utworzyć konto (jest bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="c16f0-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="c16f0-164">W przeciwnym razie Zaloguj się przy użyciu poświadczeń konta.</span><span class="sxs-lookup"><span data-stu-id="c16f0-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="c16f0-165">Następnie kliknij przycisk **kompilatora** w prawym górnym rogu strony.</span><span class="sxs-lookup"><span data-stu-id="c16f0-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="c16f0-166">Ta akcja umożliwia do *obszaru roboczego* interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="c16f0-167">Upewnij się, że platforma sprzętowa, którego używasz, zostanie wyświetlona w prawym górnym rogu okna, lub kliknij ikonę w prawym rogu, aby wybrać platforma sprzętowa.</span><span class="sxs-lookup"><span data-stu-id="c16f0-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="c16f0-168">Kliknij przycisk **importu** w menu głównym.</span><span class="sxs-lookup"><span data-stu-id="c16f0-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="c16f0-169">Następnie kliknij przycisk **kliknij tutaj, aby zaimportować z adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-169">Then click **Click here to import from URL**.</span></span>
   
    ![Uruchom importowanie do obszaru roboczego mbed][6]

1. <span data-ttu-id="c16f0-171">W oknie podręcznym wprowadź link do https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ kod przykładowy, a następnie kliknij przycisk **importu**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importuj przykładowy kod do obszaru roboczego mbed][7]

1. <span data-ttu-id="c16f0-173">W oknie kompilatora mbed widać, że importowanie tego projektu również importuje bibliotek różnych.</span><span class="sxs-lookup"><span data-stu-id="c16f0-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="c16f0-174">Niektóre są dostarczane i obsługiwane przez zespół Azure IoT ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), a inne są dostępne w katalogu bibliotek mbed bibliotek innych firm.</span><span class="sxs-lookup"><span data-stu-id="c16f0-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Widok projektu mbed][8]

1. <span data-ttu-id="c16f0-176">W **obszaru roboczego programu**, kliknij prawym przyciskiem myszy **Centrum iothub\_amqp\_transportu** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="c16f0-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="c16f0-177">W **obszaru roboczego programu**, kliknij prawym przyciskiem myszy **azure\_amqp\_c** biblioteki, kliknij przycisk **usunąć**, a następnie kliknij przycisk **OK** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="c16f0-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="c16f0-178">Kliknij prawym przyciskiem myszy **remote_monitoring** projektu w **obszaru roboczego programu**, wybierz pozycję **biblioteki importu**, a następnie wybierz pozycję **z adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Import biblioteki do obszaru roboczego mbed Start][6]

1. <span data-ttu-id="c16f0-180">W oknie podręcznym wprowadź link do https://developer.mbed.org/users/AzureIoTClient/code/iothub biblioteki transportu MQTT\_mqtt\_transportu / kliknięcie **importu**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importuj biblioteki do obszaru roboczego mbed][12]

1. <span data-ttu-id="c16f0-182">Powtórz poprzedni krok, aby dodać biblioteki MQTT z https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="c16f0-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="c16f0-183">Obszar roboczy teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c16f0-183">Your workspace now looks like the following:</span></span>

    ![Wyświetl obszar roboczy mbed][13]

1. <span data-ttu-id="c16f0-185">Otwórz zdalnego\_monitoring\remote_monitoring.c plików i Zastąp istniejące `#include` instrukcje następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c16f0-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

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
1. <span data-ttu-id="c16f0-186">Usuń wszystkie pozostałe kod w zdalnym\_monitoring\remote\_monitoring.c pliku.</span><span class="sxs-lookup"><span data-stu-id="c16f0-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="c16f0-187">Tworzenie i uruchamianie próbki</span><span class="sxs-lookup"><span data-stu-id="c16f0-187">Build and run the sample</span></span>

<span data-ttu-id="c16f0-188">Dodaj kod, aby wywołać **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c16f0-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="c16f0-189">Dodaj **głównego** funkcji z następujący kod na końcu zdalnego\_monitoring.c pliku do wywołania **zdalnego\_monitorowania\_Uruchom** funkcji:</span><span class="sxs-lookup"><span data-stu-id="c16f0-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="c16f0-190">Kliknij przycisk **skompilować** do tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="c16f0-191">Można bezpiecznie zignorować ostrzeżenia, ale jeśli kompilacja generuje błędy, usuń je przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="c16f0-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="c16f0-192">Jeśli kompilacja zakończy się pomyślnie, witryna kompilatora mbed generuje plik bin z nazwą projektu i pliki do pobrania na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c16f0-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="c16f0-193">Skopiuj plik bin na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="c16f0-194">Zapisywanie pliku bin do urządzenia powoduje, że urządzenie, aby ponownie uruchomić, a następnie uruchom program zawarte w pliku bin.</span><span class="sxs-lookup"><span data-stu-id="c16f0-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="c16f0-195">Można ręcznie uruchomić ponownie program w dowolnym momencie naciśnięcia przycisku resetowania urządzenia mbed.</span><span class="sxs-lookup"><span data-stu-id="c16f0-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="c16f0-196">Nawiąż połączenie z urządzeniem przy użyciu aplikacji klienta SSH, takiego jak PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c16f0-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="c16f0-197">Można określić portu szeregowego, używanych przez urządzenia, sprawdzając Menedżera urządzeń z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c16f0-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="c16f0-198">W programu PuTTY, kliknij przycisk **Serial** typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="c16f0-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="c16f0-199">Urządzenie łączy się zwykle przy transmisji 9600, dlatego należy wprowadzić 9600 w **szybkości** pole.</span><span class="sxs-lookup"><span data-stu-id="c16f0-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="c16f0-200">Następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="c16f0-200">Then click **Open**.</span></span>

1. <span data-ttu-id="c16f0-201">Program rozpoczyna wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="c16f0-201">The program starts executing.</span></span> <span data-ttu-id="c16f0-202">Może zajść potrzeba zresetowania tablicy (naciśnij klawisze CTRL + Break lub naciśnij przycisk reset tablicy), jeśli program nie zostanie uruchomiony automatycznie po połączeniu.</span><span class="sxs-lookup"><span data-stu-id="c16f0-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
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
