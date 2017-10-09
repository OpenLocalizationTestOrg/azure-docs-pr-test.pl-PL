<span data-ttu-id="3d3f7-101">Użyj tooadd grupę zasobów tooa tag **zestawu grup azure**.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="3d3f7-102">Jeśli grupa zasobów hello nie ma żadnych znaczników, przekazać hello tagu.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="3d3f7-103">Tagi są aktualizowane jako całość.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-103">Tags are updated as a whole.</span></span> <span data-ttu-id="3d3f7-104">Jeśli chcesz tooadd tag tooa grupę zasobów, w której ma znaczników, przekazuj wszystkie tagi hello.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="3d3f7-105">Tagi nie są dziedziczone przez zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="3d3f7-106">Użyj tooadd zasób tooa tag **zestaw zasobów platformy azure**.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="3d3f7-107">Przekaż hello numer wersji interfejsu API dla typu zasobu hello dodawanego hello tagu.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="3d3f7-108">Wersja interfejsu API hello tooretrieve, należy użyć hello następujące polecenia z hello dostawcy zasobów dla typu hello ustawieniu:</span><span class="sxs-lookup"><span data-stu-id="3d3f7-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="3d3f7-109">W wynikach hello Wyszukaj żądany typ zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="3d3f7-110">Teraz, podaj tej wersji interfejsu API, nazwa grupy zasobów, nazwę zasobu typu zasobu i wartość tagu jako parametry.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="3d3f7-111">Znaczniki istnieje bezpośrednio na zasobów i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="3d3f7-112">Pobierz toosee hello znaczników, grupy zasobów i jej zasobach z **Pokaż grupy azure**.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="3d3f7-113">Polecenie to zwraca metadane dotyczące grupy zasobów hello, w tym wszelkie tooit znaczniki zastosowane.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="3d3f7-114">Możesz wyświetlić przy użyciu hello tagi dla określonego zasobu **Pokaż zasobów platformy azure**.</span><span class="sxs-lookup"><span data-stu-id="3d3f7-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="3d3f7-115">Użyj tooretrieve wszystkie zasoby hello z wartością tagu:</span><span class="sxs-lookup"><span data-stu-id="3d3f7-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="3d3f7-116">Użyj wszystkich grup zasobów hello z wartością tagu tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="3d3f7-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="3d3f7-117">Możesz przeglądać znaczników hello w ramach subskrypcji hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3d3f7-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
