# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="ee0ed-101">Często zadawane pytania dotyczące dyski maszyny Wirtualnej Azure IaaS i zarządzane i niezarządzane — wersja premium</span><span class="sxs-lookup"><span data-stu-id="ee0ed-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="ee0ed-102">Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące dysków zarządzanych Azure i usługa Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="ee0ed-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="ee0ed-103">Managed Disks</span></span>

<span data-ttu-id="ee0ed-104">**Co to jest Azure zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="ee0ed-105">Dyski zarządzane jest funkcja, która ułatwia zarządzanie dyskami dla maszyn wirtualnych IaaS platformy Azure dzięki obsłudze Zarządzanie kontem magazynu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="ee0ed-106">Aby uzyskać więcej informacji, zobacz [omówienie dysków zarządzanych](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="ee0ed-107">**Jeśli utworzyć standardowych dysków zarządzanych z istniejącego dysku VHD, 80 GB, ile będzie tego koszt mnie?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="ee0ed-108">Standardowa dysków zarządzanych utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako dalej rozmiar dostępnych dysków w warstwie standardowa, który jest dyskiem s10 w warstwie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="ee0ed-109">Są naliczane opłaty zgodnie z s10 w warstwie cenowej dysku.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="ee0ed-110">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ee0ed-111">**Czy istnieją kosztów transakcji dla standardowych dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="ee0ed-112">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-112">Yes.</span></span> <span data-ttu-id="ee0ed-113">W przypadku naliczona opłata za każdą transakcję.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-113">You're charged for each transaction.</span></span> <span data-ttu-id="ee0ed-114">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ee0ed-115">**Dla standardowych dysków zarządzanych I obciążymy rzeczywisty rozmiar danych na dysku lub elastycznie pojemność dysku?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="ee0ed-116">Są naliczane opłaty oparte na elastycznie pojemność dysku.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="ee0ed-117">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ee0ed-118">**Jak jest inny niż dyski niezarządzane cennik dysków zarządzanych w warstwie premium?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="ee0ed-119">Cennik dysków zarządzanych w warstwie premium jest taka sama jak dyski premium niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="ee0ed-120">**Można zmienić typu (standardowy lub Premium) konta magazynu z dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="ee0ed-121">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-121">Yes.</span></span> <span data-ttu-id="ee0ed-122">Można zmienić typu konta magazynu dysków zarządzanych za pomocą portalu Azure, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="ee0ed-123">**Czy istnieje sposób, aby I skopiuj lub wyeksportować dysków zarządzanych do konta magazynu prywatnej?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="ee0ed-124">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-124">Yes.</span></span> <span data-ttu-id="ee0ed-125">Dyski zarządzane można wyeksportować za pomocą portalu Azure, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="ee0ed-126">**Aby utworzyć dysków zarządzanych za pomocą innej subskrypcji można użyć pliku VHD na koncie magazynu platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="ee0ed-127">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-127">No.</span></span>

<span data-ttu-id="ee0ed-128">**Aby utworzyć dysków zarządzanych w innym regionie można użyć pliku VHD na koncie magazynu platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="ee0ed-129">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-129">No.</span></span>

<span data-ttu-id="ee0ed-130">**Czy istnieją jakiekolwiek ograniczenia skali dla klientów korzystających z zarządzanego dyski?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="ee0ed-131">Dyski zarządzane eliminuje limity skojarzonego z kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="ee0ed-132">Jednak liczbę zarządzanych dysków dla subskrypcji jest ograniczona do 2000 domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="ee0ed-133">Możesz wywołać pomocy technicznej, aby zwiększyć ten numer.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-133">You can call support to increase this number.</span></span>

<span data-ttu-id="ee0ed-134">**Czy można wykonać przyrostowej migawki dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="ee0ed-135">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-135">No.</span></span> <span data-ttu-id="ee0ed-136">Pełną kopię dysków zarządzanych sprawia, że bieżąca funkcja migawki.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="ee0ed-137">Jednak firma Microsoft planuje obsługuje przyrostowe migawek w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="ee0ed-138">**Maszyny wirtualne w zestawie dostępności może zawierać kombinację dysków zarządzane i niezarządzane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="ee0ed-139">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-139">No.</span></span> <span data-ttu-id="ee0ed-140">Maszyn wirtualnych w zestawie dostępności muszą używać wszystkich zarządzanych dysków lub wszystkie dyski niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="ee0ed-141">Podczas tworzenia zestawu dostępności można wybrać typu dysków, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="ee0ed-142">**Jest domyślną opcją w portalu Azure zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="ee0ed-143">Aktualnie nie ale stanie się domyślnie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="ee0ed-144">**Można utworzyć pusty dysk zarządzany?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="ee0ed-145">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-145">Yes.</span></span> <span data-ttu-id="ee0ed-146">Możesz utworzyć pusty dysk.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-146">You can create an empty disk.</span></span> <span data-ttu-id="ee0ed-147">Dysk zarządzany można tworzyć niezależnie od maszyny Wirtualnej, na przykład bez dołączeniu go do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="ee0ed-148">**Co to liczba domen błędów obsługiwanych dostępności ustawiono używającym dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="ee0ed-149">W zależności od regionu, w którym znajduje się zestaw dostępności, który używa dysków zarządzanych liczba domen błędów obsługiwanych jest 2 lub 3.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="ee0ed-150">**Jak jest to konto magazynu w warstwie standardowa dla diagnostyki Konfigurowanie?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="ee0ed-151">Skonfiguruj konto magazynu prywatne dla diagnostyki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="ee0ed-152">W przyszłości firma Microsoft planuje także przełącznik diagnostyki do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="ee0ed-153">**Jakiego rodzaju obsługi kontroli dostępu opartej na rolach jest dostępna dla dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="ee0ed-154">Zarządzane dysków obsługuje trzy kluczowe domyślne role:</span><span class="sxs-lookup"><span data-stu-id="ee0ed-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="ee0ed-155">Właściciel: Mogą zarządzać wszystkim łącznie z dostępem</span><span class="sxs-lookup"><span data-stu-id="ee0ed-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="ee0ed-156">Współautor: Mogą zarządzać wszystkim poza dostępem</span><span class="sxs-lookup"><span data-stu-id="ee0ed-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="ee0ed-157">Czytnik: Można przeglądać wszystko, ale nie można wprowadzić zmian</span><span class="sxs-lookup"><span data-stu-id="ee0ed-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="ee0ed-158">**Czy istnieje sposób, aby I skopiuj lub wyeksportować dysków zarządzanych do konta magazynu prywatnej?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="ee0ed-159">Można pobrać sygnatury dostępu współdzielonego tylko do odczytu identyfikatora URI dla dysków zarządzanych i go użyć do kopiowania zawartości do magazynu konta lub lokalnego magazynu prywatnych.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="ee0ed-160">**Można utworzyć kopię dysku zarządzanego?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="ee0ed-161">Klienci mogą migawki dysków zarządzanych, a następnie użyj migawki do tworzenia dysków zarządzanych w innym.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="ee0ed-162">**Niezarządzane dyski nadal są obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="ee0ed-163">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-163">Yes.</span></span> <span data-ttu-id="ee0ed-164">Firma Microsoft obsługuje dyski niezarządzane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="ee0ed-165">Zalecamy dysków zarządzanych dla nowych obciążeń, a migracja bieżącego obciążeń do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="ee0ed-166">**Jeśli I Utwórz dysk 128 GB i dopiero potem zwiększyć rozmiar 130 GB I obciążymy dla następnego rozmiar dysku (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="ee0ed-167">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-167">Yes.</span></span>

<span data-ttu-id="ee0ed-168">**Magazyn lokalnie nadmiarowy, Magazyn geograficznie nadmiarowy, można utworzyć i dyskach zarządzanych przez Magazyn strefowo nadmiarowy?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="ee0ed-169">Dyskach zarządzanych platformy Azure obsługuje obecnie tylko lokalnie nadmiarowego magazynu zarządzane dyski.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="ee0ed-170">**Można zmniejszyć lub downsize dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="ee0ed-171">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-171">No.</span></span> <span data-ttu-id="ee0ed-172">Ta funkcja nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="ee0ed-173">**Właściwość Nazwa komputera można zmienić po specjalistycznej (nie utworzone przy użyciu narzędzia przygotowywania systemu lub uogólniony) dysku systemu operacyjnego jest używany do udostępnienia maszyny Wirtualnej?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="ee0ed-174">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-174">No.</span></span> <span data-ttu-id="ee0ed-175">Nie można zaktualizować właściwości Nazwa komputera.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-175">You can't update the computer name property.</span></span> <span data-ttu-id="ee0ed-176">Nowa maszyna wirtualna dziedziczy z elementu nadrzędnego maszyny Wirtualnej, który został użyty do utworzenia dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="ee0ed-177">**Gdzie można znaleźć przykładowych szablonów usługi Azure Resource Manager do tworzenia maszyn wirtualnych z dyskami zarządzanych**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="ee0ed-178">Lista szablonów przy użyciu dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="ee0ed-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="ee0ed-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="ee0ed-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="ee0ed-180">Zarządzane dysków i szyfrowanie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="ee0ed-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="ee0ed-181">**Jest szyfrowanie usługi Magazyn Azure domyślnie podczas tworzenia dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="ee0ed-182">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-182">Yes.</span></span>

<span data-ttu-id="ee0ed-183">**Kto zarządza klucze szyfrowania?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="ee0ed-184">Firma Microsoft zarządza kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="ee0ed-185">**Do zarządzanych dysków można wyłączyć szyfrowanie usługi Magazyn?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="ee0ed-186">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-186">No.</span></span>

<span data-ttu-id="ee0ed-187">**Jest szyfrowanie usługi Magazyn dostępna tylko w określonych regionach?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="ee0ed-188">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-188">No.</span></span> <span data-ttu-id="ee0ed-189">Jest dostępna we wszystkich regionach, gdzie dostępna jest opcja dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="ee0ed-190">Dyski zarządzane jest dostępna we wszystkich regionach publicznego i Niemczech.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="ee0ed-191">**Jak można sprawdzić w przypadku zarządzanych dysku są szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="ee0ed-192">Można ustalić czas utworzenia dysków zarządzanych w portalu Azure, interfejsu wiersza polecenia Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="ee0ed-193">Gdy czas po 9 czerwca 2017 dysku są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="ee0ed-194">**Jak można zaszyfrować Moje istniejących dysków, które zostały utworzone przed 10 czerwca 2017 r.**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="ee0ed-195">Począwszy od 10 czerwca 2017 nowych danych istniejących dysków zarządzanych jest szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="ee0ed-196">Możemy również planowania szyfrowania istniejących danych i szyfrowanie nastąpi asynchronicznie w tle.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="ee0ed-197">Jeśli musi teraz zaszyfrować dane, należy utworzyć kopię dysku.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="ee0ed-198">Nowe dyski zostaną zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="ee0ed-199">Kopiowanie dysków zarządzanych przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ee0ed-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="ee0ed-200">Kopiowanie dysków zarządzanych za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee0ed-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="ee0ed-201">**Są zarządzane migawki i obrazy szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="ee0ed-202">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-202">Yes.</span></span> <span data-ttu-id="ee0ed-203">Wszystkie zarządzane migawki i obrazy utworzone po 9 czerwca 2017 r są szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="ee0ed-204">**Czy mogę przekonwertować maszyny wirtualne z dyskami niezarządzane, które znajdują się na kontach magazynu, które są lub wcześniej były szyfrowane do zarządzanych dysków**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="ee0ed-205">Tak</span><span class="sxs-lookup"><span data-stu-id="ee0ed-205">Yes</span></span>

<span data-ttu-id="ee0ed-206">**Wyeksportowane wirtualnego dysku twardego z zarządzanego dysku lub migawka także będą zaszyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="ee0ed-207">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-207">No.</span></span> <span data-ttu-id="ee0ed-208">Ale jeśli możesz wyeksportować do konta magazynu zaszyfrowanego dysku VHD z zaszyfrowanego zarządzane dysku lub migawki, a następnie jest on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="ee0ed-209">Dyski Premium: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="ee0ed-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="ee0ed-210">**Jeśli maszyna wirtualna używa rozmiar serii, która obsługuje magazyn w warstwie Premium, takich jak DSv2, można dołączyć zarówno premium i dyski standardowe danych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="ee0ed-211">Tak.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-211">Yes.</span></span>

<span data-ttu-id="ee0ed-212">**Do rozmiaru serii, która nie obsługuje usługi Premium Storage, takich jak seria D, Dv2, G lub F można podłączyć zarówno premium i dyski standardowe danych?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="ee0ed-213">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-213">No.</span></span> <span data-ttu-id="ee0ed-214">Tylko dyski standardowe danych można dołączyć do maszyn wirtualnych, które nie używają serii rozmiar, który obsługuje magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="ee0ed-215">**Jeśli dysk danych — warstwa premium można utworzyć z istniejącego dysku VHD, który był 80 GB, ile będzie tego koszt?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="ee0ed-216">Dysk z danymi premium utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako rozmiaru dysku premium dostępne dalej, który jest dyskiem P10.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="ee0ed-217">Są naliczane opłaty zgodnie z cennik P10 dysku.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="ee0ed-218">**Czy istnieją koszty transakcji do użycia magazyn w warstwie Premium?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="ee0ed-219">Brak koszt stały rozmiar każdego dysku, które pojawia się z określonym limity udostępnionym IOPS i przepustowość.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="ee0ed-220">Inne koszty są przepustowości wychodzącej i pojemność migawki, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="ee0ed-221">Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ee0ed-222">**Jakie są limity dla IOPS i przepływność, którą można pobrać z pamięci podręcznej dysku?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="ee0ed-223">Łączne limity dla pamięci podręcznej i lokalny dysk SSD dla serii DS są 4000 IOPS na podstawowe i 33 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="ee0ed-224">Serii GS oferuje 5000 IOPS na podstawowe i 50 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="ee0ed-225">**Lokalny dysk SSD jest obsługiwana dla maszyny Wirtualnej, zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="ee0ed-226">Lokalny dysk SSD jest tymczasowego magazynu, który jest dołączony do maszyny Wirtualnej dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="ee0ed-227">Jest nie żadnymi dodatkowymi kosztami dla tego magazynu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="ee0ed-228">Firma Microsoft zaleca, aby używać tego lokalny dysk SSD do przechowywania danych aplikacji, ponieważ nie jest on utrwalane w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="ee0ed-229">**Czy istnieją żadnych skutków PRZYCINANIE do użytku na dyski premium?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="ee0ed-230">Nie ma żadnych wadą interfejsu użyciem PRZYCINANIE na dyskach platformy Azure w warstwie premium albo lub dyski standardowe.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="ee0ed-231">Nowy rozmiar dysku: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="ee0ed-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="ee0ed-232">**Co to jest największy rozmiar dysku systemu operacyjnego i dysków z danymi obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="ee0ed-233">Typ partycji, który Azure obsługuje dla dysku systemu operacyjnego jest główny rekord rozruchowy (MBR).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="ee0ed-234">Obsługuje format MBR dysk rozmiar do 2 TB.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="ee0ed-235">Największy rozmiar, który Azure obsługuje dla dysku systemu operacyjnego jest 2 TB.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="ee0ed-236">Azure obsługuje do 4 TB dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="ee0ed-237">**Co to jest największy rozmiar strony obiektu blob jest obsługiwana?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="ee0ed-238">Największy rozmiar strony obiektu blob Azure obsługuje jest 8 TB (8191 GB).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="ee0ed-239">Nie obsługujemy stronicowe obiekty BLOB większych niż 4 TB (4,095 GB) dołączona do maszyny Wirtualnej jako dane lub dysków systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="ee0ed-240">**Należy użyć nowej wersji narzędzi platformy Azure do tworzenia, Dołącz, zmienianie rozmiaru i przekaż dysków większych niż 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="ee0ed-241">Nie trzeba uaktualnić Azure istniejących narzędzi do tworzenia, Dołącz lub zmieniać rozmiar dysków większych niż 1 TB.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="ee0ed-242">Aby przesłać plik wirtualnego dysku twardego z lokalnymi bezpośrednio na platformie Azure jako stronicowy obiekt blob lub niezarządzane dysku, należy użyć najnowszej zestawów narzędzia:</span><span class="sxs-lookup"><span data-stu-id="ee0ed-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="ee0ed-243">Narzędzia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ee0ed-243">Azure tools</span></span>      | <span data-ttu-id="ee0ed-244">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="ee0ed-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="ee0ed-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee0ed-245">Azure PowerShell</span></span> | <span data-ttu-id="ee0ed-246">Numer wersji 4.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="ee0ed-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="ee0ed-247">Interfejs wiersza polecenia platformy Azure w wersji 1</span><span class="sxs-lookup"><span data-stu-id="ee0ed-247">Azure CLI v1</span></span>     | <span data-ttu-id="ee0ed-248">Numer wersji 0.10.13: 2017 może zwolnić lub nowszy</span><span class="sxs-lookup"><span data-stu-id="ee0ed-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="ee0ed-249">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="ee0ed-249">AzCopy</span></span>           | <span data-ttu-id="ee0ed-250">Numer wersji 6.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="ee0ed-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="ee0ed-251">Obsługa interfejsu wiersza polecenia Azure w wersji 2 i Eksploratora usługi Storage platformy Azure będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="ee0ed-252">**P4 i P6 rozmiary dysków są obsługiwane dla niezarządzanego dysków lub stronicowych obiektów blob?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="ee0ed-253">Nie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-253">No.</span></span> <span data-ttu-id="ee0ed-254">P4 (32 GB) i P6 rozmiary dysków (64 GB) są obsługiwane tylko w przypadku dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="ee0ed-255">Obsługa dysków niezarządzane i stronicowe obiekty BLOB będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="ee0ed-256">**Jeśli Mój istniejący premium zarządzane na dysku z mniej niż 64 GB został utworzony przed włączeniem małego dysku (około 15 czerwca 2017 r), jak jest on rozliczany?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="ee0ed-257">Istniejące premium małe dyski mniej niż 64 GB nadal będą naliczane opłaty zgodnie z warstwy cenowej P10.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="ee0ed-258">**Jak można zmienić warstwy dysków premium małe dyski, mniejsze niż 64 GB z P10 P4 lub P6?**</span><span class="sxs-lookup"><span data-stu-id="ee0ed-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="ee0ed-259">Można utworzyć migawkę małe dyski, a następnie utwórz dysk, aby automatycznie Zmień warstwę cenową P4 lub P6 zależnie od rozmiaru elastycznie.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="ee0ed-260">Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?</span><span class="sxs-lookup"><span data-stu-id="ee0ed-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="ee0ed-261">Jeśli Twoje pytanie nie ma na liście w tym miejscu, Daj nam znać, a pomożemy Ci znaleźć odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="ee0ed-262">W komentarzach można Zadaj pytanie na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ee0ed-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="ee0ed-263">Aby współpracować z zespołu usługi Magazyn Azure i innymi członkami społeczności informacje w tym artykule, należy użyć MSDN [forum usługi Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="ee0ed-264">Aby poprosić o funkcje, przesłać żądania i pomysłami, które [forum opinii usługi Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="ee0ed-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
