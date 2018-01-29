---
title: "Punkty końcowe usługi sieci wirtualnej platformy Azure | Microsoft Docs"
description: "Dowiedz się, jak włączyć bezpośredni dostęp do zasobów platformy Azure z sieci wirtualnej przy użyciu punktów końcowych usługi."
services: virtual-network
documentationcenter: na
author: anithaa
manager: narayan
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/15/2017
ms.author: anithaa
ms.custom: 
ms.openlocfilehash: 7b5675dacd1d9effd73f3bc51ea4efc0ea6be029
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="virtual-network-service-endpoints-preview"></a>Punkty końcowe usługi sieci wirtualnej (wersja zapoznawcza)

Punkty końcowe usługi sieci wirtualnej rozszerzają prywatną przestrzeń adresową i tożsamość sieci wirtualnej do usług platformy Azure za pośrednictwem bezpośredniego połączenia. Punkty końcowe umożliwiają zabezpieczanie krytycznych zasobów usługi platformy Azure tylko do sieci wirtualnych. Ruch z sieci wirtualnej do usługi platformy Azure zawsze pozostaje w sieci szkieletowej platformy Microsoft Azure.

Ta funkcja jest dostępna w wersji zapoznawczej dla następujących regionów i usług platformy Azure:

- **Azure Storage**: wszystkie regiony w chmurze publicznej Azure.
- **Azure SQL**: wszystkie regiony w chmurze publicznej Azure.

