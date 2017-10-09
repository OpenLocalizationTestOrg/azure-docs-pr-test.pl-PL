<span data-ttu-id="039a9-101">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="039a9-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="039a9-102">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="039a9-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="039a9-103">toosee hello dostępnych lokalizacji, uruchom hello `az appservice list-locations` polecenia.</span><span class="sxs-lookup"><span data-stu-id="039a9-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="039a9-104">Zasadniczo tworzysz zasoby w pobliskim regionie.</span><span class="sxs-lookup"><span data-stu-id="039a9-104">You generally create resources in a region near you.</span></span>
