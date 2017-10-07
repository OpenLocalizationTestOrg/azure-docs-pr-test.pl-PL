---
title: "aaaWorkflows konfigurowania obwodu usługi ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona przeprowadzi Cię przez przepływy pracy hello związane z konfigurowaniem obwodu ExpressRoute i komunikacji równorzędnych"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Przepływy pracy ExpressRoute dla aprowizacji obwodu i stanów obwodu
Ta strona przeprowadzi Cię przez Inicjowanie obsługi usługi hello i przepływy pracy routingu configuration na wysokim poziomie.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Witaj Poniższa ilustracja i odpowiadające jej kroki Pokaż hello zadań należy wykonać w kolejności toohave ExpressRoute obwodu elastycznie end-to-end. 

1. Za pomocą programu PowerShell tooconfigure obwodu usługi ExpressRoute. Postępuj zgodnie z instrukcjami hello hello [obwody tworzenia usługi ExpressRoute](expressroute-howto-circuit-classic.md) artykułu, aby uzyskać więcej informacji.
2. Kolejność łączność z usługodawcą hello. Ten proces może być różna. Skontaktuj się z dostawcą połączenia, aby uzyskać więcej informacji o tym, jak tooorder łączności.
3. Upewnij się, że obwód hello zainicjowano pomyślnie weryfikując obwodu ExpressRoute hello udostępniania stanu za pomocą programu PowerShell. 
4. Konfigurowanie domen routingu. Jeśli dostawca połączenia zarządza warstwy 3, firma chce skonfigurować routing dla obwodu. Jeśli dostawca połączenia udostępnia tylko usługi warstwy 2, należy skonfigurować routing według wskazówek opisanych w hello [wymagania dotyczące routingu](expressroute-routing.md) i [konfiguracji routingu](expressroute-howto-routing-classic.md) stron.
   
   * Włącz Azure prywatnej komunikacji równorzędnej — musi umożliwić tej komunikacji równorzędnej tooVMs tooconnect / wdrożone w ramach sieci wirtualnej usługi w chmurze.
   * Włącz Azure publicznej komunikacji równorzędnej — należy włączyć Azure publicznej komunikacji równorzędnej w razie potrzeby tooconnect tooAzure usług hostowanych na publiczne adresy IP. Jest to wymaganie tooaccess zasobów platformy Azure, jeśli wybrano tooenable routing domyślny dla platformy Azure prywatnej komunikacji równorzędnej.
   * Włączanie komunikacji równorzędnej firmy Microsoft — należy włączyć to tooaccess usługi Office 365 i Dynamics 365. 
     
     > [!IMPORTANT]
     > Należy upewnić się, że używasz oddzielnego serwera proxy / tooMicrosoft tooconnect krawędzi niż używany dla hello hello Internet. Przy użyciu hello samej krawędzi ExpressRoute i hello Internet będą powodować asymetrycznego routingu i powodować awarie łączność w sieci.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Połączenie wirtualnej sieci obwody tooExpressRoute — możesz połączyć obwodu ExpressRoute tooyour sieci wirtualnych. Postępuj zgodnie z instrukcjami [toolink sieci wirtualnych](expressroute-howto-linkvnet-arm.md) tooyour obwodu. Te sieci wirtualne mogą być w tej samej subskrypcji platformy Azure jako obwodu ExpressRoute hello hello, lub może być w innej subskrypcji.

## <a name="expressroute-circuit-provisioning-states"></a>Inicjowanie obsługi administracyjnej stanów obwodu usługi expressroute
Każdy obwód usługi ExpressRoute ma dwa stany:

* Stan inicjowania obsługi administracyjnej dostawcy usługi
* Stan

Stan reprezentuje stan inicjowania obsługi administracyjnej firmy Microsoft. Ta właściwość ma wartość tooEnabled, podczas tworzenia obwodu usługi Expressroute

