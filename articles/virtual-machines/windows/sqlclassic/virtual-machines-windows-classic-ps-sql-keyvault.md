---
title: aaaIntegrate Key Vault z programem SQL Server na maszynach wirtualnych systemu Windows na platformie Azure (klasyczne) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooautomate hello konfiguracji programu SQL Server szyfrowania do użycia z usługą Azure Key Vault. W tym temacie wyjaśniono, jak utworzyć toouse integracji magazynu kluczy Azure z maszyn wirtualnych programu SQL Server w hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Wdrożenie klasyczne](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Omówienie
Istnieje wiele funkcji szyfrowania programu SQL Server, takich jak [przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [szyfrowania na poziomie kolumny (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), i [szyfrowania kopii zapasowych](https://msdn.microsoft.com/library/dn449489.aspx). Te formy szyfrowania wymaga toomanage i przechowywania kluczy kryptograficznych hello używanego do szyfrowania. Witaj usługi Azure Key Vault (AKV) jest zaprojektowana tooimprove hello zabezpieczeń i zarządzanie tych kluczy w lokalizacji bezpieczne i wysokiej dostępności. Witaj [Łącznik usług SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) włącza te klucze z usługi Azure Key Vault toouse programu SQL Server.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Jeśli korzystasz z programu SQL Server z lokalnymi maszynami, istnieją [kroki można wykonać tooaccess usługi Azure Key Vault z komputera lokalnego programu SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Jednak dla programu SQL Server na maszynach wirtualnych Azure, można oszczędzić czas za pomocą hello *integracji magazynu kluczy Azure* funkcji. Z kilku tooenable poleceń cmdlet programu Azure PowerShell tej funkcji, można zautomatyzować hello konfiguracji niezbędne do tooaccess maszyny Wirtualnej SQL magazynu kluczy.

Gdy ta funkcja jest włączona, automatycznie jest instalowana hello Łącznik usług SQL Server, konfiguruje tooaccess dostawcy EKM hello Azure Key Vault i tworzy tooallow poświadczeń hello możesz tooaccess Twojego magazynu. Jeśli użytkownik przeglądał hello kroki hello wcześniej wymienionymi lokalnej dokumentacji, zobaczysz, że ta funkcja pozwala zautomatyzować kroki 2 i 3. jedyną operacją Hello nadal musisz toodo ręcznie jest toocreate hello — magazyn kluczy i kluczy. Dostępne jest zautomatyzowany hello wszystkie ustawienia maszyny wirtualnej SQL. Po ukończeniu tej konfiguracji tej funkcji można wykonywać toobegin instrukcje T-SQL szyfrowania z bazy danych lub kopii zapasowych w zwykły sposób.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Skonfiguruj Integracja
Za pomocą programu PowerShell tooconfigure integracji magazynu kluczy Azure. Witaj następujące sekcje zawierają omówienie hello wymagane parametry, a następnie przykładowy skrypt programu PowerShell.

### <a name="install-hello-sql-server-iaas-extension"></a>Zainstaluj hello IaaS rozszerzenie dotyczące programu SQL Server
Najpierw [zainstalować hello IaaS rozszerzenie dotyczące programu SQL Server](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Zrozumienie hello parametrów wejściowych
Witaj następujące tabeli list hello wymagane parametry skryptu PowerShell hello toorun w następnej sekcji hello.

| Parametr | Opis | Przykład |
| --- | --- | --- |
| **$akvURL** |**adres URL magazynu kluczy Hello** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Główna nazwa usługi** |"fde2b411 - 33d 5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Klucz tajny nazwy głównej usługi** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM =" |
| **$credName** |**Nazwa poświadczenia**: integracja powoduje utworzenie poświadczenia w programie SQL Server, dzięki czemu hello wirtualna toohave dostępu toohello klucza magazynu. Wybierz nazwę tego poświadczenia. |"mycred1" |
| **$vmName** |**Nazwa maszyny wirtualnej**: hello nazwę wcześniej utworzonej maszyny Wirtualnej SQL. |"myvmname" |
| **$serviceName** |**Nazwa usługi**: hello usługi w chmurze nazwę, która jest skojarzona z hello maszyny Wirtualnej SQL. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>Włącz integracja przy użyciu programu PowerShell
Witaj **AzureVMSqlServerKeyVaultCredentialConfig nowy** polecenie cmdlet tworzy obiekt konfiguracji dla funkcji integracji magazynu kluczy Azure hello. Witaj **AzureVMSqlServerExtension zestaw** konfiguruje tej integracji z hello **KeyVaultCredentialSettings** parametru. Witaj, jak po Pokaż kroki toouse tych poleceń.

1. W programie Azure PowerShell najpierw skonfigurować parametry wejściowe hello wartościami określonych zgodnie z opisem w poprzednich sekcjach tego tematu, hello. Przykładem jest Hello następującego skryptu.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Następnie użyj następujących hello skryptu tooconfigure i Włącz integracja.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Witaj rozszerzenia agenta SQL IaaS zaktualizuje hello maszyny Wirtualnej SQL przy użyciu tej nowej konfiguracji.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

