---
title: "dane osobowe aaaProtect z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="e5721-103">Ochrona danych osobowych z atakami i naruszeń: Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="e5721-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="e5721-104">Ten artykuł pomoże Ci zrozumieć, jak dane osobowe tooprotect Centrum zabezpieczeń Azure toouse z naruszeń i ataków.</span><span class="sxs-lookup"><span data-stu-id="e5721-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="e5721-105">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="e5721-105">Scenario</span></span> 

<span data-ttu-id="e5721-106">Firma rejs dużych, siedzibą hello Stanów Zjednoczonych, rozwija trasy toooffer jego operacji w hello Śródziemnego i Bałtyckiego mórz oraz hello brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="e5721-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="e5721-107">toohelp w tych działań, uzyskała mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i hello Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="e5721-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="e5721-108">Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="e5721-109">Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej.</span><span class="sxs-lookup"><span data-stu-id="e5721-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="e5721-110">Zawiera również zasoby ludzkie informacji takich jak:</span><span class="sxs-lookup"><span data-stu-id="e5721-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="e5721-111">Adresy</span><span class="sxs-lookup"><span data-stu-id="e5721-111">Addresses</span></span>
- <span data-ttu-id="e5721-112">Numery telefonów</span><span class="sxs-lookup"><span data-stu-id="e5721-112">Phone numbers</span></span>
- <span data-ttu-id="e5721-113">Numery identyfikacyjne podatku</span><span class="sxs-lookup"><span data-stu-id="e5721-113">Tax identification numbers</span></span>
- <span data-ttu-id="e5721-114">Inne informacje</span><span class="sxs-lookup"><span data-stu-id="e5721-114">Medical information</span></span>

<span data-ttu-id="e5721-115">wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność.</span><span class="sxs-lookup"><span data-stu-id="e5721-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="e5721-116">Pracownikom firmy dostępu hello sieci z biurach zdalnych i agentów podróży hello firmy znajdujących się wokół Witaj świecie mają dostęp do zasobów firmowych toosome.</span><span class="sxs-lookup"><span data-stu-id="e5721-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="e5721-117">Dane osobowe są przesyłane w sieci hello między tymi lokalizacjami i centrum danych firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="e5721-118">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="e5721-118">Problem statement</span></span>

<span data-ttu-id="e5721-119">Witaj firmy zależy od zagrożeń hello ataków na ich zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5721-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="e5721-120">Chcą narażenia tooprevent osób toounauthorized danych osobowych pracowników i klientów.</span><span class="sxs-lookup"><span data-stu-id="e5721-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="e5721-121">Chcą, aby uzyskać wskazówki dotyczące zarówno związanych z zapobieganiem i odpowiedzi/korygowania, a także efektywny sposób toomonitor hello trwającą bezpieczeństwa zasobów w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e5721-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="e5721-122">Muszą one silne linię obrony przed atakami współczesnych zaawansowane i organizowane.</span><span class="sxs-lookup"><span data-stu-id="e5721-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="e5721-123">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="e5721-123">Company goal</span></span>

<span data-ttu-id="e5721-124">Jednym z celów firmy hello jest tooensure hello prywatności danych osobowych pracowników i klientów, aby chronić go przed zagrożeniami.</span><span class="sxs-lookup"><span data-stu-id="e5721-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="e5721-125">Jest jednym z celów ich toorespond, natychmiast toosigns toomitigate naruszenia hello wpływ.</span><span class="sxs-lookup"><span data-stu-id="e5721-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="e5721-126">Wymaga to sposób tooassess hello bieżący stan zabezpieczeń, identyfikację narażone konfiguracji i usuwać z nich.</span><span class="sxs-lookup"><span data-stu-id="e5721-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="e5721-127">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e5721-127">Solutions</span></span>

