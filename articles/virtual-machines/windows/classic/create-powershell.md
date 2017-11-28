---
title: "aaaCreate maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Tworzenie maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell i hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="5dded-103">Utwórz maszynę wirtualną systemu Windows z programu PowerShell i hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="5dded-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5dded-104">Portal Azure — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5dded-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="5dded-105">PowerShell — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5dded-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="5dded-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5dded-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5dded-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5dded-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5dded-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5dded-109">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5dded-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5dded-110">Te kroki pokazują, jak toocustomize zestaw programu Azure PowerShell polecenia, który utworzyć i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5dded-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="5dded-111">Można użyć tego procesu tooquickly utworzyć zestaw poleceń dla nowej maszyny wirtualnej z systemem Windows i rozwiń istniejącego wdrożenia lub toocreate polecenia wiele zestawów szybkiego tworzenia i testowania niestandardowych lub środowisku specjalista IT.</span><span class="sxs-lookup"><span data-stu-id="5dded-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="5dded-112">Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="5dded-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="5dded-113">Takie podejście może być przydatna, jeśli są nowe tooPowerShell lub chcesz tooknow toospecify jakie wartości dla Konfiguracja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5dded-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="5dded-114">Użytkownicy zaawansowani programu PowerShell można wykonać polecenia hello i podstaw wartości zmiennych hello (hello wiersze rozpoczynające się od "$").</span><span class="sxs-lookup"><span data-stu-id="5dded-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="5dded-115">Jeśli jeszcze tego nie zrobiono tego wcześniej, użyj instrukcji hello w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="5dded-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="5dded-116">Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dded-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="5dded-117">Krok 1: Dodaj swoje konto</span><span class="sxs-lookup"><span data-stu-id="5dded-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="5dded-118">W wierszu polecenia programu PowerShell hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5dded-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="5dded-119">Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="5dded-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="5dded-120">Wpisz hasło powitania dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="5dded-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="5dded-121">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="5dded-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="5dded-122">Krok 2: Ustaw subskrypcji i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="5dded-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="5dded-123">Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="5dded-124">Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawne nazwy.</span><span class="sxs-lookup"><span data-stu-id="5dded-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="5dded-125">Nazwa subskrypcji poprawne hello można pobrać z hello Właściwość Nazwa subskrypcji hello dane wyjściowe hello **Get-AzureSubscription** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dded-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="5dded-126">Można uzyskać nazwy konta magazynu poprawne hello hello właściwości Label hello dane wyjściowe hello **Get-AzureStorageAccount** polecenia po uruchomieniu hello **AzureSubscription wybierz** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dded-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="5dded-127">Krok 3: Określanie hello ImageFamily</span><span class="sxs-lookup"><span data-stu-id="5dded-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="5dded-128">Następnie należy toodetermine hello ImageFamily lub wartość etykiety dla odpowiedniego toohello określony obraz powitania ma toocreate maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dded-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="5dded-129">Możesz uzyskać hello listę dostępnych wartości ImageFamily za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dded-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="5dded-130">Poniżej przedstawiono przykładowe wartości ImageFamily dla komputerów z systemem Windows:</span><span class="sxs-lookup"><span data-stu-id="5dded-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="5dded-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="5dded-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="5dded-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="5dded-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="5dded-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="5dded-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="5dded-134">SQL Server 2012 z dodatkiem SP1 Enterprise w systemie Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5dded-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="5dded-135">Jeśli okaże się obraz powitania, którego szukasz, otwórz wystąpienie świeże hello edytora tekstu, wybór lub hello PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="5dded-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5dded-136">Skopiuj następujące hello do nowego pliku tekstowego hello lub hello PowerShell ISE, zastępując wartości ImageFamily hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="5dded-137">W niektórych przypadkach hello nazwa obrazu jest hello zamiast hello ImageFamily wartość właściwości etykiety.</span><span class="sxs-lookup"><span data-stu-id="5dded-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="5dded-138">Jeśli nie możesz znaleźć hello obrazu, który chcesz uzyskać za pomocą właściwości ImageFamily hello, listy obrazów hello za ich właściwości Label, przy użyciu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dded-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="5dded-139">Jeśli okaże się hello prawy obraz za pomocą tego polecenia, otwórz wystąpienie świeże hello edytora tekstu, wybór lub hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="5dded-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="5dded-140">Skopiuj następujące hello do nowego pliku tekstowego hello lub hello PowerShell ISE, zastępując wartość etykiety hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="5dded-141">Krok 4: Utwórz zestaw poleceń</span><span class="sxs-lookup"><span data-stu-id="5dded-141">Step 4: Build your command set</span></span>
<span data-ttu-id="5dded-142">Tworzenie rest hello polecenia ustawione przez kopiowanie hello odpowiedni zestaw bloków poniżej do nowego pliku tekstowego lub hello ISE i następnie wypełnianie hello wartości zmiennych i usuwanie hello < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="5dded-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="5dded-143">Zobacz hello dwa [przykłady](#examples) na końcu hello ten artykuł, aby pomysł hello wynik końcowy.</span><span class="sxs-lookup"><span data-stu-id="5dded-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="5dded-144">Uruchom polecenie ustawić, wybierając jedną z tych bloków dwa polecenia (wymagane).</span><span class="sxs-lookup"><span data-stu-id="5dded-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="5dded-145">Opcja 1: Określ nazwę maszyny wirtualnej i rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="5dded-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="5dded-146">Opcja 2: Określ nazwę, rozmiar i nazwa zbioru dostępności.</span><span class="sxs-lookup"><span data-stu-id="5dded-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="5dded-147">Witaj InstanceSize wartości dla D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dded-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5dded-148">Jeśli masz umowy Enterprise Agreement z Software Assurance i mają tootake zaletą hello systemu Windows Server [korzyści Użyj hybrydowego](https://azure.microsoft.com/pricing/hybrid-use-benefit/), Dodaj **- LicenseType** toohello parametru  **Nowy AzureVMConfig** polecenia cmdlet, przekazanie wartości hello **Windows_Server** hello typowy przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="5dded-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="5dded-149">Upewnij się, że używasz obrazu, które zostały przekazane; Nie można używać standardowy obraz z galerii hello hello korzyści użyć hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="5dded-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="5dded-150">Opcjonalnie na autonomicznym komputerze z systemem Windows Określ hello konta administratora lokalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="5dded-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="5dded-151">Wybierz silne hasło.</span><span class="sxs-lookup"><span data-stu-id="5dded-151">Choose a strong password.</span></span> <span data-ttu-id="5dded-152">toocheck jego siły, zobacz [narzędzie do sprawdzania haseł: używanie silnych haseł](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dded-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="5dded-153">Opcjonalnie hello tooadd Windows komputera tooan istniejącej domeny usługi Active Directory, określ hello konta administratora lokalnego i hasło, hello domeny i hello nazwę i hasło konta domeny.</span><span class="sxs-lookup"><span data-stu-id="5dded-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="5dded-154">Dla dodatkowych opcji konfiguracji wstępnej dla maszyn wirtualnych z systemem Windows, zobacz składnię hello hello **Windows** i **WindowsDomain** zestawy parametrów [ Dodaj AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="5dded-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="5dded-155">Określony adres IP, znany jako statyczny adres DIP opcjonalnie przypisać hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dded-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="5dded-156">Można sprawdzić, czy określony adres IP jest dostępna w programie:</span><span class="sxs-lookup"><span data-stu-id="5dded-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="5dded-157">Opcjonalnie można przypisać określonej podsieci tooa hello maszyny wirtualnej w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dded-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="5dded-158">Opcjonalnie dodaj maszynę wirtualną toohello danych jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="5dded-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="5dded-159">Kontroler domeny usługi Active Directory, ustawić $hcaching także "None".</span><span class="sxs-lookup"><span data-stu-id="5dded-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="5dded-160">Opcjonalnie dodaj hello maszyny wirtualnej tooan istniejącego zestawu równoważeniem obciążenia dla zewnętrznego ruchu.</span><span class="sxs-lookup"><span data-stu-id="5dded-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="5dded-161">Na koniec wybierz jedną z tych bloków polecenia wymagane do utworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="5dded-162">Opcja 1: Utworzenie maszyny wirtualnej hello w istniejącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5dded-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="5dded-163">Krótka nazwa usługi w chmurze hello Hello jest nazwą hello jest widoczna na liście hello usługi w chmurze w portalu Azure hello lub liście hello grup zasobów w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="5dded-164">Opcja 2: Utworzenie maszyny wirtualnej hello w istniejącej usługi chmury i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dded-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="5dded-165">Krok 5: Uruchom polecenie zestawu</span><span class="sxs-lookup"><span data-stu-id="5dded-165">Step 5: Run your command set</span></span>
<span data-ttu-id="5dded-166">Przejrzyj zestaw poleceń programu Azure PowerShell hello, które zostały utworzone w edytorze tekstu lub hello PowerShell ISE składające się z wielu bloków poleceń z kroku 4.</span><span class="sxs-lookup"><span data-stu-id="5dded-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="5dded-167">Upewnij się określono wszystkie zmienne hello potrzebne i mają poprawne wartości hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="5dded-168">Upewnij się, że zostały usunięte wszystkie znaki hello < i > również.</span><span class="sxs-lookup"><span data-stu-id="5dded-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="5dded-169">Jeśli korzystasz z edytora tekstów, polecenie hello kopiowania ustawić toohello Schowka i kliknij prawym przyciskiem myszy Otwórz wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dded-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="5dded-170">To wystawiać zestaw poleceń hello jako serię poleceń programu PowerShell i utworzyć maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dded-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="5dded-171">Alternatywnie Uruchom polecenie hello w hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="5dded-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="5dded-172">Jeśli zostanie utworzony ponownie tę maszynę wirtualną lub podobne jeden, możesz:</span><span class="sxs-lookup"><span data-stu-id="5dded-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="5dded-173">Zapisz to polecenie Ustaw jako plik skryptu programu PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="5dded-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="5dded-174">Zapisz to polecenie Ustaw jako element runbook usługi Automatyzacja Azure w hello **kont automatyzacji** sekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5dded-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="5dded-175"><a id="examples"></a>Przykłady</span><span class="sxs-lookup"><span data-stu-id="5dded-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="5dded-176">Poniżej przedstawiono dwa przykłady użycia hello powyższą toobuild zestawy poleceń programu Azure PowerShell, utworzonych opartych na systemie Windows Azure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dded-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="5dded-177">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="5dded-177">Example 1</span></span>
<span data-ttu-id="5dded-178">Potrzebuję programu PowerShell polecenia set toocreate hello początkowej maszyny wirtualnej do kontrolera domeny usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="5dded-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="5dded-179">Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="5dded-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="5dded-180">Ma nazwę hello AZDC1.</span><span class="sxs-lookup"><span data-stu-id="5dded-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="5dded-181">Jest komputerem autonomicznym.</span><span class="sxs-lookup"><span data-stu-id="5dded-181">Is a standalone computer.</span></span>
* <span data-ttu-id="5dded-182">Ma dysk danych dodatkowych 20 GB.</span><span class="sxs-lookup"><span data-stu-id="5dded-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="5dded-183">Ma statyczny adres IP hello 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="5dded-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="5dded-184">Znajduje się w podsieci wewnętrznej bazy danych hello hello AZDatacenter wirtualnej sieci.</span><span class="sxs-lookup"><span data-stu-id="5dded-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="5dded-185">Jest hello Azure TailspinToys w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5dded-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="5dded-186">Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="5dded-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="5dded-187">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="5dded-187">Example 2</span></span>
<span data-ttu-id="5dded-188">Potrzebuję programu PowerShell zestawu poleceń toocreate maszyny wirtualnej dla serwera biznesowych — które:</span><span class="sxs-lookup"><span data-stu-id="5dded-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="5dded-189">Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="5dded-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="5dded-190">Ma nazwę hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="5dded-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="5dded-191">Jest elementem członkowskim domeny corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="5dded-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="5dded-192">Ma dysk danych dodatkowych 200 GB.</span><span class="sxs-lookup"><span data-stu-id="5dded-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="5dded-193">Znajduje się w podsieci frontonu hello hello AZDatacenter wirtualnej sieci.</span><span class="sxs-lookup"><span data-stu-id="5dded-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="5dded-194">Jest hello Azure TailspinToys w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5dded-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="5dded-195">Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dded-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="5dded-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5dded-196">Next steps</span></span>
<span data-ttu-id="5dded-197">Jeśli potrzebujesz dysk systemu operacyjnego, który jest większy niż 127 GB, możesz [rozwiń dysk systemu operacyjnego hello](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5dded-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

