---
title: "aaaTroubleshooting maszyny Wirtualnej systemu Linux błędów alokacji | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyny Wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a>Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyn wirtualnych systemu Linux na platformie Azure
Podczas tworzenia maszyny Wirtualnej, ponownego uruchomienia zatrzymanej maszyny wirtualnej (cofnięciu przydziału) lub zmień rozmiar maszyny Wirtualnej Microsoft Azure przydziela zasoby obliczeniowe tooyour subskrypcji. Czasami może pojawić błędy podczas przeprowadzania tych operacji — nawet zanim przejdziesz hello limity subskrypcji platformy Azure. W tym artykule opisano niektóre typowe błędy alokacji hello hello przyczyny, a także sugeruje możliwe korygowania. Planując wdrożenie hello usług Hello informacje mogą być również przydatne. Możesz również [Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyn wirtualnych systemu Windows na platformie Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

