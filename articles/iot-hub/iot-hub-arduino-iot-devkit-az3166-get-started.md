---
title: "Zestaw deweloperski IoT do chmury - nawiązać Centrum IoT Azure IoT zestaw deweloperski AZ3166 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować i AZ3166 zestaw deweloperski IoT nawiązać połączenia z Centrum IoT Azure go do przesyłania danych do platformy w chmurze platformy Azure, w tym samouczku."
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
ms.openlocfilehash: 122fac584ac5b954ef7b33a3121bee2c502ebc63
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="a5aa5-103">AZ3166 zestaw deweloperski IoT nawiązać połączenia z Centrum IoT Azure w chmurze</span><span class="sxs-lookup"><span data-stu-id="a5aa5-103">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="a5aa5-104">[Zestaw deweloperski IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) służy do opracowywania i rozwiązań Internetu rzeczy (IoT) prototypu na wykorzystaniu usług Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-104">The [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used to develop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="a5aa5-105">Obejmuje on Arduino tablicy zgodny z zaawansowanych urządzeń peryferyjnych i czujników, pakiet tablicy open source i rosnącym [katalogu projektów](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="a5aa5-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a5aa5-106">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="a5aa5-106">What you do</span></span>
<span data-ttu-id="a5aa5-107">Połącz [zestaw deweloperski](https://microsoft.github.io/azure-iot-developer-kit/) w Centrum Azure IoT utworzony zbierania danych temperatury i wilgotności, z czujników i wysyłania danych do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors and send the data to IoT hub.</span></span>

<span data-ttu-id="a5aa5-108">Nie masz jeszcze zestaw deweloperski?</span><span class="sxs-lookup"><span data-stu-id="a5aa5-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="a5aa5-109">Uzyskać nowy [tutaj](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="a5aa5-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a5aa5-110">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a5aa5-110">What you learn</span></span>

* <span data-ttu-id="a5aa5-111">Jak zestaw deweloperski IoT nawiązać połączenia z punktem dostępu bezprzewodowego i przygotowywanie środowiska projektowego.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-111">How to connect IoT DevKit to Wireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="a5aa5-112">Jak utworzyć Centrum IoT i zarejestrować urządzenie zestaw deweloperski IoT MXChip.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-112">How to create an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="a5aa5-113">Jak zbierać dane czujników, uruchamiając na zestaw deweloperski IoT MXChip przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-113">How to collect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="a5aa5-114">Jak wysyłać dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-114">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a5aa5-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="a5aa5-115">What you need</span></span>

* <span data-ttu-id="a5aa5-116">Zestaw deweloperski IoT MXChip tablicy za pomocą kabla USB micro.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="a5aa5-117">Pobierz teraz</span><span class="sxs-lookup"><span data-stu-id="a5aa5-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="a5aa5-118">Komputer z systemem Windows 10 lub macOS 10.10 +</span><span class="sxs-lookup"><span data-stu-id="a5aa5-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="a5aa5-119">Aktywną subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a5aa5-119">An active Azure subscription</span></span>
  * <span data-ttu-id="a5aa5-120">Aktywuj [bezpłatne 30-dniowej wersji próbnej konto Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="a5aa5-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="a5aa5-121">Przygotowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="a5aa5-121">Prepare your hardware</span></span>

<span data-ttu-id="a5aa5-122">Podłączanie sprzętu do komputera.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-122">Hook up the hardware to your computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="a5aa5-123">Sprzęt niezbędny</span><span class="sxs-lookup"><span data-stu-id="a5aa5-123">Hardware you need</span></span>

* <span data-ttu-id="a5aa5-124">Zestaw deweloperski tablicy</span><span class="sxs-lookup"><span data-stu-id="a5aa5-124">DevKit board</span></span>
* <span data-ttu-id="a5aa5-125">Micro kabla USB</span><span class="sxs-lookup"><span data-stu-id="a5aa5-125">Micro USB cable</span></span>

![Pobieranie uruchomiona — sprzęt](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a><span data-ttu-id="a5aa5-127">Łączenie się z komputerem zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-127">Connect DevKit to your computer</span></span>

1. <span data-ttu-id="a5aa5-128">Połącz koniec USB do komputera</span><span class="sxs-lookup"><span data-stu-id="a5aa5-128">Connect USB end to your PC</span></span>
2. <span data-ttu-id="a5aa5-129">Połącz koniec Micro USB do zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-129">Connect Micro USB end to the DevKit</span></span>
3. <span data-ttu-id="a5aa5-130">Zielona LED obok zasilania potwierdza połączenia</span><span class="sxs-lookup"><span data-stu-id="a5aa5-130">The green LED next to power confirms connection</span></span>

![pobieranie rozpoczęto — połączenia](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="a5aa5-132">Konfigurowanie sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a5aa5-132">Configure WiFi</span></span>

<span data-ttu-id="a5aa5-133">Projektami IoT jest zależne od łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="a5aa5-134">Użyj poniższych instrukcji, aby skonfigurować zestaw deweloperski, aby nawiązać połączenie sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-134">Use the following instructions to configure the DevKit to connect to WiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="a5aa5-135">Tryb region</span><span class="sxs-lookup"><span data-stu-id="a5aa5-135">Enter AP Mode</span></span>

<span data-ttu-id="a5aa5-136">Przytrzymaj naciśnięty przycisk B, wypychania i zwolnij przycisk reset, a następnie zwolnij przycisk B. Twoje zestaw deweloperski przejdzie trybu region konfigurowania sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-136">Hold down button B, then push and release the reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="a5aa5-137">Na ekranie będą wyświetlani Identifier(SSID) ustawić usługi zestaw deweloperski, a także adres IP portalu w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-137">The screen will display the Service Set Identifier(SSID) of the DevKit as well as the configuration portal IP address:</span></span>

![wprowadzenie — uruchomiona — sieci Wi-Fi region](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a><span data-ttu-id="a5aa5-139">Nawiązać zestaw deweloperski region</span><span class="sxs-lookup"><span data-stu-id="a5aa5-139">Connect to DevKit AP</span></span>

<span data-ttu-id="a5aa5-140">Teraz Użyj innego urządzenia włączone sieci Wi-Fi (komputera lub telefonu komórkowego), aby nawiązać połączenie SSID zestaw deweloperski (wyróżnione na zrzucie ekranu powyżej), pozostaw puste hasło.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-140">Now, use another WiFi enabled device (PC or mobile phone) to connect to the DevKit SSID (highlighted in the screenshot above), leave the password empty.</span></span>

![pobieranie pracy — identyfikator ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="a5aa5-142">Konfigurowanie sieci Wi-Fi dla zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="a5aa5-143">Otwórz adres IP wyświetlany na ekranie zestaw deweloperski w przeglądarce PC lub telefonu komórkowego, wybierz sieć Wi-Fi, ma zestaw deweloperski, aby nawiązać połączenie, a następnie wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-143">Open the IP address shown on the DevKit screen on your PC or mobile phone browser, select the WiFi network you want the DevKit to connect to, then type the password.</span></span> <span data-ttu-id="a5aa5-144">Kliknij przycisk **Connect** do ukończenia:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-144">Click **Connect** to complete:</span></span>

![pobieranie rozpoczęto — sieci Wi-Fi portalu](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="a5aa5-146">Po pomyślnym połączenia, zestaw deweloperski zostanie ponownie uruchomiony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-146">Once the connection succeeds, the DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="a5aa5-147">Jeśli zakończyło się pomyślnie, na ekranie zostanie wyświetlony sieci Wi-Fi nazwy i adresu IP:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-147">If succeeded, you will see the WiFi name and IP address on the screen:</span></span>

![pobieranie rozpoczęto — sieci Wi-Fi ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="a5aa5-149">Adres IP wyświetlany w zdjęcia może nie odpowiadać rzeczywista IP przypisany i wyświetlane na ekranie zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-149">The IP address displayed in the photo may not match the actual IP assigned and displayed on the DevKit screen.</span></span> <span data-ttu-id="a5aa5-150">Jest to normalne, jak dynamiczne przypisywanie adresów IP sieci Wi-Fi korzysta z protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-150">This is normal as WiFi uses DHCP to dynamically assign IPs.</span></span>

<span data-ttu-id="a5aa5-151">Po skonfigurowaniu sieci Wi-Fi, poświadczenia zostaną utrwalone na urządzeniu dla tego połączenia, nawet jeśli odłączony.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-151">After WiFi is configured, your credentials will be persisted on the device for that connection, even if unplugged.</span></span> <span data-ttu-id="a5aa5-152">Na przykład jeśli skonfigurowany zestaw deweloperski dla sieci Wi-Fi w domu, a następnie trwało zestaw deweloperski urzędowi, należy ponownie skonfigurować tryb region (poczynając od kroku **Wprowadź tryb region**) do nawiązania połączenia z biurem sieci Wi-Fi zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-152">For example, if you configured the DevKit for WiFi in your home and then took the DevKit to the office, you will need to reconfigure AP mode (starting at step **Enter AP Mode**) to connect the DevKit to your office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="a5aa5-153">Uruchom przy użyciu zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-153">Start using DevKit</span></span>

<span data-ttu-id="a5aa5-154">Domyślna aplikacja uruchomiona na zestaw deweloperski sprawdzi najnowszej wersji oprogramowania układowego i wyświetli niektóre dane diagnostyki czujników za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-154">The default app running on DevKit will check the latest version of the firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-to-the-latest-firmware"></a><span data-ttu-id="a5aa5-155">Uaktualnij do najnowszego oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="a5aa5-155">Upgrade to the latest firmware</span></span>

<span data-ttu-id="a5aa5-156">Zostanie wyświetlony monit na ekranie wymagane zarówno bieżąca, najnowsza wersja oprogramowania układowego w przypadku uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-156">You will be prompted on the screen both the current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="a5aa5-157">Postępuj zgodnie z [uaktualnienie oprogramowania układowego](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) przewodnik ją uaktualnić.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide to upgrade it.</span></span>

![wprowadzenie — uruchomiona-oprogramowania układowego](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="a5aa5-159">To jest jednorazowe wysiłku, po rozpoczęciu tworzenia na zestaw deweloperski i przekazać aplikację, mają najnowszego oprogramowania układowego pochodzą z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-159">This is a one-time effort, once you start developing on the DevKit and upload your app, you will have the latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="a5aa5-160">Testowanie różnych czujników</span><span class="sxs-lookup"><span data-stu-id="a5aa5-160">Test various sensors</span></span>

<span data-ttu-id="a5aa5-161">Naciśnij przycisk B do testowania czujników, nadal naciśnięcie klawisza i zwolnieniem przycisku B, aby przechodzić kolejno przez każdy czujnika.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-161">Press button B to test sensors, continue pressing and releasing the B button to cycle through each sensor.</span></span>

![wprowadzenie — uruchomiona czujników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="a5aa5-163">Przygotuj Środowisko deweloperskie</span><span class="sxs-lookup"><span data-stu-id="a5aa5-163">Prepare development environment</span></span>

<span data-ttu-id="a5aa5-164">Teraz nadszedł czas, aby skonfigurować środowisko projektowe: narzędzia i pakietów do tworzenia niezwykłych aplikacji IoT.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-164">Now it's time to set up the development environment: tools and packages for you to build stunning IoT applications.</span></span> <span data-ttu-id="a5aa5-165">Można wybrać systemu Windows lub wersji macOS zgodnie z systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-165">You can choose Windows or macOS version according to your operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="a5aa5-166">Windows</span><span class="sxs-lookup"><span data-stu-id="a5aa5-166">Windows</span></span>

<span data-ttu-id="a5aa5-167">Firma Microsoft zachęca do użycia pakietu instalacyjnego, aby przygotować Środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-167">We encourage you to use the installation package to prepare the development environment.</span></span> <span data-ttu-id="a5aa5-168">Jeśli wystąpią problemy, można wykonać [ręczne](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) do wykonywania pracy.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-168">If you encounter any issues, you can follow the [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) to get it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="a5aa5-169">Pobierz najnowszy pakiet</span><span class="sxs-lookup"><span data-stu-id="a5aa5-169">Download latest package</span></span>

<span data-ttu-id="a5aa5-170">`.zip` Należy pobrać plik zawiera wszystkie niezbędne narzędzia i wymagane przez zestaw deweloperski programowanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-170">The `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="a5aa5-171">Pobieranie</span><span class="sxs-lookup"><span data-stu-id="a5aa5-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="a5aa5-172">`.zip` Plik zawiera następujące narzędzia i pakietów.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-172">The `.zip` file contains the following tools and packages.</span></span> <span data-ttu-id="a5aa5-173">Jeśli masz już pewne składniki zainstalowane, skrypt wykryje i Pomiń nich.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-173">If you already have some components installed, the script will detect and skip them.</span></span>
> * <span data-ttu-id="a5aa5-174">Node.js i Yarn: program obsługi dla skryptu Instalatora i automatycznych zadań</span><span class="sxs-lookup"><span data-stu-id="a5aa5-174">Node.js and Yarn: Runtime for the setup script and automated tasks</span></span>
> * <span data-ttu-id="a5aa5-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -środowiska wiersza polecenia i platform do zarządzania zasobami platformy Azure, MSI zawiera zależnej Python i pip.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, the MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="a5aa5-176">[Visual Studio Code](https://code.visualstudio.com/): Edytor niewielki kod dla rozwoju zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="a5aa5-177">[Rozszerzenia programu Visual Studio Code Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): włącza Arduino Programowanie w kodzie VS</span><span class="sxs-lookup"><span data-stu-id="a5aa5-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="a5aa5-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): rozszerzenie Arduino zależy od tego narzędzia</span><span class="sxs-lookup"><span data-stu-id="a5aa5-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): The extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="a5aa5-179">Pakiet tablicy zestaw deweloperski: Narzędzie łańcuchy, biblioteki i projektów dla zestaw deweloperski</span><span class="sxs-lookup"><span data-stu-id="a5aa5-179">DevKit Board Package: Tool chains, libraries and projects for the DevKit</span></span>
> * <span data-ttu-id="a5aa5-180">Narzędzie ST łącza: Niezbędne narzędzia i sterowniki</span><span class="sxs-lookup"><span data-stu-id="a5aa5-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="a5aa5-181">Uruchom skrypt instalacji</span><span class="sxs-lookup"><span data-stu-id="a5aa5-181">Run installation script</span></span>

<span data-ttu-id="a5aa5-182">W Eksploratorze plików systemu Windows, Znajdź `.zip` i wyodrębnij go, Znajdź `install.cmd`, kliknij prawym przyciskiem myszy i wybierz **"Uruchom jako administrator"** można uruchomić.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-182">In Windows File Explorer, locate the `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** to start.</span></span>

![wprowadzenie — uruchomiona — Uruchom — administrator](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="a5aa5-184">Podczas instalacji będzie wyświetlany jest postęp każdego narzędzia lub pakietu.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-184">During installation, you will see the progress of each tool or package.</span></span>

![pobieranie rozpoczęto Zainstaluj](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a><span data-ttu-id="a5aa5-186">Upewnij się, aby zainstalować sterowniki</span><span class="sxs-lookup"><span data-stu-id="a5aa5-186">Confirm to install drivers</span></span>

<span data-ttu-id="a5aa5-187">Kod VS rozszerzenia Arduino zależy od Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-187">The VS Code for Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="a5aa5-188">Jeśli instalujesz Arduino IDE po raz pierwszy, wyświetli się monit o zainstalowanie odpowiednich sterowników:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-188">If this is the first time you are installing the Arduino IDE, you will be prompted to install relevant drivers:</span></span>

![pobieranie rozpoczęto sterowników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="a5aa5-190">Zakończenie instalacji, w zależności od szybkości Internet powinno zająć około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-190">It should take around 10 minutes to finish installation depending on your Internet speed.</span></span> <span data-ttu-id="a5aa5-191">Po zakończeniu instalacji programu Visual Studio Code i Arduino IDE skróty powinny być widoczne na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-191">Once the installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="a5aa5-192">Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="a5aa5-193">Aby go rozwiązać, zamknij kodzie VS, uruchom raz Arduino IDE i kodzie VS należy zlokalizować Arduino IDE ścieżkę poprawnie.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-193">To solve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="a5aa5-194">System macOS (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a5aa5-194">macOS (Preview)</span></span>

<span data-ttu-id="a5aa5-195">Wykonaj następujące kroki, aby przygotować środowisko projektowe na macOS.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-195">Follow these steps to prepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="a5aa5-196">Instalowanie interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a5aa5-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="a5aa5-197">Postępuj zgodnie z [oficjalnym przewodniku](https://docs.microsoft.com//cli/azure/install-azure-cli) instalowania 2.0 interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-197">Follow the [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) to install Azure CLI 2.0:</span></span>

<span data-ttu-id="a5aa5-198">Zainstaluj 2.0 interfejsu wiersza polecenia platformy Azure z jednym `curl` polecenia:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="a5aa5-199">I ponownie uruchom z powłoki poleceń, aby zmiany zaczęły obowiązywać:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-199">And restart your command shell for changes to take effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="a5aa5-200">Zainstaluj Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="a5aa5-200">Install Arduino IDE</span></span>

<span data-ttu-id="a5aa5-201">Rozszerzenia programu Visual Studio Code Arduino zależy od Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-201">The Visual Studio Code Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="a5aa5-202">Pobierz i zainstaluj [Arduino IDE dla macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="a5aa5-202">Download and install the [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="a5aa5-203">Zainstaluj kod programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5aa5-203">Install Visual Studio Code</span></span>

<span data-ttu-id="a5aa5-204">Pobierz i zainstaluj [Visual Studio Code dla macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a5aa5-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="a5aa5-205">Są to narzędzie tworzenia podstawowego do tworzenia aplikacji IoT zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-205">This will be the primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="a5aa5-206">Pobierz najnowszy pakiet</span><span class="sxs-lookup"><span data-stu-id="a5aa5-206">Download latest package</span></span>

1. <span data-ttu-id="a5aa5-207">Zainstaluj środowisko Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-207">Install Node.js.</span></span> <span data-ttu-id="a5aa5-208">Można użyć Menedżera pakietów macOS popularnych [Homebrew](https://brew.sh/) lub [wstępnie skompilowany Instalator](https://nodejs.org/en/download/) go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) to install it.</span></span>

2. <span data-ttu-id="a5aa5-209">Pobierz `.zip` plik zawierający skrypty zadań niezbędnych zestaw deweloperski w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="a5aa5-210">Pobieranie</span><span class="sxs-lookup"><span data-stu-id="a5aa5-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="a5aa5-211">Zlokalizuj `.zip` i wyodrębnij go.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-211">Locate the `.zip` and extract it.</span></span> <span data-ttu-id="a5aa5-212">Następnie uruchom **Terminal** aplikacji i uruchom następujące polecenia, aby skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-212">Then launch **Terminal** app and run the following commands to configure:</span></span>

   <span data-ttu-id="a5aa5-213">Przenieś wyodrębnionego folderu do folderu macOS użytkownika:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-213">Move extracted folder to your macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="a5aa5-214">Zainstaluj `npm` pakiety:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="a5aa5-215">Zainstaluj rozszerzenie kodzie VS dla Arduino</span><span class="sxs-lookup"><span data-stu-id="a5aa5-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="a5aa5-216">Visual Studio Code umożliwia instalowanie rozszerzeń Marketplace bezpośrednio w narzędziu, wystarczy kliknąć ikonę rozszerzenia w okienku po lewej stronie menu i wyszukiwać `Arduino` do zainstalowania:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-216">Visual Studio Code allows you to install Marketplace extensions directly in the tool, simply click the extensions icon in the left menu pane and then search `Arduino` to install:</span></span>

![Instalacja rozszerzenia](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="a5aa5-218">Zainstaluj zestaw deweloperski pakiet tablicy</span><span class="sxs-lookup"><span data-stu-id="a5aa5-218">Install DevKit board package</span></span>

<span data-ttu-id="a5aa5-219">Należy dodać zestaw deweloperski tablicy za pomocą Menedżera tablicy w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-219">You will need to add the DevKit board using the Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="a5aa5-220">Użyj `Cmd+Shift+P` do wywołania palety polecenia i wpisz **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Menedżer tablicy**.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-220">Use `Cmd+Shift+P` to invoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="a5aa5-221">Kliknij przycisk **dodatkowych adresów URL** w prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-221">Click **'Additional URLs'** at the bottom right.</span></span>
   <span data-ttu-id="a5aa5-222">![Instalacja dodatkowych-adresów URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="a5aa5-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="a5aa5-223">W `settings.json` plików, dodawanie wiersza w dolnej części `USER SETTINGS` okienko i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-223">In the `settings.json` file, add a line at the bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![json instalacji — ustawienia](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="a5aa5-225">Teraz w Menedżerze tablicy wyszukiwanie "az3166" i zainstaluj najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-225">Now in the Board Manager search for 'az3166' and install the latest version.</span></span>
   <span data-ttu-id="a5aa5-226">![az3166 instalacji](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="a5aa5-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="a5aa5-227">Masz teraz wszystkie niezbędne narzędzia i pakiety zainstalowane dla macOS.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-227">You now have all the necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="a5aa5-228">Otwórz projekt folderu</span><span class="sxs-lookup"><span data-stu-id="a5aa5-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="a5aa5-229">Uruchom program VS Code</span><span class="sxs-lookup"><span data-stu-id="a5aa5-229">Launch VS Code</span></span>

<span data-ttu-id="a5aa5-230">Upewnij się, że nie jest połączona z zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="a5aa5-231">Najpierw uruchom kodzie VS i łączenie się z komputerem zestaw deweloperski.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-231">Launch VS Code first and connect the DevKit to your computer.</span></span> <span data-ttu-id="a5aa5-232">Kod VS będzie automatycznie ją znaleźć i wyskakujące strona wprowadzenia:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="a5aa5-234">Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="a5aa5-235">Aby go rozwiązać, zamknij kodzie VS, uruchom ponownie Arduino IDE i kodzie VS należy zlokalizować Arduino IDE ścieżkę poprawnie.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-235">To solve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="a5aa5-236">Otwórz folder Arduino przykłady</span><span class="sxs-lookup"><span data-stu-id="a5aa5-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="a5aa5-237">Przełącz się do **"Przykłady Arduino"** karcie, przejdź do `Examples for MXCHIP AZ3166 > AzureIoT` i wybierz polecenie `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-237">Switch to **'Arduino Examples'** tab, navigate to `Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Mini solution — przykłady](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="a5aa5-239">W przypadku zamknąć okienko, aby załadować ponownie, należy użyć `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) do wywołania palety polecenia i wpisz **Arduino** Aby znaleźć i wybrać **Arduino: przykłady**.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-239">If you happen to close the pane, to reload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** to find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="a5aa5-240">Udostępnianie usług platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a5aa5-240">Provision Azure services</span></span>

<span data-ttu-id="a5aa5-241">W oknie rozwiązania, uruchom zadanie za pośrednictwem `Ctrl+P` (macOS: `Cmd+P`), wpisując "task chmury przepisu":</span><span class="sxs-lookup"><span data-stu-id="a5aa5-241">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="a5aa5-242">W kodzie VS terminali interakcyjne wiersza polecenia poprowadzi Cię przez Inicjowanie obsługi administracyjnej wymaganych usług Azure:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-242">In the VS Code terminal, an interactive command line will guide you through provisioning the required Azure services:</span></span>

![Mini-solution-chmury provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="a5aa5-244">Tworzenie i przekazywanie Arduino szkicu</span><span class="sxs-lookup"><span data-stu-id="a5aa5-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="a5aa5-245">Zainstalować wymaganej biblioteki</span><span class="sxs-lookup"><span data-stu-id="a5aa5-245">Install required library</span></span>

1. <span data-ttu-id="a5aa5-246">Naciśnij klawisz `F1` lub `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) do wywołania palety polecenia i wpisz **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Library Manager**.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="a5aa5-247">Wyszukaj `ArduinoJson` biblioteki i kliknij przycisk **instalacji**</span><span class="sxs-lookup"><span data-stu-id="a5aa5-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-the-device-code"></a><span data-ttu-id="a5aa5-248">Tworzenie i przekazywanie kodu urządzenia</span><span class="sxs-lookup"><span data-stu-id="a5aa5-248">Build and upload the device code</span></span>

<span data-ttu-id="a5aa5-249">Użyj `Ctrl+P` (macOS: `Cmd+P`) do uruchamiania "zadań przekazywania urządzenie".</span><span class="sxs-lookup"><span data-stu-id="a5aa5-249">Use `Ctrl+P` (macOS: `Cmd+P`) to run 'task device-upload'.</span></span> <span data-ttu-id="a5aa5-250">Terminal wyświetli monit o wprowadzenie trybu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-250">The terminal will prompt you to enter configuration mode.</span></span> <span data-ttu-id="a5aa5-251">Aby to zrobić, przytrzymaj naciśnięty przycisk A, a następnie wypychania, a następnie zwolnij przycisk resetowania.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-251">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="a5aa5-252">Na ekranie będą wyświetlani "Konfiguracja".</span><span class="sxs-lookup"><span data-stu-id="a5aa5-252">The screen will display 'Configuration'.</span></span> <span data-ttu-id="a5aa5-253">Jest to można ustawić parametry połączenia, które pobiera z kroku "zadań chmurze provision".</span><span class="sxs-lookup"><span data-stu-id="a5aa5-253">This is to set the connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="a5aa5-254">Następnie zostanie ona rozpoczęta Weryfikowanie i przekazywanie szkicu Arduino:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-254">Then it will start verifying and uploading the Arduino sketch:</span></span>

![Mini-solution urządzenia wysyłania](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="a5aa5-256">Zestaw deweloperski spowoduje ponowny rozruch i uruchamianie kodu.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-256">The DevKit will reboot and start running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="a5aa5-257">Projekt testowy</span><span class="sxs-lookup"><span data-stu-id="a5aa5-257">Test the project</span></span>

<span data-ttu-id="a5aa5-258">W kodzie VS kliknij ikonę plug zasilania na pasku stanu, aby otworzyć Serial Monitor.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-258">In VS Code, click the power plug icon on the status bar to open the Serial Monitor.</span></span>

<span data-ttu-id="a5aa5-259">Przykładowa aplikacja działa prawidłowo, gdy pojawi się następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-259">The sample application is running successfully when you see the following results:</span></span>

* <span data-ttu-id="a5aa5-260">Serial Monitor wyświetla te same informacje jak zawartość na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-260">The Serial Monitor displays the same information as the content in the screenshot below.</span></span>
* <span data-ttu-id="a5aa5-261">LED na zestaw deweloperski IoT MXChip jest migający.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-261">The LED on MXChip IoT DevKit is blinking.</span></span>

![Ostateczne dane wyjściowe w kodzie VS](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="a5aa5-263">Problemy i opinie</span><span class="sxs-lookup"><span data-stu-id="a5aa5-263">Problems and feedback</span></span>

<span data-ttu-id="a5aa5-264">Można znaleźć [— często zadawane pytania](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) w przypadku wystąpienia problemów lub dotrzeć do nas z kanałów poniżej.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out to us from the channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5aa5-265">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5aa5-265">Next steps</span></span>

<span data-ttu-id="a5aa5-266">Pomyślnie połączony zestaw deweloperski IoT MXChip Centrum IoT i wysyłane dane czujników przechwyconych do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a5aa5-266">You have successfully connected an MXChip IoT DevKit to your IoT Hub, and sent the captured sensor data to your IoT hub.</span></span>

<span data-ttu-id="a5aa5-267">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="a5aa5-267">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="a5aa5-268">Zarządzanie przesyłaniem komunikatów między chmurą a urządzeniem za pomocą narzędzia iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a5aa5-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="a5aa5-269">Zapisywanie komunikatów usługi IoT Hub w magazynie danych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a5aa5-269">Save IoT Hub messages to Azure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="a5aa5-270">Użyj usługi Power BI do wizualizacji danych czujnika w czasie rzeczywistym z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a5aa5-270">Use Power BI to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="a5aa5-271">Korzystanie z aplikacji sieci Web platformy Azure do wizualizacji danych czujnika w czasie rzeczywistym z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a5aa5-271">Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="a5aa5-272">Pogody prognozy przy użyciu danych czujnika z Centrum IoT w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a5aa5-272">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="a5aa5-273">Zarządzanie urządzeniami za pomocą narzędzia iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a5aa5-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="a5aa5-274">Zdalne monitorowanie i powiadomienia w usłudze Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a5aa5-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)