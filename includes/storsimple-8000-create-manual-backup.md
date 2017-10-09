
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="86523-101">toocreate ręcznego tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="86523-101">toocreate a manual backup</span></span>

1. <span data-ttu-id="86523-102">Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="86523-102">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="86523-103">Z hello Tabelaryczny spis urządzeń wybierz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="86523-103">From hello tabular listing of devices, select your device.</span></span> <span data-ttu-id="86523-104">Przejdź za**Ustawienia > Zarządzaj > zasady tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="86523-104">Go too**Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="86523-105">Witaj **zasady tworzenia kopii zapasowej** bloku zawiera listę wszystkich zasad tworzenia kopii zapasowej hello w formie tabeli, w tym zasad hello hello woluminu, który ma tooback się.</span><span class="sxs-lookup"><span data-stu-id="86523-105">hello **Backup policies** blade lists all hello backup policies in a tabular format, including hello policy for hello volume that you want tooback up.</span></span> <span data-ttu-id="86523-106">Wybierz zasady hello skojarzonych z hello wolumin, który chcesz tooback zapasowe i menu kontekstowego hello tooinvoke kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="86523-106">Select hello policy associated with hello volume you want tooback up and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="86523-107">Wybierz z listy rozwijanej hello **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="86523-107">From hello dropdown list, select **Back up now**.</span></span>

    ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="86523-109">W hello **wykonaj kopię zapasową teraz** bloku hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="86523-109">In hello **Back up now** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="86523-110">Wybierz odpowiednie hello **migawki typu** z listy rozwijanej hello: **lokalnego** migawki lub **chmury** migawki.</span><span class="sxs-lookup"><span data-stu-id="86523-110">Choose hello appropriate **Snapshot type** from hello dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="86523-111">Wybierz migawkę lokalną, jeśli chcesz szybko tworzyć kopie zapasowe lub je przywracać, albo migawkę w chmurze, jeśli zależy Ci na odporności danych.</span><span class="sxs-lookup"><span data-stu-id="86523-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="86523-113">Kliknij przycisk **OK** toostart toocreate zadania migawki.</span><span class="sxs-lookup"><span data-stu-id="86523-113">Click **OK** toostart a job toocreate a snapshot.</span></span> <span data-ttu-id="86523-114">Po pomyślnym utworzeniu zadania hello, otrzymają powiadomienie u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="86523-114">You will see a notification at hello top of hello page after hello job is successfully created.</span></span>

        ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="86523-116">Witaj toomonitor zadania, kliknij przycisk hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="86523-116">toomonitor hello job, click hello notification.</span></span> <span data-ttu-id="86523-117">Powoduje to przejście toohello **zadania** bloku, w którym można wyświetlić postęp zadania hello.</span><span class="sxs-lookup"><span data-stu-id="86523-117">This takes you toohello **Jobs** blade where you can view hello job progress.</span></span>


5. <span data-ttu-id="86523-118">Po zakończeniu zadania tworzenia kopii zapasowej hello Przejdź toohello **katalog kopii zapasowej** kartę.</span><span class="sxs-lookup"><span data-stu-id="86523-118">After hello backup job is finished, go toohello **Backup catalog** tab.</span></span>

6. <span data-ttu-id="86523-119">Ustaw hello filtru opcje toohello odpowiedniego urządzenia, zasad tworzenia kopii zapasowej i zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="86523-119">Set hello filter selections toohello appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="86523-120">Hello kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych jest wyświetlany w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="86523-120">hello backup should appear in hello list of backup sets that is displayed in hello catalog.</span></span>

