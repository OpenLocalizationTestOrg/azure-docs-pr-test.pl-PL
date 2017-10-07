---
title: aaaAutomated poprawki dla programu SQL Server VMs (Resource Manager) | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji Automatyczne stosowanie poprawek powitania dla programu SQL Server maszyn wirtualnych działających na platformie Azure za pomocą Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Automatyczne stosowanie poprawek dla programu SQL Server w usłudze Azure Virtual Machines (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-patching.md)
> * [Wdrożenie klasyczne](../classic/sql-automated-patching.md)
> 
> 

Automatyczne Patching ustanawia okna obsługi dla maszyny wirtualnej platformy Azure działa program SQL Server. Automatyczne aktualizacje można zainstalować tylko w tym oknie obsługi. Dla programu SQL Server to rescriction gwarantuje, że aktualizacje systemu i ponowne uruchomienia, skojarzone są wykonywane hello najlepsze możliwe hello bazy danych. Automatyczne Patching zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Zobacz tooview hello klasycznej wersji w tym artykule [automatyczne stosowanie poprawek dla programu SQL Server w klasycznym maszyny wirtualne Azure](../classic/sql-automated-patching.md).

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

* [Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview) Jeśli planujesz tooconfigure automatyczne stosowanie poprawek przy użyciu programu PowerShell.

> [!NOTE]
> Automatyczne Patching polega na powitania rozszerzenia agenta programu SQL Server IaaS. Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie. Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Ustawienia
Witaj poniższej tabeli opisano opcje hello, które można skonfigurować dla automatyczne stosowanie poprawek. kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.

| Ustawienie | Możliwe wartości | Opis |
| --- | --- | --- |
| **Automatyczne stosowanie poprawek** |Włącza/wyłącza (wyłączone) |Włącza lub wyłącza automatyczne stosowanie poprawek dla maszyny wirtualnej platformy Azure. |
| **Harmonogram konserwacji** |Codziennie, poniedziałek, Wtorek, środę, czwartek, piątek, sobota, niedziela |Harmonogram Hello pobieranie i instalowanie aktualizacji systemu Windows, programu SQL Server i Microsoft dla maszyny wirtualnej. |
| **Godzina rozpoczęcia konserwacji** |0-24 |Witaj uruchamiania lokalnego czasu tooupdate hello maszyny wirtualnej. |
| **Czas trwania okna obsługi** |30-180 |Witaj liczbę minut dozwolone toocomplete hello pobierania i instalacji aktualizacji. |
| **Poprawka kategorii** |Ważne |Kategoria Hello toodownload aktualizacji i instalacji. |

## <a name="configuration-in-hello-portal"></a>Konfiguracja w hello portalu
Można użyć hello tooconfigure portalu Azure automatyczne stosowanie poprawek podczas inicjowania obsługi lub dla istniejących maszyn wirtualnych.

### <a name="new-vms"></a>Nowe maszyny wirtualne
Użyj hello tooconfigure portalu Azure automatyczne stosowanie poprawek podczas tworzenia nowej maszyny wirtualnej serwera SQL w modelu wdrażania usługi Resource Manager hello.

W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne stosowanie poprawek**. Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **automatyczne stosowanie poprawek SQL** bloku.

![SQL automatyczne stosowanie poprawek w portalu Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Istniejące maszyny wirtualne
W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server. Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.

![SQL automatyczne stosowanie poprawek dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

W hello **konfigurację programu SQL Server** bloku, kliknij przycisk hello **Edytuj** przycisku na powitania automatycznego stosowania poprawek sekcji.

![Skonfiguruj automatyczne stosowanie poprawek SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.

Jeśli włączasz automatyczne stosowanie poprawek dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello. W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatyczne stosowanie poprawek. Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany. Po tym hello Azure portal odzwierciedla hello nowych ustawień.

> [!NOTE]
> Można również skonfigurować automatyczne stosowanie poprawek za pomocą szablonu. Aby uzyskać więcej informacji, zobacz [szablon Szybki Start Azure automatyczne stosowanie poprawek](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Konfiguracja przy użyciu programu PowerShell
Po aprowizacji maszyny Wirtualnej SQL, użyj programu PowerShell tooconfigure automatyczne stosowanie poprawek.

Poniższy przykład hello, programu PowerShell jest używane tooconfigure automatyczne stosowanie poprawek na istniejącej maszyny Wirtualnej programu SQL Server. Witaj **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** polecenie konfiguruje nowe okno obsługi, aktualizacje automatyczne.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

Na podstawie tego przykładu, hello poniższej tabeli opisano praktyce hello w celu hello maszyny Wirtualnej platformy Azure:

| Parametr | Efekt |
| --- | --- |
| **DayOfWeek** |Każdy czwartek zainstalowanych poprawek. |
| **MaintenanceWindowStartingHour** |Aktualizacje BEGIN o 11:00. |
| **MaintenanceWindowsDuration** |Poprawki muszą być zainstalowane w ciągu 120 minut. Na podstawie hello czasu rozpoczęcia, użytkownicy muszą wykonać przez 1:00 pm. |
| **PatchCategory** |Witaj, to tylko możliwe ustawienie tego parametru to **ważne**. |

Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.

toodisable automatyczne stosowanie poprawek, uruchom hello sam skrypt bez hello **-Włącz** toohello parametru **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**. Witaj braku hello **-Włącz** parametru sygnały hello polecenia toodisable hello funkcji.

## <a name="next-steps"></a>Następne kroki
Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

