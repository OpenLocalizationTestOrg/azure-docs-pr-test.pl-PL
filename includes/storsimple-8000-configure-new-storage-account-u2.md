<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="59891-101">Aby dodać poświadczenia konta magazynu w tej samej subskrypcji platformy Azure jako usługa Menedżer urządzeń StorSimple</span><span class="sxs-lookup"><span data-stu-id="59891-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="59891-102">Przejdź do usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="59891-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="59891-103">W sekcji **Konfiguracja** kliknij pozycję **Poświadczenia konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="59891-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![Poświadczenia konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="59891-105">W bloku **Poświadczenia konta magazynu** kliknij pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="59891-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![Dodawanie poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="59891-107">W bloku **Dodawanie poświadczenia konta magazynu** wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59891-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="59891-108">Ponieważ dodajesz poświadczenie konta magazynu w tej samej subskrypcji platformy Azure co usługa, upewnij się, że pole **Bieżące** zostało zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="59891-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="59891-109">Z listy rozwijanej **kont magazynu** wybierz istniejące konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="59891-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="59891-110">W oparciu o wybrane konto magazynu zostanie wyświetlona **lokalizacja** (wyszarzona— nie można jej zmienić w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="59891-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="59891-111">Wybierz opcję **Włącz tryb SSL**, aby utworzyć bezpieczny kanał komunikacji sieciowej między urządzeniem i chmurą.</span><span class="sxs-lookup"><span data-stu-id="59891-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="59891-112">Wyłącz opcję **Włącz protokół SSL** tylko, jeśli pracujesz w chmurze prywatnej.</span><span class="sxs-lookup"><span data-stu-id="59891-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![Blok dodawania poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="59891-114">Kliknij pozycję **Dodaj**, aby uruchomić zadanie tworzenia dla poświadczenia konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="59891-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="59891-115">Po pomyślnym utworzeniu poświadczenia konta magazynu otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="59891-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![Powiadomienie o powodzeniu dla poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="59891-117">Nowo utworzone konto magazynu zostanie wyświetlone w obszarze listy **Poświadczenia konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="59891-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![Lista poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

