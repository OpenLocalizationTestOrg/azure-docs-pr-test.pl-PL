---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych (klasyczne) — portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych (klasyczne) za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej (klasyczne) przy użyciu hello portalu Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Zarządzanie statycznego prywatnego adresu IP w modelu wdrażania usługi Resource Manager hello](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Poniższe kroki przykładowe Hello oczekiwać środowisku niezłożonym już utworzone. Jeśli kroki hello toorun wyświetlaną w tym dokumencie, należy najpierw utworzyć hello środowisko testowe opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Jak toospecify statycznych prywatnych adresów IP podczas tworzenia maszyny Wirtualnej
toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:

1. W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **nowy** > **obliczeniowe** > **systemu Windows Server 2012 R2 Datacenter**, zwróć uwagę, że hello **wybierz model wdrożenia** listy już pokazuje **klasycznego**, a następnie kliknij przycisk **Utwórz**.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. W hello **Utwórz maszynę Wirtualną** bloku, wprowadź nazwę hello hello toobe maszyny Wirtualnej utworzone (*DNS01* w naszym scenariuszu), hello konta administratora lokalnego i hasło.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Kliknij przycisk **konfiguracji opcjonalnej** > **sieci** > **sieci wirtualnej**, a następnie kliknij przycisk **TestVNet**. Jeśli **TestVNet** jest niedostępny, upewnij się, że używasz hello *środkowe stany USA* lokalizacji i utworzeniu hello środowisko testowe opisane na początku hello tego artykułu.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. W hello **sieci** jest upewnij się, że podsieci hello aktualnie zaznaczonego bloku *frontonu*, następnie kliknij przycisk **adresów IP**w obszarze **przypisywania adresów IP** kliknij **statycznych**, a następnie wprowadź *192.168.1.101* dla **adres IP** jak pokazano poniżej.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Kliknij przycisk **OK** w hello **adresów IP** bloku, następnie kliknij przycisk **OK** w hello **sieci** bloku, a następnie kliknij przycisk **OK**w hello **opcjonalne config** bloku.
7. W hello **Utwórz maszynę Wirtualną** bloku, kliknij przycisk **Utwórz**. Powiadomienie hello kafelka poniżej wyświetlane na pulpicie nawigacyjnym.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej
tooview hello statycznych prywatne informacje o adresie IP dla hello się, że maszyna wirtualna utworzona z powyższych kroków hello wykonaj poniższe kroki hello.

1. W portalu Azure, Azure hello, kliknij polecenie **PRZEGLĄDAJ wszystko** > **maszyn wirtualnych (klasyczne)** > **DNS01**  >   **Wszystkie ustawienia** > **adresów IP** i zwróć uwagę, hello przypisywania adresów IP i adres IP, jak pokazano poniżej.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej
tooremove hello statycznego prywatnego adresu IP z powitalne maszyny Wirtualnej utworzone powyżej, wykonaj poniższe kroki hello.

1. Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **dynamiczne** toohello po prawej **przypisywania adresów IP**, następnie kliknij przycisk **zapisać**, a następnie Kliknij przycisk **tak**.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Jak tooadd statycznego prywatnego adresu IP adresów tooan istniejącej maszyny Wirtualnej
tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu powyższych kroków hello wykonaj poniższe kroki hello:

1. Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **statycznych** toohello prawo **przypisywania adresów IP**.
2. Typ *192.168.1.101* dla **adres IP**, następnie kliknij przycisk **zapisać**, a następnie kliknij przycisk **tak**.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.
* Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.
* Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).

