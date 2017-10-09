<span data-ttu-id="a723d-101">kroki Hello do tego celu zadań sieci wirtualnej na podstawie hello wartości w powitania po konfiguracji na liście odwołania.</span><span class="sxs-lookup"><span data-stu-id="a723d-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="a723d-102">Nazwy i dodatkowe ustawienia są także opisane w tej listy.</span><span class="sxs-lookup"><span data-stu-id="a723d-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="a723d-103">Nie używamy tej listy bezpośrednio w hello czynności, chociaż dodamy zmienne na podstawie wartości hello na tej liście.</span><span class="sxs-lookup"><span data-stu-id="a723d-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="a723d-104">Skopiuj toouse listy hello jako odwołanie, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="a723d-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="a723d-105">**Lista odwołań konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="a723d-105">**Configuration reference list**</span></span>

* <span data-ttu-id="a723d-106">Nazwa sieci wirtualnej = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="a723d-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="a723d-107">Przestrzeń adresową sieci wirtualnej = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a723d-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="a723d-108">Grupa zasobów = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="a723d-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="a723d-109">Podsieć1 Name = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="a723d-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="a723d-110">Przestrzeń adresowa podsieć1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="a723d-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="a723d-111">Nazwa podsieci bramy: "GatewaySubnet" zawsze nazwę podsieci bramy *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="a723d-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="a723d-112">Przestrzeń adresów podsieci bramy = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="a723d-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="a723d-113">Region = "Wschodnie stany USA"</span><span class="sxs-lookup"><span data-stu-id="a723d-113">Region = "East US"</span></span>
* <span data-ttu-id="a723d-114">Nazwa bramy = "GW"</span><span class="sxs-lookup"><span data-stu-id="a723d-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="a723d-115">Nazwa IP bramy = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="a723d-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="a723d-116">Konfigurację IP bramy Name = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="a723d-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="a723d-117">Typ: "ExpressRoute" tego typu jest wymagany dla konfiguracji usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a723d-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="a723d-118">Nazwa publicznego adresu IP bramy = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="a723d-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="a723d-119">Dodaj bramę</span><span class="sxs-lookup"><span data-stu-id="a723d-119">Add a gateway</span></span>
1. <span data-ttu-id="a723d-120">Połącz tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a723d-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="a723d-121">Deklarowanie zmiennych w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="a723d-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="a723d-122">Należy się tooedit hello próbki tooreflect hello ustawień, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="a723d-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="a723d-123">Obiekt sieci wirtualnej hello magazynu jako zmienną.</span><span class="sxs-lookup"><span data-stu-id="a723d-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="a723d-124">Dodaj tooyour podsieci bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a723d-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="a723d-125">podsieć bramy Hello musi o nazwie "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="a723d-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="a723d-126">Należy utworzyć podsieć bramy, która jest /27 lub większy (/ 26, / 25, itp.).</span><span class="sxs-lookup"><span data-stu-id="a723d-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="a723d-127">Ustaw konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="a723d-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="a723d-128">Przechowywanie podsieci bramy hello jako zmienną.</span><span class="sxs-lookup"><span data-stu-id="a723d-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="a723d-129">Prześlij żądanie dotyczące publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a723d-129">Request a public IP address.</span></span> <span data-ttu-id="a723d-130">Przed utworzeniem bramy hello wymagany jest adres IP Hello.</span><span class="sxs-lookup"><span data-stu-id="a723d-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="a723d-131">Nie można określić hello adresu IP, które mają toouse; dynamicznie został przydzielony.</span><span class="sxs-lookup"><span data-stu-id="a723d-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="a723d-132">Ten adres IP będzie używany w następnej sekcji konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="a723d-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="a723d-133">Witaj AllocationMethod muszą być dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="a723d-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="a723d-134">Utwórz hello konfiguracji dla bramy.</span><span class="sxs-lookup"><span data-stu-id="a723d-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="a723d-135">Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a723d-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="a723d-136">W tym kroku określasz hello konfiguracji, który będzie używany podczas tworzenia hello bramy.</span><span class="sxs-lookup"><span data-stu-id="a723d-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="a723d-137">Ten krok nie powoduje utworzenia obiektu bramy hello.</span><span class="sxs-lookup"><span data-stu-id="a723d-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="a723d-138">Użyj przykładowych hello poniżej toocreate konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="a723d-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="a723d-139">Utwórz bramę hello.</span><span class="sxs-lookup"><span data-stu-id="a723d-139">Create hello gateway.</span></span> <span data-ttu-id="a723d-140">W tym kroku hello **elementu GatewayType -** jest szczególnie ważne.</span><span class="sxs-lookup"><span data-stu-id="a723d-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="a723d-141">Należy użyć wartości hello **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="a723d-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="a723d-142">Po uruchomieniu tych poleceń cmdlet, hello bramy może potrwać 45 minut lub więcej toocreate.</span><span class="sxs-lookup"><span data-stu-id="a723d-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="a723d-143">Sprawdź, czy utworzono bramę hello</span><span class="sxs-lookup"><span data-stu-id="a723d-143">Verify hello gateway was created</span></span>
<span data-ttu-id="a723d-144">Użyj następującego polecenia, które utworzono tooverify, który hello bramy hello:</span><span class="sxs-lookup"><span data-stu-id="a723d-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="a723d-145">Zmień rozmiar bramy</span><span class="sxs-lookup"><span data-stu-id="a723d-145">Resize a gateway</span></span>
<span data-ttu-id="a723d-146">Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="a723d-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="a723d-147">Możesz użyć hello następujące polecenia toochange hello jednostka SKU bramy w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="a723d-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a723d-148">To polecenie nie działa dla UltraPerformance bramy.</span><span class="sxs-lookup"><span data-stu-id="a723d-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="a723d-149">toochange bramy UltraPerformance tooan bramy, najpierw usuń hello istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="a723d-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="a723d-150">najpierw usuń toodowngrade bramy sieci z bramy UltraPerformance hello UltraPerformance bramy, a następnie utwórz nową bramę.</span><span class="sxs-lookup"><span data-stu-id="a723d-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="a723d-151">Usuń bramę</span><span class="sxs-lookup"><span data-stu-id="a723d-151">Remove a gateway</span></span>
<span data-ttu-id="a723d-152">Użyj hello następujące polecenia tooremove bramy:</span><span class="sxs-lookup"><span data-stu-id="a723d-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```