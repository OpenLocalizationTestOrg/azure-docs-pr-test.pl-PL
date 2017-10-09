---
title: tootag aaaHow zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o znakowanie utworzona na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello maszynę wirtualną systemu Windows"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Jak tootag maszynę wirtualną systemu Windows na platformie Azure
W tym artykule opisano różne sposoby tootag maszynę wirtualną systemu Windows na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager hello. Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów. Obecnie Azure obsługuje tagi too15 według zasobu i grupy zasobów. Tagi mogą być umieszczane w zasobie na powitania godzina utworzenia lub dodać tooan istniejącego zasobu. Należy pamiętać, że tagi są obsługiwane dla zasobów utworzone za pośrednictwem modelu wdrażania usługi Resource Manager hello tylko. Jeśli chcesz tootag maszyny wirtualnej systemu Linux, zobacz [jak tootag maszyny wirtualnej systemu Linux na platformie Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Znakowanie przy użyciu programu PowerShell
toocreate, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw tooset się z [środowiska PowerShell z usługą Azure Resource Manager][PowerShell environment with Azure Resource Manager]. Po zakończeniu instalacji hello można umieścić znaczniki zasobów obliczeniowych, sieci i magazynu podczas tworzenia lub hello zasób został utworzony za pomocą programu PowerShell. W tym artykule będzie skoncentrować się na wyświetlanie/edytowanie tagów umieszczone na maszynach wirtualnych.

Przejdź najpierw tooa maszyny wirtualnej za pośrednictwem hello `Get-AzureRmVM` polecenia cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Maszyna wirtualna zawiera już znaczników, zostanie wtedy wyświetlone wszystkie tagi hello na zasobu:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Jeśli chcesz tooadd tagów za pomocą programu PowerShell, możesz użyć hello `Set-AzureRmResource` polecenia. Należy zwrócić uwagę podczas aktualizowania tagów za pomocą programu PowerShell, tagi są aktualizowane jako całość. Dlatego w przypadku dodawania jeden tag tooa zasób, który ma już tagi, konieczne będzie tooinclude wszystkie tagi hello, które mają toobe dotyczącymi zasobów hello. Poniżej przedstawiono przykładowy sposób tooadd dodatkowe znaczniki tooa zasobów za pomocą poleceń cmdlet programu PowerShell.

To pierwsze polecenie cmdlet ustawia wszystkich znaczników hello dotyczącymi *MyTestVM* toohello *$tags* zmiennej przy użyciu hello `Get-AzureRmResource` i `Tags` właściwości.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

drugie polecenie Hello Wyświetla hello tagów hello podane zmiennej.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

trzecie polecenie Hello dodaje toohello dodatkowe tag *$tags* zmiennej. Należy zwrócić uwagę użycie hello hello  **+=**  tooappend hello nowe toohello pary klucz wartość *$tags* listy.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

polecenie czwarty Hello ustawia wszystkich znaczników hello zdefiniowane w hello *$tags* zmiennej toohello danego zasobu. W takim przypadku jest MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

polecenie piątym powitania Wyświetla wszystkie znaczniki hello hello zasobu. Jak widać, *lokalizacji* jest teraz zdefiniowany jako tag *MyLocation* jako wartość hello.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

więcej informacji o toolearn znakowanie za pomocą programu PowerShell, zapoznaj się z hello [polecenia cmdlet usługi Azure Resource][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [tooorganize przy użyciu tagów zasobów platformy Azure] [ Using Tags tooorganize your Azure Resources].
* toosee tagi ułatwia zarządzanie korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
