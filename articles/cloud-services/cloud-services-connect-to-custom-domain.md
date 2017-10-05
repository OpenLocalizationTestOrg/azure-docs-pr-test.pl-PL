---
title: "Połączenie usługi w chmurze z kontrolerem domeny niestandardowe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć role sieć web/proces roboczy na domenę niestandardową AD przy użyciu programu PowerShell i rozszerzenia domeny usługi AD"
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="f1306-103">Łączenie role usługi w chmurze Azure z niestandardowego kontrolera domeny AD hostowana na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f1306-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="f1306-104">Sieć wirtualną (VNet) zostanie najpierw skonfigurowanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f1306-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="f1306-105">Następnie dodamy kontroler domeny usługi Active Directory (obsługiwanych na maszynie wirtualnej platformy Azure) do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f1306-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="f1306-106">Następnie firma Microsoft będzie Dodaj istniejące role usługi w chmurze do wstępnie utworzone sieci wirtualnej, a następnie podłącz je do kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="f1306-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="f1306-107">Początek, kilka rzeczy, które należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="f1306-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="f1306-108">W tym samouczku korzysta z programu PowerShell, upewnij się, że masz programu Azure PowerShell zainstalowana i rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="f1306-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="f1306-109">Aby uzyskać pomoc dotyczącą konfigurowania programu Azure PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1306-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="f1306-110">Swoich wystąpień kontroler domeny usługi AD i roli sieć Web/proces roboczy muszą znajdować się w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f1306-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="f1306-111">Wykonaj ten krok po kroku, a jeśli wystąpiły problemy, pozostaw komentarz na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f1306-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="f1306-112">Ktoś będzie zająć się (tak, odczytano komentarzy).</span><span class="sxs-lookup"><span data-stu-id="f1306-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="f1306-113">Sieć, do którego odwołuje się przez usługę w chmurze musi być **klasycznej sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="f1306-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="f1306-114">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f1306-114">Create a Virtual Network</span></span>
<span data-ttu-id="f1306-115">Można utworzyć sieć wirtualną na platformie Azure przy użyciu portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1306-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="f1306-116">W tym samouczku używamy środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1306-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="f1306-117">Aby utworzyć sieć wirtualną przy użyciu portalu Azure, zobacz [tworzenie sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="f1306-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="f1306-118">Utworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f1306-118">Create a Virtual Machine</span></span>
<span data-ttu-id="f1306-119">Po zakończeniu konfigurowania sieci wirtualnej, należy utworzyć kontroler domeny usługi AD.</span><span class="sxs-lookup"><span data-stu-id="f1306-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="f1306-120">W tym samouczku firma Microsoft będzie Trwa konfigurowanie kontrolera domeny AD na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f1306-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="f1306-121">Aby to zrobić, utwórz maszynę wirtualną za pomocą programu PowerShell przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="f1306-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="f1306-122">Podwyższ poziom maszyny wirtualnej do poziomu kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="f1306-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="f1306-123">Aby skonfigurować maszynę wirtualną jako kontroler domeny usługi AD, należy zalogować się do maszyny Wirtualnej i skonfigurować go.</span><span class="sxs-lookup"><span data-stu-id="f1306-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="f1306-124">Aby zalogować się do maszyny Wirtualnej, można pobrać pliku RDP za pomocą programu PowerShell, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="f1306-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="f1306-125">Gdy użytkownik jest zalogowany do maszyny Wirtualnej, konfigurowanie maszyny wirtualnej jako kontrolera domeny usługi AD wykonując przewodnik krok po kroku na [sposobu konfigurowania klienta kontroler domeny usługi AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1306-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="f1306-126">Dodaj do sieci wirtualnej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="f1306-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="f1306-127">Następnie należy dodać do nowej sieci wirtualnej wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="f1306-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="f1306-128">Aby to zrobić, należy zmodyfikować z cscfg usługi chmury przez dodanie odpowiednich sekcji do Twojej cscfg przy użyciu programu Visual Studio lub dowolnego edytora.</span><span class="sxs-lookup"><span data-stu-id="f1306-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="f1306-129">Następnie skompilowanie projektu usługi w chmurze i wdrożyć go na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f1306-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="f1306-130">Aby uzyskać pomoc dotyczącą wdrażania pakietu usługi w chmurze na platformie Azure, zobacz [sposobu tworzenia i wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="f1306-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="f1306-131">Połącz się z domeną role sieć web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="f1306-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="f1306-132">Po wdrożeniu projekt usługi w chmurze na platformie Azure nawiązać niestandardowej domeny AD za pomocą rozszerzenia domeny AD wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="f1306-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="f1306-133">Dodaj rozszerzenie AD domeny do istniejącego wdrożenia usługi w chmurze i przyłączania do domeny niestandardowe, wykonaj następujące polecenia w programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1306-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="f1306-134">A to wszystko.</span><span class="sxs-lookup"><span data-stu-id="f1306-134">And that's it.</span></span>

<span data-ttu-id="f1306-135">Usługi w chmurze powinny należeć do kontrolera domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="f1306-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="f1306-136">Jeśli chcesz dowiedzieć się więcej o różnych opcjach konfigurowania rozszerzenia domeny AD, korzystanie z pomocy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1306-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="f1306-137">Kilka przykładów wykonaj:</span><span class="sxs-lookup"><span data-stu-id="f1306-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
