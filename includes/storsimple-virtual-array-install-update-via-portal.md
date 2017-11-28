<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="fc8f5-101">Aby zainstalować aktualizacje za pośrednictwem witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc8f5-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="fc8f5-102">Przejdź do menedżera urządzeń StorSimple i wybierz pozycję **Urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="fc8f5-103">Na liście urządzeń połączonych z usługą wybierz i kliknij urządzenie, które chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="fc8f5-105">W bloku **Ustawienia** kliknij pozycję **Aktualizacje urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="fc8f5-107">Zostanie wyświetlony komunikat, jeśli aktualizacje oprogramowania są dostępne.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="fc8f5-108">Aby sprawdzić dostępność aktualizacji, możesz także kliknąć pozycję **Skanuj**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-108">To check for updates, you can also click **Scan**.</span></span>

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="fc8f5-110">Otrzymasz powiadomienie, gdy skanowanie zostanie uruchomione i zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="fc8f5-112">Po przeskanowaniu aktualizacji kliknij pozycję **Pobierz aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="fc8f5-114">W bloku **Nowe aktualizacje** zapoznaj się z informacjami o konieczności potwierdzenia instalacji po pobraniu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="fc8f5-115">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-115">Click **OK**.</span></span>

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="fc8f5-117">Otrzymasz powiadomienie, gdy przekazywanie zostanie uruchomione i zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-117">You are notified when the upload starts and completes successfully.</span></span>

     ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="fc8f5-119">W bloku **Aktualizacje urządzeń** kliknij pozycję **Instaluj**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-119">In the **Device updates** blade, click **Install**.</span></span>

     ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="fc8f5-121">W bloku **Nowe aktualizacje** zostanie wyświetlone ostrzeżenie, że aktualizacja spowoduje utrudnienia.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="fc8f5-122">Ponieważ macierz wirtualna to urządzenie o jednym węźle, urządzenie zostanie ponownie uruchomione po zaktualizowaniu.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="fc8f5-123">Spowoduje to zakłócenie wszystkich operacji we/wy.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="fc8f5-124">Kliknij przycisk **OK**, aby zainstalować aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-124">Click **OK** to install the updates.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="fc8f5-126">Otrzymasz powiadomienie o uruchomieniu zadania instalacji.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-126">You are notified when the install job starts.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="fc8f5-128">Gdy zadanie instalacji zakończy się pomyślnie, kliknij link **Wyświetl zadanie** w bloku **Aktualizacje urządzeń** w celu monitorowania instalacji.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="fc8f5-130">Spowoduje to przejście do bloku **Instalowanie aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="fc8f5-131">W tym miejscu możesz wyświetlić szczegółowe informacje o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-131">You can view detailed information about the job here.</span></span>

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="fc8f5-133">Po pomyślnym zainstalowaniu aktualizacji, zostanie wyświetlony komunikat w tym celu w bloku aktualizacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="fc8f5-134">Wersja oprogramowania również jest zmieniana na **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="fc8f5-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![aktualizowanie urządzenia](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)