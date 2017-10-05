---
title: "Grupy w usłudze Azure Active Directory w wersji dedykowanej | Dokumentacja firmy Microsoft"
description: "Przegląd grup jak dedykowanych działają w usłudze Azure Active Directory oraz sposób ich tworzenia."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="fb5ac-103">Grupy dedykowane w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5ac-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="fb5ac-104">W usłudze Azure Active Directory (Azure AD) funkcja grupy dedykowane automatycznie tworzy i wypełnia członkostwa w grupach usługi Azure AD, wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="fb5ac-105">Członkowie grupy dedykowane nie można dodać lub usunąć przy użyciu klasycznego portalu Azure, poleceń cmdlet programu Windows PowerShell, lub programowo.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5ac-106">Grupy dedykowane wymagają przypisania do licencji Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="fb5ac-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="fb5ac-107">Administratora zarządzającego regułą grupy</span><span class="sxs-lookup"><span data-stu-id="fb5ac-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="fb5ac-108">Wszyscy użytkownicy, którzy są wybrane przez regułę jako członek grupy</span><span class="sxs-lookup"><span data-stu-id="fb5ac-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="fb5ac-109">**Aby włączyć grupy dedykowane**</span><span class="sxs-lookup"><span data-stu-id="fb5ac-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="fb5ac-110">W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="fb5ac-111">Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz edytować.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="fb5ac-112">Wybierz **Konfiguruj** karcie, a następnie ustaw **Włącz grupy dedykowane** do **tak**.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="fb5ac-113">Po ustawieniu przełącznika włączyć grupy dedykowane **tak**, dodatkowo można włączyć w katalogu, aby automatycznie utworzyć dedykowane grupie Wszyscy użytkownicy, ustawiając **włączyć "Wszyscy użytkownicy" grupy** przełączyć się do  **Tak**.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="fb5ac-114">Następnie można również edytować nazwę tej grupy dedykowane wpisując ją **"Wszyscy użytkownicy" Nazwa wyświetlana grupy** pola.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="fb5ac-115">Grupy Wszyscy użytkownicy, można przypisać te same uprawnienia do wszystkich użytkowników w katalogu.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="fb5ac-116">Na przykład można przyznać wszystkim użytkownikom w katalogu dostęp do aplikacji SaaS, przypisując dostępu dla grupy dedykowane wszystkich użytkowników w tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="fb5ac-117">Dedykowany grupy Wszyscy użytkownicy należą wszyscy użytkownicy w katalogu, w tym gości i użytkowników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="fb5ac-118">Jeśli potrzebujesz grupy który wyklucza użytkowników zewnętrznych, a następnie można to zrobić, tworząc grupy z opartych na atrybutach dynamiczne reguły, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="fb5ac-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="fb5ac-119">Grupy, która nie obejmuje wszystkich gości należy użyć reguły podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="fb5ac-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="fb5ac-120">Aby dowiedzieć się, jak tworzyć reguły *zaawansowane* (czyli takie, które mogą zawierać więcej niż jedno porównanie) na potrzeby dynamicznego zarządzania członkostwem w grupach, zobacz [Tworzenie reguł zaawansowanych za pomocą atrybutów](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="fb5ac-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="fb5ac-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb5ac-121">Next steps</span></span>
<span data-ttu-id="fb5ac-122">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb5ac-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="fb5ac-123">Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5ac-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="fb5ac-124">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5ac-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="fb5ac-125">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb5ac-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="fb5ac-126">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5ac-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
