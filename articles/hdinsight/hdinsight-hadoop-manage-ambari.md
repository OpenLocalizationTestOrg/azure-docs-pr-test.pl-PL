---
title: "aaaMonitor i zarządzać nimi za pomocą interfejsu użytkownika sieci Web Ambari w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Ambari toomonitor i zarządzania klastrami usługi HDInsight opartej na systemie Linux. W tym dokumencie możesz dowiedzieć się, jak klastrów hello toouse Interfejsu sieci Web Ambari dołączone do usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="02d0e-104">Zarządzanie klastrami usługi HDInsight za pomocą hello Interfejsu sieci Web Ambari</span><span class="sxs-lookup"><span data-stu-id="02d0e-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="02d0e-105">Apache Ambari upraszcza hello zarządzania i monitorowania klastrów platformy Hadoop, zapewniając łatwy toouse interfejsu użytkownika i REST interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="02d0e-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="02d0e-106">Ambari znajduje się w klastrach HDInsight opartych na systemie Linux i jest używane toomonitor hello klastra i dokonywać zmian konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="02d0e-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="02d0e-107">W tym dokumencie możesz dowiedzieć się, jak toouse hello Interfejsu sieci Web Ambari z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02d0e-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="02d0e-108"><a id="whatis"></a>Co to jest Ambari?</span><span class="sxs-lookup"><span data-stu-id="02d0e-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="02d0e-109">[Apache Ambari](http://ambari.apache.org) ułatwia zarządzanie Hadoop, zapewniając łatwy w użyciu interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="02d0e-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="02d0e-110">Można używać narzędzia Ambari tworzenia, zarządzania i monitorowania klastrów platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="02d0e-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="02d0e-111">Deweloperzy mogą integrować te możliwości w swoich aplikacjach przy użyciu hello [interfejsów API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="02d0e-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="02d0e-112">Domyślnie z klastrami usługi HDInsight, które używają systemu operacyjnego Linux hello jest udostępniany Hello Interfejsu sieci Web Ambari.</span><span class="sxs-lookup"><span data-stu-id="02d0e-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02d0e-113">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="02d0e-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="02d0e-114">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="02d0e-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="02d0e-115">Łączność</span><span class="sxs-lookup"><span data-stu-id="02d0e-115">Connectivity</span></span>

<span data-ttu-id="02d0e-116">Hello Interfejsu sieci Web Ambari jest dostępna w klastrze usługi HDInsight w HTTPS://CLUSTERNAME.azurehdidnsight.net, gdzie **CLUSTERNAME** jest hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02d0e-117">Połączenie tooAmbari w usłudze HDInsight wymaga protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="02d0e-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="02d0e-118">Po wyświetleniu monitu na potrzeby uwierzytelniania, użyj nazwy konta administratora hello i hasło podane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="02d0e-119">Tunel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="02d0e-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="02d0e-120">Gdy Ambari dla klastra jest dostępny bezpośrednio przez hello Internet, niektóre łącza z interfejsu użytkownika sieci Web Ambari (na przykład toohello JobTracker) nie są widoczne na powitania hello internet.</span><span class="sxs-lookup"><span data-stu-id="02d0e-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="02d0e-121">tooaccess tych usług, należy utworzyć tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="02d0e-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="02d0e-122">Aby uzyskać więcej informacji, zobacz [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="02d0e-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="02d0e-123">Interfejs użytkownika sieci Web Ambari</span><span class="sxs-lookup"><span data-stu-id="02d0e-123">Ambari Web UI</span></span>

<span data-ttu-id="02d0e-124">Podczas łączenia z toohello Interfejsu sieci Web Ambari, to zostanie wyświetlony monit o tooauthenticate toohello strony.</span><span class="sxs-lookup"><span data-stu-id="02d0e-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="02d0e-125">Użyj użytkownika Administrator klastra hello (ustawienie domyślne Admin) i hasło użyte podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="02d0e-126">Gdy zostanie otwarta strona hello, należy pamiętać, pasek hello u góry hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="02d0e-127">Ten pasek zawiera hello następujące informacje i kontrolki:</span><span class="sxs-lookup"><span data-stu-id="02d0e-127">This bar contains hello following information and controls:</span></span>

