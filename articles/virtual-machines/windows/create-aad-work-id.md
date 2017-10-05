---
title: "Tworzenie tożsamości służbowe w usłudze AAD dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć tożsamość firmy lub szkoły w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7694b959a384aaed213adc31e02debca31b7c131
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-windows-vms"></a>Tworzenie tożsamości służbowe w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Windows
Jeśli utworzone osobiste konto platformy Azure lub osobistych subskrypcji MSDN i utworzyć konto platformy Azure, aby skorzystać z środków MSDN Azure — użyto *konta Microsoft* tożsamości, aby go utworzyć. Wiele najważniejszych funkcji Azure-- [Szablony grupy zasobów](../../azure-resource-manager/resource-group-overview.md) przykładem — wymagają konta firmowego lub szkolnego (tożsamość zarządzane przez usługę Azure Active Directory) do pracy. Aby wykonać instrukcjami poniżej, aby utworzyć nowe konta firmowego lub szkolnego, ponieważ na szczęście z czynności najważniejsze informacje osobiste konta platformy Azure jest pochodzi z domyślnej domeny usługi Azure Active Directory służy do tworzenia nowego konta firmowego lub szkolnego korzystające z funkcjami platformy Azure, które tego wymagają.

Jednak ostatnie zmiany umożliwiają Zarządzanie subskrypcją z dowolnego typu za pomocą konta Azure `azure login` metody logowania interakcyjnego opisanej [tutaj](../../xplat-cli-connect.md). Możesz użyć tego mechanizmu, lub możesz wykonać postępuj zgodnie z instrukcjami. Możesz również [tworzenie służbowego tożsamości w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

