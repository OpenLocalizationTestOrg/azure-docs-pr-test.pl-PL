---
title: "Różne sposoby tworzenia maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla listę różnych sposobów tworzenia maszyny wirtualnej systemu Windows za pomocą Menedżera zasobów."
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a>Różne sposoby tworzenia maszyny wirtualnej systemu Windows

System Azure oferuje różne sposoby tworzenia maszyny wirtualnej, ponieważ maszyny wirtualne są odpowiednie dla różnych użytkowników i celów. Oznacza to, należy wybrać niektóre opcje dotyczące maszyny wirtualnej i utwórz go. Ten artykuł zawiera podsumowanie tych opcji i linki do instrukcji.

## <a name="azure-portal"></a>Azure Portal
Przy użyciu portalu Azure jest prosty sposób na wypróbowanie maszynę wirtualną, zwłaszcza jeśli zaczynasz przy użyciu platformy Azure. 

[Tworzenie maszyny wirtualnej z systemem Windows przy użyciu portalu](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Szablon
Maszyny wirtualne wymagają różnych zasobów (np. o dostępności zestawów i kont magazynu). Zamiast wdrażanie i zarządzanie każdego zasobu oddzielnie, można utworzyć szablonu usługi Azure Resource Manager, który wdraża i udostępnia wszystkie zasoby w jednej, skoordynowanej operacji.

* [Tworzenie maszyny wirtualnej z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Jeśli wolisz Praca w powłoce poleceń, można użyć programu Azure PowerShell.

* [Tworzenie maszyny wirtualnej z systemem Windows przy użyciu programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Do tworzenia, zarządzania i wdrażania maszyn wirtualnych przy użyciu narzędzi platformy Azure dla programu Visual Studio i zestawu Azure SDK, należy użyć programu Visual Studio.

[Azure Tools dla programu Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

