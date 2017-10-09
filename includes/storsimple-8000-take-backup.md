<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="3798d-101">tootake kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="3798d-101">tootake a backup</span></span>

1. <span data-ttu-id="3798d-102">Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3798d-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3798d-103">Z hello tabelarycznej listę urządzeń, wybierz i kliknij urządzenie, a następnie kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="3798d-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="3798d-104">W hello **ustawienia** bloku Przejdź zbyt**Ustawienia > Zarządzaj > kopii zapasowej zasad**.</span><span class="sxs-lookup"><span data-stu-id="3798d-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="3798d-106">W hello **kopii zapasowej zasad** bloku, kliknij przycisk **+ Dodaj zasady**.</span><span class="sxs-lookup"><span data-stu-id="3798d-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="3798d-108">W hello **tworzenia zasad tworzenia kopii zapasowej** bloku, podaj nazwę, która zawiera od 3 do 150 znaków dla zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3798d-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="3798d-109">Wybierz hello toobe woluminów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3798d-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="3798d-110">W przypadku wybrania więcej niż jednego woluminu woluminy te są zgrupowane razem toocreate kopia zapasowa spójna w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="3798d-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="3798d-112">W bloku **Dodaj pierwszy harmonogram**:</span><span class="sxs-lookup"><span data-stu-id="3798d-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="3798d-113">Wybierz typ hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3798d-113">Select hello type of backup.</span></span> <span data-ttu-id="3798d-114">Aby szybciej przeprowadzać operacje przywracania, wybierz pozycję **Migawka lokalna**.</span><span class="sxs-lookup"><span data-stu-id="3798d-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="3798d-115">Aby zachować odporność danych, wybierz pozycję **Migawka w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="3798d-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="3798d-116">Określ częstotliwość wykonywania kopii zapasowych hello w minuty, godziny, dni lub tygodnie.</span><span class="sxs-lookup"><span data-stu-id="3798d-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="3798d-117">Wybierz czas przechowywania.</span><span class="sxs-lookup"><span data-stu-id="3798d-117">Select a retention time.</span></span> <span data-ttu-id="3798d-118">Witaj opcje przechowywania zależą od hello częstotliwość wykonywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3798d-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="3798d-119">Na przykład codzienne zasad, przechowywania hello można określić w tygodniach, natomiast czas przechowywania w przypadku zasad miesięcznych jest w miesiącach.</span><span class="sxs-lookup"><span data-stu-id="3798d-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="3798d-120">Wybierz hello uruchamianie czasu i daty hello zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3798d-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="3798d-121">Kliknij przycisk **OK** zasad tworzenia kopii zapasowej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3798d-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="3798d-123">Kliknij przycisk **Utwórz** tworzenia zasad tworzenia kopii zapasowej hello toostart.</span><span class="sxs-lookup"><span data-stu-id="3798d-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="3798d-124">Użytkownik jest powiadamiany o hello zasad tworzenia kopii zapasowej został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3798d-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="3798d-125">Zaktualizowano także Hello listę zasad tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3798d-125">hello list of backup policies is also updated.</span></span>
      
      ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="3798d-127">Masz teraz zasady kopii zapasowych, które będą powodować tworzenie zaplanowanych kopii zapasowych danych woluminu.</span><span class="sxs-lookup"><span data-stu-id="3798d-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




