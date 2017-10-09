Istnieją dwa typy kont magazynu:

### <a name="general-purpose-storage-accounts"></a>Konta magazynu ogólnego przeznaczenia
Zapewnia konta magazynu ogólnego przeznaczenia, dostęp tooAzure magazynu usług, takich jak tabel, kolejek, plików, obiekty BLOB i Azure dysków maszyny wirtualnej w ramach jednego konta. Ten typ konta magazynu ma dwie warstwy wydajności:

* Warstwę wydajności magazynu standardowego, co pozwala toostore tabel, kolejek, plików, obiekty BLOB i Azure dysków maszyny wirtualnej.
* Warstwę wydajności magazynu w warstwie Premium, która obecnie obsługuje tylko dyski maszyny wirtualnej Azure. Zobacz temat [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: usługa Storage o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure), aby uzyskać szczegółowe informacje o usłudze Premium Storage.

### <a name="blob-storage-accounts"></a>Konta usługi Blob Storage
Konto usługi Blob Storage to specjalne konto magazynu służące do przechowywania danych niestrukturalnych w formie obiektów blob w usłudze Azure Storage. Konta magazynu obiektów blob są podobne tooyour istniejących kont magazynu ogólnego przeznaczenia i udostępnianie wszystkich hello dużą trwałości, dostępności, skalowalności i wydajności funkcji czy używane obecnie, łącznie z 100% spójnością interfejsu API dla blokowych obiektów blob i uzupełnialnych obiektów blob. W przypadku aplikacji wymagających tylko magazynu obiektów blokowych lub uzupełnialnych obiektów blob zalecamy używanie kont usługi Blob Storage.

> [!NOTE]
> Konta Magazynu obiektów blob obsługują tylko blokowe obiekty blob i uzupełnialne obiekty blob — stronicowe obiekty blob nie są obsługiwane.
> 
> 

Konta magazynu obiektów blob udostępniają hello **warstwy dostępu** atrybut, który można określić podczas tworzenia konta i modyfikować później zgodnie z potrzebami. Istnieją dwa typy warstw dostępu, które można określić na podstawie wzorca dostępu do danych:

* A **gorąca** warstwy dostępu, co oznacza, że hello obiektów hello koncie magazynu uzyskuje się częściej. Dzięki temu można toostore danych na niższe koszty dostępu.
* A **chłodnych** warstwy dostępu, co oznacza, że hello obiektów hello koncie magazynu uzyskuje się rzadziej. Dzięki temu dane toostore koszt będzie niższy koszt przechowywania danych.

W przypadku zmiany wzorca użycia hello danych, można także przełączać się między tymi warstwami dostępu w dowolnym momencie. Zmiana warstwy dostępu hello może spowodować naliczenie dodatkowych opłat. Więcej szczegółowych informacji znajduje się w temacie [Pricing and billing for Blob storage accounts](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) (Cennik i rozliczenia — konta usługi Blob Storage).

Więcej szczegółowych informacji na temat kont usługi Blob Storage znajduje się w temacie [Azure Blob Storage: Cool and Hot tiers](../articles/storage/blobs/storage-blob-storage-tiers.md) (Usługa Azure Blob Storage: warstwa chłodna i gorąca).

Przed utworzeniem konta magazynu musi mieć subskrypcję platformy Azure, która jest plan, który zapewnia dostęp do różnych tooa usług platformy Azure. Możesz rozpocząć pracę z platformą Azure od [utworzenia bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/). Po wybraniu toopurchase planu subskrypcji, można wybrać różne [opcji zakupu](https://azure.microsoft.com/pricing/purchase-options/). Jeśli jesteś [subskrybentem portalu MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), możesz uzyskać bezpłatne miesięczne środki na korzystanie z usług Azure, m.in. Azure Storage. Informacje dotyczące cennika woluminów znajdują się w temacie [Azure Storage Pricing ](https://azure.microsoft.com/pricing/details/storage/) (Cennik usługi Azure Storage).

toolearn toocreate konta magazynu, zobacz temat [Utwórz konto magazynu](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) więcej szczegółów. Możesz utworzyć zapasowej too200 jednoznacznie o nazwie konta magazynu z jedną subskrypcją. Aby uzyskać szczegółowe informacje na temat limitów konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../articles/storage/common/storage-scalability-targets.md).

