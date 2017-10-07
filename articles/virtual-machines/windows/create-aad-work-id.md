---
title: "aaaCreate służbowego tożsamości w usłudze AAD dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate służbowego tożsamości w usłudze Azure Active Directory toouse maszynom wirtualnym z systemem Windows."
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
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a>Tworzenie tożsamości służbowe w toouse usługi Azure Active Directory z maszynami wirtualnymi systemu Windows
Jeśli utworzone osobiste konto platformy Azure lub osobistych subskrypcji MSDN i utworzyć hello konta Azure tootake z środków na korzystanie hello MSDN Azure — użyto *konta Microsoft* toocreate tożsamości go. Wiele najważniejszych funkcji Azure-- [Szablony grupy zasobów](../../azure-resource-manager/resource-group-overview.md) przykładem — wymagają konta firmowego lub szkolnego (tożsamości zarządzanych przez usługę Azure Active Directory) toowork. Możesz wykonać instrukcje hello poniżej toocreate się, że nowe służbowego konta, ponieważ na szczęście z hello czynności najważniejsze informacje osobiste konta platformy Azure jest czy pochodzą z domyślną domenę usługi Azure Active Directory służy toocreate nowej pracy lub nauki konto, które można używać z funkcje platformy Azure, które tego wymagają.

Jednak najnowszych zmian była możliwa toomanage subskrypcji z dowolnego typu konta platformy Azure przy użyciu hello `azure login` metody logowania interakcyjnego opisanej [tutaj](../../xplat-cli-connect.md). Możesz użyć tego mechanizmu, lub możesz wykonać hello postępuj zgodnie z instrukcjami. Możesz również [tworzenie służbowego tożsamości w usłudze Azure Active Directory toouse z maszyn wirtualnych systemu Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

