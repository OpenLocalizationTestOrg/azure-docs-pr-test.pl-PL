### <span data-ttu-id="1c868-101"><a name="gwipnoconnection"></a>Aby zmodyfikować element „GatewayIpAddress” bramy sieci lokalnej — brak połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="1c868-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="1c868-102">W przypadku zmiany publicznego adresu IP urządzenia sieci VPN, z którym chcesz nawiązać połączenie, musisz zmodyfikować bramę sieci lokalnej w celu odzwierciedlenia tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="1c868-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="1c868-103">Użyj przykładu, aby zmodyfikować bramę sieci lokalnej bez połączenia bramy.</span><span class="sxs-lookup"><span data-stu-id="1c868-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="1c868-104">Podczas modyfikowania tej wartości możesz również zmodyfikować prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="1c868-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="1c868-105">Użyj istniejącej nazwy bramy sieci lokalnej w celu zastąpienia bieżących ustawień.</span><span class="sxs-lookup"><span data-stu-id="1c868-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="1c868-106">Jeśli użyjesz innej nazwy, utworzysz nową bramę sieci lokalnej, a nie zastąpisz istniejącej.</span><span class="sxs-lookup"><span data-stu-id="1c868-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="1c868-107"><a name="gwipwithconnection"></a>Aby zmodyfikować element „GatewayIpAddress” bramy sieci lokalnej — istniejące połączenie bramy</span><span class="sxs-lookup"><span data-stu-id="1c868-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="1c868-108">W przypadku zmiany publicznego adresu IP urządzenia sieci VPN, z którym chcesz nawiązać połączenie, musisz zmodyfikować bramę sieci lokalnej w celu odzwierciedlenia tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="1c868-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="1c868-109">Jeśli istnieje już połączenie bramy, musisz je najpierw usunąć.</span><span class="sxs-lookup"><span data-stu-id="1c868-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="1c868-110">Po usunięciu połączenia możesz zmodyfikować adres IP bramy i ponownie utworzyć nowe połączenie.</span><span class="sxs-lookup"><span data-stu-id="1c868-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="1c868-111">Jednocześnie możesz również zmodyfikować prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="1c868-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="1c868-112">Spowoduje to pewien przestój połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="1c868-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="1c868-113">W przypadku modyfikowania adresu IP bramy nie musisz usuwać bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="1c868-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="1c868-114">Musisz usunąć tylko połączenie.</span><span class="sxs-lookup"><span data-stu-id="1c868-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="1c868-115">Usuń połączenie.</span><span class="sxs-lookup"><span data-stu-id="1c868-115">Remove the connection.</span></span> <span data-ttu-id="1c868-116">Nazwę połączenia możesz znaleźć przy użyciu polecenia cmdlet „Get-AzureRmVirtualNetworkGatewayConnection”.</span><span class="sxs-lookup"><span data-stu-id="1c868-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="1c868-117">Zmodyfikuj wartość klasy „GatewayIpAddress”.</span><span class="sxs-lookup"><span data-stu-id="1c868-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="1c868-118">Jednocześnie możesz również zmodyfikować prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="1c868-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="1c868-119">Pamiętaj, aby użyć istniejącej nazwy bramy sieci lokalnej w celu zastąpienia bieżących ustawień.</span><span class="sxs-lookup"><span data-stu-id="1c868-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="1c868-120">Jeśli tego nie zrobisz, utworzysz nową bramę sieci lokalnej, a nie zastąpisz istniejącej.</span><span class="sxs-lookup"><span data-stu-id="1c868-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="1c868-121">Utwórz połączenie.</span><span class="sxs-lookup"><span data-stu-id="1c868-121">Create the connection.</span></span> <span data-ttu-id="1c868-122">W tym przykładzie skonfigurujemy połączenie typu IPsec.</span><span class="sxs-lookup"><span data-stu-id="1c868-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="1c868-123">Podczas ponownego tworzenia połączenia należy użyć typu połączenia, który został określony dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1c868-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="1c868-124">O dodatkowych typach połączeń można przeczytać na stronie [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) (Polecenia cmdlet programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1c868-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="1c868-125">Aby uzyskać nazwę bramy VirtualNetworkGateway, można uruchomić polecenie cmdlet „Get-AzureRmVirtualNetworkGateway”.</span><span class="sxs-lookup"><span data-stu-id="1c868-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="1c868-126">Ustaw zmienne.</span><span class="sxs-lookup"><span data-stu-id="1c868-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="1c868-127">Utwórz połączenie.</span><span class="sxs-lookup"><span data-stu-id="1c868-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```