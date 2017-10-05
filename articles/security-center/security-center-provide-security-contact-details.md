---
title: "Podaj szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób podać szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="c62f2-103">Podaj szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="c62f2-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="c62f2-104">Centrum zabezpieczeń Azure zaleca Podaj szczegóły dotyczące kontaktu zabezpieczeń dla subskrypcji platformy Azure, jeśli nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="c62f2-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="c62f2-105">Te informacje będą używane przez firmę Microsoft do kontaktowania się z Tobą, gdy centrum Microsoft Security Response Center (MSRC) wykryje, że osoby nieupoważnione lub działające niezgodnie z prawem uzyskały dostęp do Twoich danych klienta.</span><span class="sxs-lookup"><span data-stu-id="c62f2-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="c62f2-106">MSRC wykonuje monitorowanie zabezpieczeń wybierz sieć platformy Azure i infrastruktury i odbiera zagrożeń analizy i nadużycia utrudnień od osób trzecich.</span><span class="sxs-lookup"><span data-stu-id="c62f2-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="c62f2-107">Wiadomość e-mail z powiadomieniem jest wysyłany na pierwsze wystąpienie codzienne alertu oraz tylko alerty o wysokim znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="c62f2-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="c62f2-108">Preferencje poczty e-mail można konfigurować tylko dla zasad subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c62f2-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="c62f2-109">Grupy zasobów w ramach subskrypcji odziedziczy te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c62f2-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="c62f2-110">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c62f2-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c62f2-111">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="c62f2-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c62f2-112">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="c62f2-112">Implement the recommendation</span></span>
1. <span data-ttu-id="c62f2-113">W **zalecenia** bloku, wybierz opcję **podać szczegóły dotyczące kontaktu zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="c62f2-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="c62f2-114">![Podaj kontaktu zabezpieczeń][1]</span><span class="sxs-lookup"><span data-stu-id="c62f2-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="c62f2-115">Spowoduje to otwarcie bloku **podać szczegóły dotyczące kontaktu zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="c62f2-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="c62f2-116">Wybierz subskrypcję platformy Azure, aby udostępnić informacje kontaktowe na.</span><span class="sxs-lookup"><span data-stu-id="c62f2-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="c62f2-117">![Podawanie szczegółów dotyczących kontaktu ds. zabezpieczeń][2]</span><span class="sxs-lookup"><span data-stu-id="c62f2-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="c62f2-118">Drugi **podać szczegóły dotyczące kontaktu zabezpieczeń** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="c62f2-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="c62f2-119">Wprowadź adres e-mail kontaktu zabezpieczeń lub adresów rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="c62f2-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="c62f2-120">Nie jest ograniczona liczba adresów e-mail, które można wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="c62f2-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="c62f2-121">Wprowadź jeden zabezpieczeń kontaktu międzynarodowy numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="c62f2-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="c62f2-122">Aby otrzymywać wiadomości e-mail o alertach o wysokim znaczeniu, włącz opcję **Wyślij do mnie wiadomość e-mail o alertach**.</span><span class="sxs-lookup"><span data-stu-id="c62f2-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="c62f2-123">W przyszłości konieczne będzie opcja do wysyłania powiadomień e-mail do właścicieli subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c62f2-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="c62f2-124">Ta opcja jest obecnie wygaszone.</span><span class="sxs-lookup"><span data-stu-id="c62f2-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="c62f2-125">Wybierz **OK** do zastosowania zabezpieczeń informacji kontaktowych do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c62f2-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="c62f2-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c62f2-126">See also</span></span>
<span data-ttu-id="c62f2-127">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="c62f2-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c62f2-128">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c62f2-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c62f2-129">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c62f2-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c62f2-130">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c62f2-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c62f2-131">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="c62f2-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c62f2-132">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="c62f2-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c62f2-133">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="c62f2-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c62f2-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.</span><span class="sxs-lookup"><span data-stu-id="c62f2-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
