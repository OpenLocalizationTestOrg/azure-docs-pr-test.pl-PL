---
title: Nazwa FQDN maszyny Wirtualnej systemu Windows, w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate w pełni kwalifikowana nazwa domeny lub nazwę FQDN dla Menedżera zasobów na podstawie maszyny wirtualnej w hello portalu Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Tworzenie w pełni kwalifikowaną nazwą domeny na powitania portalu Azure dla maszyny Wirtualnej systemu Windows

Po utworzeniu maszyny wirtualnej (VM) hello [portalu Azure](https://portal.azure.com), publicznego adresu IP zasobu hello maszyny wirtualnej jest tworzony automatycznie. Możesz użyć tego adresu IP adres tooremotely dostępu hello maszyny Wirtualnej. Mimo że nie tworzy hello portal [pełną nazwę domeny](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), lub nazwę FQDN, możesz ją utworzyć utworzone hello maszyny Wirtualnej. W tym artykule przedstawiono hello kroki toocreate nazwy DNS lub nazwy FQDN.

## <a name="create-a-fqdn"></a>Utwórz nazwę FQDN
W tym artykule przyjęto założenie, że utworzono już maszyny Wirtualnej. W razie potrzeby można [tworzenie maszyny Wirtualnej w portalu hello](quick-create-portal.md) lub [przy użyciu programu Azure PowerShell](quick-create-powershell.md). Po skonfigurowaniu i uruchomieniu maszyny Wirtualnej, wykonaj następujące kroki:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Teraz można podłączyć zdalnie toohello maszyny Wirtualnej przy użyciu tej nazwy DNS takich jak dla protokołu RDP (Remote Desktop).

## <a name="next-steps"></a>Następne kroki
Teraz, gdy maszyna wirtualna ma nazwę publicznego adresu IP i DNS, można wdrożyć wspólnej struktury aplikacji lub usług, takich jak IIS, SQL i programu SharePoint.

Można również uzyskać więcej informacji [za pomocą Menedżera zasobów](../../azure-resource-manager/resource-group-overview.md) porady na temat budowania Azure wdrożeń.

