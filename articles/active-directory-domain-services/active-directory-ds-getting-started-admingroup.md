---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="1697f-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="1697f-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="1697f-104">Zadanie 3: Konfigurowanie grupy administracyjnej</span><span class="sxs-lookup"><span data-stu-id="1697f-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="1697f-105">W tym zadaniu konfiguracji grupy administracyjnej tworzenia w katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1697f-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="1697f-106">Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*.</span><span class="sxs-lookup"><span data-stu-id="1697f-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="1697f-107">Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny toohello domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="1697f-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="1697f-108">Na komputerach przyłączonych do domeny ta grupa jest dodawana toohello grupy Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="1697f-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="1697f-109">Ponadto Członkowie tej grupy można użyć maszyny zdalnie przyłączonych toodomain tooconnect pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="1697f-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="1697f-110">Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa hello domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="1697f-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="1697f-111">W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę hello i nie będą dostępne toousers w ramach dzierżawy hello.</span><span class="sxs-lookup"><span data-stu-id="1697f-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="1697f-112">Można jednak użyć hello specjalnej grupy administracyjne utworzone w tej konfiguracji tooperform zadań niektóre czynności uprzywilejowane.</span><span class="sxs-lookup"><span data-stu-id="1697f-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="1697f-113">Tych operacji zalicza się dołączenie komputerów domeny toohello, należącego do grupy administracyjnej toohello na komputerach przyłączonych do domeny i konfigurowania zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="1697f-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="1697f-114">Witaj Kreator automatycznie tworzy grupy administracyjnej hello w katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1697f-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="1697f-115">Ta grupa jest nazywany "Administratorzy usługi AAD kontrolera domeny".</span><span class="sxs-lookup"><span data-stu-id="1697f-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="1697f-116">Jeśli istnieje już grupa o tej nazwie w katalogu usługi Azure AD, Kreator hello wybiera tej grupy.</span><span class="sxs-lookup"><span data-stu-id="1697f-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="1697f-117">Można skonfigurować przy użyciu hello członkostwa w grupie **grupy administratorów** strony kreatora.</span><span class="sxs-lookup"><span data-stu-id="1697f-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="1697f-118">członkostwo w grupie tooconfigure, kliknij przycisk **Administratorzy kontrolera domeny usługi AAD**.</span><span class="sxs-lookup"><span data-stu-id="1697f-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Konfigurowanie członkostwa w grupie](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="1697f-120">Kliknij przycisk hello **dodawać członków** przycisk tooadd użytkowników z grupy administrator toohello katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1697f-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="1697f-121">Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **Podsumowanie** hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="1697f-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="1697f-122">Na powitania **Podsumowanie** hello kreatora przejrzyj ustawienia konfiguracji hello hello domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="1697f-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="1697f-123">Możesz wrócić krok tooany hello kreatora toomake zmian, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1697f-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="1697f-124">Gdy wszystko będzie gotowe, kliknij przycisk **OK** toocreate hello nowego zarządzanego domeny.</span><span class="sxs-lookup"><span data-stu-id="1697f-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Podsumowanie](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="1697f-126">Zostanie wyświetlone powiadomienie, że pokazuje hello postęp wdrażania usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1697f-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="1697f-127">Kliknij powiadomienie hello toosee szczegółowe postępu hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1697f-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Powiadomienie — wdrożenie w toku](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="1697f-129">Zapewnij domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="1697f-129">Provision your managed domain</span></span>
<span data-ttu-id="1697f-130">Proces inicjowania obsługi administracyjnej domeny zarządzanej Hello może potrwać godzinę tooan.</span><span class="sxs-lookup"><span data-stu-id="1697f-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="1697f-131">Podczas wdrożenia jest w toku, możesz wyszukać frazę "usługi domeny" w hello **wyszukiwania zasobów** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1697f-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="1697f-132">Wybierz **usług domenowych Azure AD** z hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1697f-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="1697f-133">Witaj **usług domenowych Azure AD** bloku wymieniono hello domeny zarządzanej, która jest inicjowana.</span><span class="sxs-lookup"><span data-stu-id="1697f-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="1697f-135">Kliknij nazwę hello toosee domeny (na przykład "contoso100.com") hello zarządzane więcej szczegółów na temat hello domeny.</span><span class="sxs-lookup"><span data-stu-id="1697f-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="1697f-137">Witaj **omówienie** karcie są wyświetlane tej domeny hello jest aktualnie aprowizowany.</span><span class="sxs-lookup"><span data-stu-id="1697f-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="1697f-138">Nie można skonfigurować hello domeny zarządzanej, dopóki nie jest w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="1697f-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="1697f-139">Może potrwać godzinę tooan Twojego toobe domeny zarządzanej, w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="1697f-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="1697f-140">Usługi domenowe — karta Przegląd podczas hello stan inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="1697f-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="1697f-141">Gdy domeny zarządzanej hello jest w pełni zaaprowizowanym, hello **omówienie** karta przedstawia stan domen hello jako **systemem**.</span><span class="sxs-lookup"><span data-stu-id="1697f-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="1697f-143">Na powitania **właściwości** kartę, zobacz dwa adresy IP, w której domeny są dostępne dla sieci wirtualnej hello kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="1697f-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Usługi domenowe — karta właściwości po w pełni zaaprowizowanym](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="1697f-145">Następny krok</span><span class="sxs-lookup"><span data-stu-id="1697f-145">Next step</span></span>
[<span data-ttu-id="1697f-146">Zadanie 4: aktualizowanie ustawień DNS hello hello sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1697f-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
