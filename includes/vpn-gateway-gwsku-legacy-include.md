Brama sieci VPN (stare) starszych Hello są jednostki SKU:

* Podstawowa
* Standardowa (Standard)
* Wysoka wydajność (HighPerformance)

Brama sieci VPN nie używa jednostka SKU bramy UltraPerformance hello. Informacji o hello UltraPerformance SKU znajduje się w temacie hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) dokumentacji.

Podczas pracy z hello starszej wersji produktu, rozważ następujące hello:

* Jeśli chcesz toouse typu PolicyBased sieci VPN, należy użyć hello podstawowy SKU. Sieć VPN PolicyBased (nazywana wcześniej routingiem statycznym) nie jest obsługiwana w żadnych innych jednostkach SKU.
* Protokół BGP nie jest obsługiwany na powitania podstawowy SKU.
* Brama sieci VPN ExpressRoute współistnieją konfiguracje nie są obsługiwane na powitania podstawowy SKU.
* Na powitania tylko jednostki SKU wysokowydajnej można skonfigurować połączenia bramy sieci VPN S2S aktywny aktywny.
