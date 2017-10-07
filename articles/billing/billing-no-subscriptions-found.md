---
title: "Subskrypcje aaaNo znaleziono błąd po spróbuj toosign w portalu tooAzure lub Centrum konta platformy Azure | Dokumentacja firmy Microsoft"
description: "Zapewnia hello rozwiązanie problemu, w którym subskrypcji nie znaleziono błąd występuje, gdy Zaloguj się w portalu tooAzure lub Centrum konta platformy Azure."
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
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="4996d-103">Nie znaleziono żadnych subskrypcji błąd w portalu Azure lub Centrum konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4996d-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="4996d-104">Może być pojawi się komunikat o błędzie "Nie można odnaleźć subskrypcji" podczas próby toosign w toohello [portalu Azure](https://portal.azure.com/) lub hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="4996d-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="4996d-105">Ten artykuł zawiera rozwiązanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="4996d-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="4996d-106">Objaw</span><span class="sxs-lookup"><span data-stu-id="4996d-106">Symptom</span></span>

<span data-ttu-id="4996d-107">Podczas próby toosign w toohello [portalu Azure](https://portal.azure.com/) lub hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions), pojawi się następujący komunikat o błędzie hello: "Nie można odnaleźć subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="4996d-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="4996d-108">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="4996d-108">Cause</span></span>

<span data-ttu-id="4996d-109">Ten problem występuje, jeśli konto nie ma wystarczających uprawnień.</span><span class="sxs-lookup"><span data-stu-id="4996d-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="4996d-110">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="4996d-110">Solution</span></span>

<span data-ttu-id="4996d-111">Upewnij się, czy logujesz się jako administrator poprawne hello.</span><span class="sxs-lookup"><span data-stu-id="4996d-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="4996d-112">Administrator konta ma dostęp tylko hello Centrum konta.</span><span class="sxs-lookup"><span data-stu-id="4996d-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="4996d-113">Administratorzy usługi (SA) i Współadministratorzy (CA) mają tylko toohello uprawnienia dostępu do portalu Azure lub hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4996d-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="4996d-114">Scenariusz 1: Odebrano komunikat o błędzie w hello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4996d-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="4996d-115">toofix tego problemu:</span><span class="sxs-lookup"><span data-stu-id="4996d-115">toofix this issue:</span></span>

* <span data-ttu-id="4996d-116">Upewnij się, tym hello poprawny katalogu platformy Azure jest zaznaczona, klikając konto w prawym górnym narożniku hello.</span><span class="sxs-lookup"><span data-stu-id="4996d-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Wybierz hello katalogu hello górnego prawego hello portalu Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="4996d-118">Jeśli hello bezpośrednio do usługi Azure directory jest zaznaczony, ale nadal hello komunikat o błędzie, [swoje konto jako właściciela](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="4996d-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="4996d-119">Scenariusz 2: Odebrano komunikat o błędzie w hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="4996d-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="4996d-120">Sprawdź, czy konto użyte hello hello konta administratora.</span><span class="sxs-lookup"><span data-stu-id="4996d-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="4996d-121">tooverify, który hello administratora konta, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4996d-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="4996d-122">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4996d-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4996d-123">W menu Centrum hello wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="4996d-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="4996d-124">Wybierz subskrypcję hello mają toocheck, a następnie wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4996d-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="4996d-125">Wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="4996d-125">Select **Properties**.</span></span> <span data-ttu-id="4996d-126">Witaj administratora konta subskrypcji hello jest wyświetlany w hello **administrator konta** pole.</span><span class="sxs-lookup"><span data-stu-id="4996d-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="4996d-127">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="4996d-127">Need help?</span></span> <span data-ttu-id="4996d-128">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="4996d-128">Contact support.</span></span>
<span data-ttu-id="4996d-129">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="4996d-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