<span data-ttu-id="e5721-128">Microsoft Azure Security Center (ASC) zapewnia zabezpieczenia zintegrowane monitorowanie i zasady rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e5721-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="e5721-129">Zapewnia łatwy w użyciu i skuteczne zapobieganie, wykrywanie i odpowiedzi możliwości.</span><span class="sxs-lookup"><span data-stu-id="e5721-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="e5721-130">Zapobieganie</span><span class="sxs-lookup"><span data-stu-id="e5721-130">Prevention</span></span>

<span data-ttu-id="e5721-131">ASC pomaga zapobiec naruszeń włączając tooset zasady zabezpieczeń, dostęp w czasie i zaimplementować zalecenia dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5721-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="e5721-132">Zasady zabezpieczeń określają hello zestaw kontrolek zalecane dla zasobów w hello określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="e5721-133">Tylko w czasie dostępu może być używane toolock tooyour ruch przychodzący maszynach wirtualnych platformy Azure, zmniejszenie zagrożeń tooattacks w dół.</span><span class="sxs-lookup"><span data-stu-id="e5721-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="e5721-134">Zalecenia dotyczące zabezpieczeń są tworzone przez ASC po przeanalizowaniu hello stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5721-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="e5721-135">Jak ustawić zasady zabezpieczeń w ASC?</span><span class="sxs-lookup"><span data-stu-id="e5721-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="e5721-136">Zasady zabezpieczeń można skonfigurować dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="e5721-137">toomodify zasady zabezpieczeń, musi być właścicielem lub współautorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="e5721-138">W portalu Azure hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e5721-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="e5721-139">Wybierz **zasad** hello ASC w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e5721-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="e5721-140">Wybierz subskrypcję hello, na którym ma zostać tooenable hello zasad.</span><span class="sxs-lookup"><span data-stu-id="e5721-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="e5721-141">Wybierz **zasady zapobiegania** tooconfigure zasady dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="e5721-142">**Zbieranie danych z maszyn wirtualnych** powinna być ustawiona zbyt**na.**</span><span class="sxs-lookup"><span data-stu-id="e5721-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="e5721-143">W hello **zasady zapobiegania** opcji wybierz **na** tooenable hello zalecenia dotyczące zabezpieczeń związane hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="e5721-144">Aby uzyskać szczegółowe instrukcje i informacje o wszystkich hello zaleceń dotyczących zasad, które mogą być włączone, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="e5721-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="e5721-145">Jak skonfigurować tylko w czasie dostępu (JIT)?</span><span class="sxs-lookup"><span data-stu-id="e5721-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="e5721-146">Po włączeniu JIT Centrum zabezpieczeń blokuje ruch przychodzący tooyour maszynach wirtualnych platformy Azure przez tworzenie reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="e5721-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="e5721-147">Wybierz porty hello na powitania toowhich maszyny Wirtualnej zostanie zablokowana ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="e5721-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="e5721-148">toouse JIT dostępu, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e5721-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="e5721-149">Wybierz hello **bezpośrednio w kafelku dostęp maszyny Wirtualnej czas** na powitania ASC bloku.</span><span class="sxs-lookup"><span data-stu-id="e5721-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="e5721-150">Wybierz hello **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="e5721-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="e5721-151">W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable.</span><span class="sxs-lookup"><span data-stu-id="e5721-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="e5721-152">Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5721-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="e5721-153">Wybierz **włączyć JIT** na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5721-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="e5721-154">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e5721-154">Select **Save**.</span></span>

