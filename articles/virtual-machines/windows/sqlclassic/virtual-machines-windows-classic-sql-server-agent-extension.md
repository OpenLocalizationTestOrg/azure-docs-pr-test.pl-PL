---
title: "zadania zarządzania aaaAutomate na maszynach wirtualnych SQL (klasyczne) | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toomanage hello rozszerzenia agenta programu SQL Server, który automatyzuje określonych zadań administracyjnych programu SQL Server. Obejmują one automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure. W tym temacie używa trybu klasycznego wdrożenia hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatyzacji zadań zarządzania na maszynach wirtualnych platformy Azure z hello rozszerzenie agenta serwera SQL (klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Wdrożenie klasyczne](../classic/sql-server-agent-extension.md)
> 
>
 
Witaj rozszerzenia agenta IaaS programu SQL Server (SQLIaaSAgent) działa na zadań administracyjnych tooautomate maszyn wirtualnych platformy Azure. Ten temat zawiera omówienie usług hello obsługiwany przez rozszerzenie hello, jak również instrukcje dotyczące instalacji, stanu i usuwania.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. wersja Menedżera zasobów hello tooview tego artykułu, zobacz [rozszerzenie agenta serwera SQL dla programu SQL Server maszyn wirtualnych Menedżera zasobów](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Obsługiwane usługi
Witaj rozszerzenia agenta programu SQL Server IaaS obsługuje hello następujące zadania administracyjne:

| Funkcja administracji | Opis |
| --- | --- |
| **Automatyczna usługa Backup SQL** |Automatyzuje hello Planowanie tworzenia kopii zapasowych dla wszystkich baz danych dla hello domyślnego wystąpienia programu SQL Server w hello maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [automatycznego tworzenia kopii zapasowej dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-backup.md). |
| **Automatyczne stosowanie poprawek SQL** |Konfiguruje podczas aktualizacji, które tooyour, maszyna wirtualna może potrwać umieszczone, okna obsługi, aby uniknąć aktualizacje w godzinach szczytu dla obciążenia. Aby uzyskać więcej informacji, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-patching.md). |
| **Integracja z usługą Azure Key Vault** |Umożliwia tooautomatically należy zainstalować i skonfigurować usługi Azure Key Vault na maszyną Wirtualną programu SQL Server. Aby uzyskać więcej informacji, zobacz [Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (klasyczne)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Wymagania wstępne
Wymagania dotyczące toouse hello rozszerzenie agenta IaaS serwera SQL na maszynie Wirtualnej:

### <a name="operating-system"></a>System operacyjny:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Wersje programu SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Program Azure PowerShell:
[Pobierz i skonfiguruj hello najnowszych poleceń programu Azure PowerShell](/powershell/azure/overview).

Uruchom program Windows PowerShell i podłącz go tooyour subskrypcji platformy Azure z hello **Add-AzureAccount** polecenia.

    Add-AzureAccount

Jeśli masz wiele subskrypcji, użyj **AzureSubscription wybierz** tooselect hello subskrypcji, która zawiera urządzenie docelowe klasyczne maszyny Wirtualnej.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

W tym momencie można uzyskać listę hello klasycznych maszyn wirtualnych i ich nazwy usługi skojarzone z hello **Get-AzureVM** polecenia.

    Get-AzureVM

## <a name="installation"></a>Instalacja
Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooinstall hello rozszerzenia agenta programu SQL Server IaaS i skonfigurować skojarzonych z nimi usług. Użyj hello **AzureVMSqlServerExtension zestaw** rozszerzenia hello tooinstall polecenia cmdlet programu PowerShell. Na przykład hello następujące polecenie instaluje hello rozszerzenia na maszynie Wirtualnej serwera systemu Windows (klasyczne) i nadaje "SQLIaaSExtension".

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Po aktualizacji najnowszej wersji toohello hello rozszerzenia agenta IaaS SQL, należy ponownie uruchomić maszynę wirtualną po zaktualizowaniu hello rozszerzenia.

> [!NOTE]
> Klasycznych maszyn wirtualnych nie ma tooinstall opcji i skonfigurować hello rozszerzenia agenta SQL IaaS za pośrednictwem portalu hello.
> 
> 

## <a name="status"></a>Stan
Jednokierunkowej tooverify, że zainstalowano rozszerzenia hello jest stan agenta hello tooview w hello portalu Azure. Wybierz maszynę wirtualną na liście hello bloku maszyny wirtualnej, a następnie kliknij polecenie **rozszerzenia**. Powinny pojawić się hello **SQLIaaSAgent** rozszerzenie na liście.

![Rozszerzenie IaaS agenta serwera SQL w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Można również użyć hello **Get-AzureVMSqlServerExtension** polecenia cmdlet programu Azure Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Usuwanie
W portalu Azure hello, można odinstalować rozszerzenia hello przez kliknięcie przycisku wielokropka hello na powitania **rozszerzenia** bloku właściwości maszyny wirtualnej. Następnie kliknij przycisk **Odinstaluj**.

![Odinstaluj hello rozszerzenia agenta programu SQL Server IaaS w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Można również użyć hello **AzureVMSqlServerExtension Usuń** polecenia cmdlet programu Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Następne kroki
Przy użyciu jednej z usług hello obsługiwany przez rozszerzenie hello BEGIN. Aby uzyskać więcej informacji, zobacz Tematy hello, występujący w odwołaniu w hello [obsługiwane usługi](#supported-services) sekcji tego artykułu.

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

