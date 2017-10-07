---
title: "zadania zarządzania aaaAutomate na maszynach wirtualnych SQL (Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toomanage hello rozszerzenia agenta programu SQL Server, który automatyzuje określonych zadań administracyjnych programu SQL Server. Obejmują one automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure. W tym temacie tryb hello Menedżera zasobów wdrożenia."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatyzacji zadań zarządzania na maszynach wirtualnych platformy Azure z hello rozszerzenie agenta serwera SQL (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Wdrożenie klasyczne](../classic/sql-server-agent-extension.md)
> 
> 

Witaj rozszerzenia agenta IaaS programu SQL Server (SQLIaaSExtension) działa na zadań administracyjnych tooautomate maszyn wirtualnych platformy Azure. Ten temat zawiera omówienie usług hello obsługiwany przez rozszerzenie hello, jak również instrukcje dotyczące instalacji, stanu i usuwania.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Zobacz tooview hello klasycznej wersji w tym artykule [rozszerzenie agenta serwera SQL dla programu SQL Server VMs klasycznego](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Obsługiwane usługi
Witaj rozszerzenia agenta programu SQL Server IaaS obsługuje hello następujące zadania administracyjne:

| Funkcja administracji | Opis |
| --- | --- |
| **Automatyczna usługa Backup SQL** |Automatyzuje hello Planowanie tworzenia kopii zapasowych dla wszystkich baz danych dla hello domyślnego wystąpienia programu SQL Server w hello maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [automatycznego tworzenia kopii zapasowej dla programu SQL Server w maszynach wirtualnych platformy Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Automatyczne stosowanie poprawek SQL** |Konfiguruje podczas aktualizacji, które tooyour, maszyna wirtualna może potrwać umieszczone, okna obsługi, aby uniknąć aktualizacje w godzinach szczytu dla obciążenia. Aby uzyskać więcej informacji, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w maszynach wirtualnych platformy Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Integracja z usługą Azure Key Vault** |Umożliwia tooautomatically należy zainstalować i skonfigurować usługi Azure Key Vault na maszyną Wirtualną programu SQL Server. Aby uzyskać więcej informacji, zobacz [Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Po zainstalowaniu i uruchomione, hello rozszerzenia agenta programu SQL Server IaaS udostępnia te funkcje administracyjne w panelu programu SQL Server hello hello maszyny wirtualnej w portalu Azure hello i za pomocą programu Azure PowerShell dla obrazów w witrynie marketplace programu SQL Server i za pośrednictwem W przypadku ręcznej instalacji rozszerzenia hello programu Azure PowerShell. 

## <a name="prerequisites"></a>Wymagania wstępne
Wymagania dotyczące toouse hello rozszerzenie agenta IaaS serwera SQL na maszynie Wirtualnej:

**System operacyjny**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Wersje programu SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Program Azure PowerShell**:

* [Pobierz i skonfiguruj hello najnowszych poleceń programu Azure PowerShell](/powershell/azure/overview)

## <a name="installation"></a>Instalacja
Rozszerzenie agenta programu SQL Server IaaS Hello jest automatycznie instalowany podczas udostępniania jednego z obrazów Galeria maszyny wirtualnej programu SQL Server hello. Rozszerzenie hello tooreinstall ręcznie na jednym z tych maszyn wirtualnych serwera SQL, należy użyć hello następującego polecenia programu PowerShell:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Możliwe jest również możliwe tooinstall hello rozszerzenie agenta IaaS serwera SQL na maszynie wirtualnej tylko do systemu operacyjnego Windows Server. To ustawienie jest obsługiwane tylko, jeśli ręcznie zainstalowano program SQL Server na tym komputerze. Następnie zainstaluj rozszerzenie hello ręcznie przy użyciu hello sam **AzureVMSqlServerExtension zestaw** polecenia cmdlet programu PowerShell.

> [!NOTE]
> Jeśli hello rozszerzenia agenta programu SQL Server IaaS można ręcznie zainstalować na maszynie Wirtualnej tylko do systemu operacyjnego Windows Server, nie można zarządzać hello ustawień konfiguracji programu SQL Server za pośrednictwem hello portalu Azure. W tym scenariuszu należy wszystkie zmiany przy użyciu programu PowerShell.

## <a name="status"></a>Stan
Jednokierunkowej tooverify, że zainstalowano rozszerzenia hello jest stan agenta hello tooview w hello portalu Azure. Wybierz **wszystkie ustawienia** w hello bloku maszyny wirtualnej, a następnie kliknij polecenie **rozszerzenia**. Powinny pojawić się hello **SQLIaaSExtension** rozszerzenie na liście.

![Rozszerzenie IaaS agenta serwera SQL w portalu Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

Można również użyć hello **Get-AzureVMSqlServerExtension** polecenia cmdlet programu Azure Powershell.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

poprzednie polecenie Hello potwierdza hello agent jest zainstalowany i zawiera ogólne informacje. Można także uzyskać informacje dotyczące automatycznego tworzenia kopii zapasowej i Patching określonego stanu z hello następujące polecenia.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Usuwanie
W portalu Azure hello, można odinstalować rozszerzenia hello przez kliknięcie przycisku wielokropka hello na powitania **rozszerzenia** bloku właściwości maszyny wirtualnej. Następnie kliknij przycisk **usunąć**.

![Odinstaluj hello rozszerzenia agenta programu SQL Server IaaS w portalu Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

Można również użyć hello **AzureRmVMSqlServerExtension Usuń** polecenia cmdlet programu Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Następne kroki
Przy użyciu jednej z usług hello obsługiwany przez rozszerzenie hello BEGIN. Aby uzyskać więcej informacji, zobacz Tematy hello, występujący w odwołaniu w hello [obsługiwane usługi](#supported-services) sekcji tego artykułu.

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

