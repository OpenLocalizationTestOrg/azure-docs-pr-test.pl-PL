---
title: "aaaHandling alerty zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia przypadki naruszenia zabezpieczeń toohandle toouse Centrum zabezpieczeń Azure możliwości."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="203de-103">Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="203de-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="203de-104">Klasyfikowane i badanie alertów zabezpieczeń może zająć dużo czasu na powitania nawet najbardziej doświadczona analityków zabezpieczeń i dla wielu jest tooeven twardym wiedzieć, gdzie toobegin.</span><span class="sxs-lookup"><span data-stu-id="203de-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="203de-105">Za pomocą [analytics](security-center-detection-capabilities.md) tooconnect hello informacji między różne [alerty zabezpieczeń](security-center-managing-and-responding-alerts.md), Centrum zabezpieczeń zapewnia jednolity obraz kampanii ataku i wszystkich hello powiązanych alertów — możesz szybko poznać trwało atakująca hello jakie akcje i jakie zasoby został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="203de-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="203de-106">W tym dokumencie omówiono sposób zabezpieczeń toouse ostrzec możliwości w Centrum zabezpieczeń tooassist obsługi zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="203de-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="203de-107">Co to jest zdarzenie naruszenia zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="203de-107">What is a security incident?</span></span>
<span data-ttu-id="203de-108">W usłudze Security Center zdarzenie naruszenia zabezpieczeń to agregacja wszystkich alertów zasobu, które są zgodne ze wzorcami [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/), tzw. „zabójczego łańcucha”.</span><span class="sxs-lookup"><span data-stu-id="203de-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="203de-109">Zdarzenia są wyświetlane w hello [alerty zabezpieczeń](security-center-managing-and-responding-alerts.md) kafelków i bloku.</span><span class="sxs-lookup"><span data-stu-id="203de-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="203de-110">Zdarzenie będzie ujawnić hello listę powiązanych alertów, dzięki czemu możesz tooobtain więcej informacji na temat każdego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="203de-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="203de-111">Zarządzanie zdarzeniami naruszenia zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="203de-111">Managing security incidents</span></span>
<span data-ttu-id="203de-112">Patrząc na kafelku alerty zabezpieczeń hello można przejrzeć bieżącego przypadki naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="203de-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="203de-113">Dostęp do portalu Azure hello i wykonaj kroki hello poniżej toosee więcej szczegółów na temat każdego zdarzenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="203de-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="203de-114">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, zobaczysz hello **alerty zabezpieczeń** kafelka.</span><span class="sxs-lookup"><span data-stu-id="203de-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Kafelek Alerty zabezpieczeń w usłudze Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="203de-116">Kliknięcie tego kafelka tooexpand go i jeśli zostanie wykryty zdarzenia zabezpieczeń, zostanie wyświetlony w obszarze hello wykres alerty zabezpieczeń w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="203de-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="203de-118">Powiadomienie, że opis zdarzenia zabezpieczeń hello ma inną ikonę porównywany tooother alertów.</span><span class="sxs-lookup"><span data-stu-id="203de-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="203de-119">Kliknij go tooview bardziej szczegółowe informacje dotyczące tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="203de-119">Click on it tooview more details about this incident.</span></span>

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="203de-121">Na powitania **zdarzenia** bloku pojawi się bardziej szczegółowych informacji o tego zdarzenia zabezpieczeń obejmuje pełny opis, jego ważności (czyli w tym przypadku wysokiej), jego bieżący stan (w tym przypadku jest nadal *aktywny*, które sugeruje hello użytkownika nie podjęte tooit działania — można to zrobić, klikając prawym przyciskiem myszy na powitania zdarzenia w programie hello **alerty zabezpieczeń** blok), zasobu atak powitania (w tym przypadku *VM1*), hello czynności korygujące dla zdarzenia hello i w hello dolne okienko masz hello alertów, które wchodzą w skład tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="203de-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="203de-122">Więcej informacji o każdym alercie ma tooobtain zostanie otwarty po prostu kliknij go, a kolejny blok, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="203de-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="203de-124">Hello informacji na temat tego bloku różnią się zgodnie z toohello alertu.</span><span class="sxs-lookup"><span data-stu-id="203de-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="203de-125">Odczyt [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) Aby uzyskać więcej informacji na temat toomanage te alerty.</span><span class="sxs-lookup"><span data-stu-id="203de-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="203de-126">Pewne istotne kwestie dotyczące tej funkcji:</span><span class="sxs-lookup"><span data-stu-id="203de-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="203de-127">Nowy filtr umożliwia toocustomize, który tooIncident z widoku tylko alerty tylko, lub obie.</span><span class="sxs-lookup"><span data-stu-id="203de-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="203de-128">powitalne tego samego alertu może istnieć w ramach zdarzenia (jeśli dotyczy), a także toobe widoczne jako alert autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="203de-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="203de-129">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="203de-129">See also</span></span>
<span data-ttu-id="203de-130">W tym dokumencie przedstawiono sposób toouse hello możliwości zdarzenia zabezpieczeń w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="203de-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="203de-131">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="203de-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="203de-132">Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="203de-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="203de-133">Funkcje wykrywania usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="203de-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="203de-134">Przewodnik planowania i obsługi usługi Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="203de-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="203de-135">Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="203de-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="203de-136">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="203de-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="203de-137">[Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="203de-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