<span data-ttu-id="e5721-155">Następnie można zobaczyć hello domyślnych portów, które ASC zaleca włączana na potrzeby JIT.</span><span class="sxs-lookup"><span data-stu-id="e5721-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="e5721-156">Można również dodać i skonfigurować nowy port, na którym ma zostać hello tooenable tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="e5721-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="e5721-157">Witaj **bezpośrednio w dostęp do maszyny Wirtualnej czasu** kafelka w Centrum zabezpieczeń hello pokazuje liczbę hello skonfigurowana dla dostępu JIT maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5721-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="e5721-158">Zawiera także hello liczba żądań zatwierdzonych dostępu wprowadzone w hello ostatniego tygodnia.</span><span class="sxs-lookup"><span data-stu-id="e5721-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="e5721-159">Aby uzyskać instrukcje dotyczące toodo, oraz dodatkowe informacje na temat tylko w czasie dostępu, zobacz [zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="e5721-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="e5721-160">Jak wdrożyć ASC zalecenia dotyczące zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="e5721-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="e5721-161">Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia.</span><span class="sxs-lookup"><span data-stu-id="e5721-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="e5721-162">zalecenia Hello pomocne hello proces konfigurowania kontrolek hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="e5721-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="e5721-163">Wybierz hello **zalecenia** kafelka na pulpicie nawigacyjnym ASC hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="e5721-164">Wyświetl zalecenia hello, które są wyświetlane w formacie tabeli, w której każdy wiersz zawiera jeden zalecenia.</span><span class="sxs-lookup"><span data-stu-id="e5721-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="e5721-165">Wybierz zalecenia toofilter **filtru** i wybierz hello ważność i stan wartości mają toosee.</span><span class="sxs-lookup"><span data-stu-id="e5721-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="e5721-166">toodismiss rekomendację, która nie ma zastosowania, można kliknij prawym przyciskiem myszy i wybierz **odrzucenia.**</span><span class="sxs-lookup"><span data-stu-id="e5721-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="e5721-167">Należy ocenić, które zalecenie powinny być stosowane najpierw.</span><span class="sxs-lookup"><span data-stu-id="e5721-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="e5721-168">Stosować zalecenia hello w kolejności priorytetów.</span><span class="sxs-lookup"><span data-stu-id="e5721-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="e5721-169">Listę możliwych zalecenia i przewodników dotyczących tooapply, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="e5721-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="e5721-170">Wykrywanie i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e5721-170">Detection and Response</span></span>

<span data-ttu-id="e5721-171">Wykrywanie i odpowiedzi go razem można dowolnie toorespond możliwie jak najszybciej po wykryciu zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="e5721-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="e5721-172">Wykrywanie zagrożeń ASC polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych.</span><span class="sxs-lookup"><span data-stu-id="e5721-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="e5721-173">ASC szybko może aktualizować algorytmy wykrywania, jak osoby atakujące wersji nowy, coraz bardziej zaawansowany luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="e5721-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="e5721-174">Aby uzyskać szczegółowe informacje dotyczące sposobu działania wykrywanie zagrożeń ASC firmy, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="e5721-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="e5721-175">Jak zarządzać i odpowiadanie na alerty toosecurity?</span><span class="sxs-lookup"><span data-stu-id="e5721-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="e5721-176">Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem.</span><span class="sxs-lookup"><span data-stu-id="e5721-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="e5721-177">Centrum zabezpieczeń zawiera także zalecenia dotyczące tooremediate atak.</span><span class="sxs-lookup"><span data-stu-id="e5721-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="e5721-178">alerty zabezpieczeń, wykonaj następujące hello toomanage:</span><span class="sxs-lookup"><span data-stu-id="e5721-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="e5721-179">Wybierz hello **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="e5721-180">To przedstawia szczegółowe informacje o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="e5721-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="e5721-181">Wybierz alerty toofilter na podstawie daty, stanu i ważności, **filtru** a następnie wybierz wartości hello ma toosee.</span><span class="sxs-lookup"><span data-stu-id="e5721-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="e5721-182">toorespond tooan alert, zaznacz go i przejrzyj informacje hello, a następnie wybierz hello zaatakowany zasób.</span><span class="sxs-lookup"><span data-stu-id="e5721-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="e5721-183">W hello **opis** pola, zobaczysz szczegółowe informacje, łącznie z zalecanych czynności naprawczych.</span><span class="sxs-lookup"><span data-stu-id="e5721-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="e5721-184">Aby uzyskać szczegółowe instrukcje dotyczące odpowiada alerty toosecurity, zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="e5721-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="e5721-185">Aby uzyskać dalszą pomoc w badania alertów zabezpieczeń firmy hello można zintegrować ASC alerty z własnego rozwiązania SIEM, za pomocą [integracji dziennika Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="e5721-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="e5721-186">Jak zarządzać przypadki naruszenia zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="e5721-186">How do I manage security incidents?</span></span>

