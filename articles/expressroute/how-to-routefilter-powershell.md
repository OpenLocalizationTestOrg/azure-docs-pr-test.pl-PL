---
title: "Konfigurowanie filtrów trasy dla komunikacji równorzędnej platformy Azure ExpressRoute Microsoft: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak trasy tooconfigure filtrów dla Peering firmy Microsoft przy użyciu programu PowerShell"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Konfigurowanie filtrów tras dla komunikacji równorzędnej firmy Microsoft

Filtry trasy są tooconsume sposób podzbiór obsługiwane usługi za pomocą komunikacji równorzędnej firmy Microsoft. Witaj czynnościach w ramach tej pomocy artykułu, konfigurowanie i zarządzanie nimi Filtry trasy dla obwody usługi ExpressRoute.

Usługi Dynamics 365 i usługi Office 365, takich jak Exchange Online, SharePoint Online i Skype dla firm, są dostępne za pośrednictwem hello komunikacji równorzędnej firmy Microsoft. W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft w obwodu usługi ExpressRoute, wszystkie usługi powiązane toothese prefiksy są rozgłaszane za pośrednictwem sesji BGP hello, które są ustalane. Wartość społeczności protokołu BGP jest dołączone tooevery prefiks tooidentify hello usługa, która jest dostępna za pośrednictwem hello prefiks. Listę wartości społeczności BGP hello i usług hello są one wykonywane na zawiera [społeczności BGP](expressroute-routing.md#bgp).

Jeśli potrzebujesz usług łączności tooall dużej liczby prefiksów są rozgłaszane za pomocą protokołu BGP. To znacznie zwiększa rozmiar hello tabel tras hello obsługiwanego przez routery w sieci. Jeśli planujesz tooconsume tylko podzestaw usług oferowanymi w ramach komunikacji równorzędnej firmy Microsoft, można zmniejszyć rozmiar hello tabel tras na dwa sposoby. Możesz:

- Odfiltrować niechciane prefiksy, stosując filtry tras na Wspólnot protokołu BGP. To jest standardową praktyką sieci i jest powszechnie używany w wielu sieciach.

- Zdefiniuj filtry tras i zastosować je tooyour obwodu ExpressRoute. Filtr tras jest nowy zasób umożliwia wybór hello listę usług, możesz zaplanować tooconsume za pomocą komunikacji równorzędnej firmy Microsoft. Usługi routerami wysłać tylko hello listę prefiksów, które należy usług toohello określonych w filtrze trasy hello.

### <a name="about"></a>Informacje o filtrach trasy

W przypadku skonfigurowania komunikacji równorzędnej firmy Microsoft na obwodu ExpressRoute, routery brzegowe Microsoft hello ustanowić parę sesje BGP z routerami krawędzi hello (należy do Ciebie lub dostawcą połączenia). Nie trasy są anonsowany tooyour sieci. tooenable sieci tooyour anonsów tras, należy skojarzyć filtr tras.

Filtr tras umożliwia zidentyfikowanie usług ma tooconsume za pomocą komunikacji równorzędnej firmy Microsoft obwodu usługi ExpressRoute. Jest zasadniczo białą listę wszystkich wartości społeczności BGP hello. Gdy zasób filtr trasy jest zdefiniowana i dołączyć tooan obwodu usługi expressroute, wszystkie prefiksy, które mapują toohello BGP społeczności wartości są anonsowany tooyour sieci.

filtry tras stanie tooattach toobe z usługami Office 365 na nich, musi mieć usługi Office 365 tooconsume autoryzacji za pośrednictwem usługi ExpressRoute. Jeśli nie jesteś autoryzowanym tooconsume usługi Office 365 usługi ExpressRoute, filtry tras tooattach operacji hello kończy się niepowodzeniem. Aby uzyskać więcej informacji na temat procesu autoryzacji hello zobacz [Azure ExpressRoute dla usługi Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Łączność tooDynamics 365 usługi nie wymagają żadnych poprzednich autoryzacji.

> [!IMPORTANT]
> Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane za pomocą komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy. Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu.
> 
> 

### <a name="workflow"></a>Przepływ pracy

toobe toosuccessfully mogli łączyć się tooservices za pośrednictwem komunikacji równorzędnej firmy Microsoft, należy wykonać następujące kroki konfiguracji hello:

- Musisz mieć aktywne obwodu usługi ExpressRoute z Microsoft równorzędna elastycznie. Program hello następujące instrukcje tooaccomplish te zadania:
  - [Utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie elastycznie i włączona.
  - [Utwórz komunikacji równorzędnej firmy Microsoft](expressroute-circuit-peerings.md) Jeśli zarządzasz hello bezpośrednio sesję protokołu BGP. Lub mieć dostawcą połączenia udostępniania Microsoft komunikacji równorzędnej dla obwodu.

-  Należy utworzyć i skonfigurować filtr trasy.
    - Zidentyfikuj hello usług tooconsume za pomocą komunikacji równorzędnej firmy Microsoft
    - Określenie listy hello BGP wartości społeczności związanych z usługami hello
    - Utwórz regułę tooallow hello prefiks listy zgodnych hello wartości społeczności BGP

-  Należy dołączyć obwodu ExpressRoute toohello hello trasy filtru.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem konfiguracji upewnij się, że spełnia hello następujące kryteria:

 - Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [zainstalować i skonfigurować Azure PowerShelll](/powershell/azure/install-azurerm-ps).

  > [!NOTE]
  > Pobieranie hello najnowszej wersji z galerii programu PowerShell hello, zamiast hello Instalatora. obecnie Hello Instalatora nie obsługuje hello wymaganych poleceń cmdlet.
  > 

 - Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.

 - Musisz mieć aktywny obwód usługi ExpressRoute. Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie elastycznie i włączona.

 - Musisz mieć aktywne komunikacji równorzędnej firmy Microsoft. Postępuj zgodnie z instrukcjami w [tworzenia i modyfikowania konfiguracji komunikacji równorzędnej](expressroute-circuit-peerings.md)

### <a name="log-in-tooyour-azure-account"></a>Zaloguj się za tooyour konto platformy Azure

Przed rozpoczęciem tej konfiguracji, należy zalogować się tooyour konto platformy Azure. polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell.

Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień, a następnie połącz tooyour konta. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
```

Jeśli masz wiele subskrypcji Azure, sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

Określ, które mają toouse subskrypcji hello.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>Krok 1. Pobierz listę prefiksów wartości społeczności BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Pobierz listę wartości społeczności BGP

Użyj następującego polecenia cmdlet tooget hello lista BGP wartości społeczności związanych z usługami dostępny za pośrednictwem komunikacji równorzędnej firmy Microsoft hello i hello listę prefiksów skojarzonych z nimi:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Tworzenie listy wartości hello, które mają toouse

Należy sporządzić listę BGP społeczności wartości, które mają toouse hello trasy filtru. Na przykład wartość społeczności BGP dla usługi Dynamics 365 hello jest 12076:5040.

## <a name="filter"></a>Krok 2. Utwórz filtr tras i regułę filtra

Filtr tras może mieć tylko jedną regułę, a zasada hello musi być typu "Zezwalaj". Ta zasada może mieć listy wartości społeczności BGP skojarzonych z nim.

### <a name="1-create-a-route-filter"></a>1. Utwórz filtr trasy

Najpierw należy utworzyć filtr trasy hello. polecenie Hello "New-AzureRmRouteFilter" tworzy tylko zasób filtr trasy. Po utworzeniu zasobu hello, należy utworzyć regułę i dołączenie go toohello trasy filtru obiektu. Uruchom następujące polecenie toocreate hello zasób filtr trasy:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Utwórz regułę filtru

Można określić zestaw Wspólnot protokołu BGP jako listę rozdzielaną przecinkami, jak pokazano w przykładzie hello. Uruchom następujące polecenie toocreate hello nową regułę:
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Dodaj filtr trasy toohello reguły hello

Uruchom następujące polecenie tooadd hello reguły toohello trasy filtru hello:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>Krok 3. Dołącz obwodu ExpressRoute tooan hello trasy filtru

Uruchom następujące polecenie tooattach hello trasy filtru toohello obwodu usługi expressroute, przy założeniu, że masz tylko komunikacji równorzędnej firmy Microsoft hello:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>właściwości hello tooget filtr tras

właściwości hello tooget filtru trasy, użyj hello następujące kroki:

1. Hello uruchom następujące polecenie tooget hello trasy filtru zasobów:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Pobrać reguły filtrowania hello trasy dla zasobu filtru tras hello, uruchamiając następujące polecenie hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>właściwości hello tooupdate filtr tras

Jeśli filtr trasy hello jest już dołączony tooa obwód, listy społeczności BGP toohello aktualizacji automatycznie propaguje zmiany anonsu prefiksu za pośrednictwem hello ustanowić sesji BGP. Można aktualizować hello BGP społeczności listy filtru trasy przy użyciu następującego polecenia hello:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach filtr tras z obwodu usługi ExpressRoute

Gdy filtr tras jest odłączony od hello obwodu usługi expressroute, prefiksy nie są rozgłaszane za pomocą sesji protokołu BGP hello. Można odłączyć filtr tras z obwodu usługi ExpressRoute, za pomocą następującego polecenia hello:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>toodelete filtr tras

Można tylko Usuń filtr trasy, jeśli nie jest dołączony tooany obwodu. Upewnij się, że filtr trasy hello nie jest dołączony obwodu tooany przed podjęciem próby wykonania toodelete go. Można usunąć filtr trasy, używając hello następujące polecenie:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
