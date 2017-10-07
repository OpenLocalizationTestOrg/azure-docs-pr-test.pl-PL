---
title: "grupy NSG aaaManage przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage istniejących grup NSG przy użyciu hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Zarządzanie za pomocą portalu hello grupy NSG

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [Program PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Pobieranie informacji
Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.

### <a name="view-existing-nsgs"></a>Wyświetlanie istniejących grup NSG

tooview wszystkich istniejących grup NSG w ramach subskrypcji, pełną hello następujące kroki:

1. W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.

2. Kliknij przycisk **Przeglądaj >** > **sieciowej grupy zabezpieczeń**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Sprawdź listę hello grup NSG w hello **sieciowej grupy zabezpieczeń** bloku.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Widok grup NSG, w grupie zasobów

tooview hello lista grup NSG w hello **NSG zarządcy zasobów** grupy zasobów, pełny hello następujące kroki:

1. Kliknij przycisk **grup zasobów >** > **NSG zarządcy zasobów** > **...** .

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Hello listy zasobów, szukać elementów Wyświetlanie hello NSG ikony, jak pokazano w hello **zasobów** bloku poniżej.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Wyświetl listę wszystkich reguł dla grupy NSG

tooview hello reguły NSG o nazwie **frontonu NSG**pełnego hello następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.

2. W hello **ustawienia** , kliknij pozycję **reguły zabezpieczeń dla ruchu przychodzącego**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Witaj **reguły zabezpieczeń dla ruchu przychodzącego** bloku jest wyświetlana, jak pokazano poniżej.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. W hello **ustawienia** , kliknij pozycję **reguł zabezpieczeń dla ruchu wychodzącego** toosee hello reguł dla ruchu wychodzącego.

    > [!NOTE]
    > reguły domyślne tooview, kliknij przycisk hello **domyślne zasady** ikona u góry bloku hello, który wyświetla reguły hello hello.
    >

### <a name="view-nsgs-associations"></a>Wyświetlanie grup NSG powiązań

tooview hello jakie zasoby **frontonu NSG** grupa NSG jest pełną, powiąż z hello następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.

2. W hello **ustawienia** , kliknij pozycję **podsieci** tooview podsieci, które są skojarzone toohello NSG.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. W hello **ustawienia** , kliknij pozycję **interfejsy sieciowe** tooview co karty sieciowe są skojarzone toohello NSG.

## <a name="manage-rules"></a>Zarządzaj regułami
Można dodawać reguły tooan istniejące grupy NSG, edytować istniejące zasady i Usuń reguły.

### <a name="add-a-rule"></a>Dodawanie reguły
tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **NSG frontonu** NSG, pełną hello następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.
2. W hello **ustawienia** , kliknij pozycję **reguły zabezpieczeń dla ruchu przychodzącego**.
3. W hello **reguły zabezpieczeń dla ruchu przychodzącego** bloku, kliknij przycisk **Dodaj**. Następnie w hello **Dodaj regułę zabezpieczeń dla ruchu przychodzącego** bloku, wypełnij hello wartości, jak pokazano poniżej, a następnie kliknij **OK**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Po kilku sekundach zauważyć hello nową regułę w hello **reguły zabezpieczeń dla ruchu przychodzącego** bloku.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Zmień reguły
Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** hello pełną, tylko następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.
2. W hello **ustawienia** , kliknij pozycję reguły hello utworzone powyżej.
3. W hello **Zezwalaj https** bloku, zmień hello **źródła** właściwości, jak pokazano poniżej, a następnie kliknij przycisk **zapisać**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Usuwanie reguły

toodelete hello reguły utworzone powyżej, pełną hello następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.
2. W hello **ustawienia** , kliknij pozycję reguły hello utworzone powyżej.
3. W hello **Zezwalaj https** bloku, kliknij przycisk **usunąć**, a następnie kliknij przycisk **tak**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Zarządzanie skojarzenia
Możesz skojarzyć toosubnets NSG i kart interfejsu sieciowego. Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.

### <a name="associate-an-nsg-tooa-nic"></a>Kojarzenie grupy NSG tooa karty Sieciowej
Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:

1. Z hello **sieciowej grupy zabezpieczeń** bloku lub hello **zasobów** bloku przedstawionych powyżej, kliknij przycisk **frontonu NSG**.
2. W hello **ustawienia** , kliknij pozycję **interfejsy sieciowe** > **skojarzyć** > **TestNICWeb1**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Usuń skojarzenie grupy NSG z karty Sieciowej

Witaj toodissociate **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:

1. Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestNICWeb1**.

2. W hello **TestNICWeb1** bloku, kliknij przycisk **zmiany zabezpieczeń...**   >  **Brak**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Umożliwia także tego bloku tooassociate hello kart tooany istniejące grupy NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Usuń skojarzenie grupy NSG z podsiecią

Witaj toodissociate **frontonu NSG** grupy NSG z hello **frontonu** podsieci, pełną hello następujące kroki:

1. Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestVNet**.

2. W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Brak**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. W hello **frontonu** bloku, kliknij przycisk **zapisać**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Kojarzenie grupy NSG podsieci tooa

Witaj tooassociate **frontonu NSG** NSG toohello **FronEnd** ponownie podsieci, pełną hello następujące kroki:

1. Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **TestVNet**.
2. W hello **ustawienia** bloku, kliknij przycisk **podsieci** > **frontonu** > **sieciowej grupy zabezpieczeń**  >  **Frontonu NSG**.
3. W hello **frontonu** bloku, kliknij przycisk **zapisać**.

> [!NOTE]
> Można również skojarzyć podsieci tooa grupy NSG z thh NSG **ustawienia** bloku.
>

## <a name="delete-an-nsg"></a>Usuwanie grupy NSG
Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów. toodelete grupy NSG, pełną hello następujące kroki:.

1. Witaj portalu Azure kliknij **grup zasobów >** > **NSG zarządcy zasobów** > **...**   >  **Frontonu NSG**.
2. W hello **ustawienia** bloku, kliknij przycisk **interfejsy sieciowe**.
3. W przypadku wszystkie karty sieciowe na liście kliknij hello karty Sieciowej i wykonaj krok 2 w [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC).
4. Powtórz krok 3 dla każdej karty sieciowej.
5. W hello **ustawienia** bloku, kliknij przycisk **podsieci**.
6. Jeśli ma żadnych podsieci na liście, kliknij hello podsieci i wykonaj kroki 2 i 3 w [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet).
7. Przewija po lewej stronie toohello **frontonu NSG** bloku, następnie kliknij przycisk **usunąć** > **tak**.

    ![Portal Azure — grup NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Następne kroki
* [Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.
