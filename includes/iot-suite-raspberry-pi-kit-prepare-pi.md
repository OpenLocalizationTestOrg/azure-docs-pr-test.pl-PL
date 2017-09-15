## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="f7c05-101">Przygotowanie Twojego malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="f7c05-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="f7c05-102">Zainstaluj Raspbian</span><span class="sxs-lookup"><span data-stu-id="f7c05-102">Install Raspbian</span></span>

<span data-ttu-id="f7c05-103">Jeśli jest to w przypadku korzystania z Pi malina po raz pierwszy, musisz zainstalować Raspbian systemu operacyjnego za pomocą NOOBS na kartę SD. zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="f7c05-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="f7c05-104">[Malina Pi oprogramowania przewodnik] [ lnk-install-raspbian] opisuje sposób instalowania systemu operacyjnego na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f7c05-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="f7c05-105">W tym samouczku założono, że na Twoje Pi malina zainstalowano Raspbian systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f7c05-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c05-106">Karta SD objęte [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] ma już zainstalowany NOOBS.</span><span class="sxs-lookup"><span data-stu-id="f7c05-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="f7c05-107">Możesz rozruch Pi malina z tej karty i wybrać opcję instalacji systemu operacyjnego Raspbian.</span><span class="sxs-lookup"><span data-stu-id="f7c05-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="f7c05-108">Konfigurowanie sprzętu</span><span class="sxs-lookup"><span data-stu-id="f7c05-108">Set up the hardware</span></span>

<span data-ttu-id="f7c05-109">Czujnik BME280 zawarte w samouczku [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] do generowania danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="f7c05-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="f7c05-110">Zastosowano LED, aby wskazać, kiedy Pi malina przetwarza wywołania metody, z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7c05-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="f7c05-111">Składniki na tablicy chleb są:</span><span class="sxs-lookup"><span data-stu-id="f7c05-111">The components on the bread board are:</span></span>

- <span data-ttu-id="f7c05-112">Czerwony LED</span><span class="sxs-lookup"><span data-stu-id="f7c05-112">Red LED</span></span>
- <span data-ttu-id="f7c05-113">Ohm — 220 rezystor (czerwony, czerwony, brązowy)</span><span class="sxs-lookup"><span data-stu-id="f7c05-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="f7c05-114">Czujnik BME280</span><span class="sxs-lookup"><span data-stu-id="f7c05-114">BME280 sensor</span></span>

<span data-ttu-id="f7c05-115">Na poniższym diagramie przedstawiono sposób podłączania sprzętu:</span><span class="sxs-lookup"><span data-stu-id="f7c05-115">The following diagram shows how to connect your hardware:</span></span>

![Ustawienia sprzętu pi malina][img-connection-diagram]

