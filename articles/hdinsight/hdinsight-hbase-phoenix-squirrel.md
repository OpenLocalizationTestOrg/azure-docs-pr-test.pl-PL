---
title: aaaUse Apache Phoenix i SQuirreL z systemem Windows Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Apache Phoenix w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="cb530-103">Użyj Apache Phoenix i SQuirreL z klastrami HBase opartych na systemie Windows w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb530-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="cb530-104">Dowiedz się, jak toouse [Apache Phoenix](http://phoenix.apache.org/) w usłudze HDInsight i w jaki sposób tooinstall i skonfigurować SQuirreL na stacji roboczej klastra HBase tooan tooconnect w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb530-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="cb530-105">Aby uzyskać więcej informacji na temat Phoenix, zobacz [Phoenix w ciągu 15 minut lub mniej](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="cb530-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="cb530-106">Aby hello Phoenix gramatyki, zobacz [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="cb530-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="cb530-107">Aby hello Phoenix informacje o wersji w usłudze HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cb530-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="cb530-108">Witaj czynnościach w ramach tego dokumentu działa tylko w przypadku klastrów usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="cb530-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="cb530-109">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="cb530-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="cb530-110">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cb530-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cb530-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="cb530-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="cb530-112">Uzyskać informacji na temat używania Phoenix na opartych na systemie Linux usługi HDInsight, zobacz [Użyj Apache Phoenix z bazy danych HBase opartych na systemie Linux klastrów w usłudze HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb530-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="cb530-113">Użyj SQLLine</span><span class="sxs-lookup"><span data-stu-id="cb530-113">Use SQLLine</span></span>
<span data-ttu-id="cb530-114">[SQLLine](http://sqlline.sourceforge.net/) jest tooexecute narzędzie wiersza polecenia SQL.</span><span class="sxs-lookup"><span data-stu-id="cb530-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cb530-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb530-115">Prerequisites</span></span>
<span data-ttu-id="cb530-116">Przed użyciem SQLLine, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="cb530-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="cb530-117">**Klaster HBase w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cb530-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="cb530-118">Aby uzyskać informacje dotyczące udostępniania bazy danych HBase klastra, zobacz [Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="cb530-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="cb530-119">**Połącz klaster HBase toohello za pośrednictwem protokołu RDP hello**.</span><span class="sxs-lookup"><span data-stu-id="cb530-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="cb530-120">Aby uzyskać instrukcje, zobacz [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu klasycznego portalu Azure hello][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="cb530-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="cb530-121">**toofind limit hello nazwy hosta**</span><span class="sxs-lookup"><span data-stu-id="cb530-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="cb530-122">Otwórz **wiersza polecenia platformy Hadoop** z hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="cb530-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="cb530-123">Uruchom hello następującego sufiksu DNS hello tooget polecenia:</span><span class="sxs-lookup"><span data-stu-id="cb530-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="cb530-124">Zapisz **sufiks DNS konkretnego połączenia**.</span><span class="sxs-lookup"><span data-stu-id="cb530-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="cb530-125">Na przykład *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="cb530-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="cb530-126">Po ustanowieniu połączenia klastra HBase tooan należy tooone tooconnect z hello dozorcy przy użyciu nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="cb530-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="cb530-127">Każdy klaster usługi HDInsight ma dozorcy 3.</span><span class="sxs-lookup"><span data-stu-id="cb530-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="cb530-128">Są one *zookeeper0*, *zookeeper1*, i *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="cb530-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="cb530-129">Witaj nazwa FQDN będzie wyglądać mniej więcej tak *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="cb530-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="cb530-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="cb530-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="cb530-131">Otwórz **wiersza polecenia platformy Hadoop** z hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="cb530-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="cb530-132">Uruchom następujące polecenia tooopen SQLLine hello:</span><span class="sxs-lookup"><span data-stu-id="cb530-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="cb530-134">Witaj polecenia używane w przykładowym hello:</span><span class="sxs-lookup"><span data-stu-id="cb530-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="cb530-135">Aby uzyskać więcej informacji, zobacz [ręcznego SQLLine](http://sqlline.sourceforge.net/#manual) i [gramatyki Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="cb530-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="cb530-136">Użyj SQuirreL</span><span class="sxs-lookup"><span data-stu-id="cb530-136">Use SQuirreL</span></span>
<span data-ttu-id="cb530-137">[Klient SQL sQuirreL](http://squirrel-sql.sourceforge.net/) graficznego program Java, który pozwala tooview hello struktury bazy danych zgodne JDBC, Przeglądaj hello dane w tabelach, wydania poleceń SQL itp. Może być używane tooconnect tooApache Phoenix w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb530-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="cb530-138">W tej sekcji opisano sposób tooinstall i skonfigurować SQuirreL na stacji roboczej tooconnect tooan HBase klastra w usłudze HDInsight za pośrednictwem sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="cb530-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cb530-139">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb530-139">Prerequisites</span></span>
<span data-ttu-id="cb530-140">Przed wykonaniem procedury hello, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="cb530-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="cb530-141">Klaster HBase wdrożyć tooan sieci wirtualnej platformy Azure z maszyną wirtualną DNS.</span><span class="sxs-lookup"><span data-stu-id="cb530-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="cb530-142">Aby uzyskać instrukcje, zobacz [HBase Tworzenie klastrów w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="cb530-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="cb530-143">Pobierz sufiks DNS konkretnego połączenia programu hello HBase klastra klastra.</span><span class="sxs-lookup"><span data-stu-id="cb530-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="cb530-144">tooget go RDP do klastra hello, a następnie uruchom polecenie IPConfig.</span><span class="sxs-lookup"><span data-stu-id="cb530-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="cb530-145">sufiks DNS Hello jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="cb530-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="cb530-146">Pobierz i zainstaluj [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="cb530-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="cb530-147">Konieczne będzie makecert z toocreate pakietu hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cb530-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="cb530-148">Pobierz i zainstaluj [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="cb530-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="cb530-149">SQuirreL SQL klienta w wersji 3.0 lub nowszego wymaga środowiska JRE wersji 1.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cb530-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="cb530-150">Skonfiguruj toohello połączenia sieci VPN typu punkt-lokacja sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cb530-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="cb530-151">Obejmuje 3 kroki konfigurowania połączenia VPN punkt lokacja:</span><span class="sxs-lookup"><span data-stu-id="cb530-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="cb530-152">Konfigurowanie sieci wirtualnej i brama routingu dynamicznego</span><span class="sxs-lookup"><span data-stu-id="cb530-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="cb530-153">Tworzenie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="cb530-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="cb530-154">Konfigurowanie klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="cb530-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="cb530-155">Zobacz [skonfigurować tooan połączenia sieci VPN typu punkt-lokacja sieci wirtualnej Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cb530-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="cb530-156">Konfigurowanie sieci wirtualnej i brama routingu dynamicznego</span><span class="sxs-lookup"><span data-stu-id="cb530-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="cb530-157">Upewnić się, że po uprzednim udostępnieniu klaster HBase w sieci wirtualnej platformy Azure (patrz wymagania wstępne powitania dla tej sekcji).</span><span class="sxs-lookup"><span data-stu-id="cb530-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="cb530-158">Witaj następnym krokiem jest tooconfigure połączenie punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="cb530-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="cb530-159">**połączenie punkt lokacja hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="cb530-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="cb530-160">Zaloguj się toohello [klasycznego portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="cb530-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="cb530-161">Powitania po lewej stronie, kliknij przycisk **sieci**.</span><span class="sxs-lookup"><span data-stu-id="cb530-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="cb530-162">Kliknij przycisk hello sieci wirtualnej zostały utworzone (zobacz [klastrów HBase udostępniania w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="cb530-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="cb530-163">Kliknij przycisk **Konfiguruj** od góry hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="cb530-164">W hello **połączenie punkt lokacja** zaznacz **Konfiguracja połączenia punkt lokacja**.</span><span class="sxs-lookup"><span data-stu-id="cb530-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="cb530-165">Skonfiguruj **uruchamianie IP** i **CIDR** adresów toospecify hello zakres adresów IP z których klienci VPN będą otrzymywać adresu IP po połączeniu.</span><span class="sxs-lookup"><span data-stu-id="cb530-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="cb530-166">Witaj zakresu nie może nakładać się ze wszystkimi hello zakresy znajduje się w lokalnej sieci i hello sieci wirtualnej platformy Azure, które będą łączyć się.</span><span class="sxs-lookup"><span data-stu-id="cb530-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="cb530-167">Na przykład.</span><span class="sxs-lookup"><span data-stu-id="cb530-167">For example.</span></span> <span data-ttu-id="cb530-168">w przypadku wybrania 10.0.0.0/20 hello sieci wirtualnej, można wybrać 10.1.0.0/24 dla przestrzeni adresowej powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="cb530-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="cb530-169">Zobacz hello [punkt-lokacja, łączność] [ vnet-point-to-site-connectivity] strony, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cb530-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="cb530-170">W sekcji spacje adresów sieci wirtualnej powitania kliknij **Dodaj podsieć bramy**.</span><span class="sxs-lookup"><span data-stu-id="cb530-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="cb530-171">Kliknij przycisk **ZAPISAĆ** na powitania u dołu strony hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="cb530-172">Kliknij przycisk **tak** tooconfirm hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="cb530-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="cb530-173">Poczekaj, aż hello system zakończył wprowadzania hello zmiany przed kontynuowaniem toohello następnej procedury.</span><span class="sxs-lookup"><span data-stu-id="cb530-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="cb530-174">**toocreate dynamiczne bramy routingu**</span><span class="sxs-lookup"><span data-stu-id="cb530-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="cb530-175">Hello klasycznego portalu Azure, kliknij **pulpitu NAWIGACYJNEGO** od góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="cb530-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="cb530-176">Kliknij przycisk **Tworzenie bramy** od dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="cb530-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="cb530-177">Kliknij przycisk **tak** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="cb530-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="cb530-178">Poczekaj, aż utworzeniu hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cb530-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="cb530-179">Kliknij przycisk **pulpitu NAWIGACYJNEGO** od góry hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="cb530-180">Zostanie wyświetlony visual diagram hello sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="cb530-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Diagram wirtualnego punkt lokacja sieci wirtualnej platformy Azure][img-vnet-diagram]

    <span data-ttu-id="cb530-182">Witaj diagram przedstawia 0 połączeń klientów.</span><span class="sxs-lookup"><span data-stu-id="cb530-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="cb530-183">Po wprowadzeniu toohello połączenia wirtualnej sieci numer hello będzie tooone zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="cb530-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="cb530-184">Tworzenie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="cb530-184">Create your certificates</span></span>
<span data-ttu-id="cb530-185">Jednym ze sposobów toocreate jest certyfikatu X.509 przy użyciu hello narzędzie tworzenia certyfikatów (makecert.exe), który jest dostarczany z [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb530-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="cb530-186">**toocreate certyfikat główny z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="cb530-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="cb530-187">Na stacji roboczej otwórz okno wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb530-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="cb530-188">Przejdź folder Narzędzia Visual Studio toohello.</span><span class="sxs-lookup"><span data-stu-id="cb530-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="cb530-189">następujące polecenie w poniższym przykładzie hello Hello utworzy i zainstalować certyfikat główny w magazynie certyfikatów osobistych hello na stacji roboczej i również utworzyć odpowiedni plik .cer będzie jego przesłania toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cb530-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="cb530-190">Zmień toohello katalogu, który ma być hello toobe pliku .cer znajdują się w, gdzie HBaseVnetVPNRootCertificate jest nazwa hello mają toouse hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cb530-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="cb530-191">Nie zamykaj hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb530-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="cb530-192">Będzie on potrzebny w następnej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb530-193">Ponieważ utworzono certyfikat główny, z którego zostanie wygenerowana certyfikaty klienta, może mają tooexport ten certyfikat wraz z kluczem prywatnym i zapisz go w bezpiecznym miejscu tooa, których mogą zostać odzyskane.</span><span class="sxs-lookup"><span data-stu-id="cb530-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="cb530-194">**toocreate certyfikatu klienta**</span><span class="sxs-lookup"><span data-stu-id="cb530-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="cb530-195">Z hello sam wiersz polecenia (ma toobe na powitania tym samym komputerze, na którym utworzono hello certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="cb530-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="cb530-196">certyfikat klienta na powitania musi zostać wygenerowany z hello certyfikatu głównego), uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cb530-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="cb530-197">HBaseVnetVPNRootCertificate jest nazwa certyfikatu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="cb530-198">Ma ona nazwę certyfikatu głównego hello toomatch.</span><span class="sxs-lookup"><span data-stu-id="cb530-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="cb530-199">Zarówno hello certyfikatu głównego, jak i certyfikat klienta na powitania są przechowywane w magazynie certyfikatów osobistych na komputerze.</span><span class="sxs-lookup"><span data-stu-id="cb530-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="cb530-200">Użyj certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="cb530-200">Use certmgr.msc tooverify.</span></span>

    ![Certyfikat sieci VPN punkt lokacja sieci wirtualnej platformy Azure][img-certificate]

    <span data-ttu-id="cb530-202">Certyfikat klienta należy zainstalować na każdym komputerze, które mają sieci wirtualnej toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cb530-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="cb530-203">Zaleca się tworzenia unikatowych klientów certyfikatów dla każdego komputera, które mają sieci wirtualnej toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cb530-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="cb530-204">certyfikaty klienta hello tooexport, użyj certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="cb530-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="cb530-205">**tooupload hello głównego certyfikatu toohello klasycznego portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="cb530-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="cb530-206">Hello klasycznego portalu Azure, kliknij **sieci** powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="cb530-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="cb530-207">Kliknij przycisk hello sieci wirtualnej wdrożonym klastra HBase do.</span><span class="sxs-lookup"><span data-stu-id="cb530-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="cb530-208">Kliknij przycisk **certyfikaty** od góry hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="cb530-209">Kliknij przycisk **przekazać** z hello dołu, a następnie określ plik certyfikatu głównego hello utworzonego w procedurze hello przed ostatnią.</span><span class="sxs-lookup"><span data-stu-id="cb530-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="cb530-210">Poczekaj, aż hello certyfikat został zaimportowany.</span><span class="sxs-lookup"><span data-stu-id="cb530-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="cb530-211">Kliknij przycisk **pulpitu NAWIGACYJNEGO** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="cb530-212">Witaj wirtualnych diagram przedstawia stan hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="cb530-213">Konfigurowanie klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="cb530-213">Configure your VPN client</span></span>
<span data-ttu-id="cb530-214">**pakiet sieci VPN klienta hello toodownload i instalacji**</span><span class="sxs-lookup"><span data-stu-id="cb530-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="cb530-215">Ze strony pulpitu NAWIGACYJNEGO hello hello sieci wirtualnej, w sekcji szybkiego dostępu powitania kliknij **pobierania hello 64-bitowego klienta VPN pakietu** lub **pobierania hello pakietu sieci VPN klienta 32-bitowego** na podstawie użytkownika wersja systemu operacyjnego stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="cb530-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="cb530-216">Kliknij przycisk **Uruchom** tooinstall hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="cb530-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="cb530-217">W wierszu hello zabezpieczeń, kliknij przycisk **więcej informacji o**, a następnie kliknij przycisk **Uruchom mimo to**.</span><span class="sxs-lookup"><span data-stu-id="cb530-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="cb530-218">Kliknij przycisk **tak** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="cb530-218">Click **Yes** twice.</span></span>

<span data-ttu-id="cb530-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="cb530-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="cb530-220">Na pulpicie hello stacji roboczej kliknij ikonę sieci hello na pasku zadań hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="cb530-221">Zostanie wyświetlona połączenia sieci VPN z nazwą sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cb530-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="cb530-222">Kliknij nazwę połączenia VPN hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="cb530-223">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="cb530-223">Click **Connect**.</span></span>

<span data-ttu-id="cb530-224">**Witaj tootest rozpoznawania nazw połączenia i domen sieci VPN**</span><span class="sxs-lookup"><span data-stu-id="cb530-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="cb530-225">Witaj stacji roboczej, otwórz wiersz polecenia i ping powitania od nazwy podanej klastra HBase hello sufiks DNS jest myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="cb530-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="cb530-226">Instalowanie i konfigurowanie SQuirreL na stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="cb530-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="cb530-227">**tooinstall SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="cb530-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="cb530-228">Pobierz plik jar klienta hello SQuirreL SQL z [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="cb530-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="cb530-229">Witaj Otwórz i uruchom plik jar.</span><span class="sxs-lookup"><span data-stu-id="cb530-229">Open/run hello jar file.</span></span> <span data-ttu-id="cb530-230">Wymaga to hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="cb530-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="cb530-231">Kliknij przycisk **dalej** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="cb530-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="cb530-232">Określ ścieżkę, w którym masz hello uprawnienie do zapisu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cb530-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cb530-233">domyślny folder instalacji Hello znajduje się w folderze C:\Program Files\squirrel-sql 3,6 hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="cb530-234">W ścieżce toothis toowrite kolejności Instalator hello musi mieć przyznane uprawnienia administratora hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="cb530-235">Można otworzyć wiersz polecenia jako administrator, przejdź na tooJava folder bin, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="cb530-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="cb530-236">Java.exe-jar [ścieżka hello plik jar SQuirreL hello]</span><span class="sxs-lookup"><span data-stu-id="cb530-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="cb530-237">Kliknij przycisk **OK** tooconfirm tworzenie hello katalog docelowy.</span><span class="sxs-lookup"><span data-stu-id="cb530-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="cb530-238">Witaj domyślne ustawienie to tooinstall hello Base i standardowe pakietów.</span><span class="sxs-lookup"><span data-stu-id="cb530-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="cb530-239">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cb530-239">Click **Next**.</span></span>
7. <span data-ttu-id="cb530-240">Kliknij przycisk **dalej** dwa razy, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="cb530-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="cb530-241">**tooinstall hello Phoenix sterownika**</span><span class="sxs-lookup"><span data-stu-id="cb530-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="cb530-242">Plik jar sterownika phoenix Hello znajduje się na powitania klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="cb530-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="cb530-243">Ścieżka Hello jest podobne następujące toohello oparte na wersji hello:</span><span class="sxs-lookup"><span data-stu-id="cb530-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="cb530-244">Należy toocopy go tooyour stacji roboczej, w obszarze hello [folder instalacji SQuirreL] / lib ścieżki.</span><span class="sxs-lookup"><span data-stu-id="cb530-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="cb530-245">Witaj Najprostszym sposobem jest tooRDP na powitania klastra, a następnie użyj pliku kopiowanie i wklejanie (CTRL + C i CTRL + V) toocopy on tooyour stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="cb530-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="cb530-246">**tooadd tooSQuirreL sterownika Phoenix**</span><span class="sxs-lookup"><span data-stu-id="cb530-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="cb530-247">Otwórz klienta SQL SQuirreL ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="cb530-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="cb530-248">Kliknij przycisk hello **sterownika** kartę powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="cb530-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="cb530-249">Z hello **sterowniki** menu, kliknij przycisk **nowego sterownika**.</span><span class="sxs-lookup"><span data-stu-id="cb530-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="cb530-250">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cb530-250">Enter hello following information:</span></span>

   * <span data-ttu-id="cb530-251">**Nazwa**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="cb530-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="cb530-252">**Przykładowy adres URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="cb530-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="cb530-253">**Nazwa klasy**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="cb530-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="cb530-254">Użytkownik małe litery w hello przykładowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="cb530-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="cb530-255">Można użyć ich pełną dozorcy kworum w przypadku, gdy jeden z nich jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="cb530-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="cb530-256">nazwy hostów Hello są zookeeper0, zookeeper1 i zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="cb530-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL sterownika][img-squirrel-driver]
5. <span data-ttu-id="cb530-258">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb530-258">Click **OK**.</span></span>

<span data-ttu-id="cb530-259">**toocreate klaster HBase toohello aliasu**</span><span class="sxs-lookup"><span data-stu-id="cb530-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="cb530-260">SQuirreL, kliknij hello **aliasy** kartę powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="cb530-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="cb530-261">Z hello **aliasy** menu, kliknij przycisk **nowy Alias**.</span><span class="sxs-lookup"><span data-stu-id="cb530-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="cb530-262">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cb530-262">Enter hello following information:</span></span>

   * <span data-ttu-id="cb530-263">**Nazwa**: hello nazwę klastra HBase hello lub dowolną nazwę preferowane.</span><span class="sxs-lookup"><span data-stu-id="cb530-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="cb530-264">**Sterownik**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="cb530-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="cb530-265">To musi odpowiadać nazwie sterownik hello, utworzony w poprzedniej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="cb530-266">**Adres URL**: hello adres URL jest kopiowana z konfiguracji sterownika.</span><span class="sxs-lookup"><span data-stu-id="cb530-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="cb530-267">Upewnij się, że toouser małe litery.</span><span class="sxs-lookup"><span data-stu-id="cb530-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="cb530-268">**Nazwa użytkownika**: może być dowolny tekst.</span><span class="sxs-lookup"><span data-stu-id="cb530-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="cb530-269">Ponieważ używane połączenie z siecią VPN w tym miejscu hello nazwa użytkownika nie jest używany w ogóle.</span><span class="sxs-lookup"><span data-stu-id="cb530-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="cb530-270">**Hasło**: może być dowolny tekst.</span><span class="sxs-lookup"><span data-stu-id="cb530-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL sterownika][img-squirrel-alias]
4. <span data-ttu-id="cb530-272">Kliknij przycisk **testu**.</span><span class="sxs-lookup"><span data-stu-id="cb530-272">Click **Test**.</span></span>
5. <span data-ttu-id="cb530-273">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="cb530-273">Click **Connect**.</span></span> <span data-ttu-id="cb530-274">Po jego nawiązaniu połączenia hello, SQuirreL wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="cb530-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="cb530-276">**toorun testu**</span><span class="sxs-lookup"><span data-stu-id="cb530-276">**toorun a test**</span></span>

1. <span data-ttu-id="cb530-277">Kliknij przycisk hello **SQL** karcie prawo dalej toohello **obiektów** kartę.</span><span class="sxs-lookup"><span data-stu-id="cb530-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="cb530-278">Skopiuj i Wklej hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="cb530-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="cb530-279">Kliknij przycisk Uruchom hello.</span><span class="sxs-lookup"><span data-stu-id="cb530-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="cb530-281">Przełącz wstecz toohello **obiektów** kartę.</span><span class="sxs-lookup"><span data-stu-id="cb530-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="cb530-282">Rozwiń nazwę aliasu hello, a następnie rozwiń **tabeli**.</span><span class="sxs-lookup"><span data-stu-id="cb530-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="cb530-283">Zostanie wyświetlona nowa tabela hello kategorii.</span><span class="sxs-lookup"><span data-stu-id="cb530-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb530-284">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb530-284">Next steps</span></span>
<span data-ttu-id="cb530-285">W tym artykule wiesz już, jak toouse Apache Phoenix w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb530-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="cb530-286">toolearn więcej, zobacz</span><span class="sxs-lookup"><span data-stu-id="cb530-286">toolearn more, see</span></span>

* <span data-ttu-id="cb530-287">[Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="cb530-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="cb530-288">[Udostępnianie klastrów HBase w sieci wirtualnej Azure][hdinsight-hbase-provision-vnet]: Z integracji sieci wirtualnej klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak aplikacje mogą komunikować się z HBase bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="cb530-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="cb530-289">[Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md): Dowiedz się, jak replikacji bazy danych HBase tooconfigure między dwoma centrami danych Azure.</span><span class="sxs-lookup"><span data-stu-id="cb530-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="cb530-290">[Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]: Dowiedz się, jak toodo w czasie rzeczywistym [analizy wskaźniki nastrojów klientów](http://en.wikipedia.org/wiki/Sentiment_analysis) dużych danych przy użyciu bazy danych HBase w klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb530-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
