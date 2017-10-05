---
title: "Łączenie produktów dotyczących zabezpieczeń z rozwiązaniem Zabezpieczenia i inspekcja w pakiecie Operations Management Suite (OMS) | Microsoft Docs"
description: "Ten dokument ułatwia łączenie produktów dotyczących zabezpieczeń z rozwiązaniem Zabezpieczenia i inspekcja w pakiecie Operations Management Suite przy użyciu formatu CEF (Common Event Format)."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="cfc28-103">Łączenie produktów dotyczących zabezpieczeń z rozwiązaniem Zabezpieczenia i inspekcja w pakiecie Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="cfc28-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="cfc28-104">Ten dokument ułatwia łączenie produktów dotyczących zabezpieczeń z rozwiązaniem Zabezpieczenia i inspekcja w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="cfc28-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="cfc28-105">Obsługiwane są następujące źródła:</span><span class="sxs-lookup"><span data-stu-id="cfc28-105">The following sources are supported:</span></span>

- <span data-ttu-id="cfc28-106">Zdarzenia w formacie Common Event Format (CEF)</span><span class="sxs-lookup"><span data-stu-id="cfc28-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="cfc28-107">Zdarzenia Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="cfc28-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="cfc28-108">Co to jest format CEF?</span><span class="sxs-lookup"><span data-stu-id="cfc28-108">What is CEF?</span></span>
<span data-ttu-id="cfc28-109">Common Event Format (CEF) to standardowy format branżowy komunikatów dzienników systemu używany przez wielu dostawców zabezpieczeń w celu umożliwienia współdziałania zdarzeń między różnymi platformami.</span><span class="sxs-lookup"><span data-stu-id="cfc28-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="cfc28-110">Rozwiązanie Zabezpieczenia i inspekcja w pakiecie OMS obsługuje pozyskiwanie danych w formacie CEF, który umożliwia łączenie produktów dotyczących zabezpieczeń z zabezpieczeniami pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="cfc28-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="cfc28-111">Połączenie źródła danych z pakietem OMS umożliwia korzystanie z następujących funkcji należących do tej platformy:</span><span class="sxs-lookup"><span data-stu-id="cfc28-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="cfc28-112">Wyszukiwanie i korelacja</span><span class="sxs-lookup"><span data-stu-id="cfc28-112">Search & Correlation</span></span>
- <span data-ttu-id="cfc28-113">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="cfc28-113">Auditing</span></span>
- <span data-ttu-id="cfc28-114">Alerty</span><span class="sxs-lookup"><span data-stu-id="cfc28-114">Alert</span></span>
- <span data-ttu-id="cfc28-115">Analiza zagrożeń</span><span class="sxs-lookup"><span data-stu-id="cfc28-115">Threat Intelligence</span></span>
- <span data-ttu-id="cfc28-116">Problemy godne uwagi</span><span class="sxs-lookup"><span data-stu-id="cfc28-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="cfc28-117">Zbieranie dzienników rozwiązań dotyczących zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="cfc28-117">Collection of security solution logs</span></span>

