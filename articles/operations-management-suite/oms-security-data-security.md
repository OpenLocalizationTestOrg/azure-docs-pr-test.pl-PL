---
title: "aaaOperations zabezpieczeń pakietu zarządzania i bezpieczeństwo danych rozwiązania inspekcji | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób zarządzania danymi i ich ochrony w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="2a68b-103">Bezpieczeństwo danych w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2a68b-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="2a68b-104">Klienci toohelp zapobiegania, wykrywania i odpowiadać toothreats, [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](operations-management-suite-overview.md) zbiera i przetwarza dane dotyczące zasobów, w tym:</span><span class="sxs-lookup"><span data-stu-id="2a68b-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="2a68b-105">Dziennik zdarzeń zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2a68b-105">Security event log</span></span>
* <span data-ttu-id="2a68b-106">Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="2a68b-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="2a68b-107">Zdarzenia inspekcji funkcji AppLocker</span><span class="sxs-lookup"><span data-stu-id="2a68b-107">AppLocker auditing events</span></span>
* <span data-ttu-id="2a68b-108">Dziennik zapory systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2a68b-108">Windows Firewall log</span></span>
* <span data-ttu-id="2a68b-109">Zdarzenia rozwiązania Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="2a68b-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="2a68b-110">Wyniki oceny linii bazowej</span><span class="sxs-lookup"><span data-stu-id="2a68b-110">Results of baseline assessment</span></span>
* <span data-ttu-id="2a68b-111">Wyniki oceny oprogramowania chroniącego przed złośliwym kodem</span><span class="sxs-lookup"><span data-stu-id="2a68b-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="2a68b-112">Wyniki oceny aktualizacji/poprawek</span><span class="sxs-lookup"><span data-stu-id="2a68b-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="2a68b-113">Strumienie audyt dzienników systemowych, które są jawnie włączone w agencie hello</span><span class="sxs-lookup"><span data-stu-id="2a68b-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="2a68b-114">Firma Microsoft wprowadzać silne zobowiązań tooprotect hello prywatności i bezpieczeństwa tych danych.</span><span class="sxs-lookup"><span data-stu-id="2a68b-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="2a68b-115">Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi.</span><span class="sxs-lookup"><span data-stu-id="2a68b-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="2a68b-116">Ten artykuł przedstawia sposób zarządzania danymi i ich ochrony w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="2a68b-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="2a68b-117">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="2a68b-117">Data sources</span></span>
<span data-ttu-id="2a68b-118">Zabezpieczenia OMS i rozwiązanie inspekcji analizować dane z maszyn wirtualnych i fizycznych komputerów z zainstalowanym hello Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="2a68b-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="2a68b-119">Rozwiązanie Zabezpieczenia i inspekcja w pakiecie OMS może zbierać informacje o konfiguracji dotyczące zdarzeń zabezpieczeń, takich jak zdarzenia systemu Windows, dzienniki inspekcji, dzienniki usług IIS i komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="2a68b-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="2a68b-120">Przykłady takich danych to: typ i wersja systemu operacyjnego, uruchomione procesy, nazwa maszyny, adresy IP, zalogowany użytkownik i identyfikator dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2a68b-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="2a68b-121">Ochrona danych</span><span class="sxs-lookup"><span data-stu-id="2a68b-121">Data protection</span></span>
<span data-ttu-id="2a68b-122">**Podział danych**: dane są przechowywane logicznie oddzielnie dla każdego składnika w całym hello usługi.</span><span class="sxs-lookup"><span data-stu-id="2a68b-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="2a68b-123">Wszystkie dane są otagowane informacjami o organizacji.</span><span class="sxs-lookup"><span data-stu-id="2a68b-123">All data is tagged per organization.</span></span> <span data-ttu-id="2a68b-124">Znakowanie ten będzie nadal występował w całym cyklu życia danych hello i są wymuszane w każdej warstwie hello usługi.</span><span class="sxs-lookup"><span data-stu-id="2a68b-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="2a68b-125">**Dostęp do danych**: tooprovide zalecenia dotyczące zabezpieczeń i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft może uzyskać dostępu do informacji zbieranych lub przeanalizowane przez usługi.</span><span class="sxs-lookup"><span data-stu-id="2a68b-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="2a68b-126">Firma Microsoft jest zgodna toohello [warunki dotyczące usług Online firmy Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) i [zasady zachowania poufności informacji](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), którego stan czy Microsoft będą używane dane klienta lub nie pochodzi informacji z niego anonsowaniu lub podobne do celów komercyjnych.</span><span class="sxs-lookup"><span data-stu-id="2a68b-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="2a68b-127">zalecenia dotyczące zabezpieczeń tooprovide i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft może uzyskać dostępu do informacji zbieranych lub przeanalizowane przez usługi.</span><span class="sxs-lookup"><span data-stu-id="2a68b-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="2a68b-128">Tylko używamy danych klienta jako tooprovide potrzebne, możesz z platformy Azure, usług, łącznie z celów jest zgodny z dostarczanie tych usług.</span><span class="sxs-lookup"><span data-stu-id="2a68b-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="2a68b-129">Można zachować wszystkie prawa tooyour własnych danych.</span><span class="sxs-lookup"><span data-stu-id="2a68b-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="2a68b-130">**Użyj danych**: Firma Microsoft wykorzystuje wzorce i analizy zagrożeń widoczne w wielu dzierżawy tooenhance naszych możliwości wykrywania i zapobiegania; że odbywa się zgodnie z opisem w temacie zobowiązaniami prywatności hello naszych [prywatności Instrukcja](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a68b-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2a68b-131">Lokalizacja danych jest skonfigurowana na poziomie obszar roboczy OMS hello, podczas tworzenia obszaru roboczego hello, która jest częścią hello początkowej OMS zabezpieczeń i inspekcji procesu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2a68b-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="2a68b-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2a68b-132">See also</span></span>
<span data-ttu-id="2a68b-133">W tym dokumencie przedstawiono sposób zarządzania danymi i ich ochrony w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="2a68b-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="2a68b-134">toolearn więcej informacji na temat zabezpieczeń OMS i inspekcji rozwiązania, zobacz:</span><span class="sxs-lookup"><span data-stu-id="2a68b-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="2a68b-135">Omówienie pakietu Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="2a68b-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="2a68b-136">Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji</span><span class="sxs-lookup"><span data-stu-id="2a68b-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="2a68b-137">Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2a68b-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