![Nawiguj do ambari](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="02d0e-129">**Logo narzędzia Ambari** -pulpit nawigacyjny hello zostanie otwarta, które mogą być używane toomonitor hello klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="02d0e-130">**Ops # nazwy klastra** -Wyświetla liczbę hello trwających operacji narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="02d0e-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="02d0e-131">Wybieranie nazwy klastra hello lub **# ops** zostanie wyświetlona lista operacje w tle.</span><span class="sxs-lookup"><span data-stu-id="02d0e-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="02d0e-132">**alerty #** -wyświetla ostrzeżenia lub alerty krytyczne dla hello klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="02d0e-133">**Pulpit nawigacyjny** -Wyświetla hello w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="02d0e-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="02d0e-134">**Usługi** — ustawienia informacji i konfiguracji usług hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="02d0e-135">**Hosty** -informacji i ustawień konfiguracji dla hello węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="02d0e-136">**Alerty** -dziennika informacje, ostrzeżenia i alerty krytyczne.</span><span class="sxs-lookup"><span data-stu-id="02d0e-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="02d0e-137">**Administrator** -oprogramowania stosu/usług, które są zainstalowane w klastrze hello, informacje o koncie usługi i zabezpieczeń protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="02d0e-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="02d0e-138">**Przycisk Admin** -Ambari zarządzania, ustawienia użytkownika i wylogowania.</span><span class="sxs-lookup"><span data-stu-id="02d0e-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="02d0e-139">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="02d0e-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="02d0e-140">Alerty</span><span class="sxs-lookup"><span data-stu-id="02d0e-140">Alerts</span></span>

<span data-ttu-id="02d0e-141">Witaj Poniższa lista zawiera hello wspólnej stany alertów używana przez narzędzia Ambari:</span><span class="sxs-lookup"><span data-stu-id="02d0e-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="02d0e-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="02d0e-142">**OK**</span></span>
* <span data-ttu-id="02d0e-143">**Ostrzeżenie**</span><span class="sxs-lookup"><span data-stu-id="02d0e-143">**Warning**</span></span>
* <span data-ttu-id="02d0e-144">**KRYTYCZNE**</span><span class="sxs-lookup"><span data-stu-id="02d0e-144">**CRITICAL**</span></span>
* <span data-ttu-id="02d0e-145">**NIEZNANY**</span><span class="sxs-lookup"><span data-stu-id="02d0e-145">**UNKNOWN**</span></span>

<span data-ttu-id="02d0e-146">Alerty innych niż **OK** spowodować hello **alerty #** wpis u góry hello hello strony toodisplay hello liczbę alertów.</span><span class="sxs-lookup"><span data-stu-id="02d0e-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="02d0e-147">Wybranie tego wpisu powoduje wyświetlenie hello alertów i ich stan.</span><span class="sxs-lookup"><span data-stu-id="02d0e-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="02d0e-148">Alerty są podzielone na kilka domyślnych grup, które mogą być wyświetlane z hello **alerty** strony.</span><span class="sxs-lookup"><span data-stu-id="02d0e-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![Strona alertów](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="02d0e-150">Witaj grup można zarządzać za pomocą hello **akcje** menu i wybierając **Zarządzaj grupami alertu**.</span><span class="sxs-lookup"><span data-stu-id="02d0e-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![Zarządzanie grupami alertu w oknie dialogowym](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="02d0e-152">Można również zarządzać metody alertów i utworzyć powiadomienia o alertach z hello **akcje** menu, wybierając __Zarządzanie powiadomienia Alert__.</span><span class="sxs-lookup"><span data-stu-id="02d0e-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="02d0e-153">Bieżący powiadomienia są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="02d0e-153">Any current notifications are displayed.</span></span> <span data-ttu-id="02d0e-154">Powiadomienia można również utworzyć w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="02d0e-154">You can also create notifications from here.</span></span> <span data-ttu-id="02d0e-155">Powiadomienia mogą być wysyłane za pośrednictwem **E-mail** lub **SNMP** przypadku wystąpienia określonych ważności alertu/kombinacji.</span><span class="sxs-lookup"><span data-stu-id="02d0e-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="02d0e-156">Na przykład możesz wysłać wiadomość e-mail, gdy dowolne hello alertów w hello **domyślne YARN** grupy ustawiono zbyt**krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="02d0e-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![Tworzenie okna dialogowego alertu](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="02d0e-158">Ponadto wybierając __Zarządzaj ustawieniami Alert__ z hello __akcje__ menu pozwala tooset hello liczba alertu musi wystąpić, aby wysłać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="02d0e-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="02d0e-159">To ustawienie może być powiadomienia tooprevent używanych w przypadku błędów przejściowych.</span><span class="sxs-lookup"><span data-stu-id="02d0e-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="02d0e-160">Klaster</span><span class="sxs-lookup"><span data-stu-id="02d0e-160">Cluster</span></span>

<span data-ttu-id="02d0e-161">Witaj **metryki** kartę hello pulpit nawigacyjny zawiera szereg elementy widget, dzięki któremu można łatwo toomonitor hello stan klastra jeden rzut oka.</span><span class="sxs-lookup"><span data-stu-id="02d0e-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="02d0e-162">Kilka elementów widget, takich jak **użycie procesora CPU**, znajdują się dodatkowe informacje po kliknięciu.</span><span class="sxs-lookup"><span data-stu-id="02d0e-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![pulpit nawigacyjny z metryk](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="02d0e-164">Witaj **Heatmaps** karcie są wyświetlane jako kolorowe heatmaps, z zielonym toored metryki.</span><span class="sxs-lookup"><span data-stu-id="02d0e-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![pulpit nawigacyjny z heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="02d0e-166">Aby uzyskać więcej informacji na powitania węzłów w klastrze hello wybierz **hostów**.</span><span class="sxs-lookup"><span data-stu-id="02d0e-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="02d0e-167">Następnie wybierz hello określonego węzła, który chcesz.</span><span class="sxs-lookup"><span data-stu-id="02d0e-167">Then select hello specific node you are interested in.</span></span>

![Szczegóły hosta](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="02d0e-169">Usługi</span><span class="sxs-lookup"><span data-stu-id="02d0e-169">Services</span></span>

<span data-ttu-id="02d0e-170">Witaj **usług** paska bocznego na powitania pulpit nawigacyjny zapewnia szybki wgląd w stan hello hello usługi działające na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="02d0e-171">Różne ikony są używane tooindicate stanu lub akcje, które należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="02d0e-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="02d0e-172">Na przykład symbol żółty odtworzenia jest wyświetlana, jeśli usługa musi toobe ponownego przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="02d0e-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![pasek boczny usług](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="02d0e-174">usługi Hello wyświetlane różnią się typy klastrów usługi HDInsight i wersje.</span><span class="sxs-lookup"><span data-stu-id="02d0e-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="02d0e-175">usługi Hello tutaj wyświetlane mogą być inne niż usług hello wyświetlane dla klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="02d0e-176">Wybranie usługi powoduje wyświetlenie bardziej szczegółowych informacji w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-176">Selecting a service displays more detailed information on hello service.</span></span>

![Podsumowanie usługi](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="02d0e-178">Szybkie łącza</span><span class="sxs-lookup"><span data-stu-id="02d0e-178">Quick links</span></span>

<span data-ttu-id="02d0e-179">Wyświetlanie niektórych usług **szybkie linki** łącze u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="02d0e-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="02d0e-180">Może to być używane tooaccess specyficzne dla usługi web UI, takich jak:</span><span class="sxs-lookup"><span data-stu-id="02d0e-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="02d0e-181">**Historia zadań** -historii zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="02d0e-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="02d0e-182">**Menedżer zasobów** -YARN ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="02d0e-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="02d0e-183">**NameNode** -Hadoop Distributed Interfejsu NameNode (HDFS) systemu plików.</span><span class="sxs-lookup"><span data-stu-id="02d0e-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="02d0e-184">**Interfejs użytkownika sieci Web Oozie** -Oozie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02d0e-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="02d0e-185">Wybranie dowolnego z tych łączy otwiera nową kartę w przeglądarce, która wyświetla hello wybranej strony.</span><span class="sxs-lookup"><span data-stu-id="02d0e-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="02d0e-186">Wybór hello **szybkie linki** wpis dla usługi mogą zwracać błąd "nie można odnaleźć serwera".</span><span class="sxs-lookup"><span data-stu-id="02d0e-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="02d0e-187">Jeśli ten błąd wystąpi, należy użyć tunelu SSH przy użyciu hello **szybkie linki** wpis dla tej usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="02d0e-188">Aby uzyskać informacje, zobacz [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="02d0e-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="02d0e-189">Zarządzanie</span><span class="sxs-lookup"><span data-stu-id="02d0e-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="02d0e-190">Ambari użytkowników, grup i uprawnień</span><span class="sxs-lookup"><span data-stu-id="02d0e-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="02d0e-191">Praca z użytkownikami, grupami i uprawnienia są obsługiwane w przypadku korzystania z [przyłączony do domeny](hdinsight-domain-joined-introduction.md) klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02d0e-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="02d0e-192">Uzyskać informacji na temat używania hello interfejsu użytkownika zarządzania Ambari w klastrze przyłączonych do domeny, zobacz [zarządzania klastrami HDInsight przyłączonych do domeny](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02d0e-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="02d0e-193">Nie należy zmieniać hasła hello hello Ambari strażnika (hdinsightwatchdog) w klastrze usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="02d0e-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="02d0e-194">Zmiana podziały hasła hello hello akcji skryptu toouse możliwości lub operacji skalowania z klastrem.</span><span class="sxs-lookup"><span data-stu-id="02d0e-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="02d0e-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="02d0e-195">Hosts</span></span>

<span data-ttu-id="02d0e-196">Witaj **hostów** strona zawiera listę wszystkich hostów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="02d0e-197">hosty toomanage, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="02d0e-197">toomanage hosts, follow these steps.</span></span>

![strony hosty](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="02d0e-199">Dodawanie, wycofywanie z eksploatacji i recommissioning hosta nie można używać z klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02d0e-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="02d0e-200">Wybierz host hello, że chcesz toomanage.</span><span class="sxs-lookup"><span data-stu-id="02d0e-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="02d0e-201">Użyj hello **akcje** hello akcji tooselect menu, że chcesz tooperform:</span><span class="sxs-lookup"><span data-stu-id="02d0e-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="02d0e-202">**Uruchom wszystkie składniki** -uruchomić wszystkie składniki hello hoście.</span><span class="sxs-lookup"><span data-stu-id="02d0e-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="02d0e-203">**Zatrzymaj wszystkie składniki** -zatrzymania wszystkich składników na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="02d0e-204">**Uruchom ponownie wszystkie składniki** — zatrzymano i uruchomić wszystkie składniki na powitania hosta.</span><span class="sxs-lookup"><span data-stu-id="02d0e-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="02d0e-205">**Włącz tryb konserwacji** -pomija alerty dla hello hosta.</span><span class="sxs-lookup"><span data-stu-id="02d0e-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="02d0e-206">W tym trybie powinien być włączony, jeśli przeprowadzasz akcje, które generują alerty.</span><span class="sxs-lookup"><span data-stu-id="02d0e-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="02d0e-207">Na przykład zatrzymywania i uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="02d0e-208">**Wyłącz tryb konserwacji** — zwraca tekst hello alerty toonormal hosta.</span><span class="sxs-lookup"><span data-stu-id="02d0e-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="02d0e-209">**Zatrzymaj** -zatrzymuje DataNode lub NodeManagers na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="02d0e-210">**Uruchom** — uruchamia DataNode lub NodeManagers na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="02d0e-211">**Uruchom ponownie** -przerywa działanie i uruchamia DataNode lub NodeManagers na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="02d0e-212">**Likwidowanie** — usuwa z hello klastra hosta.</span><span class="sxs-lookup"><span data-stu-id="02d0e-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="02d0e-213">Nie należy używać tej akcji w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02d0e-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="02d0e-214">**Recommission** -dodaje toohello wcześniej zlikwidowana hosta klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="02d0e-215">Nie należy używać tej akcji w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02d0e-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="02d0e-216"><a id="service"></a>Usługi</span><span class="sxs-lookup"><span data-stu-id="02d0e-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="02d0e-217">Z hello **pulpitu nawigacyjnego** lub **usług** Użyj hello **akcje** znajdujący się u dołu hello hello listę usług toostop i uruchomić wszystkie usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Akcje usługi](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="02d0e-219">Gdy **Dodaj usługę** znajduje się w tym menu powinna być klastra usługi HDInsight toohello usług używanych tooadd.</span><span class="sxs-lookup"><span data-stu-id="02d0e-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="02d0e-220">Należy dodać nowe usługi za pomocą akcji skryptu podczas inicjowania obsługi klastra.</span><span class="sxs-lookup"><span data-stu-id="02d0e-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="02d0e-221">Aby uzyskać więcej informacji dotyczących za pomocą akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="02d0e-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="02d0e-222">Podczas hello **akcje** przycisku można uruchomić ponownie wszystkie usługi, często ma toostart zatrzymanie i ponowne uruchamianie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="02d0e-223">Użyj hello, wykonując kroki tooperform akcje na pojedynczej usługi:</span><span class="sxs-lookup"><span data-stu-id="02d0e-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="02d0e-224">Z hello **pulpitu nawigacyjnego** lub **usług** wybierz opcję usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="02d0e-225">Z góry hello hello **Podsumowanie** Użyj hello **akcji usługi** przycisk i wybierz hello tootake akcji.</span><span class="sxs-lookup"><span data-stu-id="02d0e-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="02d0e-226">Spowoduje to ponowne uruchomienie usługi hello we wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="02d0e-226">This restarts hello service on all nodes.</span></span>

    ![działanie usługi](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="02d0e-228">Ponowne uruchamianie niektórych usług uruchomionej hello klastra może generować alerty.</span><span class="sxs-lookup"><span data-stu-id="02d0e-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="02d0e-229">tooavoid alertów, można użyć hello **akcji usługi** tooenable przycisk **trybu konserwacji** hello usługi przed wykonaniem hello ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="02d0e-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="02d0e-230">Po wybraniu akcji hello **# op** wpis u góry hello hello strony zwiększa tooshow, która jest wykonywana operacji w tle.</span><span class="sxs-lookup"><span data-stu-id="02d0e-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="02d0e-231">Jeśli skonfigurowano toodisplay, zostanie wyświetlona lista hello operacje w tle.</span><span class="sxs-lookup"><span data-stu-id="02d0e-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02d0e-232">Jeśli włączono **trybu konserwacji** usługi hello Pamiętaj toodisable go za pomocą hello **akcji usługi** przycisku po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="02d0e-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="02d0e-233">tooconfigure usługi, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="02d0e-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="02d0e-234">Z hello **pulpitu nawigacyjnego** lub **usług** wybierz opcję usługi.</span><span class="sxs-lookup"><span data-stu-id="02d0e-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="02d0e-235">Wybierz hello **Configs** kartę hello bieżącej konfiguracji jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="02d0e-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="02d0e-236">Wyświetlana jest również lista poprzedniej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="02d0e-236">A list of previous configurations is also displayed.</span></span>

    ![Konfiguracje](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="02d0e-238">Użyj hello pola wyświetlane toomodify hello konfiguracji, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="02d0e-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="02d0e-239">Lub wybierz poprzednią konfigurację, a następnie wybierz **stać się bieżącym** tooroll kopii toohello poprzednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="02d0e-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="02d0e-240">Widoki Ambari</span><span class="sxs-lookup"><span data-stu-id="02d0e-240">Ambari views</span></span>

<span data-ttu-id="02d0e-241">Widoki Ambari pozwalają deweloperom tooplug elementy interfejsu użytkownika do hello Ambari Web UI za pomocą hello [Framework widoków Ambari](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="02d0e-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="02d0e-242">Usługa HDInsight zapewnia hello następujące widoki z typami klastra usługi Hadoop:</span><span class="sxs-lookup"><span data-stu-id="02d0e-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="02d0e-243">Yarn menedżera kolejek: hello menedżera kolejek udostępnia prosty interfejs do wyświetlanie i modyfikowanie kolejek YARN.</span><span class="sxs-lookup"><span data-stu-id="02d0e-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="02d0e-244">Widok hive: hello Hive View pozwala toorun zapytań programu Hive bezpośrednio z przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="02d0e-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="02d0e-245">Możesz zapisać zapytania, wyświetlić wyniki, zapisane wyniki w magazynie klastra toohello lub pobrać systemu lokalnego tooyour wyników.</span><span class="sxs-lookup"><span data-stu-id="02d0e-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="02d0e-246">Aby uzyskać więcej informacji na korzystanie z widoków Hive, zobacz [Użyj widoki Hive z usługą HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="02d0e-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="02d0e-247">Widok tez: hello widoku Tez pozwala toobetter zrozumieć i zoptymalizować zadania.</span><span class="sxs-lookup"><span data-stu-id="02d0e-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="02d0e-248">Można wyświetlać informacje w sposób Tez zadania są wykonywane, i jakie zasoby są używane.</span><span class="sxs-lookup"><span data-stu-id="02d0e-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
