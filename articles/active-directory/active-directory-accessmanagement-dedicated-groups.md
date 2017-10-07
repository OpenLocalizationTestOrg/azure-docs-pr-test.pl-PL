---
title: "aaaDedicated grup w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="863e1-103">Grupy dedykowane w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="863e1-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="863e1-104">W usłudze Azure Active Directory (Azure AD) funkcja grupy dedykowane hello automatycznie tworzy i wypełnia członkostwa w grupach usługi Azure AD, wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="863e1-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="863e1-105">Nie można dodać członków grupy dedykowane lub usuniętych za pomocą hello klasycznym portalu, programu Windows PowerShell polecenia cmdlet systemu Azure, lub programowo.</span><span class="sxs-lookup"><span data-stu-id="863e1-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="863e1-106">Grupy dedykowane wymagają przypisania do licencji Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="863e1-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="863e1-107">Witaj administratora, który zarządza hello regułą grupy</span><span class="sxs-lookup"><span data-stu-id="863e1-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="863e1-108">Wszyscy użytkownicy, którzy na podstawie hello reguły toobe hello grupy</span><span class="sxs-lookup"><span data-stu-id="863e1-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="863e1-109">**grupy tooenable w wersji dedykowanej**</span><span class="sxs-lookup"><span data-stu-id="863e1-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="863e1-110">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="863e1-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="863e1-111">Wybierz hello **grup** kartę, a następnie otwórz hello grupę tooedit.</span><span class="sxs-lookup"><span data-stu-id="863e1-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="863e1-112">Wybierz hello **Konfiguruj** karcie, a następnie ustaw **Włącz grupy dedykowane** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="863e1-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="863e1-113">Po ustawieniu hello przełącznika włączyć grupy dedykowane zbyt**tak**, dodatkowo można włączyć tooautomatically katalogu hello Tworzenie grupy dedykowane wszyscy użytkownicy hello przez ustawienie hello **włączyć "Wszyscy użytkownicy" grupy** Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="863e1-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="863e1-114">Następnie można również edytować hello nazwę tej grupy dedykowane przez wpisanie jej w hello **"Wszyscy użytkownicy" Nazwa wyświetlana grupy** pola.</span><span class="sxs-lookup"><span data-stu-id="863e1-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="863e1-115">Witaj grupy Wszyscy użytkownicy mogą służyć tooassign hello tych samych uprawnień tooall hello użytkowników w katalogu.</span><span class="sxs-lookup"><span data-stu-id="863e1-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="863e1-116">Na przykład można przyznać wszyscy użytkownicy w Twojej tooa dostępu do katalogu aplikacji SaaS, przypisując dostępu dla wszystkich użytkowników grupy dedykowane toothis aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="863e1-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="863e1-117">Witaj w wersji dedykowanej wszystkich użytkowników grupy należą wszyscy użytkownicy w katalogu hello, w tym gości i użytkowników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="863e1-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="863e1-118">Jeśli potrzebujesz grupy który wyklucza użytkowników zewnętrznych, a następnie można to zrobić, tworząc grupy z opartych na atrybutach dynamiczne reguły, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="863e1-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="863e1-119">Grupy, która nie obejmuje wszystkich gości należy użyć reguły, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="863e1-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="863e1-120">toolearn o tym, jak toocreate *zaawansowane* reguły (zasady, które mogą zawierać więcej niż jedno porównanie) na dynamiczne członkostwo w grupie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="863e1-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="863e1-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="863e1-121">Next steps</span></span>
<span data-ttu-id="863e1-122">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="863e1-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="863e1-123">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="863e1-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="863e1-124">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="863e1-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="863e1-125">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="863e1-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="863e1-126">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="863e1-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
