### <span data-ttu-id="86ed4-101"><a name="gwipnoconnection"></a>Brama sieci lokalnej hello toomodify "GatewayIpAddress" — Brak połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="86ed4-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="86ed4-102">Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="86ed4-103">Użyj toomodify przykład hello bramy sieci lokalnej, która nie ma połączenia bramy.</span><span class="sxs-lookup"><span data-stu-id="86ed4-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="86ed4-104">Podczas modyfikowania tej wartości, można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="86ed4-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="86ed4-105">Należy się toouse hello istniejącą nazwę bramy sieci lokalnej w kolejności toooverwrite hello bieżące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="86ed4-106">Jeśli używasz innej nazwy, Utwórz nową bramę sieci lokalnej, zamiast zastępowanie hello istniejący.</span><span class="sxs-lookup"><span data-stu-id="86ed4-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="86ed4-107"><a name="gwipwithconnection"></a>Brama sieci lokalnej hello toomodify "GatewayIpAddress" - istniejące połączenie bramy</span><span class="sxs-lookup"><span data-stu-id="86ed4-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="86ed4-108">Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="86ed4-109">Jeśli istnieje już połączenie bramy, musisz najpierw tooremove hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="86ed4-110">Po usunięciu hello połączenia można zmodyfikować adres IP bramy hello i utworzyć nowe połączenie.</span><span class="sxs-lookup"><span data-stu-id="86ed4-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="86ed4-111">Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="86ed4-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="86ed4-112">Spowoduje to pewien przestój połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="86ed4-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="86ed4-113">Podczas modyfikowania adres IP bramy hello, nie potrzebujesz bramy sieci VPN hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="86ed4-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="86ed4-114">Wystarczy tooremove hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="86ed4-115">Usuń połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-115">Remove hello connection.</span></span> <span data-ttu-id="86ed4-116">Za pomocą polecenia cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, można znaleźć hello nazwę połączenia.</span><span class="sxs-lookup"><span data-stu-id="86ed4-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="86ed4-117">Zmień wartość "GatewayIpAddress" hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="86ed4-118">Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="86ed4-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="86ed4-119">Należy się toouse hello istniejącej nazwy sieci lokalnej bramy toooverwrite hello bieżących ustawień.</span><span class="sxs-lookup"><span data-stu-id="86ed4-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="86ed4-120">Jeśli nie istnieje, Utwórz nową bramę sieci lokalnej, zamiast zastępowanie hello istniejący.</span><span class="sxs-lookup"><span data-stu-id="86ed4-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="86ed4-121">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-121">Create hello connection.</span></span> <span data-ttu-id="86ed4-122">W tym przykładzie skonfigurujemy połączenie typu IPsec.</span><span class="sxs-lookup"><span data-stu-id="86ed4-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="86ed4-123">Podczas ponownego tworzenia połączenia, należy użyć hello typu połączenia, który jest określony dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="86ed4-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="86ed4-124">Dla typów dodatkowego połączenia, zobacz hello [polecenia cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="86ed4-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="86ed4-125">Nazwa VirtualNetworkGateway hello tooobtain, można uruchomić polecenia cmdlet "Get-AzureRmVirtualNetworkGateway" hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="86ed4-126">Ustaw zmienne hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="86ed4-127">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="86ed4-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```