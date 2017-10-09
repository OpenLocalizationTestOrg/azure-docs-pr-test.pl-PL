---
title: aaaInstall Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfigurować rozszerzenia zabezpieczeń firmy Symantec Endpoint Protection hello na nowej lub istniejącej maszyny Wirtualnej Azure utworzone za pomocą hello klasycznego modelu wdrożenia."
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
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="ac2b9-103">Jak tooinstall i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ac2b9-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ac2b9-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac2b9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ac2b9-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ac2b9-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="ac2b9-107">W tym artykule opisano sposób tooinstall i skonfigurować powitania klienta firmy Symantec Endpoint Protection na istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="ac2b9-108">Ta pełnego klienta zawiera usług, takich jak wirusów i ochrony przed programami szpiegującymi, zapory i zapobiegania nieautoryzowanego dostępu.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="ac2b9-109">powitania klienta jest instalowany jako rozszerzenia zabezpieczeń przy użyciu hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="ac2b9-110">Jeśli masz istniejącą subskrypcję od firmy Symantec dla rozwiązania lokalnego umożliwia tooprotect maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="ac2b9-111">Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="ac2b9-112">Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz [Symantec Endpoint Protection na platformie Azure przez firmę Microsoft][Symantec].</span><span class="sxs-lookup"><span data-stu-id="ac2b9-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="ac2b9-113">Ta strona zawiera również linki toolicensing informacje i instrukcje dotyczące instalowania powitania klienta, jeśli już masz klienta firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="ac2b9-114">Zainstaluj Symantec Endpoint Protection na istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2b9-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="ac2b9-115">Przed rozpoczęciem należy hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ac2b9-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="ac2b9-116">Witaj modułu Azure PowerShell, wersja 0.8.2 lub nowszym, na komputerze pracy.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="ac2b9-117">Można sprawdzić wersji hello programu Azure PowerShell, zainstalowanym z hello **azure Get-Module | wersja formatu tabeli** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="ac2b9-118">Aby uzyskać instrukcje i toohello łącze najnowszej wersji, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="ac2b9-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="ac2b9-119">Zaloguj się przy użyciu subskrypcji platformy Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="ac2b9-120">Witaj agenta maszyny Wirtualnej z systemem hello maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="ac2b9-121">Po pierwsze sprawdzenie hello, że Agent maszyny Wirtualnej jest już zainstalowana na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="ac2b9-122">Wypełnij hello nazwa usługi w chmurze i nazwy maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora hello.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="ac2b9-123">Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="ac2b9-124">Jeśli nie znasz nazwy maszyny wirtualnej usługi chmury hello i uruchom **Get-AzureVM** toolist hello nazwy dla wszystkich maszyn wirtualnych w ramach Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="ac2b9-125">Jeśli hello **hosta zapisu** polecenie wyświetla **True**, hello jest zainstalowany Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="ac2b9-126">Jeśli Wyświetla **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello Azure wpis w blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="ac2b9-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="ac2b9-127">Jeśli hello agenta maszyny Wirtualnej jest zainstalowany, należy uruchomić te polecenia tooinstall hello Symantec Endpoint Protection agenta.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="ac2b9-128">tooverify, który hello rozszerzenia zabezpieczeń firmy Symantec został zainstalowany i jest aktualne:</span><span class="sxs-lookup"><span data-stu-id="ac2b9-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="ac2b9-129">Zaloguj się na toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="ac2b9-130">Aby uzyskać instrukcje, zobacz [jak tooLog na tooa maszyny wirtualnej z systemu Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="ac2b9-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="ac2b9-131">Dla systemu Windows Server 2008 R2, kliknij przycisk **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="ac2b9-132">Dla systemu Windows Server 2012 lub Windows Server 2012 R2 z ekranu startowego hello, wpisz **firmy Symantec**, a następnie kliknij przycisk **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="ac2b9-133">Z hello **stan** kartę hello **stan Symantec Endpoint Protection** okna, stosowania aktualizacji lub uruchom ponownie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="ac2b9-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac2b9-134">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ac2b9-134">Additional resources</span></span>
<span data-ttu-id="ac2b9-135">[Jak tooLog na tooa maszyny wirtualnej z systemu Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="ac2b9-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="ac2b9-136">[Maszyna wirtualna platformy Azure rozszerzeń i funkcji][Ext]</span><span class="sxs-lookup"><span data-stu-id="ac2b9-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
