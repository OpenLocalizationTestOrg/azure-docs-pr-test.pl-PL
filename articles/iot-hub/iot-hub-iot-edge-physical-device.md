---
title: "aaaUse fizyczne urządzenia Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Jak toouse Texas Instruments w Sensor tag urządzenia toosend danych tooan Centrum IoT przez bramę krawędzi IoT uruchamianie na urządzeniu malina Pi 3. bramy Hello jest utworzony przy użyciu usługi Azure IoT krawędzi."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="33648-104">Użyj Azure IoT krawędź Pi malina tooIoT wiadomości urządzenia do chmury tooforward Centrum</span><span class="sxs-lookup"><span data-stu-id="33648-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="33648-105">W tym przewodniku hello [próbki niski energii Bluetooth] [ lnk-ble-samplecode] przedstawiono toouse [Azure IoT krawędzi] [ lnk-sdk] do:</span><span class="sxs-lookup"><span data-stu-id="33648-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="33648-106">Przekazuj tooIoT telemetrii urządzenia do chmury Centrum z urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="33648-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="33648-107">Polecenia trasy z urządzenia fizycznego tooa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="33648-108">Przewodnik składa się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="33648-108">This walkthrough covers:</span></span>

* <span data-ttu-id="33648-109">**Architektura**: ważne informacje architektury o hello Bluetooth niski energii próbki.</span><span class="sxs-lookup"><span data-stu-id="33648-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="33648-110">**Tworzenie i uruchamianie**: hello kroki wymagane toobuild i przykładowa hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="33648-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="33648-111">Architektura</span><span class="sxs-lookup"><span data-stu-id="33648-111">Architecture</span></span>

<span data-ttu-id="33648-112">wskazówki Hello pokazuje, jak toobuild i uruchom bramę brzegową IoT 3 Pi malina z systemem Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="33648-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="33648-113">Brama Hello jest utworzony przy użyciu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="33648-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="33648-114">Witaj w przykładzie użyto danych temperatury toocollect urządzenia Texas Instruments Sensor tag Bluetooth małej energii (cz).</span><span class="sxs-lookup"><span data-stu-id="33648-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="33648-115">Po uruchomieniu hello brama brzegowa IoT go:</span><span class="sxs-lookup"><span data-stu-id="33648-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="33648-116">Łączy tooa urządzeń Sensor tag przy użyciu hello energii małej Bluetooth (cz) protokołu.</span><span class="sxs-lookup"><span data-stu-id="33648-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="33648-117">Łączy tooIoT Centrum przy użyciu protokołu hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="33648-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="33648-118">Przekazuje dane telemetryczne z tooIoT urządzeń Sensor tag hello koncentratora.</span><span class="sxs-lookup"><span data-stu-id="33648-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="33648-119">Kieruje poleceń z urządzeń Sensor tag toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="33648-120">Brama Hello zawiera następujące moduły krawędzi IoT hello:</span><span class="sxs-lookup"><span data-stu-id="33648-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="33648-121">A *modułu cz* który interfejsy z cz urządzenia tooreceive temperatury danych z urządzenia hello i wysyłania poleceń toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="33648-122">A *modułu toodevice chmury cz* konwertujący JSON wiadomości wysyłane z Centrum IoT w instrukcji cz hello *modułu cz*.</span><span class="sxs-lookup"><span data-stu-id="33648-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="33648-123">A *modułu rejestratora* który rejestruje wszystkie bramy wiadomości tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="33648-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="33648-124">*Moduł mapowania tożsamości* który tłumaczy adresy MAC cz urządzenia i tożsamości urządzenia Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33648-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="33648-125">*Modułu Centrum IoT* który przekazuje Centrum IoT tooan danych telemetrycznych i odbiera polecenia urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="33648-126">A *cz drukarki moduł* interpretuje dane telemetryczne z hello cz urządzenia i drukowanie sformatowanych danych toohello konsoli tooenable Rozwiązywanie problemów i debugowania.</span><span class="sxs-lookup"><span data-stu-id="33648-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="33648-127">Jak dane przepływają przez bramę hello</span><span class="sxs-lookup"><span data-stu-id="33648-127">How data flows through hello gateway</span></span>

