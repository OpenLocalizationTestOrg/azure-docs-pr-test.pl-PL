---
title: "Nawiązać połączenie przy użyciu sieci wirtualnych - Azure HDInsight Kafka | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nawiązać bezpośrednie Kafka w usłudze HDInsight przy użyciu sieci wirtualnej platformy Azure. Dowiedz się, jak połączyć się z Kafka z klientów Programowanie przy użyciu bramy sieci VPN lub klienci w sieci lokalnej za pomocą urządzenia bramy sieci VPN."
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="d6580-104">Nawiązać Kafka w usłudze HDInsight (wersja zapoznawcza) za pośrednictwem sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6580-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="d6580-105">Dowiedz się, jak nawiązać bezpośrednie Kafka w usłudze HDInsight przy użyciu sieci wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="d6580-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="d6580-106">Ten dokument zawiera informacje dotyczące nawiązywania połączenia Kafka przy użyciu następujących konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d6580-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="d6580-107">Z zasobów w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-107">From resources in an on-premises network.</span></span> <span data-ttu-id="d6580-108">To połączenie zostanie nawiązane za pomocą urządzenia sieci VPN (oprogramowania lub sprzętu) w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="d6580-109">Środowiska programowania przy użyciu oprogramowania klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d6580-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="d6580-110">Planowanie i architektura</span><span class="sxs-lookup"><span data-stu-id="d6580-110">Architecture and planning</span></span>

