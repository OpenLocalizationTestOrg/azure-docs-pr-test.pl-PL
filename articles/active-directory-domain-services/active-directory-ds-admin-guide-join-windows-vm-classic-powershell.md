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
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Przyłączanie się do systemu Windows Server maszyny wirtualnej tooa zarządzanych domeny przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Klasyczny portal Azure — systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell — systemu Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Usługi domenowe Azure AD nie obsługuje obecnie hello modelu Resource Manager.
>
>

Te kroki pokazują, jak toocustomize zestaw programu Azure PowerShell polecenia, który utworzyć i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego. Te kroki ułatwiające tworzenie maszyny wirtualnej opartych na systemie Windows Azure i dołącz go do domeny zarządzanej usług domenowych Azure AD tooan.

Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure. Takie podejście może być przydatna, jeśli są nowe tooPowerShell lub tooknow toospecify jakie wartości dla Konfiguracja zakończyła się pomyślnie. Użytkownicy zaawansowani programu PowerShell można wykonać polecenia hello i podstaw wartości zmiennych hello (hello wiersze rozpoczynające się od "$").

Jeśli jeszcze tego nie zrobiono tego wcześniej, użyj instrukcji hello w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall programu Azure PowerShell na komputerze lokalnym. Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.

## <a name="step-1-add-your-account"></a>Krok 1: Dodaj swoje konto
1. W wierszu polecenia programu PowerShell hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.
2. Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.
3. Wpisz hasło powitania dla Twojego konta.
4. Kliknij przycisk **Zaloguj**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Krok 2: Ustaw subskrypcji i konto magazynu
Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell hello. Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawne nazwy.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Nazwa subskrypcji poprawne hello można pobrać z hello Właściwość Nazwa subskrypcji hello dane wyjściowe hello **Get-AzureSubscription** polecenia. Można uzyskać nazwy konta magazynu poprawne hello hello właściwości Label hello dane wyjściowe hello **Get-AzureStorageAccount** polecenia po uruchomieniu hello **AzureSubscription wybierz** polecenia.

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Krok 3: Przewodnik krok po kroku - aprowizowanie maszyny wirtualnej hello i przyłączyć go toohello domeny zarządzanej
Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.

Określ informacje o toobe maszyny wirtualnej systemu Windows hello udostępnione.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Witaj InstanceSize wartości dla D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Podaj informacje o hello domeny zarządzanej.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Określ nazwę hello hello usługi w chmurze.

    $svcname="Contoso100-test"

Określ nazwę hello Witaj sieci wirtualnej toowhich Witaj, które mają być łączone maszyny Wirtualnej. Upewnij się, ta domena AAD-DS zarządzane hello jest dostępna w tej sieci wirtualnej.

    $vnetname="MyPreviewVnet"

Wybierz hello wirtualna obrazu toobe używane tooprovision hello maszyny Wirtualnej.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Skonfiguruj hello VM - Nazwa maszyny Wirtualnej zestawu toobe rozmiar & obrazu wystąpienie używane.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Uzyskaj poświadczenia administratora lokalnego dla hello maszyny Wirtualnej. Wybierz hasło administratora lokalnego silne.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Uzyskaj poświadczenia dla konta użytkownika należące Administratorzy DC too'AAD grupy toojoin wirtualna toohello zarządzanych domeny. Nie określaj nazwy domeny hello — wystąpienia, w tym przykładzie określono "bob" hello nazwy użytkownika.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Skonfiguruj hello maszyny Wirtualnej — Określ wymagania sprzężenia domeny & wymagane poświadczenia.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Ustaw podsieci hello maszyny Wirtualnej.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Opcjonalnie: Adres IP punktu toohello hello domeny. Jeśli ustawisz adresy IP hello hello toobe domeny zarządzanej usług domenowych Azure AD hello serwery DNS dla sieci wirtualnej hello, ten krok nie jest wymagane.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Teraz należy hello przyłączonych do domeny maszyny Wirtualnej systemu Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Skrypt tooprovision Maszynę wirtualną systemu Windows i automatycznie Dołącz go do domeny zarządzanej usług domenowych w usłudze AAD tooan
Ten zestaw poleceń programu PowerShell tworzy maszynę wirtualną dla serwera z biznesowych, który:

* Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.
* Jest bardzo małe maszyny wirtualnej.
* Ma nazwę hello Contoso100 testu.
* Jest automatycznie domeny zarządzanej contoso100 toohello przyłączone do domeny.
* Dodaje się toohello tej samej sieci wirtualnej jako hello zarządzane domeny.

Oto hello maszyny wirtualnej systemu Windows hello pełny przykład skryptu toocreate i automatycznie Dołącz go do domeny zarządzanej usług domenowych Azure AD toohello.

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

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