<span data-ttu-id="cfc28-118">Zabezpieczenia pakietu OMS obsługują zbieranie dzienników w formacie CEF przez dzienniki systemu i dzienniki rozwiązania [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="cfc28-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="cfc28-119">W tym przykładzie źródłem (komputerem generującym dzienniki) jest komputer z systemem Linux z uruchomionym demonem syslog-ng, a obiektem docelowym jest funkcja zabezpieczeń w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="cfc28-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="cfc28-120">Aby przygotować komputer z systemem Linux, wykonaj następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="cfc28-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="cfc28-121">Pobierz agenta pakietu OMS dla systemu Linux w wersji 1.2.0-25 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cfc28-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="cfc28-122">Postępuj zgodnie z instrukcjami przedstawionymi w sekcji **krótkiego przewodnika instalacji** w [tym artykule](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux), aby zainstalować agenta i dołączyć go do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="cfc28-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="cfc28-123">Zwykle agent jest zainstalowany na innym komputerze niż ten, na którym są generowane dzienniki.</span><span class="sxs-lookup"><span data-stu-id="cfc28-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="cfc28-124">Przekazanie dzienników do maszyny agenta zwykle wymaga wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cfc28-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="cfc28-125">Skonfiguruj produkt/maszynę rejestrowania w celu przekazywania wymaganych zdarzeń do demona dziennika systemu (rsyslog lub syslog-ng) na maszynie agenta.</span><span class="sxs-lookup"><span data-stu-id="cfc28-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="cfc28-126">Włącz demona dziennika systemu na maszynie agenta, aby odbierać komunikaty z systemu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="cfc28-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="cfc28-127">Na maszynie agenta zdarzenia muszą być wysyłane z demona dziennika systemu do lokalnego portu UDP 25226.</span><span class="sxs-lookup"><span data-stu-id="cfc28-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="cfc28-128">Agent nasłuchuje na tym porcie pod kątem zdarzeń przychodzących.</span><span class="sxs-lookup"><span data-stu-id="cfc28-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="cfc28-129">Poniżej przedstawiono przykładową konfigurację wysyłania wszystkich zdarzeń z systemu lokalnego do agenta (możesz zmodyfikować konfigurację tak, aby dopasować ją do ustawień lokalnych):</span><span class="sxs-lookup"><span data-stu-id="cfc28-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="cfc28-130">Otwórz okno terminalu i przejdź do katalogu */etc/syslog-ng/*</span><span class="sxs-lookup"><span data-stu-id="cfc28-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="cfc28-131">Utwórz nowy plik *security-config-omsagent.conf* i dodaj następującą zawartość: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="cfc28-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="cfc28-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="cfc28-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="cfc28-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="cfc28-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="cfc28-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="cfc28-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="cfc28-135">Pobierz plik *security_events.conf* i umieść go w katalogu */etc/opt/microsoft/omsagent/conf/omsagent.d/* na komputerze agenta pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="cfc28-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="cfc28-136">Wpisz poniższe polecenie, aby ponownie uruchomić demona syslog: *dla ng syslog, uruchom:*</span><span class="sxs-lookup"><span data-stu-id="cfc28-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="cfc28-137">*Uruchamianie demona rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="cfc28-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="cfc28-138">Wpisz poniższe polecenie, aby ponownie uruchomić agenta pakietu OMS:</span><span class="sxs-lookup"><span data-stu-id="cfc28-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="cfc28-139">*Uruchamianie demona syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="cfc28-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="cfc28-140">*Uruchamianie demona rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="cfc28-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="cfc28-141">Wpisz poniższe polecenie i przejrzyj wynik, aby upewnić się, że w dzienniku agenta pakietu OMS nie ma żadnych błędów:</span><span class="sxs-lookup"><span data-stu-id="cfc28-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="cfc28-142">Przeglądanie zebranych zdarzeń zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="cfc28-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="cfc28-143">Po zakończeniu konfiguracji funkcja zabezpieczeń w pakiecie OMS zacznie pozyskiwać zdarzenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="cfc28-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="cfc28-144">Aby zwizualizować te zdarzenia, otwórz wyszukiwanie w dzienniku, wpisz polecenie *Type=CommonSecurityLog* w polu wyszukiwania i naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="cfc28-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="cfc28-145">W poniższym przykładzie przedstawiono wynik tego polecenia. W tym przypadku funkcja zabezpieczeń pakietu OMS już pozyskała dzienniki zabezpieczeń od wielu dostawców:</span><span class="sxs-lookup"><span data-stu-id="cfc28-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="cfc28-147">Możesz zawęzić kryteria wyszukiwania do jednego dostawcy. Aby na przykład zwizualizować dzienniki Cisco online, wpisz: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="cfc28-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="cfc28-148">Element „CommonSecurityLog” ma wstępnie zdefiniowane pola dla każdego nagłówka CEF, łącznie z podstawowymi rozszerzeniami, natomiast pozostałe rozszerzenia (niezależnie od tego, czy są to rozszerzenia niestandardowe) zostaną wstawione w polu „AdditionalExtensions”.</span><span class="sxs-lookup"><span data-stu-id="cfc28-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="cfc28-149">Funkcja pól niestandardowych umożliwia uzyskanie dedykowanych pól.</span><span class="sxs-lookup"><span data-stu-id="cfc28-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="cfc28-150">Dostęp do komputerów, dla których brak oceny linii bazowej</span><span class="sxs-lookup"><span data-stu-id="cfc28-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="cfc28-151">Pakiet OMS obsługuje profil linii bazowej członka domeny w systemie Windows Server od wersji 2008 R2 do wersji 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="cfc28-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="cfc28-152">Ostateczna wersja linii bazowej dla systemu Windows Server 2016 nie jest jeszcze opracowana i zostanie dodana natychmiast po jej opublikowaniu.</span><span class="sxs-lookup"><span data-stu-id="cfc28-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="cfc28-153">Wszystkie inne systemy operacyjne skanowane za pomocą oceny linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS są widoczne w sekcji **Komputery, dla których brak oceny linii bazowej**.</span><span class="sxs-lookup"><span data-stu-id="cfc28-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="cfc28-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cfc28-154">See also</span></span>
<span data-ttu-id="cfc28-155">W tym dokumencie pokazano, jak połączyć rozwiązanie CEF z pakietem OMS.</span><span class="sxs-lookup"><span data-stu-id="cfc28-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="cfc28-156">Więcej informacji na temat zabezpieczeń w pakiecie OMS zawierają następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cfc28-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="cfc28-157">Omówienie pakietu Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="cfc28-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="cfc28-158">Monitorowanie alertów zabezpieczeń i reagowanie na nie w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="cfc28-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="cfc28-159">Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="cfc28-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

