<span data-ttu-id="b3499-101">Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="b3499-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="b3499-102">Odłączanie dysku usuwa hello dysk od maszyny wirtualnej hello, ale nie powoduje usunięcia dysku hello z hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3499-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="b3499-103">Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.</span><span class="sxs-lookup"><span data-stu-id="b3499-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="b3499-104">toodetach dysku systemu operacyjnego, należy najpierw maszyny wirtualnej hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b3499-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="b3499-105">Znajdź hello dysku</span><span class="sxs-lookup"><span data-stu-id="b3499-105">Find hello disk</span></span>
<span data-ttu-id="b3499-106">Jeśli nie znasz nazwy hello z hello dysku lub mają tooverify zanim ją odłączyć, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="b3499-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="b3499-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3499-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b3499-108">Kliknij przycisk **maszyn wirtualnych**, a następnie wybierz hello odpowiedniej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3499-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="b3499-109">Kliknij przycisk **dysków** wzdłuż hello lewej krawędzi hello pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b3499-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="b3499-110">pulpit nawigacyjny maszyny wirtualnej Hello Wyświetla hello nazwę i typ wszystkich dołączonych dysków.</span><span class="sxs-lookup"><span data-stu-id="b3499-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="b3499-111">Na przykład na tym ekranie przedstawiono maszynę wirtualną z jednym dyskiem systemu operacyjnego (OS) i jednym dyskiem danych:</span><span class="sxs-lookup"><span data-stu-id="b3499-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Znajdowanie dysku danych](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="b3499-113">Odłączanie dysku hello</span><span class="sxs-lookup"><span data-stu-id="b3499-113">Detach hello disk</span></span>
1. <span data-ttu-id="b3499-114">Witaj portalu Azure kliknij **maszyn wirtualnych**, a następnie kliknij przycisk hello nazwę hello maszynę wirtualną, która ma być toodetach dysk danych hello.</span><span class="sxs-lookup"><span data-stu-id="b3499-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="b3499-115">Kliknij przycisk **dysków** wzdłuż hello lewej krawędzi hello pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b3499-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="b3499-116">Kliknij dysk hello ma toodetach.</span><span class="sxs-lookup"><span data-stu-id="b3499-116">Click hello disk you want toodetach.</span></span>

  ![Zidentyfikuj hello toodetach dysku](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="b3499-118">Na pasku poleceń hello, kliknij **Detach**.</span><span class="sxs-lookup"><span data-stu-id="b3499-118">From hello command bar, click **Detach**.</span></span>

  ![Zlokalizuj hello odłączyć polecenia](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="b3499-120">W oknie potwierdzenia powitania kliknij **tak** toodetach hello dysku.</span><span class="sxs-lookup"><span data-stu-id="b3499-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Potwierdź Trwa odłączanie dysku hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="b3499-122">dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3499-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
