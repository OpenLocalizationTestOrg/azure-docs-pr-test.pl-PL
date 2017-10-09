# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="1b1bc-101">Często zadawane pytania dotyczące dyski maszyny Wirtualnej Azure IaaS i zarządzane i niezarządzane — wersja premium</span><span class="sxs-lookup"><span data-stu-id="1b1bc-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="1b1bc-102">Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące dysków zarządzanych Azure i usługa Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="1b1bc-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="1b1bc-103">Managed Disks</span></span>

<span data-ttu-id="1b1bc-104">**Co to jest Azure zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="1b1bc-105">Dyski zarządzane jest funkcja, która ułatwia zarządzanie dyskami dla maszyn wirtualnych IaaS platformy Azure dzięki obsłudze Zarządzanie kontem magazynu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="1b1bc-106">Aby uzyskać więcej informacji, zobacz hello [omówienie dysków zarządzanych](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="1b1bc-107">**Jeśli utworzyć standardowych dysków zarządzanych z istniejącego dysku VHD, 80 GB, ile będzie tego koszt mnie?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="1b1bc-108">Standardowa dysków zarządzanych utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako dalej rozmiaru dysku standardowe hello, który jest dyskiem s10 w warstwie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="1b1bc-109">Są naliczane opłaty zgodnie z toohello s10 w warstwie dysków cennik.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="1b1bc-110">Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1b1bc-111">**Czy istnieją kosztów transakcji dla standardowych dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="1b1bc-112">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-112">Yes.</span></span> <span data-ttu-id="1b1bc-113">W przypadku naliczona opłata za każdą transakcję.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-113">You're charged for each transaction.</span></span> <span data-ttu-id="1b1bc-114">Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1b1bc-115">**Dla standardowych dysków zarządzanych I obciążymy hello rzeczywisty rozmiar hello danych na dysku hello lub hello elastycznie pojemność dysku hello?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="1b1bc-116">Są naliczane opłaty oparte na powitania elastycznie pojemność dysku hello.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="1b1bc-117">Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1b1bc-118">**Jak jest inny niż dyski niezarządzane cennik dysków zarządzanych w warstwie premium?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="1b1bc-119">jak w przypadku dysków premium niezarządzanym jest hello Hello cennik dysków zarządzanych w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="1b1bc-120">**Czy można zmienić hello typu konta magazynu (standardowa lub Premium) z dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="1b1bc-121">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-121">Yes.</span></span> <span data-ttu-id="1b1bc-122">Można zmienić typu konta magazynu hello dysków zarządzanych za pomocą hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="1b1bc-123">**Czy istnieje sposób, aby I skopiuj lub wyeksportować konta magazynu prywatnego tooa dysków zarządzanych w?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="1b1bc-124">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-124">Yes.</span></span> <span data-ttu-id="1b1bc-125">Dyski zarządzane można wyeksportować za pomocą hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="1b1bc-126">**Czy można użyć pliku wirtualnego dysku twardego w toocreate konta magazynu Azure dysków zarządzanych z innej subskrypcji?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="1b1bc-127">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-127">No.</span></span>

<span data-ttu-id="1b1bc-128">**Czy można użyć pliku wirtualnego dysku twardego w toocreate konta magazynu Azure dysków zarządzanych w innym regionie?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="1b1bc-129">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-129">No.</span></span>

<span data-ttu-id="1b1bc-130">**Czy istnieją jakiekolwiek ograniczenia skali dla klientów korzystających z zarządzanego dyski?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="1b1bc-131">Dyski zarządzane eliminuje limity hello skojarzonego z kontami magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="1b1bc-132">Hello liczby zarządzanych dysków dla subskrypcji jest jednak ograniczona too2, 000 domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="1b1bc-133">Obsługa tooincrease można wywołać ten numer.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="1b1bc-134">**Czy można wykonać przyrostowej migawki dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="1b1bc-135">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-135">No.</span></span> <span data-ttu-id="1b1bc-136">Bieżąca funkcja migawki Hello sprawia, że pełna kopia dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="1b1bc-137">Jednak firma Microsoft są planowania toosupport przyrostowe migawki w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="1b1bc-138">**Maszyny wirtualne w zestawie dostępności może zawierać kombinację dysków zarządzane i niezarządzane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="1b1bc-139">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-139">No.</span></span> <span data-ttu-id="1b1bc-140">Hello maszyn wirtualnych w zestawie dostępności muszą używać wszystkich zarządzanych dysków lub wszystkie dyski niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="1b1bc-141">Podczas tworzenia zestawu dostępności można wybrać typu dyski mają toouse.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="1b1bc-142">**Jest opcja domyślna hello dysków zarządzanych w portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="1b1bc-143">Aktualnie nie ale będzie gotowa do domyślnego hello w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="1b1bc-144">**Można utworzyć pusty dysk zarządzany?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="1b1bc-145">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-145">Yes.</span></span> <span data-ttu-id="1b1bc-146">Możesz utworzyć pusty dysk.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-146">You can create an empty disk.</span></span> <span data-ttu-id="1b1bc-147">Dysk zarządzany można tworzyć niezależnie od maszyny Wirtualnej, na przykład bez podłączany tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="1b1bc-148">**Co to jest liczba domen błędów hello obsługiwane dla zestawu dostępności używającym dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="1b1bc-149">W zależności od hello regionu, w którym znajduje się zestaw dostępności hello, który używa dysków zarządzanych liczba domen błędów hello obsługiwane jest 2 lub 3.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="1b1bc-150">**W jaki sposób hello konta standard storage dla diagnostyki Konfigurowanie?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="1b1bc-151">Skonfiguruj konto magazynu prywatne dla diagnostyki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="1b1bc-152">W przyszłości hello, planujemy diagnostyki tooswitch również tooManaged dysków.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="1b1bc-153">**Jakiego rodzaju obsługi kontroli dostępu opartej na rolach jest dostępna dla dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="1b1bc-154">Zarządzane dysków obsługuje trzy kluczowe domyślne role:</span><span class="sxs-lookup"><span data-stu-id="1b1bc-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="1b1bc-155">Właściciel: Mogą zarządzać wszystkim łącznie z dostępem</span><span class="sxs-lookup"><span data-stu-id="1b1bc-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="1b1bc-156">Współautor: Mogą zarządzać wszystkim poza dostępem</span><span class="sxs-lookup"><span data-stu-id="1b1bc-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="1b1bc-157">Czytnik: Można przeglądać wszystko, ale nie można wprowadzić zmian</span><span class="sxs-lookup"><span data-stu-id="1b1bc-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="1b1bc-158">**Czy istnieje sposób, aby I skopiuj lub wyeksportować konta magazynu prywatnego tooa dysków zarządzanych w?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="1b1bc-159">Możesz uzyskać sygnatury dostępu współdzielonego tylko do odczytu identyfikator URI dla hello zarządzane na dysku i korzystać z niego toocopy hello zawartość tooa prywatnego składowania konta lub lokalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="1b1bc-160">**Można utworzyć kopię dysku zarządzanego?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="1b1bc-161">Klienci mogą migawki dysków zarządzanych, a następnie użyj toocreate migawki hello dysków zarządzanych w innym.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="1b1bc-162">**Niezarządzane dyski nadal są obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="1b1bc-163">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-163">Yes.</span></span> <span data-ttu-id="1b1bc-164">Firma Microsoft obsługuje dyski niezarządzane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="1b1bc-165">Zalecamy dysków zarządzanych dla nowych obciążeń, a następnie migracji dysków toomanaged bieżącego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="1b1bc-166">**Jeśli. Utwórz dysk 128 GB i dopiero potem zwiększyć jej hello rozmiar too130 GB, będzie I naliczona opłata za hello dalej rozmiar dysku (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="1b1bc-167">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-167">Yes.</span></span>

<span data-ttu-id="1b1bc-168">**Magazyn lokalnie nadmiarowy, Magazyn geograficznie nadmiarowy, można utworzyć i dyskach zarządzanych przez Magazyn strefowo nadmiarowy?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="1b1bc-169">Dyskach zarządzanych platformy Azure obsługuje obecnie tylko lokalnie nadmiarowego magazynu zarządzane dyski.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="1b1bc-170">**Można zmniejszyć lub downsize dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="1b1bc-171">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-171">No.</span></span> <span data-ttu-id="1b1bc-172">Ta funkcja nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="1b1bc-173">**Właściwość Nazwa komputera hello można zmienić, gdy specjalistycznej (nie utworzone przy użyciu narzędzia przygotowywania systemu hello lub uogólniony) dysku systemu operacyjnego jest używany tooprovision maszyny Wirtualnej?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="1b1bc-174">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-174">No.</span></span> <span data-ttu-id="1b1bc-175">Nie można zaktualizować właściwości Nazwa komputera hello.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-175">You can't update hello computer name property.</span></span> <span data-ttu-id="1b1bc-176">Hello nowej maszyny Wirtualnej dziedziczy on hello nadrzędna maszyna wirtualna, będącą dysku systemu operacyjnego hello toocreate używane.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="1b1bc-177">**Gdzie można znaleźć przykładowe usługi Azure Resource Manager toocreate szablony maszyn wirtualnych z dyskami zarządzanych**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="1b1bc-178">Lista szablonów przy użyciu dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="1b1bc-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="1b1bc-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="1b1bc-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="1b1bc-180">Zarządzane dysków i szyfrowanie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="1b1bc-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="1b1bc-181">**Jest szyfrowanie usługi Magazyn Azure domyślnie podczas tworzenia dysków zarządzanych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="1b1bc-182">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-182">Yes.</span></span>

<span data-ttu-id="1b1bc-183">**Kto zarządza hello klucze szyfrowania?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="1b1bc-184">Firma Microsoft zarządza hello kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="1b1bc-185">**Do zarządzanych dysków można wyłączyć szyfrowanie usługi Magazyn?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="1b1bc-186">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-186">No.</span></span>

<span data-ttu-id="1b1bc-187">**Jest szyfrowanie usługi Magazyn dostępna tylko w określonych regionach?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="1b1bc-188">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-188">No.</span></span> <span data-ttu-id="1b1bc-189">Jest dostępna we wszystkich regionach hello, gdzie dostępna jest opcja dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="1b1bc-190">Dyski zarządzane jest dostępna we wszystkich regionach publicznego i Niemczech.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="1b1bc-191">**Jak można sprawdzić w przypadku zarządzanych dysku są szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="1b1bc-192">Można ustalić hello godzina utworzenia dysków zarządzanych z hello portalu Azure, hello wiersza polecenia platformy Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="1b1bc-193">Jeśli godzina powitania po 9 czerwca 2017 dysku są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="1b1bc-194">**Jak można zaszyfrować Moje istniejących dysków, które zostały utworzone przed 10 czerwca 2017 r.**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="1b1bc-195">Począwszy od 10 czerwca 2017 nowych danych tooexisting zarządzane dysków jest szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="1b1bc-196">Firma Microsoft są także planowania tooencrypt istniejących danych i szyfrowania hello nastąpi asynchronicznie w tle hello.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="1b1bc-197">Jeśli musi teraz zaszyfrować dane, należy utworzyć kopię dysku.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="1b1bc-198">Nowe dyski zostaną zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="1b1bc-199">Kopiowanie dysków zarządzanych za pomocą hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b1bc-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="1b1bc-200">Kopiowanie dysków zarządzanych za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b1bc-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="1b1bc-201">**Są zarządzane migawki i obrazy szyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="1b1bc-202">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-202">Yes.</span></span> <span data-ttu-id="1b1bc-203">Wszystkie zarządzane migawki i obrazy utworzone po 9 czerwca 2017 r są szyfrowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="1b1bc-204">**Z niezarządzanego dysków, które znajdują się na kontach magazynu, które są lub toomanaged wcześniej zaszyfrowanych dysków można przekonwertować maszyny wirtualne?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="1b1bc-205">Tak</span><span class="sxs-lookup"><span data-stu-id="1b1bc-205">Yes</span></span>

<span data-ttu-id="1b1bc-206">**Wyeksportowane wirtualnego dysku twardego z zarządzanego dysku lub migawka także będą zaszyfrowane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="1b1bc-207">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-207">No.</span></span> <span data-ttu-id="1b1bc-208">Jeśli możesz wyeksportować tooan wirtualnego dysku twardego, ale szyfrowane konta magazynu z zaszyfrowanych dysków zarządzanych lub migawki, a następnie jest on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="1b1bc-209">Dyski Premium: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="1b1bc-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="1b1bc-210">**Jeśli maszyna wirtualna używa rozmiar serii, która obsługuje magazyn w warstwie Premium, takich jak DSv2, można dołączyć zarówno premium i dyski standardowe danych?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="1b1bc-211">Tak.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-211">Yes.</span></span>

<span data-ttu-id="1b1bc-212">**Czy mogę dołączyć zarówno premium i standardowa danych dysków tooa rozmiar serii, która nie obsługuje usługi Premium Storage, takich jak seria D, Dv2, G lub F?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="1b1bc-213">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-213">No.</span></span> <span data-ttu-id="1b1bc-214">Można dołączać tylko tooVMs dyski standardowe danych, który nie należy używać serii rozmiar, który obsługuje magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="1b1bc-215">**Jeśli dysk danych — warstwa premium można utworzyć z istniejącego dysku VHD, który był 80 GB, ile będzie tego koszt?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="1b1bc-216">Dysk z danymi premium utworzone na podstawie wirtualny dysk twardy 80 GB jest traktowany jako rozmiar dysku dostępny dalej premium hello, który jest dyskiem P10.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="1b1bc-217">Jest naliczane opłaty zgodnie z toohello P10 dysku cennik.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="1b1bc-218">**Czy istnieją toouse kosztów transakcji magazynu Premium?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="1b1bc-219">Brak koszt stały rozmiar każdego dysku, które pojawia się z określonym limity udostępnionym IOPS i przepustowość.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="1b1bc-220">Witaj innych kosztów są przepustowości wychodzącej i pojemności migawki, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="1b1bc-221">Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1b1bc-222">**Jakie są limity hello IOPS i przepływność, którą można pobrać z pamięci podręcznej dysku hello?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="1b1bc-223">Witaj łączne limity dla pamięci podręcznej i lokalny dysk SSD dla serii DS są 4000 IOPS na podstawowe i 33 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="1b1bc-224">Witaj serii GS oferuje 5000 IOPS na podstawowe i 50 MB na sekundę na podstawowe.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="1b1bc-225">**To jest hello obsługiwany przez lokalny dysk SSD dla maszyny Wirtualnej, zarządzane dyski?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="1b1bc-226">Witaj lokalny dysk SSD jest tymczasowego magazynu, który jest dołączony do maszyny Wirtualnej dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="1b1bc-227">Jest nie żadnymi dodatkowymi kosztami dla tego magazynu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="1b1bc-228">Firma Microsoft zaleca, aby używać tego toostore lokalnych dysków SSD dane aplikacji, ponieważ nie jest on utrwalane w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="1b1bc-229">**Są dostępne wszelkie następstwa dla hello używać TRIM na dysków w warstwie premium?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="1b1bc-230">Nie jest używana toohello wadą interfejsu TRIM na dyskach platformy Azure w warstwie premium albo lub dyski standardowe.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="1b1bc-231">Nowy rozmiar dysku: zarządzanych i niezarządzanych</span><span class="sxs-lookup"><span data-stu-id="1b1bc-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="1b1bc-232">**Co to jest hello największy rozmiar dysku systemu operacyjnego i dysków z danymi obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="1b1bc-233">Typ partycji Hello Azure obsługuje dla dysku systemu operacyjnego jest hello główny rekord rozruchowy (MBR).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="1b1bc-234">Hello MBR format obsługuje rozmiaru dysku too2 TB.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="1b1bc-235">Witaj największy rozmiar, który Azure obsługuje dla dysku systemu operacyjnego jest 2 TB.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="1b1bc-236">Azure obsługuje too4 TB dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="1b1bc-237">**Co to jest hello największy blob rozmiar strony jest obsługiwana?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="1b1bc-238">Hello największy strony rozmiar obiektu blob Azure obsługującym jest 8 TB (8191 GB).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="1b1bc-239">Nie obsługujemy stronicowe obiekty BLOB większych niż 4 TB (4,095 GB) dołączona tooa maszyny Wirtualnej jako dane lub dysków systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="1b1bc-240">**Należy toouse nowej wersji z toocreate narzędzi platformy Azure, Dołącz, zmienianie rozmiaru i przekazać dysków większych niż 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="1b1bc-241">Nie ma potrzeby tooupgrade Twojego istniejących toocreate narzędzia Azure, Dołącz lub zmieniać rozmiar dysków większych niż 1 TB.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="1b1bc-242">tooupload dysk VHD plik z lokalnymi bezpośrednio tooAzure jako stronicowy obiekt blob lub niezarządzane dysku, należy toouse hello najnowsze narzędzia zestawów:</span><span class="sxs-lookup"><span data-stu-id="1b1bc-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="1b1bc-243">Narzędzia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b1bc-243">Azure tools</span></span>      | <span data-ttu-id="1b1bc-244">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="1b1bc-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="1b1bc-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b1bc-245">Azure PowerShell</span></span> | <span data-ttu-id="1b1bc-246">Numer wersji 4.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1b1bc-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="1b1bc-247">Interfejs wiersza polecenia platformy Azure w wersji 1</span><span class="sxs-lookup"><span data-stu-id="1b1bc-247">Azure CLI v1</span></span>     | <span data-ttu-id="1b1bc-248">Numer wersji 0.10.13: 2017 może zwolnić lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1b1bc-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="1b1bc-249">Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="1b1bc-249">AzCopy</span></span>           | <span data-ttu-id="1b1bc-250">Numer wersji 6.1.0: czerwiec 2017 wersji lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1b1bc-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="1b1bc-251">Witaj obsługę wiersza polecenia platformy Azure w wersji 2 i Eksploratora usługi Storage platformy Azure będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="1b1bc-252">**P4 i P6 rozmiary dysków są obsługiwane dla niezarządzanego dysków lub stronicowych obiektów blob?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="1b1bc-253">Nie.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-253">No.</span></span> <span data-ttu-id="1b1bc-254">P4 (32 GB) i P6 rozmiary dysków (64 GB) są obsługiwane tylko w przypadku dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="1b1bc-255">Obsługa dysków niezarządzane i stronicowe obiekty BLOB będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="1b1bc-256">**Jeśli Mój istniejący premium zarządzane na dysku z mniej niż 64 GB został utworzony przed włączeniem hello małego dysku (około 15 czerwca 2017 r), jak jest on rozliczany?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="1b1bc-257">Istniejące dyski premium małych mniej niż 64 GB nadal toobe rozliczane zgodnie z toohello P10 warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="1b1bc-258">**Jak można zmienić warstwy dysku hello dyski premium małych mniejsze niż 64 GB P10 tooP4 lub P6?**</span><span class="sxs-lookup"><span data-stu-id="1b1bc-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="1b1bc-259">Można utworzyć migawkę małe dyski, a następnie utworzyć dysku hello przełącznika tooautomatically tooP4 warstwy cenowej lub P6 na podstawie hello elastycznie rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="1b1bc-260">Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?</span><span class="sxs-lookup"><span data-stu-id="1b1bc-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="1b1bc-261">Jeśli Twoje pytanie nie ma na liście w tym miejscu, Daj nam znać, a pomożemy Ci znaleźć odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="1b1bc-262">W komentarzach hello można Zadaj pytanie na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1b1bc-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="1b1bc-263">tooengage z zespołem usługi Azure Storage hello i innymi członkami społeczności informacje w tym artykule, należy użyć hello MSDN [forum usługi Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="1b1bc-264">Funkcje toorequest przesłać toohello Twojego żądania i pomysły [forum opinii usługi Azure Storage](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="1b1bc-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