<span data-ttu-id="d6580-111">HDInsight nie zezwala na bezpośrednie połączenie Kafka za pośrednictwem publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="d6580-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="d6580-112">Zamiast tego Kafka klientów (producenci i konsumenci) muszą używać jednej z następujących metod połączenia:</span><span class="sxs-lookup"><span data-stu-id="d6580-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="d6580-113">Uruchom klienta w tej samej sieci wirtualnej, jak Kafka w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6580-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="d6580-114">Ta konfiguracja jest używana w [rozpoczynać Apache Kafka (wersja zapoznawcza) w usłudze HDInsight](hdinsight-apache-kafka-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6580-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="d6580-115">Klient uruchamia bezpośrednio na węzłach klastra usługi HDInsight lub inną maszynę wirtualną w tej samej sieci.</span><span class="sxs-lookup"><span data-stu-id="d6580-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="d6580-116">Połączenie sieci prywatnej, takich jak sieci lokalnej do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="d6580-117">Ta konfiguracja pozwala klientom w sieci lokalnej pracować bezpośrednio z Kafka.</span><span class="sxs-lookup"><span data-stu-id="d6580-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="d6580-118">Aby włączyć tę konfigurację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d6580-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="d6580-119">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="d6580-120">Tworzenie bramy sieci VPN, która używa konfiguracji lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="d6580-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="d6580-121">Konfiguracja użyta w tym dokumencie łączy się urządzenie bramy sieci VPN w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="d6580-122">Utwórz serwer DNS w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="d6580-123">Konfiguruj przekazywanie między serwer DNS w każdej sieci.</span><span class="sxs-lookup"><span data-stu-id="d6580-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="d6580-124">Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="d6580-125">Aby uzyskać więcej informacji, zobacz [nawiązywanie Kafka z sieci lokalnej](#on-premises) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6580-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="d6580-126">Połączenie poszczególnych maszyn z sieci wirtualnej przy użyciu bramy sieci VPN i klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d6580-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="d6580-127">Aby włączyć tę konfigurację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d6580-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="d6580-128">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="d6580-129">Tworzenie bramy sieci VPN, która używa konfiguracji punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="d6580-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="d6580-130">Ta konfiguracja zapewnia klienta sieci VPN, który może zostać zainstalowany na komputerach klienckich z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="d6580-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="d6580-131">Zainstaluj Kafka w usłudze HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="d6580-132">Skonfiguruj Kafka IP reklamy.</span><span class="sxs-lookup"><span data-stu-id="d6580-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="d6580-133">Ta konfiguracja umożliwia klientowi łączyć się przy użyciu adresów IP zamiast nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="d6580-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="d6580-134">Pobranie i użycie klienta sieci VPN w systemie deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="d6580-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="d6580-135">Aby uzyskać więcej informacji, zobacz [nawiązywanie Kafka za pomocą klienta VPN](#vpnclient) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6580-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="d6580-136">Ta konfiguracja jest zalecana tylko do celów programistycznych, ze względu na następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="d6580-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="d6580-137">Każdy klient musi połączyć za pomocą oprogramowania klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d6580-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="d6580-138">Platforma Azure udostępnia tylko klient z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="d6580-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="d6580-139">Klient nie zostały spełnione żądań rozpoznawania nazw do sieci wirtualnej, należy użyć do komunikacji z Kafka o adresowaniu IP.</span><span class="sxs-lookup"><span data-stu-id="d6580-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="d6580-140">Komunikacja IP wymaga dodatkowej konfiguracji klastra Kafka.</span><span class="sxs-lookup"><span data-stu-id="d6580-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="d6580-141">Aby uzyskać więcej informacji na temat używania usługi HDInsight w sieci wirtualnej, zobacz [rozszerzyć HDInsight przy użyciu sieci wirtualnych Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="d6580-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="d6580-142"><a id="on-premises"></a>Nawiązywanie połączenia z siecią lokalną do Kafka</span><span class="sxs-lookup"><span data-stu-id="d6580-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="d6580-143">Aby utworzyć klaster Kafka, który komunikuje się z sieci lokalnej, postępuj zgodnie z instrukcjami [HDInsight połączyć się z siecią lokalną](./connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6580-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6580-144">Podczas tworzenia klastra usługi HDInsight, wybierz __Kafka__ typ klastra.</span><span class="sxs-lookup"><span data-stu-id="d6580-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="d6580-145">Te kroki Utwórz następującą konfigurację:</span><span class="sxs-lookup"><span data-stu-id="d6580-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="d6580-146">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d6580-146">Azure Virtual Network</span></span>
* <span data-ttu-id="d6580-147">Brama VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="d6580-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="d6580-148">Konto usługi Azure Storage (używane przez usługi HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d6580-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="d6580-149">Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6580-149">Kafka on HDInsight</span></span>

<span data-ttu-id="d6580-150">Aby sprawdzić, czy klient Kafka łączy do klastra z lokalnych, wykonaj czynności w [przykład: Python klienta](#python-client) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6580-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="d6580-151"><a id="vpnclient"></a>Połączenie z Kafka z klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="d6580-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="d6580-152">Wykonaj kroki w tej sekcji, aby utworzyć następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d6580-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="d6580-153">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d6580-153">Azure Virtual Network</span></span>
* <span data-ttu-id="d6580-154">Brama sieci VPN punkt lokacja</span><span class="sxs-lookup"><span data-stu-id="d6580-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="d6580-155">Konto usługi Azure Storage (używane przez usługi HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d6580-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="d6580-156">Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6580-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="d6580-157">Postępuj zgodnie z instrukcjami [Praca z certyfikatów z podpisem własnym dla połączenia punkt lokacja](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6580-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="d6580-158">Ten dokument tworzy certyfikaty wymagane dla bramy.</span><span class="sxs-lookup"><span data-stu-id="d6580-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="d6580-159">Otwórz wiersz programu PowerShell i użyć poniższego kodu, aby zalogować się do subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d6580-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="d6580-160">Aby utworzyć zmienne, które zawierają informacje o konfiguracji, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="d6580-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="d6580-161">Aby utworzyć grupy zasobów platformy Azure i siecią wirtualną, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="d6580-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="d6580-162">Może upłynąć kilka minut na zakończenie danego procesu.</span><span class="sxs-lookup"><span data-stu-id="d6580-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="d6580-163">Aby utworzyć kontener konto magazynu Azure i obiektów blob, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="d6580-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="d6580-164">Poniższy kod umożliwia utworzenie klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d6580-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="d6580-165">Ten proces trwa około 20 minut, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="d6580-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="d6580-166">Aby pobrać adres URL dla klienta VPN systemu Windows dla sieci wirtualnej, użyj następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d6580-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="d6580-167">Aby pobrać klienta VPN systemu Windows, należy użyć zwracane identyfikatora URI w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6580-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="d6580-168">Skonfiguruj Kafka do celów reklamowych IP</span><span class="sxs-lookup"><span data-stu-id="d6580-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="d6580-169">Domyślnie dozorcy zwraca nazwę domeny brokerzy Kafka do klientów.</span><span class="sxs-lookup"><span data-stu-id="d6580-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="d6580-170">Ta konfiguracja nie działa z oprogramowania klienta sieci VPN, ponieważ nie może używać rozpoznawania nazw dla jednostek w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="d6580-171">W przypadku tej konfiguracji umożliwia skonfigurowanie Kafka anonsowanie adresów IP zamiast nazwy domeny następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d6580-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="d6580-172">Przy użyciu przeglądarki sieci web, przejdź do https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d6580-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="d6580-173">Zastąp __CLUSTERNAME__ o nazwie Kafka w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6580-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="d6580-174">Po wyświetleniu monitu użyj protokołu HTTPS, nazwę użytkownika i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="d6580-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="d6580-175">Zostanie wyświetlony interfejs użytkownika sieci Web Ambari dla klastra.</span><span class="sxs-lookup"><span data-stu-id="d6580-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="d6580-176">Aby wyświetlić informacje o Kafka, wybierz __Kafka__ na liście z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="d6580-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Lista usług z Kafka wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="d6580-178">Zaznacz, aby wyświetlić konfigurację Kafka __Configs__ ze środka top.</span><span class="sxs-lookup"><span data-stu-id="d6580-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Łącza Configs Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="d6580-180">Aby znaleźć __kafka env__ konfiguracji, wprowadź `kafka-env` w __filtru__ w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="d6580-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Konfiguracja Kafka, kafka env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="d6580-182">Aby skonfigurować Kafka anonsowanie adresów IP, Dodaj poniższy tekst do dołu __kafka env szablonów__ pola:</span><span class="sxs-lookup"><span data-stu-id="d6580-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="d6580-183">Aby skonfigurować interfejs, który nasłuchuje Kafka, wprowadź `listeners` w __filtru__ w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="d6580-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="d6580-184">Aby skonfigurować Kafka do nasłuchiwania na wszystkich interfejsach sieciowych, zmień wartość w __odbiorników__ do `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="d6580-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="d6580-185">Aby zapisać zmiany konfiguracji, użyj __zapisać__ przycisku.</span><span class="sxs-lookup"><span data-stu-id="d6580-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="d6580-186">Wprowadź wiadomość tekstową opisujące zmiany.</span><span class="sxs-lookup"><span data-stu-id="d6580-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="d6580-187">Wybierz __OK__ po zapisaniu zmian.</span><span class="sxs-lookup"><span data-stu-id="d6580-187">Select __OK__ once the changes have been saved.</span></span>

    ![Konfiguracja przyciskiem Zapisz](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="d6580-189">Aby zapobiec błędom podczas ponownego uruchamiania Kafka, należy użyć __akcji usługi__ i wybrać __włączyć w trybie konserwacji__.</span><span class="sxs-lookup"><span data-stu-id="d6580-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="d6580-190">Wybierz przycisk OK, aby wykonać tę operację.</span><span class="sxs-lookup"><span data-stu-id="d6580-190">Select OK to complete this operation.</span></span>

    ![Włącz funkcję obsługi wyróżnione akcje usługi](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="d6580-192">Aby ponownie uruchomić Kafka, należy użyć __Uruchom ponownie__ i wybrać __ponowne uruchomienie wszystkich wpływ__.</span><span class="sxs-lookup"><span data-stu-id="d6580-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="d6580-193">Upewnij się, ponowne uruchomienie, a następnie użyj __OK__ przycisku po ukończeniu tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d6580-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Uruchom ponownie przycisk o ponowne uruchomienie wszystkich wpływ wyróżnione](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="d6580-195">Aby wyłączyć tryb konserwacji, użyj __akcji usługi__ i wybrać __włączyć Wyłącz tryb konserwacji__.</span><span class="sxs-lookup"><span data-stu-id="d6580-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="d6580-196">Wybierz **OK** do ukończenia tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d6580-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="d6580-197">Łączenie się z bramą sieci VPN</span><span class="sxs-lookup"><span data-stu-id="d6580-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="d6580-198">Aby połączyć się z bramą sieci VPN z __klienta systemu Windows__, użyj __nawiązywanie połączenia z usługi Azure__ sekcji [skonfigurować połączenie punkt-lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6580-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="d6580-199"><a id="python-client"></a>Przykład: Python klienta</span><span class="sxs-lookup"><span data-stu-id="d6580-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="d6580-200">Do sprawdzania poprawności łączności Kafka, należy użyć do tworzenia i uruchamiania producent Python i konsumentów następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d6580-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="d6580-201">Można pobrać w pełni kwalifikowanej nazwy domeny (FQDN) i adresy IP w węzłach klastra Kafka, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="d6580-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

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

    <span data-ttu-id="d6580-202">Ten skrypt, przy założeniu, że `$resourceGroupName` to nazwa grupy zasobów platformy Azure, która zawiera sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6580-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="d6580-203">Zapisz informacje zwrócone do użycia w następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="d6580-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="d6580-204">Należy zainstalować następujące [kafka python](http://kafka-python.readthedocs.io/) klienta:</span><span class="sxs-lookup"><span data-stu-id="d6580-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="d6580-205">Aby wysłać dane do Kafka, należy użyć poniższego kodu Python:</span><span class="sxs-lookup"><span data-stu-id="d6580-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="d6580-206">Zastąp `'kafka_broker'` wpisów z adresami zwrócony z kroku 1 w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6580-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="d6580-207">Jeśli używasz __klienta VPN oprogramowania__, Zastąp `kafka_broker` wpisów z adresu IP z węzłami procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="d6580-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="d6580-208">Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp `kafka_broker` wpisów z nazwą FQDN węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="d6580-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d6580-209">Ten kod wysyła ciąg `test message` do tematu `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="d6580-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="d6580-210">Domyślna konfiguracja Kafka w usłudze HDInsight jest tworzenie tematu, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d6580-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="d6580-211">Aby pobrać komunikaty z Kafka, należy użyć poniższego kodu Python:</span><span class="sxs-lookup"><span data-stu-id="d6580-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="d6580-212">Zastąp `'kafka_broker'` wpisów z adresami zwrócony z kroku 1 w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6580-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="d6580-213">Jeśli używasz __klienta VPN oprogramowania__, Zastąp `kafka_broker` wpisów z adresu IP z węzłami procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="d6580-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="d6580-214">Jeśli masz __włączone rozpoznawanie nazw za pomocą niestandardowy serwer DNS__, Zastąp `kafka_broker` wpisów z nazwą FQDN węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="d6580-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6580-215">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6580-215">Next steps</span></span>

<span data-ttu-id="d6580-216">Aby uzyskać więcej informacji o korzystaniu z usługi HDInsight z sieci wirtualnej, zobacz [rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure](hdinsight-extend-hadoop-virtual-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6580-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="d6580-217">Aby uzyskać więcej informacji na temat tworzenia sieci wirtualnej platformy Azure z bramą sieci VPN typu punkt-lokacja można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="d6580-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="d6580-218">Skonfiguruj połączenie punkt-lokacja za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d6580-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="d6580-219">Skonfiguruj połączenie punkt-lokacja za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6580-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="d6580-220">Więcej informacji na temat pracy z klastrem Kafka w usłudze HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="d6580-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="d6580-221">Wprowadzenie do platformy Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6580-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="d6580-222">Użyj funkcji dublowania z Kafka w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6580-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
