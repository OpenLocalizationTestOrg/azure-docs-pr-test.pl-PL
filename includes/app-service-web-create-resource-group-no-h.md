<span data-ttu-id="53cd1-101">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="53cd1-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="53cd1-102">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="53cd1-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="53cd1-103">Zasadniczo grupy zasobów i zasoby są tworzone w pobliskim regionie.</span><span class="sxs-lookup"><span data-stu-id="53cd1-103">You generally create your resource group and the resources in a region near you.</span></span> <span data-ttu-id="53cd1-104">Aby wyświetlić wszystkie obsługiwane lokalizacje dla usługi Azure Web Apps, uruchom polecenie `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="53cd1-104">To see all supported locations for Azure Web Apps, run the `az appservice list-locations` command.</span></span> 