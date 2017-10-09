---
title: aaaCreate HBase clusters w sieci wirtualnej - Azure | Dokumentacja firmy Microsoft
description: "Rozpoczynanie pracy z bazy danych HBase w usłudze Azure HDInsight. Dowiedz się, jak toocreate HDInsight HBase clusters w sieci wirtualnej Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Tworzenie klastrów HBase w usłudze HDInsight w sieci wirtualnej platformy Azure
Dowiedz się, jak toocreate Azure HDInsight HBase clusters w [sieci wirtualnej Azure][1].

Dzięki integracji sieci wirtualnej, klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak że aplikacje mogą komunikować się bezpośrednio, z bazy danych HBase. Witaj korzyści:

* Bezpośrednie połączenie między hello sieci web aplikacji toohello węzłów klastra HBase hello, co umożliwia komunikację za pomocą procedury zdalnej bazy danych HBase w języku Java wywoływania interfejsów API (RPC).
* Większa wydajność, ponieważ nie ma ruchu przejdź przez wiele bram i moduły równoważenia obciążenia.
* Witaj możliwości tooprocess poufne informacje w bardziej bezpieczny sposób bez narażania publiczny punkt końcowy.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Stacja robocza z programem Azure PowerShell**. Zobacz [instalacja i używanie programu Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Tworzenie klastra HBase w sieci wirtualnej
W tej sekcji, utworzyć klaster HBase opartych na systemie Linux z hello zależne konto magazynu Azure w sieci wirtualnej platformy Azure przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Inne metody tworzenia klastrów i opis ustawień hello, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Więcej informacji o używaniu toocreate szablonu Hadoop klastrów w usłudze HDInsight, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Niektóre właściwości są zakodowane na stałe do hello szablonu. Na przykład:
>
> * **Lokalizacja**: wschodnie stany USA 2
> * **Wersja klastra**: 3.5
> * **Liczba węzłów procesu roboczego klastra**: 2
> * **Domyślne konto magazynu**: unikatowy ciąg
> * **Nazwa sieci wirtualnej**: &lt;nazwa klastra >-Sieć wirtualna
> * **Przestrzeń adresową sieci wirtualnej**: 10.0.0.0/16
> * **Nazwa podsieci**: podsieć1
> * **Zakres adresów podsieci**: 10.0.0.0/24
>
> &lt;Nazwa klastra > jest zastępowany nazwą klastra hello udzielać przy użyciu szablonu hello.
>
>

1. Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure. Szablon Hello znajduje się w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Z hello **wdrożenie niestandardowe** bloku, wprowadź hello następujące właściwości:

   * **Subskrypcja**: wybierz klaster usługi HDInsight hello toocreate subskrypcji platformy Azure używana, hello zależne konto magazynu i hello sieci wirtualnej platformy Azure.
   * **Grupa zasobów**: Wybierz **Utwórz nowy**i określ nazwę nowej grupy zasobów.
   * **Lokalizacja**: Wybierz lokalizację dla grupy zasobów hello.
   * **ClusterName**: Wprowadź nazwę toobe klastra Hadoop hello utworzony.
   * **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.
   * **Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.  Tę nazwę można zmienić.
   * **Zgadzam się toohello warunki użytkowania hello podanych powyżej**: (Wybierz)
3. Kliknij pozycję **Kup**. Trwa około 20 minut toocreate klastra. Po utworzeniu klastra hello, możesz kliknąć hello bloku klastra w portalu tooopen hello go.

Po ukończeniu samouczka hello można toodelete hello klastra. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany. Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane. Witaj instrukcje dotyczące usuwania klastra znajdują się [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

Praca z nowego klastra HBase toobegin można użyć procedur hello w [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight HBase](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Połącz toohello klastra HBase przy użyciu interfejsów API RPC Java HBase
1. Tworzenie infrastruktury jako usługi (IaaS) maszyny wirtualnej w tej samej sieci wirtualnej platformy Azure hello i hello tej samej podsieci. Aby uzyskać instrukcje dotyczące tworzenia nowej maszyny wirtualnej IaaS, zobacz [tworzenia maszyny wirtualnej systemem Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Następujące kroki hello w tym dokumencie, należy użyć następującej wartości konfiguracji sieci hello hello:

   * **Sieć wirtualna**: &lt;nazwa klastra >-Sieć wirtualna
   * **Podsieci**: podsieć1

   > [!IMPORTANT]
   > Zastąp &lt;nazwa klastra > o nazwie hello są używane podczas tworzenia klastra usługi HDInsight hello w poprzednich krokach.
   >
   >

   Używając tych wartości, hello maszyna wirtualna jest umieszczona w hello sama sieć wirtualna i podsieć jako hello klastra usługi HDInsight. Ta konfiguracja pozwala toodirectly komunikują się ze sobą. Brak toocreate sposób klastra usługi HDInsight z węzłem krawędzi puste. węzeł brzegowy Hello może być używane toomanage hello klastra.  Aby uzyskać więcej informacji, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).

2. Korzystając z tooHBase tooconnect aplikacji Java zdalnie, możesz korzystać hello pełną nazwę domeny (FQDN). toodetermine, należy uzyskać sufiks DNS konkretnego połączenia hello hello klastra HBase. toodo, których można używać jednej z następujących metod hello:

   * Użyj toomake przeglądarki sieci Web Ambari wywołania:

     Przeglądaj toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hostuje? minimal_response = true. Monitor przechodzi w stan to plik JSON o hello sufiksów DNS.
   * Użyj narzędzia Ambari hello witryny sieci Web:

     1. Przeglądaj zbyt https://&lt;ClusterName >. azurehdinsight.net.
     2. Kliknij przycisk **hostów** z górnego menu hello.
   * Użyj wywołań REST toomake Curl:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     W hello zwrócone dane JavaScript Object Notation (JSON), Znajdź pozycję "host_name" hello. Zawiera ona hello FQDN hello węzłów w klastrze hello. Na przykład:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     Witaj część hello domeny nazwa rozpoczynający się od nazwy klastra hello jest hello sufiks DNS. Na przykład mycluster.b1.cloudapp.net.
   * Korzystanie z programu Azure PowerShell

     Użyj powitania po hello tooregister skrypt programu PowerShell usługi Azure **Get ClusterDetail** funkcji, która może być sufiks DNS używany tooreturn hello:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Po uruchamianie skryptu programu Azure PowerShell hello następujące hello Użyj polecenie sufiks DNS hello tooreturn przy użyciu hello **Get ClusterDetail** funkcji. Określ nazwę klastra HDInsight HBase, nazwę administratora i hasło administratora kopii, korzystając z tego polecenia.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     To polecenie zwraca hello sufiks DNS. Na przykład **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify, który hello maszyny wirtualnej mogą komunikować się z hello klastra HBase, użyj polecenia hello `ping headnode0.<dns suffix>` z hello maszyny wirtualnej. Na przykład headnode0.mycluster.b1.cloudapp.net ping.

toouse tych informacji w aplikacji Java, można wykonać kroki hello w [aplikacji Java toobuild Użyj Maven, korzystających z bazy danych HBase w usłudze HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate aplikacji. Aplikacja hello toohave połączenia zdalnego serwera bazy danych HBase tooa, zmodyfikuj hello **hbase-site.xml** pliku w ten przykład toouse hello FQDN dozorcy. Na przykład:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Aby uzyskać więcej informacji na temat rozpoznawania nazw w sieci wirtualnych platformy Azure w tym jak toouse własny serwer DNS, zobacz [rozpoznawania nazw (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób toocreate klaster HBase. toolearn więcej, zobacz:

* [Rozpoczynanie pracy z usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Użyj węzłami pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md)
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Rozpoczynanie pracy z platformą Hadoop w usłudze HDInsight przy użyciu bazy danych HBase](hdinsight-hbase-tutorial-get-started.md)
* [Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Omówienie sieci wirtualnej][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Szczegóły udostępniania dla nowego klastra HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Użyj akcji skryptu toocustomize klastra HBase"

[azure-preview-portal]: https://portal.azure.com
