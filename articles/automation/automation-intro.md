---
title: "Omówienie usługi Azure Automation | Microsoft Docs"
description: "Dowiedz się, jak używać usługi Azure Automation do automatyzacji cyklu życia infrastruktury i aplikacji."
services: automation
author: eamonoreilly
documentationcenter: 
keywords: "azure automation, DSC, powershell, konfiguracja żądanego stanu, zarządzanie aktualizacjami, śledzenie zmian, spis, elementy runbook, python, graficzne"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/13/2017
ms.author: eamono
ms.custom: mvc
ms.openlocfilehash: 896bcd9630a6a7c942bd3f1a986832442a474cce
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="an-introduction-to-azure-automation"></a>Wprowadzenie do usługi Azure Automation

Usługa Azure Automation udostępnia opartą na chmurze usługę automatyzacji i konfiguracji, która zapewnia spójne zarządzanie w środowiskach platformy Azure i w innych środowiskach. Obejmuje ona automatyzację procesów, zarządzanie aktualizacjami i funkcje konfiguracji. Usługa Azure Automation zapewnia pełną kontrolę podczas wdrażania, działania i likwidacji obciążeń i zasobów.
Ten artykuł zawiera krótkie omówienie usługi Azure Automation i odpowiedzi na niektóre często zadawane pytania. Aby uzyskać więcej informacji o różnych możliwościach, odwiedź linki zawarte w tym omówieniu.

## <a name="azure-automation-capabilities"></a>Możliwości usługi Azure Automation

![Możliwości automatyzacji — omówienie](media/automation-overview/automation-overview.png)

### <a name="process-automation"></a>Automatyzacja procesów

Usługa Azure Automation zapewnia możliwość automatyzacji częstych, czasochłonnych i podatnych na błędy zadań zarządzania w chmurze. Ta automatyzacja pozwala skoncentrować się na pracy, która przynosi wymierne efekty ekonomiczne. Poprzez zmniejszenie liczby błędów i zwiększenie wydajności pozwala ona również zmniejszyć koszty operacyjne. Możesz zintegrować usługi platformy Azure i innych systemów publicznych, które są wymagane podczas wdrażania, konfigurowania i zarządzania całościowymi procesami. Usługa umożliwia graficzne [tworzenie elementów Runbook](automation-runbook-types.md) w programie PowerShell lub Python. Przy użyciu hybrydowego procesu roboczego elementu Runbook, możesz ujednolicić zarządzanie poprzez organizowanie środowisk lokalnych. [Elementy Webhook](automation-webhooks.md) określają sposób spełniania żądań i zapewniania ciągłego dostarczania oraz operacji, wyzwalając automatyzację z ITSM, DevOps oraz monitorowanie systemów.

### <a name="configuration-management"></a>Zarządzanie konfiguracją

[Konfiguracja żądanego stanu](automation-dsc-overview.md) usługi Azure Automation to oparte na chmurze rozwiązanie dla konfiguracji PowerShell DSC, które świadczy usługi wymagane w środowiskach przedsiębiorstw. Zarządzaj swoimi zasobami DSC w usłudze Azure Automation i stosuj konfiguracje do maszyn wirtualnych lub fizycznych z serwera ściągania konfiguracji DSC w chmurze platformy Azure. Rozwiązanie to udostępnia raporty, które informują Cię o ważnych zdarzeniach, takich jak odchylenie węzłów od ich przypisanej konfiguracji. Możesz monitorować i automatycznie aktualizować konfigurację maszyn fizycznych i wirtualnych z systemami Windows lub Linux w środowiskach lokalnych oraz w chmurze.

Możesz uzyskać spis zasobów gościa w celu umożliwienia wglądu w zainstalowane aplikacje i inne elementy konfiguracji. Dostępne są bogate możliwości raportowania i wyszukiwania pozwalające szybko znaleźć szczegółowe informacje pomagające zrozumieć, co jest skonfigurowane w ramach systemu operacyjnego. Możesz śledzić zmiany w usługach, demonach, oprogramowaniu, rejestrze i plikach, aby szybko określić, co może powodować problemy. Ponadto DSC może ułatwić diagnozowanie i generowanie alertów w przypadku wystąpienia niepożądanych zmian w środowisku.

### <a name="update-management"></a>Zarządzanie aktualizacjami

Aktualizuj systemy Windows i Linux w środowiskach hybrydowych za pomocą usługi Azure Automation. Uzyskasz widoczność zgodności aktualizacji na platformie Azure, lokalnie i w innych chmurach. Możesz utworzyć harmonogram wdrożenia w celu zorganizowania instalacji aktualizacji w ramach określonego okna konserwacji. Jeśli nie można zainstalować aktualizacji na maszynie, możesz wykluczyć te aktualizacje z wdrożenia.

