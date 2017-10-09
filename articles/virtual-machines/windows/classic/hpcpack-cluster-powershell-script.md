---
title: klaster HPC systemu Windows toodeploy skrypt aaaPowerShell | Dokumentacja firmy Microsoft
description: "Uruchom toodeploy skryptu środowiska PowerShell klastra systemu Windows HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Tworzenie klastra wysokiej wydajności (HPC) systemu Windows przy użyciu skryptu wdrażania hello HPC Pack IaaS
Uruchom hello HPC Pack IaaS wdrożenia programu PowerShell skryptu toodeploy całego klastra HPC Pack 2012 R2 dla obciążeń systemu Windows na maszynach wirtualnych platformy Azure. Witaj klaster składa się z węzłem głównym przyłączonych do usługi Active Directory systemem Windows Server i Microsoft HPC Pack i zasoby, które określisz obliczeniowe dodatkowe okna. Jeśli dla obciążeń systemu Linux toodeploy klastra HPC Pack na platformie Azure, zobacz [utworzyć klaster HPC systemu Linux hello skrypt wdrożenia HPC Pack IaaS](../../linux/classic/hpcpack-cluster-powershell-script.md). Można również użyć toodeploy szablonu usługi Azure Resource Manager klastra HPC Pack. Przykłady można znaleźć [utworzyć klaster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) i [utworzyć klaster HPC z obrazem węzła niestandardowego obliczania](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Witaj skrypt programu PowerShell opisanych w tym artykule jest tworzony klaster Microsoft HPC Pack 2012 R2 na platformie Azure przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
> Ponadto skryptu hello opisane w tym artykule nie obsługuje HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Przykładowe pliki konfiguracji
W hello następujące przykłady, należy zastąpić własne wartości dla Twojego identyfikatora subskrypcji lub nazwy i nazwy usługi oraz konta hello.

### <a name="example-1"></a>Przykład 1
Witaj następującego pliku konfiguracji wdraża klaster HPC Pack węzła głównego z lokalnych baz danych i systemem operacyjnym Windows Server 2012 R2 hello pięć węzłów obliczeniowych. Wszystkie usługi w chmurze hello są tworzone bezpośrednio w hello lokalizacji zachodnie stany USA. węzła głównego Hello działa jako kontroler domeny w lesie domeny hello.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a>Przykład 2
Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny. klaster Hello ma 1 węzła głównego z lokalnych baz danych i 12 obliczeniowe węzłów o hello zastosować rozszerzenia BGInfo maszyny Wirtualnej.
Automatyczne instalowanie aktualizacji systemu Windows jest wyłączona dla wszystkich hello maszyn wirtualnych w lesie domeny hello. Wszystkie usługi w chmurze hello są tworzone bezpośrednio w lokalizacji Azja Wschodnia. węzły obliczeniowe Hello są tworzone trzy usługi w chmurze i kont magazynu trzy: *MyHPCCN 0001* za*MyHPCCN 0005* w *MyHPCCNService01* i  *mycnstorage01*; *MyHPCCN 0006* za*MyHPCCN0010* w *MyHPCCNService02* i *mycnstorage02*; i  *MyHPCCN-0011* za*MyHPCCN 0012* w *MyHPCCNService03* i *mycnstorage03*). węzły obliczeniowe Hello są tworzone na podstawie istniejącego obrazu prywatnej przechwytywane z węzła obliczeń. Witaj automatycznie zwiększyć lub zmniejszyć włączono usługę z domyślnymi zwiększyć lub zmniejszyć odstępach czasu.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
      </DomainController>
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a>Przykład 3
Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny. Witaj klastra zawiera jednego węzła głównego, jeden serwer bazy danych z dysku danych 500 GB, dwa węzły brokera zainstalowano system operacyjny Windows Server 2012 R2 hello oraz systemem operacyjnym Windows Server 2012 R2 hello pięć węzłów obliczeniowych. usługi w chmurze MyHPCCNService jest tworzony w grupie koligacji hello Hello *MyIBAffinityGroup*, a hello innych usług w chmurze są tworzone w grupie koligacji hello *MyAffinityGroup*. Witaj HPC interfejsu API REST harmonogramu dla zadania i portalu internetowego HPC są włączone na powitania węzła głównego.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a>Przykład 4
Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny. klaster Hello ma dwa węzła głównego z lokalnych baz danych, są tworzone dwa szablony Azure węzła i dla szablonu węzła Azure są tworzone trzy węzły Azure średni rozmiar *AzureTemplate1*. Plik skryptu działa na powitania węzła głównego po skonfigurowaniu hello węzła głównego.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* **Błąd "Sieci wirtualnej nie istnieje"** — Jeśli uruchomisz toodeploy skryptu hello wielu klastrów na platformie Azure jednocześnie w ramach jednej subskrypcji, co najmniej jednego wdrożenia może działać z powodu błędu hello "sieci wirtualnej *sieci wirtualnej\_nazwa* nie istnieje".
  Jeśli ten błąd występuje, uruchom skrypt hello ponownie dla wdrożenia hello nie powiodło się.
