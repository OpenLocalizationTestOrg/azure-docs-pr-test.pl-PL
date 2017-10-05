---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)"
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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="a8e58-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a8e58-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="a8e58-104">Zadanie 3: Konfigurowanie grupy administracyjnej</span><span class="sxs-lookup"><span data-stu-id="a8e58-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="a8e58-105">W tym zadaniu konfiguracji grupy administracyjnej tworzenia w katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e58-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="a8e58-106">Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*.</span><span class="sxs-lookup"><span data-stu-id="a8e58-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="a8e58-107">Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="a8e58-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="a8e58-108">Na komputerach przyłączonych do domeny ta grupa jest dodawane do grupy Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="a8e58-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="a8e58-109">Ponadto Członkowie tej grupy służy pulpitu zdalnego do łączności zdalnej dla komputerów przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="a8e58-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="a8e58-110">Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a8e58-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="a8e58-111">W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę i nie są udostępniane użytkownikom w ramach dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="a8e58-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="a8e58-112">Jednak można użyć specjalnej grupy administracyjne utworzone w ramach tego zadania konfiguracji można wykonać pewne operacje uprzywilejowane.</span><span class="sxs-lookup"><span data-stu-id="a8e58-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="a8e58-113">Tych operacji zalicza się przyłączanie komputerów do domeny, należą do tej grupy administracyjnej na komputerach przyłączonych do domeny i konfigurowania zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="a8e58-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="a8e58-114">Kreator automatycznie tworzy grupy administracyjnej w katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e58-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="a8e58-115">Ta grupa jest nazywany "Administratorzy usługi AAD kontrolera domeny".</span><span class="sxs-lookup"><span data-stu-id="a8e58-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="a8e58-116">Jeśli istnieje już grupa o tej nazwie w katalogu usługi Azure AD, Kreator wybierze tej grupy.</span><span class="sxs-lookup"><span data-stu-id="a8e58-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="a8e58-117">Można skonfigurować przy użyciu członkostwa w grupie **grupy administratorów** strony kreatora.</span><span class="sxs-lookup"><span data-stu-id="a8e58-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="a8e58-118">Kliknij, aby skonfigurować członkostwo w grupie **Administratorzy kontrolera domeny usługi AAD**.</span><span class="sxs-lookup"><span data-stu-id="a8e58-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Konfigurowanie członkostwa w grupie](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="a8e58-120">Kliknij przycisk **dodawać członków** przycisk, aby dodać użytkowników z katalogu usługi Azure AD do grupy administratorów.</span><span class="sxs-lookup"><span data-stu-id="a8e58-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="a8e58-121">Gdy wszystko będzie gotowe, kliknij przycisk **OK** można przenieść do **Podsumowanie** stronie kreatora.</span><span class="sxs-lookup"><span data-stu-id="a8e58-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="a8e58-122">Na **Podsumowanie** strony kreatora należy przejrzeć ustawienia konfiguracji dla domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="a8e58-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="a8e58-123">Można przejść wstecz do dowolnego kroku kreatora, aby wprowadzić zmiany, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a8e58-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="a8e58-124">Gdy wszystko będzie gotowe, kliknij przycisk **OK** do utworzenia nowej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="a8e58-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Podsumowanie](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="a8e58-126">Zostanie wyświetlone powiadomienie, że będzie wyświetlany postęp wdrażania usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e58-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="a8e58-127">Kliknij powiadomienie, aby wyświetlić szczegółowe informacje o postępie dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a8e58-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Powiadomienie — wdrożenie w toku](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="a8e58-129">Zapewnij domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="a8e58-129">Provision your managed domain</span></span>
<span data-ttu-id="a8e58-130">Proces inicjowania obsługi administracyjnej domeny zarządzanej może potrwać do godziny.</span><span class="sxs-lookup"><span data-stu-id="a8e58-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="a8e58-131">Gdy wdrożenie jest w toku, możesz wyszukać "usługi domeny", w **wyszukiwania zasobów** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a8e58-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="a8e58-132">Wybierz **usług domenowych Azure AD** z wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a8e58-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="a8e58-133">**Usług domenowych Azure AD** bloku wymieniono domeny zarządzanej, która jest inicjowana.</span><span class="sxs-lookup"><span data-stu-id="a8e58-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="a8e58-135">Kliknij nazwę domeny zarządzanej (na przykład "contoso100.com"), aby zobaczyć więcej szczegółów dotyczących domeny.</span><span class="sxs-lookup"><span data-stu-id="a8e58-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="a8e58-137">**Omówienie** kartę pokazuje, że domena jest aktualnie aprowizowany.</span><span class="sxs-lookup"><span data-stu-id="a8e58-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="a8e58-138">Nie można skonfigurować domeny zarządzanej, dopóki nie jest w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="a8e58-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="a8e58-139">Może potrwać do godziny dla domeny zarządzanej być w pełni obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="a8e58-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="a8e58-140">Usługi domenowe — karta Przegląd w stanie inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="a8e58-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="a8e58-141">Gdy domeny zarządzanej jest w pełni zaaprowizowanym, **omówienie** stan wyświetlany na karcie domeny jako **systemem**.</span><span class="sxs-lookup"><span data-stu-id="a8e58-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="a8e58-143">Na **właściwości** kartę, zobacz dwa adresy IP, w której domeny kontrolery są dostępne dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e58-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Usługi domenowe — karta właściwości po w pełni zaaprowizowanym](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="a8e58-145">Następny krok</span><span class="sxs-lookup"><span data-stu-id="a8e58-145">Next step</span></span>
[<span data-ttu-id="a8e58-146">Zadanie 4. Aktualizowanie ustawień usługi DNS dla sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a8e58-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
