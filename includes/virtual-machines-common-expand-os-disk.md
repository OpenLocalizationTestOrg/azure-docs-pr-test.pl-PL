## <a name="overview"></a><span data-ttu-id="d0864-101">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d0864-101">Overview</span></span>
<span data-ttu-id="d0864-102">Po utworzeniu nowej maszyny wirtualnej (VM) w grupie zasobów przez wdrożenie obrazu z witryny [Azure Marketplace](https://azure.microsoft.com/marketplace/) domyślny dysk systemu operacyjnego ma pojemność 127 GB.</span><span class="sxs-lookup"><span data-stu-id="d0864-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="d0864-103">Mimo iż możliwe jest dodawanie dysków danych do maszyny wirtualnej (ich liczba zależy od wybranej jednostki magazynowej), a ponadto zaleca się instalowanie aplikacji i obciążeń intensywnie wykorzystujących procesor CPU na tych dodatkowych dyskach, klienci często muszą rozszerzać dysk systemu operacyjnego w celu obsługi niektórych scenariuszy, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="d0864-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="d0864-104">Obsługa starszych aplikacji, które instalują składniki na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0864-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="d0864-105">Migrowanie fizycznego komputera lub maszyny wirtualnej ze środowiska lokalnego z większym dyskiem systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0864-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0864-106">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: model wdrażania przy użyciu usługi Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="d0864-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="d0864-107">W tym artykule opisano używanie modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0864-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="d0864-108">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0864-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="d0864-109">Zmiana rozmiaru dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="d0864-109">Resize the OS drive</span></span>
<span data-ttu-id="d0864-110">W tym artykule opisano zadanie zmiany rozmiaru dysku systemu operacyjnego przy użyciu modułów usługi Resource Manager programu [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d0864-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="d0864-111">Otwórz okno programu Powershell ISE lub Powershell w trybie administracyjnym:</span><span class="sxs-lookup"><span data-stu-id="d0864-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="d0864-112">Zaloguj się na swoje konto platformy Microsoft Azure w trybie zarządzania zasobami i wybierz swoją subskrypcję w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="d0864-113">Ustaw nazwę swojej grupy zasobów i nazwę maszyny wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="d0864-114">Uzyskaj odwołanie do maszyny wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="d0864-115">Zatrzymaj maszynę wirtualną przed zmianą rozmiaru dysku w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="d0864-116">A teraz moment, na który wszyscy czekaliśmy!</span><span class="sxs-lookup"><span data-stu-id="d0864-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="d0864-117">Ustaw rozmiar dysku systemu operacyjnego na żądaną wartość i zaktualizuj maszynę wirtualną w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="d0864-118">Nowy rozmiar powinien być większy niż istniejący rozmiar dysku.</span><span class="sxs-lookup"><span data-stu-id="d0864-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="d0864-119">Maksymalny dozwolony rozmiar to 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="d0864-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="d0864-120">Zaktualizowanie maszyny wirtualnej może potrwać kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="d0864-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="d0864-121">Po zakończeniu wykonywania polecenia uruchom ponownie maszynę wirtualną w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d0864-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="d0864-122">To wszystko!</span><span class="sxs-lookup"><span data-stu-id="d0864-122">And that’s it!</span></span> <span data-ttu-id="d0864-123">Teraz połącz protokół RDP z maszyną wirtualną, otwórz okno Zarządzanie komputerem (lub Zarządzanie dyskiem) i rozszerz dysk przy użyciu nowo przydzielonego miejsca.</span><span class="sxs-lookup"><span data-stu-id="d0864-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="d0864-124">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d0864-124">Summary</span></span>
<span data-ttu-id="d0864-125">W tym artykule rozszerzyliśmy dysk systemu operacyjnego maszyny wirtualnej IaaS przy użyciu modułów usługi Azure Resource Manager programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="d0864-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="d0864-126">Do celów informacyjnych podano poniżej odtworzony kompletny skrypt:</span><span class="sxs-lookup"><span data-stu-id="d0864-126">Reproduced below is the complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="d0864-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0864-127">Next Steps</span></span>
<span data-ttu-id="d0864-128">Mimo iż w tym artykule skupiliśmy się głównie na rozszerzeniu dysku systemu operacyjnego maszyny wirtualnej, przy użyciu utworzonego skryptu można także rozszerzyć dyski danych dołączone do maszyny wirtualnej, zmieniając jeden wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="d0864-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="d0864-129">Aby na przykład rozszerzyć pierwszy dysk danych dołączony do maszyny wirtualnej, zamień obiekt ```OSDisk``` elementu ```StorageProfile``` na tablicę ```DataDisks``` i przy użyciu indeksu liczbowego uzyskaj odwołanie do pierwszego dołączonego dysku danych, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="d0864-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="d0864-130">W podobny sposób możesz odwoływać się do innych dysków danych dołączonych do maszyny wirtualnej — przy użyciu indeksu, jak pokazano powyżej, lub przy użyciu właściwości ```Name``` dysku, jak przedstawiono poniżej:</span><span class="sxs-lookup"><span data-stu-id="d0864-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="d0864-131">Jeśli chcesz dowiedzieć się, jak dołączyć dyski do maszyny wirtualnej usługi Azure Resource Manager, zapoznaj się z tym [artykułem](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0864-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

