---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Tworzenie i modyfikowanie obwodu usługi ExpressRoute
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-circuit-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-circuit-classic.md)
>

W tym artykule opisano, jak toocreate obwodu Azure ExpressRoute przy użyciu hello Azure portal hello usługi Azure Resource Manager deployment modelu. Hello także następujące kroki opisano, jak toocheck hello stanu obwodu hello, zaktualizuj lub usuń i anulowanie zastrzeżenia go.


## <a name="before-you-begin"></a>Przed rozpoczęciem
* Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Upewnij się, że masz dostęp do toohello [portalu Azure](https://portal.azure.com).
* Upewnij się, że masz uprawnienia toocreate nowych zasobów sieciowych. Jeśli nie masz odpowiednich uprawnień hello, skontaktuj się z administratorem konta.
* Możesz [wyświetlanie wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) przed rozpoczęciem w kolejności toobetter zrozumieć kroki hello.

## <a name="create-and-provision-an-expressroute-circuit"></a>Tworzenie i przydzielanie obwodu usługi ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. Zaloguj się toohello portalu Azure
W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Utwórz nowy obwód usługi ExpressRoute
> [!IMPORTANT]
> Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute. Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.
> 
> 

1. Można utworzyć obwodu usługi ExpressRoute, wybierając hello opcja toocreate nowy zasób. Kliknij przycisk **nowy** > **sieci** > **ExpressRoute**, jak pokazano w powitania po obrazu:
   
    ![Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Po kliknięciu **ExpressRoute**, zobaczysz hello **obwodu ExpressRoute utworzyć** bloku. Po jest wypełnianie hello wartości w tym bloku, upewnij się, możesz określić hello prawidłowe jednostki SKU warstwy i pomiaru danych.
   
   * **Warstwa** Określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium. Można określić **standardowe** tooget hello standardowy SKU lub **Premium** dla hello premium dodatku.
   * **Pomiaru danych** Określa typ rozliczeń hello. Można określić **Metered** planu dane naliczane i **nieograniczone** planu nieograniczone danych. Zmiana typu rozliczeń hello z **Metered** za**nieograniczone**, ale nie można zmienić typu hello z **nieograniczone** za**Metered**.
     
     ![Skonfiguruj hello SKU warstwy i pomiaru danych](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Należy pamiętać, że hello lokalizacja komunikacji równorzędnej wskazuje hello [lokalizacji fizycznej](expressroute-locations.md) gdzie są komunikacji równorzędnej z firmą Microsoft. Jest to **nie** połączone za właściwość "Lokalizacja", która odwołuje się toohello lokalizacji geograficznej, gdzie znajduje się hello dostawcy zasobów sieciowych Azure. Gdy nie są powiązane, jest dobrym rozwiązaniem toochoose dostawcy zasobów sieciowych toohello geograficznie Zamknij lokalizacja komunikacji równorzędnej hello obwodu. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Widok hello obwody i właściwości
**Wyświetlanie wszystkich obwodów hello**

Można wyświetlić wszystkich obwodów hello, które zostały utworzone przez wybranie **wszystkie zasoby** w menu po lewej stronie powitania.

![Obwody widoku](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Wyświetl właściwości hello**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Wyświetl właściwości](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi
W tym bloku **stan dostawcy** zawiera informacje na temat hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello. **Stan obwodu** zawiera stan hello na powitania po stronie firmy Microsoft. Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.

Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:

Stan dostawcy: nie zainicjowano obsługę administracyjną<BR>
Stan obwodu: włączone

![Zainicjuj proces inicjowania obsługi administracyjnej](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

obwodu Hello ulegnie zmianie po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello:

Stan dostawcy: Inicjowanie obsługi administracyjnej<BR>
Stan obwodu: włączone

Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:

Stan dostawcy: zainicjowano obsługę administracyjną<BR>
Stan obwodu: włączone

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza
Można wyświetlić właściwości hello obwodu hello są zainteresowani przez zaznaczenie go. Sprawdź hello **stan dostawcy** i upewnij się, że została przeniesiona za**obsługiwane administracyjnie** przed kontynuowaniem.

![Stan obwodu i dostawcy](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Tworzenie konfiguracji routingu
Aby uzyskać instrukcje, zobacz toohello [obwodu ExpressRoute konfiguracji routingu](expressroute-howto-routing-portal-resource-manager.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.

> [!IMPORTANT]
> Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Link sieci wirtualnej tooan obwodu usługi expressroute
Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute. Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](expressroute-howto-linkvnet-arm.md) artykuł podczas pracy z modelu wdrażania usługi Resource Manager hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Pobieranie stanu hello obwodu usługi ExpressRoute
Stan hello obwód można wyświetlić, wybierając go. 

![Stan obwodu usługi ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modyfikowanie obwodu usługi ExpressRoute
Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.

Możesz zrobić hello po bez przestojów:

* Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.
* Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność. Należy pamiętać, że zmiany na starszą wersję hello przepustowości obwodu nie jest obsługiwany. 
* Zmień hello planu z danych naliczane tooUnlimited danych pomiaru. Należy pamiętać, zmiana planu zliczania hello z tooMetered nieograniczone danych, danych nie jest obsługiwane.
* Można włączyć lub wyłączyć *operacje klasycznego*.

Aby uzyskać więcej informacji na limity i ograniczenia, można znaleźć toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

toomodify obwodu usługi ExpressRoute, wybierz polecenie hello **konfiguracji** pokazane na poniższej ilustracji hello.

![Modyfikowanie obwodu](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Można zmodyfikować hello przepustowości, jednostka SKU, modelu rozliczeń i zezwolić klasycznego operacji w obrębie bloku konfiguracji hello.

> [!IMPORTANT]
> Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności. Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.
>
> Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń. Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.
> 
> Wyłączenie dodatku premium operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Anulowania obsługi i usuwania obwodu usługi ExpressRoute
Można usunąć obwodu usługi ExpressRoute, wybierając hello **usunąć** ikony. Należy uwzględnić następujące hello:

* Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute. Jeśli ta operacja nie powiedzie się, sprawdź, czy wszystkie sieci wirtualne są połączone toohello obwodu.
* Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok. Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.
* Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello. Spowoduje to zatrzymanie rozliczeń dla obwodu hello

## <a name="next-steps"></a>Następne kroki
Po utworzeniu obwodu, upewnij się, że hello następujące:

* [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)

