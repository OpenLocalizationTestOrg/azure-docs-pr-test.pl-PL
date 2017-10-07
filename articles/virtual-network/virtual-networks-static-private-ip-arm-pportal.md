---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Portalu Azure (klasyczne)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (klasyczny)](virtual-networks-static-private-ip-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure (klasyczne)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Poniższe kroki przykładowe Hello oczekiwać środowisku niezłożonym już utworzone. Jeśli kroki hello toorun wyświetlaną w tym dokumencie, należy najpierw utworzyć hello środowisko testowe opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Jak adresy toocreate Maszynę wirtualną do testowania statycznego prywatnego adresu IP
Nie można ustawić statycznego prywatnego adresu IP podczas tworzenia maszyny Wirtualnej w tryb wdrażania usługi Resource Manager hello hello przy użyciu hello portalu Azure. Należy najpierw utworzyć hello maszyny Wirtualnej, tehn ustaw jej prywatnego adresu IP toobe statycznych.

toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet*, wykonaj poniższe kroki hello.

1. W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **nowy** > **obliczeniowe** > **systemu Windows Server 2012 R2 Datacenter**, zwróć uwagę, że hello **wybierz model wdrożenia** listy już pokazuje **Resource Manager**, a następnie kliknij przycisk **Utwórz**, jak pokazano na poniższej ilustracji hello.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. W hello **podstawy** bloku, wprowadź nazwę hello hello toobe maszyny Wirtualnej utworzone (*DNS01* w naszym scenariuszu), hello konta administratora lokalnego i hasło, jak pokazano na poniższej ilustracji hello.
   
    ![Blok Podstawowe](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Upewnij się, że hello **lokalizacji** jest *środkowe stany USA*, następnie kliknij przycisk **wybierz istniejącą** w obszarze **grupy zasobów**, następnie kliknij przycisk **Grupy zasobów** ponownie, następnie kliknij przycisk *TestRG*, a następnie kliknij przycisk **OK**.
   
    ![Blok Podstawowe](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. W hello **wybierz rozmiar** bloku, wybierz opcję **A1 standardowe**, a następnie kliknij przycisk **wybierz**.
   
    ![Wybierz rozmiar bloku](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. W **ustawienia** bloku Utwórz hello się następujące właściwości są ustawiane są konfigurowane przy użyciu wartości hello poniżej, a następnie kliknij przycisk **OK**.
   
    -**Konto magazynu**: *vnetstorage*
   
   * **Sieci**: *TestVNet*
   * **Podsieci**: *frontonu*
     
     ![Wybierz rozmiar bloku](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. W hello **Podsumowanie** bloku, kliknij przycisk **OK**. Powiadomienie hello kafelka poniżej wyświetlane na pulpicie nawigacyjnym.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej
tooview hello statycznych prywatne informacje o adresie IP dla hello się, że maszyna wirtualna utworzona z powyższych kroków hello wykonaj poniższe kroki hello.

1. W portalu Azure, Azure hello, kliknij polecenie **PRZEGLĄDAJ wszystko** > **maszyn wirtualnych** > **DNS01** > **wszystkie ustawienia** > **interfejsy sieciowe** a następnie kliknij polecenie hello tylko interfejsu sieciowego na liście.
   
    ![Wdrażanie maszyny Wirtualnej kafelka](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. W hello **interfejsu sieciowego** bloku, kliknij przycisk **wszystkie ustawienia** > **adresów IP** i hello powiadomienia **przypisania** i **Adres IP** wartości.
   
    ![Wdrażanie maszyny Wirtualnej kafelka](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Jak tooadd statycznego prywatnego adresu IP adresów tooan istniejącej maszyny Wirtualnej
tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu powyższych kroków hello wykonaj poniższe kroki hello:

1. Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **statycznych** w obszarze **przypisania**.
2. Typ *192.168.1.101* dla **adres IP**, a następnie kliknij przycisk **zapisać**.
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Jeśli po kliknięciu przycisku **zapisać** można zauważyć, że przypisanie hello nadal jest ustawione zbyt**dynamiczne**, oznacza to, że wpisany adres IP hello jest już używana. Spróbuj innego adresu IP.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej
tooremove hello statycznego prywatnego adresu IP z powitalne maszyny Wirtualnej utworzone powyżej, wykonaj powitania po kroku:

Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **dynamiczne** w obszarze **przypisania**, a następnie kliknij przycisk **zapisać**.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.
* Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.
* Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).

