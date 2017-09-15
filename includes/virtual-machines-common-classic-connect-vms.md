

![Maszyny wirtualne w autonomicznej usługi w chmurze](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="6dcbe-102">Jeśli w sieci wirtualnej maszyn wirtualnych, można zdecydować, zestawy dostępności i równoważenia obciążenia ile ma być używany dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want to use for load balancing and availability sets.</span></span> <span data-ttu-id="6dcbe-103">Ponadto można organizować maszyn wirtualnych w podsieciach w taki sam sposób jak sieci lokalnej, a także połączyć sieć wirtualną do sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-103">Additionally, you can organize the virtual machines on subnets in the same way as your on-premises network and connect the virtual network to your on-premises network.</span></span> <span data-ttu-id="6dcbe-104">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="6dcbe-104">Here's an example:</span></span>

![Maszyny wirtualne w sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="6dcbe-106">Sieci wirtualne są zalecanym sposobem Podłączanie maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-106">Virtual networks are the recommended way to connect virtual machines in Azure.</span></span> <span data-ttu-id="6dcbe-107">Najlepszym rozwiązaniem jest skonfigurowanie każdej warstwy aplikacji w usłudze w chmurze oddzielne.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-107">The best practice is to configure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="6dcbe-108">Jednak może być konieczne łączenie niektórych maszyn wirtualnych z warstwami innej aplikacji w tej samej usługi w chmurze ma pozostać w ciągu maksymalnie 200 usługi w chmurze na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-108">However, you may need to combine some virtual machines from different application tiers into the same cloud service to remain within the maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="6dcbe-109">Aby przejrzeć to i inne ograniczenia, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="6dcbe-109">To review this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="6dcbe-110">Połączenie maszyn wirtualnych w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6dcbe-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="6dcbe-111">Umożliwia podłączanie maszyn wirtualnych w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="6dcbe-111">To connect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="6dcbe-112">Utwórz sieć wirtualną w [portalu Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) i określ "classic deployment".</span><span class="sxs-lookup"><span data-stu-id="6dcbe-112">Create the virtual network in the [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="6dcbe-113">Utwórz zbiór usługi w chmurze dla danego wdrożenia w celu odzwierciedlenia projektu dla zestawów dostępności i równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-113">Create the set of cloud services for your deployment to reflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="6dcbe-114">W portalu Azure, kliknij przycisk **nowe > obliczenia > Usługa w chmurze** dla każdej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-114">In the Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="6dcbe-115">W trakcie wypełniania szczegóły usługi chmury, wybierz taki sam _grupy zasobów_ używane z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-115">As you fill out the cloud service details, choose the same _resource group_ used with the virtual network.</span></span>

3. <span data-ttu-id="6dcbe-116">Aby utworzyć każdej nowej maszyny wirtualnej, kliknij przycisk **nowy > obliczeniowe**, następnie wybierz odpowiedni obraz maszyny Wirtualnej z **wyróżnionych aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-116">To create each new virtual machine, click **New > Compute**, then select the appropriate VM image from the **Featured apps**.</span></span>

  <span data-ttu-id="6dcbe-117">W maszynie Wirtualnej **podstawy** bloku, wybierz taki sam _grupy zasobów_ używane z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-117">In the VM **Basics** blade, choose the same _resource group_ used with the virtual network.</span></span>

  ![Blok podstawowych ustawień maszyny Wirtualnej przy użyciu sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="6dcbe-119">W trakcie wypełniania maszyny Wirtualnej **ustawienia**, wybierz poprawny _usługi w chmurze_ lub _sieci wirtualnej_ dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-119">As you fill out the VM **Settings**, choose the correct _Cloud service_ or _virtual network_ for the VM.</span></span>

  <span data-ttu-id="6dcbe-120">Azure wybierze inny element zależności.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-120">Azure will select the other item based on your selection.</span></span>

  ![Blok ustawień maszyny Wirtualnej przy użyciu sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="6dcbe-122">Połączenie maszyn wirtualnych w autonomicznej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6dcbe-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="6dcbe-123">Umożliwia podłączanie maszyn wirtualnych w autonomicznej usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="6dcbe-123">To connect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="6dcbe-124">Tworzenie usługi w chmurze w [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dcbe-124">Create the cloud service in the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="6dcbe-125">Kliknij przycisk **nowe > obliczenia > Usługa w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="6dcbe-126">Lub po utworzeniu pierwszej maszyny wirtualnej można utworzyć usługi w chmurze dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-126">Or, you can create the cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="6dcbe-127">Podczas tworzenia maszyn wirtualnych, należy wybrać tej samej grupy zasobów, które są używane z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-127">When you create the virtual machines, choose the same resource group used with the cloud service.</span></span>

  ![Dodaj maszynę wirtualną do istniejącej usługi w chmurze](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="6dcbe-129">W trakcie wypełniania szczegóły maszyny Wirtualnej, wybierz nazwę utworzonego w pierwszym kroku usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6dcbe-129">As you fill out the VM details, choose the name of cloud service created in the first step.</span></span>

  ![Wybierając usługę chmury dla maszyny wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
