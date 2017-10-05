---
title: "HDInsight nawiązać połączenia z siecią lokalną - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia klastra usługi HDInsight w sieci wirtualnej platformy Azure, a następnie połącz go z sieci lokalnej. Dowiedz się, jak skonfigurować rozpoznawanie nazw między HDInsight i siecią lokalną przy użyciu niestandardowego serwera DNS."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="b39b2-104">HDInsight nawiązać połączenie z siecią lokalną</span><span class="sxs-lookup"><span data-stu-id="b39b2-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="b39b2-105">Dowiedz się, jak HDInsight połączyć się z sieci lokalnej przy użyciu sieci wirtualnych Azure i bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b39b2-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="b39b2-106">Ten dokument zawiera informacje na temat planowania na:</span><span class="sxs-lookup"><span data-stu-id="b39b2-106">This document provides planning information on:</span></span>

* <span data-ttu-id="b39b2-107">Za pomocą usługi HDInsight w sieci wirtualnej Azure, który łączy się z siecią lokalną.</span><span class="sxs-lookup"><span data-stu-id="b39b2-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="b39b2-108">Konfigurowanie rozpoznawania nazw DNS między sieci wirtualnej i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="b39b2-109">Konfigurowanie grup zabezpieczeń sieci, aby ograniczyć dostęp do Internetu do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b39b2-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="b39b2-110">Porty dostarczanych z usługą HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="b39b2-111">Utwórz konfigurację sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b39b2-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b39b2-112">Jeśli szukasz wskazówki krok po kroku dotyczące łączenia HDInsight do lokalnej sieci za pomocą sieci wirtualnej platformy Azure, zobacz [HDInsight połączyć się z siecią lokalną](connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="b39b2-113">Aby dowiedzieć się, jak utworzyć sieci wirtualnej Azure, która jest połączona z siecią lokalną, należy użyć następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="b39b2-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="b39b2-114">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b39b2-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="b39b2-115">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b39b2-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="b39b2-116">Korzystanie z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b39b2-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="b39b2-117">Konfigurowanie rozpoznawania nazw</span><span class="sxs-lookup"><span data-stu-id="b39b2-117">Configure name resolution</span></span>

<span data-ttu-id="b39b2-118">Aby umożliwić HDInsight i zasoby przyłączone do sieci w celu komunikacji według nazwy, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b39b2-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="b39b2-119">Utwórz niestandardowy serwer DNS w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b39b2-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="b39b2-120">Skonfiguruj sieć wirtualną do użycia niestandardowego serwera DNS, zamiast domyślnej Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="b39b2-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="b39b2-121">Konfiguruj przekazywanie między niestandardowy serwer DNS i serwer DNS lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b39b2-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="b39b2-122">Ta konfiguracja zapewnia następujące działania:</span><span class="sxs-lookup"><span data-stu-id="b39b2-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="b39b2-123">Żądania dla nazwy FQDN, które mają sufiks DNS __dla sieci wirtualnej__ są przekazywane do niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="b39b2-124">Niestandardowy serwer DNS przekazuje następnie te żądania do usługi Azure cyklicznego programu rozpoznawania nazw, która zwraca adres IP.</span><span class="sxs-lookup"><span data-stu-id="b39b2-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="b39b2-125">Wszystkie inne żądania są przekazywane do lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="b39b2-126">Nawet żądania publicznego zasobów internetowych, takich jak microsoft.com są przekazywane do lokalnego serwera DNS do rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="b39b2-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="b39b2-127">Na poniższym diagramie zielony wiersze są żądania dotyczące zasobów, które kończą się sufiksem DNS w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="b39b2-128">Niebieski wiersze są żądania dotyczące zasobów w sieci lokalnej lub w publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="b39b2-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagram przedstawiający sposób żądania DNS są rozpoznawane w konfiguracji używane w tym dokumencie](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="b39b2-130">Utwórz niestandardowy serwer DNS</span><span class="sxs-lookup"><span data-stu-id="b39b2-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b39b2-131">Należy utworzyć i skonfigurować serwer DNS, przed zainstalowaniem usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="b39b2-132">Do utworzenia maszyny Wirtualnej systemu Linux, który używa [powiązać](https://www.isc.org/downloads/bind/) oprogramowania DNS, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b39b2-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="b39b2-133">Następujące kroki użyj [portalu Azure](https://portal.azure.com) do utworzenia maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b39b2-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="b39b2-134">Aby uzyskać inne sposoby tworzenia maszyny wirtualnej, zobacz [Utwórz maszynę Wirtualną — interfejsu wiersza polecenia Azure](../virtual-machines/linux/quick-create-cli.md) i [Utwórz maszynę Wirtualną — program Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) dokumentów.</span><span class="sxs-lookup"><span data-stu-id="b39b2-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="b39b2-135">Z [portalu Azure](https://portal.azure.com), wybierz pozycję  __+__ , __obliczeniowe__, i __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Tworzenie maszyny wirtualnej systemu Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="b39b2-137">Z __podstawy__ sekcji, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b39b2-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="b39b2-138">__Nazwa__: przyjazną nazwę identyfikującą tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="b39b2-139">Na przykład __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="b39b2-140">__Nazwa użytkownika__: Nazwa konta SSH.</span><span class="sxs-lookup"><span data-stu-id="b39b2-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="b39b2-141">__Klucz publiczny SSH__ lub __hasło__: metodę uwierzytelniania dla konta SSH.</span><span class="sxs-lookup"><span data-stu-id="b39b2-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="b39b2-142">Zalecamy używanie kluczy publicznych, ponieważ są one bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="b39b2-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="b39b2-143">Aby uzyskać więcej informacji, zobacz [tworzenia i używania kluczy SSH dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="b39b2-144">__Grupa zasobów__: Wybierz __Użyj istniejącego__, a następnie wybierz grupę zasobów, która zawiera utworzony wcześniej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="b39b2-145">__Lokalizacja__: Wybierz z tej samej lokalizacji co sieć wirtualna.</span><span class="sxs-lookup"><span data-stu-id="b39b2-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Maszyny wirtualnej konfiguracji podstawowej](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="b39b2-147">Pozostaw innych pozycji na wartości domyślne, a następnie wybierz __OK__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="b39b2-148">Z __wybierz rozmiar__ wybierz rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="b39b2-149">W tym samouczku wybierz opcję najmniejszą i najniższy koszt.</span><span class="sxs-lookup"><span data-stu-id="b39b2-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="b39b2-150">Aby kontynuować, należy użyć __wybierz__ przycisku.</span><span class="sxs-lookup"><span data-stu-id="b39b2-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="b39b2-151">Z __ustawienia__ sekcji, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b39b2-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="b39b2-152">__Sieć wirtualna__: Wybierz sieć wirtualną, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="b39b2-153">__Podsieci__: Wybierz domyślną podsieć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="b39b2-154">Czy __nie__ wybierz w podsieci używanej przez bramę sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b39b2-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="b39b2-155">__Konto magazynu diagnostyki__: Wybierz istniejące konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="b39b2-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Ustawienia sieci wirtualnej](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="b39b2-157">Pozostaw wartość domyślną innych pozycji, a następnie wybierz __OK__ aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="b39b2-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="b39b2-158">Z __zakupu__ zaznacz __zakupu__ przycisk, aby utworzyć maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b39b2-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="b39b2-159">Po utworzeniu maszyny wirtualnej, jego __omówienie__ sekcja jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="b39b2-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="b39b2-160">Wybierz z listy po lewej stronie __właściwości__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="b39b2-161">Zapisz __publicznego adresu IP__ i __prywatny adres IP__ wartości.</span><span class="sxs-lookup"><span data-stu-id="b39b2-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="b39b2-162">Będzie używany w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b39b2-162">It will be used in the next section.</span></span>

    ![Publiczne i prywatne adresy IP](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="b39b2-164">Instalowanie i konfigurowanie Bind (oprogramowania DNS)</span><span class="sxs-lookup"><span data-stu-id="b39b2-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="b39b2-165">Używanie protokołu SSH do nawiązania połączenia __publicznego adresu IP__ maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="b39b2-166">Poniższy przykład nawiązuje połączenie z maszyną wirtualną na 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="b39b2-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="b39b2-167">Zastąp `sshuser` przy użyciu konta użytkownika SSH określone podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="b39b2-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b39b2-168">Istnieje wiele sposobów, aby uzyskać `ssh` narzędzia.</span><span class="sxs-lookup"><span data-stu-id="b39b2-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="b39b2-169">W systemie Linux, Unix i macOS jest podana jako część systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b39b2-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="b39b2-170">Jeśli korzystasz z systemu Windows, weź pod uwagę jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="b39b2-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="b39b2-171">Powłoka w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="b39b2-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="b39b2-172">Bash na Ubuntu w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="b39b2-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="b39b2-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="b39b2-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="b39b2-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="b39b2-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="b39b2-175">Aby zainstalować Bind, użyj następujących poleceń w sesji SSH:</span><span class="sxs-lookup"><span data-stu-id="b39b2-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="b39b2-176">Aby skonfigurować powiązania do przekazywania żądań rozpoznawania nazw do lokalnego serwera DNS, użyj następującego tekstu zawartość, `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="b39b2-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="b39b2-177">Zastąp wartości w `goodclients` sekcji z zakresem adresów IP sieci wirtualnej i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="b39b2-178">Ta sekcja definiuje adresów, które ten serwer DNS odbiera z.</span><span class="sxs-lookup"><span data-stu-id="b39b2-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="b39b2-179">Zastąp `192.168.0.1` wpis w `forwarders` sekcji przy użyciu adresu IP serwera DNS lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b39b2-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="b39b2-180">Ten wpis kieruje żądania DNS do lokalnego serwera DNS do rozpoznawania.</span><span class="sxs-lookup"><span data-stu-id="b39b2-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="b39b2-181">Aby edytować ten plik, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b39b2-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="b39b2-182">Aby zapisać plik, użyj __Ctrl + X__, __Y__, a następnie __Enter__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="b39b2-183">W sesji SSH Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b39b2-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="b39b2-184">To polecenie zwraca wartość podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b39b2-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="b39b2-185">`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` Tekst jest __sufiks DNS__ dla tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="b39b2-186">Zapisz tę wartość, ponieważ jest używana później.</span><span class="sxs-lookup"><span data-stu-id="b39b2-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="b39b2-187">Aby skonfigurować powiązania do rozpoznawania nazw DNS dla zasobów w sieci wirtualnej, użyj następującego tekstu jako zawartość `/etc/bind/named.conf.local` pliku:</span><span class="sxs-lookup"><span data-stu-id="b39b2-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="b39b2-188">Należy zastąpić `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` sufiksu DNS został wcześniej pobrany.</span><span class="sxs-lookup"><span data-stu-id="b39b2-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="b39b2-189">Aby edytować ten plik, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b39b2-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="b39b2-190">Aby zapisać plik, użyj __Ctrl + X__, __Y__, a następnie __Enter__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="b39b2-191">Aby uruchomić Bind, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b39b2-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="b39b2-192">Aby zweryfikować tego powiązania mogły rozpoznawać nazwy zasobów w sieci lokalnej, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="b39b2-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b39b2-193">Zastąp `dns.mynetwork.net` z w pełni kwalifikowaną nazwę (FQDN) zasobu w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="b39b2-194">Zastąp `10.0.0.4` z __wewnętrzny adres IP__ niestandardowego serwera DNS w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="b39b2-195">Odpowiedź jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="b39b2-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="b39b2-196">Skonfiguruj sieć wirtualną do używania niestandardowych serwera DNS</span><span class="sxs-lookup"><span data-stu-id="b39b2-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="b39b2-197">Aby skonfigurować sieci wirtualnej, aby użyć niestandardowego serwera DNS zamiast Azure cyklicznego programu rozpoznawania nazw, należy użyć następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b39b2-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="b39b2-198">W [portalu Azure](https://portal.azure.com), wybierz sieć wirtualną, a następnie wybierz __serwerów DNS__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="b39b2-199">Wybierz __niestandardowych__, a następnie wprowadź __wewnętrzny adres IP__ niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="b39b2-200">Na koniec wybierz __zapisać__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-200">Finally, select __Save__.</span></span>

    ![Ustaw niestandardowy serwer DNS w sieci](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="b39b2-202">Konfigurowanie lokalnego serwera DNS</span><span class="sxs-lookup"><span data-stu-id="b39b2-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="b39b2-203">W poprzedniej sekcji należy skonfigurować niestandardowy serwer DNS do przekazywania żądań do lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="b39b2-204">Następnie skonfiguruj lokalny serwer DNS do przekazywania żądań do niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="b39b2-205">Aby poznać konkretne kroki dotyczące sposobu konfigurowania serwera DNS zajrzyj do dokumentacji oprogramowania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="b39b2-206">Szukaj, aby uzyskać instrukcje dotyczące sposobu konfigurowania __warunkowego przesyłania dalej__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="b39b2-207">Warunkowe do przodu przekazuje tylko żądania dotyczące określonego sufiksu DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="b39b2-208">W takim przypadku należy skonfigurować usługę przesyłania dalej dla sufiksu DNS w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="b39b2-209">Adres IP serwera DNS, niestandardowe powinny zostać przekazane żądania dla tego sufiksu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="b39b2-210">Następujący tekst jest przykładem konfiguracji warunkowego przesyłania dalej dla **powiązać** oprogramowania DNS:</span><span class="sxs-lookup"><span data-stu-id="b39b2-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="b39b2-211">Aby uzyskać informacje dotyczące korzystania z systemu DNS **systemu Windows Server 2016**, zobacz [DnsServerConditionalForwarderZone Dodaj](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) dokumentacji...</span><span class="sxs-lookup"><span data-stu-id="b39b2-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="b39b2-212">Po skonfigurowaniu lokalnego serwera DNS, możesz użyć `nslookup` z sieci lokalnej, aby sprawdzić, czy można rozwiązać nazwy w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="b39b2-213">Poniższy przykład</span><span class="sxs-lookup"><span data-stu-id="b39b2-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="b39b2-214">W tym przykładzie używane lokalnego serwera DNS na 196.168.0.4 do rozpoznania nazwy niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="b39b2-215">Zamień adres IP dla lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="b39b2-216">Zastąp `dnsproxy` adresu z w pełni kwalifikowaną nazwę niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="b39b2-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="b39b2-217">Opcjonalne: Ruch sieciowy kontroli</span><span class="sxs-lookup"><span data-stu-id="b39b2-217">Optional: Control network traffic</span></span>

<span data-ttu-id="b39b2-218">Grupy zabezpieczeń sieci (NSG) lub trasy zdefiniowane przez użytkownika (przez) służy do kontroli ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b39b2-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="b39b2-219">Grupy NSG umożliwiają filtrowanie ruchu przychodzącego i wychodzącego, a akceptować lub odrzucać ruchu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="b39b2-220">Udr pozwala na kontrolowanie, jak przepływa ruch między zasobami w sieci wirtualnej, internet oraz sieć lokalną.</span><span class="sxs-lookup"><span data-stu-id="b39b2-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="b39b2-221">HDInsight wymaga dostępu ruchu przychodzącego z określonych adresów IP w chmurze Azure i nieograniczony dostęp ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="b39b2-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="b39b2-222">Za pomocą grup NSG lub Udr kontroli ruchu, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b39b2-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="b39b2-223">Znajdowanie adresów IP do lokalizacji zawierającej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="b39b2-224">Aby uzyskać listę wymaganych adresów IP według lokalizacji, zobacz [adresów IP wymagana](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="b39b2-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="b39b2-225">Zezwalaj na ruch przychodzący z adresów IP.</span><span class="sxs-lookup"><span data-stu-id="b39b2-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="b39b2-226">__Grupa NSG__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z __Internet__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="b39b2-227">__PRZEZ__: Ustaw __następnego przeskoku__ typu trasy do __Internet__.</span><span class="sxs-lookup"><span data-stu-id="b39b2-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="b39b2-228">Na przykład do tworzenia grup NSG za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure, zobacz [rozszerzenie usługi HDInsight za pomocą sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="b39b2-229">Tworzenie klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b39b2-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="b39b2-230">Niestandardowy serwer DNS należy skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="b39b2-231">Wykonaj kroki w [tworzenia klastra usługi HDInsight przy użyciu portalu Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) dokumentu, aby utworzyć klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b39b2-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="b39b2-232">Podczas tworzenia klastra musisz wybrać lokalizację, który zawiera sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="b39b2-233">W __Zaawansowane ustawienia__ część konfiguracji, należy wybrać sieć wirtualna i podsieć, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b39b2-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="b39b2-234">Nawiązywanie połączenia z usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b39b2-234">Connecting to HDInsight</span></span>

<span data-ttu-id="b39b2-235">Większość dokumentacji w usłudze HDInsight założono, że dostęp do klastra za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="b39b2-236">Na przykład czy możesz połączyć się z klastrem w https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="b39b2-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b39b2-237">Ten adres używa publicznego brama nie jest dostępna w przypadku użycia grup NSG lub Udr ograniczyć dostęp z Internetu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="b39b2-238">Bezpośrednio z usługi HDInsight za pośrednictwem sieci wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b39b2-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="b39b2-239">Aby odnaleźć wewnętrzny pełni kwalifikowane nazwy domen z węzłów klastra usługi HDInsight, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="b39b2-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="b39b2-240">Aby ustalić port, który usługa jest dostępna na, zobacz [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b39b2-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b39b2-241">Niektóre usługi hostowanej o węzłach głównych są tylko aktywne na jednym węźle naraz.</span><span class="sxs-lookup"><span data-stu-id="b39b2-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="b39b2-242">Jeśli nie powiedzie się próby uzyskiwania dostępu do usługi na jednym węźle głównym, Przełącz do innego węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="b39b2-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="b39b2-243">Na przykład Ambari jest tylko aktywna na jednym węźle głównym naraz.</span><span class="sxs-lookup"><span data-stu-id="b39b2-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="b39b2-244">Jeśli dostęp do narzędzia Ambari w jednym węźle głównym zwraca błąd 404, następnie uruchomiona w innym węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="b39b2-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b39b2-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b39b2-245">Next steps</span></span>

* <span data-ttu-id="b39b2-246">Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="b39b2-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="b39b2-247">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b39b2-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="b39b2-248">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="b39b2-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="b39b2-249">Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b39b2-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
