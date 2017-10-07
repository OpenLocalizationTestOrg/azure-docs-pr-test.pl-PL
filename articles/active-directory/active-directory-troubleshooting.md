---
title: "Rozwiązywanie problemów: Element usługi Active Directory jest lub jest ona niedostępna | Dokumentacja firmy Microsoft"
description: "Toodo gdy element menu usługi Active Directory nie jest wyświetlane w portalu zarządzania Azure hello."
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
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="a2c88-103">Rozwiązywanie problemów: Element usługi Active Directory jest lub jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="a2c88-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="a2c88-104">Wiele hello instrukcje dotyczące korzystania z funkcji usługi Azure Active Directory i usług rozpoczynać się od "Przejdź toohello portalu zarządzania Azure i kliknij polecenie **usługi Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="a2c88-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="a2c88-105">Ale co zrobić, jeśli nie ma elementu menu lub rozszerzenie usługi Active Directory hello lub jest on oznaczony **nie jest dostępny**?</span><span class="sxs-lookup"><span data-stu-id="a2c88-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="a2c88-106">Ten temat jest zaprojektowana toohelp.</span><span class="sxs-lookup"><span data-stu-id="a2c88-106">This topic is designed toohelp.</span></span> <span data-ttu-id="a2c88-107">Opisuje warunki hello, w którym **usługi Active Directory** nie pojawia się lub jest niedostępna i wyjaśniono, jak tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a2c88-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="a2c88-108">Brak usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2c88-108">Active Directory is missing</span></span>
<span data-ttu-id="a2c88-109">Zazwyczaj **usługi Active Directory** element będzie wyświetlany w menu nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a2c88-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="a2c88-110">Hello instrukcjami procedury usługi Azure Active Directory założono, że ten element jest w danym widoku.</span><span class="sxs-lookup"><span data-stu-id="a2c88-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Zrzut ekranu: usługi Active Directory na platformie Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="a2c88-112">Witaj usługi Active Directory element będzie wyświetlany w menu nawigacji po lewej stronie powitania, gdy spełniony jest dowolny z hello następujące warunki.</span><span class="sxs-lookup"><span data-stu-id="a2c88-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="a2c88-113">W przeciwnym razie nie ma elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a2c88-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="a2c88-114">bieżący użytkownik Hello zalogować się przy użyciu konta Microsoft (znanego wcześniej jako identyfikator Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="a2c88-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="a2c88-115">LUB</span><span class="sxs-lookup"><span data-stu-id="a2c88-115">OR</span></span>
* <span data-ttu-id="a2c88-116">Witaj dzierżawą platformy Azure ma katalogu i hello bieżącego konta administratora katalogu.</span><span class="sxs-lookup"><span data-stu-id="a2c88-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="a2c88-117">LUB</span><span class="sxs-lookup"><span data-stu-id="a2c88-117">OR</span></span>
* <span data-ttu-id="a2c88-118">Hello dzierżawy Azure ma co najmniej jedną przestrzeń nazw kontroli dostępu usługi Azure AD (ACS).</span><span class="sxs-lookup"><span data-stu-id="a2c88-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="a2c88-119">Aby uzyskać więcej informacji, zobacz [Namespace kontroli dostępu](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2c88-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="a2c88-120">LUB</span><span class="sxs-lookup"><span data-stu-id="a2c88-120">OR</span></span>
* <span data-ttu-id="a2c88-121">Witaj dzierżawy Azure ma co najmniej jednego dostawcę usługi Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="a2c88-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="a2c88-122">Aby uzyskać więcej informacji, zobacz [administrowanie dostawców uwierzytelniania wieloskładnikowego Azure](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="a2c88-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="a2c88-123">toocreate kontroli dostępu przestrzeni nazw lub dostawcę usługi Multi-Factor Authentication kliknij **+ nowy** > **usługi aplikacji** > **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a2c88-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="a2c88-124">tooget prawa administracyjne tooa katalogu, ma administrator przypisać administrator konta tooyour roli.</span><span class="sxs-lookup"><span data-stu-id="a2c88-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="a2c88-125">Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a2c88-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="a2c88-126">Active Directory nie jest dostępna</span><span class="sxs-lookup"><span data-stu-id="a2c88-126">Active Directory is not available</span></span>
<span data-ttu-id="a2c88-127">Po kliknięciu **+ nowy** > **usługi aplikacji**, **usługi Active Directory** element będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="a2c88-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="a2c88-128">W szczególności hello usługi Active Directory element jest wyświetlany, gdy hello funkcji usługi Active Directory, takich jak katalog, kontroli dostępu lub Dostawca uwierzytelniania MFA, są dostępne toohello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a2c88-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="a2c88-129">Jednak podczas ładowania strony hello elementu hello jest przyciemnione i jest oznaczony jako **nie jest dostępny**.</span><span class="sxs-lookup"><span data-stu-id="a2c88-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="a2c88-130">Jest to stan przejściowy.</span><span class="sxs-lookup"><span data-stu-id="a2c88-130">This is a temporary state.</span></span> <span data-ttu-id="a2c88-131">Jeśli Poczekaj kilka sekund, hello element staje się dostępna.</span><span class="sxs-lookup"><span data-stu-id="a2c88-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="a2c88-132">Jeśli opóźnienie hello zostanie przedłużony, odświeżanie strony sieci web hello często rozwiązuje hello problem.</span><span class="sxs-lookup"><span data-stu-id="a2c88-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Zrzut ekranu: Active Directory nie jest dostępna](./media/active-directory-troubleshooting/not-available.png)

