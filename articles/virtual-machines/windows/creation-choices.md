---
title: "aaaDifferent sposobów toocreate maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla listę toocreate różne sposoby hello maszynę wirtualną za pomocą Menedżera zasobów systemu Windows."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Różne sposoby toocreate maszyny wirtualnej systemu Windows

System Azure oferuje różne sposoby toocreate maszyny wirtualnej, ponieważ maszyny wirtualne są odpowiednie dla różnych użytkowników i celów. To oznacza, że konieczne toomake niektóre opcje dotyczące maszyny wirtualnej hello i w jaki sposób toocreate go. Ten artykuł zawiera podsumowanie tych opcji oraz łączy tooinstructions.

## <a name="azure-portal"></a>Azure Portal
Przy użyciu portalu Azure hello jest tootry prosty sposób limit maszynę wirtualną, zwłaszcza, jeśli zaczynasz przy użyciu platformy Azure. 

[Utwórz maszynę wirtualną z systemem Windows przy użyciu portalu hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Szablon
Maszyny wirtualne wymagają różnych zasobów (np. o dostępności zestawów i kont magazynu). Zamiast wdrażanie i zarządzanie każdego zasobu oddzielnie, można utworzyć szablonu usługi Azure Resource Manager, który wdraża i udostępnia wszystkie zasoby hello w jednej, skoordynowanej operacji.

* [Tworzenie maszyny wirtualnej z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Jeśli wolisz Praca w powłoce poleceń, można użyć programu Azure PowerShell.

* [Tworzenie maszyny wirtualnej z systemem Windows przy użyciu programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Użyj toobuild programu Visual Studio, zarządzać i wdrażanie maszyn wirtualnych o hello Azure Tools dla programu Visual Studio oraz hello Azure SDK.

[Azure Tools dla programu Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

