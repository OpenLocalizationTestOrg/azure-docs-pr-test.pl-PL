---
title: "aaaAzure ExpressRoute dla dostawców rozwiązań w chmurze | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje o dostawcy usług w chmurze tego tooincorporate chcesz Azure usługi i usługi ExpressRoute w ich oferty."
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>Usługa ExpressRoute dla dostawców rozwiązań w chmurze (CSP)
Firma Microsoft udostępnia usługi funkcji Hyper skalowania dla odsprzedawców tradycyjnych a dystrybutorów (CSP) toobe toorapidly można udostępnić nowych usług i rozwiązań dla klientów bez hello potrzebne tooinvest w tworzeniu tych nowych usług. tooallow hello Cloud Solution Provider (CSP) hello możliwości toodirectly zarządzać tych nowych usług, firma Microsoft udostępnia programy i interfejsy API umożliwiające hello toomanage dostawcy usług Kryptograficznych Microsoft Azure zasobów w imieniu klientów. Jednym z tych zasobów jest usługa ExpressRoute. ExpressRoute umożliwia hello dostawcy usług Kryptograficznych tooconnect istniejących zasobów tooAzure działu pomocy technicznej. ExpressRoute jest szybkich tooservices łącze dla prywatnej komunikacji na platformie Azure. 

ExpresRoute składa się z pary obwody wysokiej dostępności, które są dołączone tooa subskrypcje jednego odbiorcy i nie może być współużytkowane przez wielu klientów. Każdy obwód powinno zostać zakończone w różnych router toomaintain hello wysokiej dostępności.

> [!NOTE]
> Usługa ExpressRoute obejmuje przepustowość i zakończenia połączenia, co oznacza, że duże/złożone wdrożenia będą wymagały wielu obwodów usługi ExpressRoute dla jednego klienta.
> 
> 

Microsoft Azure udostępnia coraz więcej usług, że możesz zaoferować klientom tooyour.  toobest korzystanie z tych usług wymaga użycia hello ExpressRoute połączeń tooprovide szybkich małych opóźnieniach dostępu toohello Microsoft Azure środowiska.

