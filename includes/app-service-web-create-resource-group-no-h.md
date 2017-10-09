<span data-ttu-id="909d0-101">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="909d0-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="909d0-102">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="909d0-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="909d0-103">Ogólnie rzecz biorąc tworzenia zasobu grupy i hello zasobów w regionie, w pobliżu.</span><span class="sxs-lookup"><span data-stu-id="909d0-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="909d0-104">toosee obsługiwane lokalizacje dla aplikacji sieci Web platformy Azure, uruchom hello `az appservice list-locations` polecenia.</span><span class="sxs-lookup"><span data-stu-id="909d0-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
