---
title: "Ochrona danych osobowych z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ochrona danych osobistych, przy użyciu Centrum zabezpieczeń Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="986cd-103">Ochrona danych osobowych z atakami i naruszeń: Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="986cd-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="986cd-104">Ten artykuł pomoże Ci zrozumieć sposób korzystania z Centrum zabezpieczeń Azure do ochrony danych osobowych przed naruszeniami i ataków.</span><span class="sxs-lookup"><span data-stu-id="986cd-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="986cd-105">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="986cd-105">Scenario</span></span> 

<span data-ttu-id="986cd-106">Rejs duże przedsiębiorstwo, siedzibą w Stanach Zjednoczonych rozwija operacjach oferowanie trasy w DS i Bałtyckiego mórz oraz brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="986cd-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="986cd-107">Aby pomóc w tych działań, ustawił mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="986cd-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="986cd-108">Przez firmę Microsoft Azure do przechowywania danych firmowych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="986cd-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="986cd-109">Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej.</span><span class="sxs-lookup"><span data-stu-id="986cd-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="986cd-110">Zawiera również zasoby ludzkie informacji takich jak:</span><span class="sxs-lookup"><span data-stu-id="986cd-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="986cd-111">Adresy</span><span class="sxs-lookup"><span data-stu-id="986cd-111">Addresses</span></span>
- <span data-ttu-id="986cd-112">Numery telefonów</span><span class="sxs-lookup"><span data-stu-id="986cd-112">Phone numbers</span></span>
- <span data-ttu-id="986cd-113">Numery identyfikacyjne podatku</span><span class="sxs-lookup"><span data-stu-id="986cd-113">Tax identification numbers</span></span>
- <span data-ttu-id="986cd-114">Inne informacje</span><span class="sxs-lookup"><span data-stu-id="986cd-114">Medical information</span></span>

<span data-ttu-id="986cd-115">Wiersz rejs zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność.</span><span class="sxs-lookup"><span data-stu-id="986cd-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="986cd-116">Pracownikom firmy dostępu do sieci w oddziałach firmy i podróży agentów na całym świecie mają dostęp do niektórych zasobów firmy.</span><span class="sxs-lookup"><span data-stu-id="986cd-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="986cd-117">Dane osobowe są przesyłane w sieci między te lokalizacje i centrum danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="986cd-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="986cd-118">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="986cd-118">Problem statement</span></span>

<span data-ttu-id="986cd-119">Firma jest zajmującym się zagrożenie atakami ich zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="986cd-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="986cd-120">Chcą wyeliminowania zagrożenia pracowników i klientów danych osobowych do osoby nieupoważnione.</span><span class="sxs-lookup"><span data-stu-id="986cd-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="986cd-121">Chcą, aby uzyskać wskazówki dotyczące zarówno związanych z zapobieganiem i odpowiedzi/korygowania, jak i efektywny sposób monitorowania bieżących bezpieczeństwa zasobów w chmurze.</span><span class="sxs-lookup"><span data-stu-id="986cd-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="986cd-122">Muszą one silne linię obrony przed atakami współczesnych zaawansowane i organizowane.</span><span class="sxs-lookup"><span data-stu-id="986cd-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="986cd-123">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="986cd-123">Company goal</span></span>

<span data-ttu-id="986cd-124">Jest jednym z celów firmy można zapewnić poufności danych osobowych pracowników i klientów, aby chronić go przed zagrożeniami.</span><span class="sxs-lookup"><span data-stu-id="986cd-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="986cd-125">Jest jednym z celów ich natychmiast odpowiadać na znaki zmniejszyć skuteczność naruszenia.</span><span class="sxs-lookup"><span data-stu-id="986cd-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="986cd-126">Wymaga to sposób ocenić bieżący stan zabezpieczeń, identyfikowanie narażone konfiguracje i usuwać z nich.</span><span class="sxs-lookup"><span data-stu-id="986cd-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="986cd-127">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="986cd-127">Solutions</span></span>

