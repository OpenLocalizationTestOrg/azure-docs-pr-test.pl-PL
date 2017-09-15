## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="4d589-101">Przygotowanie programu Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4d589-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="4d589-102">Aby ukończyć instalację na sprzęt, musisz:</span><span class="sxs-lookup"><span data-stu-id="4d589-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="4d589-103">Twoje NUC Intel nawiązać połączenia z zasilacz zawarte w zestawie.</span><span class="sxs-lookup"><span data-stu-id="4d589-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="4d589-104">Twoje NUC Intel nawiązać połączenia z siecią za pośrednictwem kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="4d589-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="4d589-105">Ukończono konfigurację sprzętu urządzenie bramy Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4d589-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="4d589-106">Zaloguj się i uzyskać dostęp terminala</span><span class="sxs-lookup"><span data-stu-id="4d589-106">Sign in and access the terminal</span></span>

<span data-ttu-id="4d589-107">Dostępne są dwie opcje środowisku terminala dla Twojej firmy Intel NUC dostępu do:</span><span class="sxs-lookup"><span data-stu-id="4d589-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="4d589-108">Jeśli masz klawiatury i monitora podłączone do sieci NUC firmy Intel, możesz uzyskać dostęp powłoki bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="4d589-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="4d589-109">Poświadczenia domyślne są username **głównego** i hasło **głównego**.</span><span class="sxs-lookup"><span data-stu-id="4d589-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="4d589-110">Dostęp do powłoki na Twojej NUC Intel przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="4d589-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="4d589-111">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="4d589-111">Sign in with SSH</span></span>

<span data-ttu-id="4d589-112">Aby zalogować się przy użyciu protokołu SSH, należy adres IP Twojego NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="4d589-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="4d589-113">Jeśli masz klawiatury i monitora podłączone do sieci NUC firmy Intel, użyj `ifconfig` polecenie, aby znaleźć adres IP.</span><span class="sxs-lookup"><span data-stu-id="4d589-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="4d589-114">Można również nawiązać router w taki sposób, aby wyświetlić listę adresów urządzeń w sieci.</span><span class="sxs-lookup"><span data-stu-id="4d589-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="4d589-115">Zaloguj się przy użyciu nazwy użytkownika **głównego** i hasło **głównego**.</span><span class="sxs-lookup"><span data-stu-id="4d589-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="4d589-116">Opcjonalnie: Udostępnianie folderu w Twojej NUC Intel</span><span class="sxs-lookup"><span data-stu-id="4d589-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="4d589-117">Opcjonalnie można udostępnić folder w sieci NUC Intel środowisko pulpitu.</span><span class="sxs-lookup"><span data-stu-id="4d589-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="4d589-118">Udostępnianie folderu pozwala na użycie w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) do edycji plików w sieci NUC Intel zamiast `nano` lub `vi`.</span><span class="sxs-lookup"><span data-stu-id="4d589-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="4d589-119">Aby udostępnić folder z systemem Windows, należy skonfigurować serwer Samba na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4d589-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="4d589-120">Alternatywnie można użyć serwera SFTP na NUC Intel za pomocą protokołu SFTP klienta na komputerze pulpitu.</span><span class="sxs-lookup"><span data-stu-id="4d589-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
