---
title: "Domena niestandardowa tooa użytkowników aaaAssign w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toopopulate domeny niestandardowej w usłudze Azure Active Directory z kontami użytkowników."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="ce405-103">Przypisywanie użytkowników tooa niestandardową domenę</span><span class="sxs-lookup"><span data-stu-id="ce405-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="ce405-104">Po dodaniu tooAzure Twojego niestandardową domenę usługi Active Directory, należy dodać hello kont użytkowników dla tej domeny, dzięki czemu będzie można ich uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="ce405-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce405-105">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ce405-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="ce405-106">Aby uzyskać jak toomanage Twojego nazw domen w Centrum administracyjnym hello Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce405-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="ce405-107">Użytkownicy synchronizowane z katalogu lokalnego</span><span class="sxs-lookup"><span data-stu-id="ce405-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="ce405-108">Jeśli już ustawiono połączenia między lokalnymi usługi Active Directory i Azure Active Directory, synchronizacji można wypełnić hello kont.</span><span class="sxs-lookup"><span data-stu-id="ce405-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="ce405-109">Aby uzyskać więcej informacji na temat toosynchronize usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz temat [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ce405-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="ce405-110">Użytkownicy dodawane i zarządzane w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="ce405-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="ce405-111">toochange hello domeny do istniejącego konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="ce405-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="ce405-112">Otwórz hello klasycznego portalu Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce405-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="ce405-113">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="ce405-113">Open your directory.</span></span>
3. <span data-ttu-id="ce405-114">Wybierz hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce405-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="ce405-115">Wybierz hello użytkownika z listy hello.</span><span class="sxs-lookup"><span data-stu-id="ce405-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="ce405-116">Zmiana domeny hello hello użytkownika, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ce405-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="ce405-117">Można to także zrobić przy użyciu [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) lub hello [interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="ce405-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="ce405-118">Wybierz domenę niestandardową, podczas tworzenia nowego użytkownika</span><span class="sxs-lookup"><span data-stu-id="ce405-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="ce405-119">Otwórz hello klasycznego portalu Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce405-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="ce405-120">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="ce405-120">Open your directory.</span></span>
3. <span data-ttu-id="ce405-121">Wybierz hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce405-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="ce405-122">Na pasku poleceń hello, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ce405-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="ce405-123">Po dodaniu hello nazwy użytkownika z listy domeny hello należy wybrać hello domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="ce405-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="ce405-124">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ce405-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce405-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce405-125">Next steps</span></span>
* [<span data-ttu-id="ce405-126">Przy użyciu domeny niestandardowej nazwy toosimplify hello logowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="ce405-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="ce405-127">Zarządzanie niestandardowymi nazwami domen</span><span class="sxs-lookup"><span data-stu-id="ce405-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="ce405-128">Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce405-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

