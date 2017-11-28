<span data-ttu-id="8eb7b-101">Gdy już nie potrzebujesz dysku danych dołączonego do maszyny wirtualnej, możesz go łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="8eb7b-102">Odłączenie dysku powoduje jego usunięcie z maszyny wirtualnej, ale nie usuwa go z konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="8eb7b-103">Jeśli chcesz użyć danych znajdujących się na tym dysku, możesz dołączyć go ponownie do tej samej lub innej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="8eb7b-104">Aby odłączyć dysk systemu operacyjnego, najpierw musisz usunąć maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="8eb7b-105">Wyszukiwanie dysku</span><span class="sxs-lookup"><span data-stu-id="8eb7b-105">Find the disk</span></span>
<span data-ttu-id="8eb7b-106">Jeśli nie znasz nazwy dysku lub chcesz ją sprawdzić przed odłączeniem dysku, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="8eb7b-107">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8eb7b-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8eb7b-108">Kliknij pozycję **Maszyny wirtualne**, a następnie wybierz odpowiednią maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="8eb7b-109">Kliknij pozycję **Dyski** z lewej strony pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="8eb7b-110">Pulpit nawigacyjny maszyny wirtualnej zawiera listę nazw i typów wszystkich dołączonych dysków.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="8eb7b-111">Na przykład na tym ekranie przedstawiono maszynę wirtualną z jednym dyskiem systemu operacyjnego (OS) i jednym dyskiem danych:</span><span class="sxs-lookup"><span data-stu-id="8eb7b-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Znajdowanie dysku danych](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="8eb7b-113">Odłączanie dysku</span><span class="sxs-lookup"><span data-stu-id="8eb7b-113">Detach the disk</span></span>
1. <span data-ttu-id="8eb7b-114">W witrynie Azure Portal kliknij pozycję **Maszyny wirtualne**, a następnie kliknij nazwę maszyny wirtualnej zawierającej dysk danych, który chcesz odłączyć.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="8eb7b-115">Kliknij pozycję **Dyski** z lewej strony pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="8eb7b-116">Kliknij dysk, który chcesz odłączyć.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-116">Click the disk you want to detach.</span></span>

  ![Identyfikowanie dysku do odłączenia](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="8eb7b-118">Na pasku poleceń kliknij pozycję **Odłącz**.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-118">From the command bar, click **Detach**.</span></span>

  ![Znajdowanie polecenia Odłącz](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="8eb7b-120">W oknie potwierdzenia kliknij przycisk **Tak**, aby odłączyć dysk.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Potwierdzanie odłączania dysku](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="8eb7b-122">Odłączony dysk pozostaje w magazynie, lecz nie jest już dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8eb7b-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>
