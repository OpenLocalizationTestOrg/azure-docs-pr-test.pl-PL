---
title: "aaaCollect i analizować komunikaty dziennika systemowego w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "SYSLOG jest protokół rejestrowania zdarzeń, który jest tooLinux wspólnej. W tym artykule opisano, jak tooconfigure kolekcję komunikatów Syslog w analizy dzienników i szczegóły rekordów hello tworzą w repozytorium OMS hello."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="3a861-104">SYSLOG źródeł danych w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="3a861-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="3a861-105">SYSLOG jest protokół rejestrowania zdarzeń, który jest tooLinux wspólnej.</span><span class="sxs-lookup"><span data-stu-id="3a861-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="3a861-106">Aplikacje będą wysyłać wiadomości, które mogą być przechowywane na komputerze lokalnym hello lub dostarczony moduł zbierający Syslog tooa.</span><span class="sxs-lookup"><span data-stu-id="3a861-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="3a861-107">Po zainstalowaniu hello Agent pakietu OMS dla systemu Linux, konfiguruje hello Syslog demon tooforward wiadomości toohello agent lokalny.</span><span class="sxs-lookup"><span data-stu-id="3a861-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="3a861-108">Witaj agent wysyła następnie tooLog wiadomość hello Analytics której zostaje utworzony rekord odpowiedniego hello OMS repozytorium.</span><span class="sxs-lookup"><span data-stu-id="3a861-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="3a861-109">Analiza dzienników obsługuje kolekcji komunikatów wysłanych przez rsyslog lub syslog ng, gdzie rsyslog jest hello demon domyślne.</span><span class="sxs-lookup"><span data-stu-id="3a861-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="3a861-110">demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="3a861-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="3a861-111">Witaj toocollect syslog danych z tej wersji tych dystrybucji [demon rsyslog](http://rsyslog.com) powinien być zainstalowany i skonfigurowany tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="3a861-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Kolekcja SYSLOG](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="3a861-113">Konfigurowanie usługi Syslog</span><span class="sxs-lookup"><span data-stu-id="3a861-113">Configuring Syslog</span></span>
<span data-ttu-id="3a861-114">Hello Agent pakietu OMS dla systemu Linux są zbierane zdarzenia za pomocą urządzeń hello i ważności, które są określone w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3a861-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="3a861-115">Syslog można skonfigurować za pośrednictwem portalu OMS hello lub przez zarządzanie plikami konfiguracji na agentów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3a861-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="3a861-116">Konfigurowanie w portalu OMS hello Syslog</span><span class="sxs-lookup"><span data-stu-id="3a861-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="3a861-117">Konfigurowanie Syslog z hello [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="3a861-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="3a861-118">Ta konfiguracja jest dostarczana toohello pliku konfiguracji na każdym agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3a861-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="3a861-119">Można dodać nowego zakładu, wpisując jej nazwę, a następnie klikając polecenie  **+** .</span><span class="sxs-lookup"><span data-stu-id="3a861-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="3a861-120">Dla każdego obiektu zostaną zebrane tylko wiadomości powitania wybrane ważności.</span><span class="sxs-lookup"><span data-stu-id="3a861-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="3a861-121">Sprawdź hello wag dla obiektu określonego hello, które mają toocollect.</span><span class="sxs-lookup"><span data-stu-id="3a861-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="3a861-122">Nie można podać wszelkie dodatkowe kryteria toofilter wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3a861-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Konfigurowanie usługi Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="3a861-124">Domyślnie wszystkie zmiany konfiguracji są automatycznie wypychana agentów tooall.</span><span class="sxs-lookup"><span data-stu-id="3a861-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="3a861-125">Jeśli chcesz tooconfigure Syslog ręcznie na każdym agenta systemu Linux, usuń zaznaczenie pola hello *Zastosuj poniżej maszyny z systemem Linux toomy konfiguracji*.</span><span class="sxs-lookup"><span data-stu-id="3a861-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="3a861-126">Skonfiguruj Syslog na agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3a861-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="3a861-127">Gdy hello [OMS agent jest zainstalowany na komputerze klienckim Linux](log-analytics-linux-agents.md), instaluje domyślny plik konfiguracji programu syslog definiujący funkcje hello i ważność hello wiadomości, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="3a861-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="3a861-128">Można zmodyfikować tę konfigurację hello toochange pliku.</span><span class="sxs-lookup"><span data-stu-id="3a861-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="3a861-129">plik konfiguracji Hello jest różne w zależności od hello Syslog demon, który hello klienta został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="3a861-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="3a861-130">Edytuj hello syslog konfiguracji, należy ponownie uruchomić demon syslog hello hello zmiany tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="3a861-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="3a861-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="3a861-131">rsyslog</span></span>
<span data-ttu-id="3a861-132">Witaj pliku konfiguracyjnego rsyslog znajduje się w **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="3a861-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="3a861-133">Poniżej przedstawiono domyślną zawartość.</span><span class="sxs-lookup"><span data-stu-id="3a861-133">Its default contents are shown below.</span></span>  <span data-ttu-id="3a861-134">Umożliwia zbieranie informacji wysyłanych z agenta lokalne powitania dla wszystkich obiektów o poziomie ostrzeżenia lub komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="3a861-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="3a861-135">Należy usunąć obiekt przez usunięcie jego sekcji hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3a861-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="3a861-136">Można ograniczyć hello wag, które są zbierane dla konkretnego obiektu przez zmodyfikowanie wpisu tego obiektu.</span><span class="sxs-lookup"><span data-stu-id="3a861-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="3a861-137">Na przykład toolimit hello użytkownika zakładzie toomessages z ważność błędu lub wyższy jaki modyfikuje się tego wiersza toohello pliku konfiguracji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3a861-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="3a861-138">SYSLOG ng</span><span class="sxs-lookup"><span data-stu-id="3a861-138">syslog-ng</span></span>
<span data-ttu-id="3a861-139">plik konfiguracji Hello syslog ng jest lokalizacji **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="3a861-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="3a861-140">Poniżej przedstawiono domyślną zawartość.</span><span class="sxs-lookup"><span data-stu-id="3a861-140">Its default contents are shown below.</span></span>  <span data-ttu-id="3a861-141">Umożliwia zbieranie informacji wysyłanych z agenta lokalne powitania dla wszystkich urządzeń i wszystkich wag komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="3a861-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="3a861-142">Należy usunąć obiekt przez usunięcie jego sekcji hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3a861-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="3a861-143">Można ograniczyć hello wag, które są zbierane dla konkretnego obiektu, usuwając je z listy.</span><span class="sxs-lookup"><span data-stu-id="3a861-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="3a861-144">Na przykład toolimit hello użytkownika zakładzie toojust komunikaty alertów i krytycznego, jaki modyfikuje tej sekcji toohello pliku konfiguracji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3a861-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="3a861-145">Zbieranie danych z dodatkowych portów usługi Syslog</span><span class="sxs-lookup"><span data-stu-id="3a861-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="3a861-146">agent pakietu OMS Hello odbiera komunikaty dziennika systemowego na powitania klienta lokalnego na porcie 25224.</span><span class="sxs-lookup"><span data-stu-id="3a861-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="3a861-147">Po zainstalowaniu agenta hello domyślnej konfiguracji programu syslog jest stosowane i znaleźć w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="3a861-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="3a861-148">Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="3a861-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="3a861-149">SYSLOG ng:`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="3a861-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="3a861-150">Można zmienić numer portu hello przez utworzenie dwóch plików konfiguracyjnych: FluentD pliku konfiguracji i pliku ng rsyslog lub syslog, w zależności od demon Syslog hello został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="3a861-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="3a861-151">plik konfiguracji FluentD Hello powinien być nowy plik znajduje się w: `/etc/opt/microsoft/omsagent/conf/omsagent.d` i zastąp wartość hello w hello **portu** wpis o numer portu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="3a861-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="3a861-152">Rsyslog, należy utworzyć plik konfiguracji znajduje się w: `/etc/rsyslog.d/` i Zastąp hello wartość % SYSLOG_PORT numer portu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="3a861-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="3a861-153">Jeśli zmodyfikujesz tę wartość w pliku konfiguracyjnym hello `95-omsagent.conf`, zostaną zastąpione, gdy hello agent dotyczy konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="3a861-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="3a861-154">Hello config syslog ng powinno zostać zmodyfikowane przez skopiowanie hello Przykładowa konfiguracja pokazano poniżej i dodawanie toohello zmodyfikowane ustawienia niestandardowe hello koniec pliku konfiguracji syslog ng.conf hello znajduje się w `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="3a861-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="3a861-155">Czy **nie** Użyj etykiety domyślnej hello **% WORKSPACE_ID % _oms** lub **% WORKSPACE_ID_OMS**, zdefiniować niestandardowe etykiety toohelp odróżnić zmiany.</span><span class="sxs-lookup"><span data-stu-id="3a861-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="3a861-156">Jeśli zmodyfikujesz hello domyślne wartości w pliku konfiguracyjnym hello, zostaną one zastąpione gdy hello agent dotyczy konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="3a861-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="3a861-157">Po zakończeniu zmiany hello, hello Syslog i hello usługę agenta musi ponownie uruchomić toobe tooensure hello konfiguracji zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="3a861-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="3a861-158">Właściwości rekordu dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="3a861-158">Syslog record properties</span></span>
<span data-ttu-id="3a861-159">Rekordy dziennika systemowego zawiera typu **Syslog** i mają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a861-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="3a861-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3a861-160">Property</span></span> | <span data-ttu-id="3a861-161">Opis</span><span class="sxs-lookup"><span data-stu-id="3a861-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a861-162">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="3a861-162">Computer</span></span> |<span data-ttu-id="3a861-163">Komputer, który hello zdarzeń zostały zebrane.</span><span class="sxs-lookup"><span data-stu-id="3a861-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="3a861-164">Funkcje</span><span class="sxs-lookup"><span data-stu-id="3a861-164">Facility</span></span> |<span data-ttu-id="3a861-165">Definiuje hello częścią systemu hello, który wygenerował wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="3a861-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="3a861-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="3a861-166">HostIP</span></span> |<span data-ttu-id="3a861-167">Adres IP systemu hello wysyłania wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="3a861-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="3a861-168">Nazwa hosta</span><span class="sxs-lookup"><span data-stu-id="3a861-168">HostName</span></span> |<span data-ttu-id="3a861-169">Nazwa systemu hello wysyłania wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="3a861-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="3a861-170">Poziom ważności</span><span class="sxs-lookup"><span data-stu-id="3a861-170">SeverityLevel</span></span> |<span data-ttu-id="3a861-171">Poziom ważności hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="3a861-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="3a861-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="3a861-172">SyslogMessage</span></span> |<span data-ttu-id="3a861-173">Tekst wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="3a861-173">Text of hello message.</span></span> |
| <span data-ttu-id="3a861-174">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="3a861-174">ProcessID</span></span> |<span data-ttu-id="3a861-175">Identyfikator procesu hello, który wygenerował wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="3a861-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="3a861-176">eventTime</span><span class="sxs-lookup"><span data-stu-id="3a861-176">EventTime</span></span> |<span data-ttu-id="3a861-177">Data i godzina hello zdarzeń został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="3a861-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="3a861-178">Dziennik zapytań dotyczących rekordów dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="3a861-178">Log queries with Syslog records</span></span>
<span data-ttu-id="3a861-179">Witaj poniższej tabeli przedstawiono różne przykłady dziennika zapytań, które pobierają rekordy dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="3a861-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="3a861-180">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="3a861-180">Query</span></span> | <span data-ttu-id="3a861-181">Opis</span><span class="sxs-lookup"><span data-stu-id="3a861-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a861-182">Typ = Syslog</span><span class="sxs-lookup"><span data-stu-id="3a861-182">Type=Syslog</span></span> |<span data-ttu-id="3a861-183">Wszystkie audyt dzienników systemowych.</span><span class="sxs-lookup"><span data-stu-id="3a861-183">All Syslogs.</span></span> |
| <span data-ttu-id="3a861-184">Typ = poziom ważności Syslog = błąd</span><span class="sxs-lookup"><span data-stu-id="3a861-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="3a861-185">Wszystkie rekordy dziennika systemowego o ważności błędu.</span><span class="sxs-lookup"><span data-stu-id="3a861-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="3a861-186">Typ = Syslog &#124; count() miary w przeliczeniu na komputer</span><span class="sxs-lookup"><span data-stu-id="3a861-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="3a861-187">Liczba Syslog rejestruje przez komputer.</span><span class="sxs-lookup"><span data-stu-id="3a861-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="3a861-188">Typ = Syslog &#124; Miara count() przez funkcje</span><span class="sxs-lookup"><span data-stu-id="3a861-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="3a861-189">Liczba Syslog rejestruje przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="3a861-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="3a861-190">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.</span><span class="sxs-lookup"><span data-stu-id="3a861-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="3a861-191">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="3a861-191">Query</span></span> | <span data-ttu-id="3a861-192">Opis</span><span class="sxs-lookup"><span data-stu-id="3a861-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a861-193">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="3a861-193">Syslog</span></span> |<span data-ttu-id="3a861-194">Wszystkie audyt dzienników systemowych.</span><span class="sxs-lookup"><span data-stu-id="3a861-194">All Syslogs.</span></span> |
| <span data-ttu-id="3a861-195">SYSLOG &#124; gdy poziom ważności == "error"</span><span class="sxs-lookup"><span data-stu-id="3a861-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="3a861-196">Wszystkie rekordy dziennika systemowego o ważności błędu.</span><span class="sxs-lookup"><span data-stu-id="3a861-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="3a861-197">SYSLOG &#124; Podsumuj AggregatedValue = count() przez komputer</span><span class="sxs-lookup"><span data-stu-id="3a861-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="3a861-198">Liczba Syslog rejestruje przez komputer.</span><span class="sxs-lookup"><span data-stu-id="3a861-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="3a861-199">SYSLOG &#124; Podsumuj AggregatedValue = count() przez funkcje</span><span class="sxs-lookup"><span data-stu-id="3a861-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="3a861-200">Liczba Syslog rejestruje przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="3a861-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a861-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a861-201">Next steps</span></span>
* <span data-ttu-id="3a861-202">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="3a861-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="3a861-203">Użyj [pola niestandardowe](log-analytics-custom-fields.md) tooparse danych z rekordów dziennika systemowego do poszczególnych pól.</span><span class="sxs-lookup"><span data-stu-id="3a861-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="3a861-204">[Konfigurowanie agentów systemu Linux](log-analytics-linux-agents.md) toocollect innych typów danych.</span><span class="sxs-lookup"><span data-stu-id="3a861-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
