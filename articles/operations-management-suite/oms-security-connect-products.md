---
title: "aaaConnecting Twojego zabezpieczeń produktów toohello zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia możesz tooconnect tooOperations produkty zabezpieczeń zabezpieczeń pakietu administracyjnego i rozwiązanie inspekcji za pomocą typowego formatu zdarzeń."
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
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="6cafa-103">Łączenie z zabezpieczeń produktów toohello zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji</span><span class="sxs-lookup"><span data-stu-id="6cafa-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="6cafa-104">Ten dokument ułatwia połączenie z produktów zabezpieczeń hello OMS zabezpieczeń i rozwiązanie inspekcji.</span><span class="sxs-lookup"><span data-stu-id="6cafa-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="6cafa-105">obsługiwane są następujące źródła Hello:</span><span class="sxs-lookup"><span data-stu-id="6cafa-105">hello following sources are supported:</span></span>

- <span data-ttu-id="6cafa-106">Zdarzenia w formacie Common Event Format (CEF)</span><span class="sxs-lookup"><span data-stu-id="6cafa-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="6cafa-107">Zdarzenia Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="6cafa-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="6cafa-108">Co to jest format CEF?</span><span class="sxs-lookup"><span data-stu-id="6cafa-108">What is CEF?</span></span>
<span data-ttu-id="6cafa-109">Typowe formatu zdarzeń (CEF) jest branży formatem u góry komunikaty dziennika systemowego, używane przez wielu dostawców tooallow zdarzeń zgodności zabezpieczeń między różnymi platformami.</span><span class="sxs-lookup"><span data-stu-id="6cafa-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="6cafa-110">Zabezpieczenia OMS i inspekcji rozwiązanie obsługuje wprowadzanie danych przy użyciu CEF, co pozwala tooconnect produkty zabezpieczeń z zabezpieczeniami OMS.</span><span class="sxs-lookup"><span data-stu-id="6cafa-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="6cafa-111">Nawiązując połączenie z tooOMS źródła danych, jest możliwe tootake zaletą hello następujące funkcje, które są częścią tej platformy:</span><span class="sxs-lookup"><span data-stu-id="6cafa-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="6cafa-112">Wyszukiwanie i korelacja</span><span class="sxs-lookup"><span data-stu-id="6cafa-112">Search & Correlation</span></span>
- <span data-ttu-id="6cafa-113">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="6cafa-113">Auditing</span></span>
- <span data-ttu-id="6cafa-114">Alerty</span><span class="sxs-lookup"><span data-stu-id="6cafa-114">Alert</span></span>
- <span data-ttu-id="6cafa-115">Analiza zagrożeń</span><span class="sxs-lookup"><span data-stu-id="6cafa-115">Threat Intelligence</span></span>
- <span data-ttu-id="6cafa-116">Problemy godne uwagi</span><span class="sxs-lookup"><span data-stu-id="6cafa-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="6cafa-117">Zbieranie dzienników rozwiązań dotyczących zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="6cafa-117">Collection of security solution logs</span></span>

