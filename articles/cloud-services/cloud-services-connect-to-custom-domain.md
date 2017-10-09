---
title: "aaaConnect tooa usługi w chmurze niestandardowego kontrolera domeny | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect niestandardowe tooa role sieć web/proces roboczy domeny AD przy użyciu programu PowerShell i rozszerzenia domeny usługi AD"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Łączenie niestandardowe tooa role usługi w chmurze Azure, kontroler domeny AD hostowana na platformie Azure
Sieć wirtualną (VNet) zostanie najpierw skonfigurowanie na platformie Azure. Następnie dodamy toohello kontrolera domeny Active Directory (obsługiwanych na maszynie wirtualnej platformy Azure) sieci wirtualnej. Następnie firma Microsoft będzie Dodawanie istniejących toohello chmury usługi ról, wstępnie utworzone sieci wirtualnej, a następnie połącz je toohello kontrolera domeny.

Początek, kilka z tookeep rzeczy pamiętać:

1. W tym samouczku korzysta z programu PowerShell, dlatego upewnij się, należy mieć zainstalowany program Azure PowerShell i gotowe toogo. tooget pomoc dotyczącą konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
2. Swoich wystąpień kontroler domeny usługi AD i roli sieć Web/proces roboczy musi toobe w hello sieci wirtualnej.

Wykonaj ten przewodnik krok po kroku, a jeśli wystąpiły problemy, pozostaw komentarz na końcu hello hello artykułu. Ktoś będzie odzyskanie tooyou (tak, odczytano komentarzy).

musi być Hello sieci, która odwołuje się do niego usługa w chmurze hello **klasycznej sieci wirtualnej**.

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Można utworzyć sieć wirtualną na platformie Azure przy użyciu hello portalu Azure lub programu PowerShell. W tym samouczku używamy środowiska PowerShell. toocreate sieci wirtualnych za pomocą funkcji hello Azure portalu, zobacz [tworzenie sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Utworzenie maszyny wirtualnej
Po zakończeniu konfigurowania hello sieci wirtualnej, należy toocreate kontrolera domeny usługi AD. W tym samouczku firma Microsoft będzie Trwa konfigurowanie kontrolera domeny AD na maszynie wirtualnej platformy Azure.

toodo, utwórz maszynę wirtualną za pomocą programu PowerShell przy użyciu hello następującego polecenia:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Podwyższ poziom tooa Twojej maszyny wirtualnej kontrolera domeny
Witaj tooconfigure maszyny wirtualnej jako kontrolera domeny usługi AD, należy toolog w toohello maszyny Wirtualnej, a jest skonfigurowana.

toolog w toohello maszyny Wirtualnej, można uzyskać plik RDP hello za pomocą programu PowerShell, hello Użyj następującego polecenia:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Po zalogowaniu toohello maszyny Wirtualnej skonfigurować maszynę wirtualną jako kontroler domeny usługi AD przez następujące hello przewodnik krok po kroku na [jak tooset Twojego odbiorców kontroler domeny usługi AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Dodaj użytkownika usługi w chmurze toohello sieci wirtualnej
Następnie należy tooadd Twojego toohello wdrożenia usługi chmury nowej sieci wirtualnej. toodo, zmodyfikować cscfg usługi z chmury, dodając cscfg tooyour odpowiednich sekcji hello przy użyciu programu Visual Studio lub hello dowolnego edytora.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

Następnie skompilowanie projektu usługi w chmurze i wdróż je tooAzure. Zobacz tooget pomoc dotyczącą wdrażania z pakietu tooAzure usług chmury [jak tooCreate i wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Połącz domenę toohello role sieć web/proces roboczy.
Po wdrożeniu projekt usługi w chmurze na platformie Azure, Połącz domenę toohello AD niestandardowego wystąpienia roli przy użyciu hello rozszerzenia domeny AD. tooadd hello rozszerzenia domeny AD tooyour istniejące wdrożenie usług chmury i Dołącz do domeny niestandardowej hello, wykonaj następujące polecenia w programie PowerShell hello:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

A to wszystko.

Usługi w chmurze powinny być tooyour dołączonego do kontrolera domeny niestandardowej. Jeśli chcesz toolearn hello więcej informacji na temat różnych opcji dostępnych dla sposób pomóc tooconfigure rozszerzenia domeny AD, hello Użyj programu PowerShell. Kilka przykładów wykonaj:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
