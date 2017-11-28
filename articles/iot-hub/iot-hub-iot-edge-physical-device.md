---
title: "Urządzenie fizyczne za pomocą usługi Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Jak korzystać z urządzenia Texas Instruments w Sensor tag do wysyłania danych do Centrum IoT przez bramę krawędzi IoT uruchamianie na urządzeniu malina Pi 3. Brama jest utworzony przy użyciu usługi Azure IoT krawędzi."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="9ad5c-104">W systemie Azure IoT krawędzi Pi malina do przekazywania wiadomości urządzenia do chmury do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9ad5c-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="9ad5c-105">Ten przewodnik [próbki niski energii Bluetooth] [ lnk-ble-samplecode] przedstawiono sposób użycia [Azure IoT krawędzi] [ lnk-sdk] do:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="9ad5c-106">Przesyła dane telemetryczne urządzenia do chmury Centrum IoT z urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="9ad5c-107">Trasy poleceń z Centrum IoT urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="9ad5c-108">Przewodnik składa się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-108">This walkthrough covers:</span></span>

* <span data-ttu-id="9ad5c-109">**Architektura**: ważnych architektury informacji dotyczących przykładowych niski energii Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="9ad5c-110">**Kompilowanie i uruchamianie**: czynności wymagane do skompilowania i uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="9ad5c-111">Architektura</span><span class="sxs-lookup"><span data-stu-id="9ad5c-111">Architecture</span></span>

<span data-ttu-id="9ad5c-112">Przewodniku zademonstrowano, jak skompilować i uruchomić brama brzegowa IoT na malina Pi 3 z systemem Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="9ad5c-113">Brama jest utworzony przy użyciu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="9ad5c-114">W przykładzie użyto urządzenia Texas Instruments Sensor tag Bluetooth małej energii (cz) do zbierania danych temperatury.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="9ad5c-115">Po uruchomieniu brama brzegowa IoT go:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="9ad5c-116">Nawiązuje połączenie z urządzeniem Sensor tag przy użyciu protokołu energii małej Bluetooth (cz).</span><span class="sxs-lookup"><span data-stu-id="9ad5c-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="9ad5c-117">Nawiązuje połączenie z Centrum IoT przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="9ad5c-118">Przekazuje dane telemetryczne z urządzeń Sensor tag do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="9ad5c-119">Polecenia tras z Centrum IoT na urządzeniu Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="9ad5c-120">Brama zawiera następujące moduły krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="9ad5c-121">A *modułu cz* który interfejsy z urządzeniem cz otrzymywanie temperatury danych z urządzenia i wysyłać polecenia do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="9ad5c-122">A *cz chmury do urządzenia moduł* konwertujący JSON wiadomości wysyłane z Centrum IoT w instrukcji cz *modułu cz*.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="9ad5c-123">A *modułu rejestratora* który rejestruje komunikaty bramy do lokalnego pliku.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="9ad5c-124">*Moduł mapowania tożsamości* który tłumaczy adresy MAC cz urządzenia i tożsamości urządzenia Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="9ad5c-125">*Modułu Centrum IoT* który przekazuje dane telemetryczne w Centrum IoT i odbiera polecenia urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="9ad5c-126">A *cz drukarki moduł* który interpretuje dane telemetryczne z urządzenia cz i drukowanie sformatowanych danych do konsoli umożliwiające rozwiązywanie problemów i debugowania.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="9ad5c-127">Jak dane przepływają przez bramę</span><span class="sxs-lookup"><span data-stu-id="9ad5c-127">How data flows through the gateway</span></span>

