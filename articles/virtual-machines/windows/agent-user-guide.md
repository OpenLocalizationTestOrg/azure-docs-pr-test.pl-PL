---
title: "Omówienie agenta maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Omówienie agenta maszyny wirtualnej platformy Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: 24ad2c2d2872f844e32d3fae559683c3d992bd00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="f0395-103">Omówienie usługi Azure agenta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0395-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="f0395-104">Agent maszyny wirtualnej programu Microsoft Azure (AM Agent) jest procesem zabezpieczonych, lekkie, który zarządza wirtualna interakcji z kontrolerem sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-104">The Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="f0395-105">Agent maszyny Wirtualnej ma podstawową rolą włączenie i wykonywania rozszerzenia maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="f0395-106">Włączanie rozszerzenia maszyny Wirtualnej po konfiguracji wdrożenia maszyn wirtualnych, takie jak instalowanie i konfigurowanie oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="f0395-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="f0395-107">Rozszerzenia maszyn wirtualnych również włączyć funkcje odzyskiwania, np. zresetowania hasła administracyjnego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="f0395-108">Bez agenta maszyny Wirtualnej Azure nie można uruchomić rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="f0395-109">Ten dokument zawiera szczegóły dotyczące instalacji, wykrywania i usuwania agenta maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="f0395-110">Zainstaluj agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0395-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="f0395-111">Obraz w galerii Azure</span><span class="sxs-lookup"><span data-stu-id="f0395-111">Azure gallery image</span></span>

<span data-ttu-id="f0395-112">Agent maszyny Wirtualnej Azure jest instalowany domyślnie wdrażana z obrazu galerii Azure maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f0395-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="f0395-113">Podczas wdrażania obrazu galerii Azure z portalu, programu PowerShell, interfejsu wiersza polecenia lub szablonu usługi Azure Resource Manager, jest również instalowany Agent maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="f0395-114">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="f0395-114">Manual installation</span></span>

<span data-ttu-id="f0395-115">Agent maszyny Wirtualnej systemu Windows można ręcznie zainstalować za pomocą pakietu Instalatora Windows.</span><span class="sxs-lookup"><span data-stu-id="f0395-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="f0395-116">Instalacja ręczna może być konieczne, podczas tworzenia obrazu niestandardowego maszyny wirtualnej, który zostanie wdrożony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="f0395-117">Aby ręcznie zainstalować agenta maszyny Wirtualnej systemu Windows, Pobierz Instalator agenta maszyny Wirtualnej z tej lokalizacji [Pobierz agenta maszyny Wirtualnej systemu Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="f0395-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="f0395-118">Agent maszyny Wirtualnej mogą być instalowane przez dwukrotne kliknięcie pliku Instalatora windows.</span><span class="sxs-lookup"><span data-stu-id="f0395-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="f0395-119">Automatyczna lub z instalacji nienadzorowanej instalacji agenta maszyny Wirtualnej uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="f0395-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="f0395-120">Wykryj agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0395-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="f0395-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0395-121">PowerShell</span></span>

<span data-ttu-id="f0395-122">Moduł programu PowerShell usługi Azure Resource Manager można pobrać informacji o maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="f0395-123">Uruchomiona `Get-AzureRmVM` zwraca dość nieco informacji w tym stan inicjowania obsługi administracyjnej dla agenta maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f0395-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="f0395-124">Poniżej znajduje się tylko ich podzbiór `Get-AzureRmVM` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f0395-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="f0395-125">Powiadomienie `ProvisionVMAgent` zagnieżdżona właściwość `OSProfile`, ta właściwość służy do określenia, czy agent maszyny Wirtualnej został wdrożony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="f0395-126">Poniższy skrypt może służyć do zwrócenia listę krótkie nazwy maszyn wirtualnych i stan agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="f0395-127">Ręczne wykrywania</span><span class="sxs-lookup"><span data-stu-id="f0395-127">Manual Detection</span></span>

<span data-ttu-id="f0395-128">Po zalogowaniu się do maszyny Wirtualnej systemu Windows Azure, Menedżer zadań może służyć do sprawdzenia uruchomionych procesów.</span><span class="sxs-lookup"><span data-stu-id="f0395-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="f0395-129">Aby sprawdzić, czy Agent maszyny Wirtualnej Azure, otwórz Menedżera zadań > kliknij kartę szczegółów, a następnie wyszukaj nazwę procesu `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="f0395-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="f0395-130">Obecność tego procesu wskazuje, czy agent maszyny Wirtualnej jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="f0395-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="f0395-131">Uaktualnienie agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0395-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="f0395-132">Azure VM Agent dla systemu Windows zostanie automatycznie uaktualniony.</span><span class="sxs-lookup"><span data-stu-id="f0395-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="f0395-133">Podczas wdrażania nowych maszyn wirtualnych na platformie Azure, otrzymają najnowsza wersja agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="f0395-134">Niestandardowe obrazy maszyny Wirtualnej należy ręcznie zaktualizować Aby dołączyć nowy agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0395-134">Custom VM images should be manually updated to include the new VM agent.</span></span>