---
title: "aaaIntegrate dzienników z zasobów platformy Azure do systemów SIEM | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat integracji Azure dziennika, jego kluczowych możliwości i jak działa."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Wprowadzenie tooMicrosoft integracji dzienników Azure
Więcej informacji na temat integracji Azure dziennika, jego kluczowych możliwości i jak działa.

## <a name="overview"></a>Omówienie

Integracja dzienników Azure jest bezpłatna rozwiązania, które umożliwia toointegrate nowych dzienników z zasobów platformy Azure systemów lokalnych tooyour Security Information and Event Management (SIEM).

Integracja dzienników Azure zdarzeń systemu Windows zbiera dzienniki Podglądu zdarzeń systemu Windows, [Dzienniki aktywności Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [alerty Centrum zabezpieczeń Azure](../security-center/security-center-intro.md), i [dzienników diagnostycznych Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) z zasobów platformy Azure. Integracja ta pomaga zapewnić jednolity pulpit nawigacyjny dla wszystkich zasobów rozwiązania SIEM, lokalnymi lub w chmurze hello, dzięki czemu można zagregować skorelowania, analizowanie i alertów zdarzeń zabezpieczeń.

>[!NOTE]
W tej chwili chmur hello tylko obsługiwane są Azure handlowych i Azure dla instytucji rządowych. Inne chmury nie są obsługiwane.

![Integracja dzienników platformy Azure][1]

## <a name="what-logs-can-i-integrate"></a>Jakie dzienniki można zintegrować?
Azure tworzy szczegółowe rejestrowanie dla każdej usługi Azure. Te dzienniki stanowią trzy typy dzienników:

* **Dzienniki sterowania i zarządzania nimi** zapewniają wgląd w hello [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) operacji tworzenia, AKTUALIZOWANIA lub usuwania. Przykładem tego typu dziennika jest Dzienniki aktywności platformy Azure.
* **Dane płaszczyzny dzienniki** zapewniają wgląd w zdarzenia hello zgłoszone jako część hello użycie zasobów platformy Azure. Przykładem tego typu dziennika jest hello Podgląd zdarzeń systemu Windows w **systemu**, **zabezpieczeń**, i **aplikacji** kanałów na maszynie wirtualnej systemu Windows. Innym przykładem jest rejestrowania diagnostyki skonfigurowane za pośrednictwem Monitora Azure
* **Przetworzonych zdarzeń** przeanalizowane zdarzeń i informacji o alertach przetwarzane w Twoim imieniu. Przykładem tego typu zdarzenia jest Azure zabezpieczeń Centrum alerty, gdy Centrum zabezpieczeń Azure ma przetwarzane i analizowane subskrypcji tooprovide alerty odpowiednich tooyour bieżącego strukturę bezpieczeństwa.

Integracja z usługą Azure dziennika obsługuje ArcSight, QRadar i Splunk. Czy mają one natywnego łącznika w każdej sytuacji, skontaktuj się z Twojego tooassess dostawcy SIEM. W niektórych przypadkach nie musisz toouse Azure dziennika integracji dostępnych łączników macierzystego. Dodatkowe informacje na temat obsługiwanych dziennika, odwiedź stronę typy hello — często zadawane pytania.

>[!NOTE]
Podczas integracji dziennika Azure to rozwiązanie bezpłatne, istnieją wynikające z magazynu informacji o pliku dziennika hello koszty usługi Azure storage.

Społeczność pomoc jest dostępna za pośrednictwem hello [Forum MSDN integracji dziennika Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Hello forum zapewnia hello AzLog społeczności hello możliwości toosupport siebie pytania, odpowiedzi, porady i wskazówki na jak tooget najbardziej hello poza integracji dziennika Azure. Ponadto hello Azure dziennika integracji zespołu monitoruje tym forum i zawierają informacje pomocne przy każdym możemy.

Można również otworzyć [żądania obsługi](../azure-supportability/how-to-create-azure-support-request.md). toodo ten, wybierz **integracji dziennika** jako usługa hello żądania pomocy technicznej.

## <a name="next-steps"></a>Następne kroki
W tym dokumencie możesz zostały wprowadzone tooAzure dziennika integracji. toolearn więcej informacji na temat usługi Azure dziennika integracji i typy hello dzienników obsługiwane, zobacz następujące hello:

* [Microsoft Azure dziennika integracji](https://www.microsoft.com/download/details.aspx?id=53324) — Centrum pobierania, aby uzyskać szczegółowe informacje, wymagania systemowe i zainstalować instrukcje dotyczące integracji dzienników Azure.
* [Wprowadzenie do integracji dzienników Azure](security-azure-log-integration-get-started.md) — w tym samouczku przeprowadzi Cię przez proces instalacji integracji dzienników Azure i integrowanie dzienniki z magazynu Azure WAD, dzienniki aktywności platformy Azure, alerty Centrum zabezpieczeń Azure i usługi Azure Active Directory dzienniki inspekcji.
* [Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — ten wpis w blogu pokazuje, jak tooconfigure Azure dziennika toowork integracji z rozwiązań partnerskich Splunk HP ArcSight i IBM QRadar. Ten blog reprezentuje nasze bieżące położenie na temat konfigurowania hello rozwiązań partnerskich. We wszystkich przypadkach można znaleźć w dokumentacji rozwiązania toopartner najpierw.
* [Działanie i ASC alertów za pośrednictwem syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) — ten wpis w blogu instrukcje hello alerty Centrum zabezpieczeń Azure i działania toosend za pośrednictwem syslog tooQRadar
* [Dzienników Azure — często zadawane pytania (FAQ) integracji](security-azure-log-integration-faq.md) — to często zadawane pytania dotyczące odpowiedzi na pytania dotyczące integracji dzienników Azure.
* [Integrowanie Centrum zabezpieczeń alertów z usługi Azure dziennika integracji](../security-center/security-center-integrating-alerts-with-log-integration.md) — tym dokumencie przedstawiono, jak alerty Centrum zabezpieczeń Azure toosync z integracją dziennika Azure.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
