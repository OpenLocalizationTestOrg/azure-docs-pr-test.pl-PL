## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="72853-101">Przygotowanie Twojego malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="72853-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="72853-102">Zainstaluj Raspbian</span><span class="sxs-lookup"><span data-stu-id="72853-102">Install Raspbian</span></span>

<span data-ttu-id="72853-103">Jeśli po raz pierwszy używasz programu Pi malina to hello należy tooinstall hello Raspbian systemu operacyjnego za pomocą NOOBS na karcie SD hello zawarte w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="72853-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="72853-104">Hello [malina Pi oprogramowania przewodnik] [ lnk-install-raspbian] w tym artykule opisano sposób tooinstall systemu operacyjnego na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="72853-105">W tym samouczku założono, że zainstalowano system operacyjny Raspbian hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="72853-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="72853-106">Karta Hello SD objęte hello [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] ma już NOOBS zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="72853-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="72853-107">Można uruchomić hello Pi malina z tej karty i wybrać hello tooinstall Raspbian systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="72853-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="72853-108">Konfigurowanie sprzętu hello</span><span class="sxs-lookup"><span data-stu-id="72853-108">Set up hello hardware</span></span>

<span data-ttu-id="72853-109">W tym samouczku korzysta z czujnika hello BME280 objęte hello [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] toogenerate danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="72853-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="72853-110">Używa tooindicate LED po wywołaniu metody z pulpitu nawigacyjnego rozwiązania hello przetwarza hello malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="72853-111">składniki Hello na tablicy chleb hello są:</span><span class="sxs-lookup"><span data-stu-id="72853-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="72853-112">Czerwony LED</span><span class="sxs-lookup"><span data-stu-id="72853-112">Red LED</span></span>
- <span data-ttu-id="72853-113">Ohm — 220 rezystor (czerwony, czerwony, brązowy)</span><span class="sxs-lookup"><span data-stu-id="72853-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="72853-114">Czujnik BME280</span><span class="sxs-lookup"><span data-stu-id="72853-114">BME280 sensor</span></span>

<span data-ttu-id="72853-115">Witaj poniższym diagramie przedstawiono sposób tooconnect sprzętu:</span><span class="sxs-lookup"><span data-stu-id="72853-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Ustawienia sprzętu pi malina][img-connection-diagram]

