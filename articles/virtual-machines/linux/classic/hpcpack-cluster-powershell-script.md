---
title: aaaPowerShell skryptu toodeploy klastra HPC systemu Linux | Dokumentacja firmy Microsoft
description: "Uruchom toodeploy skryptu środowiska PowerShell klastra Linux HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Tworzenie klastra wysokiej wydajności (HPC) systemu Linux przy użyciu skryptu wdrażania hello HPC Pack IaaS
Uruchom hello HPC Pack IaaS wdrożenia programu PowerShell skryptu toodeploy całego klastra HPC Pack 2012 R2 dla systemu Linux obciążeń na maszynach wirtualnych platformy Azure. Witaj klaster składa się z węzłem głównym przyłączonych do usługi Active Directory systemem Windows Server i Microsoft HPC Pack i węzły obliczeniowe, które Uruchom jedno z hello dystrybucje systemu Linux obsługiwane przez HPC Pack. Jeśli chcesz toodeploy klastra HPC Pack w obciążeń Azure dla systemu Windows, zobacz [utworzyć klaster HPC systemu Windows hello skrypt wdrożenia HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Można również użyć toodeploy szablonu usługi Azure Resource Manager klastra HPC Pack. Na przykład zobacz [utworzyć klaster HPC z węzłami obliczeniowymi Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Witaj skrypt programu PowerShell opisanych w tym artykule jest tworzony klaster Microsoft HPC Pack 2012 R2 na platformie Azure przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
> Ponadto skryptu hello opisane w tym artykule nie obsługuje HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Przykładowy plik konfiguracji
Witaj następującego pliku konfiguracji tworzy kontroler domeny i lasu domen i wdraża klastra HPC Pack, który ma jednego węzła głównego z lokalnych baz danych i węzły obliczeniowe Linux 10. Wszystkie usługi w chmurze hello są tworzone bezpośrednio w lokalizacji Azja Wschodnia hello. Hello Linux węzły obliczeniowe są tworzone w dwóch usług w chmurze i dwóch kont magazynu (to znaczy *MyLnxCN 0001* do *MyLnxCN 0005* w *MyLnxCNService01* i *mylnxstorage01*, i *MyLnxCN 0006* do *MyLnxCN 0010* w *MyLnxCNService02* i *mylnxstorage02* ). węzły obliczeniowe Hello są tworzone na podstawie obrazu OpenLogic CentOS Linux w wersji 7.0. 

Zastąp wartości hello nazwy usługi oraz konta i nazwę subskrypcji.

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
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>Rozwiązywanie problemów
* **Błąd "Sieci wirtualnej nie istnieje"**. Po uruchomieniu hello HPC Pack IaaS wdrożenia skryptu toodeploy wielu klastrów na platformie Azure jednocześnie w ramach jednej subskrypcji, co najmniej jednego wdrożenia może działać z powodu błędu hello "sieci wirtualnej *sieci wirtualnej\_nazwa* nie istnieje".
  Jeśli ten błąd występuje, uruchom ponownie skrypt hello wdrożenia hello nie powiodło się.
* **Problem podczas uzyskiwania dostępu do hello Internet z hello sieci wirtualnej platformy Azure**. Jeśli utworzysz klaster HPC Pack z nowego kontrolera domeny za pomocą skryptu wdrażania hello lub ręczne podwyższenie węzła głównego kontrolera toodomain maszyny Wirtualnej, mogą wystąpić problemy z połączeniem maszyn wirtualnych hello w toohello sieci wirtualnej platformy Azure hello Internet. Może to występować, jeśli usługa przesyłania dalej serwera DNS jest automatycznie konfigurowane na kontrolerze domeny hello, a usługi przesyłania dalej serwera DNS nie jest rozpoznawane poprawnie.
  
    toowork rozwiązać ten problem, zaloguj się na kontrolerze domeny toohello i ustawienia konfiguracji usługi przesyłania dalej albo usuń hello lub skonfiguruj prawidłową usługę przesyłania dalej serwera DNS. toodo, w Menedżerze serwera kliknij **narzędzia** > **DNS** tooopen Menedżera DNS, a następnie kliknij dwukrotnie **usług przesyłania dalej**.

## <a name="next-steps"></a>Następne kroki
* Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) uzyskać informacji o obsługiwanych dystrybucjach systemu Linux, przenoszenia danych i przesyłanie zadań tooan HPC Pack klastra z systemem Linux węzły obliczeniowe.
* Samouczki hello skryptu toocreate klastra i uruchom obciążenia HPC systemu Linux zobacz:
  * [Uruchamianie NAMD z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure](hpcpack-cluster-namd.md)
  * [Uruchamianie OpenFOAM z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure](hpcpack-cluster-openfoam.md)
  * [Uruchomienie GWIAZDĘ — CCM + z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure](hpcpack-cluster-starccm.md)