Stan inicjowania obsługi administracyjnej dostawcy łączności Hello reprezentuje stan powitania po stronie powitania połączenia dostawcy. Może to być *NotProvisioned*, *inicjowania obsługi administracyjnej*, lub *obsługiwane administracyjnie*. Hello obwodu ExpressRoute należy w stanie obsługiwane administracyjnie możesz toobe stanie toouse go.

### <a name="possible-states-of-an-expressroute-circuit"></a>Możliwe stany obwodu usługi ExpressRoute
Ta sekcja zawiera limit hello możliwe stany dla obwodu usługi ExpressRoute.

**W czasie tworzenia**

Zostanie wyświetlone hello obwodu usługi expressroute w powitania po stanie tak szybko, jak można uruchomić obwodu ExpressRoute hello toocreate polecenia cmdlet programu PowerShell hello.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Gdy dostawca połączenia jest w procesie inicjowania obsługi administracyjnej obwodu hello hello**

Zobaczysz hello obwodu usługi expressroute w powitania po stanie tak szybko, jak możesz przekazać hello usługodawcy klucza toohello łączności i uruchomienia hello w procesie inicjowania obsługi.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Po zakończeniu procesu udostępniania hello dostawca połączenia**

Zobaczysz hello obwodu usługi expressroute w powitania po stanu, jak dostawca połączenia hello ukończono hello w procesie inicjowania obsługi.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Zainicjowano obsługę administracyjną i włączone jest hello obwodu hello stanu może być tylko w dla możesz toobe stanie toouse go. Jeśli używasz dostawcy warstwy 2, można skonfigurować routing dla obwodu tylko wtedy, gdy znajduje się w tym stanie.

**Gdy dostawca połączenia jest anulowania obsługi hello obwodu**

Jeśli zażądano hello usługi dostawcy toodeprovision hello obwodu usługi expressroute, pojawi się zestawu obwodu hello toohello po stanie po zakończeniu hello anulowania obsługi procesu hello dostawcy usług.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Możesz wybrać toore włącz go, jeśli potrzebne lub uruchamiania poleceń cmdlet programu PowerShell toodelete hello obwodu.  

> [!IMPORTANT]
> Po uruchomieniu hello PowerShell polecenia cmdlet toodelete hello obwodu hello ServiceProviderProvisioningState jest operacja hello inicjowania obsługi administracyjnej lub obsługiwane administracyjnie zakończy się niepowodzeniem. Należy najpierw współpracować obwodu ExpressRoute hello toodeprovision dostawcy łączność, a następnie usuń hello obwodu. Firma Microsoft będzie toobill hello obwód, dopóki nie zostanie uruchomione hello obwodu hello toodelete polecenia cmdlet programu PowerShell.
> 
> 

## <a name="routing-session-configuration-state"></a>Stan konfiguracji sesji routingu
Hello stan inicjowania obsługi protokołu BGP pozwala sprawdzić, czy sesji BGP hello został włączony na powitania Microsoft edge. Witaj stanu, należy włączyć możesz toobe toouse stanie hello równorzędna.

Jest stan sesji BGP hello ważne toocheck szczególnie w przypadku komunikacji równorzędnej firmy Microsoft. Toohello dodanie BGP stan inicjowania obsługi administracyjnej, istnieje inny stan o nazwie *stanu publiczne prefiksy anonsowane*. Witaj anonsowany stan prefiksów publicznych musi być w *skonfigurowane* stanu, zarówno dla toobe sesji BGP hello się i Twoje routingu toowork end-to-end. 

Jeśli hello anonsowane ustawiony stan publicznego prefiks tooa *weryfikacji potrzebne* stanu sesji BGP hello nie jest włączona, jak hello anonsowane prefiksy jest niezgodny z hello jako liczba w żadnym hello rejestrów routingu. 

> [!IMPORTANT]
> Jeśli stan publiczne prefiksy anonsowane hello jest *weryfikowanie ręczne* stanu, należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i udowodnić, że posiadanych adresów IP hello anonsowane wzdłuż z hello skojarzony numer systemu autonomicznego.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Skonfiguruj połączenie usługi ExpressRoute.
  
  * [Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](expressroute-howto-circuit-arm.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-arm.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)

