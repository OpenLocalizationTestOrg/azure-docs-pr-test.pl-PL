---
title: "Usługami domenowymi Azure Active Directory: Przewodnik administrowania | Dokumentacja firmy Microsoft"
description: "Przyłącz maszynę wirtualną systemu Windows do domeny zarządzanej przy użyciu programu Azure PowerShell i klasycznym modelu wdrażania."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="fb4e8-103">Dołącz maszynę wirtualną systemu Windows Server do domeny zarządzanej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb4e8-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb4e8-104">Klasyczny portal Azure — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fb4e8-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="fb4e8-105">PowerShell — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fb4e8-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="fb4e8-106">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fb4e8-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fb4e8-107">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="fb4e8-108">Usługi domenowe Azure AD aktualnie nie obsługuje modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="fb4e8-109">Te kroki pokazują, jak dostosować zestaw poleceń programu Azure PowerShell, które tworzą i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="fb4e8-110">Te kroki ułatwiające tworzenie maszyny wirtualnej opartych na systemie Windows Azure i przyłączyć go do domeny zarządzanej usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="fb4e8-111">Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="fb4e8-112">Ta metoda może być przydatna, jeśli jesteś nowym użytkownikiem programu PowerShell lub chcesz dowiedzieć się, jakie wartości, aby określić, czy konfiguracja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="fb4e8-113">Użytkownicy wersji Advanced programu PowerShell można wykonać polecenia i podstaw wartości zmiennych (wiersze rozpoczynające się od "$").</span><span class="sxs-lookup"><span data-stu-id="fb4e8-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="fb4e8-114">Jeśli jeszcze tego nie zrobiono tego wcześniej, postępuj zgodnie z instrukcjami w [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) do zainstalowania programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="fb4e8-115">Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="fb4e8-116">Krok 1: Dodaj swoje konto</span><span class="sxs-lookup"><span data-stu-id="fb4e8-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="fb4e8-117">W wierszu polecenia programu PowerShell wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="fb4e8-118">Wpisz adres e-mail skojarzony z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="fb4e8-119">Wpisz hasło dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="fb4e8-120">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="fb4e8-121">Krok 2: Ustaw subskrypcji i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="fb4e8-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="fb4e8-122">Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="fb4e8-123">Zastąp wszystko w obrębie oferty, w tym < i > znaków o poprawne nazwy.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="fb4e8-124">Nazwa subskrypcji poprawne można pobrać z właściwości Nazwa subskrypcji dane wyjściowe **Get-AzureSubscription** polecenia.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="fb4e8-125">Nazwa konta magazynu poprawne można pobrać z właściwości Label dane wyjściowe **Get-AzureStorageAccount** polecenia po uruchomieniu **AzureSubscription wybierz** polecenia.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="fb4e8-126">Krok 3: Przewodnik krok po kroku - aprowizowanie maszyny wirtualnej i przyłączyć go do domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="fb4e8-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="fb4e8-127">Oto odpowiedniego programu Azure PowerShell zestaw poleceń do utworzenia tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="fb4e8-128">Określ informacje dotyczące maszyny wirtualnej systemu Windows do obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="fb4e8-129">Dla wartości InstanceSize D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb4e8-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="fb4e8-130">Zawierają informacje dotyczące domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="fb4e8-131">Określ nazwę usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="fb4e8-132">Określ nazwę sieci wirtualnej, do którego powinny zostać przyłączone maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="fb4e8-133">Upewnij się, że domeny zarządzanej usługi AAD DS jest dostępny w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="fb4e8-134">Wybierz obraz maszyny Wirtualnej, aby go użyć do udostępnienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="fb4e8-135">Skonfiguruj maszynę Wirtualną — Ustaw nazwę maszyny Wirtualnej, rozmiar wystąpienia & obraz ma być używany.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="fb4e8-136">Uzyskaj poświadczenia administratora lokalnego dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="fb4e8-137">Wybierz hasło administratora lokalnego silne.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="fb4e8-138">Uzyskaj poświadczenia dla konta użytkownika należącego do grupy "Administratorzy kontrolera domeny usługi AAD" do przyłączenia do domeny zarządzanej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="fb4e8-139">Nie określaj na przykład nazwa domeny — w naszym przykładzie, "bob" jest określona jako nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="fb4e8-140">Skonfiguruj maszynę Wirtualną — Określ wymagania sprzężenia domeny & wymagane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="fb4e8-141">Ustaw podsieci dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="fb4e8-142">Opcjonalnie: Wskaż adres IP domeny.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="fb4e8-143">Jeśli ustawisz adresy IP domeny zarządzanej usług domenowych Azure AD, serwery DNS dla sieci wirtualnej, ten krok nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="fb4e8-144">Teraz obsłużyć maszyny Wirtualnej systemu Windows przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="fb4e8-145">Skrypt obsługi administracyjnej maszyny Wirtualnej systemu Windows i automatycznie dołączone do domeny zarządzanej usług domenowych w usłudze AAD</span><span class="sxs-lookup"><span data-stu-id="fb4e8-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="fb4e8-146">Ten zestaw poleceń programu PowerShell tworzy maszynę wirtualną dla serwera z biznesowych, który:</span><span class="sxs-lookup"><span data-stu-id="fb4e8-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="fb4e8-147">Użyty obraz systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="fb4e8-148">Jest bardzo małe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="fb4e8-149">Nazwa testu Contoso100 jest.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="fb4e8-150">Jest automatycznie przyłączone do domeny do domeny zarządzanej contoso100.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="fb4e8-151">Zostanie dodany do tej samej sieci wirtualnej jako domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="fb4e8-152">W tym miejscu jest pełna przykładowy skrypt, aby utworzyć maszynę wirtualną systemu Windows i automatycznie dołączone do domeny zarządzanej usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb4e8-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="fb4e8-153">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="fb4e8-153">Related Content</span></span>
* [<span data-ttu-id="fb4e8-154">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="fb4e8-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="fb4e8-155">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="fb4e8-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
