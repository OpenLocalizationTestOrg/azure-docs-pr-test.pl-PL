---
title: "Usługa Azure Active Directory raportowania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Raportowanie często zadawane pytania dotyczące usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="163ad-103">Usługa Azure Active Directory raportowania — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="163ad-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="163ad-104">Ten artykuł zawiera odpowiedzi na często zadawane pytania (FAQ) dotyczące raportowania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="163ad-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="163ad-105">Aby uzyskać więcej informacji, zobacz [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="163ad-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="163ad-106">**Pytanie: co to jest przechowywanie danych o Dzienniki aktywności (inspekcji i logowania) w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="163ad-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="163ad-107">**Odpowiedź:** 7 dni danych udostępniamy klientom wolnego i przełączanie do usługi Azure AD Premium 1 lub Premium 2 licencji, dostęp do danych przez maksymalnie 30 dni.</span><span class="sxs-lookup"><span data-stu-id="163ad-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="163ad-108">Aby uzyskać więcej szczegółów na przechowywania, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="163ad-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="163ad-109">**Pytanie: jak długo trwa do momentu mogę zobaczyć dane o aktywności, po zakończeniu I Moje zadania?**</span><span class="sxs-lookup"><span data-stu-id="163ad-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="163ad-110">**Odpowiedź:** dzienników inspekcji działania mają opóźnienia, począwszy od 15 minut do godziny.</span><span class="sxs-lookup"><span data-stu-id="163ad-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="163ad-111">Dzienniki aktywności logowania ma opóźnienia — od 15 minut dla większości rekordów i maksymalnie 2 godziny dla niewielkiej liczby rekordów.</span><span class="sxs-lookup"><span data-stu-id="163ad-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="163ad-112">**Pytanie: należy być administratorem globalnym, aby zobaczyć działanie dzienniki w portalu Azure lub w celu uzyskania danych za pośrednictwem interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="163ad-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="163ad-113">**Odpowiedź:** Nie.</span><span class="sxs-lookup"><span data-stu-id="163ad-113">**A:** No.</span></span> <span data-ttu-id="163ad-114">Może to być **czytnika zabezpieczeń**, **administratora zabezpieczeń** lub **administratora globalnego** Aby wyświetlić dane w portalu Azure lub dostępu do niego za pośrednictwem interfejsu API raportowania.</span><span class="sxs-lookup"><span data-stu-id="163ad-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="163ad-115">**Pytanie: czy można uzyskać informacji dziennika aktywności usługi Office 365 za pomocą portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="163ad-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="163ad-116">**Odpowiedź:** mimo że działania usługi Office 365 i Azure AD działania dzienniki udziału dużej ilości zasobów katalogu, jeśli chcesz pełnego widoku Dzienniki aktywności usługi Office 365, należy przejść do Centrum administracyjne usługi Office 365, aby uzyskać informacje dziennika Office 365 działania.</span><span class="sxs-lookup"><span data-stu-id="163ad-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="163ad-117">**Pytanie: które interfejsów API należy używać można pobrać informacji o dziennikach Office 365 działania?**</span><span class="sxs-lookup"><span data-stu-id="163ad-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="163ad-118">**Odpowiedź:** uzyskiwać dostęp do interfejsów API usługi Office 365 Management [Office 365 działanie logowania za pośrednictwem interfejsu API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="163ad-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="163ad-119">**Pytanie: jak wiele rekordów I można pobrać z portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="163ad-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="163ad-120">**Odpowiedź:** maksymalnie 120 rekordów K można pobrać z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="163ad-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="163ad-121">Rekordy są sortowane według *najnowszych* i domyślnie uzyskać najnowsze rekordy 120 K.</span><span class="sxs-lookup"><span data-stu-id="163ad-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="163ad-122">**Pytanie: jak wiele rekordów można zbadać za pomocą działania interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="163ad-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="163ad-123">**Odpowiedź:** można zbadać 1 milion rekordy (Jeśli nie jest używany operator top sortuje rekordu przez większość ostatnie).</span><span class="sxs-lookup"><span data-stu-id="163ad-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="163ad-124">Użycie operatora "top" można badać się do rekordów 500 KB.</span><span class="sxs-lookup"><span data-stu-id="163ad-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="163ad-125">Przykładowe zapytania można znaleźć na temat korzystania z interfejsu API w tym miejscu [tutaj](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="163ad-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="163ad-126">**Pytanie: jak uzyskać licencję premium?**</span><span class="sxs-lookup"><span data-stu-id="163ad-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="163ad-127">**Odpowiedź:** zobacz [wprowadzenie do korzystania z usługi Azure Active Directory Premium](active-directory-get-started-premium.md) dla odpowiedzi na to pytanie.</span><span class="sxs-lookup"><span data-stu-id="163ad-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="163ad-128">**Pytanie: jak najszybciej Zobacz dane działań po otrzymaniu licencji premium?**</span><span class="sxs-lookup"><span data-stu-id="163ad-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="163ad-129">**Odpowiedź:** Jeśli masz już dane działań jako wolne licencji, a następnie można zobaczyć te same dane.</span><span class="sxs-lookup"><span data-stu-id="163ad-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="163ad-130">Jeśli nie masz żadnych danych, ich może zająć jeden lub dwa dni.</span><span class="sxs-lookup"><span data-stu-id="163ad-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="163ad-131">**Pytanie: wyświetlane dane z ostatniego miesiąca po otrzymaniu licencji usługi Azure AD premium?**</span><span class="sxs-lookup"><span data-stu-id="163ad-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="163ad-132">**Odpowiedź:** Jeśli włączono ostatnio do wersji Premium (w tym wersja próbna), można wyświetlić danych się do 7 dni początkowo.</span><span class="sxs-lookup"><span data-stu-id="163ad-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="163ad-133">Gromadzi dane, zobaczysz maksymalnie 30 dni.</span><span class="sxs-lookup"><span data-stu-id="163ad-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="163ad-134">**Pytanie: Brak zdarzeń ryzyko w ochronę tożsamości, ale nie widzę odpowiedniego logowania w wszystkie sesje logowania. Jest to oczekiwane?**</span><span class="sxs-lookup"><span data-stu-id="163ad-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="163ad-135">**Odpowiedź:** tak, Identity Protection ocenia ryzyko dla wszystkich przepływów uwierzytelniania czy jeśli interakcyjnego lub nieinterakcyjnym.</span><span class="sxs-lookup"><span data-stu-id="163ad-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="163ad-136">Jednak wszystkie sesje logowania tylko przedstawia tylko interakcyjnego logowania.</span><span class="sxs-lookup"><span data-stu-id="163ad-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="163ad-137">**Pytanie: jak można pobrać raportu "Użytkownicy oflagowani ryzyka" w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="163ad-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="163ad-138">**A:** opcję, aby pobrać *użytkownicy oflagowani ryzyka* raportu zostanie dodany wkrótce.</span><span class="sxs-lookup"><span data-stu-id="163ad-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="163ad-139">**Pytanie: jak dowiedzieć, dlaczego logowania lub użytkownikiem zostało oznaczone ryzykowne w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="163ad-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="163ad-140">**Odpowiedź:** klienci wersji Premium można dowiedzieć się więcej o podstawowym zdarzenia o podwyższonym ryzyku, klikając na użytkownika w "Użytkownicy oflagowani ryzyka" lub klikając na "ryzykowne logowania".</span><span class="sxs-lookup"><span data-stu-id="163ad-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="163ad-141">Klienci bezpłatne i podstawowych wydanie uzyskać zagrożonych użytkowników i logowanie bez podstawowych informacji o zdarzeniu ryzyka.</span><span class="sxs-lookup"><span data-stu-id="163ad-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="163ad-142">**Pytanie: jak adresy IP są obliczane w logowania i logowania ryzykowne raport?**</span><span class="sxs-lookup"><span data-stu-id="163ad-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="163ad-143">**Odpowiedź:** adresy IP są przydzielane w taki sposób, że istnieje połączenie ostateczne między adresu IP i gdzie fizycznie znajduje się komputer o tym adresie.</span><span class="sxs-lookup"><span data-stu-id="163ad-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="163ad-144">Skomplikowany czynników, takich jak przenośnych dostawców i sieci VPN często bardzo wydawania adresów IP z puli centralnej daleko od których urządzenie klienckie będzie faktycznie używana.</span><span class="sxs-lookup"><span data-stu-id="163ad-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="163ad-145">Mając na uwadze powyższe, konwertowania adresu IP do fizycznej lokalizacji jest starań, na podstawie danych śledzenia, dane rejestru, odwrotnej wyszukiwań i inne informacje.</span><span class="sxs-lookup"><span data-stu-id="163ad-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
