---
title: "Azure Active Directory Domain Services: Przyłącz do domeny zarządzanej tooa wirtualna RHEL | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Red Hat Enterprise Linux usług domenowych w usłudze tooAzure AD"
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
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="06ed1-103">Dołącz do domeny zarządzanej tooa Red Hat Enterprise Linux 7 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="06ed1-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="06ed1-104">W tym artykule opisano sposób toojoin Red Hat Enterprise Linux (RHEL) 7 tooan maszyny wirtualnej usługi domenowe Azure AD zarządzania domeny.</span><span class="sxs-lookup"><span data-stu-id="06ed1-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="06ed1-105">Aprowizowanie maszyny wirtualnej Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="06ed1-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="06ed1-106">Wykonaj hello następującej maszyny wirtualnej tooprovision systemów RHEL 7 czynności przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="06ed1-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="06ed1-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06ed1-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Pulpitu nawigacyjnego portalu Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="06ed1-109">Kliknij przycisk **nowy** na powitania lewe okienko i typ **Red Hat** na pasku wyszukiwania hello pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="06ed1-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="06ed1-110">Wpisy dla Red Hat Enterprise Linux są wyświetlane w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="06ed1-111">Kliknij przycisk **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="06ed1-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="06ed1-113">wyniki wyszukiwania Hello w hello **wszystko** okienko powinny zawierać obraz powitania Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="06ed1-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="06ed1-114">Kliknij przycisk **Red Hat Enterprise Linux 7.2** tooview więcej informacji na temat hello obraz maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="06ed1-116">W hello **Red Hat Enterprise Linux 7.2** okienku powinien zostać wyświetlony więcej informacji na temat hello obraz maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="06ed1-117">W hello **wybierz model wdrożenia** listy rozwijanej wybierz **klasycznego**.</span><span class="sxs-lookup"><span data-stu-id="06ed1-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="06ed1-118">Następnie kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="06ed1-118">Then click hello **Create** button.</span></span>

    ![Wyświetlanie szczegółów obrazu](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="06ed1-120">W hello **podstawy** strony hello **tworzenia maszyny wirtualnej** kreatora wprowadź hello **nazwy hosta** hello nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="06ed1-121">Również określić nazwę użytkownika administratora lokalnego w hello **nazwy użytkownika** pola i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="06ed1-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="06ed1-122">Można również wybrać toouse użytkownik lokalny administrator hello tooauthenticate klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="06ed1-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="06ed1-123">Wybierz również **warstwy cenowej** hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Tworzenie maszyny Wirtualnej — podstawy strony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="06ed1-125">W hello **rozmiar** strony hello **tworzenia maszyny wirtualnej** hello kreatora, wybierz rozmiar maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Tworzenie maszyny Wirtualnej — wybierz rozmiar](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="06ed1-127">W hello **ustawienia** strony hello **tworzenia maszyny wirtualnej** hello kreatora, wybierz konto magazynu dla maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="06ed1-128">Kliknij przycisk **sieci wirtualnej** tooselect hello sieci wirtualnej toowhich hello maszyny Wirtualnej systemu Linux powinny zostać wdrożone.</span><span class="sxs-lookup"><span data-stu-id="06ed1-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="06ed1-129">W hello **sieci wirtualnej** bloku, wybierz hello sieci wirtualnej, w których są dostępne usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06ed1-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="06ed1-130">W tym przykładzie mamy wybierz sieć wirtualną "MyPreviewVNet" hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Tworzenie maszyny Wirtualnej — Wybieranie sieci wirtualnej](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="06ed1-132">Na powitania **Podsumowanie** strony hello **tworzenia maszyny wirtualnej** hello kreatora przejrzyj a kliknij **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="06ed1-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Tworzenie maszyny Wirtualnej — wybrana sieć wirtualna](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="06ed1-134">Należy zacząć wdrożenia hello nowej maszyny wirtualnej na podstawie obrazu hello RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="06ed1-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Tworzenie maszyny Wirtualnej — rozpoczęto wdrażanie](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="06ed1-136">Po kilku minutach hello maszyny wirtualnej należy pomyślnie wdrożone i gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="06ed1-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Tworzenie maszyny Wirtualnej — wdrożony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="06ed1-138">Nawiązanie połączenia zdalnego maszyny wirtualnej systemu Linux toohello nowo udostępnione</span><span class="sxs-lookup"><span data-stu-id="06ed1-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="06ed1-139">maszyny wirtualnej Hello RHEL 7.2 zainicjowano na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="06ed1-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="06ed1-140">następne zadanie Hello jest tooconnect zdalnie toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="06ed1-141">**Podłącz maszynę wirtualną toohello RHEL 7.2** hello instrukcjami w artykule hello [jak toolog na tooa maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06ed1-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="06ed1-142">Witaj pozostałe kroki hello przyjęto założenie, że używasz hello PuTTY SSH klienta tooconnect toohello RHEL maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="06ed1-143">Aby uzyskać więcej informacji, zobacz hello [strony pobierania programu PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="06ed1-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="06ed1-144">Otwórz hello PuTTY program.</span><span class="sxs-lookup"><span data-stu-id="06ed1-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="06ed1-145">Wprowadź hello **nazwy hosta** dla hello nowo utworzony RHEL maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="06ed1-146">W tym przykładzie naszych maszyna wirtualna ma hello nazwy hosta "contoso-rhel.cloudapp .net".</span><span class="sxs-lookup"><span data-stu-id="06ed1-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="06ed1-147">Jeśli nie masz pewności hello nazwy hosta maszyny Wirtualnej, można znaleźć pulpitu nawigacyjnego wirtualna toohello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="06ed1-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Łączenie programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="06ed1-149">Zaloguj się na maszynie wirtualnej toohello przy użyciu poświadczeń administratora lokalnego hello określone podczas tworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="06ed1-150">W tym przykładzie użyliśmy konta administratora lokalnego hello "mahesh".</span><span class="sxs-lookup"><span data-stu-id="06ed1-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Logowania programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="06ed1-152">Zainstaluj wymagane pakiety na maszynie wirtualnej systemu Linux hello</span><span class="sxs-lookup"><span data-stu-id="06ed1-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="06ed1-153">Po łączącego toohello maszyny wirtualnej hello następne zadanie jest wymagane do przyłączania do domeny na maszynie wirtualnej hello pakiety tooinstall.</span><span class="sxs-lookup"><span data-stu-id="06ed1-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="06ed1-154">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="06ed1-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="06ed1-155">**Zainstaluj realmd:** pakietu realmd hello jest używany do przyłączania do domeny.</span><span class="sxs-lookup"><span data-stu-id="06ed1-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="06ed1-156">W terminalu PuTTY wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="06ed1-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="06ed1-157">sudo yum instalacji realmd</span><span class="sxs-lookup"><span data-stu-id="06ed1-157">sudo yum install realmd</span></span>

    ![Zainstaluj realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="06ed1-159">Po kilku minutach hello realmd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="06ed1-161">**Zainstaluj sssd:** hello realmd pakiet jest zależny od operacji łączenia domeny tooperform sssd.</span><span class="sxs-lookup"><span data-stu-id="06ed1-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="06ed1-162">W terminalu PuTTY wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="06ed1-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="06ed1-163">sudo yum instalacji sssd</span><span class="sxs-lookup"><span data-stu-id="06ed1-163">sudo yum install sssd</span></span>

    ![Zainstaluj sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="06ed1-165">Po kilku minutach hello sssd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="06ed1-167">**Instalowanie protokołu kerberos:** w terminalu PuTTY wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="06ed1-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="06ed1-168">sudo yum instalacji stacji roboczej krb5 krb5-biblioteki</span><span class="sxs-lookup"><span data-stu-id="06ed1-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalowanie protokołu kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="06ed1-170">Po kilku minutach hello realmd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Protokół Kerberos jest zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="06ed1-172">Dołącz do domeny zarządzanej toohello maszyny wirtualnej systemu Linux hello</span><span class="sxs-lookup"><span data-stu-id="06ed1-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="06ed1-173">Obecnie pakiety hello wymagane są zainstalowane na maszynie wirtualnej systemu Linux hello, następne zadanie hello jest domeny zarządzanej toohello toojoin hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="06ed1-174">Wykryj domeny zarządzanej usług domenowych w usłudze AAD hello.</span><span class="sxs-lookup"><span data-stu-id="06ed1-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="06ed1-175">W terminalu PuTTY wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="06ed1-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="06ed1-176">obszar sudo odnajdywanie CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="06ed1-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Odnajdowanie obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="06ed1-178">Jeśli **odnajdowanie obszaru** jest toofind domeny zarządzanej, upewnij się, ta domena hello jest dostępny z maszyny wirtualnej hello (ping spróbuj).</span><span class="sxs-lookup"><span data-stu-id="06ed1-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="06ed1-179">Upewnij się również hello maszyny wirtualnej w rzeczywistości został wdrożony toohello tej samej sieci wirtualnej, w których hello domeny zarządzanej jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="06ed1-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="06ed1-180">Inicjowanie protokołu kerberos.</span><span class="sxs-lookup"><span data-stu-id="06ed1-180">Initialize kerberos.</span></span> <span data-ttu-id="06ed1-181">W terminalu PuTTY wpisz hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="06ed1-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="06ed1-182">Upewnij się, że podajesz użytkownik, który należy toohello "AAD kontrolera domeny" Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="06ed1-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="06ed1-183">Tylko ci użytkownicy można przyłączyć do domeny zarządzanej toohello komputerów.</span><span class="sxs-lookup"><span data-stu-id="06ed1-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="06ed1-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="06ed1-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="06ed1-186">Upewnij się, że Określ nazwę domeny hello wielkimi literami, else kinit nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="06ed1-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="06ed1-187">Dołącz hello maszyny toohello domeny.</span><span class="sxs-lookup"><span data-stu-id="06ed1-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="06ed1-188">W terminalu PuTTY wpisz hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="06ed1-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="06ed1-189">Określ hello tego samego użytkownika określonego w hello poprzedzających krok (kinit).</span><span class="sxs-lookup"><span data-stu-id="06ed1-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="06ed1-190">sudo obszaru sprzężenia — pełne CONTOSO100.COM -U "bob@CONTOSO100.COM"</span><span class="sxs-lookup"><span data-stu-id="06ed1-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Dołącz do obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="06ed1-192">Należy pobrać wiadomości ("pomyślnie zarejestrowane maszyny w obszarze") gdy komputer hello jest toohello pomyślnie przyłączone do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="06ed1-193">Sprawdź, przyłączanie do domeny</span><span class="sxs-lookup"><span data-stu-id="06ed1-193">Verify domain join</span></span>
<span data-ttu-id="06ed1-194">Można szybko sprawdzić, czy maszyna hello została toohello pomyślnie przyłączone do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="06ed1-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="06ed1-195">Połącz toohello nowo RHEL maszyny Wirtualnej przy użyciu SSH i konto użytkownika domeny, a następnie toosee wyboru, jeśli konto użytkownika hello jest poprawnie rozpoznać przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="06ed1-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="06ed1-196">W terminalu, PuTTY hello typu następujące polecenia tooconnect toohello nowo przyłączone do domeny RHEL maszyny wirtualnej przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="06ed1-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="06ed1-197">Użycie konta domeny należącego do domeny zarządzanej toohello (na przykład "bob@CONTOSO100.COM" w tym przypadku.)</span><span class="sxs-lookup"><span data-stu-id="06ed1-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="06ed1-198">SSH -l bob@CONTOSO100.COM rhel.cloudapp.net firmy contoso</span><span class="sxs-lookup"><span data-stu-id="06ed1-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="06ed1-199">W terminalu PuTTY wpisz powitania po toosee polecenia w katalogu macierzystego hello został poprawnie zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="06ed1-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="06ed1-200">pwd</span><span class="sxs-lookup"><span data-stu-id="06ed1-200">pwd</span></span>
3. <span data-ttu-id="06ed1-201">W terminalu PuTTY wpisz powitania po toosee polecenia członkostwa w grupach hello są rozpoznawane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="06ed1-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="06ed1-202">id</span><span class="sxs-lookup"><span data-stu-id="06ed1-202">id</span></span>

<span data-ttu-id="06ed1-203">Następujące przykładowe dane wyjściowe tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="06ed1-203">A sample output of these commands follows:</span></span>

![Sprawdź, przyłączanie do domeny](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="06ed1-205">Rozwiązywanie problemów z przyłączania do domeny</span><span class="sxs-lookup"><span data-stu-id="06ed1-205">Troubleshooting domain join</span></span>
<span data-ttu-id="06ed1-206">Zobacz toohello [przyłączenie do domeny Rozwiązywanie problemów](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artykułu.</span><span class="sxs-lookup"><span data-stu-id="06ed1-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="06ed1-207">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="06ed1-207">Related Content</span></span>
* [<span data-ttu-id="06ed1-208">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="06ed1-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="06ed1-209">Przyłączanie się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny</span><span class="sxs-lookup"><span data-stu-id="06ed1-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="06ed1-210">[Jak toolog na tooa maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06ed1-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="06ed1-211">Instalowanie protokołu Kerberos</span><span class="sxs-lookup"><span data-stu-id="06ed1-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="06ed1-212">Red Hat Enterprise Linux 7 — przewodnik integracji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="06ed1-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
