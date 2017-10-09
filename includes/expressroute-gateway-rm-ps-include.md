kroki Hello do tego celu zadań sieci wirtualnej na podstawie hello wartości w powitania po konfiguracji na liście odwołania. Nazwy i dodatkowe ustawienia są także opisane w tej listy. Nie używamy tej listy bezpośrednio w hello czynności, chociaż dodamy zmienne na podstawie wartości hello na tej liście. Skopiuj toouse listy hello jako odwołanie, zastępując wartości hello własne.

**Lista odwołań konfiguracji**

* Nazwa sieci wirtualnej = "TestVNet"
* Przestrzeń adresową sieci wirtualnej = 192.168.0.0/16
* Grupa zasobów = "TestRG"
* Podsieć1 Name = "FrontEnd" 
* Przestrzeń adresowa podsieć1 = "192.168.1.0/24"
* Nazwa podsieci bramy: "GatewaySubnet" zawsze nazwę podsieci bramy *GatewaySubnet*.
* Przestrzeń adresów podsieci bramy = "192.168.200.0/26"
* Region = "Wschodnie stany USA"
* Nazwa bramy = "GW"
* Nazwa IP bramy = "GWIP"
* Konfigurację IP bramy Name = "gwipconf"
* Typ: "ExpressRoute" tego typu jest wymagany dla konfiguracji usługi ExpressRoute.
* Nazwa publicznego adresu IP bramy = "gwpip"

## <a name="add-a-gateway"></a>Dodaj bramę
1. Połącz tooyour subskrypcji platformy Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Deklarowanie zmiennych w tym ćwiczeniu. Należy się tooedit hello próbki tooreflect hello ustawień, które mają toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Obiekt sieci wirtualnej hello magazynu jako zmienną.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Dodaj tooyour podsieci bramy sieci wirtualnej. podsieć bramy Hello musi o nazwie "GatewaySubnet". Należy utworzyć podsieć bramy, która jest /27 lub większy (/ 26, / 25, itp.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Ustaw konfigurację hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Przechowywanie podsieci bramy hello jako zmienną.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Prześlij żądanie dotyczące publicznego adresu IP. Przed utworzeniem bramy hello wymagany jest adres IP Hello. Nie można określić hello adresu IP, które mają toouse; dynamicznie został przydzielony. Ten adres IP będzie używany w następnej sekcji konfiguracji hello. Witaj AllocationMethod muszą być dynamiczne.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Utwórz hello konfiguracji dla bramy. Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP. W tym kroku określasz hello konfiguracji, który będzie używany podczas tworzenia hello bramy. Ten krok nie powoduje utworzenia obiektu bramy hello. Użyj przykładowych hello poniżej toocreate konfigurację bramy.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Utwórz bramę hello. W tym kroku hello **elementu GatewayType -** jest szczególnie ważne. Należy użyć wartości hello **ExpressRoute**. Po uruchomieniu tych poleceń cmdlet, hello bramy może potrwać 45 minut lub więcej toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Sprawdź, czy utworzono bramę hello
Użyj następującego polecenia, które utworzono tooverify, który hello bramy hello:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Zmień rozmiar bramy
Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Możesz użyć hello następujące polecenia toochange hello jednostka SKU bramy w dowolnym momencie.

> [!IMPORTANT]
> To polecenie nie działa dla UltraPerformance bramy. toochange bramy UltraPerformance tooan bramy, najpierw usuń hello istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance. najpierw usuń toodowngrade bramy sieci z bramy UltraPerformance hello UltraPerformance bramy, a następnie utwórz nową bramę.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Usuń bramę
Użyj hello następujące polecenia tooremove bramy:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```