---
title: Instalowanie programu Symantec Endpoint Protection w systemie Windows maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Informacje o sposobie instalowania i konfigurowania rozszerzeń zabezpieczeń firmy Symantec Endpoint Protection w nowej lub istniejącej maszyny Wirtualnej platformy Azure utworzonych za pomocą klasycznego modelu wdrożenia."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="73478-103">Jak zainstalować i skonfigurować rozwiązanie Symantec Endpoint Protection na maszynie wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="73478-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="73478-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="73478-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="73478-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="73478-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="73478-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73478-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="73478-107">W tym artykule przedstawiono sposób instalowania i konfigurowania klienta programu Symantec Endpoint Protection na istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server.</span><span class="sxs-lookup"><span data-stu-id="73478-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="73478-108">Ta pełnego klienta zawiera usług, takich jak wirusów i ochrony przed programami szpiegującymi, zapory i zapobiegania nieautoryzowanego dostępu.</span><span class="sxs-lookup"><span data-stu-id="73478-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="73478-109">Klient jest instalowany jako rozszerzenia zabezpieczeń przy użyciu agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73478-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="73478-110">Jeśli masz istniejącą subskrypcję od firmy Symantec dla rozwiązania lokalnego, można użyć go do ochrony maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73478-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="73478-111">Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="73478-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="73478-112">Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz [Symantec Endpoint Protection na platformie Azure przez firmę Microsoft][Symantec].</span><span class="sxs-lookup"><span data-stu-id="73478-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="73478-113">Ta strona zawiera również linki do informacji dotyczących licencjonowania i instrukcje dotyczące instalowania klienta, jeśli już masz klienta firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="73478-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="73478-114">Zainstaluj Symantec Endpoint Protection na istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="73478-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="73478-115">Przed rozpoczęciem, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="73478-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="73478-116">Moduł Azure PowerShell, wersja 0.8.2 lub nowszym, na komputerze pracy.</span><span class="sxs-lookup"><span data-stu-id="73478-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="73478-117">Można sprawdzić wersji programu Azure PowerShell, który został zainstalowany z **azure Get-Module | wersja formatu tabeli** polecenia.</span><span class="sxs-lookup"><span data-stu-id="73478-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="73478-118">Aby uzyskać instrukcje i łącza do najnowszej wersji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="73478-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="73478-119">Zaloguj się przy użyciu subskrypcji platformy Azure `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="73478-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="73478-120">Agent maszyny Wirtualnej uruchomione na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73478-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="73478-121">Po pierwsze sprawdzenie, czy Agent maszyny Wirtualnej jest już zainstalowany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73478-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="73478-122">Wypełnij pola Nazwa usługi w chmurze i Nazwa maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora.</span><span class="sxs-lookup"><span data-stu-id="73478-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="73478-123">Zastąp wszystko w obrębie oferty, w tym < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="73478-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="73478-124">Jeśli nie znasz nazwy maszyny wirtualnej i usługi w chmurze, uruchom **Get AzureVM** Aby wyświetlić listę nazw dla wszystkich maszyn wirtualnych w ramach Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="73478-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="73478-125">Jeśli **hosta zapisu** polecenie wyświetla **True**, Agent maszyny Wirtualnej jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="73478-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="73478-126">Jeśli Wyświetla **False**, zobacz instrukcje i łącze do pobrania w Azure blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="73478-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="73478-127">Jeśli jest zainstalowany Agent maszyny Wirtualnej, uruchom następujące polecenia, aby zainstalować agenta programu Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="73478-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="73478-128">Aby sprawdzić, czy rozszerzenie zabezpieczeń firmy Symantec został zainstalowany i jest aktualny:</span><span class="sxs-lookup"><span data-stu-id="73478-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="73478-129">Zaloguj się do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73478-129">Log on to the virtual machine.</span></span> <span data-ttu-id="73478-130">Aby uzyskać instrukcje, zobacz [jak Zaloguj się do maszyny wirtualnej systemem Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="73478-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="73478-131">Dla systemu Windows Server 2008 R2, kliknij przycisk **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="73478-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="73478-132">Dla systemu Windows Server 2012 lub Windows Server 2012 R2, na ekranie startowym wpisz **firmy Symantec**, a następnie kliknij przycisk **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="73478-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="73478-133">Z **stan** karcie **stan Symantec Endpoint Protection** okna, stosowania aktualizacji lub uruchom ponownie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="73478-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73478-134">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="73478-134">Additional resources</span></span>
<span data-ttu-id="73478-135">[Jak Zaloguj się do maszyny wirtualnej z systemem Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="73478-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="73478-136">[Maszyna wirtualna platformy Azure rozszerzeń i funkcji][Ext]</span><span class="sxs-lookup"><span data-stu-id="73478-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
