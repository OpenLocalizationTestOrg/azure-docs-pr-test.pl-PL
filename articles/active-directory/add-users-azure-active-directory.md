---
title: "Dodawanie nowych użytkowników do usługi Azure Active Directory | Microsoft Docs"
description: "Opisano sposób dodawania nowych użytkowników w usłudze Azure Active Directory."
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
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="e6aab-103">Szybki Start: Dodawanie nowych użytkowników do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6aab-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="e6aab-104">W tym artykule opisano sposób dodawania nowych użytkowników w organizacji w usłudze Azure Active Directory (Azure AD) za pomocą portalu Azure lub przez synchronizację danych konta użytkownika systemu Windows Server AD lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="e6aab-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="e6aab-105">Dodaj użytkowników w chmurze</span><span class="sxs-lookup"><span data-stu-id="e6aab-105">Add cloud-based users</span></span>
1. <span data-ttu-id="e6aab-106">Zaloguj się do [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="e6aab-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e6aab-107">Wybierz **usługi Azure Active Directory** , a następnie **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="e6aab-108">Na **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="e6aab-109">![Dodaj polecenie](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="e6aab-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="e6aab-110">Wprowadź szczegóły użytkownika, takich jak **nazwa** i **nazwy użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="e6aab-111">Część nazwy domeny nazwa użytkownika musi być początkowej domyślnej domeny nazwa "[nazwa domeny].onmicrosoft.com" lub zweryfikowane, niefederacyjnych [niestandardowej nazwy domeny](add-custom-domain.md) takich jak "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="e6aab-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="e6aab-112">Skopiuj lub w przeciwnym razie należy pamiętać wygenerowane hasło, dzięki czemu można udostępnić go użytkownikowi po zakończeniu tego procesu.</span><span class="sxs-lookup"><span data-stu-id="e6aab-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="e6aab-113">Opcjonalnie można otwierać i Wypełnij informacje w **profilu** bloku **grup** bloku lub **roli katalogu** bloku dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6aab-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="e6aab-114">Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e6aab-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="e6aab-115">Na **użytkownika** bloku, wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="e6aab-116">Bezpiecznie dystrybucji wygenerowane hasło dla nowego użytkownika, dzięki czemu użytkownicy mogą się logować.</span><span class="sxs-lookup"><span data-stu-id="e6aab-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="e6aab-117">Możesz także zsynchronizować dane konto użytkownika z lokalnego systemu Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="e6aab-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="e6aab-118">Firmy Microsoft tożsamościach span lokalnych i chmurze możliwości tworzenia tożsamością jednego użytkownika do uwierzytelniania i autoryzacji do wszystkich zasobów, niezależnie od lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e6aab-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="e6aab-119">Nazywamy to tożsamość hybrydowa.</span><span class="sxs-lookup"><span data-stu-id="e6aab-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="e6aab-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) może służyć do integracji katalogów lokalnych z usługą Azure Active Directory dla scenariuszy hybrydowych tożsamości.</span><span class="sxs-lookup"><span data-stu-id="e6aab-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="e6aab-121">Dzięki temu użytkownicy mogą posługiwać się wspólną tożsamością dla usługi Office 365, platformy Azure i aplikacji SaaS zintegrowanych z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6aab-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="e6aab-122">Usuwanie użytkowników z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6aab-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="e6aab-123">Zaloguj się do [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="e6aab-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e6aab-124">Wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="e6aab-125">Na **użytkowników i grup** bloku, wybierz użytkownika, aby usunąć z listy.</span><span class="sxs-lookup"><span data-stu-id="e6aab-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="e6aab-126">W bloku dla wybranego użytkownika, wybierz **omówienie**, a następnie na pasku poleceń Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="e6aab-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="e6aab-127">![Dodaj polecenie](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="e6aab-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="e6aab-128">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="e6aab-128">Learn more</span></span> 
* [<span data-ttu-id="e6aab-129">Dodaj użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="e6aab-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="e6aab-130">Przypisanie użytkownika do roli w usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6aab-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="e6aab-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6aab-131">Next steps</span></span>
<span data-ttu-id="e6aab-132">W tym szybkiego startu kiedy znasz już sposób dodawania nowych użytkowników do usługi Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="e6aab-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="e6aab-133">Poniższe łącze służy do tworzenia nowego użytkownika w usłudze Azure AD z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6aab-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6aab-134">Dodawanie użytkowników do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6aab-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 