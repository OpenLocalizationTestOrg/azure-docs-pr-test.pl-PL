---
title: "Azure Active Directory Domain Services: Włączanie usług Azure Active Directory Domain Services | Microsoft Docs"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="6a161-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6a161-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="6a161-104">Zadanie 3. Włączanie usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="6a161-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="6a161-105">W tym zadaniu można włączyć usługi Azure Active Directory Domain Services (Azure AD DS) dla katalogu, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6a161-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="6a161-106">Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6a161-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6a161-107">W okienku po lewej stronie powitania wybierz hello **usługi Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a161-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="6a161-108">Wybierz dzierżawę usługi Azure Active Directory (Azure AD) hello (katalog) dla której ma zostać tooenable Azure usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="6a161-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="6a161-110">Na powitania **katalogu podglądu** kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="6a161-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Karta Konfigurowanie w katalogu](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="6a161-112">W obszarze **usług domenowych w usłudze**, zmień hello **włączyć usługi domenowe dla tego katalogu** opcję zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="6a161-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="6a161-113">Na stronie powitania pojawią się dodatkowe opcje konfiguracji usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a161-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Włączanie Usług domenowych](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="6a161-115">Po włączeniu usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure AD generuje i przechowuje hello protokołu Kerberos i NTLM skrótów poświadczeń wymaganych do uwierzytelniania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6a161-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="6a161-116">Określ hello **nazwy domeny DNS, usług domenowych**.</span><span class="sxs-lookup"><span data-stu-id="6a161-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="6a161-117">Domyślna nazwa domeny Hello hello katalogu (z **. onmicrosoft.com** sufiks) jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="6a161-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="6a161-118">Witaj lista zawiera wszystkie domeny, które zostały skonfigurowane dla katalogu usługi Azure AD, w tym zarówno zweryfikowane i niezweryfikowanych domen, które są konfigurowane na powitania **domen** kartę.</span><span class="sxs-lookup"><span data-stu-id="6a161-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="6a161-119">Możesz również podać niestandardową nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="6a161-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="6a161-120">W tym przykładzie hello niestandardowa nazwa domeny jest *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="6a161-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="6a161-121">Prefiks nazwy domeny określonej Hello (na przykład *contoso100* w hello *contoso100.com* nazwa domeny) musi zawierać więcej niż 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="6a161-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="6a161-122">Nie możesz utworzyć domeny usługi Azure Active Directory Domain Services z prefiksem zawierającym ponad 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="6a161-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="6a161-123">Upewnij się, tym hello domeny DNS wybrana dla hello zarządzane domeny nie istnieje już w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="6a161-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="6a161-124">W szczególności sprawdź czy toosee:</span><span class="sxs-lookup"><span data-stu-id="6a161-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="6a161-125">Masz już domenę z hello tą samą nazwą domeny DNS w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="6a161-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="6a161-126">Witaj sieć wirtualna wybrana została ma połączenie VPN z siecią lokalną i masz domenę z hello tą samą nazwą domeny DNS w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6a161-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="6a161-127">Masz istniejącą usługę w chmurze o tej nazwie na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a161-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="6a161-128">Wybierz sieć wirtualną, na którym ma być dostępna toobe usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a161-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="6a161-129">Wybierz hello sieci wirtualnej i podsieci dedykowanego utworzony w hello **toothis sieci wirtualnej z usług domenowych Connect** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="6a161-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="6a161-130">Należy również rozważyć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6a161-130">Also consider hello following:</span></span>

   * <span data-ttu-id="6a161-131">Upewnij się, że w tej sieci wirtualnej hello, które zostały określone należy tooan region platformy Azure, który jest obsługiwany przez usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6a161-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6a161-132">tooascertain hello regiony platformy Azure, w którym usługi Azure Active Directory Domain Services jest dostępna, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="6a161-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="6a161-133">Sieci wirtualne należące do regionu tooa których Azure Active Directory Domain Services nie jest obsługiwana nie są wyświetlane na liście rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="6a161-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="6a161-134">Użyj dedykowanych podsieci w sieci wirtualnej hello Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6a161-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6a161-135">Czy *nie* wybierz hello podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="6a161-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="6a161-136">Zobacz [zagadnienia dotyczące pracy w sieci](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="6a161-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="6a161-137">Podobnie sieci wirtualnych, które zostały utworzone przy użyciu usługi Azure Resource Manager nie są wyświetlane na liście rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="6a161-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="6a161-138">Sieci wirtualne oparte na usłudze Resource Manager nie są obecnie obsługiwane przez usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6a161-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="6a161-139">Kliknij tooenable Azure Active Directory Domain Services, w okienku zadań hello u dołu strony hello hello **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6a161-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="6a161-140">Azure Active Directory Domain Services jest włączana dla katalogu, strona hello Wyświetla stan *oczekujące*.</span><span class="sxs-lookup"><span data-stu-id="6a161-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Okno włączania usług domenowych](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="6a161-142">Usługi Azure Active Directory Domain Services oferują wysoką dostępność na potrzeby domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="6a161-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="6a161-143">Po włączeniu usług domenowych Azure Active Directory w domenie, które usługi są dostępne w sieci wirtualnej hello adresy IP hello są wyświetlane pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="6a161-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="6a161-144">Hello drugiego adresu IP jest wyświetlany wkrótce po hello najpierw, jak szybko hello usługa zapewni wysoką dostępność domeny.</span><span class="sxs-lookup"><span data-stu-id="6a161-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="6a161-145">Gdy skonfigurowano wysokiej dostępności i aktywne dla domeny, powinny być widoczne dwa adresy IP w hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="6a161-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="6a161-146">Po upływie około 20 minut too30, hello pierwszy adres IP w domenie, które usługi są dostępne w Twojej sieci wirtualnej w hello **adres IP** na powitania **Konfiguruj** strony.</span><span class="sxs-lookup"><span data-stu-id="6a161-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Okno usług domenowych wyświetlające pierwszy aprowizowany adres IP](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="6a161-148">Gdy domena oferuje działającą jest wysoka dostępność, dwa adresy IP są wyświetlane na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="6a161-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="6a161-149">Twoja domena zarządzana jest dostępna w wybranej sieci wirtualnej pod tymi dwoma adresami IP.</span><span class="sxs-lookup"><span data-stu-id="6a161-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="6a161-150">Należy zwrócić uwagę hello dwa adresy IP tak, aby umożliwić aktualizację hello ustawienia DNS dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a161-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="6a161-151">Umożliwi to maszyn wirtualnych na powitania sieci wirtualnej tooconnect toohello domeny dla operacji, takich jak przyłączanie do domeny.</span><span class="sxs-lookup"><span data-stu-id="6a161-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Okno usług domenowych wyświetlające oba aprowizowane adresy IP](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="6a161-153">W zależności od rozmiaru hello dzierżawy usługi Azure AD (na przykład hello liczba użytkowników lub grupy) domeny zarządzanej tooyour synchronizacji zajmie trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="6a161-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="6a161-154">Ten proces synchronizacji jest wykonywany w tle hello.</span><span class="sxs-lookup"><span data-stu-id="6a161-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="6a161-155">W przypadku dużych dzierżaw z dziesiątkami tysięcy obiektów może potrwać dzień lub dwa dla wszystkich użytkowników, członkostwa w grupach i poświadczeń toobe zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="6a161-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="6a161-156">Następny krok</span><span class="sxs-lookup"><span data-stu-id="6a161-156">Next step</span></span>
[<span data-ttu-id="6a161-157">Zadanie 4: aktualizowanie ustawień DNS hello hello sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6a161-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
