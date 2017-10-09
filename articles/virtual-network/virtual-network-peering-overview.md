---
title: "aaaAzure sieci wirtualnej komunikacji równorzędnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat wirtualnych sieci równorzędnych na platformie Azure."
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Wirtualne sieci równorzędne
Umożliwia komunikacji równorzędnej sieci wirtualnej można tooconnect dwie sieci wirtualne w hello tego samego regionu za pośrednictwem hello Azure szkieletu sieci. Po połączyć za pomocą, Witaj dwie sieci wirtualne są wyświetlane jako na potrzeby łączności. Witaj dwie sieci wirtualne są nadal zarządzane jako oddzielne zasoby, ale maszyn wirtualnych w hello połączyć za pomocą sieci wirtualne mogą komunikować się ze sobą bezpośrednio, przy użyciu prywatnych adresów IP.

Witaj ruchu między maszynami wirtualnymi w hello połączyć za pomocą sieci wirtualnych jest kierowany przez infrastrukturę platformy Azure, w taki sam sposób, jak ruch jest przekierowywany między maszynami wirtualnymi w hello hello tej samej sieci wirtualnej. Zalety hello przy użyciu sieci wirtualnej komunikacji równorzędnej między innymi:

* Połączenie o małych opóźnieniach i dużej przepustowości między zasobami w różnych sieciach wirtualnych.
* możliwość Hello toouse zasobów, takich jak urządzenia sieciowe i bramy sieci VPN jako punkty przesyłanych w sieci wirtualnej peered.
* Witaj możliwości toopeer dwie sieci wirtualne utworzone za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello lub toopeer jednej sieci wirtualnych utworzonych za pomocą Menedżera zasobów tooa sieci wirtualnej została utworzona za pośrednictwem hello klasycznego modelu wdrażania. Hello odczytu [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) toolearn artykułu więcej informacji na temat hello różnice między hello dwa modele wdrażania platformy Azure.

## <a name="requirements-constraints"></a>Wymagania i ograniczenia