<span data-ttu-id="e5721-187">Zdarzenia zabezpieczeń ASC, to agregacji wszystkich alertów dla zasobu, które są wyrównane z wzorców łańcucha kill.</span><span class="sxs-lookup"><span data-stu-id="e5721-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="e5721-188">Zdarzenie będzie ujawnić hello listę powiązanych alertów, dzięki czemu możesz tooobtain więcej informacji na temat każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e5721-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="e5721-189">Zdarzenia są wyświetlane w powitalne Kafelek alerty zabezpieczeń i bloku.</span><span class="sxs-lookup"><span data-stu-id="e5721-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="e5721-190">tooreview i zarządzania incydentami zabezpieczeń, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e5721-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="e5721-191">Wybierz hello **alerty zabezpieczeń** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e5721-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="e5721-192">w przypadku wykrycia zdarzenia zabezpieczeń będą wyświetlane w obszarze wykresu alerty zabezpieczeń hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="e5721-193">Jej ikonę, która różni się od innych alertów.</span><span class="sxs-lookup"><span data-stu-id="e5721-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="e5721-194">Wybierz zdarzenia toosee hello więcej szczegółów dotyczących tego zdarzenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5721-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="e5721-195">Dodatkowe szczegóły obejmują jego pełny opis, jego ważność, jego bieżący stan, atak powitania zasobów, procedura korygowania hello hello zdarzenia i hello alertów, które wchodzą w skład tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e5721-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="e5721-196">Można filtrować toosee **tylko zdarzenia**, **alerty tylko**, lub **zarówno**.</span><span class="sxs-lookup"><span data-stu-id="e5721-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="e5721-197">Jak uzyskać dostęp hello raportu analizy zagrożeń</span><span class="sxs-lookup"><span data-stu-id="e5721-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="e5721-198">ASC analizuje informacje z wielu źródeł tooidentify zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="e5721-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="e5721-199">zespoły odpowiedzi na zdarzenia tooassist zbadać i eliminowanie zagrożeń, Centrum zabezpieczeń zawiera raport analizy zagrożeń, który zawiera informacje o hello zagrożenia, które zostało wykryte.</span><span class="sxs-lookup"><span data-stu-id="e5721-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="e5721-200">Centrum zabezpieczeń zawiera trzy raporty zagrożenia, które mogą się różnić na atak.</span><span class="sxs-lookup"><span data-stu-id="e5721-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="e5721-201">dostępne raporty Hello są:</span><span class="sxs-lookup"><span data-stu-id="e5721-201">hello reports available are:</span></span>

- <span data-ttu-id="e5721-202">Raport grupy działań: zawiera głębokie dives do osoby atakujące, ich cele i taktyk.</span><span class="sxs-lookup"><span data-stu-id="e5721-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="e5721-203">Raport kampanii: koncentruje się na szczegóły ataku określonej kampanii.</span><span class="sxs-lookup"><span data-stu-id="e5721-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="e5721-204">Raport podsumowania zagrożeń: obejmuje wszystkie elementy w hello poprzednich dwóch raportów.</span><span class="sxs-lookup"><span data-stu-id="e5721-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="e5721-205">Informacje tego typu jest bardzo przydatny podczas procesu odpowiedzi na zdarzenia hello, w przypadku badania trwającą hello źródło toounderstand atak powitania hello motywacji osoby atakującej i jakie toomitigate toodo wystawiać przenoszenie do przodu.</span><span class="sxs-lookup"><span data-stu-id="e5721-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="e5721-206">tooaccess hello analizy zagrożeń raportu, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e5721-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="e5721-207">Wybierz hello **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="e5721-208">Wybierz alert zabezpieczeń hello, dla której ma zostać tooobtain więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e5721-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="e5721-209">W hello **raporty** kliknij raport analizy zagrożeń toohello łącze hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="e5721-210">Spowoduje to otwarcie pliku PDF hello, który można pobrać.</span><span class="sxs-lookup"><span data-stu-id="e5721-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="e5721-211">Aby uzyskać dodatkowe informacje na temat hello raportu analizy zagrożeń ASC, zobacz [raport analizy zagrożeń z Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="e5721-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="e5721-212">Ocena</span><span class="sxs-lookup"><span data-stu-id="e5721-212">Assessment</span></span>

