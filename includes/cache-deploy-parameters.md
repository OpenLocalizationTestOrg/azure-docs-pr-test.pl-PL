
### <a name="cacheskuname"></a><span data-ttu-id="1e712-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="1e712-101">cacheSKUName</span></span>
<span data-ttu-id="1e712-102">Warstwa cenowa nowej pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1e712-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="1e712-103">Szablon definiuje wartości, które są dozwolone dla tego parametru (Basic lub Standard), a następnie przypisuje wartość domyślną (Basic), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="1e712-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="1e712-104">Basic zapewnia jeden węzeł o różnych rozmiarach dostępne w górę do 53 GB.</span><span class="sxs-lookup"><span data-stu-id="1e712-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="1e712-105">Standard udostępnia dwa węzły podstawowego/repliki o różnych rozmiarach dostępne w górę do umowy SLA 53 GB i 99,9%.</span><span class="sxs-lookup"><span data-stu-id="1e712-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="1e712-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="1e712-106">cacheSKUFamily</span></span>
<span data-ttu-id="1e712-107">Rodzina dla jednostki sku.</span><span class="sxs-lookup"><span data-stu-id="1e712-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="1e712-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="1e712-108">cacheSKUCapacity</span></span>
<span data-ttu-id="1e712-109">Rozmiar nowego wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1e712-109">The size of the new Azure Redis Cache instance.</span></span> 

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
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="1e712-110">Szablon definiuje wartości, które są dozwolone dla tego parametru (0, 1, 2, 3, 4, 5 lub 6) i przypisuje wartość domyślną (1) Jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="1e712-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="1e712-111">Te numery odpowiadają następujących rozmiarów pamięci podręcznej: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="1e712-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

