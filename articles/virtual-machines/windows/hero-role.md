---
title: aaaInstall IIS na pierwszej maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft
description: "Poeksperymentuj z pierwszej maszyny wirtualnej systemu Windows przez zainstalowanie usług IIS i otwieranie za pomocą portu 80 hello portalu Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="a9dc5-103">Poeksperymentuj z instalacją roli na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a9dc5-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="a9dc5-104">Po utworzeniu pierwszą maszynę wirtualną (VM) w górę i działa, możesz przejść na tooinstalling oprogramowania i usług.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="a9dc5-105">W tym samouczku zamierzamy toouse Menedżera serwera na powitania tooinstall maszyny Wirtualnej serwera systemu Windows usług IIS.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="a9dc5-106">Następnie utworzymy grupy zabezpieczeń sieci (NSG) przy użyciu hello Azure tooopen portalu port 80 tooIIS ruchu.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="a9dc5-107">Jeśli nie utworzono już pierwszej maszyny Wirtualnej, należy przejść wstecz zbyt[tworzenie pierwszej maszyny wirtualnej systemu Windows w portalu Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed kontynuowaniem w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="a9dc5-108">Upewnij się, że maszyna wirtualna działa, powitalne</span><span class="sxs-lookup"><span data-stu-id="a9dc5-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="a9dc5-109">Otwórz hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9dc5-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9dc5-110">W menu Centrum powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="a9dc5-111">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="a9dc5-112">Jeśli stan hello jest **zatrzymane (Deallocated)**, kliknij hello **Start** przycisk na powitania **Essentials** bloku hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="a9dc5-113">Jeśli jest w stanie hello **systemem**, można przenieść na toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="a9dc5-114">Podłącz maszynę wirtualną toohello i zaloguj się</span><span class="sxs-lookup"><span data-stu-id="a9dc5-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="a9dc5-115">W menu Centrum powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="a9dc5-116">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="a9dc5-117">W bloku hello hello maszyny wirtualnej, kliknij **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="a9dc5-118">To powoduje utworzenie i pobranie pliku Remote Desktop Protocol (plik RDP) przypomina maszynę tooyour tooconnect skrótów.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="a9dc5-119">Możesz toosave hello pliku tooyour pulpitu łatwy dostęp.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="a9dc5-120">**Otwórz** tooyour tooconnect ten plik maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Zrzut ekranu przedstawiający portal Azure hello jak tooyour tooconnect maszyny Wirtualnej](./media/hero-role/connect.png)
3. <span data-ttu-id="a9dc5-122">Zostanie wyświetlone ostrzeżenie, że hello plik RDP pochodzi od nieznanego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="a9dc5-123">Jest to normalne.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-123">This is normal.</span></span> <span data-ttu-id="a9dc5-124">W oknie pulpitu zdalnego powitania kliknij **Connect** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Zrzut ekranu przedstawiający ostrzeżenie o nieznanym wydawcy](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="a9dc5-126">W oknie zabezpieczenia systemu Windows hello Nazwa typu hello użytkownika i hasło dla konta lokalne powitania utworzonego podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="a9dc5-127">Nazwa użytkownika Hello jest wprowadzana jako *vmname*&#92; *Nazwa użytkownika*, następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający wprowadzanie nazwy maszyny Wirtualnej hello, nazwę użytkownika i hasło](./media/hero-role/credentials.png)
5. <span data-ttu-id="a9dc5-129">Zostanie wyświetlone ostrzeżenie nie można zweryfikować certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="a9dc5-130">Jest to normalne.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-130">This is normal.</span></span> <span data-ttu-id="a9dc5-131">Kliknij przycisk **tak** tooverify hello tożsamości hello maszyny wirtualnej i zakończyć logowanie.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Zrzut ekranu przedstawiający komunikat dotyczący, potwierdzenia tożsamości hello hello maszyny Wirtualnej](./media/hero-role/cert-warning.png)

