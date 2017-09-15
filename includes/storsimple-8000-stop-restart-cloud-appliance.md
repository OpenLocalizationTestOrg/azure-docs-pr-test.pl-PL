#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="5714b-101">Aby zatrzymać i uruchomić urządzenie w chmurze</span><span class="sxs-lookup"><span data-stu-id="5714b-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="5714b-102">Aby zatrzymać urządzenie w chmurze, przejdź do maszyny wirtualnej dla swojego urządzenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5714b-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="5714b-103">![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="5714b-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="5714b-104">Na pasku polecenia kliknij pozycję **Stop**.</span><span class="sxs-lookup"><span data-stu-id="5714b-104">From the command bar, click **Stop**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="5714b-106">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="5714b-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="5714b-108">Po zatrzymaniu maszyny wirtualnej następuje cofnięcie jej przydziału.</span><span class="sxs-lookup"><span data-stu-id="5714b-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="5714b-109">Gdy urządzenie w chmurze jest zatrzymywane, jego stan to **Cofanie przydziału**.</span><span class="sxs-lookup"><span data-stu-id="5714b-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="5714b-110">Po zatrzymaniu urządzenia w chmurze jego stan to **Zatrzymane (cofnięty przydział)**.</span><span class="sxs-lookup"><span data-stu-id="5714b-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="5714b-112">Po zatrzymaniu maszyny wirtualnej kliknij przycisk **Uruchom** (przycisk staje się dostępny), aby uruchomić maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5714b-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="5714b-113">Po uruchomieniu urządzenia w chmurze jego stan to **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="5714b-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="5714b-115">Użyj poniższych poleceń cmdlet do zatrzymywania i uruchamiania urządzenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5714b-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="5714b-116">Aby uruchomić ponownie urządzenie w chmurze</span><span class="sxs-lookup"><span data-stu-id="5714b-116">To restart a cloud appliance</span></span>

<span data-ttu-id="5714b-117">Aby uruchomić ponownie urządzenie w chmurze, przejdź do maszyny wirtualnej dla swojego urządzenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5714b-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="5714b-118">Na pasku poleceń kliknij pozycję **Uruchom ponownie**.</span><span class="sxs-lookup"><span data-stu-id="5714b-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="5714b-119">Po wyświetleniu monitu potwierdź ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="5714b-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="5714b-120">Gdy urządzenie w chmurze jest gotowe do użycia, jego stan to **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="5714b-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="5714b-122">Użyj poniższego polecenia cmdlet, aby ponownie uruchomić urządzenie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5714b-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

