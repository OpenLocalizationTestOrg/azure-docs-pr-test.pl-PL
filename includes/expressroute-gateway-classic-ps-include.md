Należy utworzyć sieć wirtualną i podsieć bramy, przed rozpoczęciem pracy poniższe zadania.

> [!NOTE]
> Poniższe przykłady dotyczą S2S/ExpressRoute współistnieją konfiguracje.
> Aby uzyskać więcej informacji na temat pracy z bram w konfiguracji coexist, zobacz [konfiguracji współistnienia połączeń](../articles/expressroute/expressroute-howto-coexist-classic.md#gw)

## <a name="add-a-gateway"></a>Dodaj bramę

Aby utworzyć bramę, należy użyć poniższego polecenia. Należy zastąpić wszystkie własne wartości.

```powershell
New-AzureVNetGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType DynamicRouting -GatewaySKU  Standard
```

## <a name="verify-the-gateway-was-created"></a>Sprawdź, czy utworzono bramę

Użyj poniższego polecenia, aby sprawdzić, czy utworzono bramę. To polecenie pobiera również identyfikator bramy, który jest wymagany dla innych operacji.

```powershell
Get-AzureVNetGateway
```

## <a name="resize-a-gateway"></a>Zmień rozmiar bramy

Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Następujące polecenie służy do zmiany jednostka SKU bramy w dowolnym momencie.

> [!IMPORTANT]
> To polecenie nie działa dla UltraPerformance bramy. Aby zmienić bramę do bramy UltraPerformance, najpierw usuń istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance. Na starszą wersję bramy sieci z bramy UltraPerformance, najpierw usuń UltraPerformance bramy, a następnie utwórz nową bramę. 
>
>

```powershell
Resize-AzureVNetGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

## <a name="remove-a-gateway"></a>Usuń bramę

Użyj poniższego polecenia, aby usunąć bramę

```powershell
Remove-AzureVnetGateway -GatewayId <Gateway ID>
```