<span data-ttu-id="72853-117">Witaj Poniższa tabela zawiera podsumowanie połączeń hello ze składników toohello Pi malina hello na hello breadboard:</span><span class="sxs-lookup"><span data-stu-id="72853-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="72853-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="72853-118">Raspberry Pi</span></span>            | <span data-ttu-id="72853-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="72853-119">Breadboard</span></span>             |<span data-ttu-id="72853-120">Kolor</span><span class="sxs-lookup"><span data-stu-id="72853-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="72853-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="72853-121">GND (Pin 14)</span></span>            | <span data-ttu-id="72853-122">Numer pin - kolejnych LED (18A)</span><span class="sxs-lookup"><span data-stu-id="72853-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="72853-123">Fioletowy</span><span class="sxs-lookup"><span data-stu-id="72853-123">Purple</span></span>          |
| <span data-ttu-id="72853-124">GPCLK0 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="72853-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="72853-125">Rezystor (25A)</span><span class="sxs-lookup"><span data-stu-id="72853-125">Resistor (25A)</span></span>         | <span data-ttu-id="72853-126">Orange</span><span class="sxs-lookup"><span data-stu-id="72853-126">Orange</span></span>          |
| <span data-ttu-id="72853-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="72853-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="72853-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="72853-128">CS (39A)</span></span>               | <span data-ttu-id="72853-129">Niebieski</span><span class="sxs-lookup"><span data-stu-id="72853-129">Blue</span></span>          |
| <span data-ttu-id="72853-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="72853-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="72853-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="72853-131">SCK (36A)</span></span>              | <span data-ttu-id="72853-132">Żółty</span><span class="sxs-lookup"><span data-stu-id="72853-132">Yellow</span></span>        |
| <span data-ttu-id="72853-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="72853-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="72853-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="72853-134">SDO (37A)</span></span>              | <span data-ttu-id="72853-135">Biały</span><span class="sxs-lookup"><span data-stu-id="72853-135">White</span></span>         |
| <span data-ttu-id="72853-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="72853-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="72853-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="72853-137">SDI (38A)</span></span>              | <span data-ttu-id="72853-138">Zielony</span><span class="sxs-lookup"><span data-stu-id="72853-138">Green</span></span>         |
| <span data-ttu-id="72853-139">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="72853-139">GND (Pin 6)</span></span>             | <span data-ttu-id="72853-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="72853-140">GND (35A)</span></span>              | <span data-ttu-id="72853-141">Czarny</span><span class="sxs-lookup"><span data-stu-id="72853-141">Black</span></span>         |
| <span data-ttu-id="72853-142">3.3 V (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="72853-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="72853-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="72853-143">3Vo (34A)</span></span>              | <span data-ttu-id="72853-144">Czerwony</span><span class="sxs-lookup"><span data-stu-id="72853-144">Red</span></span>           |

<span data-ttu-id="72853-145">ustawienia sprzętu hello toocomplete, musisz:</span><span class="sxs-lookup"><span data-stu-id="72853-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="72853-146">Połącz Pi malina toohello zasilacza zawarte w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="72853-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="72853-147">Łączenie sieci tooyour Pi malina za pomocą kabla Ethernet hello zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="72853-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="72853-148">Alternatywnie możesz skonfigurować [łączności bezprzewodowej] [ lnk-pi-wireless] Twojego malina pi.</span><span class="sxs-lookup"><span data-stu-id="72853-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="72853-149">Ustawienia sprzętu hello Twojej pi malina zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="72853-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="72853-150">Zaloguj się i uzyskać dostęp hello terminali</span><span class="sxs-lookup"><span data-stu-id="72853-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="72853-151">Masz dwie opcje tooaccess terminali środowiska użytkownika Pi malina:</span><span class="sxs-lookup"><span data-stu-id="72853-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="72853-152">Jeśli klawiatura i monitorowanie połączonych tooyour Pi malina, możesz użyć hello Raspbian GUI tooaccess okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="72853-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="72853-153">Dostęp z wiersza polecenia hello na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="72853-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="72853-154">Okno terminalu w hello graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="72853-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="72853-155">username są Hello domyślne poświadczenia dla Raspbian **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="72853-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="72853-156">Na pasku zadań hello w hello graficznego interfejsu użytkownika, możesz uruchomić hello **Terminal** narzędzie za pomocą ikony hello, która wygląda jak monitora.</span><span class="sxs-lookup"><span data-stu-id="72853-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="72853-157">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="72853-157">Sign in with SSH</span></span>

<span data-ttu-id="72853-158">Można użyć SSH dla wiersza polecenia dostępu tooyour malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="72853-159">Artykuł Hello [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób tooconfigure SSH na Twoje Pi malina i w jaki sposób tooconnect z [Windows] [ lnk-ssh-windows] lub [Systemu operacyjnego Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="72853-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="72853-160">Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="72853-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="72853-161">Opcjonalnie: Udostępnianie folderu w Twojej Pi malina</span><span class="sxs-lookup"><span data-stu-id="72853-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="72853-162">Opcjonalnie możesz tooshare folderem na Twoje Pi malina ze środowiskiem pulpitu.</span><span class="sxs-lookup"><span data-stu-id="72853-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="72853-163">Udostępnianie folderu umożliwia możesz toouse w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) plików tooedit na Twoje Pi malina zamiast `nano` lub `vi`.</span><span class="sxs-lookup"><span data-stu-id="72853-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="72853-164">tooshare folder z systemem Windows, skonfiguruj serwer Samba na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="72853-165">Alternatywnie można użyć wbudowanych hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serwera za pomocą klienta protokołu SFTP na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="72853-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="72853-166">Włącz SPI</span><span class="sxs-lookup"><span data-stu-id="72853-166">Enable SPI</span></span>

<span data-ttu-id="72853-167">Przed rozpoczęciem powitalne przykładowej aplikacji, należy włączyć magistrali Serial peryferyjne interfejsu (SPI) hello hello malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="72853-168">Hello Pi malina komunikuje się z urządzeniem czujnik BME280 hello za pośrednictwem hello SPI magistrali.</span><span class="sxs-lookup"><span data-stu-id="72853-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="72853-169">Użyj następującego pliku konfiguracji hello tooedit polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="72853-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="72853-170">Znajdź wiersz hello:</span><span class="sxs-lookup"><span data-stu-id="72853-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="72853-171">toouncomment hello wiersza, Usuń hello `#` na początku hello.</span><span class="sxs-lookup"><span data-stu-id="72853-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="72853-172">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="72853-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="72853-173">tooenable SPI, ponowny rozruch hello malina Pi.</span><span class="sxs-lookup"><span data-stu-id="72853-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="72853-174">Ponowny rozruch odłączy hello terminali, należy toosign w ponownie, gdy hello Pi malina uruchomieniu:</span><span class="sxs-lookup"><span data-stu-id="72853-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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