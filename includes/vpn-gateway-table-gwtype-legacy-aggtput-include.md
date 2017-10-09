Witaj poniższej tabeli przedstawiono typy bramy hello i hello szacowany łącznej przepływności przez jednostka SKU bramy. Ta tabela odnosi się toohello Resource Manager i klasycznych modeli wdrażania. 

Ceny różnych jednostek SKU bramy są różne. Aby uzyskać więcej informacji, zobacz temat [VPN Gateway — cennik](https://azure.microsoft.com/pricing/details/vpn-gateway).

Należy pamiętać, że bramy UltraPerformance hello jednostka SKU nie jest uwzględniona w tej tabeli. Informacji o hello UltraPerformance SKU znajduje się w temacie hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) dokumentacji.

|  | **Przepływność usługi VPN Gateway (1)** | **Maksymalna liczba tuneli protokołu IPsec usługi VPN Gateway (2)** | **Przepływność bramy ExpressRoute** | **Usługi VPN Gateway i ExpressRoute współistnieją** |
| --- | --- | --- | --- | --- |
| **Podstawowa jednostka SKU (3)(5)(6)** |100 Mb/s |10 |500 Mb/s (6) |Nie |
| **Standardowa jednostka SKU (4)(5)** |100 Mb/s |10 |1000 Mb/s |Tak |
| **Jednostka SKU wysokiej wydajności (4)** |200 Mb/s |30 |2000 Mb/s |Tak |


(1) Witaj przepływność sieci VPN została wstępnie oszacowana na podstawie hello pomiarów między sieciami wirtualnymi w hello tego samego regionu systemu Azure. Nie jest gwarantowanej przepustowości dla połączeń między lokalizacjami w hello Internet. Jest hello maksymalną przepustowość możliwe miary.

(2) Witaj liczba tuneli dotyczy tooRouteBased sieci VPN. Sieć VPN oparta na zasadach może obsługiwać tylko jeden tunel VPN typu lokacja-lokacja.

(3) Protokół BGP nie jest obsługiwana dla hello podstawowy SKU.

(4) Sieci VPN oparte na zasadach nie są obsługiwane w ramach tej jednostki SKU. Są obsługiwane dla hello tylko podstawowy SKU.

(5) Połączenia usługi VPN Gateway typu lokacja do lokacji (S2S) aktywne-aktywne nie są obsługiwane w ramach tej jednostki SKU. Aktywny aktywny jest obsługiwana na powitania tylko jednostki SKU wysokowydajnej.

(6) podstawowy SKU jest przestarzały do użycia z usługi ExpressRoute.
