---
title: aaaAutomated poprawki dla programu SQL Server VMs (klasyczne) | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji Automatyczne stosowanie poprawek powitania dla SQL Server maszyn wirtualnych działających w trybie klasycznym wdrożenia hello Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Automatyczne stosowanie poprawek dla programu SQL Server na maszynach wirtualnych platformy Azure (klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Wdrożenie klasyczne](../classic/sql-automated-patching.md)
> 
> 

Automatyczne Patching ustanawia okna obsługi dla maszyny wirtualnej platformy Azure działa program SQL Server. Automatyczne aktualizacje można zainstalować tylko w tym oknie obsługi. Dla programu SQL Server zapewnia, że aktualizacje systemu i ponowne uruchomienia, skojarzone są wykonywane hello najlepsze możliwe hello bazy danych. Automatyczne Patching zależy od hello [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. wersja Menedżera zasobów hello tooview tego artykułu, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w Menedżerze zasobów maszyn wirtualnych Azure](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Wymagania wstępne
toouse automatyczne stosowanie poprawek, należy wziąć pod uwagę następujące wymagania wstępne hello:

**System operacyjny**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Wersja programu SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Program Azure PowerShell**:

* [Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).

**Rozszerzenia programu SQL Server IaaS**:

* [Zainstaluj hello IaaS rozszerzenie dotyczące programu SQL Server](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Ustawienia
Witaj poniższej tabeli opisano opcje hello, które można skonfigurować dla automatyczne stosowanie poprawek. Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooconfigure te ustawienia.

| Ustawienie | Możliwe wartości | Opis |
| --- | --- | --- |
| **Automatyczne stosowanie poprawek** |Włącza/wyłącza (wyłączone) |Włącza lub wyłącza automatyczne stosowanie poprawek dla maszyny wirtualnej platformy Azure. |
| **Harmonogram konserwacji** |Codziennie, poniedziałek, Wtorek, środę, czwartek, piątek, sobota, niedziela |Harmonogram Hello pobieranie i instalowanie aktualizacji systemu Windows, programu SQL Server i Microsoft dla maszyny wirtualnej. |
| **Godzina rozpoczęcia konserwacji** |0-24 |Witaj uruchamiania lokalnego czasu tooupdate hello maszyny wirtualnej. |
| **Czas trwania okna obsługi** |30-180 |Witaj liczbę minut dozwolone toocomplete hello pobierania i instalacji aktualizacji. |
| **Poprawka kategorii** |Ważne |Kategoria Hello toodownload aktualizacji i instalacji. |

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell
Poniższy przykład hello, programu PowerShell jest używane tooconfigure automatyczne stosowanie poprawek na istniejącej maszyny Wirtualnej programu SQL Server. Witaj **AzureVMSqlServerAutoPatchingConfig nowy** polecenie konfiguruje nowe okno obsługi, aktualizacje automatyczne.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

Na podstawie tego przykładu, hello poniższej tabeli opisano praktyce hello w celu hello maszyny Wirtualnej platformy Azure:

| Parametr | Efekt |
| --- | --- |
| **DayOfWeek** |Każdy czwartek zainstalowanych poprawek. |
| **MaintenanceWindowStartingHour** |Aktualizacje BEGIN o 11:00. |
| **MaintenanceWindowsDuration** |Poprawki muszą być zainstalowane w ciągu 120 minut. Na podstawie hello czasu rozpoczęcia, użytkownicy muszą wykonać przez 1:00 pm. |
| **PatchCategory** |Witaj tylko ustawień dla tego parametru jest "Ważne". |

Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.

toodisable automatyczne stosowanie poprawek, uruchom hello sam skrypt bez hello - Włącz parametr toohello AzureVMSqlServerAutoPatchingConfig nowy. Zgodnie z instalacją, może upłynąć kilka minut toodisable automatyczne stosowanie poprawek.

## <a name="next-steps"></a>Następne kroki
Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

