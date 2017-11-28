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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="80ae6-104">Łączenie się tooKafka w usłudze HDInsight (wersja zapoznawcza) za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="80ae6-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="80ae6-105">Dowiedz się, jak toodirectly łączyć tooKafka w usłudze HDInsight przy użyciu sieci wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="80ae6-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="80ae6-106">Ten dokument zawiera informacje dotyczące łączenia tooKafka przy użyciu hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="80ae6-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="80ae6-107">Z zasobów w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-107">From resources in an on-premises network.</span></span> <span data-ttu-id="80ae6-108">To połączenie zostanie nawiązane za pomocą urządzenia sieci VPN (oprogramowania lub sprzętu) w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="80ae6-109">Środowiska programowania przy użyciu oprogramowania klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="80ae6-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="80ae6-110">Planowanie i architektura</span><span class="sxs-lookup"><span data-stu-id="80ae6-110">Architecture and planning</span></span>

<span data-ttu-id="80ae6-111">HDInsight nie zezwala na bezpośrednie połączenie tooKafka za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="80ae6-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="80ae6-112">Zamiast tego Kafka klientów (producenci i konsumenci) muszą używać jednej z hello następujących metod:</span><span class="sxs-lookup"><span data-stu-id="80ae6-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="80ae6-113">Uruchom powitania klienta w hello tej samej sieci wirtualnej, jak Kafka w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ae6-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="80ae6-114">Ta konfiguracja jest używana w hello [rozpoczynać Apache Kafka (wersja zapoznawcza) w usłudze HDInsight](hdinsight-apache-kafka-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="80ae6-115">Hello bezpośrednio uruchamia klienta na powitania HDInsight węzły klastra lub na inną maszynę wirtualną w hello sam sieci.</span><span class="sxs-lookup"><span data-stu-id="80ae6-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="80ae6-116">Połączenie sieci prywatnej, takich jak sieci lokalnej, toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="80ae6-117">Ta konfiguracja umożliwia klientom w sieci lokalnej toodirectly pracy z Kafka.</span><span class="sxs-lookup"><span data-stu-id="80ae6-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="80ae6-118">tooenable tę konfigurację, wykonaj następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="80ae6-119">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="80ae6-120">Tworzenie bramy sieci VPN, która używa konfiguracji lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="80ae6-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="80ae6-121">Konfiguracja Hello używana w tym dokumencie łączy tooa urządzenia bramy sieci VPN w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="80ae6-122">Utwórz serwer DNS w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="80ae6-123">Konfiguruj przekazywanie między powitania serwera DNS w każdej sieci.</span><span class="sxs-lookup"><span data-stu-id="80ae6-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="80ae6-124">Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="80ae6-125">Aby uzyskać więcej informacji, zobacz hello [połączenia z siecią lokalną tooKafka](#on-premises) sekcji.</span><span class="sxs-lookup"><span data-stu-id="80ae6-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="80ae6-126">Połącz poszczególnych maszyn toohello sieci wirtualnej przy użyciu bramy sieci VPN i klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="80ae6-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="80ae6-127">tooenable tę konfigurację, wykonaj następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="80ae6-128">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="80ae6-129">Tworzenie bramy sieci VPN, która używa konfiguracji punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="80ae6-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="80ae6-130">Ta konfiguracja zapewnia klienta sieci VPN, który może zostać zainstalowany na komputerach klienckich z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="80ae6-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="80ae6-131">Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="80ae6-132">Skonfiguruj Kafka IP reklamy.</span><span class="sxs-lookup"><span data-stu-id="80ae6-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="80ae6-133">Ta konfiguracja pozwala powitania klienta tooconnect przy użyciu protokołu IP adresowania zamiast nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="80ae6-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="80ae6-134">Pobranie i użycie powitania klienta sieci VPN w systemie deweloperskim hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="80ae6-135">Aby uzyskać więcej informacji, zobacz hello [tooKafka Uzyskuj dostęp do klienta sieci VPN](#vpnclient) sekcji.</span><span class="sxs-lookup"><span data-stu-id="80ae6-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="80ae6-136">Ta konfiguracja jest zalecana tylko do celów programistycznych, ze względu na powitania następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="80ae6-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="80ae6-137">Każdy klient musi połączyć za pomocą oprogramowania klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="80ae6-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="80ae6-138">Platforma Azure udostępnia tylko klient z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="80ae6-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="80ae6-139">powitania klienta nie zostały spełnione Nazwa rozwiązania żądań toohello sieci wirtualnej, trzeba używać adresów toocommunicate z Kafka IP.</span><span class="sxs-lookup"><span data-stu-id="80ae6-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="80ae6-140">Komunikacja IP wymaga dodatkowej konfiguracji hello Kafka klastra.</span><span class="sxs-lookup"><span data-stu-id="80ae6-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="80ae6-141">Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="80ae6-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="80ae6-142"><a id="on-premises"></a>Łączenie z tooKafka z sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="80ae6-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="80ae6-143">toocreate klastra Kafka, który komunikuje się z sieci lokalnej, wykonaj kroki hello hello [sieć lokalną tooyour połączyć HDInsight](./connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80ae6-144">Podczas tworzenia klastra usługi HDInsight hello, wybierz hello __Kafka__ typ klastra.</span><span class="sxs-lookup"><span data-stu-id="80ae6-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="80ae6-145">Te kroki tworzenia hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="80ae6-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="80ae6-146">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="80ae6-146">Azure Virtual Network</span></span>
* <span data-ttu-id="80ae6-147">Brama VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="80ae6-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="80ae6-148">Konto usługi Azure Storage (używane przez usługi HDInsight)</span><span class="sxs-lookup"><span data-stu-id="80ae6-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="80ae6-149">Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ae6-149">Kafka on HDInsight</span></span>

<span data-ttu-id="80ae6-150">tooverify klienta Kafka połączyć z klastra toohello z lokalnymi, użyj kroków hello hello [przykład: Python klienta](#python-client) sekcji.</span><span class="sxs-lookup"><span data-stu-id="80ae6-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="80ae6-151"><a id="vpnclient"></a>TooKafka Uzyskuj dostęp do klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="80ae6-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="80ae6-152">Wykonaj kroki hello w tym hello toocreate sekcji następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="80ae6-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="80ae6-153">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="80ae6-153">Azure Virtual Network</span></span>
* <span data-ttu-id="80ae6-154">Brama sieci VPN punkt lokacja</span><span class="sxs-lookup"><span data-stu-id="80ae6-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="80ae6-155">Konto usługi Azure Storage (używane przez usługi HDInsight)</span><span class="sxs-lookup"><span data-stu-id="80ae6-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="80ae6-156">Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ae6-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="80ae6-157">Wykonaj kroki hello hello [Praca z certyfikatów z podpisem własnym dla połączenia punkt lokacja](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="80ae6-158">Ten dokument tworzy niezbędne hello bramy certyfikaty hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="80ae6-159">Otwórz wiersz programu PowerShell i użyj powitania po toolog kodu w tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="80ae6-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="80ae6-160">Użyj następującego kodu toocreate zmiennych, które zawierają informacje o konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-160">Use hello following code toocreate variables that contain configuration information:</span></span>

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

4. <span data-ttu-id="80ae6-161">Użyj hello poniższy kod grupy zasobów platformy Azure hello toocreate i siecią wirtualną:</span><span class="sxs-lookup"><span data-stu-id="80ae6-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

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
    > <span data-ttu-id="80ae6-162">Może upłynąć kilka minut toocomplete tego procesu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="80ae6-163">Użyj następującego kodu toocreate hello konto magazynu Azure i obiektów blob kontenera hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

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

6. <span data-ttu-id="80ae6-164">Użyj powitania po klastra usługi HDInsight hello toocreate kodu:</span><span class="sxs-lookup"><span data-stu-id="80ae6-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

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
  > <span data-ttu-id="80ae6-165">Ten proces trwa około 20 minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="80ae6-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="80ae6-166">Użyj następującego polecenia cmdlet tooretrieve hello adres URL klienta VPN systemu Windows hello dla sieci wirtualnej hello hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="80ae6-167">toodownload powitania klienta VPN systemu Windows, użyj hello zwracane identyfikatora URI w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="80ae6-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="80ae6-168">Skonfiguruj Kafka do celów reklamowych IP</span><span class="sxs-lookup"><span data-stu-id="80ae6-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="80ae6-169">Domyślnie dozorcy zwraca nazwę domeny hello hello tooclients brokerzy Kafka.</span><span class="sxs-lookup"><span data-stu-id="80ae6-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="80ae6-170">Ta konfiguracja nie działa z powitania klienta oprogramowania sieci VPN, jako nie może używać rozpoznawania nazw dla jednostek w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="80ae6-171">W przypadku tej konfiguracji należy użyć następujących hello adresów Kafka tooadvertise IP tooconfigure kroki zamiast nazwy domeny:</span><span class="sxs-lookup"><span data-stu-id="80ae6-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="80ae6-172">W przeglądarce sieci web przejdź toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="80ae6-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="80ae6-173">Zastąp __CLUSTERNAME__ o nazwie hello hello Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ae6-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="80ae6-174">Po wyświetleniu monitu użyj hello HTTPS nazwę i hasło użytkownika hello klastra.</span><span class="sxs-lookup"><span data-stu-id="80ae6-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="80ae6-175">Hello Interfejsu sieci Web Ambari hello klastra jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="80ae6-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="80ae6-176">Wybierz tooview informacji na temat Kafka, __Kafka__ z listy hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="80ae6-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Lista usług z Kafka wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="80ae6-178">Wybierz tooview konfiguracji Kafka __Configs__ w środku górnej hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Łącza Configs Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="80ae6-180">Witaj toofind __kafka env__ konfiguracji, wprowadź `kafka-env` w hello __filtru__ w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Konfiguracja Kafka, kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="80ae6-182">adresy Kafka tooadvertise IP tooconfigure, Dodaj powitania od dołu toohello tekst hello __kafka env szablonów__ pola:</span><span class="sxs-lookup"><span data-stu-id="80ae6-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="80ae6-183">Wprowadź tooconfigure hello interfejs, który nasłuchuje Kafka `listeners` w hello __filtru__ w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="80ae6-184">tooconfigure toolisten Kafka na wszystkich interfejsach sieciowych, zmień wartość hello w hello __odbiorników__ pola zbyt`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="80ae6-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="80ae6-185">zmiany konfiguracji hello toosave, użyj hello __zapisać__ przycisku.</span><span class="sxs-lookup"><span data-stu-id="80ae6-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="80ae6-186">Wprowadź wiadomość tekstową opisujące hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="80ae6-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="80ae6-187">Wybierz __OK__ po hello zmiany zostały zapisane.</span><span class="sxs-lookup"><span data-stu-id="80ae6-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Konfiguracja przyciskiem Zapisz](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="80ae6-189">błędy tooprevent po ponownym uruchomieniu Kafka, użyj hello __akcji usługi__ i wybrać __włączyć w trybie konserwacji__.</span><span class="sxs-lookup"><span data-stu-id="80ae6-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="80ae6-190">Wybierz OK toocomplete tej operacji.</span><span class="sxs-lookup"><span data-stu-id="80ae6-190">Select OK toocomplete this operation.</span></span>

    ![Włącz funkcję obsługi wyróżnione akcje usługi](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="80ae6-192">toorestart Kafka, użyj hello __Uruchom ponownie__ i wybrać __ponowne uruchomienie wszystkich wpływ__.</span><span class="sxs-lookup"><span data-stu-id="80ae6-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="80ae6-193">Potwierdź hello ponownego uruchomienia, a następnie użyj hello __OK__ przycisku po wykonaniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Uruchom ponownie przycisk o ponowne uruchomienie wszystkich wpływ wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="80ae6-195">toodisable tryb konserwacji, użyj hello __akcji usługi__ i wybrać __włączyć Wyłącz tryb konserwacji__.</span><span class="sxs-lookup"><span data-stu-id="80ae6-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="80ae6-196">Wybierz **OK** toocomplete tej operacji.</span><span class="sxs-lookup"><span data-stu-id="80ae6-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="80ae6-197">Połączenie bramy sieci VPN toohello</span><span class="sxs-lookup"><span data-stu-id="80ae6-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="80ae6-198">Brama sieci VPN toohello tooconnect z __klienta systemu Windows__, użyj hello __połączyć tooAzure__ sekcji hello [skonfigurować połączenie punkt-lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="80ae6-199"><a id="python-client"></a>Przykład: Python klienta</span><span class="sxs-lookup"><span data-stu-id="80ae6-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="80ae6-200">toovalidate tooKafka łączności, użyj hello następujące kroki toocreate i uruchom producent Python i klienta:</span><span class="sxs-lookup"><span data-stu-id="80ae6-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="80ae6-201">Użyj hello następujące metody tooretrieve hello w pełni kwalifikowana nazwa domeny (FQDN) i adresy IP hello węzłów klastra Kafka hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="80ae6-202">Ten skrypt, przy założeniu, że `$resourceGroupName` jest nazwą hello hello grupy zasobów platformy Azure, która zawiera hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80ae6-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="80ae6-203">Zapisz hello zwrócił informacji do użycia w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="80ae6-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="80ae6-204">Użyj powitania po tooinstall hello [kafka python](http://kafka-python.readthedocs.io/) klienta:</span><span class="sxs-lookup"><span data-stu-id="80ae6-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="80ae6-205">toosend danych tooKafka hello Użyj następującego kodu Python:</span><span class="sxs-lookup"><span data-stu-id="80ae6-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="80ae6-206">Zastąp hello `'kafka_broker'` wpisów z adresami hello zwrócony z kroku 1 w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="80ae6-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="80ae6-207">Jeśli używasz __klienta VPN oprogramowania__, Zastąp hello `kafka_broker` wpisów z adresem IP hello węzły procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="80ae6-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="80ae6-208">Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp hello `kafka_broker` wpisów z hello FQDN hello węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="80ae6-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80ae6-209">Ten kod wysyła ciąg hello `test message` tematu toohello `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="80ae6-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="80ae6-210">Hello domyślną konfigurację Kafka w usłudze HDInsight jest toocreate hello tematu, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="80ae6-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="80ae6-211">wiadomości powitania tooretrieve z Kafka, użyj następującego kodu Python hello:</span><span class="sxs-lookup"><span data-stu-id="80ae6-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

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

    <span data-ttu-id="80ae6-212">Zastąp hello `'kafka_broker'` wpisów z adresami hello zwrócony z kroku 1 w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="80ae6-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="80ae6-213">Jeśli używasz __klienta VPN oprogramowania__, Zastąp hello `kafka_broker` wpisów z adresem IP hello węzły procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="80ae6-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="80ae6-214">Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp hello `kafka_broker` wpisów z hello FQDN hello węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="80ae6-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80ae6-215">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80ae6-215">Next steps</span></span>

<span data-ttu-id="80ae6-216">Aby uzyskać więcej informacji o korzystaniu z usługi HDInsight z sieci wirtualnej, zobacz hello [rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure](hdinsight-extend-hadoop-virtual-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="80ae6-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="80ae6-217">Aby uzyskać więcej informacji na temat tworzenia sieci wirtualnej platformy Azure z bramą sieci VPN typu punkt-lokacja Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="80ae6-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="80ae6-218">Skonfiguruj połączenie punkt-lokacja za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80ae6-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="80ae6-219">Skonfiguruj połączenie punkt-lokacja za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80ae6-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="80ae6-220">Aby uzyskać więcej informacji na temat pracy z Kafka w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="80ae6-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="80ae6-221">Wprowadzenie do platformy Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ae6-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="80ae6-222">Użyj funkcji dublowania z Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ae6-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
