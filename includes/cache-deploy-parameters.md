
### <a name="cacheskuname"></a>cacheSKUName
warstwy cenowej Hello hello Redis Azure nowej pamięci podręcznej.

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

Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (Basic lub Standard) i przypisuje wartość domyślną (Basic), jeśli nie określono wartości. Basic zapewnia jeden węzeł o różnych rozmiarach dostępne w górę too53 GB.
Standard udostępnia dwa węzły podstawowego/repliki o różnych rozmiarach dostępne w górę too53 SLA GB i 99,9%.

### <a name="cacheskufamily"></a>cacheSKUFamily
Witaj rodziny hello sku.

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


### <a name="cacheskucapacity"></a>cacheSKUCapacity
rozmiar Hello hello nowe wystąpienie pamięci podręcznej Redis Azure. 

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


Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (0, 1, 2, 3, 4, 5 lub 6) i przypisuje wartość domyślną (1) Jeśli nie określono wartości. Rozmiar pamięci podręcznej toofollowing odpowiada tych numerów: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

