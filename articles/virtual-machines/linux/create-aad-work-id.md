---
title: "aaaCreate służbowego tożsamości w usłudze AAD dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate służbowego tożsamości w usłudze Azure Active Directory toouse z maszyn wirtualnych systemu Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a>Tworzenie tożsamości służbowe w usłudze Azure Active Directory toouse z maszyn wirtualnych systemu Linux
Jeśli utworzone osobiste konto platformy Azure lub osobistych subskrypcji MSDN i utworzyć hello konta Azure tootake z środków na korzystanie hello MSDN Azure — użyto *konta Microsoft* toocreate tożsamości go. Wiele najważniejszych funkcji Azure-- [Szablony grupy zasobów](../../azure-resource-manager/resource-group-overview.md) przykładem — wymagają konta firmowego lub szkolnego (tożsamości zarządzanych przez usługę Azure Active Directory) toowork. Możesz wykonać instrukcje hello poniżej toocreate się, że nowe służbowego konta, ponieważ na szczęście z hello czynności najważniejsze informacje osobiste konta platformy Azure jest czy pochodzą z domyślną domenę usługi Azure Active Directory służy toocreate nowej pracy lub nauki konto, które można używać z funkcje platformy Azure, które tego wymagają.

Jednak najnowszych zmian była możliwa toomanage subskrypcji z dowolnego typu konta platformy Azure przy użyciu hello `azure login` metody logowania interakcyjnego opisanej [tutaj](../../xplat-cli-connect.md). Możesz użyć tego mechanizmu, lub możesz wykonać hello postępuj zgodnie z instrukcjami. Możesz również [utworzyć tożsamość firmy lub szkoły w toouse usługi Azure Active Directory z maszynami wirtualnymi systemu Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

