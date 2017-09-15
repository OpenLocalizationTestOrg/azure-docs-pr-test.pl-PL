<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="83b8d-101">Aby dodać zasady kopii zapasowych danych StorSimple</span><span class="sxs-lookup"><span data-stu-id="83b8d-101">To add a StorSimple backup policy</span></span>

1. <span data-ttu-id="83b8d-102">Przejdź do urządzenia StorSimple i kliknij pozycję **Zasady kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="83b8d-102">Go to your StorSimple device and click **Backup policy**.</span></span>

2. <span data-ttu-id="83b8d-103">W bloku **Zasady kopii zapasowych** kliknij pozycję **+ Dodaj zasady** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="83b8d-103">In the **Backup policy** blade, click **+ Add policy** from the command bar.</span></span>
   
    ![Dodawanie zasad kopii zapasowych](./media/storsimple-8000-add-backup-policy-u2/addbupol1.png)

3. <span data-ttu-id="83b8d-105">W bloku **Tworzenie zasad kopii zapasowych** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83b8d-105">In the **Create backup policy** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="83b8d-106">Pole **Wybierz urządzenie** jest automatycznie wypełniane na podstawie wybranego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="83b8d-106">**Select device** is automatically populated based on the device you selected.</span></span>
   
   2. <span data-ttu-id="83b8d-107">Podaj **Nazwę zasad** kopii zapasowych o długości od 3 do 150 znaków.</span><span class="sxs-lookup"><span data-stu-id="83b8d-107">Specify a backup **Policy name** that contains between 3 and 150 characters.</span></span> <span data-ttu-id="83b8d-108">Po utworzeniu zasad nie można zmienić ich nazwy.</span><span class="sxs-lookup"><span data-stu-id="83b8d-108">Once the policy is created, you cannot rename the policy.</span></span>
       
   3. <span data-ttu-id="83b8d-109">Aby przypisać woluminy do tych zasad kopii zapasowych, wybierz pozycję **Dodaj woluminy**, a następnie na tabelarycznej liście woluminów kliknij pola wyboru, aby przypisać woluminy do tych zasad kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="83b8d-109">To assign volumes to this backup policy, select **Add volumes** and then from the tabular listing of volumes, click the check box(es) to assign one or more volumes to this backup policy.</span></span>

       ![Dodawanie zasad kopii zapasowych](./media/storsimple-8000-add-backup-policy-u2/addbupol2.png)

   4. <span data-ttu-id="83b8d-111">Aby zdefiniować harmonogram dla tych zasad kopii zapasowych, kliknij pozycję **Pierwszy harmonogram**, a następnie zmodyfikuj następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="83b8d-111">To define a schedule for this backup policy, click **First schedule** and then modify the following parameters:</span></span>

       ![Dodawanie zasad kopii zapasowych](./media/storsimple-8000-add-backup-policy-u2/addbupol3.png)

       1. <span data-ttu-id="83b8d-113">Dla pozycji **Typ migawki** wybierz opcję **Chmura** lub **Lokalna**.</span><span class="sxs-lookup"><span data-stu-id="83b8d-113">For **Snapshot type**, select **Cloud** or **Local**.</span></span>

       2. <span data-ttu-id="83b8d-114">Podaj częstotliwość wykonywania kopii zapasowych (określ liczbę, a następnie wybierz z listy rozwijanej pozycję **Dni** lub **Tygodnie**).</span><span class="sxs-lookup"><span data-stu-id="83b8d-114">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list.</span></span>

       3. <span data-ttu-id="83b8d-115">Wprowadź harmonogram przechowywania.</span><span class="sxs-lookup"><span data-stu-id="83b8d-115">Enter a retention schedule.</span></span>

       4. <span data-ttu-id="83b8d-116">Wprowadź datę i godzinę rozpoczęcia dla zasad kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="83b8d-116">Enter a time and date for the backup policy to begin.</span></span>

       5. <span data-ttu-id="83b8d-117">Kliknij przycisk **OK**, aby zdefiniować harmonogram.</span><span class="sxs-lookup"><span data-stu-id="83b8d-117">Click **OK** to define the schedule.</span></span>

   5. <span data-ttu-id="83b8d-118">Kliknij przycisk **Utwórz**, aby utworzyć zasady kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="83b8d-118">Click **Create** to create a backup policy.</span></span>

       ![Dodawanie zasad kopii zapasowych](./media/storsimple-8000-add-backup-policy-u2/addbupol4.png)
   
   6. <span data-ttu-id="83b8d-120">Otrzymasz powiadomienie o utworzeniu zasad kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="83b8d-120">You are notified when the backup policy is created.</span></span> <span data-ttu-id="83b8d-121">Nowo dodane zasady będą wyświetlane w widoku tabelarycznym w bloku **Zasady kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="83b8d-121">The newly added policy is displayed in the tabular view on the **Backup Policy** blade.</span></span>

       ![Dodawanie zasad kopii zapasowych](./media/storsimple-8000-add-backup-policy-u2/addbupol7.png)

