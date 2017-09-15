## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="7372e-101">Przygotowanie Twojego malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="7372e-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="7372e-102">Zainstaluj Raspbian</span><span class="sxs-lookup"><span data-stu-id="7372e-102">Install Raspbian</span></span>

<span data-ttu-id="7372e-103">Jeśli jest to w przypadku korzystania z Pi malina po raz pierwszy, musisz zainstalować Raspbian systemu operacyjnego za pomocą NOOBS na kartę SD. zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="7372e-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="7372e-104">[Malina Pi oprogramowania przewodnik] [ lnk-install-raspbian] opisuje sposób instalowania systemu operacyjnego na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="7372e-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="7372e-105">W tym samouczku założono, że na Twoje Pi malina zainstalowano Raspbian systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7372e-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="7372e-106">Karta SD objęte [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] ma już zainstalowany NOOBS.</span><span class="sxs-lookup"><span data-stu-id="7372e-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="7372e-107">Możesz rozruch Pi malina z tej karty i wybrać opcję instalacji systemu operacyjnego Raspbian.</span><span class="sxs-lookup"><span data-stu-id="7372e-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="7372e-108">Aby ukończyć instalację na sprzęt, musisz:</span><span class="sxs-lookup"><span data-stu-id="7372e-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="7372e-109">Twoje Pi malina nawiązać połączenia z zasilacz zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="7372e-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="7372e-110">Twoje Pi malina nawiązanie połączenia z siecią za pomocą kabla Ethernet zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="7372e-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="7372e-111">Alternatywnie możesz skonfigurować [łączności bezprzewodowej] [ lnk-pi-wireless] Twojego malina pi.</span><span class="sxs-lookup"><span data-stu-id="7372e-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="7372e-112">Ustawienia sprzętu z Pi malina zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="7372e-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="7372e-113">Zaloguj się i uzyskać dostęp terminala</span><span class="sxs-lookup"><span data-stu-id="7372e-113">Sign in and access the terminal</span></span>

<span data-ttu-id="7372e-114">Dostępne są dwie opcje środowisku końcowych dla sieci Pi malina dostępu do:</span><span class="sxs-lookup"><span data-stu-id="7372e-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="7372e-115">Jeśli masz klawiatury i monitora podłączone do sieci Pi malina umożliwia Raspbian graficzny interfejs użytkownika dostępu okno terminala.</span><span class="sxs-lookup"><span data-stu-id="7372e-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="7372e-116">Dostęp do wiersza polecenia na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="7372e-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="7372e-117">Okno terminalu w graficznym interfejsie użytkownika</span><span class="sxs-lookup"><span data-stu-id="7372e-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="7372e-118">Nazwa użytkownika są domyślne poświadczenia dla Raspbian **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="7372e-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="7372e-119">Na pasku zadań w interfejsie GUI, uruchom **Terminal** narzędzie przy użyciu ikony, która wygląda jak monitora.</span><span class="sxs-lookup"><span data-stu-id="7372e-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="7372e-120">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="7372e-120">Sign in with SSH</span></span>

<span data-ttu-id="7372e-121">Umożliwia SSH dla wiersza polecenia dostępu użytkownika Pi malina.</span><span class="sxs-lookup"><span data-stu-id="7372e-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="7372e-122">Artykuł [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób konfigurowania SSH na Twoje Pi malina oraz sposób nawiązywania połączenia z [Windows] [ lnk-ssh-windows] lub [ System operacyjny Linux & Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="7372e-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="7372e-123">Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.</span><span class="sxs-lookup"><span data-stu-id="7372e-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="7372e-124">Opcjonalnie: Udostępnianie folderu w Twojej Pi malina</span><span class="sxs-lookup"><span data-stu-id="7372e-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="7372e-125">Opcjonalnie można udostępnić folder w sieci Pi malina środowisko pulpitu.</span><span class="sxs-lookup"><span data-stu-id="7372e-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="7372e-126">Udostępnianie folderu pozwala na użycie w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) do edycji plików w sieci Pi malina zamiast `nano` lub `vi`.</span><span class="sxs-lookup"><span data-stu-id="7372e-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="7372e-127">Aby udostępnić folder z systemem Windows, należy skonfigurować serwer Samba na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="7372e-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="7372e-128">Alternatywnie można użyć wbudowanej [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serwera za pomocą klienta protokołu SFTP na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="7372e-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/