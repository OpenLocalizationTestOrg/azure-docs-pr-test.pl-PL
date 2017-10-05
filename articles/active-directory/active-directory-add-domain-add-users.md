---
title: "Przypisywanie użytkowników do domeny niestandardowej w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Sposób wypełniania domeny niestandardowej w usłudze Azure Active Directory z kontami użytkowników."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="09faa-103">Przypisywanie użytkowników do domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="09faa-103">Assign users to a custom domain</span></span>
<span data-ttu-id="09faa-104">Po dodaniu domeny niestandardowej do usługi Azure Active Directory, należy dodać konta użytkowników dla tej domeny, dzięki czemu będzie można ich uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="09faa-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09faa-105">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="09faa-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="09faa-106">Jak zarządzać nazwy domeny w Centrum administracyjnym usługi Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09faa-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="09faa-107">Użytkownicy synchronizowane z katalogu lokalnego</span><span class="sxs-lookup"><span data-stu-id="09faa-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="09faa-108">Jeśli już ustawiono połączenia między lokalnymi usługi Active Directory i Azure Active Directory, synchronizacji można wypełnić kont.</span><span class="sxs-lookup"><span data-stu-id="09faa-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="09faa-109">Aby uzyskać więcej informacji na temat sposobu synchronizacji usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="09faa-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="09faa-110">Użytkownicy dodawane i zarządzane w chmurze</span><span class="sxs-lookup"><span data-stu-id="09faa-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="09faa-111">Aby zmienić domenę do istniejącego konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="09faa-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="09faa-112">Otwórz klasyczny portal Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09faa-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="09faa-113">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="09faa-113">Open your directory.</span></span>
3. <span data-ttu-id="09faa-114">Wybierz kartę **Użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="09faa-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="09faa-115">Wybierz użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="09faa-115">Select the user from the list.</span></span>
5. <span data-ttu-id="09faa-116">Zmiana domeny użytkownika, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="09faa-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="09faa-117">Można to także zrobić przy użyciu [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) lub [interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="09faa-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="09faa-118">Wybierz domenę niestandardową, podczas tworzenia nowego użytkownika</span><span class="sxs-lookup"><span data-stu-id="09faa-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="09faa-119">Otwórz klasyczny portal Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09faa-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="09faa-120">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="09faa-120">Open your directory.</span></span>
3. <span data-ttu-id="09faa-121">Wybierz kartę **Użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="09faa-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="09faa-122">Na pasku poleceń Wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="09faa-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="09faa-123">Po dodaniu nazwy użytkownika, wybierz domenę niestandardową z listy domen.</span><span class="sxs-lookup"><span data-stu-id="09faa-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="09faa-124">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="09faa-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09faa-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09faa-125">Next steps</span></span>
* [<span data-ttu-id="09faa-126">Aby uprościć proces logowania użytkowników przy użyciu niestandardowych nazw domen</span><span class="sxs-lookup"><span data-stu-id="09faa-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="09faa-127">Zarządzanie niestandardowymi nazwami domen</span><span class="sxs-lookup"><span data-stu-id="09faa-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="09faa-128">Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="09faa-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

