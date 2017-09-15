


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="61bdc-101">Znakowanie maszynę wirtualną za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="61bdc-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="61bdc-102">Po pierwsze Przyjrzyjmy się znakowanie za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="61bdc-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="61bdc-103">[Ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) umieszcza tagi w następujących zasobach: obliczeniowych (maszyna wirtualna), magazynu (konta magazynu) i sieci (publicznego adresu IP sieci wirtualnej i interfejsu sieciowego).</span><span class="sxs-lookup"><span data-stu-id="61bdc-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="61bdc-104">Ten szablon jest przeznaczony dla maszyny Wirtualnej systemu Windows, ale mogą być dostosowywane dla maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="61bdc-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="61bdc-105">Kliknij przycisk **wdrażanie na platformie Azure** przycisk z [łącze szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="61bdc-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="61bdc-106">Spowoduje to przejście do [portalu Azure](https://portal.azure.com/) którym można wdrożyć tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="61bdc-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Proste wdrożenie przy użyciu tagów](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="61bdc-108">Ten szablon obejmuje następujące znaczniki: *działu*, *aplikacji*, i *utworzony przez*.</span><span class="sxs-lookup"><span data-stu-id="61bdc-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="61bdc-109">Użytkownik może Dodawanie/edytowanie znaczniki bezpośrednio w szablonie Jeśli chcesz różnych nazwach.</span><span class="sxs-lookup"><span data-stu-id="61bdc-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Azure tagów w szablonie](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="61bdc-111">Jak widać, tagi są definiowane jako pary klucz wartość oddzielone dwukropkiem (:).</span><span class="sxs-lookup"><span data-stu-id="61bdc-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="61bdc-112">Tagi musi być zdefiniowana w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="61bdc-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="61bdc-113">Zapisz plik szablonu, po zakończeniu edycji za pomocą tagów wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61bdc-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="61bdc-114">Następnie w **Edytuj parametry** sekcji można wypełnić wartości dla tagów.</span><span class="sxs-lookup"><span data-stu-id="61bdc-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Edytowanie tagów w portalu Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="61bdc-116">Kliknij przycisk **Utwórz** do wdrożenia tego szablonu o wartości tagu.</span><span class="sxs-lookup"><span data-stu-id="61bdc-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="61bdc-117">Znakowanie za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="61bdc-117">Tagging through the Portal</span></span>
<span data-ttu-id="61bdc-118">Po utworzeniu zasobów za pomocą tagów, można wyświetlać, dodawania i usuwania tagów w portalu.</span><span class="sxs-lookup"><span data-stu-id="61bdc-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="61bdc-119">Wybierz ikonę znaczniki, aby wyświetlić tagów:</span><span class="sxs-lookup"><span data-stu-id="61bdc-119">Select the tags icon to view your tags:</span></span>

![Ikona tagów w portalu Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="61bdc-121">Dodaj nowy znacznik za pośrednictwem portalu, definiując własne parę klucza i wartości i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="61bdc-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Dodaj nowy znacznik w portalu Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="61bdc-123">Twoje nowy znacznik powinien zostać wyświetlony na liście tagów dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="61bdc-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Nowy znacznik zapisane w portalu Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

