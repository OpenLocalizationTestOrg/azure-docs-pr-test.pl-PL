---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="bde27-103">Szybki Start: Dodawanie nowych tooAzure użytkowników usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="bde27-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="bde27-104">W tym artykule opisano, jak tooadd nowych użytkowników w organizacji w hello Azure Active Directory (Azure AD) jeden za pomocą portalu Azure hello lub synchronizowanie użytkownika systemu Windows Server AD lokalnego konta danych.</span><span class="sxs-lookup"><span data-stu-id="bde27-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="bde27-105">Dodaj użytkowników w chmurze</span><span class="sxs-lookup"><span data-stu-id="bde27-105">Add cloud-based users</span></span>
1. <span data-ttu-id="bde27-106">Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="bde27-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="bde27-107">Wybierz **usługi Azure Active Directory** , a następnie **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bde27-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="bde27-108">Na powitania **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bde27-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="bde27-109">![Polecenie Dodaj hello](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="bde27-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="bde27-110">Wprowadź szczegóły użytkownika hello, takich jak **nazwa** i **nazwy użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bde27-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="bde27-111">Witaj nazwy użytkownika hello część nazwy domeny muszą zostać hello początkowej domyślnej domeny nazwa "[nazwa domeny].onmicrosoft.com" lub zweryfikowane, niefederacyjnych [niestandardowej nazwy domeny](add-custom-domain.md) takich jak "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="bde27-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="bde27-112">Kopiowania lub w inny sposób hello Uwaga wygenerowane hasło użytkownika, dzięki czemu możesz podać go toohello użytkownika po zakończeniu tego procesu.</span><span class="sxs-lookup"><span data-stu-id="bde27-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="bde27-113">Opcjonalnie można otwierać i podanie informacji hello w hello **profilu** bloku, hello **grup** bloku lub hello **roli katalogu** bloku hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bde27-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="bde27-114">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bde27-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="bde27-115">Na powitania **użytkownika** bloku, wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bde27-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="bde27-116">Bezpiecznie należy rozpowszechnić hello wygenerowane hasło toohello nowego użytkownika, tak aby hello użytkownicy mogą się logować.</span><span class="sxs-lookup"><span data-stu-id="bde27-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="bde27-117">Możesz także zsynchronizować dane konto użytkownika z lokalnego systemu Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="bde27-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="bde27-118">Firmy Microsoft tożsamościach span lokalnych i chmurze możliwości tworzenia tożsamością jednego użytkownika do uwierzytelniania i autoryzacji zasobów tooall, bez względu na lokalizację.</span><span class="sxs-lookup"><span data-stu-id="bde27-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="bde27-119">Nazywamy to tożsamość hybrydowa.</span><span class="sxs-lookup"><span data-stu-id="bde27-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="bde27-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) mogą być używane toointegrate katalogów lokalnych z usługą Azure Active Directory dla scenariuszy hybrydowych tożsamości.</span><span class="sxs-lookup"><span data-stu-id="bde27-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="bde27-121">Dzięki temu tooprovide wspólną tożsamością dla użytkowników dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bde27-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="bde27-122">Usuwanie użytkowników z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde27-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="bde27-123">Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="bde27-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="bde27-124">Wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bde27-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="bde27-125">Na powitania **użytkowników i grup** bloku, wybierz hello toodelete użytkownika z listy hello.</span><span class="sxs-lookup"><span data-stu-id="bde27-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="bde27-126">W bloku hello hello wybranego użytkownika, wybierz **omówienie**, a następnie na pasku poleceń hello, wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="bde27-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="bde27-127">![Polecenie Dodaj hello](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="bde27-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="bde27-128">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="bde27-128">Learn more</span></span> 
* [<span data-ttu-id="bde27-129">Dodaj użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="bde27-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="bde27-130">Przypisz rolę użytkownika tooa w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde27-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="bde27-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bde27-131">Next steps</span></span>
<span data-ttu-id="bde27-132">W tym szybkiego startu, kiedy znasz już jak tooadd nowych użytkowników tooAzure AD — wersja Premium.</span><span class="sxs-lookup"><span data-stu-id="bde27-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="bde27-133">Możesz użyć hello poniższych łączy toocreate nowego użytkownika w usłudze Azure AD z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bde27-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bde27-134">Dodaj użytkowników tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="bde27-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
