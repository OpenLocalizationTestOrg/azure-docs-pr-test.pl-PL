### <span data-ttu-id="fd69d-101"><a name="noconnection"></a>prefiksy adresów brama IP toomodify sieci lokalnej — Brak połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="fd69d-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="fd69d-102">tooadd dodatkowe prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="fd69d-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="fd69d-103">tooremove prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="fd69d-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="fd69d-104">Opuść prefiksy hello, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="fd69d-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="fd69d-105">W tym przykładzie firma Microsoft nie jest już konieczne prefiksu 20.0.0.0/24 (z hello poprzedniego przykładu), tak modyfikacjom hello bramy sieci lokalnej, z wyjątkiem tego prefiksu.</span><span class="sxs-lookup"><span data-stu-id="fd69d-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="fd69d-106"><a name="withconnection"></a>toomodify sieci lokalnej bramy prefiksów adresów IP - istniejące połączenie z bramą</span><span class="sxs-lookup"><span data-stu-id="fd69d-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="fd69d-107">Połączenie bramy i mają tooadd lub usunąć prefiksy adresów IP hello zawarte w bramie sieci lokalnej, należy najpierw hello toodo następujące kroki w kolejności.</span><span class="sxs-lookup"><span data-stu-id="fd69d-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="fd69d-108">Spowoduje to pewien przestój połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="fd69d-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="fd69d-109">Podczas modyfikowania prefiksów adresów IP, nie potrzebujesz bramy sieci VPN hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="fd69d-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="fd69d-110">Wystarczy tooremove hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="fd69d-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="fd69d-111">Usuń połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="fd69d-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="fd69d-112">Zmodyfikuj hello prefiksy adresów dla bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="fd69d-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="fd69d-113">Ustaw zmienną hello na powitania LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="fd69d-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="fd69d-114">Zmodyfikuj prefiksy hello.</span><span class="sxs-lookup"><span data-stu-id="fd69d-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="fd69d-115">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="fd69d-115">Create hello connection.</span></span> <span data-ttu-id="fd69d-116">W tym przykładzie skonfigurujemy połączenie typu IPsec.</span><span class="sxs-lookup"><span data-stu-id="fd69d-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="fd69d-117">Podczas ponownego tworzenia połączenia, należy użyć hello typu połączenia, który jest określony dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fd69d-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="fd69d-118">Dla typów dodatkowego połączenia, zobacz hello [polecenia cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="fd69d-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="fd69d-119">Ustaw zmienną hello na powitania VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="fd69d-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="fd69d-120">Utwórz połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="fd69d-120">Create hello connection.</span></span> <span data-ttu-id="fd69d-121">W tym przykładzie użyto zmiennej hello $local skonfigurowane w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="fd69d-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```