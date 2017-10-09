---
title: "sieć lokalną aaaConnect HDInsight tooyour - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toocreate HDInsight w sieci wirtualnej platformy Azure, a następnie podłącz je tooyour sieci lokalnej. Dowiedz się, jak tooconfigure rozpoznawanie nazw między HDInsight i siecią lokalną przy użyciu niestandardowego serwera DNS."
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
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="53038-104">Połączyć sieć lokalną tooyour HDInsight</span><span class="sxs-lookup"><span data-stu-id="53038-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="53038-105">Dowiedz się, jak tooconnect HDInsight tooyour lokalnej sieci przy użyciu sieci wirtualnych Azure i bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="53038-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="53038-106">Ten dokument zawiera informacje na temat planowania na:</span><span class="sxs-lookup"><span data-stu-id="53038-106">This document provides planning information on:</span></span>

* <span data-ttu-id="53038-107">Za pomocą usługi HDInsight w sieci wirtualnej Azure, który łączy tooyour lokalnej sieci.</span><span class="sxs-lookup"><span data-stu-id="53038-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="53038-108">Konfigurowanie rozpoznawania nazw DNS między hello sieci wirtualnej i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="53038-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="53038-109">Konfigurowanie sieci zabezpieczeń grupy toorestrict internet access tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="53038-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="53038-110">Porty dostarczanych z usługą HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="53038-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="53038-111">Tworzenie konfiguracji sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="53038-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53038-112">Jeśli szukasz wskazówki krok po kroku dotyczące łączenia HDInsight tooyour lokalnej sieci za pomocą sieci wirtualnej platformy Azure, zobacz hello [sieci lokalnej tooyour połączyć HDInsight](connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="53038-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="53038-113">Użyj następujących hello dokumentów toolearn jak toocreate sieci wirtualnej platformy Azure, który jest połączony tooyour lokalnej sieci:</span><span class="sxs-lookup"><span data-stu-id="53038-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="53038-114">Przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="53038-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="53038-115">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="53038-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="53038-116">Korzystanie z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="53038-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="53038-117">Konfigurowanie rozpoznawania nazw</span><span class="sxs-lookup"><span data-stu-id="53038-117">Configure name resolution</span></span>

<span data-ttu-id="53038-118">tooallow HDInsight i zasobów w hello przyłączone do sieci toocommunicate według nazwy, należy wykonać następujące akcje hello:</span><span class="sxs-lookup"><span data-stu-id="53038-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="53038-119">Utwórz niestandardowy serwer DNS w hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53038-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="53038-120">Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS zamiast domyślnego hello Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="53038-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="53038-121">Konfiguruj przekazywanie między hello niestandardowy serwer DNS i serwer DNS lokalnie.</span><span class="sxs-lookup"><span data-stu-id="53038-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="53038-122">Ta konfiguracja umożliwia hello następujące zachowanie:</span><span class="sxs-lookup"><span data-stu-id="53038-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="53038-123">Żądania dla nazwy FQDN, które mają sufiks DNS hello __dla sieci wirtualnej hello__ są przekazywane toohello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="53038-124">Hello niestandardowy serwer DNS przesyła te żądania toohello Azure cyklicznego programu rozpoznawania nazw, która zwraca hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="53038-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="53038-125">Wszystkie inne żądania są przekazywane toohello lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="53038-126">Nawet żądania publicznego zasobów internetowych, takich jak microsoft.com są przekazywane toohello serwera DNS lokalnego rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="53038-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="53038-127">W następujących diagram hello zielony wiersze są żądania zasobów kończącymi się sufiks DNS hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="53038-128">Niebieski wiersze są żądania dotyczące zasobów w sieci lokalnej hello lub na hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="53038-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagram przedstawiający sposób żądania DNS są rozpoznawane w konfiguracji hello używane w tym dokumencie](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="53038-130">Utwórz niestandardowy serwer DNS</span><span class="sxs-lookup"><span data-stu-id="53038-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53038-131">Należy utworzyć i skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="53038-132">toocreate maszyny Wirtualnej systemu Linux, który używa hello [powiązać](https://www.isc.org/downloads/bind/) oprogramowania DNS, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53038-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="53038-133">Witaj następujące kroki Użyj hello [portalu Azure](https://portal.azure.com) toocreate maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53038-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="53038-134">Dla innych sposobów toocreate maszyny wirtualnej, zobacz hello [Utwórz maszynę Wirtualną — interfejsu wiersza polecenia Azure](../virtual-machines/linux/quick-create-cli.md) i [Utwórz maszynę Wirtualną — program Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) dokumentów.</span><span class="sxs-lookup"><span data-stu-id="53038-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="53038-135">Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję  __+__ , __obliczeniowe__, i __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="53038-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Tworzenie maszyny wirtualnej systemu Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="53038-137">Z hello __podstawy__ wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="53038-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="53038-138">__Nazwa__: przyjazną nazwę identyfikującą tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="53038-139">Na przykład __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="53038-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="53038-140">__Nazwa użytkownika__: Nazwa hello hello konta SSH.</span><span class="sxs-lookup"><span data-stu-id="53038-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="53038-141">__Klucz publiczny SSH__ lub __hasło__: hello metodę uwierzytelniania dla hello konta SSH.</span><span class="sxs-lookup"><span data-stu-id="53038-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="53038-142">Zalecamy używanie kluczy publicznych, ponieważ są one bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="53038-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="53038-143">Aby uzyskać więcej informacji, zobacz hello [tworzenia i używania kluczy SSH dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="53038-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="53038-144">__Grupa zasobów__: Wybierz __Użyj istniejącego__, a następnie wybierz grupę zasobów hello, która zawiera hello sieci wirtualnej utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53038-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="53038-145">__Lokalizacja__: Wybierz hello tej samej lokalizacji co sieć wirtualna hello.</span><span class="sxs-lookup"><span data-stu-id="53038-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Maszyny wirtualnej konfiguracji podstawowej](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="53038-147">Pozostaw innych pozycji na powitania wartości domyślne, a następnie wybierz __OK__.</span><span class="sxs-lookup"><span data-stu-id="53038-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="53038-148">Z hello __wybierz rozmiar__ sekcji hello wybierz rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="53038-149">W tym samouczku wybierz hello najmniejszą i najniższy koszt opcji.</span><span class="sxs-lookup"><span data-stu-id="53038-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="53038-150">toocontinue, użyj hello __wybierz__ przycisku.</span><span class="sxs-lookup"><span data-stu-id="53038-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="53038-151">Z hello __ustawienia__ wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="53038-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="53038-152">__Sieć wirtualna__: Wybierz hello sieci wirtualnej, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53038-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="53038-153">__Podsieci__: Wybierz podsieć domyślne hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="53038-154">Czy __nie__ wybierz hello podsieci używanej przez bramę sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="53038-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="53038-155">__Konto magazynu diagnostyki__: Wybierz istniejące konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="53038-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Ustawienia sieci wirtualnej](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="53038-157">Pozostaw hello inne pozycje hello wartości domyślnej, a następnie wybierz __OK__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="53038-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="53038-158">Z hello __zakupu__ sekcji, wybierz hello __zakupu__ maszyny wirtualnej hello toocreate przycisku.</span><span class="sxs-lookup"><span data-stu-id="53038-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="53038-159">Po utworzeniu maszyny wirtualnej hello jego __omówienie__ sekcja jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="53038-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="53038-160">Wybierz z listy powitania po lewej stronie powitania __właściwości__.</span><span class="sxs-lookup"><span data-stu-id="53038-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="53038-161">Zapisz hello __publicznego adresu IP__ i __prywatny adres IP__ wartości.</span><span class="sxs-lookup"><span data-stu-id="53038-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="53038-162">Będzie używany w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="53038-162">It will be used in hello next section.</span></span>

    ![Publiczne i prywatne adresy IP](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="53038-164">Instalowanie i konfigurowanie Bind (oprogramowania DNS)</span><span class="sxs-lookup"><span data-stu-id="53038-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="53038-165">Użyj SSH tooconnect toohello __publicznego adresu IP__ hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="53038-166">Poniższy przykład Hello łączy tooa maszyny wirtualnej na 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="53038-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="53038-167">Zastąp `sshuser` z konta użytkownika SSH hello określone podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="53038-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53038-168">Istnieją różne sposoby tooobtain hello `ssh` narzędzia.</span><span class="sxs-lookup"><span data-stu-id="53038-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="53038-169">W systemie Linux, Unix i macOS jest podana jako część systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="53038-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="53038-170">Jeśli korzystasz z systemu Windows, weź pod uwagę jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="53038-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="53038-171">Powłoka w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="53038-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="53038-172">Bash na Ubuntu w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="53038-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="53038-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="53038-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="53038-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="53038-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="53038-175">tooinstall Bind, należy użyć następującego polecenia w sesji SSH hello hello:</span><span class="sxs-lookup"><span data-stu-id="53038-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="53038-176">tooconfigure Bind tooforward Nazwa rozwiązania żądań tooyour lokalnego serwera DNS, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="53038-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="53038-177">Zastąp wartości hello hello `goodclients` sekcji z zakresem adresów IP hello hello sieci wirtualnej i sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="53038-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="53038-178">Ta sekcja definiuje hello adresów, które ten serwer DNS odbiera z.</span><span class="sxs-lookup"><span data-stu-id="53038-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="53038-179">Zastąp hello `192.168.0.1` wpisu w hello `forwarders` sekcji z adresem IP hello lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="53038-180">Ten wpis trasy DNS żądań tooyour lokalnego serwera DNS do rozpoznawania.</span><span class="sxs-lookup"><span data-stu-id="53038-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="53038-181">tooedit tego pliku, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53038-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="53038-182">toosave hello pliku, użyj __Ctrl + X__, __Y__, a następnie __Enter__.</span><span class="sxs-lookup"><span data-stu-id="53038-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="53038-183">Hello sesji SSH używając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="53038-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="53038-184">To polecenie zwraca wartość toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="53038-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="53038-185">Witaj `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` tekst jest hello __sufiks DNS__ dla tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="53038-186">Zapisz tę wartość, ponieważ jest używana później.</span><span class="sxs-lookup"><span data-stu-id="53038-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="53038-187">nazwy DNS tooresolve tooconfigure powiązania dla zasobów w sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.local` pliku:</span><span class="sxs-lookup"><span data-stu-id="53038-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="53038-188">Należy zastąpić hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` sufiksu DNS hello pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53038-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="53038-189">tooedit tego pliku, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53038-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="53038-190">toosave hello pliku, użyj __Ctrl + X__, __Y__, a następnie __Enter__.</span><span class="sxs-lookup"><span data-stu-id="53038-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="53038-191">toostart Bind, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53038-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="53038-192">tooverify, który powiązać mogły rozpoznawać nazwy hello zasobów w sieci lokalnej, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="53038-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="53038-193">Zastąp `dns.mynetwork.net` z hello pełną nazwę domeny (FQDN) zasobu w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="53038-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="53038-194">Zastąp `10.0.0.4` z hello __wewnętrzny adres IP__ niestandardowego serwera DNS w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="53038-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="53038-195">odpowiedź Hello zostaną wyświetlone podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="53038-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="53038-196">Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS</span><span class="sxs-lookup"><span data-stu-id="53038-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="53038-197">tooconfigure hello sieci wirtualnej toouse hello niestandardowy serwer DNS zamiast hello Azure cyklicznego programu rozpoznawania nazw, należy użyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53038-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="53038-198">W hello [portalu Azure](https://portal.azure.com)wybierz hello sieci wirtualnej, a następnie wybierz __serwerów DNS__.</span><span class="sxs-lookup"><span data-stu-id="53038-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="53038-199">Wybierz __niestandardowych__i wprowadź hello __wewnętrzny adres IP__ hello niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="53038-200">Na koniec wybierz __zapisać__.</span><span class="sxs-lookup"><span data-stu-id="53038-200">Finally, select __Save__.</span></span>

    ![Ustaw hello niestandardowy serwer DNS dla sieci hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="53038-202">Konfigurowanie serwera DNS lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="53038-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="53038-203">W poprzedniej sekcji hello należy skonfigurować hello niestandardowe DNS serwera tooforward żądań toohello lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="53038-204">Następnie należy skonfigurować hello lokalnego serwera tooforward żądań toohello niestandardowe DNS serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="53038-205">Aby poznać konkretne kroki dotyczące tooconfigure serwera DNS, hello w dokumentacji oprogramowania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="53038-206">Wyszukaj hello kroki dotyczące tooconfigure __warunkowego przesyłania dalej__.</span><span class="sxs-lookup"><span data-stu-id="53038-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="53038-207">Warunkowe do przodu przekazuje tylko żądania dotyczące określonego sufiksu DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="53038-208">W takim przypadku należy skonfigurować usługę przesyłania dalej dla sufiksu DNS hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="53038-209">Żądania dla tego sufiksu, powinny zostać przekazane toohello adres IP hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="53038-210">Witaj następujący tekst jest przykładem konfiguracji warunkowego przesyłania dalej dla hello **powiązać** oprogramowania DNS:</span><span class="sxs-lookup"><span data-stu-id="53038-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="53038-211">Aby uzyskać informacje dotyczące korzystania z systemu DNS **systemu Windows Server 2016**, zobacz hello [DnsServerConditionalForwarderZone Dodaj](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) dokumentacji...</span><span class="sxs-lookup"><span data-stu-id="53038-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="53038-212">Po skonfigurowaniu hello lokalnego serwera DNS, możesz użyć `nslookup` z tooverify sieci lokalne powitania czy można rozwiązać nazwy w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="53038-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="53038-213">Poniższy przykład Hello</span><span class="sxs-lookup"><span data-stu-id="53038-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="53038-214">W tym przykładzie używa hello lokalnego serwera DNS na 196.168.0.4 tooresolve nazwę hello hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="53038-215">Zamień adres IP hello hello jednego serwera DNS lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="53038-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="53038-216">Zastąp hello `dnsproxy` adres z nazwą FQDN hello hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="53038-217">Opcjonalne: Ruch sieciowy kontroli</span><span class="sxs-lookup"><span data-stu-id="53038-217">Optional: Control network traffic</span></span>

<span data-ttu-id="53038-218">Możesz użyć grup zabezpieczeń sieci (NSG) lub ruchu sieciowego toocontrol trasy zdefiniowane przez użytkownika (przez).</span><span class="sxs-lookup"><span data-stu-id="53038-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="53038-219">Grupy NSG można toofilter przychodzący i wychodzący ruch sieciowy i akceptować lub odrzucać hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="53038-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="53038-220">Udr pozwalają toocontrol jak przepływa ruch między zasobami w sieci wirtualnej hello hello internet i hello sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="53038-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="53038-221">HDInsight wymaga dostępu ruchu przychodzącego z określonych adresów IP w hello chmury Azure i nieograniczony dostęp ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="53038-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="53038-222">Podczas korzystania z grup NSG lub Udr toocontrol ruchu, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53038-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="53038-223">Znajdź hello adresów IP dla lokalizacji hello, który zawiera sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="53038-224">Aby uzyskać listę wymaganych adresów IP według lokalizacji, zobacz [adresów IP wymagana](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="53038-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="53038-225">Zezwalaj na ruch przychodzący z hello adresów IP.</span><span class="sxs-lookup"><span data-stu-id="53038-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="53038-226">__Grupa NSG__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z hello __Internet__.</span><span class="sxs-lookup"><span data-stu-id="53038-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="53038-227">__PRZEZ__: hello zestaw __następnego przeskoku__ typu hello too__Internet__ trasy.</span><span class="sxs-lookup"><span data-stu-id="53038-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="53038-228">Na przykład przy użyciu programu Azure PowerShell lub hello Azure CLI toocreate grup NSG, zobacz hello [rozszerzenie usługi HDInsight za pomocą sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="53038-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="53038-229">Tworzenie klastra usługi HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="53038-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="53038-230">Należy skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="53038-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="53038-231">Użyj hello etapami hello [tworzenia klastra usługi HDInsight przy użyciu portalu Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate dokument klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="53038-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="53038-232">Podczas tworzenia klastra musisz wybrać lokalizację hello, który zawiera sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53038-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="53038-233">W hello __Zaawansowane ustawienia__ część konfiguracji, należy wybrać hello sieć wirtualna i podsieć, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="53038-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="53038-234">Łączenie tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="53038-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="53038-235">Większość dokumentacji w usłudze HDInsight założono, że klaster toohello dostęp za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="53038-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="53038-236">Na przykład, że możesz połączyć https://CLUSTERNAME.azurehdinsight.net toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="53038-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="53038-237">Ten adres używa hello publicznego bramy, która nie jest dostępna, jeśli używasz grup NSG lub Udr toorestrict dostęp z hello internet.</span><span class="sxs-lookup"><span data-stu-id="53038-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="53038-238">toodirectly łączenie się tooHDInsight za pośrednictwem sieci wirtualnej hello, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53038-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="53038-239">toodiscover hello wewnętrzny pełni kwalifikowane nazwy domen hello węzłów klastra usługi HDInsight, użyj jednej z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="53038-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

2. <span data-ttu-id="53038-240">toodetermine hello port, który usługa jest dostępna, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="53038-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="53038-241">Niektórych usług hostowanych na węzłach głównych hello są tylko aktywne na jednym węźle naraz.</span><span class="sxs-lookup"><span data-stu-id="53038-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="53038-242">Jeśli nie powiedzie się próby uzyskiwania dostępu do usługi na jednym węźle głównym, Przełącz toohello innych węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="53038-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="53038-243">Na przykład Ambari jest tylko aktywna na jednym węźle głównym naraz.</span><span class="sxs-lookup"><span data-stu-id="53038-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="53038-244">Jeśli dostęp do narzędzia Ambari w jednym węźle głównym zwraca błąd 404, a następnie jest uruchomiona na hello innych węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="53038-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53038-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53038-245">Next steps</span></span>

* <span data-ttu-id="53038-246">Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="53038-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="53038-247">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz hello [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53038-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="53038-248">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="53038-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="53038-249">Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53038-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
