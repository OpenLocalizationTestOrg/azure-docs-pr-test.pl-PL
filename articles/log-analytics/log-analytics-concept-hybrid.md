---
title: "Zbieranie danych ze środowiska z Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten temat ułatwia zrozumienie, jak zbierać dane i monitorować komputery hostowanej w lokalnej lub w innym środowisku chmury z analizy dzienników."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: magoedte
ms.openlocfilehash: 513855084c8b89d97b049f1df2ec24d0f9789afe
ms.sourcegitcommit: d247d29b70bdb3044bff6a78443f275c4a943b11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/13/2017
---
# <a name="collect-data-from-computers-in-your-environment-with-log-analytics"></a>Zbieranie danych z komputerów w środowisku z analizy dzienników

Analiza dzienników Azure można zbierać i działają na danych z komputerów z systemem Windows lub Linux znajdującej się w:

* [Maszyny wirtualne platformy Azure](log-analytics-quick-collect-azurevm.md) przy użyciu rozszerzenia maszyny Wirtualnej analizy dzienników 
* Centrum danych jako serwerów fizycznych lub maszynach wirtualnych
* Maszyny wirtualne w usłudze hostowanych w chmurze, takich jak Amazon Web Services (AWS)

Komputery hostowanych w danym środowisku może być bezpośrednio połączony do analizy dzienników, lub jeśli już monitorowania tych komputerów z System Center Operations Manager 2012 R2 lub 2016, grupy zarządzania operacje zarządzania można zintegrować z analizy dzienników i kontynuacja, obsługi strategii i procesy operacji usługi.  

## <a name="overview"></a>Omówienie

![log-Analytics-Agent-Direct-Connect-diagram](media/log-analytics-concept-hybrid/log-analytics-on-prem-comms.png)

Przed analizowanie i działającą w zebranych danych, należy najpierw zainstalować i połączyć agentów dla wszystkich komputerów, które chcesz wysyłać dane z usługą analizy dzienników. Można zainstalować agentów na komputerach lokalnych przy użyciu Instalatora, wiersza polecenia lub z żądanego stanu konfiguracji (DSC) w automatyzacji Azure. 

