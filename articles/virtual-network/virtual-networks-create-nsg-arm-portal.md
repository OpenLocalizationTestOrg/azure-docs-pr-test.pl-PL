---
title: "grupy zabezpieczeń sieci aaaManage - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a>Zarządzanie grupami zabezpieczeń sieci przy użyciu hello portalu Azure

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

w powyższym scenariuszu hello na podstawie próbek Hello PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone. Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu. Witaj kroków poniżej użyj **NSG zarządcy zasobów** jako nazwę hello hello zasobów grupy hello szablonu został wdrożony.

## <a name="create-hello-nsg-frontend-nsg"></a>Utwórz hello NSG frontonu NSG
Witaj toocreate **frontonu NSG** NSG, jak pokazano w scenariuszu hello powyżej, wykonaj kroki hello poniżej.

1. W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. W hello **sieciowej grupy zabezpieczeń** bloku, kliknij przycisk **Dodaj**.
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. W hello **Utwórz grupę zabezpieczeń sieci** bloku Utwórz grupy NSG o nazwie *frontonu NSG* w hello *NSG zarządcy zasobów* grupy zasobów, a następnie kliknij przycisk **Utwórz**.
   
    ![Portal Azure — grup NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Tworzenie reguł w istniejącej sieciowej grupie zabezpieczeń
reguły toocreate w istniejącej grupy NSG z hello portalu Azure, wykonaj kroki hello poniżej.

1. Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.
2. Na liście hello grup NSG, kliknij **frontonu NSG** > **reguły zabezpieczeń dla ruchu przychodzącego**
   
    ![Portal Azure — frontonu NSG](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Lista hello **reguły zabezpieczeń dla ruchu przychodzącego**, kliknij przycisk **Dodaj**.
   
    ![Portal Azure — Dodaj regułę](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. W hello **Dodaj regułę zabezpieczeń dla ruchu przychodzącego** bloku Utwórz reguły o nazwie *zasada sieci web* z priorytet *200* zezwalania na dostęp za pośrednictwem *TCP* tooport *80* tooany maszyny Wirtualnej z dowolnego źródła, a następnie kliknij przycisk **OK**. Zwróć uwagę, że większość tych ustawień są wartościami domyślnymi już.
   
    ![Portal Azure — ustawienia reguły](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Po kilku sekundach zobaczysz hello nową regułę w hello NSG.
   
    ![Portal Azure — nową regułę](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Powtórz kroki too6 toocreate regułę ruchu przychodzącego o nazwie *reguły protokołu rdp* z priorytet *250* zezwalania na dostęp za pośrednictwem *TCP* tooport *3389* tooany maszyny Wirtualnej z dowolnego źródła.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Skojarz hello NSG toohello frontonu podsieci
1. Kliknij przycisk **Przeglądaj >** > **grup zasobów** > **NSG zarządcy zasobów**.
2. W hello **NSG zarządcy zasobów** bloku, kliknij przycisk **...**   >  **TestVNet**.
   
    ![Portal Azure — TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Frontonu NSG**.
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. W hello **frontonu** bloku, kliknij przycisk **zapisać**.
   
    ![Portal Azure — ustawienia podsieci](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Utwórz hello NSG wewnętrznej bazy danych grupy NSG
toocreate hello **zaplecza NSG** NSG i powiązać ją toohello **zaplecza** podsieci, wykonaj poniższe kroki hello.

1. Hello Powtórz kroki opisane w temacie [hello Utwórz NSG frontonu NSG](#Create-the-NSG-FrontEnd-NSG) toocreate o nazwie grupy NSG *wewnętrznej bazy danych grupy NSG*
2. Hello Powtórz kroki opisane w temacie [tworzenia reguł w istniejącej grupy NSG](#Create-rules-in-an-existing-NSG) toocreate hello **przychodzących** reguły w poniższej tabeli hello.
   
   | Reguła ruchu przychodzącego | Reguła ruchu wychodzącego |
   | --- | --- |
   | ![Portal Azure — reguły dla ruchu przychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal Azure — Reguła ruchu wychodzącego](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Hello Powtórz kroki opisane w temacie [skojarzyć podsieci frontonu toohello NSG hello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **zaplecza NSG** NSG toohello **zaplecza** podsieci.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Zarządzanie istniejących grup NSG](virtual-network-manage-nsg-arm-portal.md)
* [Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.

