---
title: "Dodawanie wielu połączeń lokacja-lokacja bramy sieci VPN do sieci wirtualnej: Azure Portal: Resource Manager | Dokumentacja firmy Microsoft"
description: "Dodawaj połączeń S2S obejmujący wiele lokacji do bramy sieci VPN, który ma istniejącego połączenia"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: 7ec57789ee76f4ec54e4f7b68ea75c19522f3d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a>Dodaj połączenie lokacja-lokacja z sieci wirtualnej z istniejącego połączenia bramy sieci VPN

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klasyczny)](vpn-gateway-multi-site.md)
>
> 

Ten artykuł przeprowadzi Cię przez dodawanie połączeń lokacja-lokacja (S2S) do bramy sieci VPN, który ma istniejącego połączenia przy użyciu portalu Azure. Połączenia tego typu jest często określany jako "obejmujący wiele lokacji" konfiguracji. Można dodać połączenia S2S na sieć wirtualną, która ma już połączenia S2S, połączenie punkt-lokacja lub połączenia do wirtualnymi. Podczas dodawania połączenia istnieją pewne ograniczenia. Sprawdź [przed rozpoczęciem](#before) w tym artykule, aby sprawdzić przed rozpoczęciem konfiguracji. 

Ten artykuł dotyczy sieci wirtualnych utworzonych przy użyciu modelu wdrażania usługi Resource Manager mające bramy sieci RouteBased VPN. Te kroki nie dotyczą konfiguracji połączenia ważnych ExpressRoute/lokacja-lokacja. Zobacz [ważnych połączeń ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) informacji o ważnych połączenia.

### <a name="deployment-models-and-methods"></a>Modele i metody wdrażania
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji. Po udostępnieniu artykułu możemy link bezpośrednio do niego z tej tabeli.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Przed rozpoczęciem
Sprawdź następujące elementy:

* Połączenie ExpressRoute/S2S coexisting nie są tworzone.
* Masz sieci wirtualnej, który został utworzony przy użyciu modelu wdrażania usługi Resource Manager z istniejącym połączeniem.
* Brama sieci wirtualnej sieci wirtualnej jest RouteBased. Jeśli masz bramy sieci PolicyBased VPN, należy usunąć bramę sieci wirtualnej i Utwórz nową bramę sieci VPN jako RouteBased.
* Żaden z zakresów adresów nakładać się na każdej sieci wirtualnych, które ta sieć wirtualna nawiązuje połączenie z.
* Masz zgodne urządzenie sieci VPN i osoby, która jest w stanie go skonfigurować. Zobacz artykuł [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Urządzenia sieci VPN — informacje). Jeśli nie dysponujesz wiedzą niezbędną do skonfigurowania urządzenia sieci VPN lub nie znasz zakresu adresów IP ujętego w konfiguracji sieci lokalnej, skontaktuj się z osobą, która może podać Ci te dane.
* Masz zewnętrznie połączonej publiczny adres IP urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.

## <a name="part1"></a>Część 1 — Konfigurowanie połączenia
1. W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **wszystkie zasoby** i Znajdź Twojej **bramy sieci wirtualnej** z listy zasobów i kliknij ją.
3. Na **Brama sieci wirtualnej** bloku, kliknij przycisk **połączenia**.
   
    ![Blok połączeń](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")<br>
4. Na **połączeń** bloku, kliknij przycisk **+ Dodaj**.
   
    ![Dodawanie przycisku połączenia](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")<br>
5. Na **Dodaj połączenie** bloku, wypełnij następujące pola:
   
   * **Nazwa:** nazwy, którego chcesz przypisać do lokacji, które tworzysz połączenie.
   * **Typ połączenia:** wybierz **lokacja lokacja (IPsec)**.
     
     ![Dodawanie bloku połączenia](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")<br>

## <a name="part2"></a>Część 2 — Dodaj bramę sieci lokalnej
1. Kliknij przycisk **bramy sieci lokalnej** ***wybierz bramę sieci lokalnej***. Spowoduje to otwarcie **wybierz bramę sieci lokalnej** bloku.
   
    ![Wybierz bramę sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")<br>
2. Kliknij przycisk **Utwórz nowy** otworzyć **Utwórz bramę sieci lokalnej** bloku.
   
    ![Tworzenie bloku bramy sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")<br>
3. Na **Utwórz bramę sieci lokalnej** bloku, wypełnij następujące pola:
   
   * **Nazwa:** nazwa ma zostać przypisany do zasobu bramy sieci lokalnej.
   * **Adres IP:** publiczny adres IP urządzenia sieci VPN w witrynie, w której chcesz nawiązać połączenie.
   * **Przestrzeń adresowa:** przestrzeni adresowej, który ma być kierowane do nowej lokacji sieci lokalnej.
4. Kliknij przycisk **OK** na **Utwórz bramę sieci lokalnej** bloku, aby zapisać zmiany.

## <a name="part3"></a>Część 3 — Dodaj klucz udostępniony oraz utworzyć połączenie
1. Na **Dodaj połączenie** bloku, Dodaj klucz udostępniony, który ma być używany do utworzenia połączenia. Można pobrać klucza wspólnego z urządzenia sieci VPN, lub wprowadź tutaj a następnie skonfiguruj urządzenia sieci VPN w celu używania klucza współużytkowanego. Ważne jest, że klucze są dokładnie takie same.
   
    ![Klucz współużytkowany](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")<br>
2. W dolnej części bloku, kliknij przycisk **OK** do utworzenia połączenia.

## <a name="part4"></a>Część 4 - Sprawdź, czy połączenie sieci VPN


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Następne kroki

Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne. Więcej informacji zawiera [ścieżka szkoleniowa](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) dotycząca maszyn wirtualnych.
