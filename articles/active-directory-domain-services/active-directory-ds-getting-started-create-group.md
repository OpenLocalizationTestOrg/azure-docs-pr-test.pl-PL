---
title: "Azure Active Directory Domain Services: Utwórz grupę Administratorzy DC hello Azure AD | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="6221f-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6221f-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="6221f-104">W tym artykule opisano i przedstawiono hello zadania konfiguracyjne, które są wymagane dla Ciebie tooenable Azure usług domenowych Active Directory (Azure AD DS) dla dzierżawy usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6221f-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="6221f-105">[**Zamiast tego spróbuj nowe środowisko portalu hello Azure (wersja zapoznawcza)**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6221f-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="6221f-106">Zadanie 1: Tworzenie grupy Administratorzy DC hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6221f-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="6221f-107">pierwszym zadaniem Hello jest toocreate grupy administracyjnej w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6221f-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="6221f-108">Nosi nazwę tej grupy administracyjnej specjalne *Administratorzy kontrolera domeny usługi AAD*.</span><span class="sxs-lookup"><span data-stu-id="6221f-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="6221f-109">Członkowie tej grupy są przyznawane uprawnienia administracyjne na komputerach, które są przyłączone do domeny toohello zarządzanych usług domenowych Azure Active Directory domeny.</span><span class="sxs-lookup"><span data-stu-id="6221f-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="6221f-110">Na komputerach przyłączonych do domeny ta grupa jest dodawana toohello grupy Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="6221f-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="6221f-111">Ponadto Członkowie tej grupy można użyć maszyny zdalnie przyłączonych toodomain tooconnect pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6221f-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="6221f-112">Nie masz uprawnienia administratora domeny lub administratora przedsiębiorstwa hello domeny zarządzanej, który został utworzony za pomocą usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6221f-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6221f-113">W domenach zarządzanych te uprawnienia są zastrzeżone przez usługę hello i nie będą dostępne toousers w ramach dzierżawy hello.</span><span class="sxs-lookup"><span data-stu-id="6221f-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="6221f-114">Można jednak użyć hello specjalnej grupy administracyjne utworzone w tej konfiguracji tooperform zadań niektóre czynności uprzywilejowane.</span><span class="sxs-lookup"><span data-stu-id="6221f-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="6221f-115">Tych operacji zalicza się dołączenie komputerów domeny toohello, należącego do grupy administracyjnej toohello na komputerach przyłączonych do domeny i konfigurowania zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="6221f-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="6221f-116">W tym zadaniu konfiguracji tworzenia grupy administracyjnej hello i Dodaj jeden lub więcej użytkowników w grupie toohello katalogu.</span><span class="sxs-lookup"><span data-stu-id="6221f-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="6221f-117">toocreate hello grupy administracyjnej dla usługi Azure Active Directory Domain Services, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6221f-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="6221f-118">Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6221f-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6221f-119">W okienku po lewej stronie powitania wybierz hello **usługi Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6221f-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="6221f-120">Wybierz hello dzierżawy usługi Azure AD (katalog) dla której ma zostać tooenable Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6221f-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6221f-121">Można utworzyć tylko jedną domenę dla każdego katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6221f-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Wybierz katalog usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="6221f-123">Na powitania **katalogu podglądu** kliknij przycisk hello **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="6221f-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="6221f-124">Kliknij grupę dzierżawcy tooyour usługi Azure AD, w okienku zadań hello u dołu okna hello hello tooadd **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="6221f-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![przycisk Dodaj grupę Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="6221f-126">W hello **Dodaj grupę** okna dialogowego Utwórz grupę o nazwie **Administratorzy kontrolera domeny usługi AAD**, a następnie ustaw **typ grupy** za**zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="6221f-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="6221f-127">tooenable dostępu w swojej domenie zarządzanych usług domenowych Azure Active Directory, utworzyć grupę o tej nazwie dokładne.</span><span class="sxs-lookup"><span data-stu-id="6221f-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![okno dialogowe Dodawanie grupy Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="6221f-129">W hello **opis** wprowadź opis, który umożliwia innym toounderstand, że ta grupa przyznaje uprawnienia administracyjne w ramach usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6221f-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="6221f-130">Po utworzeniu grupy powitania kliknij tooview Nazwa grupy hello jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="6221f-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="6221f-131">tooadd użytkowników jako członków grupy hello u dołu okna hello powitania kliknij hello **Dodaj członków** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6221f-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Dodawanie przycisku członków grupy](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="6221f-133">W hello **dodawać członków** okno dialogowe hello Wybierz użytkowników, którzy powinny być członkami tej grupy, a następnie kliknij ikonę znacznika wyboru hello na powitania prawy dolny.</span><span class="sxs-lookup"><span data-stu-id="6221f-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Dodaj grupę tooadministrators użytkowników](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="6221f-135">Następny krok</span><span class="sxs-lookup"><span data-stu-id="6221f-135">Next step</span></span>
[<span data-ttu-id="6221f-136">Zadanie 2: Tworzenie lub Wybieranie sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6221f-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
