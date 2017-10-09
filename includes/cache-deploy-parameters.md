
### <a name="cacheskuname"></a><span data-ttu-id="06490-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="06490-101">cacheSKUName</span></span>
<span data-ttu-id="06490-102">warstwy cenowej Hello hello Redis Azure nowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="06490-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="06490-103">Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (Basic lub Standard) i przypisuje wartość domyślną (Basic), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="06490-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="06490-104">Basic zapewnia jeden węzeł o różnych rozmiarach dostępne w górę too53 GB.</span><span class="sxs-lookup"><span data-stu-id="06490-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="06490-105">Standard udostępnia dwa węzły podstawowego/repliki o różnych rozmiarach dostępne w górę too53 SLA GB i 99,9%.</span><span class="sxs-lookup"><span data-stu-id="06490-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="06490-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="06490-106">cacheSKUFamily</span></span>
<span data-ttu-id="06490-107">Witaj rodziny hello sku.</span><span class="sxs-lookup"><span data-stu-id="06490-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="06490-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="06490-108">cacheSKUCapacity</span></span>
<span data-ttu-id="06490-109">rozmiar Hello hello nowe wystąpienie pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="06490-109">hello size of hello new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="06490-110">Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (0, 1, 2, 3, 4, 5 lub 6) i przypisuje wartość domyślną (1) Jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="06490-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="06490-111">Rozmiar pamięci podręcznej toofollowing odpowiada tych numerów: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="06490-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