<span data-ttu-id="f7c05-117">Poniższa tabela zawiera podsumowanie połączeń z Pi malina do składników na breadboard:</span><span class="sxs-lookup"><span data-stu-id="f7c05-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="f7c05-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f7c05-118">Raspberry Pi</span></span>            | <span data-ttu-id="f7c05-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="f7c05-119">Breadboard</span></span>             |<span data-ttu-id="f7c05-120">Kolor</span><span class="sxs-lookup"><span data-stu-id="f7c05-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="f7c05-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="f7c05-121">GND (Pin 14)</span></span>            | <span data-ttu-id="f7c05-122">Numer pin - kolejnych LED (18A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="f7c05-123">Fioletowy</span><span class="sxs-lookup"><span data-stu-id="f7c05-123">Purple</span></span>          |
| <span data-ttu-id="f7c05-124">GPCLK0 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="f7c05-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="f7c05-125">Rezystor (25A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-125">Resistor (25A)</span></span>         | <span data-ttu-id="f7c05-126">Orange</span><span class="sxs-lookup"><span data-stu-id="f7c05-126">Orange</span></span>          |
| <span data-ttu-id="f7c05-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="f7c05-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="f7c05-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-128">CS (39A)</span></span>               | <span data-ttu-id="f7c05-129">Niebieski</span><span class="sxs-lookup"><span data-stu-id="f7c05-129">Blue</span></span>          |
| <span data-ttu-id="f7c05-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="f7c05-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="f7c05-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-131">SCK (36A)</span></span>              | <span data-ttu-id="f7c05-132">Żółty</span><span class="sxs-lookup"><span data-stu-id="f7c05-132">Yellow</span></span>        |
| <span data-ttu-id="f7c05-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="f7c05-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="f7c05-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-134">SDO (37A)</span></span>              | <span data-ttu-id="f7c05-135">Biały</span><span class="sxs-lookup"><span data-stu-id="f7c05-135">White</span></span>         |
| <span data-ttu-id="f7c05-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="f7c05-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="f7c05-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-137">SDI (38A)</span></span>              | <span data-ttu-id="f7c05-138">Zielony</span><span class="sxs-lookup"><span data-stu-id="f7c05-138">Green</span></span>         |
| <span data-ttu-id="f7c05-139">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="f7c05-139">GND (Pin 6)</span></span>             | <span data-ttu-id="f7c05-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-140">GND (35A)</span></span>              | <span data-ttu-id="f7c05-141">Czarny</span><span class="sxs-lookup"><span data-stu-id="f7c05-141">Black</span></span>         |
| <span data-ttu-id="f7c05-142">3.3 V (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="f7c05-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="f7c05-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="f7c05-143">3Vo (34A)</span></span>              | <span data-ttu-id="f7c05-144">Czerwony</span><span class="sxs-lookup"><span data-stu-id="f7c05-144">Red</span></span>           |

<span data-ttu-id="f7c05-145">Aby ukończyć instalację na sprzęt, musisz:</span><span class="sxs-lookup"><span data-stu-id="f7c05-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="f7c05-146">Twoje Pi malina nawiązać połączenia z zasilacz zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="f7c05-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="f7c05-147">Twoje Pi malina nawiązanie połączenia z siecią za pomocą kabla Ethernet zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="f7c05-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="f7c05-148">Alternatywnie możesz skonfigurować [łączności bezprzewodowej] [ lnk-pi-wireless] Twojego malina pi.</span><span class="sxs-lookup"><span data-stu-id="f7c05-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="f7c05-149">Ustawienia sprzętu z Pi malina zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="f7c05-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="f7c05-150">Zaloguj się i uzyskać dostęp terminala</span><span class="sxs-lookup"><span data-stu-id="f7c05-150">Sign in and access the terminal</span></span>

<span data-ttu-id="f7c05-151">Dostępne są dwie opcje środowisku końcowych dla sieci Pi malina dostępu do:</span><span class="sxs-lookup"><span data-stu-id="f7c05-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="f7c05-152">Jeśli masz klawiatury i monitora podłączone do sieci Pi malina umożliwia Raspbian graficzny interfejs użytkownika dostępu okno terminala.</span><span class="sxs-lookup"><span data-stu-id="f7c05-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="f7c05-153">Dostęp do wiersza polecenia na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="f7c05-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="f7c05-154">Okno terminalu w graficznym interfejsie użytkownika</span><span class="sxs-lookup"><span data-stu-id="f7c05-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="f7c05-155">Nazwa użytkownika są domyślne poświadczenia dla Raspbian **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="f7c05-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="f7c05-156">Na pasku zadań w interfejsie GUI, uruchom **Terminal** narzędzie przy użyciu ikony, która wygląda jak monitora.</span><span class="sxs-lookup"><span data-stu-id="f7c05-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="f7c05-157">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="f7c05-157">Sign in with SSH</span></span>

<span data-ttu-id="f7c05-158">Umożliwia SSH dla wiersza polecenia dostępu użytkownika Pi malina.</span><span class="sxs-lookup"><span data-stu-id="f7c05-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="f7c05-159">Artykuł [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób konfigurowania SSH na Twoje Pi malina oraz sposób nawiązywania połączenia z [Windows] [ lnk-ssh-windows] lub [ System operacyjny Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="f7c05-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="f7c05-160">Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="f7c05-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="f7c05-161">Opcjonalnie: Udostępnianie folderu w Twojej Pi malina</span><span class="sxs-lookup"><span data-stu-id="f7c05-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="f7c05-162">Opcjonalnie można udostępnić folder w sieci Pi malina środowisko pulpitu.</span><span class="sxs-lookup"><span data-stu-id="f7c05-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="f7c05-163">Udostępnianie folderu pozwala na użycie w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) do edycji plików w sieci Pi malina zamiast `nano` lub `vi`.</span><span class="sxs-lookup"><span data-stu-id="f7c05-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="f7c05-164">Aby udostępnić folder z systemem Windows, należy skonfigurować serwer Samba na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f7c05-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="f7c05-165">Alternatywnie można użyć wbudowanej [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serwera za pomocą klienta protokołu SFTP na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="f7c05-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="f7c05-166">Włącz SPI</span><span class="sxs-lookup"><span data-stu-id="f7c05-166">Enable SPI</span></span>

<span data-ttu-id="f7c05-167">Przed uruchomieniem aplikacji przykładowej, należy włączyć Pi malina magistrali Serial peryferyjne interfejsu (SPI).</span><span class="sxs-lookup"><span data-stu-id="f7c05-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="f7c05-168">Pi malina komunikuje się z urządzeniami czujnik BME280 przez magistralę SPI.</span><span class="sxs-lookup"><span data-stu-id="f7c05-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="f7c05-169">Aby edytować plik konfiguracji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f7c05-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="f7c05-170">Znajdź wiersz:</span><span class="sxs-lookup"><span data-stu-id="f7c05-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="f7c05-171">Aby Usuń komentarz z linii, Usuń `#` na początku.</span><span class="sxs-lookup"><span data-stu-id="f7c05-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="f7c05-172">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f7c05-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="f7c05-173">Aby włączyć SPI, ponowny rozruch malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f7c05-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="f7c05-174">Ponowny rozruch rozłącza terminala, musisz zalogować się ponownie, gdy Pi malina uruchomieniu:</span><span class="sxs-lookup"><span data-stu-id="f7c05-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/