### <a name="shared-capabilities"></a>Współdzielone możliwości

Usługa Azure Automation zawiera zestaw współdzielonych zasobów, które ułatwiają automatyzowanie i konfigurowanie środowiska odpowiednio do skali.

* **[Kontrola dostępu oparta na rolach](automation-role-based-access-control.md)** — kontrola dostępu do konta z rolą operatora usługi Automation umożliwiająca uruchamianie zadań bez przekazywania możliwości tworzenia.
* **[Zmienne](automation-variables.md)** — udostępniają sposób przechowywania zawartości, którą można stosować w przypadku elementów Runbook i konfiguracji. Możesz zmienić wartości bez konieczności modyfikowania jakichkolwiek elementów Runbook i konfiguracji, które odwołują się do nich.
* **[Poświadczenia](automation-credentials.md)** — bezpiecznie przechowuj poufne informacje, które mogą być używane przez elementy Runbook i konfiguracje w środowisku uruchomieniowym.
* **[Certyfikaty](automation-certificates.md)** — przechowywanie i udostępnianie w środowisku uruchomieniowym, więc mogą służyć do uwierzytelniania i zabezpieczania wdrożonych zasobów.
* **[Połączenia](automation-connections.md)** — zapisywanie par nazwa/wartość informacji zawierających wspólne informacje podczas nawiązywania połączenia z systemami w zasobach połączenia. Połączenia są definiowane przez autora modułu w celu użycia w środowisku uruchomieniowym w elementach Runbook i konfiguracjach.
* **[Harmonogramy](automation-schedules.md)** — używane przez usługę do wyzwalania automatyzacji we wstępnie zdefiniowanym czasie.
* **[Integracja z kontrolą źródła](automation-source-control-integration.md)** — wspiera konfigurację jako kod, gdzie elementy Runbook i konfiguracje można sprawdzić w systemie kontroli źródła.
* **[Moduły programu PowerShell](automation-integration-modules.md)** — moduły są używane do zarządzania platformą Azure i innymi systemami. Importowanie do konta usługi Automation firmy Microsoft poleceń cmdlet i zasobów DSC innych firm, społeczności lub niestandardowo zdefiniowanych.

### <a name="windows-and-linux"></a>System Windows i Linux

Usługa Azure Automation jest przeznaczona do pracy w środowisku chmury hybrydowej, a także w systemach Windows i Linux. Zapewnia spójny sposób automatyzacji i konfiguracji wdrożonych obciążeń i systemu operacyjnego, gdzie są uruchomione.

### <a name="community-gallery"></a>Galeria społeczności

Przeglądaj [Galerię automatyzacji](automation-runbook-gallery.md), szukając elementów Runbook i modułów, aby szybko rozpocząć integrowanie i tworzenie swoich procesów z galerii programu PowerShell i centrum skryptów firmy Microsoft.

## <a name="common-scenarios-for-automation"></a>Typowe scenariusze dotyczące usługi Automation

Usługa Azure Automation zarządza cyklem życia Twojej infrastruktury i aplikacji. Transferuj do systemu wiedzę na temat sposobu, w jaki organizacja dostarcza i utrzymuje obciążenia. Twórz w typowych w językach programu PowerShell, konfiguruj żądany stan, język Python i graficzne elementy Runbook. Pobieraj pełny spis wdrożonych zasobów dla określania miejsc docelowych, raportowania i zgodności. Identyfikuj zmiany, które mogą spowodować błąd konfiguracji, i zwiększ zgodność operacyjną.

* **Tworzenie/wdrażanie zasobów** — wdrażanie maszyn wirtualnych w środowisku hybrydowym za pomocą szablonów elementów Runbook i usługi Azure Resource Manager. Integracja z narzędziami programistycznymi, takimi jak usługi Jenkins i Visual Studio Team Services.
* **Konfigurowanie maszyn wirtualnych** — ocena i konfigurowanie maszyn z systemem Windows i Linux z żądaną konfiguracją dla infrastruktury i aplikacji.
* **Monitorowanie** — identyfikowanie zmian w maszynach, które są przyczyną problemów i korygowanie lub eskalowanie do systemów zarządzania.
* **Ochrona** — poddawanie maszyn wirtualnych kwarantannie w przypadku wystąpienia alertu zabezpieczeń. Ustaw wymagania dotyczące gościa.
* **Zarządzanie** — konfigurowanie kontroli dostępu opartej na rolach dla zespołów. Odzyskaj nieużywane zasoby.

## <a name="pricing-for-automation"></a>Cennik usługi Automation

Możesz przejrzeć ceny usługi Azure Automation na stronie [cennika](https://azure.microsoft.com/pricing/details/automation/).

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Create an automation account](automation-quickstart-create-account.md) (Tworzenie konta automatyzacji)
