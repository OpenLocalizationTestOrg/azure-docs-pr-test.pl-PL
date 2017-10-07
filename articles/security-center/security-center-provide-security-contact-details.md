---
title: "dane kontaktowe aaaProvide zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób zabezpieczeń tooprovide kontaktowe w Centrum zabezpieczeń Azure."
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
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="60ff5-103">Podaj szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="60ff5-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="60ff5-104">Centrum zabezpieczeń Azure zaleca Podaj szczegóły dotyczące kontaktu zabezpieczeń dla subskrypcji platformy Azure, jeśli nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="60ff5-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="60ff5-105">Te informacje będą używane przez Microsoft toocontact Jeśli hello Microsoft Security odpowiedzi Center (MSRC) wykrywa, że danych klienta uzyskaniu przez nieautoryzowanego lub nielegalnych stronę.</span><span class="sxs-lookup"><span data-stu-id="60ff5-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="60ff5-106">MSRC wykonuje monitorowanie zabezpieczeń wybierz hello sieć platformy Azure i infrastruktury i odbiera zagrożeń analizy i nadużycia utrudnień od osób trzecich.</span><span class="sxs-lookup"><span data-stu-id="60ff5-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="60ff5-107">Wiadomość e-mail z powiadomieniem jest wysyłany na powitania pierwsze codzienne wystąpienie alertu i tylko alerty o wysokim znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="60ff5-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="60ff5-108">Preferencje poczty e-mail można konfigurować tylko dla zasad subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60ff5-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="60ff5-109">Grupy zasobów w ramach subskrypcji odziedziczy te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="60ff5-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="60ff5-110">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="60ff5-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="60ff5-111">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="60ff5-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="60ff5-112">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="60ff5-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="60ff5-113">W hello **zalecenia** bloku, wybierz opcję **podać szczegóły dotyczące kontaktu zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="60ff5-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="60ff5-114">![Podaj kontaktu zabezpieczeń][1]</span><span class="sxs-lookup"><span data-stu-id="60ff5-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="60ff5-115">Spowoduje to otwarcie bloku hello **podać szczegóły dotyczące kontaktu zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="60ff5-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="60ff5-116">Wybierz informacje kontaktowe tooprovide hello subskrypcji platformy Azure na.</span><span class="sxs-lookup"><span data-stu-id="60ff5-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="60ff5-117">![Podawanie szczegółów dotyczących kontaktu ds. zabezpieczeń][2]</span><span class="sxs-lookup"><span data-stu-id="60ff5-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="60ff5-118">Drugi **podać szczegóły dotyczące kontaktu zabezpieczeń** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="60ff5-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="60ff5-119">Wprowadź adres e-mail kontaktu zabezpieczeń hello lub adresów rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="60ff5-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="60ff5-120">Ogranicz liczbę toohello adresów e-mail, które można wprowadzić nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="60ff5-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="60ff5-121">Wprowadź jeden zabezpieczeń kontaktu międzynarodowy numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="60ff5-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="60ff5-122">wiadomości e-mail tooreceive o alerty o wysokim znaczeniu, włącz opcję hello **Wyślij do mnie wiadomość e-mail o alertach**.</span><span class="sxs-lookup"><span data-stu-id="60ff5-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="60ff5-123">W przyszłości hello będą miały hello opcja toosend e-mail powiadomienia toosubscription właścicieli.</span><span class="sxs-lookup"><span data-stu-id="60ff5-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="60ff5-124">Ta opcja jest obecnie wygaszone.</span><span class="sxs-lookup"><span data-stu-id="60ff5-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="60ff5-125">Wybierz **OK** tooapply hello zabezpieczeń subskrypcji tooyour informacji, skontaktuj się z pomocą.</span><span class="sxs-lookup"><span data-stu-id="60ff5-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="60ff5-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="60ff5-126">See also</span></span>
<span data-ttu-id="60ff5-127">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="60ff5-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="60ff5-128">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="60ff5-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="60ff5-129">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60ff5-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="60ff5-130">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60ff5-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="60ff5-131">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="60ff5-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="60ff5-132">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="60ff5-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="60ff5-133">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="60ff5-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="60ff5-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="60ff5-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
