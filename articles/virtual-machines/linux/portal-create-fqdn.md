---
title: Nazwa FQDN maszyny Wirtualnej systemu Linux, w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate w pełni kwalifikowana nazwa domeny lub nazwę FQDN dla Menedżera zasobów na podstawie maszyny wirtualnej w hello portalu Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Tworzenie w pełni kwalifikowaną nazwą domeny na powitania portalu Azure dla maszyny Wirtualnej systemu Linux

Po utworzeniu maszyny wirtualnej (VM) hello [portalu Azure](https://portal.azure.com), publicznego adresu IP zasobu hello maszyny wirtualnej jest tworzony automatycznie. Możesz użyć tego adresu IP adres tooremotely dostępu hello maszyny Wirtualnej. Mimo że nie tworzy hello portal [pełną nazwę domeny](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), lub w pełni kwalifikowaną nazwę domeny, możesz dodać kategorię, po hello zostanie utworzona maszyna wirtualna. W tym artykule przedstawiono hello kroki toocreate nazwy DNS lub nazwy FQDN.

## <a name="create-a-fqdn"></a>Utwórz nazwę FQDN
W tym artykule przyjęto założenie, że utworzono już maszyny Wirtualnej. W razie potrzeby można [tworzenie maszyny Wirtualnej w portalu hello](quick-create-portal.md) lub [z hello Azure CLI](quick-create-cli.md). Po skonfigurowaniu i uruchomieniu maszyny Wirtualnej, wykonaj następujące kroki:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Teraz można podłączyć zdalnie toohello maszyny Wirtualnej przy użyciu tego DNS nazwa takich jak z `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy maszyna wirtualna ma nazwę publicznego adresu IP i DNS, można wdrożyć wspólnej struktury aplikacji lub usług, takich jak nginx, bazy danych MongoDB, Docker, itp.

Można również uzyskać więcej informacji [za pomocą Menedżera zasobów](../../azure-resource-manager/resource-group-overview.md) porady na temat budowania Azure wdrożeń.

