---
title: "aaaIoT zestaw deweloperski toocloud — Połącz AZ3166 zestaw deweloperski IoT tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz toosend danych toohello chmury Azure platforma AZ3166 zestaw deweloperski IoT tooAzure Centrum IoT na jej w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="53a0a-103">Połącz tooAzure AZ3166 zestaw deweloperski IoT Centrum IoT w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="53a0a-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="53a0a-104">Witaj [zestaw deweloperski IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) mogą być używane toodevelop i prototypu rozwiązań Internetu rzeczy (IoT) na wykorzystaniu usług Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="53a0a-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="53a0a-105">Obejmuje on Arduino tablicy zgodny z zaawansowanych urządzeń peryferyjnych i czujników, pakiet tablicy open source i rosnącym [katalogu projektów](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="53a0a-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="53a0a-106">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="53a0a-106">What you do</span></span>
<span data-ttu-id="53a0a-107">Połącz [zestaw deweloperski](https://microsoft.github.io/azure-iot-developer-kit/) Centrum Azure IoT tooan utworzyć zbieranie hello temperatury i wilgotności dane z czujników, a następnie wysłać hello danych tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="53a0a-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="53a0a-108">Nie masz jeszcze zestaw deweloperski?</span><span class="sxs-lookup"><span data-stu-id="53a0a-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="53a0a-109">Uzyskać nowy [tutaj](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="53a0a-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="53a0a-110">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="53a0a-110">What you learn</span></span>

* <span data-ttu-id="53a0a-111">Jak tooconnect dostępu tooWireless zestaw deweloperski IoT punktu i przygotowywanie środowiska projektowego.</span><span class="sxs-lookup"><span data-stu-id="53a0a-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="53a0a-112">Jak toocreate Centrum IoT i zarejestrować urządzenie zestaw deweloperski IoT MXChip.</span><span class="sxs-lookup"><span data-stu-id="53a0a-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="53a0a-113">Jak toocollect dane czujników, uruchamiając na zestaw deweloperski IoT MXChip przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53a0a-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="53a0a-114">Jak toosend hello Centrum IoT tooyour danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="53a0a-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="53a0a-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="53a0a-115">What you need</span></span>

* <span data-ttu-id="53a0a-116">Zestaw deweloperski IoT MXChip tablicy za pomocą kabla USB micro.</span><span class="sxs-lookup"><span data-stu-id="53a0a-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="53a0a-117">Pobierz teraz</span><span class="sxs-lookup"><span data-stu-id="53a0a-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="53a0a-118">Komputer z systemem Windows 10 lub macOS 10.10 +</span><span class="sxs-lookup"><span data-stu-id="53a0a-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="53a0a-119">Aktywną subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="53a0a-119">An active Azure subscription</span></span>
  * <span data-ttu-id="53a0a-120">Aktywuj [bezpłatne 30-dniowej wersji próbnej konto Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="53a0a-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="53a0a-121">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="53a0a-121">Prepare your hardware</span></span>

<span data-ttu-id="53a0a-122">Podłączanie hello sprzętu tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="53a0a-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="53a0a-123">Sprzęt niezbędny</span><span class="sxs-lookup"><span data-stu-id="53a0a-123">Hardware you need</span></span>

* <span data-ttu-id="53a0a-124">Zestaw deweloperski tablicy</span><span class="sxs-lookup"><span data-stu-id="53a0a-124">DevKit board</span></span>
* <span data-ttu-id="53a0a-125">Micro kabla USB</span><span class="sxs-lookup"><span data-stu-id="53a0a-125">Micro USB cable</span></span>

![Pobieranie uruchomiona — sprzęt](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="53a0a-127">Podłącz komputer tooyour zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="53a0a-128">Połączenie USB zakończenia tooyour PC</span><span class="sxs-lookup"><span data-stu-id="53a0a-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="53a0a-129">Połączenie Micro USB zakończenia toohello zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="53a0a-130">zielony Hello LED dalej toopower potwierdza połączenia</span><span class="sxs-lookup"><span data-stu-id="53a0a-130">hello green LED next toopower confirms connection</span></span>

![pobieranie rozpoczęto — połączenia](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="53a0a-132">Konfigurowanie sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="53a0a-132">Configure WiFi</span></span>

<span data-ttu-id="53a0a-133">Projektami IoT jest zależne od łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="53a0a-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="53a0a-134">Użyj hello następujące instrukcje tooconfigure hello zestaw deweloperski tooconnect tooWiFi.</span><span class="sxs-lookup"><span data-stu-id="53a0a-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="53a0a-135">Tryb region</span><span class="sxs-lookup"><span data-stu-id="53a0a-135">Enter AP Mode</span></span>

<span data-ttu-id="53a0a-136">Przytrzymaj naciśnięty przycisk B, a następnie wypychania i zwolnij przycisk reset hello, a następnie przycisk B. Twoje zestaw deweloperski przejdzie trybu region konfigurowania sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="53a0a-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="53a0a-137">ekran Hello spowoduje wyświetlenie hello usługi ustawić Identifier(SSID) z hello zestaw deweloperski, a także adres IP portalu hello konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="53a0a-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![wprowadzenie — uruchomiona — sieci Wi-Fi region](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="53a0a-139">Połącz region tooDevKit</span><span class="sxs-lookup"><span data-stu-id="53a0a-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="53a0a-140">Teraz Użyj innej sieci Wi-Fi włączone urządzenia (komputera lub telefonu komórkowego) tooconnect toohello SSID zestaw deweloperski (wyróżnione na zrzucie ekranu hello powyżej), pozostaw puste hasło hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![pobieranie pracy — identyfikator ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="53a0a-142">Konfigurowanie sieci Wi-Fi dla zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="53a0a-143">Otwórz hello adres IP wyświetlany na ekranie zestaw deweloperski hello na komputerze lub przeglądarki telefonu komórkowego, wybierz sieć Wi-Fi hello interesujące tooconnect zestaw deweloperski hello do, a następnie wpisz hasło hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="53a0a-144">Kliknij przycisk **Connect** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="53a0a-144">Click **Connect** toocomplete:</span></span>

![pobieranie rozpoczęto — sieci Wi-Fi portalu](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="53a0a-146">Po pomyślnym hello połączenia, hello zestaw deweloperski zostanie ponownie uruchomiony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="53a0a-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="53a0a-147">Jeśli zakończyło się pomyślnie, zostanie wyświetlony hello sieci Wi-Fi nazwy i adresu IP na ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="53a0a-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![pobieranie rozpoczęto — sieci Wi-Fi ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="53a0a-149">adres IP Hello wyświetlane w fotografii hello może nie odpowiadać IP rzeczywistego hello przypisane i wyświetlany na ekranie zestaw deweloperski hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="53a0a-150">Jest to normalne jako wykorzystanie sieci Wi-Fi DHCP toodynamically przypisywanie adresów IP.</span><span class="sxs-lookup"><span data-stu-id="53a0a-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="53a0a-151">Po skonfigurowaniu sieci Wi-Fi, poświadczenia zostaną utrwalone hello urządzenia dla tego połączenia, nawet wtedy, gdy odłączony.</span><span class="sxs-lookup"><span data-stu-id="53a0a-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="53a0a-152">Na przykład, jeśli skonfigurowany hello zestaw deweloperski dla sieci Wi-Fi w domu, a następnie trwało hello zestaw deweloperski toohello office, konieczne będzie tryb tooreconfigure region (poczynając od kroku **Wprowadź tryb region**) hello tooconnect office tooyour zestaw deweloperski sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="53a0a-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="53a0a-153">Uruchom przy użyciu zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-153">Start using DevKit</span></span>

<span data-ttu-id="53a0a-154">Hello domyślnej aplikacji uruchomionej na zestaw deweloperski sprawdzi hello najnowsza wersja oprogramowania układowego hello i wyświetli niektóre dane diagnostyki czujników za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="53a0a-155">Uaktualnij toohello najnowszego oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="53a0a-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="53a0a-156">Zostanie wyświetlony monit na ekranie powitania zarówno hello wersja bieżących i najnowszego oprogramowania układowego, jeśli jest konieczne uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="53a0a-157">Postępuj zgodnie z [uaktualnienie oprogramowania układowego](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) przewodnik tooupgrade go.</span><span class="sxs-lookup"><span data-stu-id="53a0a-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![wprowadzenie — uruchomiona-oprogramowania układowego](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="53a0a-159">To jest jednorazowe wysiłku, po rozpoczęciu tworzenia na powitania zestaw deweloperski i przekazać aplikację, mają najnowszego oprogramowania układowego hello pochodzą z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53a0a-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="53a0a-160">Testowanie różnych czujników</span><span class="sxs-lookup"><span data-stu-id="53a0a-160">Test various sensors</span></span>

<span data-ttu-id="53a0a-161">Naciśnij przycisk B tootest czujników, Kontynuuj naciskanie i zwalnianie toocycle przycisk hello B za pośrednictwem każdej czujnika.</span><span class="sxs-lookup"><span data-stu-id="53a0a-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![wprowadzenie — uruchomiona czujników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="53a0a-163">Przygotuj Środowisko deweloperskie</span><span class="sxs-lookup"><span data-stu-id="53a0a-163">Prepare development environment</span></span>

<span data-ttu-id="53a0a-164">Teraz nadszedł czas tooset się środowisko projektowe hello: narzędzia i pakiety toobuild ogłuszania aplikacji IoT.</span><span class="sxs-lookup"><span data-stu-id="53a0a-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="53a0a-165">Można wybrać systemu Windows lub wersji macOS zgodnie z tooyour systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="53a0a-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="53a0a-166">Windows</span><span class="sxs-lookup"><span data-stu-id="53a0a-166">Windows</span></span>

<span data-ttu-id="53a0a-167">Firma Microsoft zachęca możesz toouse hello instalacji pakietu tooprepare hello Środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="53a0a-168">Jeśli wystąpią problemy, można wykonać hello [ręczne](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget go wykonać.</span><span class="sxs-lookup"><span data-stu-id="53a0a-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="53a0a-169">Pobierz najnowszy pakiet</span><span class="sxs-lookup"><span data-stu-id="53a0a-169">Download latest package</span></span>

<span data-ttu-id="53a0a-170">Witaj `.zip` należy pobrać plik zawiera wszystkie niezbędne narzędzia i wymagane przez zestaw deweloperski programowanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="53a0a-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="53a0a-171">Pobieranie</span><span class="sxs-lookup"><span data-stu-id="53a0a-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="53a0a-172">Witaj `.zip` plik zawiera hello następujące narzędzia i pakietów.</span><span class="sxs-lookup"><span data-stu-id="53a0a-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="53a0a-173">Jeśli masz już pewne składniki zainstalowane, hello skrypt wykrywania i Pomiń nich.</span><span class="sxs-lookup"><span data-stu-id="53a0a-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="53a0a-174">Node.js i Yarn: program obsługi dla skryptu instalacyjnego hello i automatycznych zadań</span><span class="sxs-lookup"><span data-stu-id="53a0a-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="53a0a-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -wieloplatformowych środowiska wiersza polecenia do zarządzania zasobami Azure hello MSI zawiera zależnej Python i pip.</span><span class="sxs-lookup"><span data-stu-id="53a0a-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="53a0a-176">[Visual Studio Code](https://code.visualstudio.com/): Edytor niewielki kod dla rozwoju zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="53a0a-177">[Rozszerzenia programu Visual Studio Code Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): włącza Arduino Programowanie w kodzie VS</span><span class="sxs-lookup"><span data-stu-id="53a0a-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="53a0a-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello rozszerzenie Arduino zależy od tego narzędzia</span><span class="sxs-lookup"><span data-stu-id="53a0a-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="53a0a-179">Pakiet tablicy zestaw deweloperski: Narzędzie łańcuchy, biblioteki i projektów dla hello zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="53a0a-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="53a0a-180">Narzędzie ST łącza: Niezbędne narzędzia i sterowniki</span><span class="sxs-lookup"><span data-stu-id="53a0a-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="53a0a-181">Uruchom skrypt instalacji</span><span class="sxs-lookup"><span data-stu-id="53a0a-181">Run installation script</span></span>

<span data-ttu-id="53a0a-182">W Eksploratorze plików systemu Windows, Znajdź hello `.zip` i wyodrębnij go, Znajdź `install.cmd`, kliknij prawym przyciskiem myszy i wybierz **"Uruchom jako administrator"** toostart.</span><span class="sxs-lookup"><span data-stu-id="53a0a-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![wprowadzenie — uruchomiona — Uruchom — administrator](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="53a0a-184">Podczas instalacji zostanie wyświetlony postęp hello każdego narzędzia lub pakietu.</span><span class="sxs-lookup"><span data-stu-id="53a0a-184">During installation, you will see hello progress of each tool or package.</span></span>

![pobieranie rozpoczęto Zainstaluj](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="53a0a-186">Potwierdź tooinstall sterowniki</span><span class="sxs-lookup"><span data-stu-id="53a0a-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="53a0a-187">Hello kodzie VS rozszerzenia Arduino polega na powitania Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="53a0a-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="53a0a-188">Jeśli jest to hello instalujesz hello Arduino IDE po raz pierwszy, będzie tooinstall zostanie wyświetlony monit o odpowiednich sterowników:</span><span class="sxs-lookup"><span data-stu-id="53a0a-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![pobieranie rozpoczęto sterowników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="53a0a-190">Powinien upłynąć instalacji toofinish około 10 minut w zależności od szybkości Internet.</span><span class="sxs-lookup"><span data-stu-id="53a0a-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="53a0a-191">Po zakończeniu instalacji hello Visual Studio Code i Arduino IDE skróty powinny być widoczne na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="53a0a-192">Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy.</span><span class="sxs-lookup"><span data-stu-id="53a0a-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="53a0a-193">toosolve Arduino IDE jego kod VS zamknięcia uruchom raz i kodzie VS należy zlokalizować ścieżki Arduino IDE poprawnie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="53a0a-194">System macOS (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="53a0a-194">macOS (Preview)</span></span>

<span data-ttu-id="53a0a-195">Wykonaj środowisko projektowe tooprepare te kroki na macOS.</span><span class="sxs-lookup"><span data-stu-id="53a0a-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="53a0a-196">Instalowanie interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="53a0a-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="53a0a-197">Wykonaj hello [oficjalnym przewodniku](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="53a0a-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="53a0a-198">Zainstaluj 2.0 interfejsu wiersza polecenia platformy Azure z jednym `curl` polecenia:</span><span class="sxs-lookup"><span data-stu-id="53a0a-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="53a0a-199">I ponownie uruchom polecenia powłoki dla efektu tootake zmiany:</span><span class="sxs-lookup"><span data-stu-id="53a0a-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="53a0a-200">Zainstaluj Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="53a0a-200">Install Arduino IDE</span></span>

<span data-ttu-id="53a0a-201">Hello rozszerzenia programu Visual Studio Code Arduino polega na powitania Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="53a0a-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="53a0a-202">Pobierz i zainstaluj hello [Arduino IDE dla macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="53a0a-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="53a0a-203">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53a0a-203">Install Visual Studio Code</span></span>

<span data-ttu-id="53a0a-204">Pobierz i zainstaluj [Visual Studio Code dla macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="53a0a-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="53a0a-205">Są to narzędzie do projektowania głównej hello do tworzenia aplikacji IoT zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="53a0a-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="53a0a-206">Pobierz najnowszy pakiet</span><span class="sxs-lookup"><span data-stu-id="53a0a-206">Download latest package</span></span>

1. <span data-ttu-id="53a0a-207">Zainstaluj środowisko Node.js.</span><span class="sxs-lookup"><span data-stu-id="53a0a-207">Install Node.js.</span></span> <span data-ttu-id="53a0a-208">Można użyć Menedżera pakietów macOS popularnych [Homebrew](https://brew.sh/) lub [wstępnie skompilowany Instalator](https://nodejs.org/en/download/) tooinstall go.</span><span class="sxs-lookup"><span data-stu-id="53a0a-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="53a0a-209">Pobierz `.zip` plik zawierający skrypty zadań niezbędnych zestaw deweloperski w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="53a0a-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="53a0a-210">Pobieranie</span><span class="sxs-lookup"><span data-stu-id="53a0a-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="53a0a-211">Zlokalizuj hello `.zip` i wyodrębnij go.</span><span class="sxs-lookup"><span data-stu-id="53a0a-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="53a0a-212">Następnie uruchom **Terminal** hello uruchom następujące polecenia tooconfigure i aplikacji:</span><span class="sxs-lookup"><span data-stu-id="53a0a-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="53a0a-213">Przenieść folder użytkownika macOS tooyour wyodrębnionego folderu:</span><span class="sxs-lookup"><span data-stu-id="53a0a-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="53a0a-214">Zainstaluj `npm` pakiety:</span><span class="sxs-lookup"><span data-stu-id="53a0a-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="53a0a-215">Zainstaluj rozszerzenie kodzie VS dla Arduino</span><span class="sxs-lookup"><span data-stu-id="53a0a-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="53a0a-216">Visual Studio Code pozwala tooinstall Marketplace rozszerzenia bezpośrednio w narzędziu hello, po prostu kliknij ikonę rozszerzenia hello w okienku po lewej stronie menu hello i wyszukiwać `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="53a0a-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![Instalacja rozszerzenia](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="53a0a-218">Zainstaluj zestaw deweloperski pakiet tablicy</span><span class="sxs-lookup"><span data-stu-id="53a0a-218">Install DevKit board package</span></span>

<span data-ttu-id="53a0a-219">Konieczne będzie tablicy zestaw deweloperski hello tooadd przy użyciu hello Menedżera tablicy w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="53a0a-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="53a0a-220">Użyj `Cmd+Shift+P` tooinvoke polecenia palety i typ **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Menedżer tablicy**.</span><span class="sxs-lookup"><span data-stu-id="53a0a-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="53a0a-221">Kliknij przycisk **dodatkowych adresów URL** na powitania prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="53a0a-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="53a0a-222">![Instalacja dodatkowych-adresów URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="53a0a-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="53a0a-223">W hello `settings.json` plików, Dodaj wiersz na dole hello `USER SETTINGS` okienko i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="53a0a-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![json instalacji — ustawienia](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="53a0a-225">Teraz hello Menedżera tablicy Wyszukaj "az3166" i zainstaluj najnowszą wersję hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="53a0a-226">![az3166 instalacji](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="53a0a-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="53a0a-227">Masz teraz wszystkie niezbędne narzędzia hello i pakiety zainstalowane dla macOS.</span><span class="sxs-lookup"><span data-stu-id="53a0a-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="53a0a-228">Otwórz projekt folderu</span><span class="sxs-lookup"><span data-stu-id="53a0a-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="53a0a-229">Uruchom program VS Code</span><span class="sxs-lookup"><span data-stu-id="53a0a-229">Launch VS Code</span></span>

<span data-ttu-id="53a0a-230">Upewnij się, że nie jest połączona z zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="53a0a-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="53a0a-231">Najpierw uruchom kodzie VS i podłącz komputer tooyour zestaw deweloperski hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="53a0a-232">Kod VS będzie automatycznie ją znaleźć i wyskakujące strona wprowadzenia:</span><span class="sxs-lookup"><span data-stu-id="53a0a-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="53a0a-234">Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy.</span><span class="sxs-lookup"><span data-stu-id="53a0a-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="53a0a-235">toosolve Arduino IDE jego kod VS zamknięcia, uruchom ponownie i kodzie VS należy zlokalizować ścieżki Arduino IDE poprawnie.</span><span class="sxs-lookup"><span data-stu-id="53a0a-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="53a0a-236">Otwórz folder Arduino przykłady</span><span class="sxs-lookup"><span data-stu-id="53a0a-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="53a0a-237">Przełącz zbyt**"Przykłady Arduino"** karcie kolejno zbyt`Examples for MXCHIP AZ3166 > AzureIoT` i wybierz polecenie `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="53a0a-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Mini solution — przykłady](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="53a0a-239">W przypadku tooclose hello okienku tooreload go, użyj `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke polecenia palety i typ **Arduino** toofind i wybierz **Arduino: przykłady**.</span><span class="sxs-lookup"><span data-stu-id="53a0a-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="53a0a-240">Udostępnianie usług platformy Azure</span><span class="sxs-lookup"><span data-stu-id="53a0a-240">Provision Azure services</span></span>

<span data-ttu-id="53a0a-241">W oknie rozwiązania hello Uruchom zadania za pomocą `Ctrl+P` (macOS: `Cmd+P`), wpisując "task chmury przepisu":</span><span class="sxs-lookup"><span data-stu-id="53a0a-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="53a0a-242">W hello kodzie VS terminali interakcyjne wiersza polecenia poprowadzi Cię przez hello inicjowania obsługi administracyjnej wymaganych usług Azure:</span><span class="sxs-lookup"><span data-stu-id="53a0a-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![Mini-solution-chmury provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="53a0a-244">Tworzenie i przekazywanie Arduino szkicu</span><span class="sxs-lookup"><span data-stu-id="53a0a-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="53a0a-245">Zainstalować wymaganej biblioteki</span><span class="sxs-lookup"><span data-stu-id="53a0a-245">Install required library</span></span>

1. <span data-ttu-id="53a0a-246">Naciśnij klawisz `F1` lub `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke polecenia palety i typ **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Library Manager**.</span><span class="sxs-lookup"><span data-stu-id="53a0a-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="53a0a-247">Wyszukaj `ArduinoJson` biblioteki i kliknij przycisk **instalacji**</span><span class="sxs-lookup"><span data-stu-id="53a0a-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="53a0a-248">Tworzenie i przekazywanie hello urządzenia kodu</span><span class="sxs-lookup"><span data-stu-id="53a0a-248">Build and upload hello device code</span></span>

<span data-ttu-id="53a0a-249">Użyj `Ctrl+P` (macOS: `Cmd+P`) toorun "zadań urządzenia — przekazywanie".</span><span class="sxs-lookup"><span data-stu-id="53a0a-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="53a0a-250">Witaj terminali wyświetli monit o możesz tooenter trybu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="53a0a-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="53a0a-251">toodo tak, naciśnij i przytrzymaj przycisk A, a następnie przycisk reset hello wypychania i wersji.</span><span class="sxs-lookup"><span data-stu-id="53a0a-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="53a0a-252">ekran Hello wyświetli "Konfiguracja".</span><span class="sxs-lookup"><span data-stu-id="53a0a-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="53a0a-253">Jest to ciąg połączenia hello tooset pobiera z kroku "świadczenia chmury zadania".</span><span class="sxs-lookup"><span data-stu-id="53a0a-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="53a0a-254">Następnie zostanie ona rozpoczęta Weryfikowanie i przekazywanie szkicu Arduino hello:</span><span class="sxs-lookup"><span data-stu-id="53a0a-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![Mini-solution urządzenia wysyłania](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="53a0a-256">Hello zestaw deweloperski spowoduje ponowny rozruch i uruchamianie hello kodu.</span><span class="sxs-lookup"><span data-stu-id="53a0a-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="53a0a-257">Projekt testowy hello</span><span class="sxs-lookup"><span data-stu-id="53a0a-257">Test hello project</span></span>

<span data-ttu-id="53a0a-258">W kodzie VS kliknij hello zasilania plug ikonę na pasku tooopen hello Serial Monitor stanu hello.</span><span class="sxs-lookup"><span data-stu-id="53a0a-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="53a0a-259">Witaj Przykładowa aplikacja działa prawidłowo po wyświetleniu hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="53a0a-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="53a0a-260">Witaj Serial monitorów hello tych samych informacji dotyczących zawartości hello na powitania zrzucie ekranu pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="53a0a-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="53a0a-261">Witaj LED na zestaw deweloperski IoT MXChip jest migający.</span><span class="sxs-lookup"><span data-stu-id="53a0a-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Ostateczne dane wyjściowe w kodzie VS](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="53a0a-263">Problemy i opinie</span><span class="sxs-lookup"><span data-stu-id="53a0a-263">Problems and feedback</span></span>

<span data-ttu-id="53a0a-264">Można znaleźć [— często zadawane pytania](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) w przypadku wystąpienia problemów lub dotrzeć toous z kanałów hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="53a0a-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53a0a-265">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53a0a-265">Next steps</span></span>

<span data-ttu-id="53a0a-266">Pomyślnie nawiązano tooyour zestaw deweloperski IoT MXChip Centrum IoT i wysłane hello przechwycone Centrum IoT tooyour danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="53a0a-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="53a0a-267">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="53a0a-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="53a0a-268">Zarządzanie przesyłaniem komunikatów między chmurą a urządzeniem za pomocą narzędzia iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="53a0a-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="53a0a-269">Zapisz komunikaty Centrum IoT tooAzure magazynu danych</span><span class="sxs-lookup"><span data-stu-id="53a0a-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="53a0a-270">Użyj usługi Power BI toovisualize czujnika w czasie rzeczywistym danych z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="53a0a-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="53a0a-271">Korzystanie z Centrum IoT Azure danych czujnika w czasie rzeczywistym toovisualize aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="53a0a-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="53a0a-272">Prognoza pogody przy użyciu danych czujnika hello z Centrum IoT w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="53a0a-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="53a0a-273">Zarządzanie urządzeniami za pomocą narzędzia iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="53a0a-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="53a0a-274">Zdalne monitorowanie i powiadomienia w usłudze Logic Apps</span><span class="sxs-lookup"><span data-stu-id="53a0a-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)