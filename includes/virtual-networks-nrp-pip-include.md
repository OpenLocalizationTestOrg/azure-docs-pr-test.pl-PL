## <a name="public-ip-address"></a><span data-ttu-id="5ee3a-101">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="5ee3a-101">Public IP address</span></span>
<span data-ttu-id="5ee3a-102">Zasób publicznego adresu IP zawiera albo zastrzeżonego lub dynamiczny internetowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="5ee3a-103">Mimo że można utworzyć publiczny adres IP, jako autonomiczny obiekt, należy skojarzyć je do innego obiektu użyć adresu.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="5ee3a-104">Możesz skojarzyć publicznego adresu IP do modułu równoważenia obciążenia, bramy aplikacji lub karty Sieciowej, aby zapewnić dostęp do Internetu dla tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="5ee3a-105">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5ee3a-105">Property</span></span> | <span data-ttu-id="5ee3a-106">Opis</span><span class="sxs-lookup"><span data-stu-id="5ee3a-106">Description</span></span> | <span data-ttu-id="5ee3a-107">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="5ee3a-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ee3a-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="5ee3a-109">Określa, czy adres IP jest *statycznych* lub *dynamiczne*.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="5ee3a-110">statyczna, dynamiczne</span><span class="sxs-lookup"><span data-stu-id="5ee3a-110">static, dynamic</span></span> |
| <span data-ttu-id="5ee3a-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="5ee3a-112">Określa limit czasu bezczynności, wartość domyślna wynosi 4 minut.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="5ee3a-113">Jeśli w tej chwili nie zostanie odebrana nie więcej pakietów dla danej sesji, sesja zostanie zakończona.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="5ee3a-114">dowolna wartość od 4 do 30</span><span class="sxs-lookup"><span data-stu-id="5ee3a-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="5ee3a-115">**adres IP**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-115">**ipAddress**</span></span> |<span data-ttu-id="5ee3a-116">Adres IP przypisany do obiektu.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-116">IP address assigned to object.</span></span> <span data-ttu-id="5ee3a-117">Jest to właściwość tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-117">This is a read-only property.</span></span> |<span data-ttu-id="5ee3a-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="5ee3a-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="5ee3a-119">Ustawienia DNS</span><span class="sxs-lookup"><span data-stu-id="5ee3a-119">DNS settings</span></span>
<span data-ttu-id="5ee3a-120">Publiczne adresy IP mieć obiektu podrzędnego o nazwie **dnsSettings** zawierającą następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5ee3a-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="5ee3a-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5ee3a-121">Property</span></span> | <span data-ttu-id="5ee3a-122">Opis</span><span class="sxs-lookup"><span data-stu-id="5ee3a-122">Description</span></span> | <span data-ttu-id="5ee3a-123">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="5ee3a-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ee3a-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-124">**domainNameLabel**</span></span> |<span data-ttu-id="5ee3a-125">Hosta o nazwie używany do rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-125">Host named used for name resolution.</span></span> |<span data-ttu-id="5ee3a-126">WWW, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="5ee3a-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="5ee3a-127">**Nazwa FQDN**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-127">**fqdn**</span></span> |<span data-ttu-id="5ee3a-128">Pełna nazwa publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="5ee3a-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="5ee3a-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="5ee3a-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="5ee3a-130">**reverseFqdn**</span></span> |<span data-ttu-id="5ee3a-131">Pełna nazwa domeny jest rozpoznawana jako adres IP, który jest zarejestrowany w systemie DNS jako rekord PTR.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="5ee3a-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-132">www.contoso.com.</span></span> |

<span data-ttu-id="5ee3a-133">Przykładowe publicznego adresu IP w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="5ee3a-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="5ee3a-134">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5ee3a-134">Additional resources</span></span>
* <span data-ttu-id="5ee3a-135">Uzyskaj więcej informacji [publiczne adresy IP](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5ee3a-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="5ee3a-136">Dowiedz się więcej o [wystąpienie poziomu publiczne adresy IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5ee3a-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="5ee3a-137">Odczyt [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) publicznego adresu IP adresów.</span><span class="sxs-lookup"><span data-stu-id="5ee3a-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

