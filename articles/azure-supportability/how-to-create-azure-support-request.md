---
title: "Jak utworzyć żądanie pomocy technicznej platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak utworzyć żądanie pomocy technicznej platformy Azure."
services: Azure Supportability
documentationcenter: 
author: ganganarayanan
manager: scotthit
editor: 
ms.assetid: fd6841ea-c1d5-4bb7-86bd-0c708d193b89
ms.service: azure-supportability
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: gangan
ms.openlocfilehash: 70a4762383d64dc8d568c628cf260ebd8f2d179d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-an-azure-support-request"></a><span data-ttu-id="0d9be-103">Jak utworzyć żądanie obsługi na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0d9be-103">How to create an Azure support request</span></span>
## <a name="summary"></a><span data-ttu-id="0d9be-104">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0d9be-104">Summary</span></span>
<span data-ttu-id="0d9be-105">Klientów platformy Azure można tworzyć i zarządzanie żądaniami obsługi w portalu Azure [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d9be-105">Azure customers can create and manage support requests in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="0d9be-106">Portal Azure w Niemczech to [https://portal.microsoftazure.de](https://portal.microsoftazure.de) portal Azure dla instytucji rządowych Stanów Zjednoczonych to [https://portal.azure.us](https://portal.azure.us).</span><span class="sxs-lookup"><span data-stu-id="0d9be-106">Azure portal for Germany is [https://portal.microsoftazure.de](https://portal.microsoftazure.de) Azure portal for the United States government is [https://portal.azure.us](https://portal.azure.us).</span></span>
> 
> 

<span data-ttu-id="0d9be-107">Na podstawie opinii klientów, Zaktualizowaliśmy środowisko żądania pomocy technicznej skoncentrować się na trzy główne cele:</span><span class="sxs-lookup"><span data-stu-id="0d9be-107">Based on customer feedback, we’ve updated the support request experience to focus on three main goals:</span></span>

* <span data-ttu-id="0d9be-108">**Prostsze**: zmniejszyć kliknięcia i bloków, aby utworzyć prosty proces przesyłania żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0d9be-108">**Streamlined**: Reduce clicks and blades to make the process of submitting a support request simple.</span></span>
* <span data-ttu-id="0d9be-109">**Zintegrowane**: przy rozwiązywaniu problemu z zasobem platformy Azure, powinna być łatwa do otwarcia żądania pomocy technicznej dla tego zasobu bez przełączania kontekstu.</span><span class="sxs-lookup"><span data-stu-id="0d9be-109">**Integrated**: When you’re troubleshooting an issue with an Azure resource, it should be easy to open a support request for that resource without switching context.</span></span>
* <span data-ttu-id="0d9be-110">**Efektywne**: zebrać informacje o kluczu specjalistą pomocy technicznej będzie musiał wydajne rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="0d9be-110">**Efficient**: Gather the key information your support engineer will need to efficiently resolve your issue.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0d9be-111">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0d9be-111">Getting started</span></span>
<span data-ttu-id="0d9be-112">Można utworzyć żądania obsługi, w menu górnym menu nawigacyjnym lub bezpośrednio z bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="0d9be-112">You can create a support request from the top navigation menu or directly from a resource blade.</span></span>

<span data-ttu-id="0d9be-113">**W górnym pasku nawigacyjnym**</span><span class="sxs-lookup"><span data-stu-id="0d9be-113">**From the top navigation bar**</span></span>

![Nowe żądanie pomocy technicznej](./media/how-to-create-azure-support-request/NewSupportRequest.png)

<span data-ttu-id="0d9be-115">**W bloku zasobów**</span><span class="sxs-lookup"><span data-stu-id="0d9be-115">**From a resource blade**</span></span>

![W kontekście.](./media/how-to-create-azure-support-request/Incontext.png)

## <a name="basics"></a><span data-ttu-id="0d9be-117">Podstawy</span><span class="sxs-lookup"><span data-stu-id="0d9be-117">Basics</span></span>
<span data-ttu-id="0d9be-118">Pierwszym krokiem procesu żądania pomocy technicznej zbiera podstawowe informacje na temat problemu i plan pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0d9be-118">The first step of the support request process gathers basic information about your issue and your support plan.</span></span>

<span data-ttu-id="0d9be-119">Spójrzmy na przykład: jest ukierunkowane trudności techniczne z maszyny wirtualnej i podejrzewasz problem z łącznością sieciową.</span><span class="sxs-lookup"><span data-stu-id="0d9be-119">Let’s take an example: You’re facing technical difficulties with your virtual machine and suspect a network connectivity issue.</span></span>
<span data-ttu-id="0d9be-120">Wybieranie usługi ("maszyny wirtualnej systemu Windows") i zasobów (Nazwa maszyny wirtualnej) w pierwszym kroku kreatora rozpoczyna proces uzyskaniem pomocy na temat tego problemu.</span><span class="sxs-lookup"><span data-stu-id="0d9be-120">Selecting the service ("Virtual Machine running Windows") and the resource (the name of your virtual machine) in the first step of the wizard starts the process of getting help for this issue.</span></span>

![Blok Podstawowe](./media/how-to-create-azure-support-request/Basics.png)

> [!NOTE]
> <span data-ttu-id="0d9be-122">Azure zapewnia obsługę nieograniczone Zarządzanie subskrypcją (np. rozliczeń, dostosowania przydziału i transferów konta).</span><span class="sxs-lookup"><span data-stu-id="0d9be-122">Azure provides unlimited support for subscription management (things like billing, quota adjustments, and account transfers).</span></span> <span data-ttu-id="0d9be-123">Aby uzyskać pomoc techniczną konieczne jest plan pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0d9be-123">For technical support, you need a support plan.</span></span> <span data-ttu-id="0d9be-124">[Dowiedz się więcej o plany pomocy technicznej](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="0d9be-124">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

## <a name="problem"></a><span data-ttu-id="0d9be-125">Problem</span><span class="sxs-lookup"><span data-stu-id="0d9be-125">Problem</span></span>
<span data-ttu-id="0d9be-126">Drugim kroku kreatora zbiera informacje o dodatkowych szczegółów na temat problemu.</span><span class="sxs-lookup"><span data-stu-id="0d9be-126">The second step of the wizard gathers additional details about the issue.</span></span> <span data-ttu-id="0d9be-127">Udostępnia on szczegółowe dokładne informacje w tym kroku pozwala nam rozesłać tej sprawy najlepsze specjaliście pomocy technicznej dla problemu i rozpocząć diagnozowania problemu tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="0d9be-127">Providing accurate details in this step allows us to route your case to the best support engineer for the issue and to begin diagnosing the issue as soon as possible.</span></span>

![Blok problem](./media/how-to-create-azure-support-request/Problem.png)

<span data-ttu-id="0d9be-129">Kontynuowaniem z powyższego przykładu łączności maszyny wirtualnej, czy wypełnić ten formularz, aby wskazywać problem z łącznością sieciową i czy zawierają dodatkowe szczegółowe informacje o problemie, łącznie ze przybliżony czas, kiedy wystąpił problem.</span><span class="sxs-lookup"><span data-stu-id="0d9be-129">Continuing with the virtual machine connectivity example from above, you would fill out this form to indicate a network connectivity issue, and you would provide further details about the issue, including the approximate time when you experienced the issue.</span></span>

## <a name="related-help"></a><span data-ttu-id="0d9be-130">Pokrewne pomocy</span><span class="sxs-lookup"><span data-stu-id="0d9be-130">Related Help</span></span>
<span data-ttu-id="0d9be-131">W przypadku niektórych problemów firma Microsoft udostępnia linki pokrewne pomocy, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="0d9be-131">For some problems, we provide related help links to troubleshoot the issue.</span></span> <span data-ttu-id="0d9be-132">Zalecane dokumentów pomaga, możesz kontynuować proces do utworzenia żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="0d9be-132">If the recommended documents do not help, you can continue through the process to create a support request.</span></span>
<span data-ttu-id="0d9be-133">![Pokrewne pomocy](./media/how-to-create-azure-support-request/RelatedHelp.png)</span><span class="sxs-lookup"><span data-stu-id="0d9be-133">![Related help](./media/how-to-create-azure-support-request/RelatedHelp.png)</span></span>

## <a name="contact-information"></a><span data-ttu-id="0d9be-134">Informacje kontaktowe</span><span class="sxs-lookup"><span data-stu-id="0d9be-134">Contact Information</span></span>
<span data-ttu-id="0d9be-135">Ostatni krok kreatora potwierdza Twoich informacji kontaktowych, aby było wiadomo, jak nawiązać połączenie z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="0d9be-135">The last step of the wizard confirms your contact information so we know how to reach you.</span></span>
<span data-ttu-id="0d9be-136">![Informacje kontaktowe](./media/how-to-create-azure-support-request/ContactInformation.png)</span><span class="sxs-lookup"><span data-stu-id="0d9be-136">![Contact Information](./media/how-to-create-azure-support-request/ContactInformation.png)</span></span>

<span data-ttu-id="0d9be-137">W zależności od ważność problemu może być monit o wskazują, jeśli mamy się z Tobą podczas godzin pracy lub jeśli chcesz użyć odpowiedzi 24 x 7, co oznacza, że firma Microsoft może skontaktować się z Tobą w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="0d9be-137">Depending on the severity of your issue, you may be asked to indicate if you would like us to contact you during business hours or if you would prefer a 24x7 response, which means we may contact you at any time.</span></span>
<span data-ttu-id="0d9be-138">![Informacje kontaktowe 24 x 7](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span><span class="sxs-lookup"><span data-stu-id="0d9be-138">![Contact Information 24x7](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span></span>

## <a name="manage-support-requests"></a><span data-ttu-id="0d9be-139">Zarządzanie żądaniami obsługi</span><span class="sxs-lookup"><span data-stu-id="0d9be-139">Manage support requests</span></span>
<span data-ttu-id="0d9be-140">Po utworzeniu żądania obsługi, można wyświetlić szczegółów **Zarządzanie żądaniami obsługi** strony.</span><span class="sxs-lookup"><span data-stu-id="0d9be-140">After you create the support request, you can view the details from the **Manage Support Requests** page.</span></span>

<span data-ttu-id="0d9be-141">**W górnym pasku nawigacyjnym**</span><span class="sxs-lookup"><span data-stu-id="0d9be-141">**From the top navigation bar**</span></span>

![Zarządzanie łącze żądania obsługi](./media/how-to-create-azure-support-request/ManageSupportRequest-link.png)

<span data-ttu-id="0d9be-143">Na **Zarządzaj żądaniami obsługi** strony, można wyświetlić wszystkie żądania pomocy technicznej i ich stan.</span><span class="sxs-lookup"><span data-stu-id="0d9be-143">On the **Manage support requests** page, you can view all support requests and their status.</span></span>
<span data-ttu-id="0d9be-144">![Zarządzanie żądania obsługi](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span><span class="sxs-lookup"><span data-stu-id="0d9be-144">![Manage Support Request](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span></span>

<span data-ttu-id="0d9be-145">Wybierz żądanie pomocy technicznej, aby wyświetlić szczegóły, w tym ważność i szacowany czas potrzebny do pracownika pomocy technicznej odpowiedzieć.</span><span class="sxs-lookup"><span data-stu-id="0d9be-145">Select the support request to view details, including severity and the expected time it will take for a support engineer to respond.</span></span>
<span data-ttu-id="0d9be-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span><span class="sxs-lookup"><span data-stu-id="0d9be-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span></span>

<span data-ttu-id="0d9be-147">Jeśli chcesz zmienić ważność żądania, kliknij przycisk **wpływ na prowadzoną działalność** kafelka.</span><span class="sxs-lookup"><span data-stu-id="0d9be-147">If you want to change the severity of the request, click the **Business impact** tile.</span></span> <span data-ttu-id="0d9be-148">W tym przykładzie poprzedzających żądania ma obecnie ustawioną ważności C.</span><span class="sxs-lookup"><span data-stu-id="0d9be-148">In the preceeding example, the request is currently set to Severity C.</span></span>

<span data-ttu-id="0d9be-149">Kliknięcie kafelka przedstawia listę wag, które można przypisać do żądania obsługi otwarte.</span><span class="sxs-lookup"><span data-stu-id="0d9be-149">Clicking the tile shows you the list of severities you can assign to an open support request.</span></span>

> [!NOTE]
> <span data-ttu-id="0d9be-150">Poziom ważności maksymalną zależy od plan pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0d9be-150">The maximum severity level depends on your support plan.</span></span> <span data-ttu-id="0d9be-151">[Dowiedz się więcej o plany pomocy technicznej](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="0d9be-151">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

![VID-2](./media/how-to-create-azure-support-request/VID-2.png)

## <a name="feedback"></a><span data-ttu-id="0d9be-153">Opinia</span><span class="sxs-lookup"><span data-stu-id="0d9be-153">Feedback</span></span>
<span data-ttu-id="0d9be-154">Firma Microsoft zawsze są otwarte na opinie i sugestie!</span><span class="sxs-lookup"><span data-stu-id="0d9be-154">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="0d9be-155">Wyślij nam Twojej [sugestie](https://feedback.azure.com/forums/266794-support-feedback).</span><span class="sxs-lookup"><span data-stu-id="0d9be-155">Please send us your [suggestions](https://feedback.azure.com/forums/266794-support-feedback).</span></span> <span data-ttu-id="0d9be-156">Ponadto można Uwzględnij z nami za pośrednictwem [Twitter](https://twitter.com/azuresupport) lub [fora MSDN](https://social.msdn.microsoft.com/Forums/azure).</span><span class="sxs-lookup"><span data-stu-id="0d9be-156">Additionally, you can engage with us via [Twitter](https://twitter.com/azuresupport) or the [MSDN forums](https://social.msdn.microsoft.com/Forums/azure).</span></span>

## <a name="learn-more"></a><span data-ttu-id="0d9be-157">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="0d9be-157">Learn more</span></span>
[<span data-ttu-id="0d9be-158">Pomoc techniczna platformy Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0d9be-158">Azure Support FAQ</span></span>](https://azure.microsoft.com/support/faq)

