## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="02dc1-101">Przygotowanie programu Intel NUC</span><span class="sxs-lookup"><span data-stu-id="02dc1-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="02dc1-102">ustawienia sprzętu hello toocomplete, musisz:</span><span class="sxs-lookup"><span data-stu-id="02dc1-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="02dc1-103">Połącz Intel NUC toohello zasilacza zawarte w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="02dc1-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="02dc1-104">Łączenie sieci tooyour Intel NUC za pomocą kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="02dc1-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="02dc1-105">Ustawienia sprzętu hello urządzenie bramy Intel NUC zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="02dc1-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="02dc1-106">Zaloguj się i uzyskać dostęp hello terminali</span><span class="sxs-lookup"><span data-stu-id="02dc1-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="02dc1-107">Masz dwie opcje tooaccess środowisku terminal na Twojej NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="02dc1-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="02dc1-108">Klawiatura i monitorowanie połączonych tooyour NUC firmy Intel, można przejść do powłoki hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="02dc1-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="02dc1-109">poświadczenia domyślne Hello są nazwy użytkownika **głównego** i hasło **głównego**.</span><span class="sxs-lookup"><span data-stu-id="02dc1-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="02dc1-110">Powłoka hello dostępu na Twojej NUC Intel przy użyciu protokołu SSH z komputera stacjonarnego.</span><span class="sxs-lookup"><span data-stu-id="02dc1-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="02dc1-111">Zaloguj się przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="02dc1-111">Sign in with SSH</span></span>

<span data-ttu-id="02dc1-112">toosign się przy użyciu protokołu SSH, należy hello adres IP Twojego NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="02dc1-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="02dc1-113">Jeśli klawiatura i monitorowanie połączonych tooyour NUC firmy Intel, użyj hello `ifconfig` adres IP hello toofind polecenia.</span><span class="sxs-lookup"><span data-stu-id="02dc1-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="02dc1-114">Alternatywnie można połączyć z tooyour router toolist hello adresów urządzeń w sieci.</span><span class="sxs-lookup"><span data-stu-id="02dc1-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="02dc1-115">Zaloguj się przy użyciu nazwy użytkownika **głównego** i hasło **głównego**.</span><span class="sxs-lookup"><span data-stu-id="02dc1-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="02dc1-116">Opcjonalnie: Udostępnianie folderu w Twojej NUC Intel</span><span class="sxs-lookup"><span data-stu-id="02dc1-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="02dc1-117">Opcjonalnie możesz tooshare folderem na Twojej NUC Intel ze środowiskiem pulpitu.</span><span class="sxs-lookup"><span data-stu-id="02dc1-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="02dc1-118">Udostępnianie folderu umożliwia możesz toouse w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) plików tooedit na NUC Twojego Intel zamiast `nano` lub `vi`.</span><span class="sxs-lookup"><span data-stu-id="02dc1-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="02dc1-119">tooshare folder z systemem Windows, skonfiguruj serwer Samba na powitania Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="02dc1-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="02dc1-120">Można również użyć hello SFTP serwera na powitania Intel NUC za pomocą protokołu SFTP klienta na komputerze pulpitu.</span><span class="sxs-lookup"><span data-stu-id="02dc1-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
