---
title: "Tworzenie maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Tworzenie maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell i klasycznym modelu wdrażania."
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
ms.openlocfilehash: 75c6cf17ee269ae169d9f2f748d0985ca07e454e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="a0297-103">Utwórz maszynę wirtualną systemu Windows PowerShell i klasycznym modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="a0297-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0297-104">Portal Azure — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a0297-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="a0297-105">PowerShell — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a0297-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="a0297-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a0297-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a0297-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0297-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a0297-108">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a0297-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a0297-109">Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0297-109">Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a0297-110">Te kroki pokazują, jak dostosować zestaw poleceń programu Azure PowerShell, które tworzą i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a0297-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="a0297-111">Można użyć tego procesu, aby szybko utworzyć zestaw poleceń dla nowej maszyny wirtualnej z systemem Windows i rozwiń istniejącego wdrożenia lub utworzyć wiele zestawów poleceń, które szybko tworzyć niestandardowe i testowania lub środowisku specjalista IT.</span><span class="sxs-lookup"><span data-stu-id="a0297-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="a0297-112">Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="a0297-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="a0297-113">Ta metoda może być przydatna, jeśli jesteś nowym użytkownikiem programu PowerShell lub po prostu chcesz wiedzieć, jakie wartości, aby określić, czy konfiguracja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a0297-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="a0297-114">Użytkownicy wersji Advanced programu PowerShell można wykonać polecenia i podstaw wartości zmiennych (wiersze rozpoczynające się od "$").</span><span class="sxs-lookup"><span data-stu-id="a0297-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="a0297-115">Jeśli jeszcze tego nie zrobiono tego wcześniej, postępuj zgodnie z instrukcjami w [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) do zainstalowania programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="a0297-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="a0297-116">Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0297-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="a0297-117">Krok 1: Dodaj swoje konto</span><span class="sxs-lookup"><span data-stu-id="a0297-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="a0297-118">W wierszu polecenia programu PowerShell wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a0297-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="a0297-119">Wpisz adres e-mail skojarzony z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="a0297-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="a0297-120">Wpisz hasło dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="a0297-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="a0297-121">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="a0297-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="a0297-122">Krok 2: Ustaw subskrypcji i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="a0297-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="a0297-123">Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0297-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="a0297-124">Zastąp wszystko w obrębie oferty, w tym < i > znaków o poprawne nazwy.</span><span class="sxs-lookup"><span data-stu-id="a0297-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="a0297-125">Nazwa subskrypcji poprawne można pobrać z właściwości Nazwa subskrypcji dane wyjściowe **Get-AzureSubscription** polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0297-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="a0297-126">Nazwa konta magazynu poprawne można pobrać z właściwości Label dane wyjściowe **Get-AzureStorageAccount** polecenia po uruchomieniu **AzureSubscription wybierz** polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0297-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="a0297-127">Krok 3: Określanie ImageFamily</span><span class="sxs-lookup"><span data-stu-id="a0297-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="a0297-128">Następnie należy określić ImageFamily lub etykieta wartości dla określonego obrazu odpowiadającej maszynie wirtualnej Azure, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="a0297-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="a0297-129">Można uzyskać listę dostępnych wartości ImageFamily za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0297-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="a0297-130">Poniżej przedstawiono przykładowe wartości ImageFamily dla komputerów z systemem Windows:</span><span class="sxs-lookup"><span data-stu-id="a0297-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="a0297-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="a0297-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="a0297-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="a0297-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="a0297-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="a0297-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="a0297-134">SQL Server 2012 z dodatkiem SP1 Enterprise w systemie Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a0297-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="a0297-135">Jeśli okaże się obraz, którego szukasz, otwórz wystąpienie świeże edytora tekstu, wybór lub programu PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="a0297-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="a0297-136">Skopiuj następujące do nowego pliku tekstowego lub programu PowerShell ISE, zastępując wartości ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="a0297-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="a0297-137">W niektórych przypadkach nazwa obrazu jest zamiast wartości ImageFamily właściwości etykiety.</span><span class="sxs-lookup"><span data-stu-id="a0297-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="a0297-138">Jeśli nie możesz znaleźć obrazu, który chcesz uzyskać za pomocą właściwości ImageFamily, listy obrazów za ich właściwości Label, przy użyciu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0297-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="a0297-139">Jeśli okaże się prawy obraz za pomocą tego polecenia, otwórz wystąpienie świeże edytora tekstu, wybór lub programu PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a0297-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="a0297-140">Skopiuj następujące do nowego pliku tekstowego lub programu PowerShell ISE, zastępując wartość etykiety.</span><span class="sxs-lookup"><span data-stu-id="a0297-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="a0297-141">Krok 4: Utwórz zestaw poleceń</span><span class="sxs-lookup"><span data-stu-id="a0297-141">Step 4: Build your command set</span></span>
<span data-ttu-id="a0297-142">Tworzenie pozostałe polecenia ustawione przez kopiowanie odpowiedni zestaw bloków poniżej do nowego pliku tekstowego lub ISE, a następnie wypełnianie wartości zmiennych i usuwanie < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="a0297-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="a0297-143">Zobacz dwa [przykłady](#examples) na końcu tego artykułu pomysł końcowego wyniku.</span><span class="sxs-lookup"><span data-stu-id="a0297-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="a0297-144">Uruchom polecenie ustawić, wybierając jedną z tych bloków dwa polecenia (wymagane).</span><span class="sxs-lookup"><span data-stu-id="a0297-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="a0297-145">Opcja 1: Określ nazwę maszyny wirtualnej i rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="a0297-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="a0297-146">Opcja 2: Określ nazwę, rozmiar i nazwa zbioru dostępności.</span><span class="sxs-lookup"><span data-stu-id="a0297-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="a0297-147">Dla wartości InstanceSize D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0297-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a0297-148">Jeśli masz umowy Enterprise Agreement z Software Assurance i zamierzasz korzystać z systemu Windows Server [korzyści Użyj hybrydowego](https://azure.microsoft.com/pricing/hybrid-use-benefit/), Dodaj **- LicenseType** parametr  **Nowy AzureVMConfig** polecenia cmdlet, przekazując wartość **Windows_Server** dla typowy przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="a0297-148">If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.</span></span>  <span data-ttu-id="a0297-149">Upewnij się, że używasz obrazu, które zostały przekazane; Nie można używać standardowy obraz w galerii korzyści użyć hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="a0297-149">Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="a0297-150">Opcjonalnie na autonomicznym komputerze z systemem Windows Określ konto administratora lokalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="a0297-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="a0297-151">Wybierz silne hasło.</span><span class="sxs-lookup"><span data-stu-id="a0297-151">Choose a strong password.</span></span> <span data-ttu-id="a0297-152">Aby sprawdzić jego siły, zobacz [narzędzie do sprawdzania haseł: używanie silnych haseł](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0297-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="a0297-153">Opcjonalnie Aby dodać komputer z systemem Windows do istniejącej domeny usługi Active Directory, określić konto administratora lokalnego i hasło, domeny oraz nazwę i hasło konta domeny.</span><span class="sxs-lookup"><span data-stu-id="a0297-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="a0297-154">Dla dodatkowych opcji konfiguracji wstępnej dla maszyn wirtualnych z systemem Windows, zobacz składnię **Windows** i **WindowsDomain** zestawy parametrów [AzureProvisioningConfig Dodaj ](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="a0297-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="a0297-155">Określony adres IP, znany jako statyczne DIP opcjonalnie przypisać maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="a0297-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="a0297-156">Można sprawdzić, czy określony adres IP jest dostępna w programie:</span><span class="sxs-lookup"><span data-stu-id="a0297-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="a0297-157">Opcjonalnie przypisać maszynę wirtualną do określonej podsieci w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0297-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="a0297-158">Opcjonalnie Dodaj dysk pojedynczy danych do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="a0297-159">Kontroler domeny usługi Active Directory należy ustawić $hcaching "None".</span><span class="sxs-lookup"><span data-stu-id="a0297-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="a0297-160">Opcjonalnie dodaj maszynę wirtualną do istniejącego zestawu z równoważeniem obciążenia dla ruchu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="a0297-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="a0297-161">Na koniec wybierz jedną z tych bloków polecenia wymagane do utworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="a0297-162">Opcja 1: Utwórz maszynę wirtualną w istniejącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a0297-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="a0297-163">Krótka nazwa usługi w chmurze jest nazwa wyświetlana na liście usługi w chmurze w portalu Azure lub na liście grup zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a0297-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="a0297-164">Opcja 2: Utwórz maszynę wirtualną w istniejącej usługi chmury i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="a0297-165">Krok 5: Uruchom polecenie zestawu</span><span class="sxs-lookup"><span data-stu-id="a0297-165">Step 5: Run your command set</span></span>
<span data-ttu-id="a0297-166">Przejrzyj zestawu poleceń programu PowerShell systemu Azure, tworzone w edytorze tekstu lub programu PowerShell ISE składające się z wielu bloków poleceń z kroku 4.</span><span class="sxs-lookup"><span data-stu-id="a0297-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="a0297-167">Upewnij się określono wszystkie wymagane zmienne i mają poprawne wartości.</span><span class="sxs-lookup"><span data-stu-id="a0297-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="a0297-168">Upewnij się, że po usunięciu wszystkich również < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="a0297-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="a0297-169">Korzystając z edytora tekstów, skopiuj zestaw poleceń do Schowka, a następnie kliknij prawym przyciskiem myszy Otwórz wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0297-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="a0297-170">Spowoduje to wystawiać zestawu poleceń w postaci serii poleceń programu PowerShell i utworzenie maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0297-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="a0297-171">Alternatywnie Uruchom polecenie w programie PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a0297-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="a0297-172">Jeśli zostanie utworzony ponownie tę maszynę wirtualną lub podobne jeden, możesz:</span><span class="sxs-lookup"><span data-stu-id="a0297-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="a0297-173">Zapisz to polecenie Ustaw jako plik skryptu programu PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="a0297-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="a0297-174">Zapisz to polecenie Ustaw jako element runbook usługi Automatyzacja Azure w **kont automatyzacji** części portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a0297-174">Save this command set as an Azure Automation runbook in the **Automation Accounts** section of the Azure portal.</span></span>

## <span data-ttu-id="a0297-175"><a id="examples"></a>Przykłady</span><span class="sxs-lookup"><span data-stu-id="a0297-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="a0297-176">Poniżej przedstawiono dwa przykłady tworzenia zestawy poleceń programu PowerShell usługi Azure utworzonych opartych na systemie Windows Azure maszyny wirtualnej przy użyciu kroków opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="a0297-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="a0297-177">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="a0297-177">Example 1</span></span>
<span data-ttu-id="a0297-178">Potrzebuję programu PowerShell zestawu poleceń, utworzyć maszynę wirtualną początkowy dla kontrolera domeny usługi Active Directory, który:</span><span class="sxs-lookup"><span data-stu-id="a0297-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="a0297-179">Użyty obraz systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="a0297-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="a0297-180">Ma nazwę AZDC1.</span><span class="sxs-lookup"><span data-stu-id="a0297-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="a0297-181">Jest komputerem autonomicznym.</span><span class="sxs-lookup"><span data-stu-id="a0297-181">Is a standalone computer.</span></span>
* <span data-ttu-id="a0297-182">Ma dysk danych dodatkowych 20 GB.</span><span class="sxs-lookup"><span data-stu-id="a0297-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="a0297-183">Ma statyczny adres IP 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="a0297-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="a0297-184">Znajduje się w podsieci wewnętrznej bazy danych AZDatacenter sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="a0297-185">Jest usługą w chmurze Azure TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="a0297-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="a0297-186">Oto odpowiedniego programu Azure PowerShell zestaw poleceń do utworzenia tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="a0297-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
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

### <a name="example-2"></a><span data-ttu-id="a0297-187">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="a0297-187">Example 2</span></span>
<span data-ttu-id="a0297-188">Potrzebuję programu PowerShell zestawu poleceń, utworzyć maszynę wirtualną dla serwera z biznesowych, który:</span><span class="sxs-lookup"><span data-stu-id="a0297-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="a0297-189">Użyty obraz systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="a0297-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="a0297-190">Ma nazwę LOB1.</span><span class="sxs-lookup"><span data-stu-id="a0297-190">Has the name LOB1.</span></span>
* <span data-ttu-id="a0297-191">Jest elementem członkowskim domeny corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a0297-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="a0297-192">Ma dysk danych dodatkowych 200 GB.</span><span class="sxs-lookup"><span data-stu-id="a0297-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="a0297-193">Znajduje się w podsieci frontonu AZDatacenter sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="a0297-194">Jest usługą w chmurze Azure TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="a0297-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="a0297-195">Oto odpowiedniego programu Azure PowerShell zestaw poleceń do utworzenia tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0297-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
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


## <a name="next-steps"></a><span data-ttu-id="a0297-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0297-196">Next steps</span></span>
<span data-ttu-id="a0297-197">Jeśli potrzebujesz dysk systemu operacyjnego, który jest większy niż 127 GB, możesz [rozwiń dysk systemu operacyjnego](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0297-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

