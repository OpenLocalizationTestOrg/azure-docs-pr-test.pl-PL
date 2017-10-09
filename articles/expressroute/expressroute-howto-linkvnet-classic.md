---
title: "Link sieci wirtualnej tooan obwodu ExpressRoute: środowiska PowerShell: klasycznym: Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne) przy użyciu hello klasycznego modelu wdrażania i programu PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Połącz obwodu ExpressRoute tooan sieci wirtualnej przy użyciu programu PowerShell (klasyczne)
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-linkvnet-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-linkvnet-classic.md)
>

Ten artykuł pomoże Ci łączenie obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) za pomocą hello klasycznego modelu wdrażania i programu PowerShell. Sieci wirtualne może być w tej samej subskrypcji hello lub może być częścią innej subskrypcji.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji
1. Należy hello najnowszej wersji hello modułów programu Azure PowerShell. Można pobrać hello najnowsze moduły programu PowerShell z hello PowerShell części hello [Azure pobiera strony](https://azure.microsoft.com/downloads/). Postępuj zgodnie z instrukcjami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) wskazówki krok po kroku na temat tooconfigure moduły programu Azure PowerShell hello toouse komputera.
2. Należy tooreview hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
3. Musisz mieć aktywny obwód usługi ExpressRoute.
   * Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i dostawcą połączenia włączyć hello obwodu.
   * Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu. Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-classic.md) artykułu instrukcje routingu.
   * Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.
   * Musi mieć sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym. Wykonaj instrukcje hello zbyt[Skonfiguruj sieć wirtualną w przypadku połączeń ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Możesz połączyć się too10 sieci wirtualnych tooan obwodu usługi expressroute. Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi. Łączenie większej liczby sieci wirtualnych tooyour obwodu ExpressRoute lub połączyć sieci wirtualnych, które znajdują się w innych regionów geograficznymi włączenie hello dodatek usługi ExpressRoute w warstwie premium. Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu
Za pomocą następującego polecenia cmdlet hello można połączyć sieci wirtualnej tooan obwodu usługi expressroute. Upewnij się, że hello bramy sieci wirtualnej jest tworzony i jest gotowy do konsolidacji przed uruchomieniem polecenia cmdlet hello.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji
Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami. powitania po rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.

Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji. Dla wdrażania ich usług — ale działów hello można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci każdego z działów hello hello organizacji, można użyć własnej subskrypcji. Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute. Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.

> [!NOTE]
> Połączeniami i przepustowością opłat za obwód dedykowany hello będzie właściciela obwodu ExpressRoute toohello zastosowane. Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Administracja
Witaj *właściciela obwodu* jest hello administratora/coadministrator hello subskrypcji, w których hello ExpressRoute utworzeniu obwodu. Witaj właściciela obwodu może autoryzować Administratorzy/coadministrators innych subskrypcji określonego tooas *obwodu użytkowników*, toouse hello dedykowanego obwód, z której jest właścicielem. Obwód użytkowników, którzy są może obwodu ExpressRoute toouse autoryzowanych hello organizacji połączyć sieci wirtualnej hello w ich toohello subskrypcji obwodu ExpressRoute użytkownik jest uprawniony.

właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie. Odwoływanie autoryzacji spowoduje wszystkie linki usuwany z subskrypcji hello, do których dostęp został odwołany.

### <a name="circuit-owner-operations"></a>Operacje właściciela obwodu

**Tworzenie autoryzacji**

Witaj właściciela obwodu autoryzuje hello Administratorzy inne subskrypcje toouse hello określony obwodu. Poniższy przykład hello administrator hello obwodu hello (IT firmy Contoso) umożliwia administratora hello z innej subskrypcji (Test deweloperów) toolink się tootwo sieci wirtualnych toohello obwodu. administrator IT firmy Contoso Hello umożliwia to przez określenie identyfikatora hello testu deweloperów Microsoft. polecenia cmdlet Hello nie wysyła wiadomości e-mail toohello określony identyfikator firmy Microsoft. Właściciel obwodu Hello musi tooexplicitly powiadomić hello innych hello autoryzacji właściciela subskrypcji została ukończona.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Przegląd zezwolenia**

właściciela obwodu Hello można przejrzeć wszystkie autoryzacje, które są wydawane w szczególności obwód, uruchamiając następujące polecenie cmdlet hello:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Aktualizacja zezwoleń**

właściciela obwodu Hello można zmodyfikować autoryzacje za pomocą następującego polecenia cmdlet hello:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Usuwanie zezwolenia**

właściciela obwodu Hello można odwołać/usuwania użytkownika toohello autoryzacje, uruchamiając następujące polecenie cmdlet hello:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Operacje użytkownik obwodu

**Przegląd zezwolenia**

Użytkownik obwodu Hello można przejrzeć autoryzacje za pomocą następującego polecenia cmdlet hello:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Realizowanie autoryzacje łącza**

Użytkownik obwodu Hello można uruchomić następujące polecenie cmdlet tooredeem hello autoryzacji łącza:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Uruchom następujące polecenie w subskrypcji hello nowo połączone sieci wirtualnej hello:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

