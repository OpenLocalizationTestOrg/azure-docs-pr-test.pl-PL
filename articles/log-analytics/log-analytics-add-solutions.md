---
title: "rozwiązania do zarządzania Azure Log Analytics aaaAdd | Dokumentacja firmy Microsoft"
description: "Operations Management Suite (OMS) / Log Analytics rozwiązania do zarządzania są Kolekcja reguł nabycia logiki, wizualizacji i danych zawierających metryki przestawiać wokół obszaru określonego problemu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Dodaj obszar roboczy usługi Azure Log Analytics management rozwiązań tooyour

Dziennik rozwiązań do zarządzania Analytics to zbiór **logiki**, **wizualizacji**, i **reguły pozyskiwania danych** zawierających metryki przestawiać wokół obszaru określonego problemu. W tym artykule wymieniono obsługiwane przez analizy dzienników rozwiązania do zarządzania i pokazuje, jak tooadd i usuwanie obszaru roboczego przy użyciu hello portalu Azure. Można również dodać rozwiązań w portalu OMS hello za pomocą galerii rozwiązań hello.

Zezwalaj na lepszy wgląd do rozwiązania do zarządzania:

* Ułatwić badanie i rozwiązywanie problemów z działaniem szybciej
* Zbieranie i skorelowania różnych typów danych komputera
* Pomogą Ci aktywnego z działaniami, które udostępnia hello rozwiązania.

> [!NOTE]
> Analiza dzienników udostępnia funkcję wyszukiwania dziennika, więc nie trzeba tooinstall tooenable rozwiązania zarządzania go. Jednak otrzymasz wizualizacjami danych, sugerowane wyszukiwania i szczegółowe informacje, dodając roboczym tooyour rozwiązań do zarządzania.

Korzystając z tego artykułu, należy dodać roboczym tooa rozwiązań do zarządzania przy użyciu hello portalu Azure Marketplace. Po dodaniu rozwiązania, dane są zbierane z serwerów hello w infrastrukturze i wysłane toohello usługę. Przetwarzanie przez powitalne usługę zwykle trwa kilka minut tooan godzinę. Po hello usługa przetwarza dane hello, można go wyświetlić w OMS.

Gdy nie jest już potrzebne, można łatwo usunąć rozwiązania do zarządzania. Podczas usuwania rozwiązania do zarządzania jego dane nie są wysyłane tooOMS. Jeśli na powitania bezpłatnej warstwy cenowej, usuwanie rozwiązania można skrócić hello danych, pomaga pozostają w obszarze dzienny limit przydziału danych.

## <a name="view-available-management-solutions"></a>Widok zarządzania dostępnych rozwiązań

