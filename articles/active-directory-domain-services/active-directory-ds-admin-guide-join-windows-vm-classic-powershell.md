---
title: "Usługami domenowymi Azure Active Directory: Przewodnik administrowania | Dokumentacja firmy Microsoft"
description: "Dołącz do domeny systemu Windows maszyny wirtualnej tooa zarządzane przy użyciu programu Azure PowerShell i hello klasycznego modelu wdrażania."
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
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="26fe8-103">Przyłączanie się do systemu Windows Server maszyny wirtualnej tooa zarządzanych domeny przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="26fe8-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26fe8-104">Klasyczny portal Azure — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="26fe8-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="26fe8-105">PowerShell — systemu Windows</span><span class="sxs-lookup"><span data-stu-id="26fe8-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="26fe8-106">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="26fe8-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="26fe8-107">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="26fe8-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="26fe8-108">Usługi domenowe Azure AD nie obsługuje obecnie hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26fe8-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="26fe8-109">Te kroki pokazują, jak toocustomize zestaw programu Azure PowerShell polecenia, który utworzyć i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego.</span><span class="sxs-lookup"><span data-stu-id="26fe8-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="26fe8-110">Te kroki ułatwiające tworzenie maszyny wirtualnej opartych na systemie Windows Azure i dołącz go do domeny zarządzanej usług domenowych Azure AD tooan.</span><span class="sxs-lookup"><span data-stu-id="26fe8-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="26fe8-111">Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="26fe8-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="26fe8-112">Takie podejście może być przydatna, jeśli są nowe tooPowerShell lub tooknow toospecify jakie wartości dla Konfiguracja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="26fe8-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="26fe8-113">Użytkownicy zaawansowani programu PowerShell można wykonać polecenia hello i podstaw wartości zmiennych hello (hello wiersze rozpoczynające się od "$").</span><span class="sxs-lookup"><span data-stu-id="26fe8-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="26fe8-114">Jeśli jeszcze tego nie zrobiono tego wcześniej, użyj instrukcji hello w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="26fe8-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="26fe8-115">Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26fe8-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="26fe8-116">Krok 1: Dodaj swoje konto</span><span class="sxs-lookup"><span data-stu-id="26fe8-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="26fe8-117">W wierszu polecenia programu PowerShell hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.</span><span class="sxs-lookup"><span data-stu-id="26fe8-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="26fe8-118">Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="26fe8-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="26fe8-119">Wpisz hasło powitania dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="26fe8-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="26fe8-120">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="26fe8-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="26fe8-121">Krok 2: Ustaw subskrypcji i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="26fe8-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="26fe8-122">Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="26fe8-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="26fe8-123">Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawne nazwy.</span><span class="sxs-lookup"><span data-stu-id="26fe8-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="26fe8-124">Nazwa subskrypcji poprawne hello można pobrać z hello Właściwość Nazwa subskrypcji hello dane wyjściowe hello **Get-AzureSubscription** polecenia.</span><span class="sxs-lookup"><span data-stu-id="26fe8-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="26fe8-125">Można uzyskać nazwy konta magazynu poprawne hello hello właściwości Label hello dane wyjściowe hello **Get-AzureStorageAccount** polecenia po uruchomieniu hello **AzureSubscription wybierz** polecenia.</span><span class="sxs-lookup"><span data-stu-id="26fe8-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="26fe8-126">Krok 3: Przewodnik krok po kroku - aprowizowanie maszyny wirtualnej hello i przyłączyć go toohello domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="26fe8-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="26fe8-127">Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="26fe8-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="26fe8-128">Określ informacje o toobe maszyny wirtualnej systemu Windows hello udostępnione.</span><span class="sxs-lookup"><span data-stu-id="26fe8-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="26fe8-129">Witaj InstanceSize wartości dla D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="26fe8-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="26fe8-130">Podaj informacje o hello domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="26fe8-131">Określ nazwę hello hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="26fe8-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="26fe8-132">Określ nazwę hello Witaj sieci wirtualnej toowhich Witaj, które mają być łączone maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="26fe8-133">Upewnij się, ta domena AAD-DS zarządzane hello jest dostępna w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="26fe8-134">Wybierz hello wirtualna obrazu toobe używane tooprovision hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="26fe8-135">Skonfiguruj hello VM - Nazwa maszyny Wirtualnej zestawu toobe rozmiar & obrazu wystąpienie używane.</span><span class="sxs-lookup"><span data-stu-id="26fe8-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="26fe8-136">Uzyskaj poświadczenia administratora lokalnego dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="26fe8-137">Wybierz hasło administratora lokalnego silne.</span><span class="sxs-lookup"><span data-stu-id="26fe8-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="26fe8-138">Uzyskaj poświadczenia dla konta użytkownika należące Administratorzy DC too'AAD grupy toojoin wirtualna toohello zarządzanych domeny.</span><span class="sxs-lookup"><span data-stu-id="26fe8-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="26fe8-139">Nie określaj nazwy domeny hello — wystąpienia, w tym przykładzie określono "bob" hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="26fe8-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="26fe8-140">Skonfiguruj hello maszyny Wirtualnej — Określ wymagania sprzężenia domeny & wymagane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="26fe8-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="26fe8-141">Ustaw podsieci hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="26fe8-142">Opcjonalnie: Adres IP punktu toohello hello domeny.</span><span class="sxs-lookup"><span data-stu-id="26fe8-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="26fe8-143">Jeśli ustawisz adresy IP hello hello toobe domeny zarządzanej usług domenowych Azure AD hello serwery DNS dla sieci wirtualnej hello, ten krok nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="26fe8-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="26fe8-144">Teraz należy hello przyłączonych do domeny maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="26fe8-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="26fe8-145">Skrypt tooprovision Maszynę wirtualną systemu Windows i automatycznie Dołącz go do domeny zarządzanej usług domenowych w usłudze AAD tooan</span><span class="sxs-lookup"><span data-stu-id="26fe8-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="26fe8-146">Ten zestaw poleceń programu PowerShell tworzy maszynę wirtualną dla serwera z biznesowych, który:</span><span class="sxs-lookup"><span data-stu-id="26fe8-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="26fe8-147">Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="26fe8-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="26fe8-148">Jest bardzo małe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26fe8-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="26fe8-149">Ma nazwę hello Contoso100 testu.</span><span class="sxs-lookup"><span data-stu-id="26fe8-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="26fe8-150">Jest automatycznie domeny zarządzanej contoso100 toohello przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="26fe8-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="26fe8-151">Dodaje się toohello tej samej sieci wirtualnej jako hello zarządzane domeny.</span><span class="sxs-lookup"><span data-stu-id="26fe8-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="26fe8-152">Oto hello maszyny wirtualnej systemu Windows hello pełny przykład skryptu toocreate i automatycznie Dołącz go do domeny zarządzanej usług domenowych Azure AD toohello.</span><span class="sxs-lookup"><span data-stu-id="26fe8-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="26fe8-153">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="26fe8-153">Related Content</span></span>
* [<span data-ttu-id="26fe8-154">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="26fe8-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="26fe8-155">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="26fe8-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
