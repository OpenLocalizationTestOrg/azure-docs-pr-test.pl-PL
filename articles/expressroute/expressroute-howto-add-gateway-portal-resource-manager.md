---
title: "Dodawanie sieci wirtualnej tooa bramy sieci wirtualnej dla usługi ExpressRoute: Portal: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł przeprowadzi Cię przez procedurę dodawania tooan bramy sieci wirtualnej, już utworzona sieć wirtualna Menedżera zasobów dla usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>W przypadku połączeń ExpressRoute przy użyciu portalu Azure hello należy skonfigurować bramę sieci wirtualnej
> [!div class="op_single_selector"]
> * [Resource Manager — witryna Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager — program PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic — PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

W tym artykule przedstawiono hello kroki tooadd bramy sieci wirtualnej istniejące sieci wirtualnej. W tym artykule przedstawiono tooadd kroki hello, zmienianie rozmiaru i usunąć bramę sieci wirtualnej (VNet) dla istniejącej sieci wirtualnej. Witaj czynności dla tej konfiguracji są przeznaczone dla sieci wirtualnych, które zostały utworzone przy użyciu modelu wdrażania usługi Resource Manager hello, który będzie używany w konfiguracji usługi ExpressRoute. Aby uzyskać więcej informacji na temat bram sieci wirtualnej i ustawień konfiguracji bramy ExpressRoute, zobacz [temat bram sieci wirtualnej dla usługi ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Przed rozpoczęciem

kroki Hello do tego celu zadań sieci wirtualnej na podstawie hello wartości w powitania po konfiguracji na liście odwołania. W naszym przykładzie kroki możemy Użyj tej listy. Skopiuj toouse listy hello jako odwołanie, zastępując wartości hello własne.

**Lista odwołań konfiguracji**

* Nazwa sieci wirtualnej = "TestVNet"
* Przestrzeń adresową sieci wirtualnej = 192.168.0.0/16
* Nazwa podsieci = "FrontEnd" 
    * Przestrzeń adresów podsieci = "192.168.1.0/24"
* Grupa zasobów = "TestRG"
* Lokalizacja = "Wschodnie stany USA"
* Nazwa podsieci bramy: "GatewaySubnet" zawsze nazwę podsieci bramy *GatewaySubnet*.
    * Przestrzeń adresów podsieci bramy = "192.168.200.0/26"
* Nazwa bramy = "ERGW"
* Nazwa IP bramy = "MyERGWVIP"
* Typ bramy = "ExpressRoute" tego typu jest wymagany dla konfiguracji usługi ExpressRoute.
* Nazwa publicznego adresu IP bramy = "MyERGWVIP"

Możesz wyświetlić [wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) te kroki przed rozpoczęciem konfiguracji.

## <a name="create-hello-gateway-subnet"></a>Utwórz podsieć bramy hello

1. W hello [portal](http://portal.azure.com), przejdź do Menedżera zasobów sieci wirtualnej toohello, dla której ma zostać toocreate bramy sieci wirtualnej.
2. W hello **ustawienia** sekcji z bloku sieci wirtualnej, kliknij przycisk **podsieci** tooexpand hello podsieci blok podsieci.
3. Na powitania **podsieci** bloku, kliknij przycisk **+ podsieci bramy** tooopen hello **Dodaj podsieć** bloku. 
   
    ![Dodaj podsieć bramy hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Dodaj podsieć bramy hello")


4. Witaj **nazwa** dla podsieci jest automatycznie wypełniane hello wartość "GatewaySubnet". Ta wartość jest wymagana w kolejności dla podsieci hello Azure toorecognize jako hello podsieci bramy. Dostosuj hello automatycznie wypełnianej **zakres adresów** wartości toomatch wymagań dotyczących konfiguracji. Zaleca się utworzenie podsieci bramy z /27 lub większy (/ 26, / 25, itp.). Następnie kliknij przycisk **OK** toosave hello wartości i utworzyć hello podsieci bramy.

    ![Dodawanie podsieci hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Dodawanie hello podsieci")

## <a name="create-hello-virtual-network-gateway"></a>Utwórz bramę sieci wirtualnej hello

1. W portalu powitania po lewej stronie powitania kliknij  **+**  i wpisz "Brama sieci wirtualnej" w wyszukiwaniu. Zlokalizuj **Brama sieci wirtualnej** wyszukiwania hello wróć i kliknij pozycję hello. Na powitania **Brama sieci wirtualnej** bloku, kliknij przycisk **Utwórz** u dołu hello hello bloku. Spowoduje to otwarcie hello **Utwórz bramę sieci wirtualnej** bloku.
2. Na powitania **Utwórz bramę sieci wirtualnej** bloku, wypełnij hello wartości dla bramy sieci wirtualnej.

    ![Pola bloku Tworzenie bramy sieci wirtualnej](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Pola bloku Tworzenie bramy sieci wirtualnej")
3. **Nazwa**: Nadaj nazwę bramie. To jest nie hello taki sam jak nazewnictwa podsieci bramy. Jego imię i nazwisko hello hello bramy obiektu, którego jest tworzony.
4. **Typ bramy**: Wybierz **ExpressRoute**.
5. **Jednostka SKU**: jednostka SKU bramy hello wybierz z listy rozwijanej hello.
6. **Lokalizacja**: Dopasuj hello **lokalizacji** pola toopoint toohello lokalizacji, gdzie znajduje się sieci wirtualnej. Jeśli lokalizacja hello nie wskazuje region toohello, gdzie znajduje się sieci wirtualnej, hello sieci wirtualnej nie jest wyświetlane w listy rozwijanej "Wybierz sieć wirtualną" hello.
7. Wybierz hello toowhich sieci wirtualnej ma tooadd tej bramy. Kliknij przycisk **sieci wirtualnej** tooopen hello **wybierz sieć wirtualną** bloku. Wybierz hello sieci wirtualnej. Jeśli nie widzisz sieci wirtualnej, upewnij się, że hello **lokalizacji** pola wskazuje toohello regionu, w którym znajduje się sieci wirtualnej.
9. Wybierz publiczny adres IP. Kliknij przycisk **publicznego adresu IP** tooopen hello **wybierz publiczny adres IP** bloku. Kliknij przycisk **+ Utwórz nowe** tooopen hello **Utwórz blok publiczny adres IP**. Wprowadź nazwę dla publicznego adresu IP. Ten blok tworzy publiczny toowhich do obiektu adres IP, który publicznego adresu IP będą przypisywane dynamicznie. Kliknij przycisk **OK** toosave Twojego bloku toothis zmiany.
10. **Subskrypcja**: Sprawdź, że hello poprawne wybrać subskrypcję.
11. **Grupa zasobów**: to ustawienie jest określane przez hello wybranej sieci wirtualnej.
12. Nie dopasowuj hello **lokalizacji** po określeniu hello poprzednie ustawienia.
13. Sprawdź ustawienia hello. Jeśli chcesz, aby Twoje tooappear bramy na pulpicie nawigacyjnym hello, możesz wybrać **toodashboard numeru Pin** u dołu hello hello bloku.
14. Kliknij przycisk **Utwórz** toobegin tworzenie hello bramy. są weryfikowane Hello ustawień i wdraża hello bramy. Tworzenie bramy sieci wirtualnej może potrwać too45 toocomplete minut.

## <a name="next-steps"></a>Następne kroki
Po utworzeniu bramy sieci wirtualnej hello możesz połączyć tooan Twojej sieci wirtualnej obwodu usługi expressroute. Zobacz [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md).
