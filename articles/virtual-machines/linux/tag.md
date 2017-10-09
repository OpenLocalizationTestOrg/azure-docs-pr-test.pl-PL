---
title: tootag aaaHow maszyny wirtualnej systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat znakowanie Azure maszyny wirtualnej systemu Linux utworzone na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Jak tootag maszyny wirtualnej systemu Linux na platformie Azure
W tym artykule opisano różne sposoby tootag maszyny wirtualnej systemu Linux na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager hello. Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów. Obecnie Azure obsługuje tagi too15 według zasobu i grupy zasobów. Tagi mogą być umieszczane w zasobie na powitania godzina utworzenia lub dodać tooan istniejącego zasobu. Należy pamiętać, tagi są obsługiwane dla zasobów utworzone za pośrednictwem modelu wdrażania usługi Resource Manager hello tylko.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Znakowanie za pomocą interfejsu wiersza polecenia platformy Azure
toobegin, potrzebujesz hello najnowszych [2.0 interfejsu wiersza polecenia platformy Azure (wersja zapoznawcza)](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Można również wykonać te kroki hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Wszystkie właściwości można wyświetlić dla podanej maszyny wirtualnej, w tym hello tagów, za pomocą tego polecenia:

        az vm show --resource-group MyResourceGroup --name MyTestVM

tooadd nowy znacznik maszyny Wirtualnej za pośrednictwem hello wiersza polecenia platformy Azure, można użyć hello `azure vm update` polecenia wraz z parametru tag hello **— Ustawianie**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

tagi tooremove, można użyć hello **— Usuń** parametru w hello `azure vm update` polecenia.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


Firma Microsoft zastosowano tagi zasobów tooour wiersza polecenia platformy Azure i hello portalu Spójrzmy na powitania użycia szczegóły toosee hello tagów w portalu rozliczeń hello.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [tooorganize przy użyciu tagów zasobów platformy Azure] [ Using Tags tooorganize your Azure Resources].
* toosee tagi ułatwia zarządzanie korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
