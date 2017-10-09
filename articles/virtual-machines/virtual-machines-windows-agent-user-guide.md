---
title: "Omówienie agenta maszyny wirtualnej aaaAzure | Dokumentacja firmy Microsoft"
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
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="0d2df-103">Omówienie usługi Azure agenta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0d2df-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="0d2df-104">Hello agenta maszyny wirtualnej programu Microsoft Azure (Agent maszyny Wirtualnej) jest zabezpieczonych, lekkie procesu, który zarządza wirtualna interakcji z hello Azure kontrolera sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="0d2df-105">Witaj agenta maszyny Wirtualnej ma podstawową rolą włączenie i wykonywania rozszerzenia maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2df-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="0d2df-106">Włączanie rozszerzenia maszyny Wirtualnej po konfiguracji wdrożenia maszyn wirtualnych, takie jak instalowanie i konfigurowanie oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="0d2df-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="0d2df-107">Rozszerzenia maszyn wirtualnych również włączyć funkcje odzyskiwania, np. zresetowania hasła administracyjnego hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="0d2df-108">Bez hello Agent maszyny Wirtualnej nie można uruchomić rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="0d2df-109">Ten dokument zawiera szczegóły dotyczące instalacji, wykrywanie i usuwanie hello agenta maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2df-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="0d2df-110">Zainstaluj hello agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0d2df-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="0d2df-111">Obraz w galerii Azure</span><span class="sxs-lookup"><span data-stu-id="0d2df-111">Azure gallery image</span></span>

<span data-ttu-id="0d2df-112">Hello Agent maszyny Wirtualnej jest instalowana domyślnie na żadnej maszyny wirtualnej systemu Windows wdrożone z obrazu w galerii Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2df-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="0d2df-113">Podczas wdrażania obrazu galerii Azure z hello portalu, programu PowerShell, interfejsu wiersza polecenia lub szablonu usługi Azure Resource Manager, można zainstalować hello jest również Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="0d2df-114">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="0d2df-114">Manual installation</span></span>

<span data-ttu-id="0d2df-115">agent maszyny Wirtualnej systemu Windows Hello można ręcznie zainstalować za pomocą pakietu Instalatora Windows.</span><span class="sxs-lookup"><span data-stu-id="0d2df-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="0d2df-116">Instalacja ręczna może być konieczne, podczas tworzenia obrazu niestandardowego maszyny wirtualnej, który zostanie wdrożony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2df-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="0d2df-117">toomanually hello Zainstaluj agenta maszyny Wirtualnej systemu Windows, Pobierz Instalator agenta maszyny Wirtualnej hello z tej lokalizacji [Pobierz agenta maszyny Wirtualnej systemu Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="0d2df-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="0d2df-118">Witaj agenta maszyny Wirtualnej mogą być instalowane przez dwukrotne kliknięcie pliku Instalatora windows hello.</span><span class="sxs-lookup"><span data-stu-id="0d2df-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="0d2df-119">Automatyczna lub z instalacji nienadzorowanej instalacji agenta maszyny Wirtualnej hello Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="0d2df-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="0d2df-120">Wykryj hello agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0d2df-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="0d2df-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d2df-121">PowerShell</span></span>

<span data-ttu-id="0d2df-122">Moduł programu PowerShell usługi Azure Resource Manager Hello może być używane tooretrieve informacji o maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2df-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="0d2df-123">Uruchomiona `Get-AzureRmVM` zwraca dość nieco informacji w tym hello udostępniania stanu hello Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="0d2df-124">Witaj poniżej znajduje się tylko podzbiór hello `Get-AzureRmVM` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0d2df-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="0d2df-125">Powiadomienie hello `ProvisionVMAgent` zagnieżdżona właściwość `OSProfile`, ta właściwość może być toodetermine używane, jeśli hello agenta maszyny Wirtualnej został wdrożony toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="0d2df-126">Witaj następującego skryptu może być używane tooreturn listę krótkie nazwy maszyn wirtualnych i stan hello hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="0d2df-127">Ręczne wykrywania</span><span class="sxs-lookup"><span data-stu-id="0d2df-127">Manual Detection</span></span>

<span data-ttu-id="0d2df-128">Gdy zalogowany tooa maszyny Wirtualnej systemu Windows Azure, Menedżer zadań mogą być używane tooexamine uruchomionych procesów.</span><span class="sxs-lookup"><span data-stu-id="0d2df-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="0d2df-129">toocheck dla hello agenta maszyny Wirtualnej Azure, otwórz Menedżera zadań > kliknij kartę Szczegóły hello i wyszukaj nazwę procesu `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="0d2df-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="0d2df-130">obecność Hello tego procesu wskazuje, że hello agenta maszyny Wirtualnej jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="0d2df-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="0d2df-131">Witaj uaktualniania agenta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0d2df-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="0d2df-132">Hello Azure VM Agent dla systemu Windows zostanie automatycznie uaktualniony.</span><span class="sxs-lookup"><span data-stu-id="0d2df-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="0d2df-133">Nowe maszyny wirtualne są wdrożone tooAzure, otrzymają hello najnowsza wersja agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="0d2df-134">Niestandardowe obrazy maszyny Wirtualnej należy ręcznie zaktualizowanych tooinclude hello nowego agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d2df-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
