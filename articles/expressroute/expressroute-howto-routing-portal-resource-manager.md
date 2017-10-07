---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Menedżer zasobów: Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute

W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu hello portalu Azure. Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute. Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:


## <a name="configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji

* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie poleceń cmdlet hello stanie toorun toobe w kolejnych sekcjach hello.
* Jeśli planujesz toouse udostępnionego skrótu MD5/klucz można toouse się, że to po obu stronach hello tunelu i limit hello liczbę znaków tooa maksymalnie 25.

Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia konfiguruje i zarządza nimi routingu dla Ciebie. 

> [!IMPORTANT]
> Mamy obecnie nie anonsuje skonfigurowane przez dostawców usług za pośrednictwem portalu zarządzania usługami hello komunikacji równorzędnych. Pracujemy nad tym, by wkrótce włączyć tę funkcję. Skontaktuj się z dostawcą usług przed rozpoczęciem konfigurowania komunikacji równorzędnych protokołu BGP.
> 
> 

Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute. Możesz skonfigurować komunikację równorzędną w dowolnej kolejności. Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.

## <a name="azure-private-peering"></a>Prywatna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate Azure prywatnej komunikacji równorzędnej

1. Skonfiguruj hello obwodu ExpressRoute. Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem.

  ![Lista](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:

  * / 30 podsieci dla linku podstawowego hello. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * / 30 podsieci hello dodatkowej łącza. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS. Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej. Pamiętaj, aby nie używać numeru 65515.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.
3. Wybierz hello Azure prywatnej komunikacji równorzędnej wierszy, jak pokazano w hello poniższy przykład:

  ![Prywatne](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Skonfiguruj prywatną komunikację równorzędną. następujące obraz powitania przedstawiono przykład konfiguracji:

  ![Skonfiguruj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Zapisz konfigurację hello, po określeniu wszystkich parametrów. Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello poniższy przykład:

  ![Zapisz prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure prywatnej komunikacji równorzędnej szczegóły

Można wyświetlić właściwości hello prywatnej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.

![Wyświetl prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure

Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.

![Zaktualizuj prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete Azure prywatnej komunikacji równorzędnej

Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w powitania po obrazu:

![usunięcie prywatnej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Publiczna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate Azure publicznej komunikacji równorzędnej

1. Skonfiguruj obwód usługi ExpressRoute. Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem dalszych.

  ![Lista publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:

  * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4.
  * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.
3. Wybierz hello Azure publicznej komunikacji równorzędnej wierszy, jak pokazano w powitania po obrazu:

  ![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Skonfiguruj publiczną komunikację równorzędną. następujące obraz powitania przedstawiono przykład konfiguracji:

  ![Skonfiguruj publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Zapisz konfigurację hello, po określeniu wszystkich parametrów. Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello poniższy przykład:

  ![Zapisz publicznej komunikacji równorzędnej konfiguracji](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure publicznej komunikacji równorzędnej szczegóły

Można wyświetlić właściwości hello publicznej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.

![właściwości publicznej komunikacji równorzędnej widoku](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure publicznej konfiguracji komunikacji równorzędnej

Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.

![Wybierz publicznej komunikacji równorzędnej wiersza](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete Azure publicznej komunikacji równorzędnej

Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w hello poniższy przykład:

![Usuń publicznej komunikacji równorzędnej](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft

Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.

> [!IMPORTANT]
> Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy. Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu. Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate komunikacji równorzędnej firmy Microsoft

1. Skonfiguruj obwód usługi ExpressRoute. Upewnij się, że obwód hello jest w pełni zaaprowizowanym przez dostawcę łączności hello przed kontynuowaniem dalszych.

  ![Lista komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft. Upewnij się, że masz hello następujących informacji, aby kontynuować.

  * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
  * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
  * Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP. Akceptowane są tylko prefiksy publicznych adresów IP. Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listę rozdzielaną przecinkami. Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.
  * **Opcjonalne -** klienta ASN: w przypadku prefiksów reklamy, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer hello można określić jako numer toowhich są zarejestrowani.
  * Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.
3. Możesz wybrać hello równorzędna ma tooconfigure, jak pokazano w hello następujące przykładowe. Wybierz wiersz komunikacji równorzędnej firmy Microsoft hello.

  ![Wybierz wiersz komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Skonfiguruj komunikację równorzędną firmy Microsoft. następujące obraz powitania przedstawiono przykład konfiguracji:

  ![Konfigurowanie komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Zapisz konfigurację hello, po określeniu wszystkich parametrów.

  Jeśli obwodu pobiera tooa potrzebne weryfikacji stanu (jak pokazano w obrazie hello), należy otworzyć tooshow biletu pomocy technicznej dowód własności hello prefiksy tooour z pomocą techniczną.

  ![Zapisywanie konfiguracji komunikacji równorzędnej firmy Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Jak pokazano w hello poniższy przykład, można otworzyć bilet pomocy technicznej bezpośrednio z portalu hello:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Po zaakceptowaniu pomyślnie hello konfiguracji, zostanie wyświetlony coś podobnego toohello po obrazu:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>Szczegóły komunikacji równorzędnej tooview firmy Microsoft

Można wyświetlić właściwości hello publicznej komunikacji równorzędnej platformy Azure, wybierając hello komunikacji równorzędnej.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft

Możesz wybrać hello wiersza dla komunikacji równorzędnej i modyfikowanie właściwości komunikacji równorzędnej hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete komunikacji równorzędnej firmy Microsoft

Można usunąć konfiguracji komunikacji równorzędnej, wybierając ikonę Usuń hello, jak pokazano w powitania po obrazu:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Następne kroki

Następny krok [połączyć sieć wirtualną tooan obwodu usługi expressroute](expressroute-howto-linkvnet-portal-resource-manager.md)
* Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).
* Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).
* Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).
