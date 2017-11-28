---
title: "aaaInstall Trend Micro głębokie zabezpieczeń na maszynie Wirtualnej | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooinstall i skonfigurować zabezpieczenia Trend Micro maszyny Wirtualnej utworzonej z hello klasycznego modelu wdrożenia na platformie Azure."
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
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="43501-103">Jak tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="43501-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="43501-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="43501-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="43501-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="43501-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="43501-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="43501-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="43501-107">W tym artykule opisano sposób tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na nowej lub istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server.</span><span class="sxs-lookup"><span data-stu-id="43501-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="43501-108">Głębokie zabezpieczeń jako usługa obejmuje ochrony przed złośliwym oprogramowaniem, zapory systemu zapobiegania nieautoryzowanego dostępu i kontroli integralności.</span><span class="sxs-lookup"><span data-stu-id="43501-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="43501-109">Witaj klient jest instalowany jako rozszerzenie zabezpieczeń za pomocą hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43501-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="43501-110">Na nowej maszyny wirtualnej należy zainstalować hello głębokie Agent zabezpieczeń, jako hello agenta maszyny Wirtualnej jest tworzona automatycznie przez hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43501-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="43501-111">Istniejącej maszyny Wirtualnej utworzone przy użyciu klasycznego portalu hello, hello wiersza polecenia platformy Azure lub programu PowerShell może nie mieć agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43501-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="43501-112">Dla istniejącej maszyny wirtualnej, która nie ma hello agenta maszyny Wirtualnej należy toodownload i najpierw go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="43501-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="43501-113">W tym artykule opisano zarówno sytuacji.</span><span class="sxs-lookup"><span data-stu-id="43501-113">This article covers both situations.</span></span>

<span data-ttu-id="43501-114">Jeśli masz bieżącej subskrypcji z Trend Micro dla rozwiązania lokalnego, można użyć jej toohelp ochrony maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43501-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="43501-115">Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="43501-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="43501-116">Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz Trend Micro blogu hello [zabezpieczeń firmy Microsoft Azure VM Agent rozszerzenia dla bezpośrednich](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="43501-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="43501-117">Zainstaluj hello głębokie Agent zabezpieczeń na nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43501-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="43501-118">Witaj [portalu Azure](http://portal.azure.com) umożliwia instalowanie rozszerzenia zabezpieczeń Trend Micro hello, korzystając z obrazu z hello **Marketplace** maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="43501-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="43501-119">Jeśli tworzysz jednej maszyny wirtualnej za pomocą portalu hello jest łatwy sposób ochrony tooadd z Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="43501-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="43501-120">Za pomocą wpisu z hello **Marketplace** Otwiera kreatora, który pomaga skonfigurować maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="43501-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="43501-121">Użyj hello **ustawienia** bloku, panel trzeci hello hello kreatora hello tooinstall Trend Micro rozszerzenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="43501-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="43501-122">Aby uzyskać ogólne instrukcje, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="43501-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="43501-123">Jeśli otrzymasz toohello **ustawienia** bloku kreatora hello hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="43501-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="43501-124">Kliknij przycisk **rozszerzenia**, następnie kliknij przycisk **dodanie rozszerzenia** w hello następne okienko.</span><span class="sxs-lookup"><span data-stu-id="43501-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Rozpocznij dodawanie rozszerzenia hello][1]

2. <span data-ttu-id="43501-126">Wybierz **głębokie Agent zabezpieczeń** w hello **nowy zasób** okienka.</span><span class="sxs-lookup"><span data-stu-id="43501-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="43501-127">W okienku głębokie Agent zabezpieczeń powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="43501-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identyfikowanie agenta głębokie zabezpieczeń][2]

3. <span data-ttu-id="43501-129">Wprowadź hello **identyfikator dzierżawy** i **hasło aktywacji dzierżawy** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="43501-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="43501-130">Opcjonalnie możesz wprowadzić **identyfikator zasad zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="43501-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="43501-131">Następnie kliknij przycisk **OK** tooadd powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="43501-131">Then, click **OK** tooadd hello client.</span></span>

   ![Podaj szczegóły rozszerzenia][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="43501-133">Zainstaluj hello głębokie Agent zabezpieczeń na istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43501-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="43501-134">agent hello tooinstall na istniejącej maszyny Wirtualnej, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="43501-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="43501-135">Witaj modułu Azure PowerShell, wersja 0.8.2 lub nowszej, zainstalowanych na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="43501-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="43501-136">Można sprawdzić wersji hello programu Azure PowerShell, który został zainstalowany przy użyciu hello **azure Get-Module | wersja formatu tabeli** polecenia.</span><span class="sxs-lookup"><span data-stu-id="43501-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="43501-137">Aby uzyskać instrukcje i toohello łącze najnowszej wersji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43501-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="43501-138">Zaloguj się przy użyciu subskrypcji platformy Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="43501-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="43501-139">Witaj Agent maszyny Wirtualnej został zainstalowany na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43501-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="43501-140">Po pierwsze sprawdzenie hello, że Agent maszyny Wirtualnej jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="43501-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="43501-141">Wypełnij hello nazwa usługi w chmurze i nazwy maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora hello.</span><span class="sxs-lookup"><span data-stu-id="43501-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="43501-142">Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="43501-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="43501-143">Jeśli nie znasz hello usługi w chmurze i nazwy maszyny wirtualnej, należy uruchomić **Get-AzureVM** toodisplay, że informacje dla wszystkich hello maszyn wirtualnych w ramach Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="43501-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="43501-144">Jeśli hello **hosta zapisu** polecenie zwraca **True**, hello jest zainstalowany Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43501-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="43501-145">Jeśli zmienna zwraca **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello Azure wpis w blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="43501-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="43501-146">Jeśli hello agenta maszyny Wirtualnej jest zainstalowany, uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="43501-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="43501-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43501-147">Next steps</span></span>
<span data-ttu-id="43501-148">Trwa kilka minut, aż toostart agenta hello uruchomiona po jej zainstalowaniu.</span><span class="sxs-lookup"><span data-stu-id="43501-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="43501-149">Po wykonaniu tej należy tooactivate głębokie zabezpieczeń na maszynie wirtualnej hello, można nim zarządzać za głębokie Menedżera zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="43501-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="43501-150">Zobacz następujące artykuły, aby uzyskać dodatkowe instrukcje hello:</span><span class="sxs-lookup"><span data-stu-id="43501-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="43501-151">Trend w artykule o tym rozwiązaniu [Instant-On Cloud Security platformy Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="43501-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="43501-152">A [przykładowy skrypt programu Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) maszyny wirtualnej hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="43501-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="43501-153">[Instrukcje](http://go.microsoft.com/fwlink/?LinkId=404099) hello próbki</span><span class="sxs-lookup"><span data-stu-id="43501-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43501-154">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="43501-154">Additional resources</span></span>
<span data-ttu-id="43501-155">[Jak toolog na tooa maszyny wirtualnej z systemem Windows Server]</span><span class="sxs-lookup"><span data-stu-id="43501-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="43501-156">[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]</span><span class="sxs-lookup"><span data-stu-id="43501-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Jak toolog na tooa maszyny wirtualnej z systemem Windows Server]:connect-logon.md
[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