<span data-ttu-id="a9dc5-133">Jeśli zostanie uruchomione w tootrouble podczas próby tooconnect, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9dc5-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="a9dc5-134">Instalowanie usług IIS na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a9dc5-134">Install IIS on your VM</span></span>
<span data-ttu-id="a9dc5-135">Teraz, gdy użytkownik jest zalogowany toohello maszyny Wirtualnej, dzięki czemu możesz eksperymentować zostanie zainstalowany roli serwera.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="a9dc5-136">Otwórz **Menedżera serwera**, jeśli nie jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="a9dc5-137">Kliknij przycisk hello **Start** menu, a następnie kliknij przycisk **Menedżera serwera**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="a9dc5-138">W **Menedżera serwera**, wybierz pozycję **lokalnego serwera** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="a9dc5-139">Wybierz hello menu **Zarządzaj** > **Dodaj role i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="a9dc5-140">W hello Dodaj role i funkcje kreatora na powitania **typu instalacji** wybierz pozycję **Instalacja roli lub funkcji**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Zrzut ekranu przedstawiający hello Kreatora dodawania ról i funkcji kartę typu instalacji](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="a9dc5-142">Wybierz z puli serwerów hello hello maszyny Wirtualnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="a9dc5-143">Na powitania **ról serwera** wybierz pozycję **serwer sieci Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Zrzut ekranu przedstawiający hello Kreatora dodawania ról i funkcji kartę dla ról serwera](./media/hero-role/add-iis.png)
7. <span data-ttu-id="a9dc5-145">Upewnij się, że w hello wyskakującego o dodawaniu funkcje wymagane dla usług IIS, **dołączyć narzędzia do zarządzania** jest zaznaczone, a następnie kliknij przycisk **Dodaj funkcje**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="a9dc5-146">Po zamknięciu hello wyskakującego, kliknij przycisk **dalej** hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Zrzut ekranu przedstawiający wyskakujących tooconfirm Dodawanie roli IIS hello](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="a9dc5-148">Na stronie funkcji powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="a9dc5-149">Na powitania **roli Serwer sieci Web (IIS)** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="a9dc5-150">Na powitania **usług ról** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="a9dc5-151">Na powitania **potwierdzenie** kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="a9dc5-152">Po zakończeniu instalacji powitania kliknij **Zamknij** na powitania Kreatora.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="a9dc5-153">Otwieranie portu 80</span><span class="sxs-lookup"><span data-stu-id="a9dc5-153">Open port 80</span></span>
<span data-ttu-id="a9dc5-154">Aby tooaccept Twojego wirtualna ruchu przychodzącego ruchu za pośrednictwem portu 80, należy tooadd reguły dla ruchu przychodzącego toohello sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="a9dc5-155">Otwórz hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9dc5-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9dc5-156">W **maszyn wirtualnych** wybierz hello maszyny Wirtualnej, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="a9dc5-157">W ustawieniach maszyny wirtualnej hello, wybierz **interfejsy sieciowe** , a następnie wybierz hello istniejącego interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Zrzut ekranu przedstawiający hello maszyny wirtualnej ustawienie hello interfejsy sieciowe](./media/hero-role/network-interface.png)
4. <span data-ttu-id="a9dc5-159">W **Essentials** hello interfejsu sieciowego, kliknij przycisk hello **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Zrzut ekranu przedstawiający sekcji podstawowe elementy hello hello interfejsu sieciowego](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="a9dc5-161">W hello **Essentials** bloku hello NSG, powinien mieć jeden domyślny istniejącej reguły dla ruchu przychodzącego **domyślny — Zezwalaj rdp** co pozwala toolog w toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="a9dc5-162">Należy dodać innego ruchu IIS tooallow reguły dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="a9dc5-163">Kliknij pozycję **Inbound security rule** (Reguła zabezpieczeń ruchu przychodzącego).</span><span class="sxs-lookup"><span data-stu-id="a9dc5-163">Click **Inbound security rule**.</span></span>
   
    ![Zrzut ekranu przedstawiający sekcji Essentials hello hello NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="a9dc5-165">W obszarze **Inbound security rules** (Reguły zabezpieczeń ruchu przychodzącego) kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Zrzut ekranu przedstawiający tooadd przycisk hello regułę zabezpieczeń](./media/hero-role/add-rule.png)
7. <span data-ttu-id="a9dc5-167">W obszarze **Inbound security rules** (Reguły zabezpieczeń ruchu przychodzącego) kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="a9dc5-168">Typ **80** w hello zakres portów i upewnij się, że **Zezwalaj** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="a9dc5-169">Gdy skończysz, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-169">When you are done, click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający tooadd przycisk hello regułę zabezpieczeń](./media/hero-role/port-80.png)

<span data-ttu-id="a9dc5-171">Aby uzyskać więcej informacji na temat grup NSG, reguły ruchu przychodzącego i wychodzącego, zobacz [Zezwalaj dostępu zewnętrznego tooyour maszynę Wirtualną przy użyciu hello portalu Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a9dc5-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="a9dc5-172">Połącz toohello domyślna usług IIS witryna sieci Web</span><span class="sxs-lookup"><span data-stu-id="a9dc5-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="a9dc5-173">W portalu Azure hello, kliknij przycisk **maszyn wirtualnych** , a następnie wybierz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="a9dc5-174">W hello **Essentials** bloku, kopia programu **publicznego adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Zrzut ekranu pokazujący, gdzie toofind hello publicznego adresu IP maszyny Wirtualnej](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="a9dc5-176">Otwórz przeglądarkę i na pasku adresu hello, wpisz w publiczny adres IP, w następujący sposób: http://<publicIPaddress> i kliknij przycisk **Enter** toogo toothat adresu.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="a9dc5-177">Przeglądarka należy otwierać hello domyślnej strony sieci web usług IIS.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="a9dc5-178">Wygląda mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="a9dc5-178">It looks something like this:</span></span>
   
    ![Zrzut ekranu przedstawiający stronę IIS domyślne jakie hello wygląda w przeglądarce](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="a9dc5-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9dc5-180">Next steps</span></span>
* <span data-ttu-id="a9dc5-181">Poeksperymentuj z [dołączenie dysku danych](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="a9dc5-182">Dyski danych zapewniają więcej pamięci masowej dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9dc5-182">Data disks provide more storage for your virtual machine.</span></span>

