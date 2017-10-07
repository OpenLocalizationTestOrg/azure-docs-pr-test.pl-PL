---
title: aaaEnterprise integracji dla B2B - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Tworzenie przepływów pracy B2B i obsługuje scenariusze integracji przedsiębiorstwa dla usługi logic apps z hello pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="0194d-103">Omówienie: Scenariusze B2B i komunikacji z hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="0194d-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="0194d-104">Bezproblemowe komunikacji z usługą Azure Logic Apps i przepływy pracy między firmami (B2B) można włączyć scenariuszy integracji przedsiębiorstwa z rozwiązania opartego na chmurze firmy Microsoft, hello pakiet integracyjny dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="0194d-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="0194d-105">Organizacje mogą wymieniać komunikaty elektronicznie, nawet jeśli używają różnych protokołów i formaty.</span><span class="sxs-lookup"><span data-stu-id="0194d-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="0194d-106">Pakiet HELLO przekształca różnych formatach w formacie, który systemów organizacji mogą interpretować i przetwarzać.</span><span class="sxs-lookup"><span data-stu-id="0194d-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="0194d-107">Organizacje mogą wymieniać komunikaty za pośrednictwem standardowych protokołów, w tym [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), i [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="0194d-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="0194d-108">Ponadto można zabezpieczyć komunikatów przy użyciu szyfrowania i podpisy cyfrowe.</span><span class="sxs-lookup"><span data-stu-id="0194d-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="0194d-109">Jeśli znasz BizTalk Server lub usług Microsoft Azure BizTalk, funkcje integracji przedsiębiorstwa hello są łatwe toouse, ponieważ większość pojęcia są podobne.</span><span class="sxs-lookup"><span data-stu-id="0194d-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="0194d-110">Jeden główna różnica polega na tym, że integracji przedsiębiorstwa używa integracji kont toosimplify hello magazynu i zarządzania używane w komunikacji B2B artefaktów.</span><span class="sxs-lookup"><span data-stu-id="0194d-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="0194d-111">Pod względem architektury hello pakiet integracyjny dla przedsiębiorstw opiera się na "konta integracji".</span><span class="sxs-lookup"><span data-stu-id="0194d-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="0194d-112">Te konta są oparte na chmurze kontenerów, które przechowują wszystkie Twoje artefaktów jak schematów, partnerów, certyfikaty, map i umów.</span><span class="sxs-lookup"><span data-stu-id="0194d-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="0194d-113">Można użyć tych toodesign artefaktów, wdrażanie i obsługa aplikacji B2B i również toobuild B2B przepływów pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="0194d-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="0194d-114">Jednak przed użyciem tych artefaktów, należy najpierw połączyć aplikację logiki tooyour konta integracji.</span><span class="sxs-lookup"><span data-stu-id="0194d-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="0194d-115">Po wykonaniu tej aplikacji logiki mają dostęp do konta integracji artefaktów.</span><span class="sxs-lookup"><span data-stu-id="0194d-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="0194d-116">Dlaczego należy używać integracji przedsiębiorstwa?</span><span class="sxs-lookup"><span data-stu-id="0194d-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="0194d-117">Dzięki integracji przedsiębiorstwa wszystkie artefakty użytkownika można przechowywać w jednym miejscu — konta integracji.</span><span class="sxs-lookup"><span data-stu-id="0194d-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="0194d-118">Możesz skompilować B2B przepływów pracy i zintegrować z innych firm oprogramowanie jako usługa (SaaS) aplikacji, aplikacji lokalnych i aplikacji niestandardowych przy użyciu aparatu Azure Logic Apps hello i wszystkich jego łączników.</span><span class="sxs-lookup"><span data-stu-id="0194d-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="0194d-119">Można utworzyć niestandardowego kodu dla aplikacji logiki z funkcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0194d-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="0194d-120">Jak tooget wprowadzenie do integracji przedsiębiorstwa?</span><span class="sxs-lookup"><span data-stu-id="0194d-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="0194d-121">Możesz skompilować i zarządzanie aplikacjami B2B w usłudze hello pakiet integracyjny dla przedsiębiorstw przy użyciu hello projektanta aplikacji logiki w hello **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="0194d-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="0194d-122">Można również zarządzać z aplikacji logiki [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps tematy PowerShell").</span><span class="sxs-lookup"><span data-stu-id="0194d-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="0194d-123">Poniżej przedstawiono kroki wysokiego poziomu hello, które należy wykonać przed przystąpieniem do tworzenia aplikacji w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="0194d-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Obraz — omówienie](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="0194d-125">Co to są niektórych typowych scenariuszy?</span><span class="sxs-lookup"><span data-stu-id="0194d-125">What are some common scenarios?</span></span>

<span data-ttu-id="0194d-126">Integracja Enterprise obsługuje te standardy branżowe:</span><span class="sxs-lookup"><span data-stu-id="0194d-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="0194d-127">EDI - elektronicznej wymiany danych</span><span class="sxs-lookup"><span data-stu-id="0194d-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="0194d-128">Usługi EAI - integracji aplikacji dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="0194d-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="0194d-129">Oto co należy uruchomić tooget</span><span class="sxs-lookup"><span data-stu-id="0194d-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="0194d-130">Subskrypcja platformy Azure przy użyciu konta integracji</span><span class="sxs-lookup"><span data-stu-id="0194d-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="0194d-131">Visual Studio 2015 toocreate map i schematy</span><span class="sxs-lookup"><span data-stu-id="0194d-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="0194d-132">Integracji przedsiębiorstwa aplikacje logiki platformy Microsoft Azure Tools dla programu Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="0194d-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="0194d-133">Wypróbuj teraz</span><span class="sxs-lookup"><span data-stu-id="0194d-133">Try it now</span></span>

<span data-ttu-id="0194d-134">[Wdrażanie wysyłania AS2 próbki pełnej funkcjonalności i odbierać aplikacji logiki](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) używającą hello B2B funkcji dla usługi Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="0194d-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="0194d-135">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="0194d-135">Learn more</span></span>
* [<span data-ttu-id="0194d-136">Umów</span><span class="sxs-lookup"><span data-stu-id="0194d-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")
* [<span data-ttu-id="0194d-137">Scenariusze tooBusiness (B2B)</span><span class="sxs-lookup"><span data-stu-id="0194d-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Dowiedz się jak toocreate Logic apps z funkcjami B2B")  
* [<span data-ttu-id="0194d-138">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="0194d-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Dowiedz się więcej o certyfikatach integracji przedsiębiorstwa")
* [<span data-ttu-id="0194d-139">Płaskie pliku kodowania/dekodowania</span><span class="sxs-lookup"><span data-stu-id="0194d-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Dowiedz się jak tooencode i dekodowania zawartość pliku prostego")  
* [<span data-ttu-id="0194d-140">Konta integracji</span><span class="sxs-lookup"><span data-stu-id="0194d-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się więcej na temat integracji kont")
* [<span data-ttu-id="0194d-141">Mapuje</span><span class="sxs-lookup"><span data-stu-id="0194d-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")
* [<span data-ttu-id="0194d-142">Partnerzy</span><span class="sxs-lookup"><span data-stu-id="0194d-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Dowiedz się więcej na temat partnerów integracji przedsiębiorstwa")
* [<span data-ttu-id="0194d-143">Schematy</span><span class="sxs-lookup"><span data-stu-id="0194d-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Dowiedz się więcej na temat schematów integracji przedsiębiorstwa")
* [<span data-ttu-id="0194d-144">Sprawdzanie poprawności kodu XML wiadomości</span><span class="sxs-lookup"><span data-stu-id="0194d-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Dowiedz się, jak komunikaty toovalidate XML z usługą Logic apps")
* [<span data-ttu-id="0194d-145">Przekształcanie XML</span><span class="sxs-lookup"><span data-stu-id="0194d-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")
* [<span data-ttu-id="0194d-146">Łączniki integracji dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="0194d-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Dowiedz się więcej o pakiecie łączniki integracji dla przedsiębiorstw")
* [<span data-ttu-id="0194d-147">Metadane konta integracji</span><span class="sxs-lookup"><span data-stu-id="0194d-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "informacje o metadanych konta integracji")
* [<span data-ttu-id="0194d-148">Monitorowanie wiadomości B2B</span><span class="sxs-lookup"><span data-stu-id="0194d-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Dowiedz się więcej na temat monitorowania wiadomości B2B")
* [<span data-ttu-id="0194d-149">Śledzenie wiadomości B2B w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="0194d-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Dowiedz się więcej o śledzenie wiadomości B2B w portalu OMS")