<span data-ttu-id="986cd-128">Microsoft Azure Security Center (ASC) zapewnia zabezpieczenia zintegrowane monitorowanie i zasady rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="986cd-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="986cd-129">Zapewnia łatwy w użyciu i skuteczne zapobieganie, wykrywanie i odpowiedzi możliwości.</span><span class="sxs-lookup"><span data-stu-id="986cd-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="986cd-130">Zapobieganie</span><span class="sxs-lookup"><span data-stu-id="986cd-130">Prevention</span></span>

<span data-ttu-id="986cd-131">ASC pomaga zapobiegać naruszeń, należy włączyć ustawienie zasad zabezpieczeń, dostęp w czasie i zaimplementować zalecenia dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="986cd-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="986cd-132">Zasady zabezpieczeń określają zestaw mechanizmów kontrolnych, zalecane dla zasobów w określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="986cd-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="986cd-133">Tylko w czasie może służyć do blokowania ruchu przychodzącego na maszynach wirtualnych platformy Azure, ograniczenia narażenia na ataki.</span><span class="sxs-lookup"><span data-stu-id="986cd-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="986cd-134">Zalecenia dotyczące zabezpieczeń są tworzone przez ASC po przeanalizowaniu stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="986cd-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="986cd-135">Jak ustawić zasady zabezpieczeń w ASC?</span><span class="sxs-lookup"><span data-stu-id="986cd-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="986cd-136">Zasady zabezpieczeń można skonfigurować dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="986cd-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="986cd-137">Aby zmodyfikować zasady zabezpieczeń, musisz być właścicielem lub współautorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="986cd-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="986cd-138">W portalu Azure wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="986cd-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="986cd-139">Wybierz **zasad** na pulpicie nawigacyjnym ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="986cd-140">Wybierz subskrypcję, na którym chcesz włączyć zasady.</span><span class="sxs-lookup"><span data-stu-id="986cd-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="986cd-141">Wybierz **zasady zapobiegania** skonfigurować zasady dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="986cd-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="986cd-142">**Zbieranie danych z maszyn wirtualnych** powinien być ustawiony na **na.**</span><span class="sxs-lookup"><span data-stu-id="986cd-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="986cd-143">W **zasady zapobiegania** opcji wybierz **na** Aby włączyć zalecenia dotyczące zabezpieczeń, które są istotne dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="986cd-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="986cd-144">Aby uzyskać szczegółowe instrukcje i informacje o wszystkich zaleceń dotyczących zasad, które mogą być włączone, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="986cd-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="986cd-145">Jak skonfigurować tylko w czasie dostępu (JIT)?</span><span class="sxs-lookup"><span data-stu-id="986cd-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="986cd-146">Po włączeniu JIT Centrum zabezpieczeń blokuje ruch przychodzący na maszynach wirtualnych platformy Azure przez tworzenie reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="986cd-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="986cd-147">Należy wybrać porty na maszynie Wirtualnej, do którego będzie można zablokować ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="986cd-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="986cd-148">Aby korzystać z dostępu JIT, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="986cd-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="986cd-149">Wybierz **bezpośrednio w kafelku dostęp maszyny Wirtualnej czasu** w bloku ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="986cd-150">Wybierz **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="986cd-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="986cd-151">W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć.</span><span class="sxs-lookup"><span data-stu-id="986cd-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="986cd-152">Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="986cd-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="986cd-153">Wybierz **włączyć JIT** na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="986cd-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="986cd-154">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="986cd-154">Select **Save**.</span></span>

