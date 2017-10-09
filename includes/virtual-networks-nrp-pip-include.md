## <a name="public-ip-address"></a><span data-ttu-id="1b776-101">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="1b776-101">Public IP address</span></span>
<span data-ttu-id="1b776-102">Zasób publicznego adresu IP zawiera albo zastrzeżonego lub dynamiczny internetowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="1b776-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="1b776-103">Mimo że można utworzyć publiczny adres IP, jako autonomiczny obiekt, należy tooassociate go tooactually obiektu tooanother Użyj adresu hello.</span><span class="sxs-lookup"><span data-stu-id="1b776-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="1b776-104">Można skojarzyć publicznego równoważenia obciążenia tooa adres IP, brama aplikacji lub kart tooprovide dostępu toothose zasobów w Internecie.</span><span class="sxs-lookup"><span data-stu-id="1b776-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="1b776-105">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1b776-105">Property</span></span> | <span data-ttu-id="1b776-106">Opis</span><span class="sxs-lookup"><span data-stu-id="1b776-106">Description</span></span> | <span data-ttu-id="1b776-107">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="1b776-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b776-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="1b776-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="1b776-109">Określa, czy adres IP hello jest *statycznych* lub *dynamiczne*.</span><span class="sxs-lookup"><span data-stu-id="1b776-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="1b776-110">statyczna, dynamiczne</span><span class="sxs-lookup"><span data-stu-id="1b776-110">static, dynamic</span></span> |
| <span data-ttu-id="1b776-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="1b776-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="1b776-112">Definiuje hello bezczynności limit czasu, wartość domyślna wynosi 4 minut.</span><span class="sxs-lookup"><span data-stu-id="1b776-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="1b776-113">Jeśli w tej chwili nie zostanie odebrana nie więcej pakietów dla danej sesji, sesja hello jest zakończona.</span><span class="sxs-lookup"><span data-stu-id="1b776-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="1b776-114">dowolna wartość od 4 do 30</span><span class="sxs-lookup"><span data-stu-id="1b776-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="1b776-115">**adres IP**</span><span class="sxs-lookup"><span data-stu-id="1b776-115">**ipAddress**</span></span> |<span data-ttu-id="1b776-116">Tooobject przypisany adres IP.</span><span class="sxs-lookup"><span data-stu-id="1b776-116">IP address assigned tooobject.</span></span> <span data-ttu-id="1b776-117">Jest to właściwość tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="1b776-117">This is a read-only property.</span></span> |<span data-ttu-id="1b776-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="1b776-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="1b776-119">Ustawienia DNS</span><span class="sxs-lookup"><span data-stu-id="1b776-119">DNS settings</span></span>
<span data-ttu-id="1b776-120">Publiczne adresy IP mieć obiektu podrzędnego o nazwie **dnsSettings** zawierający hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="1b776-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="1b776-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1b776-121">Property</span></span> | <span data-ttu-id="1b776-122">Opis</span><span class="sxs-lookup"><span data-stu-id="1b776-122">Description</span></span> | <span data-ttu-id="1b776-123">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="1b776-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b776-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="1b776-124">**domainNameLabel**</span></span> |<span data-ttu-id="1b776-125">Hosta o nazwie używany do rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="1b776-125">Host named used for name resolution.</span></span> |<span data-ttu-id="1b776-126">WWW, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="1b776-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="1b776-127">**Nazwa FQDN**</span><span class="sxs-lookup"><span data-stu-id="1b776-127">**fqdn**</span></span> |<span data-ttu-id="1b776-128">Pełna nazwa hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="1b776-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="1b776-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="1b776-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="1b776-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="1b776-130">**reverseFqdn**</span></span> |<span data-ttu-id="1b776-131">Nazwy FQDN, który jest rozpoznawany jako adres IP toohello i jest zarejestrowana w systemie DNS jako rekord PTR.</span><span class="sxs-lookup"><span data-stu-id="1b776-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="1b776-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1b776-132">www.contoso.com.</span></span> |

<span data-ttu-id="1b776-133">Przykładowe publicznego adresu IP w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="1b776-133">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="1b776-134">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1b776-134">Additional resources</span></span>
* <span data-ttu-id="1b776-135">Uzyskaj więcej informacji [publiczne adresy IP](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="1b776-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="1b776-136">Dowiedz się więcej o [wystąpienie poziomu publiczne adresy IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="1b776-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="1b776-137">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) publicznego adresu IP adresów.</span><span class="sxs-lookup"><span data-stu-id="1b776-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

