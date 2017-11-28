---
title: aaaBackup maszyn wirtualnych systemu Windows Azure | Dokumentacja firmy Microsoft
description: "Ochrona maszyn wirtualnych systemu Windows przez tworzenie ich kopii zapasowych za pomocą usługi Kopia zapasowa Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="a4ecf-103">Tworzenie kopii zapasowych maszyn wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a4ecf-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="a4ecf-104">Możesz chronić swoje dane, tworząc kopie zapasowe w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="a4ecf-105">Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="a4ecf-106">Po przywróceniu z punktu odzyskiwania, można przywrócić hello całej maszyny Wirtualnej lub po prostu określonych plików.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="a4ecf-107">W tym artykule opisano, jak toorestore pojedynczy plik tooa wirtualna systemem Windows Server i usług IIS.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="a4ecf-108">Jeśli nie masz jeszcze toouse maszyny Wirtualnej, możesz utworzyć jedną przy użyciu hello [Szybki Start systemu Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4ecf-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="a4ecf-109">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a4ecf-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4ecf-110">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="a4ecf-111">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="a4ecf-112">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="a4ecf-113">Omówienie usługi Backup</span><span class="sxs-lookup"><span data-stu-id="a4ecf-113">Backup overview</span></span>

<span data-ttu-id="a4ecf-114">Gdy hello usługi Kopia zapasowa Azure inicjuje zadania tworzenia kopii zapasowej, wyzwala hello zapasowy numer wewnętrzny tootake migawki punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="a4ecf-115">Witaj usługi Kopia zapasowa Azure korzysta hello _VMSnapshot_ rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="a4ecf-116">rozszerzenie Hello jest instalowany podczas hello pierwszej kopii zapasowej maszyny Wirtualnej, jeśli hello maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="a4ecf-117">Jeśli hello maszyna wirtualna nie jest uruchomiona, hello usługi Kopia zapasowa tworzy migawkę hello bazowy magazynu (ponieważ nie zapisy aplikacji występuje podczas powitalne zatrzymaniu maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="a4ecf-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="a4ecf-118">Podczas wykonywania migawki maszyn wirtualnych systemu Windows, usługi Kopia zapasowa hello koordynuje z tooget usługi kopiowania woluminów w tle (VSS) hello spójne migawek dysków maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="a4ecf-119">Witaj usługi Kopia zapasowa Azure wykonuje migawkę hello, hello danych po toohello przekazanych magazynu.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="a4ecf-120">wydajność toomaximize hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="a4ecf-121">Po ukończeniu transferu danych hello hello migawka zostanie usunięta i utworzenia punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="a4ecf-122">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-122">Create a backup</span></span>
<span data-ttu-id="a4ecf-123">Tworzenie prostego zaplanowanego codziennego tworzenia kopii zapasowej tooa magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="a4ecf-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a4ecf-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a4ecf-125">W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="a4ecf-126">Wybierz tooback maszyny Wirtualnej z listy hello się.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="a4ecf-127">W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="a4ecf-128">Witaj **kopii zapasowej Włącz** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="a4ecf-129">W **magazyn usług odzyskiwania i**, kliknij przycisk **Utwórz nowy** i podaj nazwę hello hello nowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="a4ecf-130">Nowy magazyn jest tworzony w hello sam lokalizacji jako maszyna wirtualna hello i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="a4ecf-131">Kliknij przycisk **kopii zapasowej zasad**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-131">Click **Backup policy**.</span></span> <span data-ttu-id="a4ecf-132">W tym przykładzie należy zachować hello wartości domyślne, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="a4ecf-133">Na powitania **kopii zapasowej Włącz** bloku, kliknij przycisk **Włącz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="a4ecf-134">Spowoduje to utworzenie kopii zapasowej codziennie na podstawie hello domyślnego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="a4ecf-135">toocreate początkowego punktu odzyskiwania, na powitania **kopii zapasowej** kliknij bloku **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="a4ecf-136">Na powitania **Utwórz kopię zapasową teraz** bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="a4ecf-137">W hello **kopii zapasowej** bloku dla maszyny Wirtualnej, zobaczysz hello liczbę punktów odzyskiwania, które są spełnione.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Punkty odzyskiwania](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="a4ecf-139">Hello pierwszej kopii zapasowej trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="a4ecf-140">Po zakończeniu tworzenia kopii zapasowej, należy kontynuować toohello następnej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="a4ecf-141">Odzyskiwanie pliku</span><span class="sxs-lookup"><span data-stu-id="a4ecf-141">Recover a file</span></span>

<span data-ttu-id="a4ecf-142">Jeśli przypadkowo usunięte lub zmiany tooa plik, można użyć pliku hello toorecover odzyskiwanie plików z magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="a4ecf-143">Odzyskiwanie plików używa skryptu uruchamianego na powitania maszyny Wirtualnej, punkt odzyskiwania hello toomount jako dysk lokalny.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="a4ecf-144">Dyski te pozostanie zainstalowanego na 12 godzin, co można kopiować pliki z punktu odzyskiwania hello i przywracać je toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="a4ecf-145">W tym przykładzie zostanie przedstawiony sposób toorecover hello plik obrazu, który jest używany w hello domyślnej strony sieci web dla usług IIS.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="a4ecf-146">Otwórz przeglądarkę i Połącz z adresu IP toohello hello wirtualna tooshow hello domyślnej IIS strony.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="a4ecf-148">Połącz toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="a4ecf-149">Na powitania maszyny Wirtualnej, otwórz **Eksploratora plików** Przejdź too\inetpub\wwwroot i usuń plik hello **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="a4ecf-150">Na komputerze lokalnym toosee przeglądarki hello odświeżania, który hello obrazu na powitania domyślnej strony usług IIS został usunięty.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="a4ecf-152">Na komputerze lokalnym, otwórz nową kartę i przejdź Witaj Witaj [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4ecf-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="a4ecf-153">W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych** i wybierz hello wirtualna formularza hello listy.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="a4ecf-154">W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="a4ecf-155">Witaj **kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="a4ecf-156">Witaj menu u góry bloku hello hello wybierz **odzyskiwanie plików**.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="a4ecf-157">Witaj **odzyskiwanie plików** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="a4ecf-158">W **krok 1: Wybierz punkt odzyskiwania**, wybierz punkt odzyskiwania z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="a4ecf-159">W **krok 2: Pobieranie skryptu toobrowse i odzyskiwanie plików**, kliknij przycisk hello **Pobierz plik wykonywalny** przycisk.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="a4ecf-160">Zapisz hello pliku tooyour **pobiera** folderu.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="a4ecf-161">Na komputerze lokalnym, otwórz **Eksploratora plików** i przejdź tooyour **pobiera** hello folderu i skopiuj pobrany plik .exe.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="a4ecf-162">Nazwa pliku Hello będzie ona poprzedzona przez nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="a4ecf-163">Na maszynie Wirtualnej (za pośrednictwem połączenia RDP hello) Wklej toohello pliku .exe hello pulpitu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="a4ecf-164">Przejdź do pulpitu toohello maszyny wirtualnej, a następnie kliknij dwukrotnie ikonę na powitania .exe.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="a4ecf-165">Zostanie uruchomiony wiersz polecenia i zainstaluj punkt odzyskiwania hello jako udział pliku, który można uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="a4ecf-166">Po zakończeniu tworzenia udziału hello, wpisz **q** tooclose hello poleceń.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="a4ecf-167">Na maszynie Wirtualnej, należy otworzyć **Eksploratora plików** i przejdź toohello literę dysku, którego użyto do udziału plików hello.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="a4ecf-168">Przejdź too\inetpub\wwwroot i skopiuj **iisstart.png** z pliku hello udziału i wklej go do \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="a4ecf-169">Na przykład F:\inetpub\wwwroot\iisstart.png skopiuj i wklej go do pliku hello toorecover c:\inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="a4ecf-170">Na komputerze lokalnym, otwórz kartę przeglądarki hello której są podłączone adres IP toohello hello wirtualna prezentująca hello IIS domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="a4ecf-171">Naciśnij klawisze CTRL + F5 toorefresh hello przeglądarki strony.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="a4ecf-172">Powinien zostać wyświetlony ten hello obrazu została przywrócona.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="a4ecf-173">Na komputerze lokalnym, przejdź wstecz karty przeglądarki toohello hello portalu Azure i w **krok 3: odinstaluj dyski powitania po odzyskaniu** kliknij hello **odinstalować dyski** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="a4ecf-174">Jeśli zapomnisz toodo ten krok, punktu instalacji toohello połączenia hello jest automatycznie Zamknij po 12 godzinach.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="a4ecf-175">Po zakończeniu tych 12 godzin wymagane toodownload nowe toocreate skryptu nowego punktu instalacji.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4ecf-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4ecf-176">Next steps</span></span>

<span data-ttu-id="a4ecf-177">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a4ecf-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4ecf-178">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="a4ecf-179">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="a4ecf-180">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a4ecf-180">Restore a file from a backup</span></span>

<span data-ttu-id="a4ecf-181">Przejdź dalej toolearn samouczka toohello dotyczące monitorowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a4ecf-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4ecf-182">Monitorowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="a4ecf-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









