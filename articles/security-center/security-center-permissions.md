---
title: "aaaPermissions w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Centrum zabezpieczeń Azure używa toousers uprawnienia tooassign kontroli dostępu opartej na rolach i identyfikuje hello dozwolonych akcji dla każdej roli."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="34b1c-103">Uprawnienia w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="34b1c-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="34b1c-104">Centrum zabezpieczeń Azure używa [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md), która zapewnia [wbudowane role](../active-directory/role-based-access-built-in-roles.md) mogą być przypisane toousers, grup i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="34b1c-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="34b1c-105">Centrum zabezpieczeń ocenia konfiguracji hello problemy z zabezpieczeniami tooidentify zasobów i luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="34b1c-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="34b1c-106">W Centrum zabezpieczeń widoczne są tylko informacje dotyczące zasobów tooa po przypisaniu roli hello właściciela, współautora lub czytelnika dla grupy zasobów lub subskrypcji hello należącą do zasobu.</span><span class="sxs-lookup"><span data-stu-id="34b1c-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="34b1c-107">Dodanie ról toothese istnieją dwa określonych ról Centrum zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="34b1c-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="34b1c-108">**Czytnik zabezpieczeń**: użytkownika, który należy do roli toothis ma prawa tooSecurity Centrum przeglądania.</span><span class="sxs-lookup"><span data-stu-id="34b1c-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="34b1c-109">Użytkownik Hello można wyświetlić zalecenia, alertów, zasad zabezpieczeń i stanów zabezpieczeń, ale nie można wprowadzić zmian.</span><span class="sxs-lookup"><span data-stu-id="34b1c-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="34b1c-110">**Administrator zabezpieczeń**: użytkownika, który należy do roli toothis ma takie same prawa jako hello czytnika zabezpieczeń hello można również zaktualizować hello zasady zabezpieczeń i odrzucać alerty i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="34b1c-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="34b1c-111">role zabezpieczeń Hello, czytnika zabezpieczeń i Administrator zabezpieczeń mają dostęp tylko w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="34b1c-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="34b1c-112">role zabezpieczeń Hello nie mają dostępu tooother obszary usługi Azure, takiego jak magazyn, sieci Web i mobilnych lub Internetu rzeczy.</span><span class="sxs-lookup"><span data-stu-id="34b1c-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="34b1c-113">Role i dozwolonych akcji</span><span class="sxs-lookup"><span data-stu-id="34b1c-113">Roles and allowed actions</span></span>

<span data-ttu-id="34b1c-114">Witaj Poniższa tabela przedstawia role i dozwolonych akcji w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="34b1c-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="34b1c-115">X oznacza, że akcja hello jest dozwolona dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="34b1c-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="34b1c-116">Rola</span><span class="sxs-lookup"><span data-stu-id="34b1c-116">Role</span></span> | <span data-ttu-id="34b1c-117">Edytowanie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-117">Edit security policy</span></span> | <span data-ttu-id="34b1c-118">Zastosuj zalecenia dotyczące zabezpieczeń zasobu</span><span class="sxs-lookup"><span data-stu-id="34b1c-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="34b1c-119">Odrzucać alerty i zalecenia</span><span class="sxs-lookup"><span data-stu-id="34b1c-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="34b1c-120">Wyświetlanie alertów i zalecenia</span><span class="sxs-lookup"><span data-stu-id="34b1c-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="34b1c-121">Właściciel subskrypcji</span><span class="sxs-lookup"><span data-stu-id="34b1c-121">Subscription Owner</span></span> | <span data-ttu-id="34b1c-122">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-122">X</span></span> | <span data-ttu-id="34b1c-123">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-123">X</span></span> | <span data-ttu-id="34b1c-124">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-124">X</span></span> | <span data-ttu-id="34b1c-125">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-125">X</span></span> |
| <span data-ttu-id="34b1c-126">Współautor subskrypcji</span><span class="sxs-lookup"><span data-stu-id="34b1c-126">Subscription Contributor</span></span> | <span data-ttu-id="34b1c-127">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-127">X</span></span> | <span data-ttu-id="34b1c-128">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-128">X</span></span> | <span data-ttu-id="34b1c-129">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-129">X</span></span> | <span data-ttu-id="34b1c-130">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-130">X</span></span> |
| <span data-ttu-id="34b1c-131">Właściciel grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="34b1c-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="34b1c-132">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-132">X</span></span> | -- | <span data-ttu-id="34b1c-133">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-133">X</span></span> |
| <span data-ttu-id="34b1c-134">Współautor grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="34b1c-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="34b1c-135">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-135">X</span></span> | -- | <span data-ttu-id="34b1c-136">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-136">X</span></span> |
| <span data-ttu-id="34b1c-137">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="34b1c-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="34b1c-138">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-138">X</span></span> |
| <span data-ttu-id="34b1c-139">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-139">Security Administrator</span></span> | <span data-ttu-id="34b1c-140">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-140">X</span></span> | -- | <span data-ttu-id="34b1c-141">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-141">X</span></span> | <span data-ttu-id="34b1c-142">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-142">X</span></span> |
| <span data-ttu-id="34b1c-143">Czytnik zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="34b1c-144">X</span><span class="sxs-lookup"><span data-stu-id="34b1c-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="34b1c-145">Firma Microsoft zaleca, aby przypisać hello najbardziej ograniczająca rola potrzebne dla użytkowników toocomplete ich zadań.</span><span class="sxs-lookup"><span data-stu-id="34b1c-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="34b1c-146">Na przykład przypisać hello czytnika roli toousers tylko dowiedzieć tooview hello kondycja zabezpieczeń zasobów, ale nie podejmować działań, np. stosować zaleceń ani edytować zasad.</span><span class="sxs-lookup"><span data-stu-id="34b1c-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="34b1c-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34b1c-147">Next steps</span></span>
<span data-ttu-id="34b1c-148">W tym artykule wyjaśniono, jak Centrum zabezpieczeń używa toousers uprawnienia tooassign RBAC oraz zidentyfikować hello dozwolonych akcji dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="34b1c-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="34b1c-149">Teraz, kiedy znasz przypisań ról hello potrzebne toomonitor hello stan zabezpieczeń subskrypcji, edytować zasady zabezpieczeń i stosować zalecenia, Dowiedz się, jak:</span><span class="sxs-lookup"><span data-stu-id="34b1c-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="34b1c-150">Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="34b1c-151">Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="34b1c-152">Monitorowanie kondycji zabezpieczeń hello zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34b1c-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="34b1c-153">Zarządzanie i reagowanie na alerty toosecurity w Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="34b1c-154">Monitorowanie rozwiązań partnerskich zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="34b1c-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