<span data-ttu-id="9ad5c-128">Na poniższym diagramie bloku przedstawiono potoku przepływu danych przekazywania telemetrii:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Potok bramy przekazywania telemetrii](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="9ad5c-130">Dostępne są następujące kroki, które przyjmuje elementu telemetrii podróży z urządzenia cz z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="9ad5c-131">Urządzenie cz generuje próbki temperatury i wysyła je przez sieć Bluetooth modułu cz w bramie.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="9ad5c-132">Moduł cz odbiera próbki i publikuje ją do brokera oraz adres MAC urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="9ad5c-133">Moduł mapowania tożsamości przejmuje ten komunikat i używa wewnętrznej tabeli do tłumaczenia adres MAC urządzenia na tożsamości urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="9ad5c-134">Centrum IoT urządzenia tożsamości składa się z Identyfikatorem urządzenia i klucz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="9ad5c-135">Moduł mapowania tożsamości publikuje nowy komunikat zawierający temperatury przykładowych danych, adres MAC urządzenia, identyfikator urządzenia i klucz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="9ad5c-136">Moduł Centrum IoT to nowego komunikatu (generowane przez moduł mapowania tożsamości) i publikuje go do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="9ad5c-137">Moduł rejestratora rejestruje wszystkie komunikaty z brokera w lokalnym pliku.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="9ad5c-138">Na poniższym diagramie bloku przedstawiono potoku przepływu danych polecenia urządzenia:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Urządzenia polecenie bramy potoku](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="9ad5c-140">Moduł Centrum IoT okresowo sonduje Centrum IoT nowe wiadomości polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="9ad5c-141">Moduł Centrum IoT odebrania nowego komunikatu polecenia publikuje ją do brokera.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="9ad5c-142">Moduł mapowania tożsamości przejmuje komunikat polecenia i używa wewnętrznej tabeli można przetłumaczyć Identyfikatora urządzenia Centrum IoT na adres MAC urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="9ad5c-143">Go następnie publikuje nowy komunikat zawierający adres MAC urządzenia docelowego w planie właściwości komunikatu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="9ad5c-144">Moduł cz chmury do urządzenia przejmuje ten komunikat i przekształca ją w odpowiednie instrukcje cz modułu cz.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="9ad5c-145">Go następnie publikuje nowy komunikat.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="9ad5c-146">Moduł cz przejmuje ten komunikat i wykonuje instrukcję We/Wy przy komunikacji z urządzeniem cz.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="9ad5c-147">Moduł rejestratora rejestruje wszystkie komunikaty z brokera pliku na dysku.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ad5c-148">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ad5c-148">Prerequisites</span></span>

<span data-ttu-id="9ad5c-149">Do wykonania kroków tego samouczka jest potrzebna aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9ad5c-150">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9ad5c-151">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="9ad5c-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="9ad5c-152">Należy klient SSH na komputerze pulpitu umożliwia zdalny dostęp do wiersza polecenia na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="9ad5c-153">System Windows nie zawiera klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="9ad5c-154">Firma Microsoft zaleca używanie [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="9ad5c-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="9ad5c-155">Większość dystrybucje systemu Linux i Mac OS obejmują narzędzia wiersza polecenia SSH.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="9ad5c-156">Aby uzyskać więcej informacji, zobacz [SSH za pomocą systemu Linux lub Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="9ad5c-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="9ad5c-157">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="9ad5c-157">Prepare your hardware</span></span>

<span data-ttu-id="9ad5c-158">Ten samouczek zakłada się, czy używasz [Texas Instruments w Sensor tag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) urządzenie podłączone do uruchamiania Raspbian malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="9ad5c-159">Zainstaluj Raspbian</span><span class="sxs-lookup"><span data-stu-id="9ad5c-159">Install Raspbian</span></span>

<span data-ttu-id="9ad5c-160">Do zainstalowania na urządzeniu malina Pi 3 Raspbian, można użyć jednej z następujących opcji.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="9ad5c-161">Aby zainstalować najnowszą wersję Raspbian, użyj [NOOBS] [ lnk-noobs] graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="9ad5c-162">Ręcznie [Pobierz] [ lnk-raspbian] i zapisywać najnowsze obrazu systemu operacyjnego Raspbian na karcie SD..</span><span class="sxs-lookup"><span data-stu-id="9ad5c-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="9ad5c-163">Zaloguj się i uzyskać dostęp terminala</span><span class="sxs-lookup"><span data-stu-id="9ad5c-163">Sign in and access the terminal</span></span>

<span data-ttu-id="9ad5c-164">Dostępne są dwie opcje środowisku końcowych dla sieci Pi malina dostępu do:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="9ad5c-165">Jeśli masz klawiatury i monitora podłączone do sieci Pi malina umożliwia Raspbian graficzny interfejs użytkownika dostępu okno terminala.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="9ad5c-166">Dostęp do wiersza polecenia na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="9ad5c-167">Okno terminalu w graficznym interfejsie użytkownika</span><span class="sxs-lookup"><span data-stu-id="9ad5c-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="9ad5c-168">Nazwa użytkownika są domyślne poświadczenia dla Raspbian **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="9ad5c-169">Na pasku zadań w interfejsie GUI, uruchom **Terminal** narzędzie przy użyciu ikony, która wygląda jak monitora.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="9ad5c-170">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="9ad5c-170">Sign in with SSH</span></span>

<span data-ttu-id="9ad5c-171">Umożliwia SSH dla wiersza polecenia dostępu użytkownika Pi malina.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="9ad5c-172">Artykuł [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób konfigurowania SSH na Twoje Pi malina oraz sposób nawiązywania połączenia z [Windows] [ lnk-ssh-windows] lub [ System operacyjny Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="9ad5c-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="9ad5c-173">Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="9ad5c-174">Zainstaluj BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="9ad5c-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="9ad5c-175">Moduły cz skontaktować sprzętu Bluetooth za pośrednictwem BlueZ stosu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="9ad5c-176">Wymagana wersja 5.37 BlueZ dla modułów, aby działać poprawnie.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="9ad5c-177">Tych instrukcji upewnij się, że jest zainstalowana prawidłowa wersja BlueZ.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="9ad5c-178">Zatrzymaj bieżącego demona bluetooth:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="9ad5c-179">Zainstaluj zależności BlueZ:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="9ad5c-180">Pobierz kod źródłowy BlueZ z bluez.org:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="9ad5c-181">Rozpakuj kodu źródłowego:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="9ad5c-182">Zmień katalogi na nowo utworzony folder:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="9ad5c-183">Skonfiguruj kodu BlueZ ma zostać utworzony:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="9ad5c-184">Tworzenie BlueZ:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="9ad5c-185">Zainstaluj BlueZ po zakończeniu kompilowania:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="9ad5c-186">Zmienianie konfiguracji usługi systemd Bluetooth, aby wskazywał Nowy demon bluetooth w pliku `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="9ad5c-187">Zastąp linię "ExecStart" następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="9ad5c-188">Włączyć łączność z urządzeń Sensor tag z urządzenia malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="9ad5c-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="9ad5c-189">Przed uruchomieniem próbki, należy sprawdzić, czy Twoje malina Pi 3 można połączyć się z urządzeniem Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="9ad5c-190">Upewnij się, `rfkill` zainstalowano narzędzie:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="9ad5c-191">Odblokowany bluetooth na 3 Pi malina i sprawdź, czy numer wersji jest **5.37**:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="9ad5c-192">Aby wprowadzić powłoki interakcyjne bluetooth, uruchom usługę bluetooth i wykonać **bluetoothctl** polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="9ad5c-193">Wprowadź polecenie **włączania zasilania** do zasilanie kontrolera bluetooth.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="9ad5c-194">Polecenie zwraca dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="9ad5c-195">W powłoce interakcyjne bluetooth, wprowadź polecenie **na skanowania** skanowania pod kątem urządzenia bluetooth.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="9ad5c-196">Polecenie zwraca dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="9ad5c-197">Urządzeń Sensor tag stał się wykrywalny, naciskając przycisk małe (zielony LED powinien flash).</span><span class="sxs-lookup"><span data-stu-id="9ad5c-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="9ad5c-198">Pi 3 malina powinien odnajdywanie urządzeń Sensor tag:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="9ad5c-199">W tym przykładzie widać, że adres MAC urządzenia Sensor tag jest **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="9ad5c-200">Wyłącz skanowanie wprowadzając **skanowania poza** polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="9ad5c-201">Łączenie się z urządzeniem Sensor tag przy użyciu adresu MAC, wprowadzając **połączyć \<adres MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="9ad5c-202">Następujące przykładowe dane wyjściowe jest skracana dla jasności:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="9ad5c-203">Możesz wyświetlić listę właściwości GATT urządzenia ponownie, używając **listę atrybutów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="9ad5c-204">Teraz możesz odłączyć z urządzeniami przy użyciu **rozłączyć** polecenia, a następnie Zamknij z powłoki bluetooth przy użyciu **Zamknij** polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="9ad5c-205">Teraz możesz uruchomić przykładowy krawędzi IoT cz na Twoje malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="9ad5c-206">Uruchamianie przykładowych cz krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="9ad5c-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="9ad5c-207">Aby uruchomić przykładowe cz krawędzi IoT, należy wykonać trzy zadania:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="9ad5c-208">Skonfiguruj dwa przykładowe urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="9ad5c-209">Tworzenie IoT Edge na urządzeniu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="9ad5c-210">Konfigurowania i uruchamiania przykładowych cz na urządzeniu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="9ad5c-211">W momencie pisania krawędzi IoT obsługuje modułów cz tylko w bramy z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="9ad5c-212">Skonfiguruj dwa przykładowe urządzenia w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9ad5c-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="9ad5c-213">[Tworzenie Centrum IoT] [ lnk-create-hub] w Twojej subskrypcji platformy Azure, potrzebna jest nazwa Centrum w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="9ad5c-214">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="9ad5c-215">Dodaj urządzenia o nazwie **SensorTag_01** do Centrum IoT i zanotować jego klucza identyfikator i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="9ad5c-216">Można użyć [explorer urządzenie lub Centrum iothub explorer] [ lnk-explorer-tools] narzędzia dodać to urządzenie w Centrum IoT utworzony w poprzednim kroku, a następnie pobrać jego klucza.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="9ad5c-217">To urządzenie należy mapować urządzeń Sensor tag podczas konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="9ad5c-218">Tworzenie Azure IoT krawędzi w Twojej malinowe Pi 3</span><span class="sxs-lookup"><span data-stu-id="9ad5c-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="9ad5c-219">Zainstaluj zależności Edge IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="9ad5c-220">Klonowanie krawędzi IoT i wszystkie jego modułów podrzędnych do katalogu macierzystego, należy użyć następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="9ad5c-221">Jeśli masz pełną kopię repozytorium krawędzi IoT na Twoje malina Pi 3 można tworzyć za pomocą następującego polecenia z folderu, który zawiera zestaw SDK:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="9ad5c-222">Konfigurowanie i uruchamianie przykładowych cz na Twoje malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="9ad5c-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="9ad5c-223">Bootstrap i uruchomić próbki, należy skonfigurować każdy moduł IoT krawędzi, który uczestniczy w bramie.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="9ad5c-224">Tej konfiguracji znajduje się w pliku JSON, a następnie należy skonfigurować pięć uczestniczących modułach IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="9ad5c-225">Brak przykładowy plik JSON w repozytorium o nazwie **bramy\_sample.json** czy służy jako punkt początkowy do tworzenia pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="9ad5c-226">Ten plik jest **przykłady/ble_gateway/src** folderu w lokalnej kopii repozytorium IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="9ad5c-227">W poniższych sekcjach opisano, jak edytować ten plik konfiguracji przykładowej cz i założono, że repozytorium krawędzi IoT jest **/home/pi/iot-edge /** folderu na Twoje malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="9ad5c-228">Jeśli repozytorium jest w innym miejscu, należy odpowiednio zmień ścieżki.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="9ad5c-229">Konfiguracja rejestratora</span><span class="sxs-lookup"><span data-stu-id="9ad5c-229">Logger configuration</span></span>

<span data-ttu-id="9ad5c-230">Zakładając, że repozytorium bramy znajduje się w **/home/pi/iot-edge /** folderu, skonfigurować moduł rejestratora w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="9ad5c-231">Konfiguracja modułu cz</span><span class="sxs-lookup"><span data-stu-id="9ad5c-231">BLE module configuration</span></span>

<span data-ttu-id="9ad5c-232">Przykładowa konfiguracja urządzenia cz zakłada urządzenia Texas Instruments w Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="9ad5c-233">Standardowe urządzenie cz może działać jako GATT peryferyjnych powinny działać, ale może być konieczne zaktualizowanie identyfikatorów charakterystyczny GATT i danych.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="9ad5c-234">Dodaj adres MAC urządzenia Sensor tag:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="9ad5c-235">Jeśli nie używasz urządzeń Sensor tag, zapoznaj się z dokumentacją urządzenia cz określić, czy konieczne jest aktualizacja cecha GATT identyfikatorów i wartości danych.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="9ad5c-236">Moduł Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9ad5c-236">IoT Hub module</span></span>

<span data-ttu-id="9ad5c-237">Dodaj nazwę Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="9ad5c-238">Wartość sufiksu jest zwykle **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="9ad5c-239">Konfiguracja modułu mapowania tożsamości</span><span class="sxs-lookup"><span data-stu-id="9ad5c-239">Identity mapping module configuration</span></span>

<span data-ttu-id="9ad5c-240">Dodaj adres MAC urządzenia Sensor tag identyfikator urządzenia i klucz **SensorTag_01** urządzenie dodane do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="9ad5c-241">Konfiguracja modułu cz drukarki</span><span class="sxs-lookup"><span data-stu-id="9ad5c-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="9ad5c-242">Konfiguracja modułu BLEC2D</span><span class="sxs-lookup"><span data-stu-id="9ad5c-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="9ad5c-243">Konfiguracja routingu</span><span class="sxs-lookup"><span data-stu-id="9ad5c-243">Routing Configuration</span></span>

<span data-ttu-id="9ad5c-244">Następująca konfiguracja zapewnia następujące routingu między modułami krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="9ad5c-245">**Rejestratora** modułu odbiera i rejestruje wszystkie komunikaty.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="9ad5c-246">**Sensor tag** modułu wysyła komunikaty do obu **mapowania** i **drukarki cz** modułów.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="9ad5c-247">**Mapowania** moduł powoduje wysyłanie komunikatów do **Centrum IoTHub** moduł ma zostać wysłany w do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="9ad5c-248">**Centrum IoTHub** moduł powoduje wysyłanie komunikatów z powrotem do **mapowania** modułu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="9ad5c-249">**Mapowania** moduł powoduje wysyłanie komunikatów do **BLEC2D** modułu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="9ad5c-250">**BLEC2D** moduł powoduje wysyłanie komunikatów z powrotem do **Sensor Tag** modułu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="9ad5c-251">Aby uruchomić przykład, Przekaż ścieżka do pliku konfiguracji JSON jako parametr **cz\_bramy** binarnego.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="9ad5c-252">Polecenie zakłada używasz **gateway_sample.json** pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="9ad5c-253">Wykonaj to polecenie z **krawędzi iot** folderu na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="9ad5c-254">Konieczne może być naciśnięcie przycisku małych na urządzeniu Sensor tag, aby był wykrywalny przed uruchomieniem próbki.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="9ad5c-255">Po uruchomieniu próbki, można użyć [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) narzędzia do monitorowania wiadomości brama brzegowa IoT przekazuje z urządzeń Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="9ad5c-256">Na przykład za pomocą Eksploratora Centrum iothub można monitorować wiadomości urządzenia do chmury przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="9ad5c-257">Wysyłanie komunikatów z chmury do urządzeń</span><span class="sxs-lookup"><span data-stu-id="9ad5c-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="9ad5c-258">Moduł cz obsługuje również wysyłanie poleceń z Centrum IoT na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="9ad5c-259">Można użyć [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) narzędzia do wysyłania wiadomości JSON, które moduł bramy cz przekazuje do urządzenia cz.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="9ad5c-260">Jeśli korzystasz z urządzenia Texas Instruments w Sensor tag, można włączyć red LED, zielony LED lub Brzęczyk przez wysyłanie poleceń z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="9ad5c-261">Przed wysłaniem poleceń z Centrum IoT należy najpierw wysłać następujące dwa komunikaty JSON w kolejności.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="9ad5c-262">Następnie możesz wysłać do dowolnego z poleceń, aby włączyć świateł lub Brzęczyk.</span><span class="sxs-lookup"><span data-stu-id="9ad5c-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="9ad5c-263">Resetuj wszystkie LED i brzęczyka (wyłączone):</span><span class="sxs-lookup"><span data-stu-id="9ad5c-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="9ad5c-264">Skonfiguruj we/wy jako "remote":</span><span class="sxs-lookup"><span data-stu-id="9ad5c-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="9ad5c-265">Teraz możesz wysłać dowolne z poniższych poleceń, aby włączyć świateł lub Brzęczyk na urządzeniu Sensor tag:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="9ad5c-266">Włącz LED czerwony:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="9ad5c-267">Włącz LED zielony:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="9ad5c-268">Włącz brzęczyka:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="9ad5c-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ad5c-269">Next Steps</span></span>

<span data-ttu-id="9ad5c-270">Jeśli chcesz uzyskać większą wiedzę krawędzi IoT i wypróbować niektóre przykłady kodu, odwiedź następujące samouczki deweloperów i zasoby:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="9ad5c-271">[Krawędź IoT Azure][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="9ad5c-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="9ad5c-272">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="9ad5c-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9ad5c-273">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="9ad5c-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
