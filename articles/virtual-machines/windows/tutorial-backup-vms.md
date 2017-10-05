---
title: Maszyny wirtualne systemu Windows Azure Backup | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 8e58a2290e5034ef393f65cbcddb86e18cf4a6ec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="886b4-103">Tworzenie kopii zapasowych maszyn wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="886b4-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="886b4-104">Możesz chronić swoje dane, tworząc kopie zapasowe w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="886b4-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="886b4-105">Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego.</span><span class="sxs-lookup"><span data-stu-id="886b4-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="886b4-106">Po przywróceniu z punktu odzyskiwania, można przywrócić całej maszyny Wirtualnej lub po prostu określonych plików.</span><span class="sxs-lookup"><span data-stu-id="886b4-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="886b4-107">W tym artykule opisano sposób przywracania jednego pliku do maszyny Wirtualnej z systemem Windows Server i usług IIS.</span><span class="sxs-lookup"><span data-stu-id="886b4-107">This article explains how to restore a single file to a VM running Windows Server and IIS.</span></span> <span data-ttu-id="886b4-108">Jeśli nie masz jeszcze maszynę Wirtualną do obsługi, możesz utworzyć go przy użyciu [Szybki Start systemu Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="886b4-108">If you don't already have a VM to use, you can create one using the [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="886b4-109">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="886b4-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="886b4-110">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="886b4-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="886b4-111">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="886b4-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="886b4-112">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="886b4-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="886b4-113">Omówienie usługi Backup</span><span class="sxs-lookup"><span data-stu-id="886b4-113">Backup overview</span></span>

<span data-ttu-id="886b4-114">Gdy usługa Azure Backup Inicjuje zadania tworzenia kopii zapasowej, wyzwala zapasowy numer wewnętrzny do tworzenia migawki punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="886b4-114">When the Azure Backup service initiates a backup job, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="886b4-115">Używa usługi Azure Backup _VMSnapshot_ rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="886b4-115">The Azure Backup service uses the _VMSnapshot_ extension.</span></span> <span data-ttu-id="886b4-116">Rozszerzenie jest zainstalowany podczas pierwszego tworzenia kopii zapasowej maszyny Wirtualnej, jeśli maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="886b4-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="886b4-117">Jeśli maszyna wirtualna nie działa, usługa Kopia zapasowa tworzy migawkę powiązany magazyn (ponieważ nie zapisy aplikacji są wykonywane, gdy maszyna wirtualna zostanie zatrzymana).</span><span class="sxs-lookup"><span data-stu-id="886b4-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="886b4-118">Podczas wykonywania migawki maszyn wirtualnych systemu Windows, usługi Kopia zapasowa koordynuje z woluminów w tle kopii Service (VSS) do uzyskania migawki spójne z dysków maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="886b4-118">When taking a snapshot of Windows VMs, the Backup service coordinates with the Volume Shadow Copy Service (VSS) to get a consistent snapshot of the virtual machine's disks.</span></span> <span data-ttu-id="886b4-119">Gdy usługa Kopia zapasowa Azure przyjmuje migawki, dane są przesyłane do magazynu.</span><span class="sxs-lookup"><span data-stu-id="886b4-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="886b4-120">Aby zmaksymalizować wydajność, usługa identyfikuje i transferuje tylko bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="886b4-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="886b4-121">Po ukończeniu transferu danych migawki zostaną usunięte i utworzenia punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="886b4-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="886b4-122">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="886b4-122">Create a backup</span></span>
<span data-ttu-id="886b4-123">Utwórz prostą, zaplanowaną, codzienną operację tworzenia kopii zapasowych w magazynie usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="886b4-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="886b4-124">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="886b4-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="886b4-125">W menu po lewej stronie wybierz pozycję **Maszyny wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="886b4-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="886b4-126">Z listy wybierz maszynę wirtualną do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="886b4-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="886b4-127">W bloku maszyny Wirtualnej w **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="886b4-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="886b4-128">**Kopii zapasowej Włącz** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="886b4-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="886b4-129">W **magazyn usług odzyskiwania i**, kliknij przycisk **Utwórz nowy** i podaj nazwę dla nowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="886b4-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="886b4-130">Nowy magazyn jest tworzony w tej samej lokalizacji co maszyna wirtualna i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="886b4-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="886b4-131">Kliknij przycisk **kopii zapasowej zasad**.</span><span class="sxs-lookup"><span data-stu-id="886b4-131">Click **Backup policy**.</span></span> <span data-ttu-id="886b4-132">W tym przykładzie należy zachować ustawienia domyślne, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="886b4-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="886b4-133">Na **kopii zapasowej Włącz** bloku, kliknij przycisk **Włącz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="886b4-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="886b4-134">Spowoduje to utworzenie kopii zapasowej codziennie na podstawie harmonogramu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="886b4-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="886b4-135">Tworzenie punktu odzyskiwania początkowej na **kopii zapasowej** kliknij bloku **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="886b4-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="886b4-136">Na **Utwórz kopię zapasową teraz** bloku, kliknij ikonę kalendarza, użyj formant kalendarza, aby wybrać ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="886b4-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="886b4-137">W **kopii zapasowej** bloku dla maszyny Wirtualnej, zobaczysz liczbę punktów odzyskiwania, które są spełnione.</span><span class="sxs-lookup"><span data-stu-id="886b4-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Punkty odzyskiwania](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="886b4-139">Pierwszej kopii zapasowej trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="886b4-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="886b4-140">Po zakończeniu tworzenia kopii zapasowej, należy przejść do następnej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="886b4-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="886b4-141">Odzyskiwanie pliku</span><span class="sxs-lookup"><span data-stu-id="886b4-141">Recover a file</span></span>

<span data-ttu-id="886b4-142">Jeśli przypadkowo usunięte lub wprowadzić zmiany w pliku, możesz użyć odzyskiwania plików, aby odzyskać plik z magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="886b4-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="886b4-143">Odzyskiwanie plików używa skryptu uruchamianego na maszynie Wirtualnej, należy zainstalować punkt odzyskiwania jako dysk lokalny.</span><span class="sxs-lookup"><span data-stu-id="886b4-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="886b4-144">Dyski te pozostanie zainstalowanego na 12 godzin, co może kopiować pliki z punktu odzyskiwania i przywrócić je do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="886b4-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="886b4-145">W tym przykładzie zostanie przedstawiony sposób odzyskać plik obrazu, który jest używany w domyślnej strony sieci web dla usług IIS.</span><span class="sxs-lookup"><span data-stu-id="886b4-145">In this example, we show how to recover the image file that is used in the default web page for IIS.</span></span> 

1. <span data-ttu-id="886b4-146">Otwórz przeglądarkę i połącz się adres IP maszyny wirtualnej można wyświetlić domyślną stronę usług IIS.</span><span class="sxs-lookup"><span data-stu-id="886b4-146">Open a browser and connect to the IP address of the VM to show the default IIS page.</span></span>

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="886b4-148">Połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="886b4-148">Connect to the VM.</span></span>
3. <span data-ttu-id="886b4-149">Na Maszynie wirtualnej, należy otworzyć **Eksploratora plików** i przejdź do \inetpub\wwwroot i usuń plik **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="886b4-149">On the VM, open **File Explorer** and navigate to \inetpub\wwwroot and delete the file **iisstart.png**.</span></span>
4. <span data-ttu-id="886b4-150">Na komputerze lokalnym Odśwież przeglądarkę, aby zobaczyć, czy obraz na domyślną stronę usług IIS został usunięty.</span><span class="sxs-lookup"><span data-stu-id="886b4-150">On your local computer, refresh the browser to see that the image on the default IIS page is gone.</span></span>

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="886b4-152">Na komputerze lokalnym, otwórz nową kartę i Przejdź [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="886b4-152">On your local computer, open a new tab and go the the [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="886b4-153">W menu po lewej stronie wybierz **maszyn wirtualnych** i wybierz z listy formularza maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="886b4-153">In the menu on the left, select **Virtual machines** and select the VM form the list.</span></span>
8. <span data-ttu-id="886b4-154">W bloku maszyny Wirtualnej w **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="886b4-154">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="886b4-155">**Kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="886b4-155">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="886b4-156">Wybierz z menu w górnej części bloku **odzyskiwanie plików**.</span><span class="sxs-lookup"><span data-stu-id="886b4-156">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="886b4-157">**Odzyskiwanie plików** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="886b4-157">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="886b4-158">W **krok 1: Wybierz punkt odzyskiwania**, wybierz punkt odzyskiwania z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="886b4-158">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="886b4-159">W **krok 2: Pobieranie skryptu, aby przeglądać i odzyskiwanie plików**, kliknij przycisk **Pobierz plik wykonywalny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="886b4-159">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="886b4-160">Zapisz plik, aby Twoje **pobiera** folderu.</span><span class="sxs-lookup"><span data-stu-id="886b4-160">Save the file to your **Downloads** folder.</span></span>
12. <span data-ttu-id="886b4-161">Na komputerze lokalnym, otwórz **Eksploratora plików** i przejdź do Twojej **pobiera** folderu i skopiuj pobrany plik .exe.</span><span class="sxs-lookup"><span data-stu-id="886b4-161">On your local computer, open **File Explorer** and navigate to your **Downloads** folder and copy the downloaded .exe file.</span></span> <span data-ttu-id="886b4-162">Nazwa pliku będzie ona poprzedzona przez nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="886b4-162">The filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="886b4-163">Na maszynie Wirtualnej (za pośrednictwem połączenia RDP) Wklej plik .exe na pulpicie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="886b4-163">On your VM (over the RDP connection) paste the .exe file to the Desktop of your VM.</span></span> 
14. <span data-ttu-id="886b4-164">Przejdź do pulpitu z maszyną Wirtualną, a następnie kliknij dwukrotnie ikonę na .exe.</span><span class="sxs-lookup"><span data-stu-id="886b4-164">Navigate to the desktop of your VM and double-click on the .exe.</span></span> <span data-ttu-id="886b4-165">Zostanie uruchomiony wiersz polecenia i następnie zainstalować punkt odzyskiwania jako udział pliku, który można uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="886b4-165">This will launch a command prompt and then mount the recovery point as a file share that you can access.</span></span> <span data-ttu-id="886b4-166">Po zakończeniu tworzenia udziału wpisz **q** aby zamknąć okno wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="886b4-166">When it is finished creating the share, type **q** to close the command prompt.</span></span>
15. <span data-ttu-id="886b4-167">Na maszynie Wirtualnej, należy otworzyć **Eksploratora plików** i przejdź do litery dysku, którego użyto do udziału plików.</span><span class="sxs-lookup"><span data-stu-id="886b4-167">On your VM, open **File Explorer** and navigate to the drive letter that was used for the file share.</span></span>
16. <span data-ttu-id="886b4-168">Przejdź do \inetpub\wwwroot i skopiuj **iisstart.png** z pliku udziału i wklej go do \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="886b4-168">Navigate to \inetpub\wwwroot and copy **iisstart.png** from the file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="886b4-169">Na przykład F:\inetpub\wwwroot\iisstart.png skopiować i wkleić c:\inetpub\wwwroot odzyskać pliku.</span><span class="sxs-lookup"><span data-stu-id="886b4-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot to recover the file.</span></span>
17. <span data-ttu-id="886b4-170">Na komputerze lokalnym otwórz kartę przeglądarki, w której są podłączone do adresu IP maszyny wirtualnej przedstawiający domyślną stronę usług IIS.</span><span class="sxs-lookup"><span data-stu-id="886b4-170">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the IIS default page.</span></span> <span data-ttu-id="886b4-171">Naciśnij klawisze CTRL + F5, aby odświeżyć stronę przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="886b4-171">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="886b4-172">Powinna zostać wyświetlona, że obraz został przywrócony.</span><span class="sxs-lookup"><span data-stu-id="886b4-172">You should now see that the image has been restored.</span></span>
18. <span data-ttu-id="886b4-173">Na komputerze lokalnym, wróć do karty przeglądarki dla portalu Azure i w **krok 3: odinstaluj dyski po odzyskaniu** kliknij **odinstalować dyski** przycisku.</span><span class="sxs-lookup"><span data-stu-id="886b4-173">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="886b4-174">Jeśli zapomnisz wykonać ten krok, połączenie punktu instalacji jest automatycznie Zamknij po 12 godzinach.</span><span class="sxs-lookup"><span data-stu-id="886b4-174">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="886b4-175">Po tych 12 godzin należy pobrać nowe skryptu można utworzyć nowego punktu instalacji.</span><span class="sxs-lookup"><span data-stu-id="886b4-175">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="886b4-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="886b4-176">Next steps</span></span>

<span data-ttu-id="886b4-177">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="886b4-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="886b4-178">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="886b4-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="886b4-179">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="886b4-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="886b4-180">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="886b4-180">Restore a file from a backup</span></span>

<span data-ttu-id="886b4-181">Przejdź do następnego samouczka, aby dowiedzieć się więcej na temat monitorowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="886b4-181">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="886b4-182">Monitorowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="886b4-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









