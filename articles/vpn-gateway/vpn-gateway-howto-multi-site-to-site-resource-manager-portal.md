---
title: "Dodawanie wielu sieci VPN bramy lokacja-lokacja połączeń tooa sieci wirtualnej: Azure Portal: Resource Manager | Dokumentacja firmy Microsoft"
description: "Dodaj obejmujący wiele lokacji S2S połączeń tooa bramy sieci VPN z istniejącego połączenia"
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
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Dodaj tooa połączenia lokacja-lokacja sieci wirtualnej z istniejącego połączenia bramy sieci VPN

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klasyczny)](vpn-gateway-multi-site.md)
>
> 

W tym artykule przedstawiono przy użyciu hello tooadd portalu Azure do lokacji (S2S) połączeń tooa bramy sieci VPN z istniejącego połączenia. Ten typ połączenia jest często tooas określonej konfiguracji "obejmujący wiele lokacji". Możesz dodać tooa połączenia S2S sieć wirtualną, która ma już połączenia S2S, połączenie punkt-lokacja lub połączenia do wirtualnymi. Podczas dodawania połączenia istnieją pewne ograniczenia. Sprawdź hello [przed rozpoczęciem](#before) części tego artykułu tooverify, przed rozpoczęciem konfiguracji. 

Ten artykuł dotyczy tooVNets utworzone przy użyciu modelu wdrażania usługi Resource Manager hello mające bramy sieci RouteBased VPN. Te kroki należy stosować konfiguracje połączenia ważnych tooExpressRoute/lokacja-lokacja. Zobacz [ważnych połączeń ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) informacji o ważnych połączenia.

### <a name="deployment-models-and-methods"></a>Modele i metody wdrażania
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji. Artykuł jest dostępny, możemy połączyć bezpośrednio tooit z tej tabeli.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Przed rozpoczęciem
Sprawdź hello następujące elementy:

* Połączenie ExpressRoute/S2S coexisting nie są tworzone.
* Masz sieci wirtualnej, który został utworzony przy użyciu modelu wdrażania usługi Resource Manager hello z istniejącego połączenia.
* Brama sieci wirtualnej Hello sieci wirtualnej jest RouteBased. Jeśli masz bramy sieci PolicyBased VPN, należy usunąć hello bramy sieci wirtualnej i Utwórz nową bramę sieci VPN jako RouteBased.
* Nie zakresów adresów hello zachodzą na jakichkolwiek hello sieci wirtualnych, które ta sieć wirtualna nawiązuje połączenie z.
* Masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go. Zobacz artykuł [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Urządzenia sieci VPN — informacje). Jeśli nie znasz skonfigurowanie urządzenia sieci VPN lub masz doświadczenia w pracy z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która może zawiera te informacje dla Ciebie.
* Masz zewnętrznie połączonej publiczny adres IP urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.

## <a name="part1"></a>Część 1 — Konfigurowanie połączenia
1. W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **wszystkie zasoby** i Znajdź Twojej **bramy sieci wirtualnej** z listy hello zasobów i kliknij ją.
3. Na powitania **Brama sieci wirtualnej** bloku, kliknij przycisk **połączenia**.
   
    ![Blok połączeń](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Blok połączeń")<br>
4. Na powitania **połączeń** bloku, kliknij przycisk **+ Dodaj**.
   
    ![Przycisk Dodaj połączenie](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "przycisku Dodaj połączenie")<br>
5. Na powitania **Dodaj połączenie** bloku, wypełnij hello następujące pola:
   
   * **Nazwa:** hello nazwę lokacji toohello toogive tworzysz hello połączenie.
   * **Typ połączenia:** wybierz **lokacja lokacja (IPsec)**.
     
     ![Dodaj połączenie bloku](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Dodaj połączenie bloku")<br>

## <a name="part2"></a>Część 2 — Dodaj bramę sieci lokalnej
1. Kliknij przycisk **bramy sieci lokalnej** ***wybierz bramę sieci lokalnej***. Spowoduje to otwarcie hello **wybierz bramę sieci lokalnej** bloku.
   
    ![Wybierz bramę sieci lokalnej](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "wybierz bramę sieci lokalnej")<br>
2. Kliknij przycisk **Utwórz nowy** tooopen hello **Utwórz bramę sieci lokalnej** bloku.
   
    ![Bloku bramy sieci lokalnej Utwórz](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Utwórz bramę sieci lokalnej")<br>
3. Na powitania **Utwórz bramę sieci lokalnej** bloku, wypełnij hello następujące pola:
   
   * **Nazwa:** hello nazwę zasobu bramy sieci lokalnej toohello toogive.
   * **Adres IP:** hello hello urządzenia sieci VPN w witrynie hello, który ma tooconnect do publicznego adresu IP.
   * **Przestrzeń adresowa:** hello przestrzeń adresów, które mają toobe kierowane toohello nowej lokacji sieci lokalnej.
4. Kliknij przycisk **OK** na powitania **Utwórz bramę sieci lokalnej** zmiany hello toosave bloku.

## <a name="part3"></a>Część 3 — Dodaj klucz udostępniony hello oraz tworzenie połączenia hello
1. Na powitania **Dodaj połączenie** bloku, Dodaj klucz udostępniony hello mają toouse toocreate połączenia. Można albo Pobierz klucz udostępniony hello z urządzenia sieci VPN lub wprowadzić tutaj, a następnie skonfiguruj hello toouse urządzenia sieci VPN sam wspólny klucz. ważne jest operacją hello klucze są dokładnie Hello hello takie same.
   
    ![Klucz współużytkowany](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Klucz współużytkowany")<br>
2. U dołu hello hello bloku, kliknij przycisk **OK** toocreate hello połączenia.

## <a name="part4"></a>Część 4 - Sprawdź, czy hello połączenia sieci VPN


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Następne kroki

Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Zobacz maszyn wirtualnych hello [ścieżkę szkoleniową](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) Aby uzyskać więcej informacji.
