
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="cac8a-101">Ręczne tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cac8a-101">To create a manual backup</span></span>

1. <span data-ttu-id="cac8a-102">Przejdź do usługi Menedżer urządzeń StorSimple, a następnie kliknij pozycję **Urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="cac8a-102">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="cac8a-103">Na tabelarycznej liście urządzeń wybierz urządzenie.</span><span class="sxs-lookup"><span data-stu-id="cac8a-103">From the tabular listing of devices, select your device.</span></span> <span data-ttu-id="cac8a-104">Przejdź kolejno do pozycji **Ustawienia > Zarządzaj > Zasady dotyczące kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="cac8a-104">Go to **Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="cac8a-105">Blok **Zasady dotyczące kopii zapasowych** zawiera listę wszystkich zasad dotyczących kopii zapasowych w formie tabeli, w tym zasad dla woluminu, którego kopię zapasową chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="cac8a-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span></span> <span data-ttu-id="cac8a-106">Wybierz zasady skojarzone z woluminem, którego kopię zapasową chcesz utworzyć, i kliknij prawym przyciskiem myszy, aby wywołać menu kontekstowe.</span><span class="sxs-lookup"><span data-stu-id="cac8a-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span></span> <span data-ttu-id="cac8a-107">Z listy rozwijanej wybierz pozycję **Utwórz kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="cac8a-107">From the dropdown list, select **Back up now**.</span></span>

    ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="cac8a-109">W bloku **Utwórz kopię zapasową teraz** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cac8a-109">In the **Back up now** blade, do the following steps:</span></span>

    1. <span data-ttu-id="cac8a-110">Wybierz odpowiedni **typ migawki** z listy rozwijanej: migawka **lokalna** lub migawka **w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="cac8a-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="cac8a-111">Wybierz migawkę lokalną, jeśli chcesz szybko tworzyć kopie zapasowe lub je przywracać, albo migawkę w chmurze, jeśli zależy Ci na odporności danych.</span><span class="sxs-lookup"><span data-stu-id="cac8a-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="cac8a-113">Kliknij przycisk **OK**, aby uruchomić zadanie tworzenia migawki.</span><span class="sxs-lookup"><span data-stu-id="cac8a-113">Click **OK** to start a job to create a snapshot.</span></span> <span data-ttu-id="cac8a-114">Po pomyślnym utworzeniu zadania w górnej części strony zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="cac8a-114">You will see a notification at the top of the page after the job is successfully created.</span></span>

        ![Ręczne tworzenie kopii zapasowych](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="cac8a-116">Aby monitorować zadanie, kliknij powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="cac8a-116">To monitor the job, click the notification.</span></span> <span data-ttu-id="cac8a-117">Spowoduje to przejście do bloku **Zadania**, w którym można wyświetlić postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="cac8a-117">This takes you to the **Jobs** blade where you can view the job progress.</span></span>


5. <span data-ttu-id="cac8a-118">Po zakończeniu zadania tworzenia kopii zapasowej przejdź do karty **Katalog kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="cac8a-118">After the backup job is finished, go to the **Backup catalog** tab.</span></span>

6. <span data-ttu-id="cac8a-119">Ustaw wybory filtrów do odpowiedniego urządzenia, odpowiednich zasad tworzenia kopii zapasowej i odpowiedniego zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="cac8a-119">Set the filter selections to the appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="cac8a-120">Kopia zapasowa powinna pojawić się na liście zestawów kopii zapasowych, która jest wyświetlana w katalogu.</span><span class="sxs-lookup"><span data-stu-id="cac8a-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

