---
title: Zbieranie i analizowanie komunikaty dziennika systemowego w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "SYSLOG to protokół rejestrowania zdarzeń jest wspólny dla systemu Linux. W tym artykule opisano sposób konfigurowania kolekcji komunikaty dziennika systemowego w analizy dzienników i szczegóły rekordów tworzonych w repozytorium OMS."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="08689-104">SYSLOG źródeł danych w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="08689-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="08689-105">SYSLOG to protokół rejestrowania zdarzeń jest wspólny dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="08689-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="08689-106">Aplikacje będą wysyłać wiadomości, które mogą być przechowywane na komputerze lokalnym lub dostarczone do modułu zbierającego Syslog.</span><span class="sxs-lookup"><span data-stu-id="08689-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="08689-107">Po zainstalowaniu Agent pakietu OMS dla systemu Linux, konfiguruje lokalnego demon Syslog do przekazywania wiadomości do agenta.</span><span class="sxs-lookup"><span data-stu-id="08689-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="08689-108">Agent wysyła następnie komunikat do analizy dzienników, w którym odpowiedni rekord jest tworzony w repozytorium OMS.</span><span class="sxs-lookup"><span data-stu-id="08689-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="08689-109">Analiza dzienników obsługuje kolekcji komunikatów wysłanych przez rsyslog lub syslog ng, gdzie rsyslog jest demona domyślne.</span><span class="sxs-lookup"><span data-stu-id="08689-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="08689-110">Demon syslog domyślne w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="08689-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="08689-111">Do zbierania danych z serwera syslog z tej wersji tych dystrybucji [demon rsyslog](http://rsyslog.com) powinna być zainstalowana i skonfigurowana zastąpić sysklog.</span><span class="sxs-lookup"><span data-stu-id="08689-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Kolekcja SYSLOG](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="08689-113">Konfigurowanie usługi Syslog</span><span class="sxs-lookup"><span data-stu-id="08689-113">Configuring Syslog</span></span>
<span data-ttu-id="08689-114">Agent pakietu OMS dla systemu Linux są zbierane zdarzenia z urządzeń i ważności, które są określone w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="08689-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="08689-115">Syslog można skonfigurować za pośrednictwem portalu OMS lub przez zarządzanie plikami konfiguracji na agentów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="08689-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="08689-116">Skonfigurować dziennik systemowy w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="08689-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="08689-117">Skonfigurować dziennik systemowy z [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="08689-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="08689-118">Ta konfiguracja jest dostarczany do pliku konfiguracji na każdym agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="08689-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="08689-119">Można dodać nowego zakładu, wpisując jej nazwę, a następnie klikając polecenie  **+** .</span><span class="sxs-lookup"><span data-stu-id="08689-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="08689-120">Dla każdego obiektu zostaną zebrane tylko komunikatów dla wybranej ważności.</span><span class="sxs-lookup"><span data-stu-id="08689-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="08689-121">Sprawdzanie ważności dla konkretnego obiektu, który chcesz zebrać.</span><span class="sxs-lookup"><span data-stu-id="08689-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="08689-122">Nie można podać wszelkie dodatkowe kryteria filtrowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="08689-122">You cannot provide any additional criteria to filter messages.</span></span>

![Konfigurowanie usługi Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="08689-124">Domyślnie wszystkie zmiany konfiguracji są automatycznie przypisany do wszystkich agentów.</span><span class="sxs-lookup"><span data-stu-id="08689-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="08689-125">Jeśli chcesz ręcznie skonfigurować Syslog dla każdego agenta systemu Linux, usuń zaznaczenie pola *Zastosuj poniższą konfigurację na moich maszynach z systemem Linux*.</span><span class="sxs-lookup"><span data-stu-id="08689-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="08689-126">Skonfiguruj Syslog na agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="08689-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="08689-127">Gdy [OMS agent jest zainstalowany na komputerze klienckim Linux](log-analytics-linux-agents.md), instaluje domyślny plik konfiguracji programu syslog definiujący funkcje i ważność komunikatów, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="08689-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="08689-128">Można modyfikować tego pliku, aby zmienić konfigurację.</span><span class="sxs-lookup"><span data-stu-id="08689-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="08689-129">Plik konfiguracji jest różne w zależności od demon Syslog, które klient został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="08689-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="08689-130">Po zmodyfikowaniu konfiguracji programu syslog, należy ponownie uruchomić demona syslog, aby zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="08689-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="08689-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="08689-131">rsyslog</span></span>
<span data-ttu-id="08689-132">Plik konfiguracji rsyslog znajduje się w **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="08689-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="08689-133">Poniżej przedstawiono domyślną zawartość.</span><span class="sxs-lookup"><span data-stu-id="08689-133">Its default contents are shown below.</span></span>  <span data-ttu-id="08689-134">Umożliwia zbieranie informacji wysyłanych z lokalnego agenta dla wszystkich obiektów o poziomie ostrzeżenia lub komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="08689-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="08689-135">Należy usunąć obiekt przez usunięcie jego sekcji pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="08689-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="08689-136">Można ograniczyć wag, które są zbierane dla konkretnego obiektu przez zmodyfikowanie wpisu tego obiektu.</span><span class="sxs-lookup"><span data-stu-id="08689-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="08689-137">Na przykład aby ograniczyć funkcji użytkownika do wiadomości o ważności błąd lub należy zmodyfikować tego wiersza do następującego pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="08689-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="08689-138">SYSLOG ng</span><span class="sxs-lookup"><span data-stu-id="08689-138">syslog-ng</span></span>
<span data-ttu-id="08689-139">Plik konfiguracji do syslog ng jest lokalizacji **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="08689-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="08689-140">Poniżej przedstawiono domyślną zawartość.</span><span class="sxs-lookup"><span data-stu-id="08689-140">Its default contents are shown below.</span></span>  <span data-ttu-id="08689-141">Umożliwia zbieranie informacji wysyłanych z lokalnego agenta dla wszystkich urządzeń i wszystkich wag komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="08689-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="08689-142">Należy usunąć obiekt przez usunięcie jego sekcji pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="08689-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="08689-143">Można ograniczyć wag, które są zbierane dla konkretnego obiektu, usuwając je z listy.</span><span class="sxs-lookup"><span data-stu-id="08689-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="08689-144">Na przykład aby ograniczyć możliwość użytkownik po prostu alertów i krytycznych wiadomości, można zmodyfikować tej sekcji pliku konfiguracji do następującego:</span><span class="sxs-lookup"><span data-stu-id="08689-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="08689-145">Zbieranie danych z dodatkowych portów usługi Syslog</span><span class="sxs-lookup"><span data-stu-id="08689-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="08689-146">Agent pakietu OMS odbiera komunikaty dziennika systemowego na lokalnym kliencie na porcie 25224.</span><span class="sxs-lookup"><span data-stu-id="08689-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="08689-147">Po zainstalowaniu agenta domyślnej konfiguracji programu syslog jest stosowane i znaleźć w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="08689-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="08689-148">Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="08689-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="08689-149">SYSLOG ng:`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="08689-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="08689-150">Można zmienić numer portu przez utworzenie dwóch plików konfiguracyjnych: FluentD pliku konfiguracji i pliku ng rsyslog lub syslog, w zależności od demon Syslog został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="08689-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="08689-151">Plik konfiguracji FluentD powinien być nowy plik znajduje się w: `/etc/opt/microsoft/omsagent/conf/omsagent.d` i Zastąp wartości w **portu** wpis o numer portu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="08689-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="08689-152">Rsyslog, należy utworzyć plik konfiguracji znajduje się w: `/etc/rsyslog.d/` i Zastąp wartości % SYSLOG_PORT % numer portu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="08689-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="08689-153">Jeśli zmodyfikujesz tę wartość w pliku konfiguracyjnym `95-omsagent.conf`, zostaną zastąpione, gdy agent stosuje konfigurację domyślną.</span><span class="sxs-lookup"><span data-stu-id="08689-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="08689-154">Konfiguracji usługi syslog ng powinno zostać zmodyfikowane przez skopiowanie konfiguracji przykładzie pokazano poniżej i dodawanie zmodyfikowane ustawienia niestandardowe na końcu pliku konfiguracji programu syslog ng.conf znajduje się w `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="08689-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="08689-155">Czy **nie** Użyj etykiety domyślnej **% WORKSPACE_ID % _oms** lub **% WORKSPACE_ID_OMS**, zdefiniuj ułatwia odróżnienie zmiany etykiety niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="08689-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="08689-156">Zmodyfikowanie wartości domyślnych w pliku konfiguracji, zostaną one zastąpione, gdy agent stosuje konfigurację domyślną.</span><span class="sxs-lookup"><span data-stu-id="08689-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="08689-157">Po zakończeniu zmiany, Syslog i agent pakietu OMS usługi musi zostać uruchomiony ponownie, aby upewnić się, że zmiany konfiguracji zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="08689-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="08689-158">Właściwości rekordu dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="08689-158">Syslog record properties</span></span>
<span data-ttu-id="08689-159">Rekordy dziennika systemowego zawiera typu **Syslog** i mieć właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="08689-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="08689-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="08689-160">Property</span></span> | <span data-ttu-id="08689-161">Opis</span><span class="sxs-lookup"><span data-stu-id="08689-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08689-162">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="08689-162">Computer</span></span> |<span data-ttu-id="08689-163">Komputer, który zostały zebrane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="08689-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="08689-164">Funkcje</span><span class="sxs-lookup"><span data-stu-id="08689-164">Facility</span></span> |<span data-ttu-id="08689-165">Definiuje część systemu, który wygenerował komunikat.</span><span class="sxs-lookup"><span data-stu-id="08689-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="08689-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="08689-166">HostIP</span></span> |<span data-ttu-id="08689-167">Adres IP systemu wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="08689-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="08689-168">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="08689-168">HostName</span></span> |<span data-ttu-id="08689-169">Nazwa systemu wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="08689-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="08689-170">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="08689-170">SeverityLevel</span></span> |<span data-ttu-id="08689-171">Poziom ważności zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="08689-171">Severity level of the event.</span></span> |
| <span data-ttu-id="08689-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="08689-172">SyslogMessage</span></span> |<span data-ttu-id="08689-173">Tekst komunikatu.</span><span class="sxs-lookup"><span data-stu-id="08689-173">Text of the message.</span></span> |
| <span data-ttu-id="08689-174">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="08689-174">ProcessID</span></span> |<span data-ttu-id="08689-175">Identyfikator procesu, który wygenerował komunikat.</span><span class="sxs-lookup"><span data-stu-id="08689-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="08689-176">eventTime</span><span class="sxs-lookup"><span data-stu-id="08689-176">EventTime</span></span> |<span data-ttu-id="08689-177">Data i godzina wygenerowania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="08689-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="08689-178">Dziennik zapytań dotyczących rekordów dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="08689-178">Log queries with Syslog records</span></span>
<span data-ttu-id="08689-179">Poniższa tabela zawiera przykłady różnych dziennika zapytań, które pobierają rekordy dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="08689-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="08689-180">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="08689-180">Query</span></span> | <span data-ttu-id="08689-181">Opis</span><span class="sxs-lookup"><span data-stu-id="08689-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08689-182">Typ = Syslog</span><span class="sxs-lookup"><span data-stu-id="08689-182">Type=Syslog</span></span> |<span data-ttu-id="08689-183">Wszystkie audyt dzienników systemowych.</span><span class="sxs-lookup"><span data-stu-id="08689-183">All Syslogs.</span></span> |
| <span data-ttu-id="08689-184">Typ = poziom ważności Syslog = błąd</span><span class="sxs-lookup"><span data-stu-id="08689-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="08689-185">Wszystkie rekordy dziennika systemowego o ważności błędu.</span><span class="sxs-lookup"><span data-stu-id="08689-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="08689-186">Typ = Syslog &#124; count() miary w przeliczeniu na komputer</span><span class="sxs-lookup"><span data-stu-id="08689-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="08689-187">Liczba Syslog rejestruje przez komputer.</span><span class="sxs-lookup"><span data-stu-id="08689-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="08689-188">Typ = Syslog &#124; Miara count() przez funkcje</span><span class="sxs-lookup"><span data-stu-id="08689-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="08689-189">Liczba Syslog rejestruje przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="08689-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="08689-190">Jeśli Twój obszar roboczy został uaktualniony do [nowego języka zapytań usługi Log Analytics](log-analytics-log-search-upgrade.md), powyższe zapytania zmienią się w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="08689-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="08689-191">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="08689-191">Query</span></span> | <span data-ttu-id="08689-192">Opis</span><span class="sxs-lookup"><span data-stu-id="08689-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08689-193">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="08689-193">Syslog</span></span> |<span data-ttu-id="08689-194">Wszystkie audyt dzienników systemowych.</span><span class="sxs-lookup"><span data-stu-id="08689-194">All Syslogs.</span></span> |
| <span data-ttu-id="08689-195">SYSLOG &#124; gdy poziom ważności == "error"</span><span class="sxs-lookup"><span data-stu-id="08689-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="08689-196">Wszystkie rekordy dziennika systemowego o ważności błędu.</span><span class="sxs-lookup"><span data-stu-id="08689-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="08689-197">SYSLOG &#124; Podsumuj AggregatedValue = count() przez komputer</span><span class="sxs-lookup"><span data-stu-id="08689-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="08689-198">Liczba Syslog rejestruje przez komputer.</span><span class="sxs-lookup"><span data-stu-id="08689-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="08689-199">SYSLOG &#124; Podsumuj AggregatedValue = count() przez funkcje</span><span class="sxs-lookup"><span data-stu-id="08689-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="08689-200">Liczba Syslog rejestruje przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="08689-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08689-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08689-201">Next steps</span></span>
* <span data-ttu-id="08689-202">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="08689-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="08689-203">Użyj [pola niestandardowe](log-analytics-custom-fields.md) do analizowania danych z rekordów dziennika systemowego do poszczególnych pól.</span><span class="sxs-lookup"><span data-stu-id="08689-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="08689-204">[Konfigurowanie agentów systemu Linux](log-analytics-linux-agents.md) służąca do gromadzenia innych typów danych.</span><span class="sxs-lookup"><span data-stu-id="08689-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
