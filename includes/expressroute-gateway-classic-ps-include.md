Należy utworzyć sieć wirtualną i podsieć bramy, przed rozpoczęciem pracy hello następujące zadania. Zobacz artykuł hello [skonfigurować sieć wirtualną przy użyciu klasycznego portalu hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) Aby uzyskać więcej informacji.   

## <a name="add-a-gateway"></a>Dodaj bramę
Polecenie hello poniżej toocreate bramy. Można toosubstitute się, że wszystkie własne wartości.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Sprawdź, czy utworzono bramę hello
Użyj polecenia hello poniżej tooverify, który hello bramy został utworzony. To polecenie pobiera również hello identyfikator bramy, który należy innych operacji.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Zmień rozmiar bramy
Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Możesz użyć hello następujące polecenia toochange hello jednostka SKU bramy w dowolnym momencie.

> [!IMPORTANT]
> To polecenie nie działa dla UltraPerformance bramy. toochange bramy UltraPerformance tooan bramy, najpierw usuń hello istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance. najpierw usuń toodowngrade bramy sieci z bramy UltraPerformance hello UltraPerformance bramy, a następnie utwórz nową bramę. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Usuń bramę
Użyj polecenia hello poniżej tooremove bramy

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>