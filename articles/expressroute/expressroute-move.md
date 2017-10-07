---
title: "obwody usługi ExpressRoute aaaMoving z klasycznym tooResource Menedżera | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie potrzebnych tooknow o mostkowanie hello klasycznego i modeli wdrażania, hello Menedżera zasobów."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>Przenoszenie obwody usługi ExpressRoute z hello toohello klasycznego modelu wdrażania usługi Resource Manager
Ten artykuł zawiera omówienie to toomove obwodu Azure ExpressRoute z hello toohello klasycznego modelu wdrażania usługi Azure Resource Manager.

Można użyć jednego ExpressRoute obwodu tooconnect toovirtual sieci, które są wdrożone zarówno w klasycznym hello i modeli wdrażania usługi Resource Manager hello. Obwodu usługi ExpressRoute, niezależnie od tego, jak został utworzony, można teraz połączyć sieci toovirtual w obu modelach wdrażania.

![Obwodu usługi ExpressRoute, który stanowi łącze sieci toovirtual w obu modelach wdrażania](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Obwody usługi ExpressRoute, które są tworzone w hello klasycznego modelu wdrażania
Obwody usługi ExpressRoute, które są tworzone w hello klasycznego modelu wdrażania należy toobe przenieść toohello Menedżera zasobów wdrażania modelu pierwszy tooenable łączności tooboth hello classic i hello Resource Manager modele wdrażania. W przypadku przenoszenia połączenia łączność nie zostaje utracona ani zakłócona. Wszystkich łączy sieciowych obwodu to-virtual w hello klasycznego modelu wdrażania (poziomu hello sam subskrypcji i między subskrypcjami) zostaną zachowane.

Po przeniesienie hello jest ukończone pomyślnie, hello obwodu ExpressRoute wyszukuje, wykonuje i dokładnie wydaje się wymagać obwodu usługi ExpressRoute, który został utworzony w modelu wdrażania usługi Resource Manager hello. Można teraz utworzyć połączenia toovirtual sieci w modelu wdrażania usługi Resource Manager hello.

Po obwodu usługi ExpressRoute modelu wdrażania usługi Resource Manager toohello przeniesiony, można zarządzać cyklu życia hello hello obwodu ExpressRoute tylko przy użyciu modelu wdrażania usługi Resource Manager hello. Oznacza to, czy można wykonać operacje, takie jak dodawanie/aktualizowania/usuwania komunikacji równorzędnych aktualizowania właściwości obwodu (na przykład przepustowość, jednostki SKU i rozliczeń typ) i usuwania obwodów tylko w modelu wdrażania usługi Resource Manager hello. Zobacz poniższą sekcję toohello w instalacjach, które są tworzone w modelu wdrażania usługi Resource Manager hello więcej szczegółowych informacji dotyczących sposobu zarządzania modelami wdrażania tooboth dostępu.

Nie masz tooinvolve przenieść Twojej hello tooperform dostawcy łączności.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Obwody usługi ExpressRoute, które są tworzone w modelu wdrażania usługi Resource Manager hello
Można włączyć obwody usługi ExpressRoute, które są tworzone w toobe modelu wdrażania usługi Resource Manager hello dostępny z obu modeli wdrażania. Wszelkie obwodu usługi expressroute w ramach subskrypcji może być włączone toobe dostępny z obu modeli wdrażania.

* Obwody usługi ExpressRoute, które zostały utworzone w modelu wdrażania usługi Resource Manager hello nie mają domyślnie dostęp toohello klasycznego modelu wdrażania.
* Obwody usługi ExpressRoute, które zostały przeniesione z modelu wdrażania Menedżera zasobów toohello hello wdrażania klasycznego modelu jest dostępny z obu modeli wdrażania, domyślnie.
* Obwodu usługi ExpressRoute ma zawsze dostęp toohello modelu wdrażania Resource Manager, niezależnie od tego, czy został utworzony w hello Resource Manager lub w klasycznym modelu wdrażania. Oznacza to, które można utworzyć połączenia sieci toovirtual utworzone w hello modelu wdrażania usługi Resource Manager przez następujące instrukcje na [jak sieci wirtualnych toolink](expressroute-howto-linkvnet-arm.md).
* Dostęp toohello klasycznego modelu wdrażania jest kontrolowany przez hello **allowClassicOperations** parametru w hello obwodu usługi expressroute.

> [!IMPORTANT]
> Wszystkie przydziałów, które są opisane w hello [usługi limity](../azure-subscription-service-limits.md) zastosować strony. Na przykład standardowe obwodu może mieć maksymalnie 10 sieci wirtualnej łącza/połączeń na powitania klasycznego i w modelach wdrażania usługi Resource Manager hello.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Kontrolowanie dostępu toohello klasycznego modelu wdrażania
Można włączyć pojedynczego ExpressRoute obwodu toolink toovirtual sieci w obu modelach wdrażania przez ustawienie hello **allowClassicOperations** parametru hello obwodu usługi expressroute.

Ustawienie **allowClassicOperations** tooTRUE umożliwia toolink sieci wirtualne od obu toohello modeli wdrażania obwodu usługi expressroute. Możesz połączyć sieci toovirtual w hello klasycznego modelu wdrażania przez następujące wskazówki na [jak toolink sieci wirtualne w hello klasycznego modelu wdrażania](expressroute-howto-linkvnet-classic.md). Możesz połączyć sieci toovirtual w modelu wdrażania usługi Resource Manager hello według poniższych wskazówek na [jak toolink sieci wirtualne w hello modelu wdrażania usługi Resource Manager](expressroute-howto-linkvnet-arm.md).

Ustawienie **allowClassicOperations** tooFALSE zablokuje dostęp obwodu toohello z hello klasycznego modelu wdrażania. Jednak wszystkie linki sieci wirtualnej w hello klasycznego modelu wdrażania są zachowywane. W takim przypadku hello obwodu usługi expressroute nie jest widoczne w hello klasycznego modelu wdrażania.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Obsługiwane operacje w hello klasycznego modelu wdrażania
następujące operacje klasycznego Hello są obsługiwane w ExpressRoute circuit kiedy **allowClassicOperations** ustawiono tooTRUE:

* Uzyskanie informacji na temat obwodu usługi ExpressRoute
* Sieć wirtualna tworzenia/aktualizacji/get/usuwania łączy tooclassic sieci wirtualnych
* Tworzenie/aktualizowanie/pobieranie/usuwanie autoryzacji linków sieci wirtualnej względem łączności obejmującej wiele subskrypcji

Nie można wykonać następujące operacje klasycznego hello podczas **allowClassicOperations** ustawiono tooTRUE:

* Tworzenie/aktualizowanie/pobieranie/usuwanie komunikacji równorzędnej protokołu BGP dla komunikacji równorzędnej prywatnej i publicznej Azure oraz Microsoft
* Usuwanie obwodów usługi ExpressRoute

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Komunikacja między hello klasycznego i modeli wdrażania usługi Resource Manager hello
Witaj obwodu ExpressRoute działa jak mostka między hello klasycznego i modeli wdrażania usługi Resource Manager hello. Ruch między jak w sieciach wirtualnych w hello klasycznego modelu wdrażania i te w sieciach wirtualnych hello Resource Manager deployment modelu przepływów za pośrednictwem usługi ExpressRoute, jeśli obie sieci wirtualne są połączone toohello tego samego obwodu usługi expressroute.

Łącznej przepływności jest ograniczone przez pojemność przepływności hello hello bramy sieci wirtualnej. Ruch nie wprowadzać w takich przypadkach hello łączności dostawcy sieci lub sieci. Przepływ ruchu między sieciami wirtualnymi hello pełni znajduje się w sieci firmy Microsoft hello.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Publiczna tooAzure dostępu i zasoby komunikacji równorzędnej firmy Microsoft
Można kontynuować tooaccess zasobów, które są zazwyczaj dostępne za pośrednictwem usługi Azure publicznej komunikacji równorzędnej i komunikacji równorzędnej firmy Microsoft bez zakłóceń.  

## <a name="whats-supported"></a>Jakie operacje są obsługiwane
W tej sekcji opisano, jakie operacje są obsługiwane dla obwodów usługi ExpressRoute:

* Można użyć jednego ExpressRoute obwodu tooaccess sieci wirtualne, które są wdrażane w klasycznym hello i modeli wdrażania usługi Resource Manager hello.
* Można przenieść obwodu usługi ExpressRoute z hello toohello klasycznego modelu wdrażania usługi Resource Manager. Po przeniesieniu, hello obwodu ExpressRoute wygląda tak i działa jak inne utworzone w modelu wdrażania usługi Resource Manager hello obwodu ExpressRoute.
* Można przenieść tylko hello obwodu ExpressRoute. Za pomocą tej operacji nie można przenieść linków obwodu, sieci wirtualnych ani bram sieci VPN.
* Po obwodu usługi ExpressRoute modelu wdrażania usługi Resource Manager toohello przeniesiony, można zarządzać cyklu życia hello hello obwodu ExpressRoute tylko przy użyciu modelu wdrażania usługi Resource Manager hello. Oznacza to, czy można wykonać operacje, takie jak dodawanie/aktualizowania/usuwania komunikacji równorzędnych aktualizowania właściwości obwodu (na przykład przepustowość, jednostki SKU i rozliczeń typ) i usuwania obwodów tylko w modelu wdrażania usługi Resource Manager hello.
* Witaj obwodu ExpressRoute działa jak mostka między hello klasycznego i modeli wdrażania usługi Resource Manager hello. Ruch między jak w sieciach wirtualnych w hello klasycznego modelu wdrażania i te w sieciach wirtualnych hello Resource Manager deployment modelu przepływów za pośrednictwem usługi ExpressRoute, jeśli obie sieci wirtualne są połączone toohello tego samego obwodu usługi expressroute.
* Łącznością między subskrypcjami jest obsługiwane w klasycznym hello i modeli wdrażania usługi Resource Manager hello.
* Po przeniesieniu obwodu usługi ExpressRoute z modelu usługi Azure Resource Manager toohello modelu klasycznego hello można [migracji hello sieci wirtualnych połączonych toohello obwodu ExpressRoute](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Jakie operacje nie są obsługiwane
W tej sekcji opisano, jakie operacje nie są obsługiwane dla obwodów usługi ExpressRoute:

* Zarządzanie cyklem życia hello obwodu usługi ExpressRoute z hello klasycznego modelu wdrażania.
* Oparta na rolach kontroli dostępu (RBAC) obsługę hello klasycznego modelu wdrażania. Nie można wykonać obwodu tooa kontroli RBAC w hello klasycznego modelu wdrażania. Wszelkie administratora/coadministrator hello subskrypcji można połączyć lub odłącz obwodu toohello sieci wirtualnych.

## <a name="configuration"></a>Konfiguracja
Postępuj zgodnie z instrukcjami hello, które zostały opisane w [przenieść obwodu usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Następne kroki
* [Migracji hello sieci wirtualnych połączonych toohello obwodu usługi expressroute z hello klasycznego modelu toohello usługi Azure Resource Manager modelu](expressroute-migration-classic-resource-manager.md)
* Informacje o przepływach pracy można znaleźć w artykule [ExpressRoute circuit provisioning workflows and circuit states](expressroute-workflows.md) (Przepływy pracy inicjowania obsługi obwodu i stany obwodu usługi ExpressRoute).
* tooconfigure połączenia ExpressRoute:
  
  * [Tworzenie obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-arm.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)

