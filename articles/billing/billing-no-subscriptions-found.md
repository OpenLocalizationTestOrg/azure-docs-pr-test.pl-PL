---
title: "Nie znaleziono żadnych subskrypcji błąd podczas próby Zaloguj się do portalu Azure lub Centrum konta platformy Azure | Dokumentacja firmy Microsoft"
description: "Zapewnia rozwiązanie problemu, w którym subskrypcji nie znaleziono błąd występuje, gdy Zaloguj się do portalu Azure lub Centrum konta platformy Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="0a707-103">Nie znaleziono żadnych subskrypcji błąd w portalu Azure lub Centrum konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0a707-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="0a707-104">Może być pojawi się komunikat o błędzie "Nie można odnaleźć subskrypcji" podczas próby Zaloguj się do [portalu Azure](https://portal.azure.com/) lub [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="0a707-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="0a707-105">Ten artykuł zawiera rozwiązanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="0a707-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="0a707-106">Objaw</span><span class="sxs-lookup"><span data-stu-id="0a707-106">Symptom</span></span>

<span data-ttu-id="0a707-107">Podczas próby Zaloguj się do [portalu Azure](https://portal.azure.com/) lub [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions), pojawi się następujący komunikat o błędzie: "Nie można odnaleźć subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="0a707-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="0a707-108">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="0a707-108">Cause</span></span>

<span data-ttu-id="0a707-109">Ten problem występuje, jeśli konto nie ma wystarczających uprawnień.</span><span class="sxs-lookup"><span data-stu-id="0a707-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="0a707-110">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="0a707-110">Solution</span></span>

<span data-ttu-id="0a707-111">Upewnij się zalogować jako administrator poprawne.</span><span class="sxs-lookup"><span data-stu-id="0a707-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="0a707-112">Administrator konta ma dostęp do Centrum konta.</span><span class="sxs-lookup"><span data-stu-id="0a707-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="0a707-113">Administratorzy usługi (SA) i Współadministratorzy urzędu certyfikacji ma uprawnienia dostępu tylko do portalu Azure lub klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a707-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="0a707-114">Scenariusz 1: Odebrano komunikat o błędzie w [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0a707-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="0a707-115">Aby rozwiązać ten problem:</span><span class="sxs-lookup"><span data-stu-id="0a707-115">To fix this issue:</span></span>

* <span data-ttu-id="0a707-116">Upewnij się, że wybrano poprawny katalog platformy Azure, klikając konto u góry po prawej.</span><span class="sxs-lookup"><span data-stu-id="0a707-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Wybierz katalog u góry po prawej z portalu Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="0a707-118">Jeśli wybrano katalog prawo platformy Azure, ale nadal otrzymywać komunikat o błędzie [swoje konto jako właściciela](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="0a707-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="0a707-119">Scenariusz 2: Odebrano komunikat o błędzie w [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="0a707-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="0a707-120">Sprawdź, czy konto używane jest konto administratora.</span><span class="sxs-lookup"><span data-stu-id="0a707-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="0a707-121">Aby sprawdzić, który jest administratorem konta, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a707-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="0a707-122">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a707-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0a707-123">W menu Centrum wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="0a707-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="0a707-124">Wybierz subskrypcję, którą chcesz sprawdzić, a następnie wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0a707-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="0a707-125">Wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0a707-125">Select **Properties**.</span></span> <span data-ttu-id="0a707-126">Administratora konta subskrypcji jest wyświetlany w **administrator konta** pole.</span><span class="sxs-lookup"><span data-stu-id="0a707-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="0a707-127">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="0a707-127">Need help?</span></span> <span data-ttu-id="0a707-128">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="0a707-128">Contact support.</span></span>
<span data-ttu-id="0a707-129">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="0a707-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
