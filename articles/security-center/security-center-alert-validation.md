---
title: "aaaAlerts weryfikacji w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia alerty zabezpieczeń hello toovalidate w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="bf867-103">Walidacja alertów w usłudze Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bf867-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="bf867-104">Ten dokument ułatwia Dowiedz się, jak tooverify, jeśli system jest poprawnie skonfigurowany na potrzeby alerty Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="bf867-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="bf867-105">Czym są alerty zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="bf867-105">What are security alerts?</span></span>
<span data-ttu-id="bf867-106">Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci hello i połączonych rozwiązań partnerskich, takich jak zapory i punktu końcowego rozwiązań do ochrony, toodetect i alertów można toothreats.</span><span class="sxs-lookup"><span data-stu-id="bf867-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="bf867-107">Odczyt [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) Aby uzyskać więcej informacji na temat alertów zabezpieczeń i Odczyt [opis alertów zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn więcej o różnych typach hello alertów.</span><span class="sxs-lookup"><span data-stu-id="bf867-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="bf867-108">Walidacja alertu</span><span class="sxs-lookup"><span data-stu-id="bf867-108">Alert validation</span></span>
<span data-ttu-id="bf867-109">Po zainstalowaniu agenta Centrum zabezpieczeń na komputerze, wykonaj kroki hello poniżej z komputera hello miejscu zasobów atak powitania toobe hello alertu:</span><span class="sxs-lookup"><span data-stu-id="bf867-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="bf867-110">Skopiuj pulpitu toohello pliku wykonywalnego (na przykład calc.exe) lub innego katalogu wygody.</span><span class="sxs-lookup"><span data-stu-id="bf867-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="bf867-111">Zmień nazwę tego pliku zbyt**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="bf867-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="bf867-112">Otwórz wiersz polecenia hello i wykonywanie tego pliku z argumentem (po prostu fałszywych argument nazwy), takich jak: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="bf867-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="bf867-113">Zaczekaj 5 minut too10 i otwórz alerty Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf867-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="bf867-114">Powinna być widoczna alertu toofollowing podobne, co:</span><span class="sxs-lookup"><span data-stu-id="bf867-114">There you should find an alert similar toofollowing one:</span></span>

    ![Walidacja alertu](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="bf867-116">Podczas przeglądania ten alert, upewnij się, że pole hello włączyć inspekcję argumentów jest wyświetlany jako true.</span><span class="sxs-lookup"><span data-stu-id="bf867-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="bf867-117">Zawiera ona wartość false, należy najpierw tooenable argumenty wiersza polecenia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="bf867-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="bf867-118">Można włączyć tę opcję, przy użyciu następującego wiersza polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="bf867-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="bf867-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="bf867-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="bf867-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bf867-120">See also</span></span>
<span data-ttu-id="bf867-121">W tym artykule wprowadzono procesu weryfikacji toohello alertów.</span><span class="sxs-lookup"><span data-stu-id="bf867-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="bf867-122">Teraz, kiedy znasz tej weryfikacji, spróbuj hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="bf867-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="bf867-123">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="bf867-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="bf867-124">Dowiedz się, jak toomanage alerty i zdarzenia toosecurity odpowiedź w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf867-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="bf867-125">[Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="bf867-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="bf867-126">Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf867-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="bf867-127">[Informacje o alertach zabezpieczeń w usłudze Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="bf867-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="bf867-128">Dowiedz się więcej o różnych typach hello alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf867-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="bf867-129">[Przewodnik rozwiązywania problemów z usługą Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="bf867-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="bf867-130">Dowiedz się, jak tootroubleshoot typowe problemy w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bf867-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="bf867-131">[Azure Security Center — często zadawane pytania](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bf867-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="bf867-132">Znajdź często zadawane pytania dotyczące korzystania z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="bf867-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="bf867-133">[Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="bf867-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="bf867-134">Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf867-134">Find blog posts about Azure security and compliance.</span></span>

