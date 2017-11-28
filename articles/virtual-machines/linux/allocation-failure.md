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
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="f4186-103">Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f4186-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="f4186-104">Podczas tworzenia maszyny Wirtualnej, ponownego uruchomienia zatrzymanej maszyny wirtualnej (cofnięciu przydziału) lub zmień rozmiar maszyny Wirtualnej Microsoft Azure przydziela zasoby obliczeniowe tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f4186-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="f4186-105">Czasami może pojawić błędy podczas przeprowadzania tych operacji — nawet zanim przejdziesz hello limity subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4186-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="f4186-106">W tym artykule opisano niektóre typowe błędy alokacji hello hello przyczyny, a także sugeruje możliwe korygowania.</span><span class="sxs-lookup"><span data-stu-id="f4186-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="f4186-107">Planując wdrożenie hello usług Hello informacje mogą być również przydatne.</span><span class="sxs-lookup"><span data-stu-id="f4186-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="f4186-108">Możesz również [Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyn wirtualnych systemu Windows na platformie Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4186-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

