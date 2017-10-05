# Omówienie
## [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md)
## [VPN Gateway — często zadawane pytania](vpn-gateway-vpn-faq.md)
## [Limity usług i subskrypcji](../azure-subscription-service-limits.md?toc=%2fazure%2fvpn-gateway%2ftoc.json)

# Wprowadzenie
## [Planowanie i projektowanie dla usługi VPN Gateway](vpn-gateway-plan-design.md)
## [Informacje na temat ustawień usługi VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md)
## [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md)
## [Informacje o wymaganiach kryptograficznych](vpn-gateway-about-compliance-crypto.md)
## [Informacje o protokole BGP i usłudze VPN Gateway](vpn-gateway-bgp-overview.md)
## [Informacje o połączeniach z elementami o wysokiej dostępności](vpn-gateway-highlyavailable.md)

# Instrukcje
## Konfigurowanie połączenia lokacja-lokacja
### [Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
### [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
### [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
### [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
## Konfigurowanie połączenia punkt-lokacja
### [Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
### [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
### [Portal Azure (klasyczny)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
### Generowanie certyfikatów z podpisem własnym dla połączeń punkt-lokacja
#### [PowerShell](vpn-gateway-certificates-point-to-site.md)
#### [Makecert](vpn-gateway-certificates-point-to-site-makecert.md)
## Konfigurowanie połączenia sieć wirtualna-sieć wirtualna
### [Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
### [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
### [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-vnet-vnet-cli.md)
### [Portal Azure (klasyczny)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
## Konfigurowanie połączenia sieć wirtualna-sieć wirtualna między modelami wdrażania
### [Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
### [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
## Konfigurowanie połączeń między lokacjami i współistniejących połączeń usługi ExpressRoute
### [PowerShell](../expressroute/expressroute-howto-coexist-resource-manager.md?toc=%2fazure%2fvpn-gateway%2ftoc.json)
## Konfigurowanie wielu połączeń typu lokacja-lokacja
### [Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
### [PowerShell (klasyczny)](vpn-gateway-multi-site.md)
## Łączenie wielu urządzeń sieci VPN opartej na zasadach
### [PowerShell](vpn-gateway-connect-multiple-policybased-rm-ps.md)
## Konfigurowanie zasad IPsec/IKE dla połączeń
### [PowerShell](vpn-gateway-ipsecikepolicy-rm-powershell.md)
## Konfigurowanie połączeń typu aktywne-aktywne o wysokiej dostępności
### [PowerShell](vpn-gateway-activeactive-rm-powershell.md)
## Konfigurowanie protokołu BGP dla bramy sieci VPN
### [PowerShell](vpn-gateway-bgp-resource-manager-ps.md)
## Konfigurowanie wymuszonego tunelowania
### [PowerShell](vpn-gateway-forced-tunneling-rm.md)
### [PowerShell (klasyczny)](vpn-gateway-about-forced-tunneling.md)
## Modyfikowanie ustawień lokalnej bramy sieci
### [Witryna Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
### [PowerShell](vpn-gateway-modify-local-network-gateway.md)
### [Interfejs wiersza polecenia platformy Azure](vpn-gateway-modify-local-network-gateway-cli.md)
## [Weryfikowanie połączenia z bramą VPN Gateway](vpn-gateway-verify-connection-resource-manager.md)
## [Resetowanie bramy VPN Gateway](vpn-gateway-resetgw-classic.md)
## Usuwanie bramy VPN Gateway
### [Witryna Azure Portal](vpn-gateway-delete-vnet-gateway-portal.md)
### [PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
### [PowerShell (klasyczny)](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
## [Jednostki SKU bramy (starsze)](vpn-gateway-about-skus-legacy.md)
## Konfigurowanie urządzeń sieci VPN innych firm
### [Overview & Azure configuration (Omówienie i konfiguracja platformy Azure)](vpn-gateway-3rdparty-device-config-overview.md)
### [Sample: Cisco ASA device (IKEv2/no BGP) (Przykład: Urządzenie ASA Cisco [IKEv2/bez protokołu BGP])](vpn-gateway-3rdparty-device-config-cisco-asa.md)
## Rozwiązywanie problemów
### [Sprawdzanie przepustowości sieci VPN do sieci wirtualnej](vpn-gateway-validate-throughput-to-vnet.md)
### [Ustawienia sieci VPN lub urządzenia zapory sugerowane przez społeczność](vpn-gateway-third-party-settings.md)
### [Problem z połączeniem punkt-lokacja](vpn-gateway-troubleshoot-vpn-point-to-site-connection-problems.md)
### [Połączenie lokacja-lokacja jest sporadycznie rozłączane](vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently.md)
### [Nie można nawiązać połączenia lokacja-lokacja](vpn-gateway-troubleshoot-site-to-site-cannot-connect.md) 

# Dokumentacja
## [PowerShell](/powershell/module/azurerm.network/?view=azurermps-4.0.0#vpn)
## [PowerShell (klasyczny)](/powershell/module/azure/?view=azuresmps-3.7.0#networking)
## [REST](/rest/api/network/virtualnetworkgateways)
## [REST (klasyczny)](https://msdn.microsoft.com/library/jj154113)
## [Interfejs wiersza polecenia platformy Azure](/cli/azure/network/vnet-gateway)

# Powiązane
## [Virtual Network](/azure/virtual-network/)
## [Application Gateway](/azure/application-gateway/)
## [System DNS platformy Azure](/azure/dns/)
## [Traffic Manager](/azure/traffic-manager/)
## [Load Balancer](/azure/load-balancer/)
## [ExpressRoute](/azure/expressroute/)

# Zasoby
## [Harmonogram działania dla platformy Azure](https://azure.microsoft.com/roadmap/?category=networking)
## [Blog](https://azure.microsoft.com/blog/topics/networking)
## [Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [Cennik](https://azure.microsoft.com/pricing/details/vpn-gateway)
## [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/)
## [Umowa SLA](https://azure.microsoft.com/support/legal/sla)
## [Filmy wideo](https://azure.microsoft.com/documentation/videos/index/?services=vpn-gateway)