<span data-ttu-id="6cafa-118">Zabezpieczenia pakietu OMS obsługują zbieranie dzienników w formacie CEF przez dzienniki systemu i dzienniki rozwiązania [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="6cafa-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="6cafa-119">W tym przykładzie hello źródło (komputer, który generuje dzienniki hello) jest uruchomiony demon syslog ng komputera z systemem Linux i docelowy hello jest OMS zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6cafa-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="6cafa-120">komputer z systemem Linux hello tooprepare należy hello tooperform następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6cafa-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="6cafa-121">Pobierz hello Agent pakietu OMS dla systemu Linux, 1.2.0-25 wersji lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6cafa-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="6cafa-122">Postępuj zgodnie z sekcji hello **krótki przewodnik instalowania** z [w tym artykule](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall i dołączyć hello agenta tooyour roboczym.</span><span class="sxs-lookup"><span data-stu-id="6cafa-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="6cafa-123">Zazwyczaj hello agent jest zainstalowany na innym komputerze z hello są generowane, na których dzienniki hello.</span><span class="sxs-lookup"><span data-stu-id="6cafa-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="6cafa-124">Komputer agenta przekazywania hello dzienniki toohello zwykle wymaga hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6cafa-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="6cafa-125">Na maszynie agenta hello, skonfiguruj hello rejestrowania produktu/machine tooforward hello wymagane zdarzenia toohello demon syslog (rsyslog lub syslog ng).</span><span class="sxs-lookup"><span data-stu-id="6cafa-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="6cafa-126">Włącz hello demon syslog na wiadomości powitania od agenta maszyny tooreceive z systemu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6cafa-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="6cafa-127">Na maszynie agenta hello hello zdarzeń muszą toobe wysyłane z portem UDP toolocal demon syslog hello 25226.</span><span class="sxs-lookup"><span data-stu-id="6cafa-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="6cafa-128">Hello agent nasłuchuje przychodzących zdarzeń na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="6cafa-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="6cafa-129">Hello poniżej przedstawiono przykładową konfigurację do wysyłania wszystkie zdarzenia z agenta toohello systemu lokalnego hello (można modyfikować toofit konfiguracji hello ustawienia lokalne):</span><span class="sxs-lookup"><span data-stu-id="6cafa-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="6cafa-130">Witaj Otwórz okno terminala i przejdź toohello katalogu */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="6cafa-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="6cafa-131">Utwórz nowy plik *zabezpieczeń config-omsagent.conf* i Dodaj hello następującej zawartości: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="6cafa-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="6cafa-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="6cafa-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="6cafa-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="6cafa-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="6cafa-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="6cafa-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="6cafa-135">Pobierz plik hello *security_events.conf* i umieścić w */etc/opt/microsoft/omsagent/conf/omsagent.d/* w komputerze agenta pakietu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6cafa-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="6cafa-136">Wpisz poniższe polecenie hello demon syslog hello toorestart: *dla ng syslog, uruchom:*</span><span class="sxs-lookup"><span data-stu-id="6cafa-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="6cafa-137">*Uruchamianie demona rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="6cafa-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="6cafa-138">Wpisz poniższe polecenie hello hello toorestart Agent pakietu OMS:</span><span class="sxs-lookup"><span data-stu-id="6cafa-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="6cafa-139">*Uruchamianie demona syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="6cafa-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="6cafa-140">*Uruchamianie demona rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="6cafa-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="6cafa-141">Wpisz poniższe polecenie hello i przejrzyj hello wynik tooconfirm, że nie ma żadnych błędów w dzienniku agenta pakietu OMS hello:</span><span class="sxs-lookup"><span data-stu-id="6cafa-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="6cafa-142">Przeglądanie zebranych zdarzeń zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="6cafa-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="6cafa-143">Po hello konfiguracji przez program hello zdarzeń zabezpieczeń zostanie uruchomiony toobe pozyskanych przez zabezpieczenia OMS.</span><span class="sxs-lookup"><span data-stu-id="6cafa-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="6cafa-144">toovisualize tych zdarzeń, otwórz hello dziennik wyszukiwania, wpisz polecenie hello *typu = CommonSecurityLog* w hello pola wyszukiwania i naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="6cafa-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="6cafa-145">Witaj poniższy przykład przedstawia wynik hello tego polecenia Zwróć uwagę, że w takim przypadku zabezpieczeń OMS już pozyskanych dzienniki zabezpieczeń z wielu dostawców:</span><span class="sxs-lookup"><span data-stu-id="6cafa-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="6cafa-147">Można uściślić wyszukiwanie dla jednego dostawcy, na przykład toovisualize dzienniki online Cisco, typ: *typu = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="6cafa-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="6cafa-148">dla dowolnego nagłówka CEF także podstawowe extensios hello podczas inne rozszerzenia "Niestandardowe rozszerzenie" lub nie zostanie wstawiony do pola "AdditionalExtensions" Hello "CommonSecurityLog" ma wstępnie zdefiniowane pola.</span><span class="sxs-lookup"><span data-stu-id="6cafa-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="6cafa-149">Można użyć hello pola niestandardowe funkcji tooget dedykowanego pola z niego.</span><span class="sxs-lookup"><span data-stu-id="6cafa-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="6cafa-150">Dostęp do komputerów, dla których brak oceny linii bazowej</span><span class="sxs-lookup"><span data-stu-id="6cafa-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="6cafa-151">OMS obsługuje opinii linii bazowej hello domeny systemu Windows Server 2008 R2 tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6cafa-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="6cafa-152">Ostateczna wersja linii bazowej dla systemu Windows Server 2016 nie jest jeszcze opracowana i zostanie dodana natychmiast po jej opublikowaniu.</span><span class="sxs-lookup"><span data-stu-id="6cafa-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="6cafa-153">Wszystkie inne systemy operacyjne skanowania za pomocą oceny linii bazowej OMS zabezpieczeń i inspekcji są wyświetlane w obszarze hello **komputery z brakującą oceny linii bazowej** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6cafa-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="6cafa-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6cafa-154">See also</span></span>
<span data-ttu-id="6cafa-155">W tym dokumencie możesz przedstawiono sposób tooconnect Twojego tooOMS rozwiązania CEF.</span><span class="sxs-lookup"><span data-stu-id="6cafa-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="6cafa-156">toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="6cafa-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="6cafa-157">Omówienie pakietu Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6cafa-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="6cafa-158">Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji</span><span class="sxs-lookup"><span data-stu-id="6cafa-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="6cafa-159">Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6cafa-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