* **Problem podczas uzyskiwania dostępu do hello Internet z hello sieci wirtualnej platformy Azure** — Jeśli utworzyć klaster z nowego kontrolera domeny za pomocą skryptu wdrażania hello, lub ręcznie podwyższyć poziom kontrolera toodomain wirtualna węzła głównego, mogą wystąpić problemy Łączenie hello maszyn wirtualnych toohello Internet. Ten problem może wystąpić, jeśli usługa przesyłania dalej serwera DNS jest automatycznie konfigurowane na kontrolerze domeny hello, a usługi przesyłania dalej serwera DNS nie jest rozpoznawane poprawnie.
  
    toowork rozwiązać ten problem, zaloguj się na kontrolerze domeny toohello i ustawienia konfiguracji usługi przesyłania dalej albo usuń hello lub skonfiguruj prawidłową usługę przesyłania dalej serwera DNS. tooconfigure to ustawienie, w Menedżerze serwera kliknij **narzędzia** >
    **DNS** tooopen Menedżera DNS, a następnie kliknij dwukrotnie **usług przesyłania dalej**.
* **Problem z dostępem do sieci RDMA z maszyn wirtualnych obliczeniowych** — Jeśli Dodawanie obliczeń do systemu Windows Server lub węzeł brokera rozmiar maszyn wirtualnych przy użyciu z funkcją RDMA, takich jak A8 i A9, mogą wystąpić problemy z połączeniem tych maszyn wirtualnych toohello RDMA aplikacji sieci. Jedną z przyczyn się, że ten problem występuje, to jeśli hello HpcVmDrivers rozszerzenia nie jest zainstalowany prawidłowo po dodaniu klastra toohello hello maszyn wirtualnych. Na przykład rozszerzenie mogła zostać zablokowana na powitania stan instalacji.
  
    toowork rozwiązać ten problem, pierwszy stan rozszerzenia hello na maszynach wirtualnych hello hello wyboru. Jeśli nie zainstalowano poprawnie rozszerzenia hello, spróbuj usunąć hello węzłów z klastra HPC hello, a następnie ponownie Dodaj hello węzłów. Na przykład można dodać węzła obliczeniowego maszyn wirtualnych, uruchamiając skrypt HpcIaaSNode.ps1 Dodaj hello na powitania węzła głównego.

## <a name="next-steps"></a>Następne kroki
* Spróbuj uruchomić test obciążenia w klastrze hello. Na przykład zobacz hello HPC Pack [Wprowadzenie — przewodnik](https://technet.microsoft.com/library/jj884144).
* Dla hello samouczek tooscript wdrażanie klastra i uruchom obciążenia HPC, zobacz [wprowadzenie do klastra HPC Pack w obciążeń programu Excel i SOA Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Spróbuj toostart narzędzia HPC Pack, Zatrzymaj, Dodaj i usuń węzły obliczeniowe z klastra, którą utworzysz. Zobacz [Zarządzaj węzłów obliczeniowych w HPC Pack klastra w systemie Azure](hpcpack-cluster-node-manage.md).
* tooget Konfigurowanie klastra toohello zadania toosubmit z komputera lokalnego, zobacz [klastra HPC przesyłania zadań na lokalnym komputerze tooan HPC Pack na platformie Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

