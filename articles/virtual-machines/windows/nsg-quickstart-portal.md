---
title: "aaaOpen portów tooa maszynę Wirtualną przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Windows przy użyciu modelu wdrażania Menedżera zasobów hello w hello portalu Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Jak tooopen porty tooa maszynę wirtualną z hello portalu Azure
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Szybkie polecenia
Możesz również [wykonaj te czynności przy użyciu programu Azure PowerShell](nsg-quickstart-powershell.md).

Najpierw należy utworzyć grupy zabezpieczeń sieci. Wybierz, wybierz grupę zasobów, w portalu hello **Dodaj**, następnie wyszukaj i wybierz **sieciowej grupy zabezpieczeń**:

![Dodaj grupę zabezpieczeń sieci](./media/nsg-quickstart-portal/add-nsg.png)

Wprowadź nazwę dla swojej grupy zabezpieczeń sieci, wybierz lub Utwórz grupę zasobów, a następnie wybierz lokalizację. Wybierz **Utwórz** po zakończeniu:

![Utwórz grupę zabezpieczeń sieci](./media/nsg-quickstart-portal/create-nsg.png)

Wybierz nową grupę zabezpieczeń sieci. Wybierz "Reguły zabezpieczeń ruchu przychodzącego", a następnie wybierz hello **Dodaj** toocreate przycisk reguły:

![Dodaj regułę ruchu przychodzącego](./media/nsg-quickstart-portal/add-inbound-rule.png)

Wybierz popularne **usługi** z menu rozwijanego hello, takich jak *HTTP*. Możesz też wybrać *niestandardowy* tooprovide toouse określonego portu. W razie potrzeby można zmienić priorytet hello lub nazwy. Witaj priorytet ma wpływ hello kolejności w której reguły są stosowane - hello niższą wartość liczbową hello, hello wcześniejszych hello jest stosowana reguła. Możesz też wybrać **zaawansowane** u góry tego ekranu tooenter hello określonego źródła zakres bloku lub portu IP, na przykład. Gdy wszystko będzie gotowe, wybierz **OK** toocreate hello reguły:

![Utwórz regułę ruchu przychodzącego](./media/nsg-quickstart-portal/create-inbound-rule.png)

Z ostatnim krokiem jest tooassociate grupy zabezpieczeń sieci z podsiecią lub w konkretnym interfejsie sieciowym. Umożliwia kojarzenie hello sieciową grupę zabezpieczeń z podsiecią. Wybierz **podsieci**, a następnie wybierz **skojarzyć**:

![Skojarzenia sieciowej grupy zabezpieczeń z podsiecią](./media/nsg-quickstart-portal/associate-subnet.png)

Wybierz sieci wirtualnej, a następnie wybierz odpowiednie podsieci hello:

![Kojarzenie grupy zabezpieczeń sieci z obsługą sieci wirtualnej](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Teraz utworzono grupę zabezpieczeń sieci, utworzyć regułę ruchu przychodzącego, która zezwala na ruch na porcie 80, a jego skojarzony z podsiecią. Wszystkie maszyny wirtualne połączyć toothat podsieci są dostępne na porcie 80.

## <a name="more-information-on-network-security-groups"></a>Więcej informacji na temat grup zabezpieczeń sieci
Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej. Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour. Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure. Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu. Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).

## <a name="next-steps"></a>Następne kroki
W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła. Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:

* [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Co to jest sieciowa grupa zabezpieczeń?](../../virtual-network/virtual-networks-nsg.md)