### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
Witaj **połączonej usługi magazynu Azure** umożliwia toolink fabryki danych Azure tooan konta magazynu platformy Azure przy użyciu hello **klucz konta**, który zapewnia usłudze fabryka danych hello z toohello dostępu globalny usługi Azure Magazyn. Witaj w poniższej tabeli przedstawiono opis dla określonego tooAzure elementów JSON połączonej usługi magazynu.

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |musi mieć ustawioną właściwość type Hello: **AzureStorage** |Tak |
| Parametry połączenia |Określ informacje niezbędne tooconnect tooAzure magazynu dla właściwości connectionString hello. |Tak |

Zobacz hello poniższego artykułu kroki tooview/kopiowania hello konta klucza usługi Azure Storage: [wyświetlanie, kopiowanie i regenerate magazynu, klucze dostępu](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Przykład:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Sas magazynu Azure połączona usługa
Sygnatury dostępu współdzielonego (SAS) zapewnia dostęp delegowany tooresources na koncie magazynu. Umożliwia on toogrant klienta ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień, bez konieczności tooshare klucze dostępu do Twojego konta. Witaj SAS jest identyfikatorem URI, który obejmuje w jego parametrów zapytania, wszystkie informacje hello niezbędne dla zasobu magazynu tooa dostępu uwierzytelnionego. tooaccess zasoby pamięci masowej z hello SAS powitania klienta musi tylko toopass hello SAS toohello odpowiedniego konstruktora lub metody. Aby uzyskać szczegółowe informacje na temat sygnatury dostępu Współdzielonego, zobacz [sygnatury dostępu współdzielonego: hello opis modelu sygnatur dostępu Współdzielonego](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure obsługuje teraz tylko w fabryce danych **sygnatury dostępu Współdzielonego usługi** , ale nie SAS konta. Zobacz [typy z sygnatury dostępu współdzielonego](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) szczegółowe informacje dotyczące tych dwóch typów i w jaki sposób tooconstruct. Uwaga hello adres URL SAS generable z portalu Azure lub Eksploratora usługi Storage jest SAS konta, który nie jest obsługiwany.
> 

Hello SAS magazynu Azure połączone usługi umożliwia toolink fabryki danych Azure tooan konta magazynu Azure za pomocą udostępnionego podpis dostępu (SAS). Zapewnia fabryki danych hello dostęp ograniczony/czas-powiązane z określonego/tooall zasobów (kontener/obiektów blob) w magazynie hello. Witaj w poniższej tabeli przedstawiono opis dla określonych tooAzure elementów JSON SAS magazynu połączone usługi. 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |musi mieć ustawioną właściwość type Hello: **element AzureStorageSas** |Tak |
| sasUri |Określ zasoby usługi Azure Storage toohello udostępnionych URI sygnatury dostępu obiektu blob, kontenera lub tabeli.  |Tak |

**Przykład:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Podczas tworzenia **identyfikatora URI połączenia SAS**, biorąc pod uwagę następujące hello:  

* Ustaw odpowiednie odczytu/zapisu **uprawnienia** obiektów na podstawie sposobu hello połączonej usługi (Odczyt, zapis, Odczyt/zapis) jest używany w fabryce danych.
* Ustaw **czas wygaśnięcia** odpowiednio. Upewnij się, że hello dostępu tooAzure magazynu obiektów nie wygasa w aktywnym okresie potoku hello hello.
* Identyfikator URI ma być tworzony na powitania prawo kontenera/obiektów blob lub poziom tabeli oparte na powitania wymagany. Tooan identyfikatora Uri połączenia SAS obiektu blob systemu Azure umożliwia tooaccess usługi fabryka danych hello tego konkretnego obiektu blob. Kontener obiektów blob platformy Azure tooan identyfikatora Uri połączenia SAS umożliwia tooiterate usługi fabryka danych hello za pośrednictwem obiektów blob w tym kontenerze. Jeśli potrzebujesz więcej tooprovide dostępu/mniejszą liczbę obiektów później lub aktualizacji hello SAS identyfikatora URI, pamiętaj tooupdate hello połączona usługa o hello nowy identyfikator URI.   

