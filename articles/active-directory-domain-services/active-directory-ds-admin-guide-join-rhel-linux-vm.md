---
title: "Azure Active Directory Domain Services: Dołącz RHEL maszynę Wirtualną do domeny zarządzanej | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Red Hat Enterprise Linux do usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="95eee-103">Przyłączanie maszyny wirtualnej z systemem Red Hat Enterprise Linux 7 do domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="95eee-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="95eee-104">W tym artykule przedstawiono sposób Dołącz maszynę wirtualną Red Hat Enterprise Linux (RHEL) 7 do domeny zarządzanej usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95eee-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="95eee-105">Aprowizowanie maszyny wirtualnej Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="95eee-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="95eee-106">Wykonaj poniższe kroki, aby udostępnić maszynie wirtualnej RHEL 7 przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="95eee-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="95eee-107">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95eee-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Pulpitu nawigacyjnego portalu Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="95eee-109">Kliknij przycisk **nowy** w okienku po lewej stronie i typ **Red Hat** na pasku wyszukiwania, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="95eee-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="95eee-110">Wpisy dla Red Hat Enterprise Linux są wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="95eee-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="95eee-111">Kliknij przycisk **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="95eee-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="95eee-113">W wynikach wyszukiwania **wszystko** okienko powinny zawierać obrazu Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="95eee-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="95eee-114">Kliknij przycisk **Red Hat Enterprise Linux 7.2** Aby uzyskać więcej informacji o obrazie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="95eee-116">W **Red Hat Enterprise Linux 7.2** okienka, należy wyświetlić więcej informacji o obrazie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="95eee-117">W **wybierz model wdrożenia** listy rozwijanej wybierz **klasycznego**.</span><span class="sxs-lookup"><span data-stu-id="95eee-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="95eee-118">Następnie kliknij przycisk **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="95eee-118">Then click the **Create** button.</span></span>

    ![Wyświetlanie szczegółów obrazu](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="95eee-120">W **podstawy** strony **tworzenia maszyny wirtualnej** kreatora wprowadź **nazwy hosta** dla nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="95eee-121">Również określić nazwę użytkownika administratora lokalnego w **nazwy użytkownika** pola i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="95eee-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="95eee-122">Można również użyć klucza SSH do uwierzytelnienia użytkownika administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="95eee-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="95eee-123">Wybierz również **warstwy cenowej** dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Tworzenie maszyny Wirtualnej — podstawy strony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="95eee-125">W **rozmiar** strony **tworzenia maszyny wirtualnej** kreatora wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Tworzenie maszyny Wirtualnej — wybierz rozmiar](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="95eee-127">W **ustawienia** strony **tworzenia maszyny wirtualnej** kreatora, wybierz konto magazynu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="95eee-128">Kliknij przycisk **sieci wirtualnej** do wybrania sieci wirtualnej, do którego można wdrożyć maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="95eee-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="95eee-129">W **sieci wirtualnej** bloku, wybierz opcję sieci wirtualnej, w których usługi domenowe Azure AD jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="95eee-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="95eee-130">W tym przykładzie mamy wybierz "MyPreviewVNet" sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Tworzenie maszyny Wirtualnej — Wybieranie sieci wirtualnej](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="95eee-132">Na **Podsumowanie** strony **tworzenia maszyny wirtualnej** kreatora przejrzyj a kliknij **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="95eee-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Tworzenie maszyny Wirtualnej — wybrana sieć wirtualna](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="95eee-134">Należy zacząć wdrażania nowej maszyny wirtualnej na podstawie obrazu RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="95eee-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Tworzenie maszyny Wirtualnej — rozpoczęto wdrażanie](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="95eee-136">Po kilku minutach maszyny wirtualnej powinny zostać wdrożone pomyślnie i gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="95eee-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Tworzenie maszyny Wirtualnej — wdrożony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="95eee-138">Zdalne nawiązywanie połączenia nowo aprowizowanej maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="95eee-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="95eee-139">Maszyna wirtualna RHEL 7.2 zainicjowano na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="95eee-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="95eee-140">Następne zadanie jest zdalne nawiązywanie połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="95eee-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="95eee-141">**Połącz z maszyną wirtualną RHEL 7.2** postępuj zgodnie z instrukcjami w artykule [jak zalogować się do maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95eee-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="95eee-142">Pozostałe kroki przyjęto założenie, że używasz klienta PuTTY SSH do nawiązania połączenia z maszyną wirtualną RHEL.</span><span class="sxs-lookup"><span data-stu-id="95eee-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="95eee-143">Aby uzyskać więcej informacji, zobacz [strony pobierania programu PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="95eee-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="95eee-144">Otwórz PuTTY program.</span><span class="sxs-lookup"><span data-stu-id="95eee-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="95eee-145">Wprowadź **nazwy hosta** dla nowo utworzonego RHEL maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="95eee-146">W tym przykładzie naszych maszyna wirtualna ma nazwę hosta "contoso-rhel.cloudapp .net".</span><span class="sxs-lookup"><span data-stu-id="95eee-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="95eee-147">Jeśli nie masz pewności nazwy hosta maszyny wirtualnej, można znaleźć na pulpicie maszyny Wirtualnej w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="95eee-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![Łączenie programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="95eee-149">Zaloguj się do maszyny wirtualnej przy użyciu poświadczeń administratora lokalnego możesz określić podczas tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="95eee-150">W tym przykładzie użyliśmy konta administratora lokalnego "mahesh".</span><span class="sxs-lookup"><span data-stu-id="95eee-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![Logowania programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="95eee-152">Zainstaluj wymagane pakiety na maszynie wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="95eee-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="95eee-153">Po nawiązaniu połączenia z maszyną wirtualną, następne zadanie jest zainstalowanie pakietów wymagane do przyłączania do domeny na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="95eee-154">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="95eee-154">Perform the following steps:</span></span>

1. <span data-ttu-id="95eee-155">**Zainstaluj realmd:** pakietu realmd służy do przyłączania do domeny.</span><span class="sxs-lookup"><span data-stu-id="95eee-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="95eee-156">W terminalu PuTTY wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="95eee-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="95eee-157">sudo yum instalacji realmd</span><span class="sxs-lookup"><span data-stu-id="95eee-157">sudo yum install realmd</span></span>

    ![Zainstaluj realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="95eee-159">Po kilku minutach pakietu realmd powinny zostać zainstalowane na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="95eee-161">**Zainstaluj sssd:** pakiet realmd zależy od sssd do wykonania operacji łączenia domeny.</span><span class="sxs-lookup"><span data-stu-id="95eee-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="95eee-162">W terminalu PuTTY wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="95eee-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="95eee-163">sudo yum instalacji sssd</span><span class="sxs-lookup"><span data-stu-id="95eee-163">sudo yum install sssd</span></span>

    ![Zainstaluj sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="95eee-165">Po kilku minutach pakietu sssd powinny zostać zainstalowane na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="95eee-167">**Instalowanie protokołu kerberos:** w terminalu PuTTY, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="95eee-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="95eee-168">sudo yum instalacji stacji roboczej krb5 krb5-biblioteki</span><span class="sxs-lookup"><span data-stu-id="95eee-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalowanie protokołu kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="95eee-170">Po kilku minutach pakietu realmd powinny zostać zainstalowane na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95eee-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Protokół Kerberos jest zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="95eee-172">Dołącz maszynę wirtualną systemu Linux do domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="95eee-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="95eee-173">Teraz, wymagane pakiety są zainstalowane na maszynie wirtualnej systemu Linux, następne zadanie to można dołączyć maszyny wirtualnej do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="95eee-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="95eee-174">Wykryj domeny zarządzanej usług domenowych w usłudze AAD.</span><span class="sxs-lookup"><span data-stu-id="95eee-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="95eee-175">W terminalu PuTTY wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="95eee-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="95eee-176">obszar sudo odnajdywanie CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="95eee-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Odnajdowanie obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="95eee-178">Jeśli **odnajdowanie obszaru** nie może znaleźć domeny zarządzanej, upewnij się, że domena jest osiągalna z poziomu maszyny wirtualnej (ping spróbuj).</span><span class="sxs-lookup"><span data-stu-id="95eee-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="95eee-179">Upewnij się również maszyny wirtualnej w rzeczywistości został wdrożony do tej samej sieci wirtualnej, w których są dostępne domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="95eee-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="95eee-180">Inicjowanie protokołu kerberos.</span><span class="sxs-lookup"><span data-stu-id="95eee-180">Initialize kerberos.</span></span> <span data-ttu-id="95eee-181">W terminalu PuTTY wpisz następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="95eee-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="95eee-182">Upewnij się, że określ użytkownika, który należy do grupy "Administratorzy kontrolera domeny usługi AAD".</span><span class="sxs-lookup"><span data-stu-id="95eee-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="95eee-183">Tylko ci użytkownicy mogą dołączania komputerów do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="95eee-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="95eee-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="95eee-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="95eee-186">Zapewnienia, że należy określić nazwę domeny wielkimi literami, else kinit nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="95eee-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="95eee-187">Dołącz maszynę do domeny.</span><span class="sxs-lookup"><span data-stu-id="95eee-187">Join the machine to the domain.</span></span> <span data-ttu-id="95eee-188">W terminalu PuTTY wpisz następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="95eee-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="95eee-189">Określ tego samego użytkownika określonego w poprzednim kroku (kinit).</span><span class="sxs-lookup"><span data-stu-id="95eee-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="95eee-190">sudo obszaru sprzężenia — pełne CONTOSO100.COM -U "bob@CONTOSO100.COM"</span><span class="sxs-lookup"><span data-stu-id="95eee-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Dołącz do obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="95eee-192">Należy pobrać wiadomości ("pomyślnie zarejestrowane maszyny w obszarze") po maszyna jest pomyślnie dołączona do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="95eee-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="95eee-193">Sprawdź, przyłączanie do domeny</span><span class="sxs-lookup"><span data-stu-id="95eee-193">Verify domain join</span></span>
<span data-ttu-id="95eee-194">Można szybko sprawdzić, czy maszyna została pomyślnie dołączona do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="95eee-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="95eee-195">Połączyć się z nowo RHEL maszyny Wirtualnej przy użyciu SSH i konto użytkownika domeny, a następnie sprawdź, aby zobaczyć, czy konto użytkownika jest poprawnie rozpoznać przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="95eee-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="95eee-196">W terminalu PuTTY, wpisz następujące polecenie, aby połączyć się z nowo RHEL maszyny wirtualnej przy użyciu protokołu SSH przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="95eee-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="95eee-197">Użyj konta domeny, który należy do domeny zarządzanej (na przykład "bob@CONTOSO100.COM" w tym przypadku.)</span><span class="sxs-lookup"><span data-stu-id="95eee-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="95eee-198">SSH -l bob@CONTOSO100.COM rhel.cloudapp.net firmy contoso</span><span class="sxs-lookup"><span data-stu-id="95eee-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="95eee-199">W terminalu PuTTY wpisz następujące polecenie, aby zobaczyć, czy katalog macierzysty został poprawnie zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="95eee-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="95eee-200">pwd</span><span class="sxs-lookup"><span data-stu-id="95eee-200">pwd</span></span>
3. <span data-ttu-id="95eee-201">W terminalu PuTTY wpisz następujące polecenie, aby zobaczyć, czy członkostwa w grupach są rozpoznawane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="95eee-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="95eee-202">id</span><span class="sxs-lookup"><span data-stu-id="95eee-202">id</span></span>

<span data-ttu-id="95eee-203">Następujące przykładowe dane wyjściowe tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="95eee-203">A sample output of these commands follows:</span></span>

![Sprawdź, przyłączanie do domeny](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="95eee-205">Rozwiązywanie problemów z przyłączania do domeny</span><span class="sxs-lookup"><span data-stu-id="95eee-205">Troubleshooting domain join</span></span>
<span data-ttu-id="95eee-206">Zapoznaj się [przyłączenie do domeny Rozwiązywanie problemów](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artykułu.</span><span class="sxs-lookup"><span data-stu-id="95eee-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="95eee-207">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="95eee-207">Related Content</span></span>
* [<span data-ttu-id="95eee-208">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="95eee-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="95eee-209">Dołącz maszynę wirtualną systemu Windows Server do domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="95eee-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="95eee-210">[Jak zalogować się do maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95eee-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="95eee-211">Instalowanie protokołu Kerberos</span><span class="sxs-lookup"><span data-stu-id="95eee-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="95eee-212">Red Hat Enterprise Linux 7 — przewodnik integracji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="95eee-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
