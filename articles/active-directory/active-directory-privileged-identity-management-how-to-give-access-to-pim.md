---
title: "aaaHow toogive dostępu tooPrivileged Identity Management - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd toousers ról z hello rozszerzenia usługi Azure Active Directory Privileged Identity Management, którymi zarządzają usługi PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="2beb8-103">Nadanie toomanage dostępu do usługi Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2beb8-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2beb8-104">dostęp tooPIM Hello administrator globalny, który automatycznie włącza Azure AD Privileged Identity Management (PIM) dla organizacji oraz uzyskać przypisań ról.</span><span class="sxs-lookup"><span data-stu-id="2beb8-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="2beb8-105">Nikt pobiera zapisu domyślnie, łącznie z innych administratorów globalnych.</span><span class="sxs-lookup"><span data-stu-id="2beb8-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="2beb8-106">Inne globalne Administratorzy, administratorów zabezpieczeń i czytników zabezpieczeń mają dostęp tylko do odczytu tooAzure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="2beb8-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="2beb8-107">toogive tooPIM dostępu, hello pierwszego użytkownika można przypisywać innym użytkownikom toohello **administrator ról uprzywilejowanych** roli.</span><span class="sxs-lookup"><span data-stu-id="2beb8-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="2beb8-108">Ten przydział musi być wykonywane za pomocą programu PIM się i nie można zmienić za pomocą programu PowerShell lub innych portalach.</span><span class="sxs-lookup"><span data-stu-id="2beb8-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="2beb8-109">Zarządzanie programem Azure AD PIM wymaga usługi Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="2beb8-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="2beb8-110">Ponieważ konta Microsoft nie można zarejestrować dla usługi Azure MFA, użytkownik, który zaloguje się za pomocą konta Microsoft nie może uzyskać dostępu usługi Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="2beb8-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="2beb8-111">Upewnij się, zawsze istnieją co najmniej dwóch użytkowników należących do roli administrator ról uprzywilejowanych w przypadku, gdy jeden użytkownik jest zablokowany lub ich konto zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="2beb8-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="2beb8-112">Nadaj innego toomanage dostępu użytkownika PIM</span><span class="sxs-lookup"><span data-stu-id="2beb8-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="2beb8-113">Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz hello **Azure AD Privileged Identity Management** aplikacji hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2beb8-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="2beb8-114">Wybierz **Zarządzanie ról uprzywilejowanych** > **administrator ról uprzywilejowanych** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2beb8-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Dodawanie ról uprzywilejowanych administratorów — zrzut ekranu][1]
3. <span data-ttu-id="2beb8-116">W bloku użytkowników zarządzanych Dodaj hello krok 1 została już ukończona.</span><span class="sxs-lookup"><span data-stu-id="2beb8-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="2beb8-117">Zaznacz krok 2, **Wybierz użytkowników** i wyszukiwania dla użytkownika hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="2beb8-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Wybierz użytkowników — zrzut ekranu][2]
4. <span data-ttu-id="2beb8-119">Wybierz użytkownika hello z hello wyniki wyszukiwania, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="2beb8-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="2beb8-120">Kliknij przycisk **OK** toosave wybór.</span><span class="sxs-lookup"><span data-stu-id="2beb8-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="2beb8-121">Hello użytkownika, który wybrano będzie wyświetlana na liście hello ról uprzywilejowanych administratorów.</span><span class="sxs-lookup"><span data-stu-id="2beb8-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="2beb8-122">Gdy przypisujesz nowy toosomeone roli one są automatycznie konfigurowane jako rola hello tooactivate kwalifikujących się.</span><span class="sxs-lookup"><span data-stu-id="2beb8-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="2beb8-123">Jeśli chcesz, aby toomake ich stałe w roli powitania kliknij użytkownika hello na liście hello.</span><span class="sxs-lookup"><span data-stu-id="2beb8-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="2beb8-124">Wybierz **upewnij uprawnienie** hello użytkownika informacje menu.</span><span class="sxs-lookup"><span data-stu-id="2beb8-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="2beb8-125">Wyślij łącze użytkownika hello zbyt[wprowadzenie do korzystania z usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2beb8-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="2beb8-126">Usuwanie praw dostępu przez innego użytkownika do zarządzania usługi PIM</span><span class="sxs-lookup"><span data-stu-id="2beb8-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="2beb8-127">Zawsze przed usunięciem ktoś z hello administratorem ról uprzywilejowanych, upewnij się, nadal będą przypisanych tooit dwóch użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2beb8-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="2beb8-128">Na pulpicie nawigacyjnym usługi PIM hello, kliknij na powitania roli **administrator ról uprzywilejowanych**.</span><span class="sxs-lookup"><span data-stu-id="2beb8-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="2beb8-129">zostanie wyświetlona lista Hello użytkowników obecnie w tej roli.</span><span class="sxs-lookup"><span data-stu-id="2beb8-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="2beb8-130">Polecenie hello użytkownika na liście użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="2beb8-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="2beb8-131">Polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="2beb8-131">Click on **Remove**.</span></span>  <span data-ttu-id="2beb8-132">Otrzymasz komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="2beb8-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="2beb8-133">Kliknij przycisk **tak** tooremove hello użytkownika z roli hello.</span><span class="sxs-lookup"><span data-stu-id="2beb8-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="2beb8-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2beb8-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
