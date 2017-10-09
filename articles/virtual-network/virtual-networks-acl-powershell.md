---
title: "listy kontroli aaaManage dostępu do punktu końcowego platformy Azure | PowerShell | Klasycznym | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage listy kontroli dostępu przy użyciu programu PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Zarządzanie listami kontroli dostępu do punktu końcowego w hello klasycznego modelu wdrażania przy użyciu programu PowerShell
Można tworzyć i zarządzać sieci listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu Azure PowerShell lub w hello portalu zarządzania. W tym temacie znajdziesz procedury ACL typowych zadań, które można wykonać przy użyciu programu PowerShell. Listę hello programu Azure PowerShell zawiera polecenia cmdlet [poleceń cmdlet do zarządzania Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Aby uzyskać więcej informacji na temat listy kontroli dostępu, zobacz [co to jest sieć listy kontroli dostępu (ACL)?](virtual-networks-acl.md). Toomanage Twojego listy ACL za pomocą portalu zarządzania hello, zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Zarządzanie listy kontroli dostępu w sieci za pomocą programu Azure PowerShell
Można użyć toocreate poleceń cmdlet programu Azure PowerShell, usuwania i konfigurowania (set) sieci listy kontroli dostępu (ACL). Kilka przykładów niektórych hello sposobów konfigurowania listy ACL za pomocą środowiska PowerShell zostały włączone.

tooretrieve pełną listę hello poleceń cmdlet programu PowerShell listy ACL, możesz użyć dowolnej z następujących hello:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Utwórz ACL sieci przy użyciu reguł, które zezwalają na dostęp z podsieci zdalnej
Hello w poniższym przykładzie przedstawiono sposób toocreate nowej listy ACL, który zawiera reguły. Ta lista ACL jest następnie stosowany tooa punktu końcowego maszyny wirtualnej. reguły listy ACL Hello w poniższym przykładzie hello będzie zezwalał na dostęp z podsieci zdalnej. toocreate nową listę ACL sieci przy użyciu reguł zezwalania na dla podsieci zdalnej, Otwórz program Azure PowerShell ISE. Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.

1. Utwórz hello nowy obiekt listy ACL sieci.
   
        $acl1 = New-AzureAclConfig
2. Ustaw regułę, która pozwala na dostęp z podsieci zdalnej. W poniższym przykładzie hello, Ustaw regułę *100* (które mają pierwszeństwo przed reguły 200 lub nowszy) podsieci zdalnej hello tooallow *10.0.0.0/8* dostępu toohello punktu końcowego maszyny wirtualnej. Zastąp wartości hello z wymaganiami konfiguracji. Nazwa Hello "Konfiguracji ACL programu SharePoint" należy zastąpić o przyjaznej nazwie hello mają toocall tej reguły.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Dodatkowe reguły powtórz polecenie cmdlet hello, zastępując wartości hello z wymaganiami konfiguracji. Należy się toochange hello reguły kolejności tooreflect hello kolejności w której ma zostać hello toobe zasady zastosowane. Witaj mniejszą liczbę reguł mają pierwszeństwo przed hello większą liczbę.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Następnie można utworzyć nowy punkt końcowy (Dodaj) lub ustawić hello listy ACL dla istniejącego punktu końcowego (Set). W tym przykładzie dodamy, że nowy punkt końcowy maszyny wirtualnej o nazwie "web" oraz aktualizacji hello punktu końcowego maszyny wirtualnej z hello ustawień list ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Następnie połączyć polecenia cmdlet hello i uruchom skrypt hello. Na przykład hello połączonych poleceń cmdlet będzie wyglądać następująco:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Usuń regułę listy ACL sieci, która pozwala na dostęp z podsieci zdalnej
Witaj w poniższym przykładzie przedstawiono sposób tooremove reguły listy ACL sieci.  tooremove reguły list kontroli dostępu w sieci za pomocą zezwolenia reguł dla podsieci zdalnej, Otwórz program Azure PowerShell ISE. Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.

1. Pierwszym krokiem jest obiektu ACL sieci hello tooget hello punktu końcowego maszyny wirtualnej. Aby następnie usunąć hello reguły listy ACL. W takim przypadku możemy usunięcie go przez identyfikator reguły. Identyfikator reguły hello 0 spowoduje usunięcie tylko ze hello listy ACL. Nie powoduje usunięcia obiektu ACL hello z hello punktu końcowego maszyny wirtualnej.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Następnie należy zastosować punktu końcowego maszyny wirtualnej toohello obiektu ACL sieci hello i zaktualizować hello maszyny wirtualnej.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Usuń ACL sieci z punktu końcowego maszyny wirtualnej
W niektórych scenariuszach może być tooremove obiektu ACL sieci z punktu końcowego maszyny wirtualnej. toodo, który Otwórz program Azure PowerShell ISE. Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Następne kroki
[Co to jest sieć listy kontroli dostępu (ACL)?](virtual-networks-acl.md)

