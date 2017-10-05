---
title: "Rozwiązywanie problemów: Element usługi Active Directory jest lub jest ona niedostępna | Dokumentacja firmy Microsoft"
description: "Co należy zrobić, gdy element menu usługi Active Directory nie jest wyświetlane w portalu zarządzania Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="1968e-103">Rozwiązywanie problemów: Element usługi Active Directory jest lub jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="1968e-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="1968e-104">Wiele instrukcje dotyczące korzystania z funkcji usługi Azure Active Directory i usług rozpoczynać się od "Przejdź do portalu zarządzania Azure i kliknij polecenie **usługi Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="1968e-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="1968e-105">Ale co zrobić, jeśli nie ma elementu menu lub rozszerzenie usługi Active Directory lub jest on oznaczony **nie jest dostępny**?</span><span class="sxs-lookup"><span data-stu-id="1968e-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="1968e-106">W tym temacie jest przeznaczona do pomocy.</span><span class="sxs-lookup"><span data-stu-id="1968e-106">This topic is designed to help.</span></span> <span data-ttu-id="1968e-107">Opisuje warunki, w którym **usługi Active Directory** nie pojawia się lub jest niedostępna i wyjaśniono sposób kontynuować.</span><span class="sxs-lookup"><span data-stu-id="1968e-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="1968e-108">Brak usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1968e-108">Active Directory is missing</span></span>
<span data-ttu-id="1968e-109">Zazwyczaj **usługi Active Directory** element będzie wyświetlany w menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1968e-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="1968e-110">Z instrukcjami w usłudze Azure Active Directory procedury założono, że ten element jest w danym widoku.</span><span class="sxs-lookup"><span data-stu-id="1968e-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Zrzut ekranu: usługi Active Directory na platformie Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="1968e-112">Element usługi Active Directory jest wyświetlany w menu nawigacji po lewej stronie, gdy spełniony jest dowolny z następujących warunków.</span><span class="sxs-lookup"><span data-stu-id="1968e-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="1968e-113">W przeciwnym razie nie ma elementu.</span><span class="sxs-lookup"><span data-stu-id="1968e-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="1968e-114">Bieżący użytkownik zalogować się przy użyciu konta Microsoft (znanego wcześniej jako identyfikator Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="1968e-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="1968e-115">LUB</span><span class="sxs-lookup"><span data-stu-id="1968e-115">OR</span></span>
* <span data-ttu-id="1968e-116">Dzierżawy Azure ma katalog, a bieżące konto jest kontem administratora katalogu.</span><span class="sxs-lookup"><span data-stu-id="1968e-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="1968e-117">LUB</span><span class="sxs-lookup"><span data-stu-id="1968e-117">OR</span></span>
* <span data-ttu-id="1968e-118">Dzierżawy Azure ma co najmniej jedną przestrzeń nazw kontroli dostępu usługi Azure AD (ACS).</span><span class="sxs-lookup"><span data-stu-id="1968e-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="1968e-119">Aby uzyskać więcej informacji, zobacz [Namespace kontroli dostępu](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="1968e-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="1968e-120">LUB</span><span class="sxs-lookup"><span data-stu-id="1968e-120">OR</span></span>
* <span data-ttu-id="1968e-121">Dzierżawy Azure ma co najmniej jednego dostawcę usługi Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="1968e-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="1968e-122">Aby uzyskać więcej informacji, zobacz [administrowanie dostawców uwierzytelniania wieloskładnikowego Azure](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1968e-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="1968e-123">Aby utworzyć przestrzeń nazw kontroli dostępu lub dostawcy uwierzytelniania wieloskładnikowego, kliknij przycisk **+ nowy** > **usługi aplikacji** > **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1968e-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="1968e-124">Aby uzyskać uprawnienia administracyjne do katalogu, poproś administratora o Przypisz rolę administratora do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="1968e-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="1968e-125">Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1968e-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="1968e-126">Active Directory nie jest dostępna</span><span class="sxs-lookup"><span data-stu-id="1968e-126">Active Directory is not available</span></span>
<span data-ttu-id="1968e-127">Po kliknięciu **+ nowy** > **usługi aplikacji**, **usługi Active Directory** element będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="1968e-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="1968e-128">W szczególności elementu usługi Active Directory jest wyświetlany, gdy funkcji usługi Active Directory, takich jak katalog, kontroli dostępu lub Dostawca uwierzytelniania MFA, są dostępne dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1968e-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="1968e-129">Jednak podczas ładowania strony element jest niedostępna i jest oznaczony jako **nie jest dostępny**.</span><span class="sxs-lookup"><span data-stu-id="1968e-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="1968e-130">Jest to stan przejściowy.</span><span class="sxs-lookup"><span data-stu-id="1968e-130">This is a temporary state.</span></span> <span data-ttu-id="1968e-131">Jeśli Poczekaj kilka sekund, element staje się dostępna.</span><span class="sxs-lookup"><span data-stu-id="1968e-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="1968e-132">Jeśli opóźnienie zostanie przedłużony, często odświeżania strony sieci web nie zostanie rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="1968e-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Zrzut ekranu: Active Directory nie jest dostępna](./media/active-directory-troubleshooting/not-available.png)

