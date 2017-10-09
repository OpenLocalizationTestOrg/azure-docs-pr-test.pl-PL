# <a name="azure-managed-disks-overview"></a>Informacje o dyskach zarządzanych platformy Azure

Zarządzane dysku systemu Azure upraszcza zarządzanie dysku dla maszyn wirtualnych IaaS platformy Azure, zarządzając hello [kont magazynu](../articles/storage/common/storage-introduction.md) skojarzone z hello dysków maszyny Wirtualnej. Masz tylko typ hello toospecify ([Premium](../articles/storage/common/storage-premium-storage.md) lub [standardowe](../articles/storage/common/storage-standard-storage.md)) i rozmiar hello dysku należy i Azure tworzy i zarządza hello dysku.

## <a name="benefits-of-managed-disks"></a>Korzyści wynikające z dysków zarządzanych

Spójrzmy na kilka korzyści hello uzyskać przy użyciu dysków zarządzanych w programie ten film Channel 9 [lepsze odporności maszyny Wirtualnej Azure z dyskami zarządzane](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Proste i skalowalne wdrażanie maszyny Wirtualnej

Zarządzane przechowywania dojść dysków dla Ciebie tle hello. Wcześniej trzeba było toocreate kont toohold hello dysków w magazynie (pliki VHD) na maszynach wirtualnych platformy Azure. Podczas skalowania w, trzeba było toomake się, że utworzona dodatkowych kont magazynu, więc nie przekracza hello limitu IOPS dla magazynu za pomocą dowolnego z dysków. W przypadku zarządzanych dysków obsługi magazynu nie jest już ograniczeniem limity konta magazynu hello (takie jak IOPS 20 000 / konta). Możesz również już toocopy kont magazynu toomultiple niestandardowych obrazów (pliki VHD). Można nimi zarządzać w centralnej lokalizacji — jedno konto magazynu na region platformy Azure — i używać ich toocreate setki maszyn wirtualnych w ramach subskrypcji.

Dysków zarządzanych umożliwi toocreate się too10, wirtualna 000 **dysków** w ramach subskrypcji, która umożliwi toocreate tysięcy z **maszyn wirtualnych** w ramach jednej subskrypcji. Ta funkcja także dodatkowo zwiększa skalowalność hello [zestawy skalowania maszyny wirtualnej (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) , zezwalając toocreate zapasowych maszyn wirtualnych tooa tysięcy VMSS, przy użyciu obrazu z witryny Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Niezawodność zestawów dostępności

Dyski zarządzane zapewnia większą niezawodność zestawów dostępności zapewniając, że hello dyski [maszyn wirtualnych w zestawie dostępności](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) są wystarczająco odizolowane od siebie nawzajem tooavoid pojedynczych punktów awarii. Robi to automatycznie umieszczając dyski hello jednostki skalowania innego magazynu (sygnatury). Sygnatura nie powiedzie się ze względu na błąd toohardware lub oprogramowania, tylko hello wystąpień maszyny Wirtualnej z dyskami tych sygnatur zakończyć się niepowodzeniem. Na przykład załóżmy, że korzystasz z aplikacji działających na pięciu maszynach i hello maszyn wirtualnych znajdują się w zestawie dostępności. Witaj dysków dla tych maszyn wirtualnych nie wszystkie przechowywane w hello sygnatury takie same, więc jeśli jednej sygnatury ulegnie awarii, hello innych wystąpień aplikacji hello nadal toorun.

### <a name="highly-durable-and-available"></a>Duża trwałość i wysoka dostępność

Dyski platformy Azure zaprojektowano tak, aby zapewniały 99,999% dostępności. Zatrzymaj, łatwiej wiedząc, że użytkownik ma trzy repliki danych, która umożliwia wysoka trwałość. Jeśli jeden lub dwa nawet replik występują problemy, hello pozostałych replik zapewnienia trwałości danych oraz wysokiej tolerancji przed awariami. Ta architektura pomogła platformie Azure w zapewnieniu niezawodności klasy korporacyjnej dla dysków IaaS przez długi czas z rocznym współczynnikiem awarii w wysokości 0%, co stawia ją w czołówce branży. 

### <a name="granular-access-control"></a>Precyzyjną kontrolę dostępu

Można użyć [based kontroli dostępu (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign określonych uprawnień dla tooone dysków zarządzanych lub więcej użytkowników. Zarządzane dyski ujawnia różne operacje, w tym do odczytu, zapisu (Utwórz/Aktualizuj), usuwania i pobierania [sygnatury dostępu współdzielonego (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) hello dysku. Operacje związane z dostępem tooonly hello można przyznać osoby musi tooperform jego pracy. Na przykład jeśli nie chcesz toocopy osoba konto magazynu tooa dysków zarządzanych, możesz nie toogrant dostępu toohello eksportu akcji dla tego dysku zarządzanego. Podobnie, jeśli nie chcesz, aby osoba toouse toocopy identyfikatora URI połączenia SAS, dysków zarządzanych, możesz nie toogrant toohello tego uprawnienia dysków zarządzanych.

### <a name="azure-backup-service-support"></a>Obsługa usługi Kopia zapasowa Azure
Usługa Kopia zapasowa Azure za pomocą dysków zarządzanych toocreate zadania tworzenia kopii zapasowej na podstawie czasu tworzenia kopii zapasowych, łatwe przywrócenie maszyny Wirtualnej i zasady przechowywania kopii zapasowych. Dyski zarządzane obsługują tylko lokalnie nadmiarowego magazynu (LRS) jako opcję replikacji hello; oznacza to, że przechowuje trzy kopie danych hello w pojedynczym regionie. Regionalnej awarii, należy wykonać kopię zapasową dysków maszyny Wirtualnej w innym regionie przy użyciu [usługi Kopia zapasowa Azure](../articles/backup/backup-introduction-to-azure-backup.md) i konto magazynu GRS jako magazynu kopii zapasowych. Obecnie kopia zapasowa Azure obsługuje danych rozmiary dysków zapasowych too1TB kopii zapasowej. Dowiedz się więcej o tym w [usługi przy użyciu kopii zapasowej Azure dla maszyn wirtualnych z dyskami zarządzane](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Cennik i rozliczenia

Podczas korzystania z dysków zarządzanych, zastosuj następujące zagadnienia dotyczące rozliczeń hello:
* Typ magazynu

* Rozmiar dysku

* Liczba transakcji

* Wychodzące transfery danych

* Zarządzane migawki dysków (kopia zapełniony dysk)

Spójrzmy bliższe spojrzenie na te.

**Typ magazynu:** zarządzane dysków oferuje 2 warstwy wydajności: [Premium](../articles/storage/common/storage-premium-storage.md) (oparte na dysk SSD) i [standardowe](../articles/storage/common/storage-standard-storage.md) (oparte na dysk twardy). rozliczeń Hello zarządzanych dysku zależy od tego, jakiego typu magazynu wybrano hello dysku.


**Rozmiar dysku**: rozliczeń dla dysków zarządzanych zależy od rozmiaru hello elastycznie hello dysku. Azure mapy hello toohello elastycznie rozmiaru (zaokrąglona w górę) najbliższej opcja dysków zarządzanych określone w poniższych tabelach hello. Każdego tooone mapowania dysków zarządzanych z hello obsługiwane rozmiary elastycznie i jest on rozliczany odpowiednio. Na przykład jeśli tworzenie standardowych dysków zarządzanych i określ elastycznie rozmiaru 200 GB, są rozliczane zgodnie z harmonogramem hello cen hello typ dysku S20 w warstwie.

W tym miejscu są dostępne dla dysków zarządzanych w warstwie premium rozmiary dysków hello:

| **Premium zarządzane <br>typ dysku** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Rozmiar dysku        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


W tym miejscu są dostępne dla standardowych dysków zarządzanych rozmiary dysków hello:

| **Standard zarządzane <br>typ dysku** | **S4** | **S6** | **S10 W WARSTWIE** | **S20** | **S30 W WARSTWIE** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Rozmiar dysku        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Liczba transakcji**: są rozliczane hello liczbę transakcji, które można wykonywać na standardowych dysków zarządzanych. Nie ma żadnych kosztów transakcji dla dysków zarządzanych w warstwie premium.

**Transfer danych wychodzących**: [transfery danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/) (danych wychodzących z centrów danych Azure) powodują Naliczanie opłat za zużycie przepustowości.

Aby uzyskać szczegółowe informacje o cenach dla dysków zarządzanych, zobacz [zarządzane cennik dysków](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Dyski zarządzane migawki

Migawka zarządzanych jest tylko do odczytu pełnej kopii dysku zarządzanego, który jest przechowywany jako standardowych dysków zarządzanych przez domyślny. Z migawki można tworzyć kopie zapasowe dysków zarządzanych w dowolnym momencie w czasie. Te migawki istnieje niezależnie od hello dysku źródłowego i mogą być używane toocreate nowych dysków zarządzanych. Są one rozliczane na podstawie rozmiaru hello używane. Na przykład jeśli utworzysz migawki dysków zarządzanych z elastycznie 64 GB i rozmiaru rzeczywistego używanych danych wynosi 10 GB migawki będą naliczane tylko za hello używany rozmiar danych wynosi 10 GB.  

[Przyrostowe migawki](../articles/virtual-machines/windows/incremental-snapshots.md) nie są obecnie obsługiwane w przypadku dysków zarządzanych, ale będą obsługiwane w przyszłości hello.

toolearn więcej na temat sposobu migawki toocreate z zarządzanych dysków można znaleźć na te zasoby:

* [Tworzenie kopii wirtualnego dysku twardego przechowywanej jako dysk zarządzany przy użyciu migawek w systemie Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Tworzenie kopii wirtualnego dysku twardego przechowywanej jako dysk zarządzany przy użyciu migawek w systemie Linux](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Obrazy

Dyski zarządzane obsługują także tworzenie zarządzanych niestandardowego obrazu. Można utworzyć obrazu, z Twojego niestandardowego pliku VHD na koncie magazynu lub bezpośrednio z ogólnych maszyny Wirtualnej (sys prepped). To są zapisywane w jednym obrazie wszystkie zarządzane dysku skojarzonego z maszyną Wirtualną, w tym zarówno hello systemu operacyjnego i dysków z danymi. Ta umożliwia tworzenie setki maszyn wirtualnych przy użyciu niestandardowego obrazu bez hello konieczne toocopy lub zarządzać kont magazynu.

Aby uzyskać informacje na temat tworzenia obrazów można znaleźć na powitania następujące artykuły:
* [Jak toocapture zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure](../articles/virtual-machines/windows/capture-image-resource.md)
* [Jak toogeneralize i przechwycenia maszyny wirtualnej systemu Linux przy użyciu hello Azure CLI 2.0](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Obrazy i migawki

Często Zobacz hello word "obrazu" używana z maszynami wirtualnymi i spowoduje to wyświetlenie "migawki" również. Jest ważne toounderstand hello różnica między tymi. W przypadku zarządzanych dysków może potrwać obraz uogólniony maszynę Wirtualną, która alokację. Ten obraz będzie zawierać wszystkie hello toohello dołączonych dysków maszyny Wirtualnej. Można użyć tego obrazu toocreate nowej maszyny Wirtualnej, a uwzględni wszystkie dyski hello.

Migawka jest kopii dysku w momencie hello w czasie, który przyjmuje. Ma zastosowanie tylko tooone dysku. Jeśli masz maszynę Wirtualną, która zawiera tylko jeden dysk (hello systemu operacyjnego), można wykonać migawki lub obraz go i tworzenie maszyny Wirtualnej z migawki hello lub obraz powitania.

Co zrobić, jeśli maszyna wirtualna ma pięć dysków i ich są rozkładane? Można utworzyć migawkę każdej hello dysków, ale nie informacji w ramach hello wirtualna stanu hello dysków hello — Witaj migawki tylko wiedzieć o tym jeden dysk. W takim przypadku migawki hello wymagałoby toobe koordynowane ze sobą, a który nie jest obecnie obsługiwany.

## <a name="managed-disks-and-encryption"></a>Dyski zarządzane i szyfrowania

Istnieją dwa rodzaje toodiscuss szyfrowania dysków toomanaged odwołania. Witaj najpierw jedna jest magazynu usługi szyfrowania (SSE), które jest wykonywane przez usługę Magazyn hello. Witaj drugim jest szyfrowania dysków Azure, które można włączyć na powitania systemu operacyjnego i dysków z danymi dla maszyn wirtualnych.

### <a name="storage-service-encryption-sse"></a>Szyfrowanie usługi Magazyn (SSE)

[Szyfrowanie usługi Magazyn Azure](../articles/storage/common/storage-service-encryption.md) zapewnia szyfrowanie na rest i chronić Twoje toomeet danych Twojej organizacji zobowiązań zabezpieczeń i zgodności. SSE jest domyślnie włączona dla wszystkich dysków zarządzanych, migawki i obrazów we wszystkich regionach hello, gdzie dostępna jest opcja dysków zarządzanych. Uruchamianie 10 czerwca 2017 wszystkie nowe zarządzane dyski/migawek/obrazów i nowych danych tooexisting zarządzane dyski są automatycznie szyfrowane podczas spoczynku z kluczami zarządzany przez firmę Microsoft.  Odwiedź hello [strony często zadawane pytania dotyczące dysków zarządzanych](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) więcej szczegółów.


### <a name="azure-disk-encryption-ade"></a>Szyfrowanie dysków Azure (ADE)

Szyfrowanie dysków Azure umożliwia hello tooencrypt systemu operacyjnego i dysków danych używanych przez maszyny wirtualne IaaS. W tym dyski zarządzanych. W systemie Windows hello dyski są szyfrowane za pomocą technologii szyfrowania BitLocker standardowych. Dla systemu Linux dyski hello są szyfrowane za pomocą technologii hello DM-Crypt. To jest zintegrowany z usługą Azure Key Vault tooallow możesz toocontrol i zarządzać kluczami szyfrowania dysku hello. Aby uzyskać więcej informacji, zobacz [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat zarządzanych dysków zapoznaj się z toohello następujące artykuły.

### <a name="get-started-with-managed-disks"></a>Rozpoczynanie pracy z usługą Managed Disks

* [Tworzenie maszyny wirtualnej przy użyciu usługi Resource Manager i programu PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../articles/virtual-machines/linux/quick-create-cli.md)

* [Dołączanie danych zarządzanych tooa dysku maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Dodawanie dysków zarządzanych w tooa maszyny Wirtualnej systemu Linux](../articles/virtual-machines/linux/add-disk.md)

* [Zarządzane dysków programu PowerShell przykładowe skrypty](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Dysków zarządzanych w szablonach usługi Azure Resource Manager](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Porównanie dysków zarządzanych opcje magazynu

* [Magazyn w warstwie Premium i dysków](../articles/storage/common/storage-premium-storage.md)

* [Standardowy magazyn i dyski](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>Wskazówki dotyczące obsługi

* [Migrowanie z usług AWS i innych platform tooManaged dysków na platformie Azure](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Skonwertuj dyski toomanaged maszynach wirtualnych platformy Azure na platformie Azure](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
