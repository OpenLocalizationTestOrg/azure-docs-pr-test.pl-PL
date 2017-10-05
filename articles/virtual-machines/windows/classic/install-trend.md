---
title: "Zainstaluj Trend Micro głębokie zabezpieczeń na maszynie Wirtualnej | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób instalowania i konfigurowania zabezpieczeń Trend Micro na maszynie Wirtualnej utworzone za pomocą klasycznego modelu wdrożenia na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="8f217-103">Jak zainstalować i skonfigurować rozwiązanie Trend Micro Deep Security as a Service na maszynie wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8f217-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f217-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8f217-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8f217-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="8f217-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8f217-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f217-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="8f217-107">W tym artykule przedstawiono sposób instalowania i konfigurowania zabezpieczeń głębokie Trend Micro jako usługa na nowej lub istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8f217-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="8f217-108">Głębokie zabezpieczeń jako usługa obejmuje ochrony przed złośliwym oprogramowaniem, zapory systemu zapobiegania nieautoryzowanego dostępu i kontroli integralności.</span><span class="sxs-lookup"><span data-stu-id="8f217-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="8f217-109">Klient jest instalowany jako rozszerzenia zabezpieczeń, za pomocą agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8f217-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="8f217-110">Na nowej maszyny wirtualnej należy zainstalować głębokie agenta zabezpieczeń, jak Agent maszyny Wirtualnej jest tworzona automatycznie w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8f217-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="8f217-111">Istniejącej maszyny Wirtualnej utworzone przy użyciu klasycznego portalu Azure CLI lub środowiska PowerShell może nie mieć agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8f217-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="8f217-112">Dla istniejącej maszyny wirtualnej, która nie ma agenta maszyny Wirtualnej musisz pobrać i zainstalować ją najpierw.</span><span class="sxs-lookup"><span data-stu-id="8f217-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="8f217-113">W tym artykule opisano zarówno sytuacji.</span><span class="sxs-lookup"><span data-stu-id="8f217-113">This article covers both situations.</span></span>