<span data-ttu-id="e5721-213">toohelp do testowania, oceny i oceny strukturę bezpieczeństwa, ASC zapewnia oceny luk w zabezpieczeniach zintegrowane z Qualys agentów chmurze jako część jej składników zalecenia dotyczące maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5721-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="e5721-214">Witaj Qualys agenci będą raportować luki w zabezpieczeniach danych toohello Qualys platformy zarządzania, który z kolei odsyła luki w zabezpieczeniach i danych monitorowania kondycji powrotem tooASC.</span><span class="sxs-lookup"><span data-stu-id="e5721-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="e5721-215">Witaj tooadd zalecenie rozwiązanie do oceny luk w zabezpieczeniach jest wyświetlany w hello **zalecenia** bloku na pulpicie nawigacyjnym ASC hello.</span><span class="sxs-lookup"><span data-stu-id="e5721-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="e5721-216">Po zainstalowaniu rozwiązanie do oceny luk w zabezpieczeniach hello w celu hello wirtualna hello toodetect maszyny Wirtualnej i zidentyfikować luki w zabezpieczeniach systemu i aplikacji skanowania Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5721-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="e5721-217">Wykryto problemy są wyświetlane w obszarze hello **zalecenia dotyczące maszyny wirtualnej** opcji.</span><span class="sxs-lookup"><span data-stu-id="e5721-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="e5721-218">Jak wdrożyć rozwiązanie do oceny luk w zabezpieczeniach?</span><span class="sxs-lookup"><span data-stu-id="e5721-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="e5721-219">Jeśli maszyna wirtualna nie ma już wdrożone rozwiązanie do oceny luk w zabezpieczeniach zintegrowanego, Centrum zabezpieczeń zaleca się ona zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="e5721-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="e5721-220">Na pulpicie nawigacyjnym ASC hello, na powitania **zalecenia** bloku, wybierz opcję **Dodaj rozwiązanie do oceny luk w zabezpieczeniach.**</span><span class="sxs-lookup"><span data-stu-id="e5721-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="e5721-221">Wybierz maszyny wirtualne hello miejscu rozwiązanie do oceny luk w zabezpieczeniach hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e5721-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="e5721-222">Polecenie **zainstalowania na maszynach wirtualnych [numer].**</span><span class="sxs-lookup"><span data-stu-id="e5721-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="e5721-223">Wybierz rozwiązanie partnerskie w hello Azure Marketplace, lub na podstawie **użyć istniejącego rozwiązania,** wybierz **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="e5721-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="e5721-224">Ustawienia aktualizacji automatycznego hello lub wyłącz można włączyć w hello **rozwiązań partnerskich** bloku.</span><span class="sxs-lookup"><span data-stu-id="e5721-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="e5721-225">Aby uzyskać dalsze instrukcje dotyczące tooimplement rozwiązania oceny luk w zabezpieczeniach, zobacz [oceny luk w zabezpieczeniach w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="e5721-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5721-226">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5721-226">Next steps</span></span>

- [<span data-ttu-id="e5721-227">Przewodnik Szybki start dotyczący Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="e5721-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="e5721-228">Wprowadzenie tooAzure Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5721-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="e5721-229">Integrowanie z integracją dzienników Azure alerty Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="e5721-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="e5721-230">Zwiększenie wydajności Centrum zabezpieczeń Azure z oceny luk w zabezpieczeniach zintegrowane</span><span class="sxs-lookup"><span data-stu-id="e5721-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
