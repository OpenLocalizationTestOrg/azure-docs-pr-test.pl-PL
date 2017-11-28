---
title: "Zarządzanie grupami w usłudze Azure Active Directory | Microsoft Docs"
description: "Jak tworzyć grupy i zarządzać nimi, aby zarządzać użytkownikami platformy Azure przy użyciu usługi Azure Active Directory."
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
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="099d0-103">Zarządzanie grupami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="099d0-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="099d0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="099d0-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="099d0-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="099d0-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="099d0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="099d0-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="099d0-107">Jedną z funkcji zarządzania użytkownikami w usłudze Azure Active Directory (Azure AD) jest tworzenie grup użytkowników.</span><span class="sxs-lookup"><span data-stu-id="099d0-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="099d0-108">Grupa służy do wykonywania zadań zarządzania, takich jak przypisywanie licencji lub uprawnień do kilku użytkowników jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="099d0-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="099d0-109">Za pomocą grup można także przypisywać uprawnienia dostępu do:</span><span class="sxs-lookup"><span data-stu-id="099d0-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="099d0-110">zasobów takich jak obiekty w katalogu</span><span class="sxs-lookup"><span data-stu-id="099d0-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="099d0-111">Zasobów spoza katalogu, na przykład aplikacji SaaS, usług platformy Azure, witryn programu SharePoint lub zasobów lokalnych</span><span class="sxs-lookup"><span data-stu-id="099d0-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="099d0-112">Ponadto właściciel zasobu może także przypisać dostęp do tego zasobu do grupy usługi Azure AD należącej do innej osoby.</span><span class="sxs-lookup"><span data-stu-id="099d0-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="099d0-113">To przypisanie spowoduje przydzielenie dostępu do zasobu członkom tej grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="099d0-114">Następnie właściciel grupy może zarządzać członkostwem w grupie.</span><span class="sxs-lookup"><span data-stu-id="099d0-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="099d0-115">Zatem w praktyce właściciel zasobu przekazuje właścicielowi grupy uprawnienie do przypisywania użytkowników do swojego zasobu.</span><span class="sxs-lookup"><span data-stu-id="099d0-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="099d0-116">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="099d0-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="099d0-117">Aby dowiedzieć się, jak zarządzać grupami w centrum administracyjnym usługi Azure AD, zobacz [Create a group and add members in Azure Active Directory (Tworzenie grupy i dodawanie elementów członkowskich w usłudze Azure Active Directory)](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="099d0-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="099d0-118">Jak utworzyć grupę?</span><span class="sxs-lookup"><span data-stu-id="099d0-118">How do I create a group?</span></span>
<span data-ttu-id="099d0-119">W zależności od usług, które subskrybuje Twoja organizacja, możesz utworzyć grupę w jednym z następujących miejsc:</span><span class="sxs-lookup"><span data-stu-id="099d0-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="099d0-120">Klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="099d0-120">the Azure classic portal</span></span>
* <span data-ttu-id="099d0-121">Portal konta usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="099d0-121">the Office 365 account portal</span></span>
* <span data-ttu-id="099d0-122">Portal konta usługi Windows Intune</span><span class="sxs-lookup"><span data-stu-id="099d0-122">the Windows Intune account portal</span></span>

<span data-ttu-id="099d0-123">Zadania opiszemy w taki sposób, jakby były wykonywane w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="099d0-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="099d0-124">Aby uzyskać więcej informacji na temat zarządzania katalogiem Azure AD przy użyciu portali innych niż Azure, zobacz [Administrowanie katalogiem usługi Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="099d0-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="099d0-125">W [klasycznym portalu Azure](https://manage.windowsazure.com) wybierz pozycję **Active Directory**, a następnie wybierz nazwę katalogu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="099d0-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="099d0-126">Wybierz kartę **Grupy**.</span><span class="sxs-lookup"><span data-stu-id="099d0-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="099d0-127">Wybierz polecenie **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="099d0-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="099d0-128">W oknie **Dodawanie grupy** podaj nazwę i opis grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="099d0-129">Jak dodawać i usuwać pojedynczych użytkowników w grupie zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="099d0-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="099d0-130">**Aby dodać użytkownika do grupy**</span><span class="sxs-lookup"><span data-stu-id="099d0-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="099d0-131">W [klasycznym portalu Azure](https://manage.windowsazure.com) wybierz pozycję **Active Directory**, a następnie wybierz nazwę katalogu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="099d0-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="099d0-132">Wybierz kartę **Grupy**.</span><span class="sxs-lookup"><span data-stu-id="099d0-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="099d0-133">Otwórz grupę, do której chcesz dodać członków.</span><span class="sxs-lookup"><span data-stu-id="099d0-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="099d0-134">Otwórz kartę **Członkowie** wybranej grupy, jeśli nie jest jeszcze wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="099d0-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="099d0-135">Wybierz polecenie **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="099d0-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="099d0-136">Na stronie **Dodawanie członków** wybierz nazwę użytkownika, którego chcesz dodać jako członka grupy, lub nazwę grupy takich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="099d0-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="099d0-137">Upewnij się, że nazwa została dodana do okienka **Wybrane**.</span><span class="sxs-lookup"><span data-stu-id="099d0-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="099d0-138">**Aby usunąć użytkownika z grupy**</span><span class="sxs-lookup"><span data-stu-id="099d0-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="099d0-139">W [klasycznym portalu Azure](https://manage.windowsazure.com) wybierz pozycję **Active Directory**, a następnie wybierz nazwę katalogu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="099d0-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="099d0-140">Wybierz kartę **Grupy**.</span><span class="sxs-lookup"><span data-stu-id="099d0-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="099d0-141">Otwórz grupę, z której chcesz usunąć członków.</span><span class="sxs-lookup"><span data-stu-id="099d0-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="099d0-142">Wybierz kartę **Członkowie**, wybierz nazwę członka, którego chcesz usunąć z grupy, a następnie kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="099d0-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="099d0-143">Po wyświetleniu monitu potwierdź, że chcesz usunąć tego członka z grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="099d0-144">Jak dynamicznie zarządzać członkostwem w grupie?</span><span class="sxs-lookup"><span data-stu-id="099d0-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="099d0-145">W usłudze Azure AD można bardzo łatwo skonfigurować prostą regułę w celu określenia, którzy użytkownicy powinni być członkami grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="099d0-146">Prosta reguła to taka, która wykonuje tylko jedno porównanie.</span><span class="sxs-lookup"><span data-stu-id="099d0-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="099d0-147">Jeśli na przykład grupa jest przypisana do aplikacji SaaS, możesz skonfigurować regułę dodającą użytkowników, którzy mają stanowisko „Przedstawiciel handlowy”.</span><span class="sxs-lookup"><span data-stu-id="099d0-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="099d0-148">Następnie ta reguła udziela dostępu do tej aplikacji SaaS wszystkim użytkownikom mającym to stanowisko w katalogu.</span><span class="sxs-lookup"><span data-stu-id="099d0-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="099d0-149">Po zmianie dowolnych atrybutów użytkownika system ocenia wszystkie zasady dotyczące grup dynamicznych w katalogu, aby ustalić, czy zmiana atrybutów użytkownika spowoduje dodanie elementów do grupy lub usunięcie ich z niej.</span><span class="sxs-lookup"><span data-stu-id="099d0-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="099d0-150">Jeśli użytkownik spełnia wymagania zasad grupy, jest dodawany jako członek do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="099d0-151">Jeśli użytkownicy nie spełniają już zasad grupy, której są członkami, są usuwani z tej grupy.</span><span class="sxs-lookup"><span data-stu-id="099d0-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="099d0-152">Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="099d0-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="099d0-153">Aktualnie w ramach przypisywania do aplikacji na podstawie grup nie jest obsługiwane członkostwo w grupach zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="099d0-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="099d0-154">Dynamiczne zarządzanie członkostwem w grupach wymaga przypisania licencji usługi Azure AD w wersji Premium do:</span><span class="sxs-lookup"><span data-stu-id="099d0-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="099d0-155">administratora zarządzającego regułą grupy</span><span class="sxs-lookup"><span data-stu-id="099d0-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="099d0-156">Wszyscy członkowie grupy</span><span class="sxs-lookup"><span data-stu-id="099d0-156">All members of the group</span></span>
>
>

<span data-ttu-id="099d0-157">**Aby włączyć dynamiczne zarządzanie członkostwem w grupie**</span><span class="sxs-lookup"><span data-stu-id="099d0-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="099d0-158">W [klasycznym portalu Azure](https://manage.windowsazure.com) wybierz pozycję **Active Directory**, a następnie wybierz nazwę katalogu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="099d0-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="099d0-159">Wybierz kartę **Grupy** i otwórz grupę, którą chcesz edytować.</span><span class="sxs-lookup"><span data-stu-id="099d0-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="099d0-160">Wybierz kartę **Konfiguracja**, a następnie wybierz ustawienie **Tak** dla opcji **Włącz członkostwo dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="099d0-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="099d0-161">Skonfiguruj prostą regułę grupy, aby sterować sposobem działania członkostwa dynamicznego w grupie.</span><span class="sxs-lookup"><span data-stu-id="099d0-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="099d0-162">Upewnij się, że jest zaznaczona opcja **Dodaj użytkowników, dla których**, a następnie wybierz właściwość użytkownika z listy (na przykład dział, stanowisko itp.).</span><span class="sxs-lookup"><span data-stu-id="099d0-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="099d0-163">Następnie wybierz warunek (Nie równa się, Równa się, Nie rozpoczyna się od, Rozpoczyna się od, Nie zawiera, Zawiera, Nie jest zgodne, Jest zgodne).</span><span class="sxs-lookup"><span data-stu-id="099d0-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="099d0-164">Podaj wartość porównania wybranej właściwości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="099d0-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="099d0-165">Aby dowiedzieć się, jak tworzyć reguły *zaawansowane* (czyli takie, które mogą zawierać więcej niż jedno porównanie) na potrzeby dynamicznego zarządzania członkostwem w grupach, zobacz [Tworzenie reguł zaawansowanych za pomocą atrybutów](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="099d0-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="099d0-166">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="099d0-166">Additional information</span></span>
<span data-ttu-id="099d0-167">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="099d0-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="099d0-168">Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="099d0-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="099d0-169">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="099d0-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="099d0-170">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="099d0-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="099d0-171">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="099d0-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="099d0-172">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="099d0-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
