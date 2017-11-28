---
title: "aaaAzure Active Directory raportowania — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="63319-103">Usługa Azure Active Directory raportowania — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="63319-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="63319-104">Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) dotyczące raportowania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="63319-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="63319-105">Aby uzyskać więcej informacji, zobacz [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63319-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="63319-106">**Pytanie: co to jest hello przechowywanie danych o Dzienniki aktywności (inspekcji i logowania) w portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="63319-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="63319-107">**Odpowiedź:** 7 dni danych udostępniamy klientom wolnego i przełączając tooan Azure AD Premium 1 lub Premium 2 licencji, użytkownik może uzyskać dostępu do danych zapasowej too30 dni.</span><span class="sxs-lookup"><span data-stu-id="63319-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="63319-108">Aby uzyskać więcej szczegółów na przechowywania, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="63319-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="63319-109">**Pytanie: jak długo trwa do momentu wyświetlane dane o aktywności powitania po zakończeniu I Moje zadania?**</span><span class="sxs-lookup"><span data-stu-id="63319-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="63319-110">**Odpowiedź:** dzienników inspekcji działania mają opóźnienia, począwszy od godziny tooan w ciągu 15 minut.</span><span class="sxs-lookup"><span data-stu-id="63319-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="63319-111">Dzienniki aktywności logowania ma opóźnienia — od 15 minut większość rekordów oraz too2 godzin do kilku rekordów.</span><span class="sxs-lookup"><span data-stu-id="63319-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="63319-112">**Pytanie: należy toobe działania administratora globalnego toosee hello dzienników hello portalu Azure lub tooget dane za pośrednictwem hello interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="63319-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="63319-113">**Odpowiedź:** Nie.</span><span class="sxs-lookup"><span data-stu-id="63319-113">**A:** No.</span></span> <span data-ttu-id="63319-114">Może to być **czytnika zabezpieczeń**, **administratora zabezpieczeń** lub **administratora globalnego** toosee dane w portalu Azure lub dostępu do niego za pośrednictwem hello interfejsu API raportowania.</span><span class="sxs-lookup"><span data-stu-id="63319-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="63319-115">**Pytanie: czy można uzyskać informacji dziennika aktywności usługi Office 365 za pomocą portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="63319-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="63319-116">**Odpowiedź:** mimo że działania usługi Office 365 i Azure AD działania dzienniki udziału dużej ilości zasobów katalogu hello, jeśli chcesz pełnego widoku hello Dzienniki aktywności usługi Office 365, należy przejść informacje dziennika toohello Centrum administracyjne usługi Office 365 tooget Office 365 działania.</span><span class="sxs-lookup"><span data-stu-id="63319-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="63319-117">**Pytanie: co zrobić interfejsów API używać tooget informacji o dziennikach Office 365 działania?**</span><span class="sxs-lookup"><span data-stu-id="63319-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="63319-118">**A:** Użyj hello interfejsów API usługi Office 365 Management tooaccess hello [Office 365 działanie logowania za pośrednictwem interfejsu API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="63319-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="63319-119">**Pytanie: jak wiele rekordów I można pobrać z portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="63319-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="63319-120">**Odpowiedź:** można pobrać too120K rekordów z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63319-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="63319-121">rekordy Hello są sortowane według *najnowszych* i domyślnie uzyskać rekordów hello najnowszych K 120.</span><span class="sxs-lookup"><span data-stu-id="63319-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="63319-122">**Pytanie: jak wiele rekordów można zbadać za pomocą działania hello interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="63319-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="63319-123">**Odpowiedź:** można zbadać too1 miliony rekordów (Jeśli nie jest używany operator top hello, sortującej rekordu hello przez większość ostatnie).</span><span class="sxs-lookup"><span data-stu-id="63319-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="63319-124">Użyj operatora "top" hello, mogą wysyłać zapytania too500K rekordów.</span><span class="sxs-lookup"><span data-stu-id="63319-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="63319-125">Przykładowe zapytania w sposób toouse hello interfejsu API w tym miejscu można znaleźć [tutaj](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="63319-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="63319-126">**Pytanie: jak uzyskać licencję premium?**</span><span class="sxs-lookup"><span data-stu-id="63319-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="63319-127">**A:** zobacz [wprowadzenie do korzystania z usługi Azure Active Directory Premium](active-directory-get-started-premium.md) dla toothis odpowiedzi na pytanie.</span><span class="sxs-lookup"><span data-stu-id="63319-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="63319-128">**Pytanie: jak najszybciej Zobacz dane działań po otrzymaniu licencji premium?**</span><span class="sxs-lookup"><span data-stu-id="63319-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="63319-129">**Odpowiedź:** Jeśli masz już dane działań jako wolne licencji, a następnie widać hello tych samych danych.</span><span class="sxs-lookup"><span data-stu-id="63319-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="63319-130">Jeśli nie masz żadnych danych, ich może zająć jeden lub dwa dni.</span><span class="sxs-lookup"><span data-stu-id="63319-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="63319-131">**Pytanie: wyświetlane dane z ostatniego miesiąca po otrzymaniu licencji usługi Azure AD premium?**</span><span class="sxs-lookup"><span data-stu-id="63319-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="63319-132">**Odpowiedź:** ostatnio przełączane tooa wersji Premium (w tym wersja próbna) można początkowo Zobacz więcej dni too7 danych.</span><span class="sxs-lookup"><span data-stu-id="63319-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="63319-133">Gdy dane zebrane, zobaczysz too30 dni.</span><span class="sxs-lookup"><span data-stu-id="63319-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="63319-134">**Pytanie: Brak zdarzeń ryzyko w ochronę tożsamości, ale nie widzę odpowiedniego logowania w hello wszystkie sesje logowania. Jest to oczekiwane?**</span><span class="sxs-lookup"><span data-stu-id="63319-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="63319-135">**Odpowiedź:** tak, Identity Protection ocenia ryzyko dla wszystkich przepływów uwierzytelniania czy jeśli interakcyjnego lub nieinterakcyjnym.</span><span class="sxs-lookup"><span data-stu-id="63319-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="63319-136">Jednak wszystkie sesje logowania tylko przedstawia tylko hello logowania interakcyjnego.</span><span class="sxs-lookup"><span data-stu-id="63319-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="63319-137">**Pytanie: jak można pobrać raportu "Użytkownicy oflagowani ryzyka" hello, w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="63319-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="63319-138">**A:** hello opcja toodownload *użytkownicy oflagowani ryzyka* raportu zostanie dodany wkrótce.</span><span class="sxs-lookup"><span data-stu-id="63319-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="63319-139">**Pytanie: jak dowiedzieć, dlaczego logowania lub użytkownikiem zostało oznaczone ryzykowne w hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="63319-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="63319-140">**Odpowiedź:** klienci wersji Premium można dowiedzieć się więcej o hello podstawowy zdarzenia o podwyższonym ryzyku, klikając użytkownika hello w "Użytkownicy oflagowani ryzyka" lub klikając na powitania "Ryzykowne sesje logowania".</span><span class="sxs-lookup"><span data-stu-id="63319-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="63319-141">Klienci bezpłatne i podstawowych wydanie uzyskać toosee hello zagrożonych użytkowników i logowania bez hello podstawowych informacji o zdarzeniu ryzyka.</span><span class="sxs-lookup"><span data-stu-id="63319-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="63319-142">**Pytanie: jak adresy IP są obliczane w hello logowania i logowania ryzykowne raport?**</span><span class="sxs-lookup"><span data-stu-id="63319-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="63319-143">**Odpowiedź:** adresy IP są przydzielane w taki sposób, że brak ostatecznego połączenia między adresu IP i gdzie fizycznie znajduje się komputer hello przy użyciu tego adresu.</span><span class="sxs-lookup"><span data-stu-id="63319-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="63319-144">Skomplikowany czynników, takich jak przenośnych dostawców i sieci VPN często bardzo wydawania adresów IP z puli centralnej daleko od gdzie powitania klienta urządzenia są rzeczywiście używane.</span><span class="sxs-lookup"><span data-stu-id="63319-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="63319-145">Podana hello powyżej, konwertowanie fizycznej lokalizacji tooa adres IP jest starań, na podstawie danych śledzenia, dane rejestru, odwrotnej wyszukiwań i inne informacje.</span><span class="sxs-lookup"><span data-stu-id="63319-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