<span data-ttu-id="986cd-155">Następnie widać domyślnych portów, które ASC zaleca włączana na potrzeby JIT.</span><span class="sxs-lookup"><span data-stu-id="986cd-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="986cd-156">Można także dodać i skonfigurować nowy port, na którym chcesz włączyć tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="986cd-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="986cd-157">**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** kafelka w Centrum zabezpieczeń jest wyświetlana liczba maszyn wirtualnych skonfigurowana dla dostępu JIT.</span><span class="sxs-lookup"><span data-stu-id="986cd-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="986cd-158">Ponadto liczba żądań zatwierdzonych dostępu w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="986cd-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="986cd-159">W jaki sposób to zrobić oraz dodatkowe informacje na temat tylko w czasie dostępu, zobacz [zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="986cd-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="986cd-160">Jak wdrożyć ASC zalecenia dotyczące zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="986cd-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="986cd-161">Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia.</span><span class="sxs-lookup"><span data-stu-id="986cd-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="986cd-162">Przewodnik dotyczący zaleceń prowadzi użytkownika przez proces konfigurowania wymaganych kontrolek.</span><span class="sxs-lookup"><span data-stu-id="986cd-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="986cd-163">Wybierz **zalecenia** kafelka na pulpicie nawigacyjnym ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="986cd-164">Wyświetl zalecenia, które są wyświetlane w formacie tabeli, w której każdy wiersz zawiera jeden zalecenia.</span><span class="sxs-lookup"><span data-stu-id="986cd-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="986cd-165">Filtr zaleceń, wybierz opcję **filtru** i wybierz ważność i stan wartości, które chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="986cd-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="986cd-166">Aby odrzucić rekomendację, która nie ma zastosowania, kliknij prawym przyciskiem myszy i wybierz **odrzucenia.**</span><span class="sxs-lookup"><span data-stu-id="986cd-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="986cd-167">Należy ocenić, które zalecenie powinny być stosowane najpierw.</span><span class="sxs-lookup"><span data-stu-id="986cd-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="986cd-168">Stosować zalecenia w kolejności priorytetów.</span><span class="sxs-lookup"><span data-stu-id="986cd-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="986cd-169">Listę możliwych zaleceń i przewodników dotyczących stosowania każdego zawiera [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="986cd-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="986cd-170">Wykrywanie i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="986cd-170">Detection and Response</span></span>

<span data-ttu-id="986cd-171">Wykrywanie i odpowiedzi go razem, jak należy jak najszybciej po wykryciu zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="986cd-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="986cd-172">Wykrywanie zagrożeń ASC polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, sieci i rozwiązań partnerskich połączonych.</span><span class="sxs-lookup"><span data-stu-id="986cd-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="986cd-173">ASC szybko może aktualizować algorytmy wykrywania, jak osoby atakujące wersji nowy, coraz bardziej zaawansowany luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="986cd-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="986cd-174">Aby uzyskać szczegółowe informacje dotyczące sposobu działania wykrywanie zagrożeń ASC firmy, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="986cd-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="986cd-175">Jak zarządzać i reagowania na alerty zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="986cd-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="986cd-176">Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlana w Centrum zabezpieczeń oraz informacje potrzebne do szybkiego analizowania problemu.</span><span class="sxs-lookup"><span data-stu-id="986cd-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="986cd-177">Centrum zabezpieczeń zawiera także zalecenia dotyczące skorygować atak.</span><span class="sxs-lookup"><span data-stu-id="986cd-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="986cd-178">Aby zarządzać alerty zabezpieczeń, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="986cd-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="986cd-179">Wybierz **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="986cd-180">To przedstawia szczegółowe informacje o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="986cd-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="986cd-181">Aby filtrować alerty na podstawie daty, stanu i ważności, wybierz **filtru** , a następnie wybierz wartości, które mają być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="986cd-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="986cd-182">Aby odpowiedzieć alertu, zaznacz go i przejrzyj informacje, a następnie wybierz zaatakowany zasób.</span><span class="sxs-lookup"><span data-stu-id="986cd-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="986cd-183">W **opis** pola, zobaczysz szczegółowe informacje, łącznie z zalecanych czynności naprawczych.</span><span class="sxs-lookup"><span data-stu-id="986cd-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="986cd-184">Aby uzyskać szczegółowe instrukcje dotyczące reagowanie na alerty zabezpieczeń, zobacz [reagowanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure i zarządzanie nimi.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="986cd-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="986cd-185">Aby uzyskać dalszą pomoc w badania alertów zabezpieczeń firmy można zintegrować ASC alerty z własnego rozwiązania SIEM, za pomocą [integracji dziennika Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="986cd-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="986cd-186">Jak zarządzać przypadki naruszenia zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="986cd-186">How do I manage security incidents?</span></span>

<span data-ttu-id="986cd-187">Zdarzenia zabezpieczeń ASC, to agregacji wszystkich alertów dla zasobu, które są wyrównane z wzorców łańcucha kill.</span><span class="sxs-lookup"><span data-stu-id="986cd-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="986cd-188">Zdarzenie wyświetli listę powiązanych alertów, co pozwala uzyskać więcej informacji na temat każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="986cd-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="986cd-189">Zdarzenia są wyświetlane w kafelku alerty zabezpieczeń i bloku.</span><span class="sxs-lookup"><span data-stu-id="986cd-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="986cd-190">Aby przejrzeć i zarządzania incydentami zabezpieczeń, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="986cd-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="986cd-191">Wybierz **alerty zabezpieczeń** kafelka.</span><span class="sxs-lookup"><span data-stu-id="986cd-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="986cd-192">w przypadku wykrycia zdarzenia zabezpieczeń będą wyświetlane w obszarze wykresu alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="986cd-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="986cd-193">Jej ikonę, która różni się od innych alertów.</span><span class="sxs-lookup"><span data-stu-id="986cd-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="986cd-194">Wybierz zdarzenie, aby wyświetlić więcej szczegółów dotyczących tego zdarzenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="986cd-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="986cd-195">Dodatkowe szczegóły obejmują jego pełny opis, jego ważność, jego bieżący stan, zaatakowanych zasobów, czynności korygujące zdarzenia i alerty, które wchodzą w skład tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="986cd-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="986cd-196">Można filtrować, aby wyświetlić **tylko zdarzenia**, **alerty tylko**, lub **zarówno**.</span><span class="sxs-lookup"><span data-stu-id="986cd-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="986cd-197">Jak uzyskać dostępu do raportu analizy zagrożeń</span><span class="sxs-lookup"><span data-stu-id="986cd-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="986cd-198">ASC analizuje informacje z wielu źródeł do identyfikowania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="986cd-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="986cd-199">Aby pomóc odpowiedzi na zdarzenia zespoły zbadać i eliminowanie zagrożeń, Centrum zabezpieczeń zawiera raport analizy zagrożeń, który zawiera informacje dotyczące zagrożenia, które zostało wykryte.</span><span class="sxs-lookup"><span data-stu-id="986cd-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="986cd-200">Centrum zabezpieczeń zawiera trzy raporty zagrożenia, które mogą się różnić na atak.</span><span class="sxs-lookup"><span data-stu-id="986cd-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="986cd-201">Dostępne raporty:</span><span class="sxs-lookup"><span data-stu-id="986cd-201">The reports available are:</span></span>

- <span data-ttu-id="986cd-202">Raport grupy działań: zawiera głębokie dives do osoby atakujące, ich cele i taktyk.</span><span class="sxs-lookup"><span data-stu-id="986cd-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="986cd-203">Raport kampanii: koncentruje się na szczegóły ataku określonej kampanii.</span><span class="sxs-lookup"><span data-stu-id="986cd-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="986cd-204">Raport podsumowania zagrożeń: obejmuje wszystkie elementy w poprzednich dwóch raportów.</span><span class="sxs-lookup"><span data-stu-id="986cd-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="986cd-205">Informacje tego typu jest bardzo przydatny podczas procesu odpowiedzi na zdarzenia w przypadku, gdy istnieje trwającą dochodzenia zrozumienie źródło ataku, motywacji osoby atakującej i co zrobić, aby zminimalizować ten problem, przenoszenie do przodu.</span><span class="sxs-lookup"><span data-stu-id="986cd-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="986cd-206">Aby uzyskać dostęp do raportu analizy zagrożeń, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="986cd-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="986cd-207">Wybierz **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="986cd-208">Wybierz alert zabezpieczeń, dla którego chcesz uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="986cd-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="986cd-209">W **raporty** kliknij łącze do raportu analizy zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="986cd-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="986cd-210">Spowoduje to otwarcie pliku PDF, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="986cd-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="986cd-211">Aby uzyskać dodatkowe informacje na temat raportu analizy zagrożeń ASC, zobacz [raport analizy zagrożeń z Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="986cd-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="986cd-212">Ocena</span><span class="sxs-lookup"><span data-stu-id="986cd-212">Assessment</span></span>

<span data-ttu-id="986cd-213">Aby pomóc w testowania, oceny i ocenie strukturę bezpieczeństwa, ASC zapewnia oceny luk w zabezpieczeniach zintegrowane z Qualys agentów chmurze jako część jej składników zalecenia dotyczące maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="986cd-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="986cd-214">Qualys agent raporty Qualys platformy zarządzania, który następnie wysyła luki w zabezpieczeniach i kondycji danych monitorowania z powrotem do ASC danych luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="986cd-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="986cd-215">Zalecenie, aby dodać rozwiązanie do oceny luk w zabezpieczeniach jest wyświetlany w **zalecenia** bloku na pulpicie nawigacyjnym ASC.</span><span class="sxs-lookup"><span data-stu-id="986cd-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="986cd-216">Po zainstalowaniu rozwiązania do oceny luk w zabezpieczeniach na docelowej maszynie wirtualnej usługa Security Center skanuje maszynę wirtualną w celu wykrycia i zidentyfikowania luk w zabezpieczeniach systemu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="986cd-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="986cd-217">Wykryte problemy zostaną wyświetlone w obszarze **Virtual Machines Recommendations** (Zalecenia dotyczące maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="986cd-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="986cd-218">Jak wdrożyć rozwiązanie do oceny luk w zabezpieczeniach?</span><span class="sxs-lookup"><span data-stu-id="986cd-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="986cd-219">Jeśli maszyna wirtualna nie ma już wdrożone rozwiązanie do oceny luk w zabezpieczeniach zintegrowanego, Centrum zabezpieczeń zaleca się ona zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="986cd-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="986cd-220">Na pulpicie nawigacyjnym ASC na **zalecenia** bloku, wybierz opcję **Dodaj rozwiązanie do oceny luk w zabezpieczeniach.**</span><span class="sxs-lookup"><span data-stu-id="986cd-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="986cd-221">Wybierz maszyny wirtualne, które chcesz zainstalować rozwiązanie do oceny luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="986cd-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="986cd-222">Polecenie **zainstalowania na maszynach wirtualnych [numer].**</span><span class="sxs-lookup"><span data-stu-id="986cd-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="986cd-223">Wybierz rozwiązanie partnerskie w portalu Azure Marketplace, lub na podstawie **użyć istniejącego rozwiązania,** wybierz **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="986cd-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="986cd-224">Można włączyć ustawienia automatycznej aktualizacji lub wyłączyć **rozwiązań partnerskich** bloku.</span><span class="sxs-lookup"><span data-stu-id="986cd-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="986cd-225">Aby uzyskać dalsze instrukcje dotyczące implementowania rozwiązania oceny luk w zabezpieczeniach, zobacz [oceny luk w zabezpieczeniach w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="986cd-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="986cd-226">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="986cd-226">Next steps</span></span>

- [<span data-ttu-id="986cd-227">Przewodnik Szybki start dotyczący Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="986cd-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="986cd-228">Wprowadzenie do Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="986cd-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="986cd-229">Integrowanie z integracją dzienników Azure alerty Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="986cd-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="986cd-230">Zwiększenie wydajności Centrum zabezpieczeń Azure z oceny luk w zabezpieczeniach zintegrowane</span><span class="sxs-lookup"><span data-stu-id="986cd-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