<span data-ttu-id="8f217-114">Jeśli masz bieżącej subskrypcji z Trend Micro dla rozwiązania lokalnego, można użyć go w celu ochrony maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f217-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="8f217-115">Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="8f217-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="8f217-116">Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz blogu Trend Micro [zabezpieczeń firmy Microsoft Azure VM Agent rozszerzenia dla bezpośrednich](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="8f217-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="8f217-117">Zainstaluj agenta głębokie zabezpieczeń na nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8f217-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="8f217-118">[Portalu Azure](http://portal.azure.com) umożliwia instalowanie rozszerzenia zabezpieczeń Trend Micro, korzystając z obrazu z **Marketplace** można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8f217-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="8f217-119">Jeśli tworzysz jednej maszyny wirtualnej za pomocą portalu jest to prosty sposób dodawania ochrony z Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="8f217-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="8f217-120">Za pomocą wpisu z **Marketplace** Otwiera kreatora, który pomaga skonfigurować maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="8f217-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="8f217-121">Możesz użyć **ustawienia** bloku, trzeci panelu kreatora, aby zainstalować rozszerzenie zabezpieczeń Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="8f217-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="8f217-122">Aby uzyskać ogólne instrukcje, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8f217-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="8f217-123">Po przejściu do **ustawienia** bloku kreatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f217-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="8f217-124">Kliknij przycisk **rozszerzenia**, następnie kliknij przycisk **dodanie rozszerzenia** w okienku dalej.</span><span class="sxs-lookup"><span data-stu-id="8f217-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![Rozpocznij dodawanie rozszerzenia][1]

2. <span data-ttu-id="8f217-126">Wybierz **głębokie Agent zabezpieczeń** w **nowy zasób** okienka.</span><span class="sxs-lookup"><span data-stu-id="8f217-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="8f217-127">W okienku głębokie Agent zabezpieczeń kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8f217-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Identyfikowanie agenta głębokie zabezpieczeń][2]

3. <span data-ttu-id="8f217-129">Wprowadź **identyfikator dzierżawy** i **hasło aktywacji dzierżawy** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="8f217-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="8f217-130">Opcjonalnie możesz wprowadzić **identyfikator zasad zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="8f217-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="8f217-131">Następnie kliknij przycisk **OK** do dodania klienta.</span><span class="sxs-lookup"><span data-stu-id="8f217-131">Then, click **OK** to add the client.</span></span>

   ![Podaj szczegóły rozszerzenia][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="8f217-133">Zainstaluj agenta głębokie zabezpieczeń na istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8f217-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="8f217-134">Aby zainstalować agenta na istniejącej maszyny Wirtualnej, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8f217-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="8f217-135">Moduł Azure PowerShell, wersja 0.8.2 lub nowszej, zainstalowanych na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8f217-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="8f217-136">Można sprawdzić wersji programu Azure PowerShell, który został zainstalowany przy użyciu **azure Get-Module | wersja formatu tabeli** polecenia.</span><span class="sxs-lookup"><span data-stu-id="8f217-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="8f217-137">Aby uzyskać instrukcje i łącza do najnowszej wersji, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8f217-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8f217-138">Zaloguj się przy użyciu subskrypcji platformy Azure `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="8f217-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="8f217-139">Zainstalowana na docelowej maszynie wirtualnej agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8f217-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="8f217-140">Po pierwsze sprawdzenie, czy Agent maszyny Wirtualnej jest już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="8f217-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="8f217-141">Wypełnij pola Nazwa usługi w chmurze i Nazwa maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora.</span><span class="sxs-lookup"><span data-stu-id="8f217-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="8f217-142">Zastąp wszystko w obrębie oferty, w tym < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="8f217-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="8f217-143">Jeśli nie znasz usługi w chmurze i nazwy maszyny wirtualnej, należy uruchomić **Get-AzureVM** do wyświetlenia informacji dla wszystkich maszyn wirtualnych w Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8f217-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="8f217-144">Jeśli **hosta zapisu** polecenie zwraca **True**, Agent maszyny Wirtualnej jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="8f217-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="8f217-145">Jeśli zmienna zwraca **False**, zobacz instrukcje i łącze do pobrania w Azure blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="8f217-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="8f217-146">Jeśli jest zainstalowany Agent maszyny Wirtualnej, uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="8f217-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="8f217-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f217-147">Next steps</span></span>
<span data-ttu-id="8f217-148">Trwa kilka minut, aż do uruchomienia po zainstalowaniu agenta.</span><span class="sxs-lookup"><span data-stu-id="8f217-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="8f217-149">Po tym musisz aktywować głębokie zabezpieczeń na maszynie wirtualnej, więc można nim zarządzać za głębokie Menedżera zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8f217-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="8f217-150">Zobacz następujące artykuły, aby uzyskać dodatkowe instrukcje:</span><span class="sxs-lookup"><span data-stu-id="8f217-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="8f217-151">Trend w artykule o tym rozwiązaniu [Instant-On Cloud Security platformy Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="8f217-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="8f217-152">A [przykładowy skrypt programu Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) można skonfigurować maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8f217-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="8f217-153">[Instrukcje](http://go.microsoft.com/fwlink/?LinkId=404099) przykładowej</span><span class="sxs-lookup"><span data-stu-id="8f217-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f217-154">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8f217-154">Additional resources</span></span>
<span data-ttu-id="8f217-155">[Jak zalogować się do maszyny wirtualnej z systemem Windows Server]</span><span class="sxs-lookup"><span data-stu-id="8f217-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="8f217-156">[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]</span><span class="sxs-lookup"><span data-stu-id="8f217-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="8f217-157">[Jak zalogować się do maszyny wirtualnej z systemem Windows Server]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="8f217-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="8f217-158">[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="8f217-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>
