---
title: "przy użyciu sieci wirtualnych - Azure HDInsight tooKafka aaaConnect | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć toodirectly tooKafka w usłudze HDInsight przy użyciu sieci wirtualnej platformy Azure. Dowiedz się, jak tooKafka tooconnect od klientów Programowanie przy użyciu bramy sieci VPN lub z klientów w lokalnej sieci przy użyciu urządzenia bramy sieci VPN."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Łączenie się tooKafka w usłudze HDInsight (wersja zapoznawcza) za pośrednictwem sieci wirtualnej platformy Azure

Dowiedz się, jak toodirectly łączyć tooKafka w usłudze HDInsight przy użyciu sieci wirtualnych Azure. Ten dokument zawiera informacje dotyczące łączenia tooKafka przy użyciu hello następujące konfiguracje:

* Z zasobów w sieci lokalnej. To połączenie zostanie nawiązane za pomocą urządzenia sieci VPN (oprogramowania lub sprzętu) w sieci lokalnej.
* Środowiska programowania przy użyciu oprogramowania klienta sieci VPN.

## <a name="architecture-and-planning"></a>Planowanie i architektura

HDInsight nie zezwala na bezpośrednie połączenie tooKafka za pośrednictwem hello publicznej sieci internet. Zamiast tego Kafka klientów (producenci i konsumenci) muszą używać jednej z hello następujących metod:

* Uruchom powitania klienta w hello tej samej sieci wirtualnej, jak Kafka w usłudze HDInsight. Ta konfiguracja jest używana w hello [rozpoczynać Apache Kafka (wersja zapoznawcza) w usłudze HDInsight](hdinsight-apache-kafka-get-started.md) dokumentu. Hello bezpośrednio uruchamia klienta na powitania HDInsight węzły klastra lub na inną maszynę wirtualną w hello sam sieci.