<span data-ttu-id="33648-128">powitania po diagram blokowy przedstawia potoku przepływu danych przekazywania telemetrii hello:</span><span class="sxs-lookup"><span data-stu-id="33648-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Potok bramy przekazywania telemetrii](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="33648-130">Hello kroki, które przyjmuje elementu telemetrii podróży z tooIoT urządzenia cz Centrum są:</span><span class="sxs-lookup"><span data-stu-id="33648-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="33648-131">urządzenie cz Hello generuje próbki temperatury i wysyła je przez moduł cz toohello Bluetooth hello bramy.</span><span class="sxs-lookup"><span data-stu-id="33648-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="33648-132">Moduł cz Hello odbiera próbki hello i publikuje ją brokera toohello wraz z hello adres MAC urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="33648-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="33648-133">Moduł mapowania tożsamości Hello przejmuje ten komunikat i używa wewnętrznej tabeli tootranslate hello adres MAC urządzenia hello do tożsamości urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="33648-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="33648-134">Centrum IoT urządzenia tożsamości składa się z Identyfikatorem urządzenia i klucz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="33648-135">Moduł mapowania tożsamości Hello publikuje nowy komunikat zawierający hello temperatury przykładowych danych, hello adres MAC urządzenia hello, identyfikator urządzenia hello i hello klucza urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="33648-136">Hello modułu Centrum IoT odbiera ten nowy komunikat (generowane przez moduł mapowania tożsamości hello) i publikuje ją tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="33648-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="33648-137">Moduł rejestratora Hello rejestruje wszystkie komunikaty z pliku lokalnego tooa hello brokera.</span><span class="sxs-lookup"><span data-stu-id="33648-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="33648-138">powitania po diagram blokowy przedstawia potoku przepływu danych hello urządzenia polecenie:</span><span class="sxs-lookup"><span data-stu-id="33648-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Urządzenia polecenie bramy potoku](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="33648-140">Centrum IoT modułu okresowo sonduje Hello hello Centrum IoT nowe wiadomości polecenia.</span><span class="sxs-lookup"><span data-stu-id="33648-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="33648-141">Hello modułu Centrum IoT odebrania nowego komunikatu polecenie powoduje ona publikowanie go toohello brokera.</span><span class="sxs-lookup"><span data-stu-id="33648-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="33648-142">Moduł mapowania tożsamości Hello przejmuje wiadomości powitania polecenia i używa wewnętrznej tabeli tootranslate hello adres MAC urządzenia tooa identyfikator urządzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="33648-143">Go następnie publikuje nowy komunikat zawierający adres MAC urządzenia docelowego hello hello w hello właściwości mapy wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="33648-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="33648-144">Witaj cz chmury do urządzenia moduł przejmuje ten komunikat i tłumaczy go na powitania prawidłowego cz instrukcji hello cz modułu.</span><span class="sxs-lookup"><span data-stu-id="33648-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="33648-145">Go następnie publikuje nowy komunikat.</span><span class="sxs-lookup"><span data-stu-id="33648-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="33648-146">Moduł cz Hello przejmuje ten komunikat i wykonuje instrukcję we/wy hello komunikując się z urządzeniem cz hello.</span><span class="sxs-lookup"><span data-stu-id="33648-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="33648-147">Moduł rejestratora Hello rejestruje wszystkie komunikaty z hello brokera tooa dysku pliku.</span><span class="sxs-lookup"><span data-stu-id="33648-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33648-148">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="33648-148">Prerequisites</span></span>

<span data-ttu-id="33648-149">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33648-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="33648-150">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="33648-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="33648-151">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="33648-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="33648-152">Należy klient SSH na Twojej tooenable komputerów możesz tooremotely dostępu hello wiersza polecenia na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="33648-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="33648-153">System Windows nie zawiera klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="33648-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="33648-154">Firma Microsoft zaleca używanie [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="33648-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="33648-155">Większość dystrybucje systemu Linux i Mac OS obejmują narzędzia wiersza polecenia SSH hello.</span><span class="sxs-lookup"><span data-stu-id="33648-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="33648-156">Aby uzyskać więcej informacji, zobacz [SSH za pomocą systemu Linux lub Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="33648-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="33648-157">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="33648-157">Prepare your hardware</span></span>

<span data-ttu-id="33648-158">Ten samouczek zakłada się, czy używasz [Texas Instruments w Sensor tag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) urządzenie podłączone tooa malina Pi 3 systemem Raspbian.</span><span class="sxs-lookup"><span data-stu-id="33648-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="33648-159">Zainstaluj Raspbian</span><span class="sxs-lookup"><span data-stu-id="33648-159">Install Raspbian</span></span>

<span data-ttu-id="33648-160">Możesz użyć dowolnej z hello następujące opcje tooinstall Raspbian na urządzeniu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33648-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="33648-161">tooinstall hello najnowszą wersję Raspbian, użyj hello [NOOBS] [ lnk-noobs] graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33648-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="33648-162">Ręcznie [Pobierz] [ lnk-raspbian] i zapisywać najnowsze obraz powitania karty SD tooan systemu operacyjnego Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="33648-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="33648-163">Zaloguj się i uzyskać dostęp hello terminali</span><span class="sxs-lookup"><span data-stu-id="33648-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="33648-164">Masz dwie opcje tooaccess terminali środowiska użytkownika Pi malina:</span><span class="sxs-lookup"><span data-stu-id="33648-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="33648-165">Jeśli klawiatura i monitorowanie połączonych tooyour Pi malina, możesz użyć hello Raspbian GUI tooaccess okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="33648-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="33648-166">Dostęp z wiersza polecenia hello na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="33648-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="33648-167">Okno terminalu w hello graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="33648-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="33648-168">username są Hello domyślne poświadczenia dla Raspbian **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="33648-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="33648-169">Na pasku zadań hello w hello graficznego interfejsu użytkownika, możesz uruchomić hello **Terminal** narzędzie za pomocą ikony hello, która wygląda jak monitora.</span><span class="sxs-lookup"><span data-stu-id="33648-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="33648-170">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="33648-170">Sign in with SSH</span></span>

<span data-ttu-id="33648-171">Można użyć SSH dla wiersza polecenia dostępu tooyour malina Pi.</span><span class="sxs-lookup"><span data-stu-id="33648-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="33648-172">Artykuł Hello [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób tooconfigure SSH na Twoje Pi malina i w jaki sposób tooconnect z [Windows] [ lnk-ssh-windows] lub [Systemu operacyjnego Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="33648-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="33648-173">Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="33648-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="33648-174">Zainstaluj BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="33648-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="33648-175">Moduły cz Hello komunikować toohello Bluetooth sprzętu za pośrednictwem hello BlueZ stosu.</span><span class="sxs-lookup"><span data-stu-id="33648-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="33648-176">Poprawnie wymagana wersja 5.37 BlueZ dla hello toowork modułów.</span><span class="sxs-lookup"><span data-stu-id="33648-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="33648-177">Tych instrukcji upewnij się, że jest zainstalowana prawidłowa wersja BlueZ hello.</span><span class="sxs-lookup"><span data-stu-id="33648-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="33648-178">Zatrzymaj hello bieżącego demon bluetooth:</span><span class="sxs-lookup"><span data-stu-id="33648-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="33648-179">Zainstaluj zależności BlueZ hello:</span><span class="sxs-lookup"><span data-stu-id="33648-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="33648-180">Pobierz kod źródłowy BlueZ hello z bluez.org:</span><span class="sxs-lookup"><span data-stu-id="33648-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="33648-181">Rozpakuj hello kodu źródłowego:</span><span class="sxs-lookup"><span data-stu-id="33648-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="33648-182">Zmień katalogi toohello nowo utworzony folder:</span><span class="sxs-lookup"><span data-stu-id="33648-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="33648-183">Skonfiguruj toobe kodu BlueZ hello wbudowane:</span><span class="sxs-lookup"><span data-stu-id="33648-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="33648-184">Tworzenie BlueZ:</span><span class="sxs-lookup"><span data-stu-id="33648-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="33648-185">Zainstaluj BlueZ po zakończeniu kompilowania:</span><span class="sxs-lookup"><span data-stu-id="33648-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="33648-186">Zmień konfigurację usługi systemd Bluetooth, wskazuje toohello Nowy demon bluetooth w pliku hello `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="33648-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="33648-187">Zastąp wiersza "ExecStart" hello hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="33648-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="33648-188">Włącz urządzeń Sensor tag toohello łączności z urządzenia malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="33648-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="33648-189">Przed uruchomionych hello próbki należy tooverify czy Twoje malina Pi 3 można połączyć toohello urządzeń Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="33648-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="33648-190">Upewnij się, hello `rfkill` zainstalowano narzędzie:</span><span class="sxs-lookup"><span data-stu-id="33648-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="33648-191">Odblokowany bluetooth na powitania malina Pi 3 i sprawdź, czy numer wersji hello **5.37**:</span><span class="sxs-lookup"><span data-stu-id="33648-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="33648-192">tooenter hello interakcyjne bluetooth powłoki, uruchom usługę bluetooth hello i wykonać hello **bluetoothctl** polecenia:</span><span class="sxs-lookup"><span data-stu-id="33648-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="33648-193">Wprowadź polecenie hello **włączania zasilania** toopower zapasowej hello bluetooth kontrolera.</span><span class="sxs-lookup"><span data-stu-id="33648-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="33648-194">polecenie Hello zwraca dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="33648-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="33648-195">W powłoce interakcyjne bluetooth hello, wprowadź polecenie hello **na skanowania** tooscan dla urządzenia bluetooth.</span><span class="sxs-lookup"><span data-stu-id="33648-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="33648-196">polecenie Hello zwraca dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="33648-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="33648-197">Urządzeń Sensor tag hello stał się wykrywalny przez naciśnięcie przycisku małych hello (powitalne powinien flash LED zielony).</span><span class="sxs-lookup"><span data-stu-id="33648-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="33648-198">Witaj malina Pi 3 powinien odnajdywanie urządzeń Sensor tag hello:</span><span class="sxs-lookup"><span data-stu-id="33648-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="33648-199">W tym przykładzie widać, że hello adres MAC hello Sensor tag urządzenie jest **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="33648-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="33648-200">Wyłącz skanowanie wprowadzając hello **skanowania poza** polecenia:</span><span class="sxs-lookup"><span data-stu-id="33648-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="33648-201">Podłącz urządzenie Sensor tag tooyour przy użyciu adresu MAC, wprowadzając **połączyć \<adres MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="33648-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="33648-202">następujące przykładowe dane wyjściowe Hello jest skracana dla jasności:</span><span class="sxs-lookup"><span data-stu-id="33648-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="33648-203">Możesz wyświetlić listę właściwości GATT hello urządzenia hello ponownie, używając hello **listę atrybutów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="33648-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="33648-204">Teraz możesz odłączyć od hello urządzenia przy użyciu hello **rozłączyć** polecenia, a następnie Zamknij z powłoki bluetooth hello przy użyciu hello **Zamknij** polecenia:</span><span class="sxs-lookup"><span data-stu-id="33648-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="33648-205">Możesz teraz gotowy toorun hello cz IoT krawędzi próbki na Twoje malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33648-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="33648-206">Uruchom hello cz krawędzi IoT próbki</span><span class="sxs-lookup"><span data-stu-id="33648-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="33648-207">toorun hello cz krawędzi IoT próbki, należy toocomplete trzech zadań:</span><span class="sxs-lookup"><span data-stu-id="33648-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="33648-208">Skonfiguruj dwa przykładowe urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="33648-209">Tworzenie IoT Edge na urządzeniu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33648-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="33648-210">Konfigurowania i uruchamiania przykładowych cz hello na urządzeniu malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33648-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="33648-211">W czasie hello zapisu krawędzi IoT obsługuje modułów cz tylko w bramy z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="33648-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="33648-212">Skonfiguruj dwa przykładowe urządzenia w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="33648-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="33648-213">[Tworzenie Centrum IoT] [ lnk-create-hub] w Twojej subskrypcji platformy Azure, potrzebna hello nazwa Twojej toocomplete Centrum tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="33648-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="33648-214">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="33648-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="33648-215">Dodaj urządzenia o nazwie **SensorTag_01** tooyour Centrum IoT i zanotuj jego identyfikator i urządzenia klucza.</span><span class="sxs-lookup"><span data-stu-id="33648-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="33648-216">Można użyć hello [explorer urządzenie lub Centrum iothub explorer] [ lnk-explorer-tools] narzędzi tooadd tym Centrum IoT toohello urządzeń utworzone w poprzednim kroku hello i tooretrieve jego klucza.</span><span class="sxs-lookup"><span data-stu-id="33648-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="33648-217">Podczas konfigurowania bramy hello mapowania urządzeń Sensor tag toohello tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="33648-218">Tworzenie Azure IoT krawędzi w Twojej malinowe Pi 3</span><span class="sxs-lookup"><span data-stu-id="33648-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="33648-219">Zainstaluj zależności Edge IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="33648-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="33648-220">Użyj następujących hello polecenia tooclone krawędzi IoT i wszystkie jego modułów podrzędnych tooyour katalogu macierzystego:</span><span class="sxs-lookup"><span data-stu-id="33648-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="33648-221">Jeśli masz pełną kopię hello krawędzi IoT repozytorium na Twoje malina Pi 3 można tworzyć za pomocą hello następujące polecenia z folderu hello, który zawiera hello zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="33648-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="33648-222">Konfigurowanie i uruchamianie przykładowych cz hello na Twoje malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="33648-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="33648-223">toobootstrap i wykonywania hello próbki, należy skonfigurować każdy moduł IoT krawędzi, który uczestniczy w hello bramy.</span><span class="sxs-lookup"><span data-stu-id="33648-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="33648-224">Tej konfiguracji znajduje się w pliku JSON, a następnie należy skonfigurować pięć uczestniczących modułach IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="33648-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="33648-225">Brak przykładowy plik JSON w repozytorium hello o nazwie **bramy\_sample.json** których można używać jako hello punkt początkowy dla tworzenia pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33648-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="33648-226">Ten plik jest hello **przykłady/ble_gateway/src** folderu w lokalnej kopii hello krawędzi IoT repozytorium.</span><span class="sxs-lookup"><span data-stu-id="33648-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="33648-227">Witaj poniższych sekcjach opisano sposób tooedit tej konfiguracji pliku dla przykładu cz hello i założono tego repozytorium krawędzi IoT hello znajduje się w hello **/home/pi/iot-edge /** folderu na Twoje malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33648-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="33648-228">Jeśli repozytorium hello znajduje się w innym miejscu, odpowiednio hello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="33648-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="33648-229">Konfiguracja rejestratora</span><span class="sxs-lookup"><span data-stu-id="33648-229">Logger configuration</span></span>

<span data-ttu-id="33648-230">Zakładając, że hello repozytorium bramy znajduje się w hello **/home/pi/iot-edge /** folderu, skonfigurować moduł rejestratora hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="33648-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="33648-231">Konfiguracja modułu cz</span><span class="sxs-lookup"><span data-stu-id="33648-231">BLE module configuration</span></span>

<span data-ttu-id="33648-232">Przykładowa konfiguracja Hello hello cz urządzenia zakłada urządzenia Texas Instruments w Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="33648-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="33648-233">Wszystkie standardowe cz urządzenie może działać jako GATT peryferyjnych powinny działać, ale może być konieczne tooupdate hello GATT cech identyfikatorów i danych.</span><span class="sxs-lookup"><span data-stu-id="33648-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="33648-234">Dodaj hello adres MAC urządzenia Sensor tag:</span><span class="sxs-lookup"><span data-stu-id="33648-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="33648-235">Jeśli nie używasz urządzeń Sensor tag, przejrzyj hello dokumentacji dla Twojej cz toodetermine urządzenia, czy potrzebujesz tooupdate hello GATT cech identyfikatorów i wartości danych.</span><span class="sxs-lookup"><span data-stu-id="33648-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="33648-236">Moduł Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="33648-236">IoT Hub module</span></span>

<span data-ttu-id="33648-237">Dodaj nazwę hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="33648-238">Wartość sufiksu Hello jest zwykle **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="33648-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="33648-239">Konfiguracja modułu mapowania tożsamości</span><span class="sxs-lookup"><span data-stu-id="33648-239">Identity mapping module configuration</span></span>

<span data-ttu-id="33648-240">Dodaj adres MAC hello Sensor tag urządzenia i identyfikator urządzenia hello i klucza hello **SensorTag_01** urządzenie dodane tooyour Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="33648-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="33648-241">Konfiguracja modułu cz drukarki</span><span class="sxs-lookup"><span data-stu-id="33648-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="33648-242">Konfiguracja modułu BLEC2D</span><span class="sxs-lookup"><span data-stu-id="33648-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="33648-243">Konfiguracja routingu</span><span class="sxs-lookup"><span data-stu-id="33648-243">Routing Configuration</span></span>

<span data-ttu-id="33648-244">Witaj następującej konfiguracji zapewnia następujące hello routingu między modułami krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="33648-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="33648-245">Witaj **rejestratora** modułu odbiera i rejestruje wszystkie komunikaty.</span><span class="sxs-lookup"><span data-stu-id="33648-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="33648-246">Witaj **Sensor tag** moduł powoduje wysyłanie wiadomości powitania tooboth **mapowania** i **drukarki cz** modułów.</span><span class="sxs-lookup"><span data-stu-id="33648-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="33648-247">Witaj **mapowania** moduł powoduje wysyłanie wiadomości toohello **Centrum IoTHub** toobe modułu przesłane tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="33648-248">Witaj **Centrum IoTHub** moduł powoduje wysyłanie wiadomości kopii toohello **mapowania** modułu.</span><span class="sxs-lookup"><span data-stu-id="33648-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="33648-249">Witaj **mapowania** moduł powoduje wysyłanie wiadomości toohello **BLEC2D** modułu.</span><span class="sxs-lookup"><span data-stu-id="33648-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="33648-250">Witaj **BLEC2D** moduł powoduje wysyłanie wiadomości kopii toohello **Sensor Tag** modułu.</span><span class="sxs-lookup"><span data-stu-id="33648-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="33648-251">Przykładowe hello toorun, przebieg hello ścieżki toohello plik JSON konfiguracji jako toohello parametru **cz\_bramy** binarnego.</span><span class="sxs-lookup"><span data-stu-id="33648-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="33648-252">Witaj poniższego polecenia założono używasz hello **gateway_sample.json** pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33648-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="33648-253">Wykonaj to polecenie z hello **krawędzi iot** folderu na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="33648-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="33648-254">Może być konieczne toopress hello małych znajdującego się na toomake urządzeń Sensor tag hello wykrywalny go przed uruchomieniem hello próbki.</span><span class="sxs-lookup"><span data-stu-id="33648-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="33648-255">Po uruchomieniu hello przykładowe, można użyć hello [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) narzędzie toomonitor hello wiadomości powitania brama brzegowa IoT przekazuje z urządzeń Sensor tag hello.</span><span class="sxs-lookup"><span data-stu-id="33648-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="33648-256">Na przykład za pomocą Eksploratora Centrum iothub można monitorować za pomocą następującego polecenia hello wiadomości urządzenia do chmury:</span><span class="sxs-lookup"><span data-stu-id="33648-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="33648-257">Wysyłanie komunikatów z chmury do urządzeń</span><span class="sxs-lookup"><span data-stu-id="33648-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="33648-258">Moduł cz Hello obsługuje również wysyłanie poleceń z Centrum IoT toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="33648-259">Można użyć hello [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) wiadomości JSON toosend narzędzie module bramy cz hello przekazuje toohello cz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="33648-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="33648-260">Jeśli korzystasz z urządzenia Texas Instruments w Sensor tag hello, można włączyć LED hello czerwony, zielony LED lub Brzęczyk przez wysyłanie poleceń z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="33648-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="33648-261">Przed wysłaniem poleceń z Centrum IoT należy najpierw wysłać hello następujące dwa komunikaty JSON w kolejności.</span><span class="sxs-lookup"><span data-stu-id="33648-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="33648-262">Następnie możesz wysłać dowolne tooturn polecenia hello na powitania świateł lub Brzęczyk.</span><span class="sxs-lookup"><span data-stu-id="33648-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="33648-263">Resetuj wszystkie LED i brzęczyk hello (wyłączone):</span><span class="sxs-lookup"><span data-stu-id="33648-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="33648-264">Skonfiguruj we/wy jako "remote":</span><span class="sxs-lookup"><span data-stu-id="33648-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="33648-265">Teraz możesz wysłać dowolne powitania po tooturn polecenia świateł hello lub Brzęczyk na urządzeniu Sensor tag hello:</span><span class="sxs-lookup"><span data-stu-id="33648-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="33648-266">Włącz LED hello czerwony:</span><span class="sxs-lookup"><span data-stu-id="33648-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="33648-267">Włącz LED hello zielony:</span><span class="sxs-lookup"><span data-stu-id="33648-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="33648-268">Włącz Brzęczyk hello:</span><span class="sxs-lookup"><span data-stu-id="33648-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="33648-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33648-269">Next Steps</span></span>

<span data-ttu-id="33648-270">Toogain większą wiedzę krawędzi IoT i wypróbować niektóre przykłady kodu, odwiedź stronę hello następujące samouczki deweloperów i zasoby:</span><span class="sxs-lookup"><span data-stu-id="33648-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="33648-271">[Krawędź IoT Azure][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="33648-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="33648-272">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="33648-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="33648-273">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="33648-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
