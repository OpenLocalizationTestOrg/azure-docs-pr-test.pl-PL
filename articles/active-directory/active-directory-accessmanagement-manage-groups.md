---
title: "aaaManaging grup w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toocreate i Zarządzaj grupami toomanage Azure użytkowników przy użyciu usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="c2af8-103">Zarządzanie grupami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2af8-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2af8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c2af8-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="c2af8-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c2af8-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="c2af8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2af8-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="c2af8-107">Jedną z funkcji hello zarządzania użytkownika usługi Azure Active Directory (Azure AD) jest hello możliwości toocreate grup użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c2af8-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="c2af8-108">Możesz użyć zadania zarządzania tooperform grupy, takich jak przypisywanie licencji lub uprawnienia tooa liczbę użytkowników jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="c2af8-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="c2af8-109">Można również użyć grup tooassign uprawnienia do dostępu</span><span class="sxs-lookup"><span data-stu-id="c2af8-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="c2af8-110">Zasoby, takie jak obiekty w katalogu hello</span><span class="sxs-lookup"><span data-stu-id="c2af8-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="c2af8-111">Zasoby zewnętrzne toohello katalogu, takiego jak aplikacji SaaS, usług platformy Azure, witryn programu SharePoint lub zasobów lokalnych</span><span class="sxs-lookup"><span data-stu-id="c2af8-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="c2af8-112">Ponadto właściciel zasobu można również przypisywać właścicielem dostępu tooa zasobów tooan usługi Azure AD grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="c2af8-113">To przypisanie daje członkom hello zasobu toohello dostęp do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="c2af8-114">Następnie hello właściciela grupy hello zarządza członkostwo w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="c2af8-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="c2af8-115">Ostatecznie hello zasobów właściciela delegatów toohello właściciel hello grupy hello uprawnienia tooassign użytkowników tootheir zasobu.</span><span class="sxs-lookup"><span data-stu-id="c2af8-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2af8-116">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c2af8-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="c2af8-117">Aby uzyskać jak toomanage grupuje się w Centrum administracyjnym hello Azure AD, zobacz [Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2af8-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="c2af8-118">Jak utworzyć grupę?</span><span class="sxs-lookup"><span data-stu-id="c2af8-118">How do I create a group?</span></span>
<span data-ttu-id="c2af8-119">W zależności od hello toowhich usług, które zostały zasubskrybowane przez organizację można utworzyć grupę przy użyciu jednej z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="c2af8-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="c2af8-120">Witaj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c2af8-120">hello Azure classic portal</span></span>
* <span data-ttu-id="c2af8-121">portal konta Hello usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="c2af8-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="c2af8-122">Witaj w portalu konta Windows Intune</span><span class="sxs-lookup"><span data-stu-id="c2af8-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="c2af8-123">Opiszemy zadania, jak wykonywać w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c2af8-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="c2af8-124">Aby uzyskać więcej informacji o użyciu portali innych niż Azure toomanage katalogu usługi Azure AD, zobacz [administrowanie katalogiem usługi Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="c2af8-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="c2af8-125">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="c2af8-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="c2af8-126">Wybierz hello **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="c2af8-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="c2af8-127">Wybierz polecenie **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="c2af8-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="c2af8-128">W hello **Dodaj grupę** okna, określ nazwę hello i hello opis grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="c2af8-129">Jak dodawać i usuwać pojedynczych użytkowników w grupie zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="c2af8-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="c2af8-130">**tooadd grupy tooa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="c2af8-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="c2af8-131">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="c2af8-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="c2af8-132">Wybierz hello **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="c2af8-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="c2af8-133">Otwórz toowhich grupy hello tooadd członkowie.</span><span class="sxs-lookup"><span data-stu-id="c2af8-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="c2af8-134">Otwórz hello **członków** kartę hello wybrane grupy, jeśli go jeszcze nie wyświetlanie.</span><span class="sxs-lookup"><span data-stu-id="c2af8-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="c2af8-135">Wybierz polecenie **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="c2af8-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="c2af8-136">Na powitania **Dodaj członków** strony, wybierz opcję hello nazwę hello użytkownik lub grupa ma tooadd członkiem tej grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="c2af8-137">Upewnij się, że nazwa została dodana toohello **wybrane** okienka.</span><span class="sxs-lookup"><span data-stu-id="c2af8-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="c2af8-138">**tooremove użytkownika z grupy**</span><span class="sxs-lookup"><span data-stu-id="c2af8-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="c2af8-139">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="c2af8-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="c2af8-140">Wybierz hello **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="c2af8-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="c2af8-141">Otwórz grupę hello, z którego mają być członkami tooremove.</span><span class="sxs-lookup"><span data-stu-id="c2af8-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="c2af8-142">Wybierz hello **członków** kartę, wybierz hello nazwę elementu członkowskiego hello mają tooremove z tej grupy, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="c2af8-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="c2af8-143">Potwierdzenie w wierszu hello tooremove tego elementu członkowskiego z grupy hello.</span><span class="sxs-lookup"><span data-stu-id="c2af8-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="c2af8-144">Jak dynamicznie zarządzać hello członkostwa w grupie?</span><span class="sxs-lookup"><span data-stu-id="c2af8-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="c2af8-145">W usłudze Azure AD można bardzo łatwo skonfigurować toodetermine Prosta reguła, użytkowników, którzy są członkami toobe hello grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="c2af8-146">Prosta reguła to taka, która wykonuje tylko jedno porównanie.</span><span class="sxs-lookup"><span data-stu-id="c2af8-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="c2af8-147">Na przykład jeśli grupa jest przypisana tooa aplikacji SaaS, można ustawić reguły użytkowników tooadd, mających stanowisko "Przedstawiciel".</span><span class="sxs-lookup"><span data-stu-id="c2af8-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="c2af8-148">Ta reguła jest następnie udziela dostępu użytkowników tooall aplikacji SaaS toothis stanowisko w katalogu.</span><span class="sxs-lookup"><span data-stu-id="c2af8-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="c2af8-149">Gdy atrybuty zmian użytkownika, powitalne system ocenia wszystkie reguły grupy dynamicznej w toosee katalogu, jeśli zmiany atrybutu hello hello użytkownika spowoduje wywołanie żadnej grupy dodaje lub usuwa.</span><span class="sxs-lookup"><span data-stu-id="c2af8-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="c2af8-150">Jeśli użytkownika spełnia zasady grupy, są dodawane jako członek grupy toothat.</span><span class="sxs-lookup"><span data-stu-id="c2af8-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="c2af8-151">Jeśli nie spełniają hello zasady grupy, które są członkami, są usuwane jako elementy członkowskie z tej grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="c2af8-152">Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="c2af8-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="c2af8-153">Członkostwo grup zagnieżdżonych nie są obecnie obsługiwane dla tooapplications przypisywania na podstawie grupy.</span><span class="sxs-lookup"><span data-stu-id="c2af8-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="c2af8-154">Dynamiczne zarządzanie członkostwem w grupach wymaga toobe licencji Azure AD Premium, przypisane do</span><span class="sxs-lookup"><span data-stu-id="c2af8-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="c2af8-155">Witaj administratora, który zarządza hello regułą grupy</span><span class="sxs-lookup"><span data-stu-id="c2af8-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="c2af8-156">Wszyscy członkowie grupy hello</span><span class="sxs-lookup"><span data-stu-id="c2af8-156">All members of hello group</span></span>
>
>

<span data-ttu-id="c2af8-157">**tooenable członkostwo dynamiczne w grupie**</span><span class="sxs-lookup"><span data-stu-id="c2af8-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="c2af8-158">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="c2af8-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="c2af8-159">Wybierz hello **grup** kartę i hello Otwórz grupę tooedit.</span><span class="sxs-lookup"><span data-stu-id="c2af8-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="c2af8-160">Wybierz hello **Konfiguruj** karcie, a następnie ustaw **Włącz członkostwo dynamiczne** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="c2af8-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="c2af8-161">Skonfiguruj prostą regułę dla toocontrol grupy hello członkostwo dynamiczne w grupie.</span><span class="sxs-lookup"><span data-stu-id="c2af8-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="c2af8-162">Upewnij się, że hello **dodawania użytkowników gdzie** opcja jest zaznaczona, a następnie wybierz właściwość użytkownika z listy hello (na przykład dział, stanowisko, itp.),</span><span class="sxs-lookup"><span data-stu-id="c2af8-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="c2af8-163">Następnie wybierz warunek (Nie równa się, Równa się, Nie rozpoczyna się od, Rozpoczyna się od, Nie zawiera, Zawiera, Nie jest zgodne, Jest zgodne).</span><span class="sxs-lookup"><span data-stu-id="c2af8-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="c2af8-164">Określ wartość porównania hello wybrane właściwości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2af8-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="c2af8-165">toolearn o tym, jak toocreate *zaawansowane* reguły (zasady, które mogą zawierać więcej niż jedno porównanie) na dynamiczne członkostwo w grupie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c2af8-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="c2af8-166">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="c2af8-166">Additional information</span></span>
<span data-ttu-id="c2af8-167">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2af8-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c2af8-168">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2af8-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c2af8-169">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="c2af8-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="c2af8-170">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2af8-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c2af8-171">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2af8-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c2af8-172">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2af8-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
