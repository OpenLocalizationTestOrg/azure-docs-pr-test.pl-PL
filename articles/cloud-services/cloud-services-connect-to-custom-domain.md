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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="a2cf1-103">Łączenie niestandardowe tooa role usługi w chmurze Azure, kontroler domeny AD hostowana na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a2cf1-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="a2cf1-104">Sieć wirtualną (VNet) zostanie najpierw skonfigurowanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="a2cf1-105">Następnie dodamy toohello kontrolera domeny Active Directory (obsługiwanych na maszynie wirtualnej platformy Azure) sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="a2cf1-106">Następnie firma Microsoft będzie Dodawanie istniejących toohello chmury usługi ról, wstępnie utworzone sieci wirtualnej, a następnie połącz je toohello kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="a2cf1-107">Początek, kilka z tookeep rzeczy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="a2cf1-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="a2cf1-108">W tym samouczku korzysta z programu PowerShell, dlatego upewnij się, należy mieć zainstalowany program Azure PowerShell i gotowe toogo.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="a2cf1-109">tooget pomoc dotyczącą konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2cf1-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="a2cf1-110">Swoich wystąpień kontroler domeny usługi AD i roli sieć Web/proces roboczy musi toobe w hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="a2cf1-111">Wykonaj ten przewodnik krok po kroku, a jeśli wystąpiły problemy, pozostaw komentarz na końcu hello hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="a2cf1-112">Ktoś będzie odzyskanie tooyou (tak, odczytano komentarzy).</span><span class="sxs-lookup"><span data-stu-id="a2cf1-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="a2cf1-113">musi być Hello sieci, która odwołuje się do niego usługa w chmurze hello **klasycznej sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="a2cf1-114">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a2cf1-114">Create a Virtual Network</span></span>
<span data-ttu-id="a2cf1-115">Można utworzyć sieć wirtualną na platformie Azure przy użyciu hello portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="a2cf1-116">W tym samouczku używamy środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="a2cf1-117">toocreate sieci wirtualnych za pomocą funkcji hello Azure portalu, zobacz [tworzenie sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a2cf1-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="a2cf1-118">Utworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a2cf1-118">Create a Virtual Machine</span></span>
<span data-ttu-id="a2cf1-119">Po zakończeniu konfigurowania hello sieci wirtualnej, należy toocreate kontrolera domeny usługi AD.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="a2cf1-120">W tym samouczku firma Microsoft będzie Trwa konfigurowanie kontrolera domeny AD na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="a2cf1-121">toodo, utwórz maszynę wirtualną za pomocą programu PowerShell przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2cf1-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="a2cf1-122">Podwyższ poziom tooa Twojej maszyny wirtualnej kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="a2cf1-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="a2cf1-123">Witaj tooconfigure maszyny wirtualnej jako kontrolera domeny usługi AD, należy toolog w toohello maszyny Wirtualnej, a jest skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="a2cf1-124">toolog w toohello maszyny Wirtualnej, można uzyskać plik RDP hello za pomocą programu PowerShell, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2cf1-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="a2cf1-125">Po zalogowaniu toohello maszyny Wirtualnej skonfigurować maszynę wirtualną jako kontroler domeny usługi AD przez następujące hello przewodnik krok po kroku na [jak tooset Twojego odbiorców kontroler domeny usługi AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2cf1-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="a2cf1-126">Dodaj użytkownika usługi w chmurze toohello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a2cf1-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="a2cf1-127">Następnie należy tooadd Twojego toohello wdrożenia usługi chmury nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="a2cf1-128">toodo, zmodyfikować cscfg usługi z chmury, dodając cscfg tooyour odpowiednich sekcji hello przy użyciu programu Visual Studio lub hello dowolnego edytora.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

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

<span data-ttu-id="a2cf1-129">Następnie skompilowanie projektu usługi w chmurze i wdróż je tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="a2cf1-130">Zobacz tooget pomoc dotyczącą wdrażania z pakietu tooAzure usług chmury [jak tooCreate i wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="a2cf1-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="a2cf1-131">Połącz domenę toohello role sieć web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="a2cf1-132">Po wdrożeniu projekt usługi w chmurze na platformie Azure, Połącz domenę toohello AD niestandardowego wystąpienia roli przy użyciu hello rozszerzenia domeny AD.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="a2cf1-133">tooadd hello rozszerzenia domeny AD tooyour istniejące wdrożenie usług chmury i Dołącz do domeny niestandardowej hello, wykonaj następujące polecenia w programie PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a2cf1-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

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

<span data-ttu-id="a2cf1-134">A to wszystko.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-134">And that's it.</span></span>

<span data-ttu-id="a2cf1-135">Usługi w chmurze powinny być tooyour dołączonego do kontrolera domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="a2cf1-136">Jeśli chcesz toolearn hello więcej informacji na temat różnych opcji dostępnych dla sposób pomóc tooconfigure rozszerzenia domeny AD, hello Użyj programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2cf1-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="a2cf1-137">Kilka przykładów wykonaj:</span><span class="sxs-lookup"><span data-stu-id="a2cf1-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
