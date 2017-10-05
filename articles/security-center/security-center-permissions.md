---
title: "Uprawnienia w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Centrum zabezpieczeń Azure używa kontroli dostępu opartej na rolach, aby przypisać uprawnienia dla użytkowników i identyfikuje akcje dozwolone dla każdej roli."
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
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="618fe-103">Uprawnienia w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="618fe-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="618fe-104">Centrum zabezpieczeń Azure używa [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md), która zapewnia [wbudowane role](../active-directory/role-based-access-built-in-roles.md), które można przypisać do użytkowników, grup i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="618fe-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="618fe-105">Centrum zabezpieczeń ocenia konfiguracji zasobów, aby zidentyfikować problemy z zabezpieczeniami i luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="618fe-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="618fe-106">W Centrum zabezpieczeń widoczne są tylko informacje związane z zasobem, jeśli przypisano rolę właściciela, współautora lub czytelnika subskrypcji lub grupy zasobów, do której należy zasób.</span><span class="sxs-lookup"><span data-stu-id="618fe-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="618fe-107">Oprócz tych ról istnieją dwie określone role usługi Security Center:</span><span class="sxs-lookup"><span data-stu-id="618fe-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="618fe-108">**Czytnik zabezpieczeń**: użytkownika, który należy do tej roli ma uprawnienia do Centrum zabezpieczeń przeglądania.</span><span class="sxs-lookup"><span data-stu-id="618fe-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="618fe-109">Użytkownika można wyświetlić zalecenia, alertów, zasad zabezpieczeń i stanów zabezpieczeń, ale nie można wprowadzić zmian.</span><span class="sxs-lookup"><span data-stu-id="618fe-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="618fe-110">**Administrator zabezpieczeń**: użytkownika, który należy do tej roli ma te same prawa odczytu zabezpieczeń może aktualizować zasady zabezpieczeń oraz odrzucać alerty i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="618fe-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="618fe-111">Role zabezpieczeń, czytnika zabezpieczeń i Administrator zabezpieczeń mają dostęp tylko w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="618fe-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="618fe-112">Role zabezpieczeń nie mają dostępu do innych obszarów usługi Azure, takiego jak magazyn, sieci Web i mobilnych lub Internetu rzeczy.</span><span class="sxs-lookup"><span data-stu-id="618fe-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="618fe-113">Role i dozwolonych akcji</span><span class="sxs-lookup"><span data-stu-id="618fe-113">Roles and allowed actions</span></span>

<span data-ttu-id="618fe-114">Poniższa tabela przedstawia role i dozwolonych akcji w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="618fe-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="618fe-115">X oznacza, że akcja jest dozwolony dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="618fe-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="618fe-116">Rola</span><span class="sxs-lookup"><span data-stu-id="618fe-116">Role</span></span> | <span data-ttu-id="618fe-117">Edytowanie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-117">Edit security policy</span></span> | <span data-ttu-id="618fe-118">Zastosuj zalecenia dotyczące zabezpieczeń zasobu</span><span class="sxs-lookup"><span data-stu-id="618fe-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="618fe-119">Odrzucać alerty i zalecenia</span><span class="sxs-lookup"><span data-stu-id="618fe-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="618fe-120">Wyświetlanie alertów i zalecenia</span><span class="sxs-lookup"><span data-stu-id="618fe-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="618fe-121">Właściciel subskrypcji</span><span class="sxs-lookup"><span data-stu-id="618fe-121">Subscription Owner</span></span> | <span data-ttu-id="618fe-122">X</span><span class="sxs-lookup"><span data-stu-id="618fe-122">X</span></span> | <span data-ttu-id="618fe-123">X</span><span class="sxs-lookup"><span data-stu-id="618fe-123">X</span></span> | <span data-ttu-id="618fe-124">X</span><span class="sxs-lookup"><span data-stu-id="618fe-124">X</span></span> | <span data-ttu-id="618fe-125">X</span><span class="sxs-lookup"><span data-stu-id="618fe-125">X</span></span> |
| <span data-ttu-id="618fe-126">Współautor subskrypcji</span><span class="sxs-lookup"><span data-stu-id="618fe-126">Subscription Contributor</span></span> | <span data-ttu-id="618fe-127">X</span><span class="sxs-lookup"><span data-stu-id="618fe-127">X</span></span> | <span data-ttu-id="618fe-128">X</span><span class="sxs-lookup"><span data-stu-id="618fe-128">X</span></span> | <span data-ttu-id="618fe-129">X</span><span class="sxs-lookup"><span data-stu-id="618fe-129">X</span></span> | <span data-ttu-id="618fe-130">X</span><span class="sxs-lookup"><span data-stu-id="618fe-130">X</span></span> |
| <span data-ttu-id="618fe-131">Właściciel grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="618fe-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="618fe-132">X</span><span class="sxs-lookup"><span data-stu-id="618fe-132">X</span></span> | -- | <span data-ttu-id="618fe-133">X</span><span class="sxs-lookup"><span data-stu-id="618fe-133">X</span></span> |
| <span data-ttu-id="618fe-134">Współautor grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="618fe-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="618fe-135">X</span><span class="sxs-lookup"><span data-stu-id="618fe-135">X</span></span> | -- | <span data-ttu-id="618fe-136">X</span><span class="sxs-lookup"><span data-stu-id="618fe-136">X</span></span> |
| <span data-ttu-id="618fe-137">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="618fe-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="618fe-138">X</span><span class="sxs-lookup"><span data-stu-id="618fe-138">X</span></span> |
| <span data-ttu-id="618fe-139">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-139">Security Administrator</span></span> | <span data-ttu-id="618fe-140">X</span><span class="sxs-lookup"><span data-stu-id="618fe-140">X</span></span> | -- | <span data-ttu-id="618fe-141">X</span><span class="sxs-lookup"><span data-stu-id="618fe-141">X</span></span> | <span data-ttu-id="618fe-142">X</span><span class="sxs-lookup"><span data-stu-id="618fe-142">X</span></span> |
| <span data-ttu-id="618fe-143">Czytnik zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="618fe-144">X</span><span class="sxs-lookup"><span data-stu-id="618fe-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="618fe-145">Zaleca się przypisanie użytkownikom najbardziej ograniczonej roli wystarczającej do wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="618fe-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="618fe-146">Na przykład przypisać rolę czytelnika do użytkowników, którzy muszą tylko przeglądać informacje o kondycji zabezpieczeń zasobu, ale nie podejmować działań, np. stosować zaleceń ani edytować zasad.</span><span class="sxs-lookup"><span data-stu-id="618fe-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="618fe-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="618fe-147">Next steps</span></span>
<span data-ttu-id="618fe-148">W tym artykule wyjaśniono, jak Centrum zabezpieczeń używa RBAC można przypisywać uprawnienia do użytkowników i określone akcje dozwolone dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="618fe-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="618fe-149">Teraz, kiedy znasz przypisań ról niezbędne do monitorowania stanu zabezpieczeń subskrypcji, edytować zasady zabezpieczeń i stosować zalecenia, Dowiedz się, jak:</span><span class="sxs-lookup"><span data-stu-id="618fe-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="618fe-150">Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="618fe-151">Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="618fe-152">Monitorowanie kondycji zabezpieczeń zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="618fe-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="618fe-153">Zarządzanie alertami zabezpieczeń i reagowanie na nie w usłudze Security Center</span><span class="sxs-lookup"><span data-stu-id="618fe-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="618fe-154">Monitorowanie rozwiązań partnerskich zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="618fe-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
