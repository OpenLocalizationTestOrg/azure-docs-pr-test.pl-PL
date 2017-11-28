<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="4d5b5-101">Aby utworzyć kopię zapasową</span><span class="sxs-lookup"><span data-stu-id="4d5b5-101">To take a backup</span></span>

1. <span data-ttu-id="4d5b5-102">Przejdź do usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="4d5b5-103">Z tabelarycznej listy urządzeń wybierz i kliknij swoje urządzenie, a następnie kliknij pozycję **Wszystkie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="4d5b5-104">W bloku **Ustawienia** przejdź do pozycji **Ustawienia > Zarządzaj > Zasady kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="4d5b5-106">W bloku **Zasady kopii zapasowych** kliknij pozycję **+ Dodaj zasady**.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="4d5b5-108">W bloku **Określanie zasad tworzenia kopii zapasowych** podaj nazwę zasad tworzenia kopii zapasowej składającą się z 3–150 znaków.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="4d5b5-109">Wybierz woluminy do wykonania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="4d5b5-110">W przypadku wybrania więcej niż jednego woluminu woluminy te są grupowane w celu utworzenia kopii zapasowej spójnej na poziomie awarii.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="4d5b5-112">W bloku **Dodaj pierwszy harmonogram**:</span><span class="sxs-lookup"><span data-stu-id="4d5b5-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="4d5b5-113">Wybierz typ kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-113">Select the type of backup.</span></span> <span data-ttu-id="4d5b5-114">Aby szybciej przeprowadzać operacje przywracania, wybierz pozycję **Migawka lokalna**.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="4d5b5-115">Aby zachować odporność danych, wybierz pozycję **Migawka w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="4d5b5-116">Określ częstotliwość wykonywania kopii zapasowych w minutach, godzinach, dniach lub tygodniach.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="4d5b5-117">Wybierz czas przechowywania.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-117">Select a retention time.</span></span> <span data-ttu-id="4d5b5-118">Opcje przechowywania zależą od częstotliwości tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="4d5b5-119">Na przykład w przypadku zasad dziennych można określić zasady przechowywania w tygodniach, natomiast czas przechowywania w przypadku zasad miesięcznych jest wyrażany w miesiącach.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="4d5b5-120">Wybierz datę i godzinę rozpoczęcia dla zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="4d5b5-121">Kliknij pozycję **OK**, aby utworzyć zasady kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-121">Click **OK** to create the backup policy.</span></span>

        ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="4d5b5-123">Kliknij przycisk **Utwórz**, aby zacząć tworzenie zasad kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="4d5b5-124">Otrzymasz powiadomienie o pomyślnym utworzeniu zasad kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="4d5b5-125">Lista zasad kopii zapasowych także zostanie zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-125">The list of backup policies is also updated.</span></span>
      
      ![Dodawanie zasad tworzenia kopii zapasowej](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="4d5b5-127">Masz teraz zasady kopii zapasowych, które będą powodować tworzenie zaplanowanych kopii zapasowych danych woluminu.</span><span class="sxs-lookup"><span data-stu-id="4d5b5-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




