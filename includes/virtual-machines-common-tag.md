


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="fb1cc-101">Znakowanie maszynę wirtualną za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="fb1cc-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="fb1cc-102">Po pierwsze Przyjrzyjmy się znakowanie za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="fb1cc-103">[Ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) umieszcza tagi na powitania następujące zasoby: obliczeniowych (maszyna wirtualna), magazynu (konta magazynu) i sieci (publicznego adresu IP sieci wirtualnej i interfejsu sieciowego).</span><span class="sxs-lookup"><span data-stu-id="fb1cc-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="fb1cc-104">Ten szablon jest przeznaczony dla maszyny Wirtualnej systemu Windows, ale mogą być dostosowywane dla maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="fb1cc-105">Kliknij przycisk hello **wdrażanie tooAzure** przycisk od hello [łącze szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="fb1cc-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="fb1cc-106">Spowoduje to przejście toohello [portalu Azure](https://portal.azure.com/) którym można wdrożyć tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Proste wdrożenie przy użyciu tagów](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="fb1cc-108">Ten szablon obejmuje następujące znaczniki hello: *działu*, *aplikacji*, i *utworzony przez*.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="fb1cc-109">Użytkownik może Dodawanie/edytowanie znaczniki bezpośrednio w szablonie hello Jeśli chcesz różnych nazwach.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Azure tagów w szablonie](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="fb1cc-111">Jak widać, tagi hello są definiowane jako pary klucz wartość oddzielone dwukropkiem (:).</span><span class="sxs-lookup"><span data-stu-id="fb1cc-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="fb1cc-112">tagi Hello musi być zdefiniowana w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="fb1cc-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="fb1cc-113">Zapisz plik szablonu hello po zakończeniu edycji za pomocą tagów hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="fb1cc-114">Następnie w hello **Edytuj parametry** sekcji, możesz też wypełnić hello wartości dla tagów.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Edytowanie tagów w portalu Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="fb1cc-116">Kliknij przycisk **Utwórz** toodeploy tego szablonu o wartości tagu.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="fb1cc-117">Znakowanie za pośrednictwem hello portalu</span><span class="sxs-lookup"><span data-stu-id="fb1cc-117">Tagging through hello Portal</span></span>
<span data-ttu-id="fb1cc-118">Po utworzeniu zasobów za pomocą tagów, można wyświetlać, dodawania i usuwania tagów w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="fb1cc-119">Wybierz hello tagów tooview ikona tagów:</span><span class="sxs-lookup"><span data-stu-id="fb1cc-119">Select hello tags icon tooview your tags:</span></span>

![Ikona tagów w portalu Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="fb1cc-121">Dodaj nowy znacznik za pośrednictwem portalu hello, definiując własne parę klucza i wartości i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Dodaj nowy znacznik w portalu Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="fb1cc-123">Twoje nowy znacznik powinien zostać wyświetlony na liście hello znaczników dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="fb1cc-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nowy znacznik zapisane w portalu Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

