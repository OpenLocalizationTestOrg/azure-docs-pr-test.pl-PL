---
title: "Zarządzanie alertami zabezpieczeń w usłudze Azure Security Center | Microsoft Docs"
description: "Ten dokument ułatwia zarządzanie alertami zabezpieczeń i reagowanie na nie przy użyciu funkcji Centrum zabezpieczeń Azure."
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
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="3e9d6-103">Reagowanie na alerty zabezpieczeń i zarządzanie nimi w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="3e9d6-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="3e9d6-104">Ten dokument ułatwia zarządzanie alertami zabezpieczeń i reagowanie na nie przy użyciu usługi Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="3e9d6-105">Aby włączyć wykrywanie zaawansowane, przeprowadź uaktualnienie usługi Azure Security Center do wersji Standard.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="3e9d6-106">Dostępna jest bezpłatna 60-dniowa wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-106">A free 60-day trial is available.</span></span> <span data-ttu-id="3e9d6-107">W celu uaktualnienia wybierz warstwę cenową w [Zasadach zabezpieczeń](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="3e9d6-108">Aby dowiedzieć się więcej, zobacz [cennik usługi Azure Security Center](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="3e9d6-109">Czym są alerty zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="3e9d6-109">What are security alerts?</span></span>
<span data-ttu-id="3e9d6-110">Usługa Security Center automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci oraz połączonych rozwiązań partnerskich, takich jak rozwiązania zapory i ochrony punktów końcowych, aby wykrywać prawdziwe zagrożenia i redukować liczbę fałszywych alarmów.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="3e9d6-111">W usłudze Security Center jest wyświetlana lista alertów zabezpieczeń uporządkowanych według priorytetu oraz informacje potrzebne do szybkiego analizowania problemu i zalecenia dotyczące postępowania w razie ataku.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="3e9d6-112">Aby uzyskać więcej informacji na temat sposobu działania funkcji wykrywania usługi Security Center, przeczytaj [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="3e9d6-113">Zarządzanie alertami zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3e9d6-113">Managing security alerts</span></span>
<span data-ttu-id="3e9d6-114">Bieżące alerty można przeglądać przy użyciu kafelka **Alerty zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="3e9d6-115">Otwórz witrynę Azure Portal i wykonaj poniższe kroki, aby wyświetlić więcej szczegółowych informacji dotyczących poszczególnych alertów:</span><span class="sxs-lookup"><span data-stu-id="3e9d6-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="3e9d6-116">Na pulpicie nawigacyjnym Centrum zabezpieczeń widoczny jest kafelek **Alerty zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Kafelek Alerty zabezpieczeń w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="3e9d6-118">Kliknij kafelek, aby otworzyć blok **Alerty zabezpieczeń** zawierający więcej szczegółowych informacji o alertach, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![Blok kafelka Alerty zabezpieczeń w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="3e9d6-120">W dolnej części tego bloku znajdują się szczegółowe informacje o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="3e9d6-121">Aby posortować dane, kliknij kolumnę, według której chcesz wykonać sortowanie.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="3e9d6-122">Poniżej znajdują się definicje poszczególnych kolumn:</span><span class="sxs-lookup"><span data-stu-id="3e9d6-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="3e9d6-123">**Opis**: krótki opis alertu.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="3e9d6-124">**Liczba**: lista wszystkich alertów określonego typu, które zostały wykryte w określonym dniu.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="3e9d6-125">**Wykryte przez**: usługa odpowiedzialna za wyzwolenie alertu.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="3e9d6-126">**Data**: dzień, w którym wystąpiło zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="3e9d6-127">**Stan**: bieżący stan alertu.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="3e9d6-128">Istnieją dwa typy stanów:</span><span class="sxs-lookup"><span data-stu-id="3e9d6-128">There are two types of states:</span></span>
  * <span data-ttu-id="3e9d6-129">**Aktywny**: alert zabezpieczeń został wykryty.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="3e9d6-130">**Ważność**: poziom ważności (wysoki, średni lub niski).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="3e9d6-131">Filtrowanie alertów</span><span class="sxs-lookup"><span data-stu-id="3e9d6-131">Filtering alerts</span></span>
<span data-ttu-id="3e9d6-132">Alerty można filtrować na podstawie daty, stanu i ważności.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="3e9d6-133">Filtrowanie alertów może być przydatne w przypadku scenariuszy, w których należy zawęzić zakres wyświetlanych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="3e9d6-134">Możesz na przykład sprawdzić alerty zabezpieczeń, które wystąpiły w ciągu ostatnich 24 godzin, ponieważ badasz potencjalne naruszenie zabezpieczeń systemu.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="3e9d6-135">Kliknij pozycję **Filtr** w bloku **Alerty zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="3e9d6-136">Zostanie otwarty blok **Filtr**. Wybierz wartości daty, stanu i ważności, które chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Filtrowanie alertów w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="3e9d6-138">Odpowiadanie na alerty zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3e9d6-138">Respond to security alerts</span></span>
<span data-ttu-id="3e9d6-139">Wybierz alert zabezpieczeń, aby dowiedzieć się więcej o zdarzeniach, które go wywołały, oraz o czynnościach, które należy wykonać w celu wyeliminowania skutków ataku (jeśli ma to zastosowanie).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="3e9d6-140">Alerty zabezpieczeń są grupowane według typu i daty.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="3e9d6-141">Kliknięcie alertu zabezpieczeń spowoduje otwarcie bloku zawierającego listę pogrupowanych alertów.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Odpowiadanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="3e9d6-143">W tym przypadku wyzwolone alerty dotyczą podejrzanego działania protokołu RDP (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="3e9d6-144">Pierwsza kolumna zawiera zaatakowane zasoby, druga przedstawia liczbę ataków na zasób, trzecia — czas ataku, czwarta — stan alertu, a piąta — ważność ataku.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="3e9d6-145">Po przejrzeniu tych informacji kliknij zaatakowany zasób. Zostanie otwarty nowy blok.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Sugestie dotyczące zalecanych działań związanych z alertami zabezpieczeń w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="3e9d6-147">W polu **Opis** tego bloku znajdują się dalsze szczegółowe informacje na temat danego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="3e9d6-148">Te dodatkowe szczegóły dotyczą przyczyn wyzwolenia alertu zabezpieczeń, zasobu docelowego, źródłowego adresu IP (jeśli ma to zastosowanie) i zaleceń dotyczących sposobu wyeliminowania skutków ataku.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="3e9d6-149">W niektórych przypadkach źródłowy adres IP będzie pusty (niedostępny), ponieważ nie wszystkie dzienniki zdarzeń zabezpieczeń systemu Windows obejmują adres IP.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="3e9d6-150">Czynności naprawcze sugerowane w Centrum zabezpieczeń będą różnić się w zależności od alertu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="3e9d6-151">W niektórych przypadkach do wykonania zalecanych czynności naprawczych trzeba będzie użyć innych funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="3e9d6-152">Na przykład aby wyeliminować skutki takiego ataku, należy utworzyć listę niedozwolonych adresów IP generujących atak przy użyciu [sieciowej listy ACL](../virtual-network/virtual-networks-acl.md) lub reguły [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="3e9d6-153">Aby znaleźć więcej informacji na temat różnych typów alertów, przeczytaj artykuł [Alerty zabezpieczeń według typu w usłudze Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d6-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="3e9d6-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3e9d6-154">See also</span></span>
<span data-ttu-id="3e9d6-155">W tym dokumencie przedstawiono sposób konfigurowania zasad zabezpieczeń w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="3e9d6-156">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="3e9d6-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="3e9d6-157">Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3e9d6-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="3e9d6-158">Funkcje wykrywania usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3e9d6-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="3e9d6-159">Przewodnik planowania i obsługi usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3e9d6-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="3e9d6-160">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3e9d6-161">[Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9d6-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
