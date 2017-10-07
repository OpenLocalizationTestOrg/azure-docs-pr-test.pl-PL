---
title: "aaaManage alerty zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument pomaga możesz toouse Centrum zabezpieczeń Azure możliwości toomanage i Odpowiedz toosecurity alertów."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="e2dd2-103">Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="e2dd2-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="e2dd2-104">Ten dokument ułatwia Użyj toomanage Centrum zabezpieczeń Azure i reagowania na alerty toosecurity.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="e2dd2-105">wykryć tooenable zaawansowane, uaktualnienia tooAzure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="e2dd2-106">Dostępna jest bezpłatna 60-dniowa wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-106">A free 60-day trial is available.</span></span> <span data-ttu-id="e2dd2-107">tooupgrade, wybierz opcję warstwy cenowej w hello [zasady zabezpieczeń](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e2dd2-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="e2dd2-108">Zobacz [cennik Centrum zabezpieczeń Azure](security-center-pricing.md) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="e2dd2-109">Czym są alerty zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="e2dd2-109">What are security alerts?</span></span>
<span data-ttu-id="e2dd2-110">Centrum zabezpieczeń automatycznie gromadzi informacje, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci hello, połączone rozwiązań partnerskich, takich jak zapory i punktu końcowego rozwiązań do ochrony, toodetect prawdziwe zagrożenia i redukować liczbę fałszywych alarmów.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="e2dd2-111">Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem i zalecenia dotyczące tooremediate atak.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="e2dd2-112">Aby uzyskać więcej informacji na temat sposobu działania funkcji wykrywania usługi Security Center, przeczytaj [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="e2dd2-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="e2dd2-113">Zarządzanie alertami zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e2dd2-113">Managing security alerts</span></span>
<span data-ttu-id="e2dd2-114">Bieżące alerty można przeglądać, analizując hello **alerty zabezpieczeń** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="e2dd2-115">Otwórz Azure Portal i wykonaj kroki hello poniżej toosee więcej szczegółów dotyczących poszczególnych alertów:</span><span class="sxs-lookup"><span data-stu-id="e2dd2-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="e2dd2-116">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, zobaczysz hello **alerty zabezpieczeń** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Kafelek Alerty zabezpieczeń w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="e2dd2-118">Kliknij przycisk hello kafelka tooopen hello **alerty zabezpieczeń** blok zawierający więcej szczegółów na temat hello alertów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Witaj blok alerty zabezpieczeń w Centrum zabezpieczeń](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="e2dd2-120">W dolnej części tego bloku hello są hello uzyskać szczegółowe informacje o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="e2dd2-121">toosort, kliknij kolumnę hello, który ma toosort przez.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="e2dd2-122">Poniżej podano Hello definicje poszczególnych kolumn:</span><span class="sxs-lookup"><span data-stu-id="e2dd2-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="e2dd2-123">**Opis elementu**: Krótki opis alertu hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="e2dd2-124">**Liczba**: lista wszystkich alertów określonego typu, które zostały wykryte w określonym dniu.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="e2dd2-125">**Wykryte przez**: hello usługa, która jest odpowiedzialna za wyzwolenie alertu hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="e2dd2-126">**Data**: hello Data zdarzenie hello wystąpił.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="e2dd2-127">**Stan**: hello bieżący stan alertu.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="e2dd2-128">Istnieją dwa typy stanów:</span><span class="sxs-lookup"><span data-stu-id="e2dd2-128">There are two types of states:</span></span>
  * <span data-ttu-id="e2dd2-129">**Aktywne**: wykryto alert zabezpieczeń hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="e2dd2-130">**Ważność**: hello poziom ważności, który może być wysoki, średni lub niski.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="e2dd2-131">Filtrowanie alertów</span><span class="sxs-lookup"><span data-stu-id="e2dd2-131">Filtering alerts</span></span>
<span data-ttu-id="e2dd2-132">Alerty można filtrować na podstawie daty, stanu i ważności.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="e2dd2-133">Filtrowanie alertów może być przydatne w scenariuszach wymagających toonarrow hello zakres wyświetlanych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="e2dd2-134">Na przykład użytkownik ma tooaddress alerty zabezpieczeń, które wystąpiły w hello ostatnich 24 godzinach, ponieważ badasz potencjalne naruszenie zabezpieczeń w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="e2dd2-135">Kliknij przycisk **filtru** na powitania **alerty zabezpieczeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="e2dd2-136">Witaj **filtru** zostanie otwarty blok i wybierz wartości daty, stanu i ważności hello mają toosee.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Filtrowanie alertów w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="e2dd2-138">Odpowiadanie na alerty toosecurity</span><span class="sxs-lookup"><span data-stu-id="e2dd2-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="e2dd2-139">Wybierz toolearn alertu zabezpieczeń wymagają więcej informacji na temat hello zdarzenia, która wyzwoliła hello alert i co, jeśli kroki, możesz tooremediate tootake atak.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="e2dd2-140">Alerty zabezpieczeń są grupowane według typu i daty.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="e2dd2-141">Kliknięcie alertu zabezpieczeń spowoduje otwarcie bloku zawierającego listę hello pogrupowanych alertów.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Odpowiadanie na alerty toosecurity w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="e2dd2-143">W tym przypadku wyzwolone alerty hello można znaleźć toosuspicious działania protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="e2dd2-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="e2dd2-144">Witaj pierwsza kolumna zawiera zaatakowane zasoby; Witaj drugi Pokazuje ile razy zaatakowany zasób hello; Witaj innej przedstawia czas hello atak powitania; Witaj czwarty pokazuje stan alertu hello; i hello piąte pokazuje hello ważność atak powitania.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="e2dd2-145">Po przejrzeniu tych informacji kliknij zaatakowany zasób hello i zostanie otwarty nowy blok.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Sugestie dotyczące alertów jakie toodo dotyczących zabezpieczeń w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="e2dd2-147">W hello **opis** tego bloku można znaleźć więcej szczegółów dotyczących tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="e2dd2-148">Te dodatkowe szczegóły zapewniają wgląd w jaki wyzwalanych hello zabezpieczeń alertów, hello zasobu docelowego, gdy dotyczy hello źródłowy adres IP i zaleceń dotyczących tooremediate.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="e2dd2-149">W niektórych przypadkach hello źródłowy adres IP będzie pusty (niedostępny), ponieważ nie wszystkie dzienniki zdarzeń zabezpieczeń systemu Windows obejmują adres IP hello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="e2dd2-150">Witaj naprawcze sugerowane w Centrum zabezpieczeń będą się różnić zgodnie z alert zabezpieczeń toohello.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="e2dd2-151">W niektórych przypadkach może być toouse tooimplement innych funkcji platformy Azure hello zalecane korygowania.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="e2dd2-152">Na przykład Witaj korygowania takiego ataku jest adres IP hello tooblacklist generujących atak przy użyciu [sieciowej listy ACL](../virtual-network/virtual-networks-acl.md) lub [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="e2dd2-153">Aby uzyskać więcej informacji na powitania różnych typów alertów, przeczytaj [alerty zabezpieczeń według typu w Centrum zabezpieczeń Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="e2dd2-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="e2dd2-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e2dd2-154">See also</span></span>
<span data-ttu-id="e2dd2-155">W tym dokumencie możesz przedstawiono sposób tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="e2dd2-156">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e2dd2-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="e2dd2-157">Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e2dd2-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="e2dd2-158">Funkcje wykrywania usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e2dd2-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="e2dd2-159">Przewodnik planowania i obsługi usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e2dd2-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="e2dd2-160">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="e2dd2-161">[Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e2dd2-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
