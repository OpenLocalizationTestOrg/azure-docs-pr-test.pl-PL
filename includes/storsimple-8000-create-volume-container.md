<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a><span data-ttu-id="913fd-101">toocreate kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="913fd-101">toocreate a volume container</span></span>
1. <span data-ttu-id="913fd-102">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="913fd-102">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="913fd-103">Z hello tabelarycznej listę urządzeń hello wybierz i kliknij urządzenie.</span><span class="sxs-lookup"><span data-stu-id="913fd-103">From hello tabular listing of hello devices, select and click a device.</span></span> 

    ![Blok kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="913fd-105">Na pulpicie nawigacyjnym urządzenia hello, kliknij przycisk **+ Dodaj kontener woluminów**</span><span class="sxs-lookup"><span data-stu-id="913fd-105">In hello device dashboard, click **+ Add volume container**</span></span>

    ![Blok kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="913fd-107">W hello **Dodaj kontener woluminów** bloku:</span><span class="sxs-lookup"><span data-stu-id="913fd-107">In hello **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="913fd-108">urządzenie Hello jest automatycznie wybierany.</span><span class="sxs-lookup"><span data-stu-id="913fd-108">hello device is automatically selected.</span></span>
   2. <span data-ttu-id="913fd-109">Wprowadź wartość **Nazwa** kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="913fd-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="913fd-110">Nazwa Hello musi być 3 too32 znaków.</span><span class="sxs-lookup"><span data-stu-id="913fd-110">hello name must be 3 too32 characters long.</span></span> <span data-ttu-id="913fd-111">Nie można zmienić nazwy kontenera woluminów po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="913fd-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="913fd-112">Wybierz **Włącz szyfrowanie magazynu w chmurze** tooenable szyfrowania danych hello wysyłane z hello urządzenia toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="913fd-112">Select **Enable Cloud Storage Encryption** tooenable encryption of hello data sent from hello device toohello cloud.</span></span>
   4. <span data-ttu-id="913fd-113">Wprowadź i Potwierdź **klucz szyfrowania magazynu w chmurze** oznacza to 8 too32 znaków.</span><span class="sxs-lookup"><span data-stu-id="913fd-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 too32 characters long.</span></span> <span data-ttu-id="913fd-114">Ten klucz jest używany przez hello urządzenia tooaccess zaszyfrowanych danych.</span><span class="sxs-lookup"><span data-stu-id="913fd-114">This key is used by hello device tooaccess encrypted data.</span></span>
   5. <span data-ttu-id="913fd-115">Wybierz **konta magazynu** tooassociate z tym kontenerem woluminów.</span><span class="sxs-lookup"><span data-stu-id="913fd-115">Select a **Storage Account** tooassociate with this volume container.</span></span> <span data-ttu-id="913fd-116">Można wybrać istniejące konto magazynu lub hello domyślne konto, które jest generowany w momencie hello tworzenia usługi.</span><span class="sxs-lookup"><span data-stu-id="913fd-116">You can choose an existing storage account or hello default account that is generated at hello time of service creation.</span></span> <span data-ttu-id="913fd-117">Można również użyć hello **Dodaj nowe** toospecify opcji konta magazynu, który nie jest połączony toothis subskrypcji usługi.</span><span class="sxs-lookup"><span data-stu-id="913fd-117">You can also use hello **Add new** option toospecify a storage account that is not linked toothis service subscription.</span></span>
   6. <span data-ttu-id="913fd-118">Wybierz **nieograniczone** w hello **określić przepustowość** listy rozwijanej w razie potrzeby tooconsume wszystkie hello dostępną przepustowość.</span><span class="sxs-lookup"><span data-stu-id="913fd-118">Select **Unlimited** in hello **Specify bandwidth** drop-down list if you wish tooconsume all hello available bandwidth.</span></span> <span data-ttu-id="913fd-119">Można również ustawić tę opcję, zbyt**niestandardowy** tooemploy kontroli przepustowości i określ wartość z zakresu od 1 MB/s do 1000 MB/s.</span><span class="sxs-lookup"><span data-stu-id="913fd-119">You can also set this option too**Custom** tooemploy bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="913fd-120">Jeśli masz dostępnych danych użycia przepustowości, może być przepustowości może tooallocate zgodnie z harmonogramem, określając **wybierz szablon przepustowości**.</span><span class="sxs-lookup"><span data-stu-id="913fd-120">If you have your bandwidth usage information available, you may be able tooallocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="913fd-121">Procedury krok po kroku, przejdź zbyt[dodawania szablonu przepustowości](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span><span class="sxs-lookup"><span data-stu-id="913fd-121">For a step-by-step procedure, go too[Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![Blok kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="913fd-123">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="913fd-123">Click **Create**.</span></span>

        ![Blok kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="913fd-125">Użytkownik jest powiadamiany o pomyślnym utworzeniu hello kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="913fd-125">You are notified when hello volume container is successfully created.</span></span>

       ![Powiadomienie o utworzeniu kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="913fd-127">nowo utworzony kontenera woluminów Hello wymienionej na liście hello wolumin kontenerów dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="913fd-127">hello newly created volume container is listed in hello list of volume containers for your device.</span></span>

   ![Blok dodawania kontenera woluminów](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