Najbardziej aktualne powiadomienia dotyczące wersji zapoznawczej można znaleźć na stronie [aktualizacji usługi Azure Virtual Network](https://azure.microsoft.com/updates/?product=virtual-network).

>[!NOTE]
> W okresie obowiązywania wersji zapoznawczej ta funkcja może nie oferować dostępności i niezawodności na tym samym poziomie, co funkcje w wersji ogólnodostępnej. Aby uzyskać więcej informacji, zobacz [Dodatkowe warunki użytkowania dotyczące wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="key-benefits"></a>Najważniejsze korzyści

Punkty końcowe usługi oferują następujące korzyści:

- **Lepsze zabezpieczenia zasobów usługi platformy Azure**: dzięki punktom końcowym zasoby usługi platformy Azure mogą być chronione w sieci wirtualnej. Zabezpieczenie zasobów usługi w sieci wirtualnej zapewnia większe bezpieczeństwo dzięki całkowitemu usunięciu publicznego dostępu do Internetu dla tych zasobów i zezwolenie na ruch tylko z Twojej sieci wirtualnej.
- **Optymalny routing ruchu usług sieci platformy Azure z sieci wirtualnej**: obecnie wszystkie trasy w sieci wirtualnej, które wymuszają ruch internetowy za pomocą urządzeń lokalnych i/lub wirtualnych (sytuacja znana jako tunelowanie wymuszane), wymuszają również ruch w ramach usługi platformy Azure po tej samej trasie co ruch internetowy. Punkty końcowe usługi zapewniają optymalny routing ruchu platformy Azure. 

  Punkty końcowe zawsze pobierają ruch bezpośrednio z sieci wirtualnej do usługi w sieci szkieletowej platformy Microsoft Azure. Zachowywanie ruchu w sieci szkieletowej platformy Azure umożliwia kontynuowanie inspekcji i monitorowania wychodzącego ruchu internetowego z sieci wirtualnych za pośrednictwem tunelowania wymuszanego, bez wywierania wpływu na ruch usługi. Dowiedz się więcej na temat [tras definiowanych przez użytkownika i tunelowania wymuszanego](virtual-networks-udr-overview.md).
- **Prosta konfiguracja i mniejsze koszty ogólne zarządzania**: nie potrzebujesz już zastrzeżonych publicznych adresów IP w swoich sieciach wirtualnych, aby zabezpieczać zasoby platformy Azure za pośrednictwem zapory adresów IP. Do skonfigurowania punktów końcowych usługi nie jest wymagany translator adresów sieciowych ani urządzenie bramy. Punkty końcowe usługi można skonfigurować za pomocą prostego kliknięcia w podsieci. Utrzymywanie punktów końcowych nie wiąże się z dodatkowymi kosztami ogólnymi.

## <a name="limitations"></a>Ograniczenia

- Funkcja jest dostępna tylko dla sieci wirtualnych wdrożonych za pomocą modelu wdrażania przy użyciu usługi Azure Resource Manager.
- Punkty końcowe są włączone w podsieciach skonfigurowanych w sieciach wirtualnych platformy Azure. Punktów końcowych nie można używać dla ruchu ze środowiska lokalnego do usług platformy Azure. Aby uzyskać więcej informacji, zobacz [Zabezpieczanie dostępu do usług platformy Azure ze środowiska lokalnego](#securing-azure-services-to-virtual-networks)
- Punkt końcowy usługi dotyczy tylko ruchu usługi platformy Azure w regionie sieci wirtualnej. Na potrzeby obsługi ruchu w magazynach GRS i RA-GRS dla usługi Azure Storage punkty końcowe są rozszerzane, aby uwzględniać sparowane regiony, w których wdrożono sieć wirtualną. Dowiedz się więcej na temat [sparowanych regionów platformy Azure](../best-practices-availability-paired-regions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-paired-regions).

## <a name="securing-azure-services-to-virtual-networks"></a>Zabezpieczanie usług platformy Azure w sieciach wirtualnych

- Punkt końcowy usługi sieci wirtualnej zapewnia tożsamość sieci wirtualnej w usłudze platformy Azure. Po włączeniu punktów końcowych usługi w sieci wirtualnej można zabezpieczyć zasoby usług usługi platformy Azure w sieci wirtualnej przez dodanie reguły sieci wirtualnej do zasobów.
- Obecnie ruch usługi platformy Azure z sieci wirtualnej używa publicznych adresów IP jako źródłowych adresów IP. Dzięki punktom końcowym usługi ruch usługi jest przełączany na używanie prywatnych adresów sieci wirtualnej jako źródłowych adresów IP w przypadku uzyskiwania dostępu do usługi platformy Azure z sieci wirtualnej. To przełączenie umożliwia dostęp do usług bez konieczności stosowania zastrzeżonych publicznych adresów IP w zaporach adresów IP.
- __Zabezpieczanie dostępu do usług platformy Azure ze środowiska lokalnego__:

  Domyślnie nie można uzyskać dostępu do zasobów usługi platformy Azure zabezpieczonych w sieciach wirtualnych z sieci lokalnych. Jeśli chcesz zezwolić na ruch ze środowiska lokalnego, musisz również zezwolić na użycie publicznych adresów IP (zazwyczaj translatora adresów sieciowych) z sieci lokalnej lub obwodów usługi ExpressRoute. Te adresy IP można dodawać za pośrednictwem konfiguracji zapory adresów IP dla zasobów usługi platformy Azure.

  ExpressRoute: jeśli korzystasz z usługi [ExpressRoute](../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) w środowisku lokalnym na potrzeby publicznej komunikacji równorzędnej lub komunikacji równorzędnej firmy Microsoft, konieczne będzie określenie używanych adresów IP translatora adresów sieciowych. W przypadku publicznej komunikacji równorzędnej każdy obwód usługi ExpressRoute domyślnie używa dwóch adresów IP translatora adresów sieciowych stosowanych do ruchu w ramach usługi platformy Azure, gdy ruch trafia do sieci szkieletowej platformy Microsoft Azure. W przypadku komunikacji równorzędnej firmy Microsoft używane adresy IP translatora adresów sieciowych są dostarczane przez klienta lub przez dostawcę usług. Aby umożliwić dostęp do zasobów usługi, musisz zezwolić na te publiczne adresy IP w ustawieniu zapory adresu IP zasobu. Aby znaleźć adresy IP obwodów usługi ExpressRoute publicznej komunikacji równorzędnej, [otwórz bilet pomocy technicznej przy użyciu usługi ExpressRoute](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) w witrynie Azure Portal. Dowiedz się więcej o [translatorze adresów sieciowych publicznej komunikacji równorzędnej i komunikacji równorzędnej firmy Microsoft dla usługi ExpressRoute.](../expressroute/expressroute-nat.md?toc=%2fazure%2fvirtual-network%2ftoc.json#nat-requirements-for-azure-public-peering)

![Zabezpieczanie usług platformy Azure w sieciach wirtualnych](./media/virtual-network-service-endpoints-overview/VNet_Service_Endpoints_Overview.png)

### <a name="configuration"></a>Konfiguracja

- Punkty końcowe usługi są konfigurowane w podsieci sieci wirtualnej. Punkty końcowe współpracują z wystąpieniami obliczeniowymi dowolnego typu uruchomionymi w danej podsieci.
- W określonej usłudze można włączyć tylko jedną usługę punktu końcowego z podsieci. W podsieci można skonfigurować wiele punktów końcowych usługi dla wszystkich obsługiwanych usług platformy Azure (na przykład Azure Storage lub Azure SQL Database).
- Sieci wirtualne muszą znajdować się w tym samym regionie, co zasób usługi platformy Azure. Jeśli korzystasz z magazynów GRS i RA-GRS w usłudze Azure Storage, konto podstawowe powinno znajdować się w tym samym regionie, co sieć wirtualna.
- Sieć wirtualna, w której konfigurowany jest punkt końcowy, może należeć do tej samej subskrypcji, co zasób usługi platformy Azure, lub innej. Aby uzyskać więcej informacji na temat uprawnień wymaganych do konfigurowania punktów końcowych i zabezpieczania usług platformy Azure, zobacz [Aprowizowanie](#Provisioning).
- W przypadku obsługiwanych usług można zabezpieczyć nowe lub istniejące zasoby w sieciach wirtualnych za pomocą punktów końcowych usługi.

### <a name="considerations"></a>Zagadnienia do rozważenia

- Po włączeniu punktu końcowego usługi źródłowe adresy IP maszyn wirtualnych w podsieci przełączają się z używania publicznych adresów IPv4 na używanie prywatnego adresu IPv4 podczas komunikacji z usługą z poziomu tej podsieci. Wszystkie otwarte połączenia TCP z usługą są zamykane podczas tego przełączania. Upewnij się, że żadne krytyczne zadania nie działają podczas włączania lub wyłączania punktu końcowego w usłudze dla podsieci. Upewnij się również, czy aplikacje mogą automatycznie połączyć się z usługami platformy Azure po przełączeniu adresu IP.

  Przełączenie adresu IP ma wpływ tylko na ruch usługi z sieci wirtualnej. Nie ma ono wpływu na pozostałe rodzaje ruchu problemu z/do publicznych adresów IPv4 przypisanych do maszyn wirtualnych. Jeśli masz istniejące reguły zapory używające publicznych adresów IP platformy Azure dla usług platformy Azure, te reguły przestają działać po przełączeniu na użycie prywatnych adresów sieci wirtualnej.
- Dzięki punktom końcowym usług wpisy systemu DNS dla usług platformy Azure są obecnie zachowywane w aktualnej postaci i będą nadal rozpoznawać adresy IP przypisane do usługi platformy Azure.
- Sieciowe grupy zabezpieczeń z punktami końcowymi usługi:
  - Domyślnie sieciowe grupy zabezpieczeń zezwalają na ruch wychodzący z Internetu, a także na ruch z sieci wirtualnej do usług platformy Azure. Ta opcja będzie nadal współdziałać z punktami końcowymi usługi w ten sposób. 
  - Jeśli chcesz odrzucić cały ruch wychodzący z Internetu i zezwolić tylko na ruch do określonych usług platformy Azure, możesz to zrobić za pomocą opcji __„Tagi usług platformy Azure”__ w sieciowej grupie zabezpieczeń. Obsługiwane usługi platformy Azure można określić jako miejsce docelowe w regułach sieciowych grup zabezpieczeń, a konserwacją adresów IP w obrębie każdego tagu zajmuje się platforma Azure. Aby uzyskać więcej informacji, zobacz [Azure Service tags for NSGs (Tagi usług platformy Azure dla sieciowych grup zabezpieczeń)](https://aka.ms/servicetags). 

### <a name="scenarios"></a>Scenariusze

- **Równorzędne lub połączone sieci wirtualne albo wiele sieci wirtualnych**: aby zabezpieczyć usługi platformy Azure w wielu podsieciach sieci wirtualnej lub wielu sieciach wirtualnych, możesz niezależnie włączyć punkty końcowe usługi w każdej z tych podsieci i zabezpieczyć zasoby usługi platformy Azure we wszystkich tych podsieciach.
- **Filtrowanie ruchu wychodzącego z sieci wirtualnej do usług platformy Azure**: jeśli chcesz sprawdzić lub filtrować ruch kierowany do usługi platformy Azure z sieci wirtualnej, możesz wdrożyć sieciowe urządzenie wirtualne w ramach tej sieci wirtualnej. Następnie możesz zastosować punkty końcowe usługi do podsieci, w której wdrożono sieciowe urządzenie wirtualne, i zabezpieczyć zasób usługi platformy Azure tylko w tej podsieci. Ten scenariusz może być przydatny, jeśli chcesz ograniczyć dostęp do usługi platformy Azure z sieci wirtualnej tylko do określonych zasobów platformy Azure przy użyciu filtrowania sieciowych urządzeń wirtualnych. Aby uzyskać więcej informacji, zobacz [ruch wychodzący z sieciowych urządzeń wirtualnych](/azure/architecture/reference-architectures/dmz/nva-ha#egress-with-layer-7-nvas.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
- **Zabezpieczanie zasobów platformy Azure w usługach wdrożonych bezpośrednio do sieci wirtualnych**: różne usługi platformy Azure można wdrażać bezpośrednio w określonych podsieciach sieci wirtualnej. Zasoby usługi platformy Azure można zabezpieczyć w podsieciach [usługi zarządzanej](virtual-network-for-azure-services.md), konfigurując punkt końcowy usługi w podsieci usługi zarządzanej.

### <a name="logging-and-troubleshooting"></a>Rejestrowanie i rozwiązywanie problemów

Po skonfigurowaniu punktów końcowych usługi do określonej usługi zweryfikuj obowiązywanie trasy punktu końcowego usługi przez: 
 
- Weryfikowanie źródłowego adresu IP każdego żądania obsługi w diagnostyce usługi. Wszystkie nowe żądania z punktami końcowymi usługi pokazują pozycję „źródłowy adres IP” dla żądania jako prywatny adres sieci wirtualnej przypisany do klienta wysyłającego żądanie z sieci wirtualnej. Bez punktu końcowego ten adres będzie publicznym adresem IP platformy Azure.
- Wyświetlanie skutecznych tras w dowolnym interfejsie sieciowym w podsieci. Trasa do usługi:
  - Pokazuje dokładniej określoną domyślną trasę do zakresu prefiksów adresów danej usługi.
  - Ma element nextHopType o wartości *VirtualNetworkServiceEndpoint*.
  - Wskazuje, że istnieje bardziej bezpośrednie — w porównaniu z trasami tunelowania wymuszanego — połączenie z usługą.

>[!NOTE]
> Trasy punktu końcowego usługi zastępują trasy BGP lub UDR dla dopasowania prefiksu adresu usługi platformy Azure. Dowiedz się więcej na temat [rozwiązywania problemów ze skutecznymi trasami](virtual-network-routes-troubleshoot-portal.md#using-effective-routes-to-troubleshoot-vm-traffic-flow)

## <a name="provisioning"></a>Inicjowanie obsługi

Punkty końcowe usługi można niezależnie konfigurować w sieciach wirtualnych — czynność tę może wykonać użytkownik z uprawnieniami do zapisu w sieci wirtualnej. Aby zabezpieczyć zasoby usługi platformy Azure w sieci wirtualnej, użytkownik musi mieć uprawnienia do elementu *Microsoft.Network/JoinServicetoaSubnet* dla dodawanych podsieci. To uprawnienie jest domyślnie uwzględniane we wbudowanych rolach administratora usługi, domyślnie i może być modyfikowane przez tworzenie ról niestandardowych.

Dowiedz się więcej na temat [wbudowanych ról](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) i przypisywaniu określonych uprawnień do [ról niestandardowych](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

Sieci wirtualne i zasoby usług platformy Azure mogą należeć do tej samej lub różnych subskrypcji. Jeśli zasoby sieci wirtualnej i usługi platformy Azure należą do różnych subskrypcji, w okresie obowiązywania tej wersji zapoznawczej zasoby muszą znajdować się w tej samej dzierżawie usługi Active Directory (AD). 

## <a name="pricing-and-limits"></a>Ceny i limity

Za korzystanie z punktów końcowych usługi nie są naliczane dodatkowe opłaty. Obecnie stosowany jest bieżący model cen usług platformy Azure (Azure Storage, Azure SQL Database).

Nie ma limitu całkowitej liczby punktów końcowych usługi w sieci wirtualnej.

W przypadku zasobów usług platformy Azure (np. konta usługi Azure Storage) usługi mogą wymuszać limity liczby podsieci używanych do zabezpieczania zasobów. Szczegółowe informacje można znaleźć w dokumentacji dotyczącej różnych usług w sekcji [Następne kroki](#next-steps).

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak [skonfigurować punkty końcowe usługi sieci wirtualnej](virtual-network-service-endpoints-configure.md)
- Dowiedz się, jak [zabezpieczyć konto usługi Azure Storage w sieci wirtualnej](../storage/common/storage-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- Dowiedz się, jak [zabezpieczyć usługę Azure SQL Database w sieci wirtualnej](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- Dowiedz się więcej o [integracji usług platformy Azure w sieciach wirtualnych](virtual-network-for-azure-services.md)
-  Szybki start: [szablon usługi Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/201-vnet-2subnets-service-endpoints-storage-integration) do konfigurowania punktu końcowego usługi w podsieci sieci wirtualnej i zabezpieczenia konta usługi Azure Storage do tej podsieci.