## <a name="microsoft-azure-management"></a>Zarządzanie na platformie Microsoft Azure
Firma Microsoft opracowuje dla dostawców usług kryptograficznych toomanage interfejsów API powitania klienta Azure subskrypcji, zezwalając programowe integracji z własne systemy zarządzania usługi. Obsługiwane funkcje zarządzania można znaleźć [tutaj](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Zarządzanie zasobami Microsoft Azure
W zależności od hello umowy z klienta określi, jak będą zarządzane hello subskrypcji. Witaj dostawcy usług Kryptograficznych można było bezpośrednio zarządzać hello tworzenia i konserwacji zasobów lub powitania klienta mogą zachować kontrolę nad hello subskrypcji Microsoft Azure i utworzenie hello zasobów platformy Azure, zgodnie z zapotrzebowaniem. Jeśli klient zarządza hello tworzenia zasobów w swoich subskrypcji Microsoft Azure używają jednego z dwóch modeli: "Connect-za pośrednictwem" modelu lub model "Bezpośrednio do". Te modele są szczegółowo opisane w hello następujące sekcje.  

### <a name="connect-through-model"></a>Model typu „połącz przez”
![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

W hello połączenia przez model hello dostawcy usług Kryptograficznych tworzy bezpośrednie połączenie między centrum danych i klientów subskrypcji platformy Azure. Witaj połączenie bezpośrednie jest nawiązywane, przy użyciu usługi ExpressRoute, połączenie sieci platformy Azure. Następnie klient łączy sieć tooyour. Ten scenariusz wymaga klienta hello przechodzi przez hello tooaccess sieci dostawcy usług Kryptograficznych usług platformy Azure. 

Jeśli klient ma inne subskrypcje platformy Azure, które nie są zarządzane przez hello możesz, ich użyje hello publicznego Internetu lub własne prywatną tooconnect toothose usługi udostępniane w ramach subskrypcji z systemem innym niż dostawcy usług Kryptograficznych hello. 

Dostawca usług Kryptograficznych zarządzania usługami Azure zakłada się, że hello dostawcy usług Kryptograficznych ma tożsamości klienta uprzednio ustanowionym, przechowywania, która będzie następnie zostać zreplikowane do usługi Azure Active Directory dla zarządzania swoją subskrypcję dostawcy usług Kryptograficznych za pośrednictwem Administrate-On-Behalf-Of (AOBO). Klucza sterowniki dla tego scenariusza obejmują gdzie danego partnera lub dostawcy usług ma ustanowić relacji z klientem hello, powitania klienta jest aktualnie używające dostawcy usług lub partnera hello desire tooprovide kombinację hostowanych przez dostawcę i rozwiązań hostowanych Azure tooprovide elastyczność i adres odbiorcy wyzwania, które nie mogą być spełnione przez samego dostawcy usług Kryptograficznych. Ten model został przedstawiony na **rysunku** poniżej.

![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Połącz toomodel
![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/connect-to.png)

W hello Connect toomodel, dostawca usługi hello tworzy bezpośrednie połączenie między centrum danych ich klienta i hello dostawcy usług Kryptograficznych obsługi administracyjnej subskrypcji platformy Azure przy użyciu usługi ExpressRoute przez powitania klienta (klienta) sieci.

> [!NOTE]
> W przypadku połączeń ExpressRoute powitania klienta będzie muszą toocreate a obsługa hello obwodu ExpressRoute.  
> 
> 

W tym scenariuszu łączności wymaga powitania klienta łączy się bezpośrednio za pomocą klienta sieci tooaccess subskrypcji platformy Azure zarządzanego dostawcy usług Kryptograficznych, używając bezpośrednie połączenie sieciowe utworzone, własnością i zarządzanych przez klienta na powitania całości lub częściowo. Dla tych klientów zakłada się, że dostawcy hello nie ma obecnie magazynu tożsamości klienta, ustanowić i dostawcy hello może ułatwić powitania klienta replikowanie bieżącym Identyfikuj w usłudze Azure Active Directory do zarządzania ich Subskrypcja za pośrednictwem AOBO. Sterowniki klucza dla tego scenariusza obejmują gdzie danego partnera lub dostawcy usług ma ustanowić relacji z klientem hello, powitania klienta jest aktualnie używające dostawcy usług lub hello partner ma usług tooprovide desire, które są oparte wyłącznie na Rozwiązania hostowanymi na platformie Azure, bez hello mają do istniejącego dostawcy centrum danych lub infrastruktury.

![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Witaj wybór między tych dwóch opcji są oparte na potrzeby klientów i bieżące wymagają tooprovide Azure usługi. Szczegóły Hello tych modeli i hello skojarzone kontroli dostępu opartej na rolach, sieci i wzorce projektowe tożsamości są objęte szczegółów w hello następującego łącza:

* **Kontrola dostępu na podstawie ról (RBAC)** — RBAC opiera się na usłudze Azure Active Directory.  Więcej informacji na temat funkcji Azure RBAC znajduje się [tutaj](../active-directory/role-based-access-control-configure.md).
* **Sieć** — obejmuje hello różne tematy sieci w programie Microsoft Azure.
* **Azure Active Directory (AAD)** — hello Zarządzanie tożsamościami dla Microsoft Azure i aplikacji SaaS 3 udostępnia usługi AAD. Więcej informacji na temat usługi Azure AD znajduje się [tutaj](https://azure.microsoft.com/documentation/services/active-directory/).  

## <a name="network-speeds"></a>Szybkość sieci
ExpressRoute obsługuje szybkości sieci z 50 Mb/s too10Gb s. Dzięki temu klienci toopurchase hello ilość przepustowości sieci potrzebnych do ich unikatowy środowiska.

> [!NOTE]
> W razie potrzeby bez przerywania łączności można zwiększyć przepustowość sieci, ale szybkość sieci hello tooreduce wymaga przerwanie dół obwodu hello i ponowne utworzenie go na powitania mniejszej szybkości sieci.  
> 
> 

ExpressRoute obsługuje hello połączenie wielu sieci wirtualnych tooa pojedynczego obwodu usługi expressroute dla lepsze wykorzystanie hello szybkich połączeń. Pojedynczy obwodu ExpressRoute mogą być współużytkowane przez wiele subskrypcji Azure własnością hello tego samego klienta.

## <a name="configuring-expressroute"></a>Konfigurowanie usługi ExpressRoute
ExpressRoute może być skonfigurowany toosupport trzy typy ruchu ([domen routingu](#ExpressRoute-routing-domains)) za pośrednictwem jednego obwodu usługi expressroute. Ten ruch można podzielić na komunikację równorzędną Microsoft, publiczną i prywatną komunikację równorzędną Azure. Można wybrać jednego lub wszystkich rodzajów ruchu toobe wysyłane za pośrednictwem jednego obwodu ExpressRoute lub użyć wielu obwody usługi ExpressRoute w zależności od wielkości hello hello obwodu ExpressRoute i izolację wymagane przez klienta. stan zabezpieczeń powitania klienta może nie zezwalać publicznego ruchu i tootraverse prywatnej ruchu za pośrednictwem hello tego samego obwodu.

### <a name="connect-through-model"></a>Model typu „połącz przez”
W hello connect do konfiguracji będzie odpowiedzialny za wszystkie hello sieci tooconnect underpinnings subskrypcji toohello zasobów Centrum danych klientów hostowana na platformie Azure. Każdego klienta interesujące toouse funkcji platformy Azure będzie konieczne własne połączenia ExpressRoute, które będą zarządzane przez hello należy. Witaj użyjesz hello obwodu ExpressRoute hello tooprocure użyć tej samej metody powitania klienta. Witaj chcesz przeprowadzić hello te same kroki opisane w artykule hello [przepływy pracy usługi ExpressRoute](expressroute-workflows.md) kątem aprowizacji obwodów i stanów obwodów. Witaj, następnie skonfiguruje hello protokołu BGP (Border Gateway) trasy toocontrol hello ruchu przechodzenia między siecią lokalną hello i sieci wirtualnej platformy Azure.

### <a name="connect-toomodel"></a>Połącz toomodel
W connect tooconfiguration, klient istniejących tooAzure połączenia lub ma zainicjuje połączenie toohello usługodawcy internetowego połączeń ExpressRoute z centrum danych przez klienta bezpośrednio tooAzure zamiast Centrum danych. toobegin hello procesu zastrzegania, klient będzie wykonaj kroki hello, zgodnie z powyższym opisem hello Connect do modelu. Po ustanowieniu obwodu powitania klienta należy tooconfigure hello lokalnych routerów toobe stanie tooaccess sieciowe i sieci wirtualnych platformy Azure.

Mogą pomóc w skonfigurowaniu hello połączenia i konfigurowanie hello kieruje tooallow hello zasobów w Twojej toocommunicate datacenter(s) powitania klienta zasobów w centrum danych lub zasobów hello hostowana na platformie Azure.

## <a name="expressroute-routing-domains"></a>Domeny routingu usługi ExpressRoute
Usługa ExpressRoute oferuje trzy domeny routingu: publiczną, prywatną i komunikacji równorzędnej firmy Microsoft. Każdej z domen routingu hello są skonfigurowane z routerami identyczne w konfiguracji aktywny aktywny wysokiej dostępności. Więcej szczegółowych informacji dotyczących domen routingu usługi ExpressRoute można znaleźć [tutaj](expressroute-circuit-peerings.md).

Można zdefiniować trasy niestandardowe filtry tooallow tylko hello sposobu (sposobów) mają tooallow lub potrzebujesz. Aby uzyskać więcej informacji lub toosee jak toomake te zmiany w temacie artykuł: [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell](expressroute-howto-routing-classic.md) Aby uzyskać więcej informacji o filtrach routingu.

> [!NOTE]
> Microsoft i publicznej komunikacji równorzędnej łączności musi być jednak publicznego adresu IP należących do dostawcy usług Kryptograficznych lub powitania klienta i musi być zgodne tooall zdefiniowanych reguł. Aby uzyskać więcej informacji, zobacz hello [wymagania wstępne usługi ExpressRoute](expressroute-prerequisites.md) strony.  
> 
> 

## <a name="routing"></a>Routing
ExpressRoute łączy toohello Azure sieci za pośrednictwem hello Brama sieci wirtualnej platformy Azure. Bramy sieci zapewniają routing dla sieci wirtualnych Azure.

Tworzenie sieci wirtualnych Azure tworzy również tabelę routingu domyślnego hello sieci wirtualnej toodirect ruchu z podsieci hello hello sieci wirtualnej. Jeśli tabela tras domyślnych hello jest niewystarczający dla rozwiązania hello niestandardowe trasy można tworzyć urządzenia toocustom ruchu wychodzącego tooroute lub tooblock kieruje toospecific podsieci lub sieci zewnętrznych.

### <a name="default-routing"></a>Routing domyślny
Tabela tras domyślnych Hello obejmuje hello następujących tras:

* Routing w podsieci
* Podsieci do sieci w ramach sieci wirtualnej hello
* toohello Internet
* Sieć wirtualna do sieci wirtualnej przy użyciu bramy sieci VPN
* Sieć wirtualna do sieci lokalnej przy użyciu bramy sieci VPN lub usługi ExpressRoute

![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Routing zdefiniowany przez użytkownika (UDR)
Trasy zdefiniowane przez użytkownika umożliwia hello kontroli ruchu wychodzącego z hello przypisanych podsieci tooother podsieci w sieci wirtualnej hello lub hello ponad jednego z innych bram wstępnie zdefiniowane (ExpressRoute; internet lub sieć VPN). Tabela routingu Hello domyślnych systemu można zastąpić zdefiniowane przez użytkownika tabelę routingu, która zastępuje domyślną tabelę routingu hello trasy niestandardowe. Zdefiniowane przez użytkownika routingu klientów można utworzyć tooappliances określonej trasy, takich jak zapory lub urządzenia wykrywania nieautoryzowanego dostępu lub blokowanie dostępu toospecific podsieci z podsieci hello hosting hello trasy zdefiniowane przez użytkownika. Omówienie tras zdefiniowanych przez użytkownika znajduje się [tutaj](../virtual-network/virtual-networks-udr-overview.md). 

## <a name="security"></a>Bezpieczeństwo
W zależności od tego, czy model, który jest używany, Połącz tooor Connect-przez klienta definiuje zasady zabezpieczeń hello w ich sieci wirtualnej lub zawiera wymagania dotyczące zasad zabezpieczeń hello toohello dostawcy usług Kryptograficznych toodefine tootheir w sieci wirtualnych. można zdefiniować Hello następujące kryteria zabezpieczeń:

1. **Izolacja klienta** — hello platformy Azure zapewnia izolację klienta przez zapisanie informacji o identyfikator klienta i sieci wirtualnej w bezpiecznej bazie danych, która jest używana tooencapsulate ruchu każdego klienta w tunelu GRE.
2. **Sieciowe grupy zabezpieczeń (NSG)** są reguł określających dozwolony ruch do i z hello podsieci w sieci wirtualnych na platformie Azure. Domyślnie hello grupy NSG zawierają bloku reguły tooblock ruch z sieci wirtualnej toohello Internet hello i reguł zezwalania na ruch w sieci wirtualnej. Więcej informacji na temat grup zabezpieczeń sieci znajduje się [tutaj](https://azure.microsoft.com/blog/network-security-groups/).
3. **Tunelowanie** — jest to tooredirect opcji internetowych powiązany ruchu pochodzącego z Azure toobe przekierowanie za pośrednictwem toohello połączenia ExpressRoute hello w lokalnym centrum danych. Więcej informacji o na temat tunelowania wymuszonego można znaleźć [tutaj](expressroute-routing.md#advertising-default-routes).  
4. **Szyfrowanie** — mimo że obwody usługi ExpressRoute hello są dedykowane tooa określonego klienta, istnieje możliwość hello hello dostawcy sieci może być naruszone, stosowanie intruz tooexamine pakietów ruchu. tooaddress, który to ryzyko, klienta lub dostawcy usług Kryptograficznych można zaszyfrować ruchu za pośrednictwem hello połączenie przez określenie zasad trybu tunelowania IPSec dla całego ruchu przechodzenia między hello w lokalnych zasobach i zasobów platformy Azure (zobacz toohello opcjonalne trybu tunelowania IPSec dla klienta 1 na rysunku 5: ExpressRoute zabezpieczeń powyżej). Druga opcja Hello byłoby toouse urządzenia zapory w każdym punkcie końcowym hello hello obwodu usługi expressroute. Wymaga to dodatkowe strony 3 zapory zainstalowane na ruch hello tooencrypt kończy się za pośrednictwem obwodu ExpressRoute hello toobe maszyny wirtualne/urządzeń.

![tekst alternatywny](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Następne kroki
Witaj usługi Cloud Solution Provider zapewnia tooincrease sposób, potrzebują klienci tooyour wartość bez hello kosztowne zakupów infrastruktury i możliwości, przy zachowaniu stanowisko hello outsourcing podstawowego dostawcy. Integracja z Microsoft Azure można osiągnąć za pośrednictwem hello API dostawcy usług Kryptograficznych, umożliwiając toointegrate zarządzania Microsoft Azure w ramach Twojej istniejącej struktury zarządzania.  

Dodatkowe informacje można znaleźć na powitania następującego łącza:

[Microsoft Cloud Solution Provider program](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview) (Program dostawcy rozwiązań w chmurze Microsoft).  
[Pobierz gotowe tootransact jako dostawca rozwiązań w chmurze](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Microsoft Cloud Solution Provider resources](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources) (Zasoby dostawcy rozwiązań w chmurze Microsoft).

