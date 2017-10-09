### <a name="noconnection"></a>prefiksy adresów brama IP toomodify sieci lokalnej — Brak połączenia bramy

tooadd dodatkowe prefiksy adresów:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove prefiksy adresów:<br>
Opuść prefiksy hello, które nie są już potrzebne. W tym przykładzie firma Microsoft nie jest już konieczne prefiksu 20.0.0.0/24 (z hello poprzedniego przykładu), tak modyfikacjom hello bramy sieci lokalnej, z wyjątkiem tego prefiksu.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify sieci lokalnej bramy prefiksów adresów IP - istniejące połączenie z bramą

Połączenie bramy i mają tooadd lub usunąć prefiksy adresów IP hello zawarte w bramie sieci lokalnej, należy najpierw hello toodo następujące kroki w kolejności. Spowoduje to pewien przestój połączenia sieci VPN. Podczas modyfikowania prefiksów adresów IP, nie potrzebujesz bramy sieci VPN hello toodelete. Wystarczy tooremove hello połączenia.


1. Usuń połączenie hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Zmodyfikuj hello prefiksy adresów dla bramy sieci lokalnej.
   
  Ustaw zmienną hello na powitania LocalNetworkGateway.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Zmodyfikuj prefiksy hello.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Utwórz połączenie hello. W tym przykładzie skonfigurujemy połączenie typu IPsec. Podczas ponownego tworzenia połączenia, należy użyć hello typu połączenia, który jest określony dla danej konfiguracji. Dla typów dodatkowego połączenia, zobacz hello [polecenia cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) strony.
   
  Ustaw zmienną hello na powitania VirtualNetworkGateway.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Utwórz połączenie hello. W tym przykładzie użyto zmiennej hello $local skonfigurowane w kroku 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```