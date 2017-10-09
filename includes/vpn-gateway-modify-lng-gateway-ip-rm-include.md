### <a name="gwipnoconnection"></a>Brama sieci lokalnej hello toomodify "GatewayIpAddress" — Brak połączenia bramy

Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia. Użyj toomodify przykład hello bramy sieci lokalnej, która nie ma połączenia bramy.

Podczas modyfikowania tej wartości, można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie. Należy się toouse hello istniejącą nazwę bramy sieci lokalnej w kolejności toooverwrite hello bieżące ustawienia. Jeśli używasz innej nazwy, Utwórz nową bramę sieci lokalnej, zamiast zastępowanie hello istniejący.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>Brama sieci lokalnej hello toomodify "GatewayIpAddress" - istniejące połączenie bramy

Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia. Jeśli istnieje już połączenie bramy, musisz najpierw tooremove hello połączenia. Po usunięciu hello połączenia można zmodyfikować adres IP bramy hello i utworzyć nowe połączenie. Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie. Spowoduje to pewien przestój połączenia sieci VPN. Podczas modyfikowania adres IP bramy hello, nie potrzebujesz bramy sieci VPN hello toodelete. Wystarczy tooremove hello połączenia.
 

1. Usuń połączenie hello. Za pomocą polecenia cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, można znaleźć hello nazwę połączenia.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Zmień wartość "GatewayIpAddress" hello. Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie. Należy się toouse hello istniejącej nazwy sieci lokalnej bramy toooverwrite hello bieżących ustawień. Jeśli nie istnieje, Utwórz nową bramę sieci lokalnej, zamiast zastępowanie hello istniejący.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Utwórz połączenie hello. W tym przykładzie skonfigurujemy połączenie typu IPsec. Podczas ponownego tworzenia połączenia, należy użyć hello typu połączenia, który jest określony dla danej konfiguracji. Dla typów dodatkowego połączenia, zobacz hello [polecenia cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) strony.  Nazwa VirtualNetworkGateway hello tooobtain, można uruchomić polecenia cmdlet "Get-AzureRmVirtualNetworkGateway" hello.
   
    Ustaw zmienne hello.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Utwórz połączenie hello.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```