Agenta dla systemu Linux i Windows komunikuje się wychodzące z usługą analizy dzienników za pośrednictwem portu TCP 443 i jeśli komputer łączy się z serwerem zapory lub serwera proxy do komunikacji za pośrednictwem Internetu, przejrzyj [Konfigurowanie agenta do użycia z serwerem proxy lub bramy OMS](#configuring-the-agent-for-use-with-a-proxy-server-or-oms-gateway) zrozumienie będzie zmian konfiguracji, należy zastosować. Jeśli monitorowanych komputerów z System Center 2016 - Operations Manager lub programu Operations Manager 2012 R2, można wieloadresowego z usługą analizy dzienników w celu zbierania danych i przekazywać je do usługi i nadal być monitorowane przez [programu Operations Manager ](log-analytics-om-agents.md). Komputery z systemem Linux monitorowane przez grupę zarządzania programu Operations Manager zintegrowany z analizy dzienników nie mają konfiguracji dla źródła danych i do przodu zebranych danych za pośrednictwem grupy zarządzania. Agent systemu Windows może raportować do czterech obszarów roboczych, a agenta systemu Linux obsługuje tylko do jednego obszaru roboczego raporty.  

Agent dla systemu Linux i Windows, który nie jest tylko w przypadku łączenia do analizy dzienników, obsługuje również automatyzacji Azure łączenia się z hostem roli procesu roboczego Runbook hybrydowego i rozwiązań do zarządzania takich jak śledzenia zmian i zarządzania aktualizacjami.  Aby uzyskać więcej informacji na temat roli hybrydowy proces roboczy elementu Runbook, zobacz [procesu roboczego Runbook hybrydowego automatyzacji Azure](../automation/automation-offering-get-started.md#automation-architecture-overview).  

Jeśli zasady zabezpieczeń IT nie zezwalają na komputerach w sieci, aby nawiązać połączenie z Internetem, aby połączyć się z bramą OMS do odbierania informacji o konfiguracji i wysyłania danych zebranych w zależności od rozwiązania, które aktywowano można skonfigurować agenta. Aby uzyskać więcej informacji i kroki dotyczące sposobu konfigurowania agenta systemu Linux lub Windows do komunikowania się za pośrednictwem bramy OMS z usługą analizy dzienników, zobacz [łączenia komputerów przy użyciu bramy OMS OMS](log-analytics-oms-gateway.md). 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem należy przejrzeć następujące informacje, aby sprawdzić, czy zostały spełnione minimalne wymagania systemowe.

### <a name="windows-operating-system"></a>System operacyjny Windows
Windows agent oficjalnie obsługuje następujące wersje systemu operacyjnego Windows:

* Windows Server 2008 Service Pack 1 (SP1) lub nowszy
* Windows 7 z dodatkiem SP1 lub nowszy.

#### <a name="network-configuration"></a>Konfiguracja sieci
Informacje poniżej listy proxy i zapory konfiguracji wymaganych informacji dla agenta systemu Windows do komunikowania się z analizy dzienników. Ruch jest wychodzący z sieci lokalnej z usługą analizy dzienników. 

| Zasób agenta | Porty | Obejście inspekcji HTTPS|
|----------------|-------|------------------------|
|*.ods.opinsights.azure.com |443 | Tak |
|*.oms.opinsights.azure.com | 443 | Tak | 
|*.blob.core.windows.net | 443 | Tak | 
|*.azure-automation.net | 443 | Tak | 

### <a name="linux-operating-systems"></a>Systemy operacyjne Linux
Oficjalnie obsługiwane są następujące dystrybucje systemu Linux.  Jednak agenta systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.

* Linux Amazon 2012.09 do 2015.09 (x86/x64)
* CentOS Linux 5, 6 i 7 (x86/x64)
* Oracle Linux 5, 6 i 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 i 7 (x86/x64)
* Debian GNU/Linux 6, 7 i 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, LTS 16.04 (x86/x64)
* SUSE Linux Enterprise Server 11 i 12 (x86/x64)

#### <a name="network-configuration"></a>Konfiguracja sieci
Informacje poniżej listy proxy i zapory konfiguracji wymaganych informacji dla agenta systemu Linux do komunikowania się z analizy dzienników. Ruch jest wychodzący z sieci lokalnej z usługą analizy dzienników. 

|Zasób agenta| Porty |  
|------|---------|  
|*.ods.opinsights.azure.com | Port 443|   
|*.oms.opinsights.azure.com | Port 443|   
|*.blob.core.windows.net | Port 443|   
|*.azure-automation.net | Port 443|  

Agent systemu Linux obsługuje komunikacji przy użyciu serwera proxy lub bramy OMS z usługą analizy dzienników przy użyciu protokołu HTTPS.  Obsługiwane są zarówno anonimowych, jak i podstawowego uwierzytelniania (nazwy użytkownika i hasła).  Podczas instalacji lub modyfikując plik konfiguracji proxy.conf po zakończeniu instalacji można określić serwer proxy.  

Wartość konfiguracji serwera proxy ma następującą składnię:

`[protocol://][user:password@]proxyhost[:port]`

> [!NOTE]
> Jeśli serwer proxy wymaga uwierzytelnienia, agenta systemu Linux nadal wymaga podania pseudo użytkownika/hasła. Może to być wszystkie nazwy użytkownika i hasła.

|Właściwość| Opis |
|--------|-------------|
|Protokół | https |
|użytkownik | Opcjonalna nazwa użytkownika dla uwierzytelniania serwera proxy |
|hasło | Opcjonalne hasło dla uwierzytelniania serwera proxy |
|proxyhost | Adres lub nazwę FQDN serwera proxy serwera/OMS bramy |
|port | Numer portu opcjonalne dla serwera proxy serwera/OMS bramy |

Na przykład: `https://user01:password@proxy01.contoso.com:30443`

> [!NOTE]
> Jeśli takie jak używać znaków specjalnych "@" hasło, komunikat o błędzie proxy połączenia, ponieważ wartość jest nieprawidłowo przeanalizowane.  Aby obejść ten problem, należy zakodować hasła w adresie URL przy użyciu narzędzia, takie jak [URLDecode](https://www.urldecoder.org/).  

## <a name="install-and-configure-agent"></a>Instalowanie i Konfigurowanie agenta 
Łączenie komputerów lokalnych bezpośrednio z Log Analytics można zrobić przy użyciu różnych metod w zależności od wymagań. W poniższej tabeli wymieniono każdej metody, aby określić, które najlepiej w Twojej organizacji.

|Element źródłowy | Metoda | Opis|
|-------|-------------|-------------|
| Komputer z systemem Windows|- [Instalacja ręczna](log-analytics-agent-windows.md)<br>- [Konfiguracja DSC automatyzacji Azure](log-analytics-agent-windows.md#install-the-agent-using-dsc-in-azure-automation)<br>- [Szablon Menedżera zasobów Azure stosu](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/MicrosoftMonitoringAgent-ext-win) |Zainstaluj program Microsoft Monitoring agent z wiersza polecenia lub przy użyciu zautomatyzowanej metody takie jak konfiguracja DSC automatyzacji Azure [System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/deploy-applications), lub za pomocą szablonu usługi Azure Resource Manager, jeśli wdrożono firmy Microsoft Azure stosu w centrum danych.| 
|Komputer z systemem Linux| [Instalacja ręczna](log-analytics-quick-collect-linux-computer.md)|Zainstaluj agenta dla systemu Linux w usłudze GitHub otoki skryptu podczas wywoływania. | 
| System Center Operations Manager|[Integrowanie programu Operations Manager z analizy dzienników](log-analytics-om-agents.md) | Skonfiguruj integrację programu Operations Manager i analizy dzienników do przekazywania zbiera dane z systemów Linux i Windows komputerów raportowania do grupy zarządzania.|  

## <a name="next-steps"></a>Następne kroki

* Przegląd [źródeł danych](log-analytics-data-sources.md) zrozumienie źródeł danych dostępnych do zbierania danych z systemu Windows lub Linux. 

* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania. 

* Dowiedz się więcej o [rozwiązań](log-analytics-add-solutions.md) czy dodać funkcje do analizy dzienników i również zbierać dane do repozytorium OMS.