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
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Połączyć sieć lokalną tooyour HDInsight

Dowiedz się, jak tooconnect HDInsight tooyour lokalnej sieci przy użyciu sieci wirtualnych Azure i bramy sieci VPN. Ten dokument zawiera informacje na temat planowania na:

* Za pomocą usługi HDInsight w sieci wirtualnej Azure, który łączy tooyour lokalnej sieci.

* Konfigurowanie rozpoznawania nazw DNS między hello sieci wirtualnej i sieci lokalnej.

* Konfigurowanie sieci zabezpieczeń grupy toorestrict internet access tooHDInsight.

* Porty dostarczanych z usługą HDInsight w sieci wirtualnej hello.

## <a name="create-hello-virtual-network-configuration"></a>Tworzenie konfiguracji sieci wirtualnej hello

> [!IMPORTANT]
> Jeśli szukasz wskazówki krok po kroku dotyczące łączenia HDInsight tooyour lokalnej sieci za pomocą sieci wirtualnej platformy Azure, zobacz hello [sieci lokalnej tooyour połączyć HDInsight](connect-on-premises-network.md) dokumentu.

Użyj następujących hello dokumentów toolearn jak toocreate sieci wirtualnej platformy Azure, który jest połączony tooyour lokalnej sieci:
    
* [Przy użyciu hello portalu Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Korzystanie z programu Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Korzystanie z interfejsu wiersza polecenia platformy Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Konfigurowanie rozpoznawania nazw

tooallow HDInsight i zasobów w hello przyłączone do sieci toocommunicate według nazwy, należy wykonać następujące akcje hello:

* Utwórz niestandardowy serwer DNS w hello sieci wirtualnej platformy Azure.

* Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS zamiast domyślnego hello Azure cyklicznego programu rozpoznawania nazw.

* Konfiguruj przekazywanie między hello niestandardowy serwer DNS i serwer DNS lokalnie.

Ta konfiguracja umożliwia hello następujące zachowanie:

* Żądania dla nazwy FQDN, które mają sufiks DNS hello __dla sieci wirtualnej hello__ są przekazywane toohello niestandardowy serwer DNS. Hello niestandardowy serwer DNS przesyła te żądania toohello Azure cyklicznego programu rozpoznawania nazw, która zwraca hello adresu IP.

* Wszystkie inne żądania są przekazywane toohello lokalnego serwera DNS. Nawet żądania publicznego zasobów internetowych, takich jak microsoft.com są przekazywane toohello serwera DNS lokalnego rozpoznawania nazw.

W następujących diagram hello zielony wiersze są żądania zasobów kończącymi się sufiks DNS hello hello sieci wirtualnej. Niebieski wiersze są żądania dotyczące zasobów w sieci lokalnej hello lub na hello publicznej sieci internet.

![Diagram przedstawiający sposób żądania DNS są rozpoznawane w konfiguracji hello używane w tym dokumencie](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Utwórz niestandardowy serwer DNS

> [!IMPORTANT]
> Należy utworzyć i skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello powitania serwera DNS.

toocreate maszyny Wirtualnej systemu Linux, który używa hello [powiązać](https://www.isc.org/downloads/bind/) oprogramowania DNS, użyj hello następujące kroki:

> [!NOTE]
> Witaj następujące kroki Użyj hello [portalu Azure](https://portal.azure.com) toocreate maszyny wirtualnej platformy Azure. Dla innych sposobów toocreate maszyny wirtualnej, zobacz hello [Utwórz maszynę Wirtualną — interfejsu wiersza polecenia Azure](../virtual-machines/linux/quick-create-cli.md) i [Utwórz maszynę Wirtualną — program Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) dokumentów.

1. Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję  __+__ , __obliczeniowe__, i __Ubuntu Server 16.04 LTS__.

    ![Tworzenie maszyny wirtualnej systemu Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Z hello __podstawy__ wprowadź hello następujących informacji:

    * __Nazwa__: przyjazną nazwę identyfikującą tej maszyny wirtualnej. Na przykład __DNSProxy__.
    * __Nazwa użytkownika__: Nazwa hello hello konta SSH.
    * __Klucz publiczny SSH__ lub __hasło__: hello metodę uwierzytelniania dla hello konta SSH. Zalecamy używanie kluczy publicznych, ponieważ są one bardziej bezpieczne. Aby uzyskać więcej informacji, zobacz hello [tworzenia i używania kluczy SSH dla maszyn wirtualnych systemu Linux](../virtual-machines/linux/mac-create-ssh-keys.md) dokumentu.
    * __Grupa zasobów__: Wybierz __Użyj istniejącego__, a następnie wybierz grupę zasobów hello, która zawiera hello sieci wirtualnej utworzonej wcześniej.
    * __Lokalizacja__: Wybierz hello tej samej lokalizacji co sieć wirtualna hello.

    ![Maszyny wirtualnej konfiguracji podstawowej](./media/connect-on-premises-network/vm-basics.png)

    Pozostaw innych pozycji na powitania wartości domyślne, a następnie wybierz __OK__.

3. Z hello __wybierz rozmiar__ sekcji hello wybierz rozmiar maszyny Wirtualnej. W tym samouczku wybierz hello najmniejszą i najniższy koszt opcji. toocontinue, użyj hello __wybierz__ przycisku.

4. Z hello __ustawienia__ wprowadź hello następujących informacji:

    * __Sieć wirtualna__: Wybierz hello sieci wirtualnej, który został utworzony wcześniej.

    * __Podsieci__: Wybierz podsieć domyślne hello hello sieci wirtualnej. Czy __nie__ wybierz hello podsieci używanej przez bramę sieci VPN hello.

    * __Konto magazynu diagnostyki__: Wybierz istniejące konto magazynu lub Utwórz nową.

    ![Ustawienia sieci wirtualnej](./media/connect-on-premises-network/virtual-network-settings.png)

    Pozostaw hello inne pozycje hello wartości domyślnej, a następnie wybierz __OK__ toocontinue.

5. Z hello __zakupu__ sekcji, wybierz hello __zakupu__ maszyny wirtualnej hello toocreate przycisku.

6. Po utworzeniu maszyny wirtualnej hello jego __omówienie__ sekcja jest wyświetlana. Wybierz z listy powitania po lewej stronie powitania __właściwości__. Zapisz hello __publicznego adresu IP__ i __prywatny adres IP__ wartości. Będzie używany w następnej sekcji hello.

    ![Publiczne i prywatne adresy IP](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Instalowanie i konfigurowanie Bind (oprogramowania DNS)

1. Użyj SSH tooconnect toohello __publicznego adresu IP__ hello maszyny wirtualnej. Poniższy przykład Hello łączy tooa maszyny wirtualnej na 40.68.254.142:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Zastąp `sshuser` z konta użytkownika SSH hello określone podczas tworzenia klastra hello.

    > [!NOTE]
    > Istnieją różne sposoby tooobtain hello `ssh` narzędzia. W systemie Linux, Unix i macOS jest podana jako część systemu operacyjnego hello. Jeśli korzystasz z systemu Windows, weź pod uwagę jedną z hello następujące opcje:
    >
    > * [Powłoka w chmurze Azure](../cloud-shell/quickstart.md)
    > * [Bash na Ubuntu w systemie Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall Bind, należy użyć następującego polecenia w sesji SSH hello hello:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure Bind tooforward Nazwa rozwiązania żądań tooyour lokalnego serwera DNS, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:

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
    > Zastąp wartości hello hello `goodclients` sekcji z zakresem adresów IP hello hello sieci wirtualnej i sieci lokalnej. Ta sekcja definiuje hello adresów, które ten serwer DNS odbiera z.
    >
    > Zastąp hello `192.168.0.1` wpisu w hello `forwarders` sekcji z adresem IP hello lokalnego serwera DNS. Ten wpis trasy DNS żądań tooyour lokalnego serwera DNS do rozpoznawania.

    tooedit tego pliku, hello Użyj następującego polecenia:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    toosave hello pliku, użyj __Ctrl + X__, __Y__, a następnie __Enter__.

4. Hello sesji SSH używając hello następujące polecenie:

    ```bash
    hostname -f
    ```

    To polecenie zwraca wartość toohello podobne, następującego tekstu:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Witaj `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` tekst jest hello __sufiks DNS__ dla tej sieci wirtualnej. Zapisz tę wartość, ponieważ jest używana później.

5. nazwy DNS tooresolve tooconfigure powiązania dla zasobów w sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.local` pliku:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Należy zastąpić hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` sufiksu DNS hello pobranym wcześniej.

    tooedit tego pliku, hello Użyj następującego polecenia:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    toosave hello pliku, użyj __Ctrl + X__, __Y__, a następnie __Enter__.

6. toostart Bind, hello Użyj następującego polecenia:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify, który powiązać mogły rozpoznawać nazwy hello zasobów w sieci lokalnej, hello Użyj następującego polecenia:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Zastąp `dns.mynetwork.net` z hello pełną nazwę domeny (FQDN) zasobu w sieci lokalnej.
    >
    > Zastąp `10.0.0.4` z hello __wewnętrzny adres IP__ niestandardowego serwera DNS w sieci wirtualnej hello.

    odpowiedź Hello zostaną wyświetlone podobne toohello następującego tekstu:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS

tooconfigure hello sieci wirtualnej toouse hello niestandardowy serwer DNS zamiast hello Azure cyklicznego programu rozpoznawania nazw, należy użyć hello następujące kroki:

1. W hello [portalu Azure](https://portal.azure.com)wybierz hello sieci wirtualnej, a następnie wybierz __serwerów DNS__.

2. Wybierz __niestandardowych__i wprowadź hello __wewnętrzny adres IP__ hello niestandardowego serwera DNS. Na koniec wybierz __zapisać__.

    ![Ustaw hello niestandardowy serwer DNS dla sieci hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Konfigurowanie serwera DNS lokalne powitania

W poprzedniej sekcji hello należy skonfigurować hello niestandardowe DNS serwera tooforward żądań toohello lokalnego serwera DNS. Następnie należy skonfigurować hello lokalnego serwera tooforward żądań toohello niestandardowe DNS serwera DNS.

Aby poznać konkretne kroki dotyczące tooconfigure serwera DNS, hello w dokumentacji oprogramowania serwera DNS. Wyszukaj hello kroki dotyczące tooconfigure __warunkowego przesyłania dalej__.

Warunkowe do przodu przekazuje tylko żądania dotyczące określonego sufiksu DNS. W takim przypadku należy skonfigurować usługę przesyłania dalej dla sufiksu DNS hello hello sieci wirtualnej. Żądania dla tego sufiksu, powinny zostać przekazane toohello adres IP hello niestandardowy serwer DNS. 

Witaj następujący tekst jest przykładem konfiguracji warunkowego przesyłania dalej dla hello **powiązać** oprogramowania DNS:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Aby uzyskać informacje dotyczące korzystania z systemu DNS **systemu Windows Server 2016**, zobacz hello [DnsServerConditionalForwarderZone Dodaj](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) dokumentacji...

Po skonfigurowaniu hello lokalnego serwera DNS, możesz użyć `nslookup` z tooverify sieci lokalne powitania czy można rozwiązać nazwy w sieci wirtualnej hello. Poniższy przykład Hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

W tym przykładzie używa hello lokalnego serwera DNS na 196.168.0.4 tooresolve nazwę hello hello niestandardowy serwer DNS. Zamień adres IP hello hello jednego serwera DNS lokalne powitania. Zastąp hello `dnsproxy` adres z nazwą FQDN hello hello niestandardowy serwer DNS.

## <a name="optional-control-network-traffic"></a>Opcjonalne: Ruch sieciowy kontroli

Możesz użyć grup zabezpieczeń sieci (NSG) lub ruchu sieciowego toocontrol trasy zdefiniowane przez użytkownika (przez). Grupy NSG można toofilter przychodzący i wychodzący ruch sieciowy i akceptować lub odrzucać hello ruchu. Udr pozwalają toocontrol jak przepływa ruch między zasobami w sieci wirtualnej hello hello internet i hello sieci lokalnej.

> [!WARNING]
> HDInsight wymaga dostępu ruchu przychodzącego z określonych adresów IP w hello chmury Azure i nieograniczony dostęp ruchu wychodzącego. Podczas korzystania z grup NSG lub Udr toocontrol ruchu, należy wykonać hello następujące kroki:
>
> 1. Znajdź hello adresów IP dla lokalizacji hello, który zawiera sieci wirtualnej. Aby uzyskać listę wymaganych adresów IP według lokalizacji, zobacz [adresów IP wymagana](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Zezwalaj na ruch przychodzący z hello adresów IP.
>
>    * __Grupa NSG__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z hello __Internet__.
>    * __PRZEZ__: hello zestaw __następnego przeskoku__ typu hello too__Internet__ trasy.

Na przykład przy użyciu programu Azure PowerShell lub hello Azure CLI toocreate grup NSG, zobacz hello [rozszerzenie usługi HDInsight za pomocą sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) dokumentu.

## <a name="create-hello-hdinsight-cluster"></a>Tworzenie klastra usługi HDInsight hello

> [!WARNING]
> Należy skonfigurować przed zainstalowaniem usługi HDInsight w sieci wirtualnej hello hello niestandardowy serwer DNS.

Użyj hello etapami hello [tworzenia klastra usługi HDInsight przy użyciu portalu Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate dokument klastra usługi HDInsight.

> [!WARNING]
> * Podczas tworzenia klastra musisz wybrać lokalizację hello, który zawiera sieci wirtualnej.
>
> * W hello __Zaawansowane ustawienia__ część konfiguracji, należy wybrać hello sieć wirtualna i podsieć, który został utworzony wcześniej.

## <a name="connecting-toohdinsight"></a>Łączenie tooHDInsight

Większość dokumentacji w usłudze HDInsight założono, że klaster toohello dostęp za pośrednictwem hello internet. Na przykład, że możesz połączyć https://CLUSTERNAME.azurehdinsight.net toohello klastra. Ten adres używa hello publicznego bramy, która nie jest dostępna, jeśli używasz grup NSG lub Udr toorestrict dostęp z hello internet.

toodirectly łączenie się tooHDInsight za pośrednictwem sieci wirtualnej hello, użyj hello następujące kroki:

1. toodiscover hello wewnętrzny pełni kwalifikowane nazwy domen hello węzłów klastra usługi HDInsight, użyj jednej z hello następujące metody:

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

2. toodetermine hello port, który usługa jest dostępna, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.

    > [!IMPORTANT]
    > Niektórych usług hostowanych na węzłach głównych hello są tylko aktywne na jednym węźle naraz. Jeśli nie powiedzie się próby uzyskiwania dostępu do usługi na jednym węźle głównym, Przełącz toohello innych węzła głównego.
    >
    > Na przykład Ambari jest tylko aktywna na jednym węźle głównym naraz. Jeśli dostęp do narzędzia Ambari w jednym węźle głównym zwraca błąd 404, a następnie jest uruchomiona na hello innych węzła głównego.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz hello [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).

* Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).

* Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).
