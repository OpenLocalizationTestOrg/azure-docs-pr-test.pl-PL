#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="89223-101">toostop i rozpocząć urządzenia chmury</span><span class="sxs-lookup"><span data-stu-id="89223-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="89223-102">toostop urządzenia chmury, przejdź toohello maszyny Wirtualnej dla urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="89223-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="89223-103">![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="89223-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="89223-104">Na pasku poleceń hello, kliknij **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="89223-104">From hello command bar, click **Stop**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="89223-106">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="89223-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="89223-108">Po zatrzymaniu maszyny wirtualnej następuje cofnięcie jej przydziału.</span><span class="sxs-lookup"><span data-stu-id="89223-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="89223-109">Gdy urządzenia chmury hello jest zatrzymywana, jego stan jest **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="89223-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="89223-110">Po wyłączeniu urządzenia chmury hello jego stan jest **zatrzymane (cofnięciu przydziału)**.</span><span class="sxs-lookup"><span data-stu-id="89223-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="89223-112">Po zatrzymaniu maszyny Wirtualnej, kliknij przycisk **Start** (przycisk jest dostępny) hello toostart maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89223-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="89223-113">Po uruchomieniu urządzenia chmury hello, jego stan jest **uruchomiono**.</span><span class="sxs-lookup"><span data-stu-id="89223-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="89223-115">Użyj następującego polecenia cmdlet toostop hello i uruchomić urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="89223-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="89223-116">toorestart urządzenia chmury</span><span class="sxs-lookup"><span data-stu-id="89223-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="89223-117">toorestart urządzenia chmury, przejdź toohello maszyny Wirtualnej dla urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="89223-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="89223-118">Na pasku poleceń hello, kliknij **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="89223-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="89223-119">Po wyświetleniu monitu Potwierdź hello ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="89223-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="89223-120">Gdy urządzenia chmury hello jest gotowy do możesz toouse, jego stan jest **systemem**.</span><span class="sxs-lookup"><span data-stu-id="89223-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="89223-122">Użyj następującego polecenia cmdlet toorestart urządzenia chmury hello.</span><span class="sxs-lookup"><span data-stu-id="89223-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

