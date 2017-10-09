Podczas tworzenia bramy sieci wirtualnej, należy toospecify hello bramy, które mają toouse jednostki SKU. Wybierz jednostki SKU hello, które spełniają wymagania na podstawie typów hello obciążeń, przepustowości, funkcje i umowy SLA.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Obciążenia w trybie produkcyjnym *a obciążenia* w środowisku tworzenia i testowania

Powodu różnic toohello SLA i zestawy funkcji, firma Microsoft zaleca powitania po jednostki SKU dla trybu produkcyjnego *a* deweloperów testu:

| **Obciążenie**                       | **Jednostki SKU**               |
| ---                                | ---                    |
| **Tryb produkcyjny, obciążenia krytyczne** | VpnGw1, VpnGw2, VpnGw3 |
| **Środowisko tworzenia i testowania lub weryfikacja koncepcji**   | Podstawowa                  |
|                                    |                        |

Jeśli używasz starego hello jednostki SKU, hello produkcji jednostki SKU zalecenia to Standard i wysokowydajnej jednostki SKU. Informacje dotyczące hello starego SKU sekcji [jednostki SKU bramy (starszej wersji jednostki SKU)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Zestawy funkcji jednostek SKU bramy

Witaj nową bramę jednostki SKU idealne hello rozwiązanie oferowane w bramach hello:

| **SKU**| **Funkcje**|
| ---    | ---         |
|**Podstawowa**   | **Sieć VPN oparta na trasach**: 10 tuneli z połączeniami typu punkt-lokacja<br><br>**Sieć VPN oparta na zasadach** (IKEv1): 1 tunel, bez połączeń typu punkt-lokacja|
| **VpnGw1, VpnGw2 i VpnGw3** | **VPN opartej na trasach**: zapasowej tuneli too30 (*), P2S, protokołu BGP, aktywny aktywny, niestandardowe zasady IPsec i IKE, współistnienie ExpressRoute lub sieć VPN |
|        |             |

(*) Możesz skonfigurować tooconnect "PolicyBasedTrafficSelectors" opartej na trasach VPN bramy (VpnGw1, VpnGw2, VpnGw3) toomultiple urządzeń lokalnych, zapory oparte na zasadach. Odwołuje się zbyt[połączenia sieci VPN bramy toomultiple lokalnego urządzenia sieci VPN opartych na zasadach przy użyciu programu PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) szczegółowe informacje.

###  <a name="resize"></a>Zmiana rozmiaru jednostek SKU bramy

1. Można zmienić rozmiar jednostek SKU, wybierając z opcji VpnGw1, VpnGw2 i VpnGw3.
2. Podczas pracy z bramą starego hello jednostki SKU, można zmienić rozmiar między podstawowa, standardowa i wysokowydajnej jednostki SKU.
2. Możesz **nie** resize z toohello jednostki SKU Basic/Standard/wysokowydajnej nowe VpnGw1/VpnGw2/VpnGw3 jednostki SKU. Należy najpierw należy [migracji](#migrate) toohello nowe jednostki SKU.

###  <a name="migrate"></a>Migrowanie z starego toohello jednostki SKU nowe jednostki SKU

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