* Połączenie sieci prywatnej, takich jak sieci lokalnej, toohello sieci wirtualnej. Ta konfiguracja umożliwia klientom w sieci lokalnej toodirectly pracy z Kafka. tooenable tę konfigurację, wykonaj następujące zadania hello:

    1. Tworzenie sieci wirtualnej.
    2. Tworzenie bramy sieci VPN, która używa konfiguracji lokacja lokacja. Konfiguracja Hello używana w tym dokumencie łączy tooa urządzenia bramy sieci VPN w sieci lokalnej.
    3. Utwórz serwer DNS w sieci wirtualnej hello.
    4. Konfiguruj przekazywanie między powitania serwera DNS w każdej sieci.
    5. Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej hello.

    Aby uzyskać więcej informacji, zobacz hello [połączenia z siecią lokalną tooKafka](#on-premises) sekcji. 

* Połącz poszczególnych maszyn toohello sieci wirtualnej przy użyciu bramy sieci VPN i klienta sieci VPN. tooenable tę konfigurację, wykonaj następujące zadania hello:

    1. Tworzenie sieci wirtualnej.
    2. Tworzenie bramy sieci VPN, która używa konfiguracji punkt lokacja. Ta konfiguracja zapewnia klienta sieci VPN, który może zostać zainstalowany na komputerach klienckich z systemem Windows.
    3. Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej hello.
    4. Skonfiguruj Kafka IP reklamy. Ta konfiguracja pozwala powitania klienta tooconnect przy użyciu protokołu IP adresowania zamiast nazwy domeny.
    5. Pobranie i użycie powitania klienta sieci VPN w systemie deweloperskim hello.

    Aby uzyskać więcej informacji, zobacz hello [tooKafka Uzyskuj dostęp do klienta sieci VPN](#vpnclient) sekcji.

    > [!WARNING]
    > Ta konfiguracja jest zalecana tylko do celów programistycznych, ze względu na powitania następujące ograniczenia:
    >
    > * Każdy klient musi połączyć za pomocą oprogramowania klienta sieci VPN. Platforma Azure udostępnia tylko klient z systemem Windows.
    > * powitania klienta nie zostały spełnione Nazwa rozwiązania żądań toohello sieci wirtualnej, trzeba używać adresów toocommunicate z Kafka IP. Komunikacja IP wymaga dodatkowej konfiguracji hello Kafka klastra.

Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Łączenie z tooKafka z sieci lokalnej

toocreate klastra Kafka, który komunikuje się z sieci lokalnej, wykonaj kroki hello hello [sieć lokalną tooyour połączyć HDInsight](./connect-on-premises-network.md) dokumentu.

> [!IMPORTANT]
> Podczas tworzenia klastra usługi HDInsight hello, wybierz hello __Kafka__ typ klastra.

Te kroki tworzenia hello następującej konfiguracji:

* Azure Virtual Network
* Brama VPN lokacja lokacja
* Konto usługi Azure Storage (używane przez usługi HDInsight)
* Kafka w usłudze HDInsight

tooverify klienta Kafka połączyć z klastra toohello z lokalnymi, użyj kroków hello hello [przykład: Python klienta](#python-client) sekcji.

## <a id="vpnclient"></a>TooKafka Uzyskuj dostęp do klienta sieci VPN

Wykonaj kroki hello w tym hello toocreate sekcji następującej konfiguracji:

* Azure Virtual Network
* Brama sieci VPN punkt lokacja
* Konto usługi Azure Storage (używane przez usługi HDInsight)
* Kafka w usłudze HDInsight

1. Wykonaj kroki hello hello [Praca z certyfikatów z podpisem własnym dla połączenia punkt lokacja](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) dokumentu. Ten dokument tworzy niezbędne hello bramy certyfikaty hello.

2. Otwórz wiersz programu PowerShell i użyj powitania po toolog kodu w tooyour subskrypcji platformy Azure:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Użyj następującego kodu toocreate zmiennych, które zawierają informacje o konfiguracji hello:

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. Użyj hello poniższy kod grupy zasobów platformy Azure hello toocreate i siecią wirtualną:

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > Może upłynąć kilka minut toocomplete tego procesu.

5. Użyj następującego kodu toocreate hello konto magazynu Azure i obiektów blob kontenera hello:

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. Użyj powitania po klastra usługi HDInsight hello toocreate kodu:

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > Ten proces trwa około 20 minut toocomplete.

8. Użyj następującego polecenia cmdlet tooretrieve hello adres URL klienta VPN systemu Windows hello dla sieci wirtualnej hello hello:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    toodownload powitania klienta VPN systemu Windows, użyj hello zwracane identyfikatora URI w przeglądarce sieci web.

### <a name="configure-kafka-for-ip-advertising"></a>Skonfiguruj Kafka do celów reklamowych IP

Domyślnie dozorcy zwraca nazwę domeny hello hello tooclients brokerzy Kafka. Ta konfiguracja nie działa z powitania klienta oprogramowania sieci VPN, jako nie może używać rozpoznawania nazw dla jednostek w sieci wirtualnej hello. W przypadku tej konfiguracji należy użyć następujących hello adresów Kafka tooadvertise IP tooconfigure kroki zamiast nazwy domeny:

1. W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net. Zastąp __CLUSTERNAME__ o nazwie hello hello Kafka w klastrze usługi HDInsight.

    Po wyświetleniu monitu użyj hello HTTPS nazwę i hasło użytkownika hello klastra. Hello Interfejsu sieci Web Ambari hello klastra jest wyświetlana.

2. Wybierz tooview informacji na temat Kafka, __Kafka__ z listy hello powitania po lewej stronie.

    ![Lista usług z Kafka wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Wybierz tooview konfiguracji Kafka __Configs__ w środku górnej hello.

    ![Łącza Configs Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. Witaj toofind __kafka env__ konfiguracji, wprowadź `kafka-env` w hello __filtru__ w prawym górnym rogu hello.

    ![Konfiguracja Kafka, kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. adresy Kafka tooadvertise IP tooconfigure, Dodaj powitania od dołu toohello tekst hello __kafka env szablonów__ pola:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. Wprowadź tooconfigure hello interfejs, który nasłuchuje Kafka `listeners` w hello __filtru__ w prawym górnym rogu hello.

7. tooconfigure toolisten Kafka na wszystkich interfejsach sieciowych, zmień wartość hello w hello __odbiorników__ pola zbyt`PLAINTEXT://0.0.0.0:9092`.

8. zmiany konfiguracji hello toosave, użyj hello __zapisać__ przycisku. Wprowadź wiadomość tekstową opisujące hello zmiany. Wybierz __OK__ po hello zmiany zostały zapisane.

    ![Konfiguracja przyciskiem Zapisz](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. błędy tooprevent po ponownym uruchomieniu Kafka, użyj hello __akcji usługi__ i wybrać __włączyć w trybie konserwacji__. Wybierz OK toocomplete tej operacji.

    ![Włącz funkcję obsługi wyróżnione akcje usługi](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, użyj hello __Uruchom ponownie__ i wybrać __ponowne uruchomienie wszystkich wpływ__. Potwierdź hello ponownego uruchomienia, a następnie użyj hello __OK__ przycisku po wykonaniu operacji hello.

    ![Uruchom ponownie przycisk o ponowne uruchomienie wszystkich wpływ wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. toodisable tryb konserwacji, użyj hello __akcji usługi__ i wybrać __włączyć Wyłącz tryb konserwacji__. Wybierz **OK** toocomplete tej operacji.

### <a name="connect-toohello-vpn-gateway"></a>Połączenie bramy sieci VPN toohello

Brama sieci VPN toohello tooconnect z __klienta systemu Windows__, użyj hello __połączyć tooAzure__ sekcji hello [skonfigurować połączenie punkt-lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) dokumentu.

## <a id="python-client"></a>Przykład: Python klienta

toovalidate tooKafka łączności, użyj hello następujące kroki toocreate i uruchom producent Python i klienta:

1. Użyj hello następujące metody tooretrieve hello w pełni kwalifikowana nazwa domeny (FQDN) i adresy IP hello węzłów klastra Kafka hello:

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

    Ten skrypt, przy założeniu, że `$resourceGroupName` jest nazwą hello hello grupy zasobów platformy Azure, która zawiera hello sieci wirtualnej.

    Zapisz hello zwrócił informacji do użycia w następnych krokach hello.

2. Użyj powitania po tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) klienta:

        pip install kafka-python

3. toosend danych tooKafka hello Użyj następującego kodu Python:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Zastąp hello `'kafka_broker'` wpisów z adresami hello zwrócony z kroku 1 w tej sekcji:

    * Jeśli używasz __klienta VPN oprogramowania__, Zastąp hello `kafka_broker` wpisów z adresem IP hello węzły procesu roboczego.

    * Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp hello `kafka_broker` wpisów z hello FQDN hello węzłów procesu roboczego.

    > [!NOTE]
    > Ten kod wysyła ciąg hello `test message` tematu toohello `testtopic`. Hello domyślną konfigurację Kafka w usłudze HDInsight jest toocreate hello tematu, jeśli nie istnieje.

4. wiadomości powitania tooretrieve z Kafka, użyj następującego kodu Python hello:

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    Zastąp hello `'kafka_broker'` wpisów z adresami hello zwrócony z kroku 1 w tej sekcji:

    * Jeśli używasz __klienta VPN oprogramowania__, Zastąp hello `kafka_broker` wpisów z adresem IP hello węzły procesu roboczego.

    * Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp hello `kafka_broker` wpisów z hello FQDN hello węzłów procesu roboczego.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o korzystaniu z usługi HDInsight z sieci wirtualnej, zobacz hello [rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure](hdinsight-extend-hadoop-virtual-network.md) dokumentu.

Aby uzyskać więcej informacji na temat tworzenia sieci wirtualnej platformy Azure z bramą sieci VPN typu punkt-lokacja Zobacz hello w następujących dokumentach:

* [Skonfiguruj połączenie punkt-lokacja za pomocą hello portalu Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Skonfiguruj połączenie punkt-lokacja za pomocą programu Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Aby uzyskać więcej informacji na temat pracy z Kafka w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Wprowadzenie do platformy Kafka w usłudze HDInsight](hdinsight-apache-kafka-get-started.md)
* [Użyj funkcji dublowania z Kafka w usłudze HDInsight](hdinsight-apache-kafka-mirroring.md)