* Witaj połączyć za pomocą sieci wirtualnych muszą istnieć w hello sam region platformy Azure. Sieci wirtualne z różnych regionów platformy Azure można połączyć za pomocą usługi [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Witaj połączyć za pomocą sieci wirtualnych muszą mieć-nakładającymi się obszarami adresów IP.
* Nie można dodać ani usunąć przestrzeni adresowych z sieci wirtualnej po połączeniu sieci wirtualnej z inną siecią wirtualną za pomocą komunikacji równorzędnej.
* Wirtualne sieci równorzędne obejmują dwie sieci wirtualne. Nie istnieje żadna pochodna relacja przechodnia między tymi sieciami. Na przykład, jeśli virtualNetworkA jest połączyć za pomocą z virtualNetworkB i virtualNetworkB jest połączyć za pomocą z virtualNetworkC, jest virtualNetworkA *nie* połączyć za pomocą toovirtualNetworkC.
* Można elementów równorzędnych sieci wirtualnych, które istnieją w dwóch różnych subskrypcji, jak długo użytkownika uprzywilejowanego (zobacz [określonych uprawnień](create-peering-different-deployment-models-subscriptions.md#permissions)) zarówno subskrypcje autoryzuje równorzędna hello i subskrypcje hello są skojarzone toohello tego samego Dzierżawy usługi Azure Active Directory. Można użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect sieci wirtualnych w ramach subskrypcji skojarzone toodifferent dzierżawcy usługi Active Directory.
* Można można połączyć za pomocą sieci wirtualnych, jeśli są tworzone za pomocą modelu wdrażania usługi Resource Manager hello lub jedną sieć wirtualną utworzono za pomocą modelu wdrażania usługi Resource Manager hello i hello innych jest tworzony za pomocą hello klasycznego modelu wdrażania. Dwie sieci wirtualne utworzone za pośrednictwem hello klasycznego modelu wdrażania nie może być jednak połączyć za pomocą tooeach inne. Można użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dwie sieci wirtualne utworzone za pośrednictwem hello klasycznego modelu wdrażania.
* Chociaż hello komunikacji między maszynami wirtualnymi w połączyć za pomocą sieci wirtualne nie ma żadnych ograniczeń dodatkowe ograniczenie użycia przepustowości, maksymalna przepustowość sieci jest w zależności od rozmiaru maszyny wirtualnej hello, które nadal mają zastosowanie. więcej informacji na temat maksymalną przepustowość sieci dla rozmiarów inną maszynę wirtualną, przeczytaj hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny wirtualnej.
* Usługa rozpoznawania wewnętrznych nazw DNS na platformie Azure dla maszyn wirtualnych nie działa w sieciach wirtualnych połączonych za pomocą komunikacji równorzędnej. Maszyny wirtualne mają wewnętrznej nazwy DNS, które są rozpoznawalną tylko w obrębie hello lokalną sieć wirtualną. Można jednak skonfigurować sieci wirtualne toopeered maszyny wirtualne podłączone jako serwery DNS dla sieci wirtualnej. Aby uzyskać szczegółowe informacje, przeczytaj hello [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artykułu.

![Podstawowe wirtualne sieci równorzędne](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Łączność
Po dwóch sieci wirtualne są połączyć za pomocą, zasobów w każdej sieci wirtualnej mogą bezpośrednio łączyć z zasobami w sieci wirtualnej połączyć za pomocą hello. Witaj dwie sieci wirtualne mają pełnego adresu IP na poziomie połączenia.

Opóźnienie sieci Hello jest podróż między dwóch maszyn wirtualnych w sieciach wirtualnych połączyć za pomocą hello takie same jak w przypadku podróż w ramach jednej sieci wirtualnej. przepustowość sieci Hello jest oparta na przepustowość hello jest dozwolona dla maszyny wirtualnej hello, rozmiar proporcjonalne tooits. Nie ma żadnych dodatkowych ograniczenia przepustowości w ramach komunikacji równorzędnej hello.

Hello ruch między maszynami wirtualnymi w sieciach wirtualnych połączyć za pomocą jest kierowany bezpośrednio za pomocą hello Azure infrastruktury zaplecza, nie za pośrednictwem bramy.

Maszyny wirtualne tooa połączenia wirtualnej sieci mogą uzyskiwać dostęp hello wewnętrznych równoważeniem obciążenia punktów końcowych w hello połączyć za pomocą sieci wirtualnej. Grupy zabezpieczeń sieci można zastosować w sieci wirtualne sieci wirtualnej tooblock dostępu tooother lub podsieci, w razie potrzeby.

Podczas konfigurowania sieci wirtualnej komunikacji równorzędnej, możesz otwierać i zamykać hello reguły grupy zabezpieczeń sieci między sieciami wirtualnymi hello. Po otwarciu pełną łączność między połączyć za pomocą sieci wirtualnych, (co jest hello opcja domyślna), można zastosować sieci zabezpieczeń grupy toospecific podsieci lub maszyn wirtualnych tooblock lub zablokowania dostępu określonych. więcej informacji o toolearn sieciowej grupy zabezpieczeń, przeczytaj hello [Przegląd grup zabezpieczeń sieci](virtual-networks-nsg.md) artykułu.

## <a name="service-chaining"></a>Tworzenie łańcuchów usług
Można skonfigurować tras zdefiniowanych przez użytkownika tej maszyny toovirtual punktu w sieciach wirtualnych połączyć za pomocą jako Witaj, "następnego przeskoku" IP address tooenable usługi łańcucha. Tworzenie łańcuchów usługi umożliwia możesz toodirect ruchu z jednej sieci wirtualnej tooa urządzenie wirtualne w peered sieci wirtualnej za pomocą trasy zdefiniowane przez użytkownika.

Można również skutecznie tworzyć typu gwiazda środowiskach, w którym Centrum hello może obsługiwać składników infrastruktury, takiego jak urządzenie wirtualne sieci. Wszystkie sieci wirtualne gwiazdy hello można następnie elementu równorzędnego z siecią wirtualną hello koncentratora. Ruch mógł przepływać za pośrednictwem sieci wirtualnych urządzeń działających w sieci wirtualnej hello koncentratora. Krótko mówiąc równorzędna sieci wirtualnej umożliwia hello następnego przeskoku adresu IP na adresie IP hello zdefiniowane przez użytkownika tras toobe hello maszyny wirtualnej w hello połączyć za pomocą sieci wirtualnej. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika — omówienie](virtual-networks-udr-overview.md) artykułu.

## <a name="gateways-and-on-premises-connectivity"></a>Bramy i łączność lokalna
Każdej sieci wirtualnej, niezależnie od tego, czy jest połączyć z inną siecią wirtualną, za pomocą nadal mieć własną bramę i używać go tooconnect tooan lokalnej sieci. Można również skonfigurować [połączeń sieci do wirtualnych sieci wirtualnej](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) przy użyciu bram, mimo że sieci wirtualne hello są połączyć za pomocą.

Gdy obie opcje wzajemne połączenia wirtualnej sieci są skonfigurowane, hello ruchu między sieciami wirtualnymi hello przechodzi przez konfiguracji komunikacji równorzędnej hello (oznacza to, za pomocą hello Azure szkielet).

Podczas połączyć się za pomocą sieci wirtualnych, można również skonfigurować hello bramy w hello połączyć za pomocą sieci wirtualnej jako sieci lokalnej tooan punktu przesyłania. W takim przypadku hello sieci wirtualnej, który używa bramy zdalnego nie może mieć własną bramę. Jedna sieć wirtualna może mieć tylko jedną bramę. Hello bramy można bramy lokalnego lub zdalnego (w hello połączyć za pomocą sieci wirtualnej), pokazane na poniższej ilustracji hello:

![Tranzyt w komunikacji równorzędnej w sieci wirtualnej](./media/virtual-networks-peering-overview/figure02.png)

Brama przesyłania nie jest obsługiwana w komunikacji równorzędnej relacji hello między sieciami wirtualnymi utworzone przez różne modele wdrażania. Obie sieci wirtualne w komunikacji równorzędnej relacji hello utworzonych za pomocą Menedżera zasobów dla toowork przesyłania bramy.

Gdy hello sieci wirtualne, które współużytkują jedno połączenie Azure ExpressRoute są połączyć za pomocą, hello ruch między nimi przechodzi przez hello komunikacji równorzędnej relacji (oznacza to, za pomocą hello sieci szkieletu Azure). Można nadal używać bramy lokalnej w każdym obwodzie lokalnymi toohello tooconnect sieci wirtualnej. Można również użyć bramy współdzielonej i skonfigurować tranzyt dla łączności lokalnej.

## <a name="provisioning"></a>Inicjowanie obsługi
Wirtualne sieci równorzędne wymagają odpowiednich uprawnień. Jest to funkcja oddzielne w przestrzeni nazw VirtualNetworks hello. Użytkownik może uzyskać równorzędna tooauthorize określonych praw. Użytkownik, który ma dostęp do odczytu zapisu toohello wirtualnej sieci automatycznie dziedziczy tych praw.

Użytkownik, który jest albo administratora lub użytkownika uprzywilejowanego możliwości komunikacji równorzędnej hello można zainicjować komunikacji równorzędnej operację na innej sieci wirtualnej. W przypadku dopasowania żądania dla komunikacji równorzędnej hello drugiej stronie, a jeśli spełnione są inne wymagania, hello komunikacja równorzędna została ustanowiona.

## <a name="limits"></a>Limity
Istnieją ograniczenia dotyczące liczby hello komunikacji równorzędnych dozwoloną dla pojedynczego sieci wirtualnej. Aby uzyskać więcej informacji, przejrzyj hello [ograniczenia sieci Azure](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Cennik
Istnieje nominalna opłata za ruch przychodzący i wychodzący w wirtualnych sieciach równorzędnych. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Następne kroki

* Ukończ samouczek dotyczący równorzędnych sieci wirtualnych. Utworzeniu sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi, została utworzona za pośrednictwem hello takie same lub różne modele wdrażania znajdujące się w hello tych samych lub różnych subskrypcji. Ukończenie samouczka jednego hello następujące scenariusze:
 
    |Model wdrażania platformy Azure  | Subskrypcja  |
    |---------|---------|
    |Resource Manager — w obu przypadkach |[Ta sama](virtual-network-create-peering.md)|
    | |[Różne](create-peering-different-subscriptions.md)|
    |Jedna sieć — Resource Manager, druga — model klasyczny     |[Ta sama](create-peering-different-deployment-models.md)|
    | |[Różne](create-peering-different-deployment-models-subscriptions.md)|

* Dowiedz się, jak toocreate [gwiazdy topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Więcej informacji na temat wszystkich [komunikacji równorzędnej ustawień sieci wirtualnej i w jaki sposób toochange ich](virtual-network-manage-peering.md)
