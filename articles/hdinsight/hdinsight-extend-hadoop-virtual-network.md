---
title: "aaaExtend HDInsight z siecią wirtualną - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse sieci wirtualnej Azure tooconnect HDInsight tooother chmury zasobów lub zasobów w centrum danych."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure

Dowiedz się, jak toouse HDInsight z [sieci wirtualnej Azure](../virtual-network/virtual-networks-overview.md). Przy użyciu sieci wirtualnej platformy Azure umożliwia hello następujące scenariusze:

* Łączenie tooHDInsight bezpośrednio z sieci lokalnej.

* Łączenie HDInsight toodata są przechowywane w sieci wirtualnej platformy Azure.

* Bezpośrednio dostęp do usług Hadoop, które nie są dostępne publicznie ponad hello internet. Na przykład interfejsy API Kafka lub hello interfejsu API języka Java HBase.

> [!WARNING]
> Witaj informacje w tym dokumencie wymaga zrozumienia sieci TCP/IP. Jeśli nie masz doświadczenia z TCP/IP w sieci, należy partnera z osobą, która jest przed wprowadzeniem modyfikacji tooproduction sieci.

## <a name="planning"></a>Planowanie

Oto Hello hello pytania, na które należy odpowiedzieć przy planowaniu tooinstall HDInsight w sieci wirtualnej:

* Potrzebujesz tooinstall HDInsight do istniejącej sieci wirtualnej? Lub w przypadku tworzenia nowej sieci?

    Jeśli korzystasz z istniejącej sieci wirtualnej, może być konieczne konfiguracji sieci hello toomodify przed zainstalowaniem usługi HDInsight. Aby uzyskać więcej informacji, zobacz hello [Dodaj istniejącej sieci wirtualnej HDInsight tooan](#existingvnet) sekcji.

* Czy chcesz tooconnect hello sieci wirtualnej zawierający sieci wirtualnej tooanother HDInsight lub sieci lokalnej?

    tooeasily pracy z zasobami w sieciach, należy może toocreate niestandardowe DNS i skonfigurować przesyłania dalej DNS. Aby uzyskać więcej informacji, zobacz hello [łączenie wielu sieci](#multinet) sekcji.

* Czy chcesz toorestrict/przekierowanie ruchu przychodzącego i wychodzącego tooHDInsight?

    HDInsight musi mieć nieograniczony komunikację z określonych adresów IP w centrum danych Azure hello. Istnieje kilka portów, które może do komunikacji z klientem za pośrednictwem zapór. Aby uzyskać więcej informacji, zobacz hello [kontrolowanie ruchu w sieci](#networktraffic) sekcji.

## <a id="existingvnet"></a>Dodaj HDInsight tooan istniejącej sieci wirtualnej

Wykonaj kroki hello w tej sekcji toodiscover jak tooadd nowe tooan HDInsight istniejącej sieci wirtualnej platformy Azure.

> [!NOTE]
> Nie można dodać istniejącego klastra usługi HDInsight w sieci wirtualnej.

1. Dla sieci wirtualnej hello jest używany klasyczny lub modelu wdrażania usługi Resource Manager?

    HDInsight 3.4 i większa wymaga sieci wirtualnej Menedżera zasobów. Wcześniejszych wersji usługi hdinsight wymagane klasycznej sieci wirtualnej.

    Istniejącej sieci w przypadku klasycznych sieci wirtualnej, należy utworzyć sieć wirtualną Resource Manager a następnie połącz hello dwa. [Łączenie klasycznych sieci wirtualnych toonew sieci wirtualnych](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Po dołączone do usługi HDInsight w sieci usługi Resource Manager hello mogą współdziałać z zasobów w sieci klasycznego hello.

2. Należy używać tunelowania wymuszonego? Wymuszanie tunelowania jest ustawienia podsieci, wymuszający wychodzącego Internet ruchu tooa urządzenia do inspekcji i rejestrowania. HDInsight nie obsługuje wymuszanie tunelowania. Usuń wymuszanie tunelowania przed zainstalowaniem usługi HDInsight do podsieci albo utwórz nową podsieć dla usługi HDInsight.

3. Używasz grup zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub urządzenia sieci wirtualne toorestrict ruchu do lub z sieci wirtualnej hello?

    Jako zarządzanej usługi HDInsight wymaga adresów IP tooseveral nieograniczonego dostępu w centrum danych Azure hello. tooallow komunikacji z tych adresów IP, zaktualizuj żadnych istniejących grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika.

    HDInsight obsługuje wielu usług, które korzystają z różnych portów. Nie należy blokować ruchu toothese portów. Lista portów tooallow przez urządzenie wirtualne zapory, zobacz hello [zabezpieczeń](#security) sekcji.

    toofind istniejącej konfiguracji zabezpieczeń, hello Użyj następującego polecenia programu Azure PowerShell lub interfejsu wiersza polecenia Azure:

    * Grupy zabezpieczeń sieci

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) dokumentu.

        > [!IMPORTANT]
        > Reguły grupy zabezpieczeń sieci są stosowane w kolejności, w oparciu o priorytet reguły. Hello pierwszy pasujący wzorzec ruchu hello dotyczy reguła, a nie inne są stosowane dla tego ruchu. Kolejność reguł z najbardziej ograniczająca tooleast ograniczająca. Aby uzyskać więcej informacji, zobacz hello [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.

    * Trasy definiowane przez użytkownika

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z tras](../virtual-network/virtual-network-routes-troubleshoot-portal.md) dokumentu.

4. Tworzenie klastra usługi HDInsight i wybierz hello Azure Virtual Network podczas konfiguracji. Wykonaj kroki hello w hello następującego procesu tworzenia klastra hello toounderstand dokumentów:

    * [Tworzenie usługi HDInsight przy użyciu hello portalu Azure](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Create HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) (Tworzenie klastrów usługi HDInsight przy użyciu programu Azure PowerShell)
    * [Tworzenie usługi HDInsight przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Tworzenie usługi HDInsight przy użyciu szablonu usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Dodawanie HDInsight tooa sieci wirtualnej jest to krok konfiguracji opcjonalnej. Należy się, że sieć wirtualna hello tooselect podczas konfigurowania klastra hello.

## <a id="multinet"></a>Łączenie wielu sieci

Hello największych wyzwań z konfiguracji usługi sieciowej jest rozpoznawania nazw między sieciami hello.

Platforma Azure udostępnia rozpoznawanie nazw dla usług Azure, które są zainstalowane w sieci wirtualnej. To rozwiązanie nazwa wbudowanego umożliwia toohello tooconnect HDInsight następujące zasoby przy użyciu w pełni kwalifikowaną nazwą domeny (FQDN):

* Dowolnego zasobu, który jest dostępny w hello internet. Na przykład microsoft.com, google.com.

* Dowolnego zasobu, który jest w hello tej samej sieci wirtualnej Azure, używając hello __wewnętrzna nazwa DNS__ hello zasobu. Na przykład podczas rozpoznawania nazwy domyślnej hello hello poniżej przedstawiono przykład wewnętrzny DNS nazwy przypisanej tooHDInsight węzłów procesu roboczego:

    * wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Oba te węzły mogą komunikować się bezpośrednio ze sobą oraz inne węzły w usłudze HDInsight, za pomocą wewnętrznej nazwy DNS.

rozpoznawanie nazw domyślne Hello jest __nie__ Zezwalaj HDInsight tooresolve hello nazw zasobów w sieci, które są przyłączone do toohello sieci wirtualnej. Na przykład jest typowe toojoin toohello sieci wirtualnej sieci lokalnej. Z tylko hello domyślne rozpoznawania nazw HDInsight nie może uzyskiwać dostęp do zasobów w sieci lokalnej hello według nazwy. Witaj przeciwną również ma wartość true, zasobów w sieci lokalnej nie może uzyskać dostęp do zasobów w sieci wirtualnej hello według nazwy.

> [!WARNING]
> Należy utworzyć hello niestandardowy serwer DNS i skonfigurować toouse sieci wirtualnej hello hello go przed utworzeniem klastra usługi HDInsight.

rozpoznawanie nazw tooenable między zasobami w przyłączone do sieci i hello sieci wirtualnej, należy wykonać hello następujące akcje:

1. Utwórz niestandardowy serwer DNS w sieci wirtualnej platformy Azure, w którym planujesz tooinstall HDInsight hello.

2. Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS.

3. Znajdź hello Azure przypisać sufiksu DNS dla sieci wirtualnej. Ta wartość jest zbyt podobne`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Aby uzyskać informacje o hello sufiks DNS, zobacz hello [przykład: niestandardowe DNS](#example-dns) sekcji.

4. Konfiguruj przekazywanie między serwerami DNS hello. Konfiguracja Hello zależy od typu hello sieci zdalnej.

    * W przypadku sieci zdalnej hello sieci lokalnej, konfigurowanie systemu DNS w następujący sposób:
        
        * __Niestandardowe DNS__ (w sieci wirtualnej hello):

            * Przesyłania żądań dla sufiksu DNS hello hello sieci wirtualnej toohello Azure cyklicznego programu rozpoznawania nazw (168.63.129.16). Azure obsługuje żądania zasobów w sieci wirtualnej hello

            * Przekazuj wszystkie inne żądania toohello lokalnego serwera DNS. Witaj w lokalnym DNS obsługuje wszystkie inne żądania dotyczące rozpoznawania nazw, nawet żądania zasobów internetowych, takich jak Microsoft.com.

        * __DNS lokalnymi__: przekazywania żądań hello sieci wirtualnej sufiks toohello niestandardowe DNS serwera DNS. Witaj niestandardowy serwer DNS przekazuje następnie toohello Azure cyklicznego programu rozpoznawania nazw.

        Tej konfiguracji żądania trasy dla w pełni kwalifikowana nazwy domeny, które zawierają hello sufiks DNS hello sieci wirtualnej toohello niestandardowy serwer DNS. Wszystkie żądania (nawet w przypadku publicznych adresów internetowych) są obsługiwane przez serwer DNS lokalne powitania.

    * W przypadku sieci zdalnej hello innej sieci wirtualnej platformy Azure, konfigurowanie systemu DNS w następujący sposób:

        * __Niestandardowe DNS__ (w każdej sieci wirtualnej):

            * Żądania dla sufiksu DNS hello hello sieci wirtualnych są przesyłane dalej toohello niestandardowych serwerów DNS. Witaj DNS w każdej sieci wirtualnej jest odpowiedzialny za rozpoznawania zasobów w sieci.

            * Przekazuj wszystkie inne żądania toohello Azure cyklicznego programu rozpoznawania nazw. Witaj cyklicznego programu rozpoznawania nazw jest odpowiedzialny za rozwiązania lokalnego i zasobów w Internecie.

        powitania serwera DNS dla każdej sieci przekazuje żądania toohello innych, oparte na sufiks DNS. Inne żądania są rozpoznawane przy użyciu hello Azure cyklicznego programu rozpoznawania nazw.

    Na przykład każdej konfiguracji zobacz hello [przykład: niestandardowe DNS](#example-dns) sekcji.

Aby uzyskać więcej informacji, zobacz hello [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) dokumentu.

## <a name="directly-connect-toohadoop-services"></a>Bezpośrednie połączenie usługi tooHadoop

Większość dokumentacji w usłudze HDInsight założono, że klaster toohello dostęp za pośrednictwem hello internet. Na przykład, że możesz połączyć https://CLUSTERNAME.azurehdinsight.net toohello klastra. Ten adres używa hello publicznego bramy, która nie jest dostępna, jeśli używasz grup NSG lub Udr toorestrict dostęp z hello internet.

tooconnect tooAmbari i stron sieci web za pośrednictwem hello sieci wirtualnej, użyj hello następujące kroki:

1. toodiscover hello wewnętrzny pełni kwalifikowanych nazw domen (FQDN) węzły klastra usługi HDInsight hello, użyj jednej z hello następujące metody:

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

    Liście hello węzłów zwrócił Znajdź hello nazwy FQDN dla hello węzłów głównych i użyj hello nazw FQDN tooconnect tooAmbari i innych usług sieci web. Na przykład użyć `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Niektórych usług hostowanych na węzłach głównych hello są tylko aktywne na jednym węźle naraz. Jeśli spróbujesz uzyskiwanie dostępu do usługi na jednym węźle głównym i zwraca błąd 404, Przełącz toohello innych węzła głównego.

2. węzeł hello toodetermine i port, który usługa jest dostępna, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.

## <a id="networktraffic"></a>Kontrolowanie ruchu w sieci

Ruch sieciowy w sieciach wirtualnych platformy Azure mogą być kontrolowane za pomocą hello następujące metody:

* **Sieciowe grupy zabezpieczeń** (NSG) pozwalają toofilter ruchu przychodzącego i wychodzącego toohello sieci. Aby uzyskać więcej informacji, zobacz hello [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.

    > [!WARNING]
    > HDInsight nie obsługuje ograniczenia ruchu wychodzącego.

* **Trasy zdefiniowane przez użytkownika** (przez) zdefiniuj, jak przepływa ruch między zasobami w sieci hello. Aby uzyskać więcej informacji, zobacz hello [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md) dokumentu.

* **Sieci wirtualnych urządzeń** replikować hello funkcjonalność urządzeń, takich jak routery i zapory. Aby uzyskać więcej informacji, zobacz hello [urządzenia sieciowe](https://azure.microsoft.com/solutions/network-appliances) dokumentu.

Jako usługa zarządzana HDInsight wymaga nieograniczony dostęp do usług kondycji i zarządzania tooAzure w hello chmury Azure. Przy użyciu grup NSG i Udr, należy się upewnić, że HDInsight tych usług można nadal komunikować się z usługą HDInsight.

HDInsight udostępnia usługi na kilku portów. Używając urządzenie wirtualne zapory, musisz zezwolić na ruch na powitania porty używane w przypadku tych usług. Aby uzyskać więcej informacji zobacz sekcję hello [wymagane porty].

### <a id="hdinsight-ip"></a>HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika

Jeśli planujesz używanie **sieciowej grupy zabezpieczeń** lub **trasy zdefiniowane przez użytkownika** toocontrol ruch sieciowy, wykonaj następujące akcje przed zainstalowaniem usługi HDInsight hello:

1. Zidentyfikuj hello planowanie toouse HDInsight region platformy Azure.

2. Określ adresy IP hello wymagane przez HDInsight. Aby uzyskać więcej informacji, zobacz hello [adresy IP wymagane przez HDInsight](#hdinsight-ip) sekcji.

3. Tworzenie lub modyfikowanie grup zabezpieczeń sieci hello lub zdefiniowanej przez użytkownika tras dla podsieci hello zaplanowanie tooinstall HDInsight do.

    * __Sieciowe grupy zabezpieczeń__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z hello adresów IP.
    * __Trasy zdefiniowane przez użytkownika__: Utwórz adres IP tooeach trasy i ustaw hello __następnego przeskoku typu__ too__Internet__.

Aby uzyskać więcej informacji na sieciowych grup zabezpieczeń lub trasy zdefiniowane przez użytkownika Zobacz hello następującej dokumentacji:

* [Grupy zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md)

* [Trasy zdefiniowane przez użytkownika](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Wymuszone tunelowanie

Wymuszanie tunelowania jest zdefiniowane przez użytkownika konfiguracji routingu, gdzie cały ruch z podsieci jest wymuszone tooa określonej sieci lub lokalizacji, takiej jak sieć lokalną. HDInsight jest __nie__ obsługi wymuszonego tunelowania.

## <a id="hdinsight-ip"></a>Wymaganych adresów IP

> [!IMPORTANT]
> Witaj kondycji Azure i usługi zarządzania musi być w stanie toocommunicate z usługą HDInsight. Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, zezwalać na ruch z hello adresów IP dla tych tooreach usługi HDInsight.
>
> Jeśli nie używasz ruch toocontrol trasy zdefiniowane przez użytkownika i grupy zabezpieczeń sieci, można zignorować w tej sekcji.

Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, musisz zezwolić na ruch z hello Azure kondycji i zarządzania tooreach usługi HDInsight. Użyj hello następujące adresy IP hello toofind kroki, które może:

1. Zawsze musi zezwalać na ruch z hello następujących adresów IP:

    | Adres IP | Port dozwolone | Kierunek |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Przychodzący |
    | 23.99.5.239 | 443 | Przychodzący |
    | 168.61.48.131 | 443 | Przychodzący |
    | 138.91.141.162 | 443 | Przychodzący |

2. W przypadku klastra HDInsight w jednym z następujących regionach hello, następnie należy zezwolić na ruch z hello adresów IP dla regionu hello:

    > [!IMPORTANT]
    > Jeśli hello region platformy Azure, którego używasz, nie jest wyświetlana, następnie używać tylko hello cztery adresów IP z kroku 1.

    | Kraj | Region | Dozwolonych adresów IP | Port dozwolone | Kierunek |
    | ---- | ---- | ---- | ---- | ----- |
    | Azja | Azja Wschodnia | 23.102.235.122</br>52.175.38.134 | 443 | Przychodzący |
    | &nbsp; | Azja Południowo-Wschodnia | 13.76.245.160</br>13.76.136.249 | 443 | Przychodzący |
    | Australia | Australia Wschodnia | 104.210.84.115</br>13.75.152.195 | 443 | Przychodzący |
    | &nbsp; | Australia Południowo-Wschodnia | 13.77.2.56</br>13.77.2.94 | 443 | Przychodzący |
    | Brazylia | Brazylia Południowa | 191.235.84.104</br>191.235.87.113 | 443 | Przychodzący |
    | Kanada | Kanada Wschodnia | 52.229.127.96</br>52.229.123.172 | 443 | Przychodzący |
    | &nbsp; | Kanada Środkowa | 52.228.37.66</br>52.228.45.222 | 443 | Przychodzący |
    | Chiny | Chiny Północne | 42.159.96.170</br>139.217.2.219 | 443 | Przychodzący |
    | &nbsp; | Chiny Wschodnie | 42.159.198.178</br>42.159.234.157 | 443 | Przychodzący |
    | Europa | Europa Północna | 52.164.210.96</br>13.74.153.132 | 443 | Przychodzący |
    | &nbsp; | Europa Zachodnia| 52.166.243.90</br>52.174.36.244 | 443 | Przychodzący |
    | Niemcy | Niemcy Środkowe | 51.4.146.68</br>51.4.146.80 | 443 | Przychodzący |
    | &nbsp; | Niemcy Północno-Wschodnie | 51.5.150.132</br>51.5.144.101 | 443 | Przychodzący |
    | Indie | Indie Środkowe | 52.172.153.209</br>52.172.152.49 | 443 | Przychodzący |
    | Japonia | Japonia Wschodnia | 13.78.125.90</br>13.78.89.60 | 443 | Przychodzący |
    | &nbsp; | Japonia Zachodnia | 40.74.125.69</br>138.91.29.150 | 443 | Przychodzący |
    | Korea | Korea Środkowa | 52.231.39.142</br>52.231.36.209 | 433 | Przychodzący |
    | &nbsp; | Korea Południowa | 52.231.203.16</br>52.231.205.214 | 443 | Przychodzący
    | Wielka Brytania | Zachodnie Zjednoczone Królestwo | 51.141.13.110</br>51.141.7.20 | 443 | Przychodzący |
    | &nbsp; | Południowe Zjednoczone Królestwo | 51.140.47.39</br>51.140.52.16 | 443 | Przychodzący |
    | Stany Zjednoczone | Środkowe stany USA | 13.67.223.215</br>40.86.83.253 | 443 | Przychodzący |
    | &nbsp; | Środkowo-północne stany USA | 157.56.8.38</br>157.55.213.99 | 443 | Przychodzący |
    | &nbsp; | Środkowo-zachodnie stany USA | 52.161.23.15</br>52.161.10.167 | 443 | Przychodzący |
    | &nbsp; | Zachodnie stany USA 2 | 52.175.211.210</br>52.175.222.222 | 443 | Przychodzący |

    Dla informacji na temat hello IP dotyczy toouse systemu Azure dla instytucji rządowych, zobacz hello [Azure dla instytucji rządowych analizy i analiza](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) dokumentu.

3. Jeśli używasz niestandardowego serwera DNS z sieci wirtualnej, należy także zezwolić na dostęp z __168.63.129.16__. Ten adres jest platformy Azure, cyklicznego programu rozpoznawania nazw. Aby uzyskać więcej informacji, zobacz hello [rozpoznawanie nazw dla maszyn wirtualnych i roli wystąpień](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) dokumentu.

Aby uzyskać więcej informacji, zobacz hello [kontrolowanie ruchu w sieci](#networktraffic) sekcji.

## <a id="hdinsight-ports"></a>Wymagane porty

Jeśli planowane jest użycie sieci **urządzenie wirtualne zapory** toosecure hello sieci wirtualnej, a użytkownik musi zezwolić na ruch wychodzący na powitania następujące porty:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Listę portów dla określonych usług, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-port-settings-for-services.md) dokumentu.

Aby uzyskać więcej informacji na reguły zapory dla urządzenia wirtualnego, zobacz hello [scenariuszu urządzenie wirtualne](../virtual-network/virtual-network-scenario-udr-gw-nva.md) dokumentu.

## <a id="hdinsight-nsg"></a>Przykład: sieciowych grup zabezpieczeń z usługą HDInsight

Przykłady Hello w tej sekcji pokazują, jak grupy zabezpieczeń sieci toocreate zasady umożliwiające toocommunicate HDInsight z hello usług zarządzania platformy Azure. Przed użyciem przykłady hello, Dostosuj hello IP adresów toomatch hello widocznych dla hello region platformy Azure, którego używasz. Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.

### <a name="azure-resource-management-template"></a>Szablonu zarządzania zasobami platformy Azure

Witaj następujące zarządzanie zasobami szablon tworzy sieć wirtualną, która ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP hello wymagane przez HDInsight. Ten szablon tworzy klaster usługi HDInsight w sieci wirtualnej hello.

* [Wdrażanie zabezpieczonej sieci wirtualnej platformy Azure i klaster usługi HDInsight Hadoop](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz. Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.

### <a name="azure-powershell"></a>Azure PowerShell

Użyj powitania po toocreate skrypt programu PowerShell siecią wirtualną, która ogranicza ruchu przychodzącego i zezwala na ruch z hello adresów IP dla regionu Europa Północna, Europa hello.

> [!IMPORTANT]
> Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz. Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> W tym przykładzie pokazano, jak tooadd tooallow reguły ruchu przychodzącego ruchu sieciowego na adresach IP hello wymagane. Nie zawiera toorestrict reguły ruchu przychodzącego dostęp z innych źródeł.
>
> Witaj poniższy przykład przedstawia sposób tooenable SSH dostęp z Internetu hello:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Użyj hello następujące kroki toocreate sieci wirtualnej, który ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP hello wymagane przez usługi HDInsight.

1. Witaj Użyj następującego polecenia toocreate nową sieciową grupę zabezpieczeń o nazwie `hdisecure`. Zastąp **RESOURCEGROUPNAME** z grupą zasobów hello zawierający hello sieci wirtualnej platformy Azure. Zastąp **lokalizacji** hello lokalizacji (regionu) tej grupy hello został utworzony w.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Po utworzeniu grupy hello otrzymasz informacji na temat hello nowej grupy.

2. Użyj powitania po tooadd reguły toohello nową grupę zabezpieczeń sieci umożliwiająca komunikacji przychodzącej na porcie 443 z hello Azure HDInsight usługi kondycji i zarządzania. Zastąp **RESOURCEGROUPNAME** o nazwie hello hello grupy zasobów, zawierającą hello sieci wirtualnej platformy Azure.

    > [!IMPORTANT]
    > Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz. Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve hello Unikatowy identyfikator dla tej grupy zabezpieczeń sieci hello Użyj następującego polecenia:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    To polecenie zwraca wartość toohello podobne, następującego tekstu:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Użyj podwójnych cudzysłowów wokół identyfikatora w poleceniu hello, jeśli nie otrzymasz hello oczekiwano wyników.

4. Hello Użyj następującego polecenia tooapply hello zabezpieczeń grupy tooa podsieci. Zastąp hello __GUID__ i __RESOURCEGROUPNAME__ z hello te zwracane z hello w poprzednim kroku. Zastąp __VNETNAME__ i __SUBNETNAME__ z hello wirtualnej nazwy sieciowej i nazwy podsieci, które mają toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Po zakończeniu wykonywania tego polecenia można zainstalować usługi HDInsight na powitania sieci wirtualnej.

> [!IMPORTANT]
> Te czynności tylko otworzyć dostępu toohello HDInsight kondycji i zarządzania usługi na powitania chmury Azure. Wszystkie inne dostępu toohello klastra usługi HDInsight z hello zewnętrznej sieci wirtualnej jest zablokowany. tooenable dostępu z zewnętrznej sieci wirtualnej hello, należy dodać dodatkowych reguł sieciowej grupy zabezpieczeń.
>
> Witaj poniższy przykład przedstawia sposób tooenable SSH dostęp z Internetu hello:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a>Przykład: Konfiguracji DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Rozpoznawanie nazw między sieci wirtualnej i sieci połączonych lokalnie

W tym przykładzie powoduje hello następujące założenia:

* Masz sieć wirtualna Azure, która jest tooan połączone siecią lokalną przy użyciu bramy sieci VPN.

* Hello niestandardowy serwer DNS w sieci wirtualnej hello działa jako system operacyjny hello Linux lub Unix.

* [Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na powitania niestandardowy serwer DNS.

Na powitania niestandardowy serwer DNS w sieci wirtualnej hello:

1. Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure toofind hello sufiksu DNS sieci wirtualnej hello:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Na powitania niestandardowy serwer DNS dla sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.local` pliku:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Zastąp hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartość sufiksu DNS hello sieci wirtualnej.

    Ta konfiguracja kieruje wszystkie żądania sufiks DNS hello hello sieci wirtualnej toohello Azure cyklicznego programu rozpoznawania nazw DNS.

2. Na powitania niestandardowy serwer DNS dla sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Zastąp hello `10.0.0.0/16` wartość z zakresu adresów IP hello sieci wirtualnej. Ten wpis umożliwia adresy żądań rozpoznawania nazw w tym zakresie.

    * Dodaj zakres adresów IP hello toohello sieci lokalne powitania `acl goodclients { ... }` sekcji.  Wpis umożliwia żądań rozpoznawania nazw z zasobów w sieci lokalnej hello.
    
    * Zastąp wartość hello `192.168.0.1` o adresie IP hello lokalnego serwera DNS. Ten wpis kieruje wszystkich innych żądań toohello lokalnymi DNS serwera DNS.

3. Konfiguracja hello toouse, uruchom ponownie powiązania. Na przykład `sudo service bind9 restart`.

4. Dodaj serwer DNS warunkowego przesyłania dalej toohello lokalnymi. Skonfiguruj hello warunkowego przesyłania dalej toosend żądań hello sufiksu DNS z kroku 1 toohello niestandardowy serwer DNS.

    > [!NOTE]
    > Dokumentacja hello oprogramowania DNS dla szczegółowych informacji na temat tooadd warunkowego przesyłania dalej.

Po wykonaniu tych czynności możesz połączyć tooresources w każdej sieci przy użyciu w pełni kwalifikowanych nazw domen (FQDN). Teraz można zainstalować usługi HDInsight w sieci wirtualnej hello.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Rozpoznawanie nazw między dwiema połączone sieci wirtualne

W tym przykładzie powoduje hello następujące założenia:

* Masz dwie sieci wirtualnych Azure, które są połączone przy użyciu bramy sieci VPN lub komunikacji równorzędnej.

* Hello niestandardowy serwer DNS w obu sieci działa jako system operacyjny hello Linux lub Unix.

* [Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na powitania niestandardowych serwerów DNS.

1. Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure toofind hello sufiksu DNS obu sieci wirtualnych:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Witaj Użyj następującego tekstu jako zawartość hello hello `/etc/bind/named.config.local` pliku na powitania niestandardowy serwer DNS. Na powitania niestandardowy serwer DNS w sieci zarówno wirtualnych, należy wprowadzić tę zmianę.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Zastąp hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartości z sufiksem DNS hello hello __innych__ sieci wirtualnej. Ten wpis kieruje żądania dla sufiksu DNS hello toohello sieci zdalnej hello niestandardowe DNS w sieci.

3. Na powitania niestandardowych serwerów DNS w sieci zarówno wirtualnych, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Zastąp hello `10.0.0.0/16` i `10.1.0.0/16` wartości z adresem IP hello odnoszą się do zakresów sieci wirtualne. Ten wpis umożliwia zasobów w każdej sieci żądań toomake hello serwerów DNS.

    Wszystkie żądania, które nie są dostępne dla sufiksów DNS hello hello sieciami wirtualnymi (na przykład microsoft.com) jest obsługiwane przez hello Azure cyklicznego programu rozpoznawania nazw.

4. Konfiguracja hello toouse, uruchom ponownie powiązania. Na przykład `sudo service bind9 restart` na obu serwerach DNS.

Po wykonaniu tych czynności możesz połączyć tooresources w hello sieci wirtualnej przy użyciu w pełni kwalifikowanych nazw domen (FQDN). Teraz można zainstalować usługi HDInsight w sieci wirtualnej hello.

## <a name="next-steps"></a>Następne kroki

* Na przykład na trasie konfiguracji sieci lokalnej tooan tooconnect HDInsight, zobacz [sieć lokalną tooan połączyć HDInsight](./connect-on-premises-network.md).

* Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz hello [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).

* Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).

* Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).