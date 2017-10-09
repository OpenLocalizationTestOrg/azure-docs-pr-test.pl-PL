---
title: 'Link sieci wirtualnej tooan obwodu ExpressRoute: portalu Azure | Dokumentacja firmy Microsoft'
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Połączenie wirtualnej sieci tooan obwodu usługi expressroute
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-linkvnet-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-linkvnet-classic.md)
> 

Ten artykuł ułatwia łączenie obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i hello portalu Azure. Sieci wirtualne mogą być w hello tej samej subskrypcji lub może być częścią innej subskrypcji.

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute.
  
  * Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i mieć obwodu hello włączane przez dostawcą połączenia.
  * Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu. Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-portal-resource-manager.md) artykułu instrukcje routingu.
  * Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.
  * Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym. Wykonaj instrukcje hello zbyt[Tworzenie bramy sieci wirtualnej dla usługi ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Brama sieci wirtualnej dla usługi ExpressRoute używa hello elementu GatewayType "ExpressRoute", nie sieci VPN.

* Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute. Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute. 
* Możesz połączyć sieć wirtualną poza region geograficznymi hello hello obwodu ExpressRoute lub połączenia z większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute, jeśli włączono hello dodatek usługi ExpressRoute w warstwie premium. Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.
* Możesz [wyświetlanie wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) przed początek toobetter zrozumieć kroki hello.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu

### <a name="toocreate-a-connection"></a>toocreate połączenia

> [!NOTE]
> Informacje o konfiguracji protokołu BGP, nie pojawiają się jeśli dostawca warstwy 3 hello skonfigurowany z komunikacji równorzędnych. Jeśli obwodu jest w stanie elastycznie, należy toocreate stanie połączenia.
>

1. Upewnij się, że obwód usługi expressroute i Azure prywatnej komunikacji równorzędnej skonfigurowano pomyślnie. Postępuj zgodnie z instrukcjami hello [utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i [Konfigurowanie routingu](expressroute-howto-routing-arm.md). Obwodu ExpressRoute powinna wyglądać powitania po obrazu:

    ![Zrzut ekranu obwodu usługi ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Można teraz rozpocząć Inicjowanie obsługi administracyjnej toolink połączenie Twojej sieci wirtualnej bramy tooyour obwodu usługi expressroute. Kliknij przycisk **połączenia** > **Dodaj** tooopen hello **Dodaj połączenie** bloku, a następnie skonfiguruj hello wartości.

    ![Dodaj połączenie zrzut ekranu](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Po pomyślnym skonfigurowaniu połączenia obiekt połączenia są wyświetlane informacje hello hello połączenia.

     ![Zrzut ekranu obiektu połączenia](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete połączenia
Połączenie można usunąć, wybierając hello **usunąć** ikonę na powitania bloku dla połączenia.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji
Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami. Hello na poniższym rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji.
- Każdego z działów hello w obrębie organizacji hello można używać własnej subskrypcji do wdrażania usług, ale mogą współużytkować jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci.
- Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute. Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.

    > [!NOTE]
    > Połączeniami i przepustowością opłat za obwód dedykowany hello będzie właściciela obwodu ExpressRoute toohello zastosowane. Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Administrowanie — obwodu właścicieli i użytkowników obwodu

"właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute. właściciela obwodu Hello można utworzyć autoryzacje, które można wykorzystać przez "obwód użytkowników". Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute. Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).

właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie. Odwoływanie powoduje autoryzacji wszystkich połączeń usuwany z subskrypcji hello, do których dostęp został odwołany.

### <a name="circuit-owner-operations"></a>Operacje właściciela obwodu

**toocreate autoryzacji połączenia**

Właściciel obwodu Hello tworzy autoryzacji. Spowoduje to utworzenie hello klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute. Autoryzacji dotyczy tylko jedno połączenie.

1. W bloku ExpressRoute powitania kliknij **autoryzacje** , a następnie wpisz **nazwa** hello autoryzacji, a następnie kliknij przycisk **zapisać**.

    ![Zezwolenia](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Po zapisaniu konfiguracji hello skopiować hello **identyfikator zasobu** i hello **klucza autoryzacji**.

    ![Klucz autoryzacji](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete autoryzacji połączenia**

Połączenie można usunąć, wybierając hello **usunąć** ikonę na powitania bloku dla połączenia.

### <a name="circuit-user-operations"></a>Operacje użytkownik obwodu

Użytkownik obwodu Hello musi hello zasobów identyfikator i klucz autoryzacji z hello właściciela obwodu. 

**tooredeem autoryzacji połączenia**

1.  Kliknij przycisk hello **+ nowy** przycisku.

    ![Kliknij przycisk Nowy](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Wyszukaj **"Połączenia"** w hello Marketplace, zaznacz go, a następnie kliknij przycisk **Utwórz**.

    ![Wyszukiwanie połączenia](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Upewnij się, że hello **typ połączenia** ustawiono zbyt "ExpressRoute".


4.  Wypełnij hello szczegółowe informacje, a następnie kliknij przycisk **OK** w bloku podstawy hello.

    ![Blok Podstawowe](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  W hello **ustawienia** bloku, wybierz hello **Brama sieci wirtualnej** i sprawdź hello **zrealizować autoryzacji** pole wyboru.

6.  Wprowadź hello **klucza autoryzacji** i hello **elementu równorzędnego obwodu URI** i nadaj nazwę hello połączenia. Kliknij przycisk **OK**.

    ![Blok Ustawienia](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Przejrzyj informacje hello w hello **Podsumowanie** bloku i kliknij przycisk **OK**.


**toorelease autoryzacji połączenia**

Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