Hello Azure marketplace zawiera listę hello [rozwiązań do zarządzania dla analizy dzienników](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Rozwiązania do zarządzania można zainstalować z portalu Azure marketplace, klikając hello **Pobierz teraz** łącze u dołu hello poszczególnych rozwiązań.

## <a name="add-a-management-solution"></a>Dodaj rozwiązanie do zarządzania
1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com) przy użyciu subskrypcji platformy Azure.
2. W hello **nowy** bloku w obszarze **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie**.
3. W hello **monitorowanie i zarządzanie** bloku, kliknij przycisk **zobaczyć wszystkie**.  
    ![Monitorowanie + blok zarządzania](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello prawo **rozwiązań do zarządzania**, kliknij przycisk **więcej**.
5. W hello **rozwiązań do zarządzania** bloku, wybierz rozwiązanie do zarządzania, które mają tooadd tooa roboczym.  
    ![Monitorowanie + blok zarządzania](./media/log-analytics-add-solutions/management-solutions.png)  
6. W bloku rozwiązania zarządzania hello, przejrzyj informacje dotyczące hello rozwiązania do zarządzania, a następnie kliknij **Utwórz**.
7. W hello *Nazwa rozwiązania zarządzania* bloku, wybierz obszar roboczy, które mają tooassociate z rozwiązaniem do zarządzania hello.
8. Opcjonalnie można zmienić ustawienia obszaru roboczego dla hello subskrypcji platformy Azure, lokalizacji i grupy zasobów. Można również wybrać **opcje automatyzacji**. Kliknij przycisk **Utwórz**.  
    ![obszar roboczy rozwiązania](./media/log-analytics-add-solutions/solution-workspace.png)  
9. za pomocą rozwiązania do zarządzania hello dodano roboczym tooyour toostart Przejdź zbyt**analizy dzienników** > **subskrypcje** > ***nazwa obszaru roboczego ***  >  **Omówienie**. Zostanie wyświetlony nowy Kafelek rozwiązania do zarządzania. Kliknij przycisk tooopen kafelka hello go, a następnie rozpocznij za pomocą rozwiązania hello, po zebraniu danych hello rozwiązania.

## <a name="remove-a-management-solution"></a>Usuń rozwiązanie do zarządzania

1. W hello [portalu Azure](https://portal.azure.com), przejdź do zbyt**analizy dzienników** > **subskrypcje** > ***nazwa obszaru roboczego*** następnie w hello ***nazwa obszaru roboczego*** bloku, kliknij przycisk **rozwiązań**.
2. Na liście hello rozwiązań do zarządzania wybierz hello rozwiązania, które mają tooremove.
3. W bloku rozwiązania hello obszaru roboczego kliknij **usunąć**.  
    ![Usuwanie rozwiązania](./media/log-analytics-add-solutions/solution-delete.png)  
4. W oknie dialogowym potwierdzenia powitania kliknij **tak**.

## <a name="offers-and-pricing-tiers"></a>Oferty i warstw cenowych

Witaj w poniższej tabeli identyfikuje rozwiązania zarządzania należy tooeach oferty usługi Operations Management Suite.
Tabela Hello identyfikuje również hello ceny warstw, które są dostępne dla poszczególnych rozwiązań do zarządzania.
Wszystkie rozwiązania w hello w poniższej tabeli są dostępne z poziomu portalu i hello rozwiązań galerii Azure w portalu usługi Analiza dzienników hello hello.

| Rozwiązanie do zarządzania                                                                       | Oferta                                                                     | Warstwa cenowa<sup>1</sup>                                                 | Uwagi |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | 90 dni dane są dostępne bezpłatnie<br>Dane nie podmiotu toohello zakończenia warstwa bezpłatna |
| [Ocena usługi AD](log-analytics-ad-assessment.md)                                           | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Stan replikacji usługi AD](log-analytics-ad-replication-status.md)                           | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Kondycja agenta](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Dane nie podmiotu toohello zakończenia warstwa bezpłatna<br> Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Zarządzanie alertami](log-analytics-solution-alert-management.md)                            | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Łącznik aplikacji Insights (wersja zapoznawcza)](log-analytics-app-insights-connector.md)                                               | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Automatyzacja hybrydowego procesu roboczego](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automatyzacja i kontrola</li></ul>                                  | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji |
| [Analiza bramy aplikacji Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Grupy zabezpieczeń sieci Azure analityka](log-analytics-azure-networking-analytics.md)     | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Analiza Azure SQL (wersja zapoznawcza)](log-analytics-azure-sql.md)                                                       | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br>Na&nbsp;węzła&nbsp;(OMS)                                                                          | Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji|
| [Analiza w usłudze Azure Web Apps](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
|[Tworzenie kopii zapasowych](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Wgląd w dane i analizy</li></ul>                                   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)                                                                       | Wymaga klasycznego magazyn kopii zapasowych.<br> Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Pojemność i wydajność (wersja zapoznawcza)](log-analytics-capacity.md)                                                   | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Śledzenie zmian](log-analytics-change-tracking.md)                                       | <ul><li>Automatyzacja i kontrola</li></ul>                                  | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji |
| [Kontenery](log-analytics-containers.md)                                                 | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [IT usługi łącznika Management (wersja zapoznawcza)](log-analytics-itsmc-overview.md)                                              | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)     | |
| HDInsight HBase monitorowania <br>(Wersja zapoznawcza)                                                  | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Analiza usługi Key Vault](log-analytics-azure-key-vault.md)                   | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [B2B aplikacje logiki](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Ocena złośliwego oprogramowania](log-analytics-malware.md)                                            | <ul><li>Zabezpieczenia i zgodność</li></ul>                                 | Bezpłatna<br> Autonomiczna<br>Na&nbsp;węzła&nbsp;(OMS)                                                                           | Dodania rozwiązań zabezpieczeń i zgodności powitania po 19 czerwca 2017 [rozliczeń jest na węzeł](https://azure.microsoft.com/pricing/details/security-compliance/), niezależnie od obszaru roboczego hello warstwy cenowej. Hello są wolne pierwsze 60 dni.  |
| [Monitor wydajności sieci](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Wgląd w dane i analizy</li></ul>                                   | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | |
| [Analiza usługi Office 365 (wersja zapoznawcza)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Zabezpieczenia i inspekcja](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Zabezpieczenia&nbsp;i&nbsp;zgodności</li></ul>                       | Bezpłatna<br> Autonomiczna<br>Na&nbsp;węzła&nbsp;(OMS)                                                                           | Zbieranie dzienników zdarzeń zabezpieczeń wymaga tego rozwiązania<br>Dodania rozwiązań zabezpieczeń i zgodności powitania po 19 czerwca 2017 [rozliczeń jest na węzeł](https://azure.microsoft.com/pricing/details/security-compliance/), niezależnie od obszaru roboczego hello warstwy cenowej. Hello są wolne pierwsze 60 dni. |
| [Usługa sieci szkieletowej Analytics (wersja zapoznawcza)](log-analytics-service-fabric.md)                     | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Mapa usług (wersja zapoznawcza)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Wgląd w dane i analizy</li></ul>                      | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Dostępne w wschodnie stany USA, Europa Zachodnia, zachodnie środkowe stany USA    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Wgląd w dane i analizy</li></ul>                                   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)                                                                       | Wymaga klasycznego magazynu usługi Site Recovery.<br> Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Ocena serwera SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| Uruchamianie lub zatrzymywanie maszyn wirtualnych po godzinach pracy<br>(Wersja zapoznawcza)                                              | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Do oceny programu System Center Operations Manager (wersja zapoznawcza)](log-analytics-scom-assessment.md)  | <ul><li>Wgląd w dane i analizy</li><li>Log Analytics</li></ul>        | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Zarządzanie aktualizacjami](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automatyzacja i kontrola</li></ul>                                  | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji |
| [Informacje o zgodności aktualizacji (wersja zapoznawcza)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Bezpłatne danych lub w węzłach<br>Dane podlegające nie toohello warstwę bezpłatna centralnych zasad dostępu.<br> Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [Gotowość do uaktualnienia](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | Bezpłatne danych lub w węzłach<br>Dane podlegające nie toohello warstwę bezpłatna centralnych zasad dostępu.<br> Tooadd nie jest dostępna z portalu Azure/portalu marketplace. |
| [VMware monitorowania (wersja zapoznawcza)](log-analytics-vmware.md)                                | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Standardowa<br> Premium&nbsp;(OMS)<br> Na&nbsp;GB&nbsp;(autonomiczna)<br> Na&nbsp;węzła&nbsp;(OMS)   | |
| [Podczas transmisji danych 2.0 (wersja zapoznawcza)](log-analytics-wire-data.md)                                                                 | <ul><li>Wgląd w dane i analizy</li></ul>                                   | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)                                                                         | Dostępne w wschodnie stany USA, Europa Zachodnia, zachodnie środkowe stany USA |

<sup>1</sup> hello *standardowe* i *Premium (OMS)* warstwy cenowej są dostępne tylko dla klientów, którzy utworzone ich analizy dzienników obszaru roboczego wcześniejsze tooSeptember 21, 2016.

### <a name="community-provided-management-solutions"></a>Społeczność podane rozwiązania do zarządzania

Są dostępne z hello rozwiązania społeczności podane [galerii szablonu Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) i bezpośrednio z hello autorów.

| Rozwiązanie do zarządzania               | Oferta                                                                     | Warstwy cenowe                         | Uwagi |
| ---                               | ---                                                                       | ---                                   | ---   |
| Wszystkie rozwiązania podane społeczności  | <ul><li>Szczegółowe informacje o&nbsp;i&nbsp;analityka</li><li>Log Analytics</li></ul>   | Bezpłatna<br> Na&nbsp;węzła&nbsp;(OMS)     |   Wymaga programu tooan toobe połączone obszaru roboczego analizy dzienników konta automatyzacji |




## <a name="data-collection-details"></a>Szczegóły danych kolekcji
Witaj w poniższych tabelach metody zbierania danych i inne szczegółowe informacje o sposobie dane są zbierane dla analizy dzienników zarządzania rozwiązań i źródeł danych. Witaj tabele są pogrupowane według oferty rozwiązania, które są równoważne zbyt[subskrypcji warstw cenowych](https://go.microsoft.com/fwlink/?linkid=827926). Witaj rozwiązania analizy dziennika aktywności jest tooall dostępne bezpłatnie warstw cenowych.

Witaj Windows analizy dziennika agenta i System Center Operations Manager agent są zasadniczo hello takie same. Hello Windows agent zawiera dodatkowe funkcje tooallow on tooconnect toohello OMS obszaru roboczego i tras za pośrednictwem serwera proxy. Jeśli używasz agenta programu Operations Manager, musi być przeprowadzone jako toocommunicate agent pakietu OMS z usługą OMS. Agenci programu Operations Manager w tej tabeli są OMS agentów, które są połączone tooOperations Manager. Zobacz [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md) informacji o podłączaniu programu istniejących tooOMS środowiska programu Operations Manager.

> [!NOTE]
> Typ Hello agenta, którego używasz Określa, jak dane są wysyłane tooOMS, hello następujące warunki:
> - Możesz użyć agenta Windows hello lub dołączone do programu Operations Manager agent pakietu OMS.
> - Gdy wymagana jest programu Operations Manager, danych agenta programu Operations Manager dla rozwiązania hello zawsze są wysyłane przy użyciu grupy zarządzania programu Operations Manager hello tooOMS. Ponadto jeśli programu Operations Manager jest wymagane, tylko agenta programu Operations Manager hello jest używany przez rozwiązanie hello.
> - Gdy programu Operations Manager nie jest wymagana i hello tabeli pokazano, że danych agenta programu Operations Manager są przesyłane przy użyciu hello grupy zarządzania, a następnie danych agenta programu Operations Manager tooOMS zawsze są wysyłane tooOMS przy użyciu grup zarządzania. Agentów systemu Windows obejścia hello grupy zarządzania i wysyłają dane tooOMS bezpośrednio.
> - Gdy danych agenta programu Operations Manager nie są wysyłane przy użyciu grupy zarządzania, następnie hello dane wysyłane bezpośrednio tooOMS — pomijanie hello grupy zarządzania.

### <a name="insight--analytics--log-analytics"></a>Szczegółowe informacje o & Analytics / Log Analytics

| Rozwiązanie do zarządzania | Platforma | Agent monitorowania firmy Microsoft | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Activity Log Analytics | Azure |   |   |   |   |   | na powiadomienia |
| Ocena usługi AD |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dni |
| Stan replikacji usługi AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 dni |
| Kondycja agenta | System Windows i Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minuta |
| Zarządzania alertami (Nagios) |Linux |&#8226; |  |  |  |  |po przybyciu |
| Zarządzania alertami (Zabbix) |Linux |&#8226; |  |  |  |  |1 minuta |
| Zarządzania alertami (program Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minuty |
| Łącznik aplikacji Insights (wersja zapoznawcza) | Azure |   |   |   |   |   | na powiadomienia |
| Analiza bramy aplikacji Azure | Azure |   |   |   |   |   | na powiadomienia |
| Grupy zabezpieczeń sieci Azure analityka | Azure |   |   |   |   |   | na powiadomienia |
| Analiza Azure SQL (wersja zapoznawcza) |Windows |  |  |  |  |  | 10 minut |
| Zarządzanie pojemnością |Windows |&#8226; |&#8226; |  |  |&#8226; |po przybyciu |
| Kontenery | System Windows i Linux | &#8226; | &#8226; |   |   |   | 3 minuty |
| Analityka magazynu kluczy |Windows |  |  |  |  |  |na powiadomienia |
| Monitor wydajności sieci | Windows | &#8226; | &#8226; |   |   |   | TCP uzgodnienia co 5 sekund, dane wysyłane co 3 minuty |
| Analiza usługi Office 365 (wersja zapoznawcza) |Windows |  |  |  |  |  |na powiadomienia |
| Usługa sieci szkieletowej analityka |Windows |  |  |&#8226; |  |  |5 minut |
| Mapa usługi | System Windows i Linux | &#8226; | &#8226; |   |   |   | 15 sekund |
| Ocena serwera SQL |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dni |
| SurfaceHub |Windows |&#8226; |  |  |  |  |po przybyciu |
| Do oceny programu System Center Operations Manager (wersja zapoznawcza) | Windows | &#8226; | &#8226; |   |   | &#8226; | 7 dni |
| Uaktualnij Analytics (wersja zapoznawcza) | Windows | &#8226; |   |   |   |   | 2 dni |
| VMware monitorowania (wersja zapoznawcza) | Linux | &#8226; |   |   |   |   | 3 minuty |
| Dane o komunikacji sieciowej |Systemu Windows (2012 R2 / 8.1 lub nowszy) |&#8226; |&#8226; |  |  |  | 1 minuta |


### <a name="automation--control"></a>Automatyzacja i kontrola

| Rozwiązanie do zarządzania | Platforma | Agent monitorowania firmy Microsoft | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automatyzacja hybrydowego procesu roboczego | Windows | &#8226; | &#8226; |   |   |   | Nie dotyczy |
| Śledzenie zmian |Windows |&#8226; |&#8226; |  |  |&#8226; |co godzinę |
| Śledzenie zmian |Linux |&#8226; |  |  |  |  |co godzinę |
| Zarządzanie aktualizacjami | Windows |&#8226; |&#8226; |  |  |&#8226; |co najmniej 2 razy dziennie i 15 minut po zainstalowaniu aktualizacji |

### <a name="security--compliance"></a>Zabezpieczenia i zgodność z przepisami

| Rozwiązanie do zarządzania | Platforma | Agent monitorowania firmy Microsoft | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Ocena ochrony przed złośliwym oprogramowaniem |Windows |&#8226; |&#8226; |  |  |&#8226; |co godzinę |
| Bezpieczeństwo i inspekcji<sup>1</sup> | System Windows i Linux | częściowe | częściowe | częściowe |   | częściowe | różne |

<sup>1</sup> hello zabezpieczeń i rozwiązanie inspekcji mogą zbierać dzienniki z systemu Windows, programu Operations Manager i systemu Linux. Zobacz [źródeł danych](#data-sources) danych zbierania informacji o:

- Dziennik systemu
- Dzienniki zdarzeń zabezpieczeń systemu Windows
- Dzienniki zapory systemu Windows
- Dzienniki zdarzeń systemu Windows



### <a name="protection--recovery"></a>Ochrona i odzyskiwanie

| Rozwiązanie do zarządzania | Platforma | Agent monitorowania firmy Microsoft | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Tworzenie kopii zapasowych | Azure |   |   |   |   |   | Nie dotyczy |
| Azure Site Recovery | Azure |   |   |   |   |   | Nie dotyczy |


### <a name="data-sources"></a>Źródła danych


| Źródło danych | Platforma | Agent monitorowania firmy Microsoft | Agent programu Operations Manager | Azure Storage | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Dzienniki aktywności platformy Azure |Windows |  |  |  |  |  |na powiadomienia |
| Dzienniki diagnostyczne platformy Azure |Windows |  |  |  |  |  |na powiadomienia |
| Metryki diagnostycznych platformy Azure |Windows |  |  |  |  |  |na powiadomienia |
| ETW |Windows |  |  |&#8226; |  |  |5 minut |
| Dzienniki programu IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minut |
| Liczniki wydajności |Windows |&#8226; |&#8226; |  |  |  |jako zaplanowane, co najmniej 10 sekund |
| Liczniki wydajności |Linux |&#8226; |  |  |  |  |jako zaplanowane, co najmniej 10 sekund |
| Dziennik systemu |Linux |&#8226; |  |  |  |  |z usługi Azure storage: 10 minut; od agenta: Przy nadejściu |
| Dzienniki zdarzeń zabezpieczeń systemu Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |dla usługi Azure storage: 10 min; dla agenta hello: Przy nadejściu |
| Dzienniki zapory systemu Windows |Windows |&#8226; |&#8226; |  |  |  |po przybyciu |
| Dzienniki zdarzeń systemu Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |dla usługi Azure storage: 10 min; dla agenta hello: Przy nadejściu |



## <a name="preview-management-solutions-and-features"></a>Podgląd rozwiązania do zarządzania i funkcje
Uruchamiając usługi i wskazówek devops, możemy stanie toopartner z klientów toodevelop funkcji i rozwiązań.

Prywatnej wersji zapoznawczej możemy podać dla niewielkiej liczby klientów dostępu tooan wcześniejszego wykonania hello funkcji lub rozwiązanie toogain opinii i poprawiają. Ta implementacja wczesne ma minimalne funkcje i możliwości operacyjnych.

Naszym celem jest rzeczy tootry szybko, więc można odnaleźć co działa, a czego nie działa. Firma Microsoft Iterowanie za pomocą tego procesu, dopóki hello opinie od klientów prywatnej wersji zapoznawczej hello poinformuje, że jesteśmy gotowi publicznej wersji zapoznawczej.

Hello publicznej wersji zapoznawczej firma Microsoft udostępnia funkcję hello lub rozwiązania dla wszystkich użytkowników tooget więcej opinii i zweryfikować naszych skalowania i wydajność. W tej fazie:

* Funkcje w wersji zapoznawczej są wyświetlane na karcie Ustawienia hello i można ją włączyć przez dowolnego użytkownika.
* Podgląd rozwiązania zostaną dodane za pośrednictwem galerii hello lub za pomocą skryptu.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Co należy wiedzieć o funkcje w wersji zapoznawczej i rozwiązania?
Firma Microsoft Cieszymy się o nowych funkcjach i rozwiązań do zarządzania i przyłączyć Praca z toodevelop możesz je.

Funkcje w wersji zapoznawczej i rozwiązania nie są odpowiednie dla wszystkich. Przed pytaniem toojoin prywatnej wersji zapoznawczej i włączanie publicznej wersji zapoznawczej, upewnij się, że pracujesz OK z elementem jest w fazie projektowania.

Podczas włączania funkcji testowania za pośrednictwem portalu hello, zobaczysz ostrzeżenie przypominający, że funkcja hello jest w wersji zapoznawczej.

#### <a name="for-both-private-and-public-preview"></a>Dla obu *prywatnej* i *publicznego* podglądu
Witaj poniższe informacje dotyczą wersji zapoznawczych publiczne i prywatne tooboth:

* Czynności może nie zawsze działać poprawnie.
  * Problemy z zakresu od są niewielkie określenia dokuczliwości za pośrednictwem toosomething nie działa na wszystkich.
* Istnieje możliwość toohave Podgląd hello negatywnego wpływu na system / środowiska.
  * Spróbujemy tooavoid ujemna rzeczy, które występują w toku toohello systemów, używanego z usługą OMS, ale czasami nieoczekiwane elementy.
* Utrata danych / może spowodować uszkodzenie.
* Firma Microsoft może poprosić możesz dzienników diagnostycznych toocollect lub innych danych toohelp Rozwiązywanie problemów z.
* Funkcja Hello lub rozwiązania mogą zostać usunięte (tymczasowo lub na stałe).
  * Oparte na naszych learnings hello w wersji zapoznawczej firma Microsoft może zadecydować funkcja hello wersji toonot lub rozwiązania.
* Podgląd może nie działać lub może nie przetestowano we wszystkich konfiguracjach i firma Microsoft może ograniczyć:
  * Witaj systemów operacyjnych, które mogą być używane (na przykład funkcja może tylko zastosować tooLinux znajduje się w wersji zapoznawczej).
  * Witaj typu agent (MMA, Operations Manager), który może służyć (na przykład funkcja może nie działać z programem Operations Manager znajduje się w wersji zapoznawczej).  
* Podgląd rozwiązań i funkcje nie są objęte hello umową dotyczącą poziomu usług.
* Opłaty za użycie wiąże się z użycia funkcji w wersji zapoznawczej.
* Funkcje lub możliwości, że wymagane dla funkcji hello / toobe rozwiązanie przydatne mogą być brakujące lub niekompletne.
* Funkcje / rozwiązania nie mogą być dostępne we wszystkich regionach.
* Funkcje / rozwiązania nie może być lokalizowany.
* Funkcje / rozwiązania może mieć limit na liczbę hello klientów lub urządzeń, które może być używany.
* Toouse skrypty tooperform konfiguracji tooenable hello rozwiązania/funkcja i może być konieczne.
* Witaj interfejsu użytkownika (UI) jest niekompletne i mogą ulec zmianie od tooday dnia.
* Podglądy publiczny nie może być odpowiednie dla produkcyjnego / krytyczne systemów.

#### <a name="for-private-preview"></a>Aby uzyskać *prywatnej* podglądu
W powyższych elementów toohello dodanie hello następujących informacji jest podglądy określonych tooprivate:

* Oczekujemy tooprovide nam opinii na środowiska, aby firma Microsoft może wprowadzać hello rozwiązanie lub funkcję lepiej.
* Firma Microsoft może skontaktować się z Tobą opinii przy użyciu ankietach, połączenia telefoniczne lub wiadomości e-mail.
* Elementy zawsze nie działa prawidłowo.
* Firma Microsoft może wymagać Non-ujawnienie umowy (NDA) udziału lub mogą obejmować poufnej zawartości.
  * Przed przystąpieniem do obsługi blogów, tweeting lub inny sposób komunikowania się z innym firmom Sprawdź, czy z hello Menedżera Program, który jest odpowiedzialny za toounderstand Podgląd hello ograniczeń na ujawnienie.
* Nie należy uruchamiać w środowisku produkcyjnym / krytyczne systemów.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Jak uzyskać dostęp do funkcji w wersji zapoznawczej tooprivate i rozwiązania
Zapraszamy podglądy tooprivate klientów za pośrednictwem kilka różnych sposobów, w zależności od wersji zapoznawczej hello.

* Udzielenie odpowiedzi na powitania miesięczne Ankieta klienta i udzielenie nam uprawnień toofollow z Tobą zwiększa szanse trwa zaproszonych tooa prywatnej wersji zapoznawczej.
* Zespół obsługi klienta firmy Microsoft można wyznaczyć użytkownik.
* Możesz utworzyć konto elementy opublikowane w serwisie twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* Możesz utworzyć konto na podstawie zdarzeń udostępnionego społeczności szczegóły — przyjrzeć się firmie Microsoft spełniają ups konferencji w społeczności online.

## <a name="next-steps"></a>Następne kroki
* [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe informacje zebrane przez rozwiązania do zarządzania.
