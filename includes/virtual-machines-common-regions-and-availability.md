# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiony i dostępność maszyn wirtualnych na platformie Azure
Platforma Azure działa w wielu centrach danych na całym świecie. Te centra danych są grupowane w regiony geograficzne, dzięki czemu można elastycznie wybierać miejsca do kompilowania aplikacji. Ważne jest, aby zrozumieć, jak i gdzie maszyny wirtualne działają na platformie Azure, a także poznać opcje maksymalizowania wydajności, dostępności i nadmiarowości. Ten artykuł zawiera omówienie funkcji dostępności i nadmiarowości platformy Azure.

## <a name="what-are-azure-regions"></a>Co to są regiony platformy Azure?
W określonych regionach geograficznych, takimi jak zachodnie stany USA, "Europa Północna" lub "Azja południowo-wschodnia" jest utworzenie zasobów platformy Azure. Możesz zapoznać się z [listą regionów i ich lokalizacji](https://azure.microsoft.com/regions/). W każdym regionie istnieje wiele centrów danych, co zapewnia nadmiarowość i dostępność. To podejście zapewnia elastyczność podczas projektowania aplikacji do tworzenia maszyn wirtualnych najbliżej użytkowników i spełnia wszelkie prawnych, zgodności lub podatku celów.

## <a name="special-azure-regions"></a>Specjalne regiony platformy Azure
Platforma Azure ma niektóre regiony specjalne, które chcesz użyć podczas tworzenia Twojej aplikacji dla celów prawnych lub zgodności. Te regiony specjalne to:

* **Administracja USA — Wirginia** i **Administracja USA — Iowa**
  * Wystąpienie platformy Azure odizolowane fizycznie i na poziomie sieci logicznej dla instytucji rządowych oraz obsługiwane przez sprawdzony pod kątem bezpieczeństwa personel z obywatelstwem Stanów Zjednoczonych. Uwzględnia dodatkowe certyfikaty zgodności, takie jak [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) i [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Dowiedz się więcej o [platformie Azure Government](https://azure.microsoft.com/features/gov/).
* **Chiny Północne** i **Chiny Wschodnie**
  * Te regiony są dostępne dzięki unikatowemu partnerstwu firm Microsoft i 21Vianet, w ramach którego firma Microsoft nie zarządza bezpośrednio centrami danych. Dowiedz się więcej na temat [platformy Microsoft Azure w Chinach](http://www.windowsazure.cn/).
* **Niemcy Środkowe** i **Niemcy Północno-Wschodnie**
  * Te regiony są dostępne za pośrednictwem modelu zarządca danych zgodnie z którymi klient dane pozostają w Niemczech pod kontrolą systemów T, firma Telekom marki, działając jako zarządca niemieckim danych.

## <a name="region-pairs"></a>Pary regionów
Każdy region platformy Azure jest powiązany z innym regionem w obrębie tego samego obszaru geograficznego (takiego jak Stany Zjednoczone, Europa i Azja). To podejście umożliwia replikację zasobów, takich jak maszyny wirtualne, między obszarami geograficznymi, co powinno zmniejszyć prawdopodobieństwo tego, że klęski żywiołowe, niepokoje społeczne, przerwy w dostawie prądu lub awarie sieci fizycznych będą wpływać na obydwa regiony na raz. Dodatkowe korzyści wynikające z tworzenia par regionów:

* W przypadku awarii platformy Azure o większym zasięgu jeden region z każdej pary ma przydzielany wyższy priorytet, co pomaga zredukować czas wymagany do przywrócenia aplikacji. 
* Zaplanowane aktualizacje platformy Azure są wdrażane w powiązanych regionach pojedynczo, aby zminimalizować przestoje i ryzyko awarii aplikacji.
* Dla celów związanych z podatkami i egzekwowaniem prawa dane przez cały czas znajdują się w tym samym obszarze geograficznym, co para (z wyjątkiem regionu Brazylia Południowa).

Przykłady par regionów:

| Podstawowy | Pomocniczy |
|:--- |:--- |
| Zachodnie stany USA |Wschodnie stany USA |
| Europa Północna |Europa Zachodnia |
| Azja Południowo-Wschodnia |Azja Wschodnia |

Zobacz pełną [listę par regionów tutaj](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Dostępność funkcji
Niektóre usługi lub funkcje maszyn wirtualnych, takie jak określone rozmiary maszyn wirtualnych lub typy magazynu, są dostępne tylko w określonych regionach. Niektóre globalne usługi platformy Azure, takie jak [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md) lub [Azure DNS](../articles/dns/dns-overview.md), nie wymagają wybrania określonego regionu. Aby ułatwić sobie projektowanie środowiska aplikacji, sprawdź [dostępność usług Azure w poszczególnych regionach](https://azure.microsoft.com/regions/#services). Możesz również [programowo zapytania obsługiwanych rozmiarów maszyn wirtualnych i ograniczenia w każdym regionie](../articles/azure-resource-manager/resource-manager-sku-not-available-errors.md).

## <a name="storage-availability"></a>Dostępność magazynu
Zrozumienie sposobu działania regionów i obszarów geograficznych platformy Azure staje się ważne, jeśli chcesz skorzystać z dostępnych opcji replikacji magazynu. W zależności od typu magazynu masz do wyboru różne opcje replikacji.

**Azure Managed Disks**
* Magazyn lokalnie nadmiarowy (LRS)
  * Umożliwia trzykrotne replikowanie danych w regionie, w którym utworzono konto magazynu.

**Dyski oparte na koncie magazynu**
* Magazyn lokalnie nadmiarowy (LRS)
  * Umożliwia trzykrotne replikowanie danych w regionie, w którym utworzono konto magazynu.
* Magazyn strefowo nadmiarowy (ZRS)
  * Umożliwia trzykrotne replikowanie danych w ramach dwóch lub trzech obiektów, w jednym lub dwóch regionach.
* Magazyn geograficznie nadmiarowy (GRS)
  * Umożliwia replikowanie danych do regionu pomocniczego, który jest oddalony od regionu podstawowego o setki kilometrów.
* Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)
  * Umożliwia replikowanie danych do regionu pomocniczego, podobnie jak w przypadku magazynu GRS, ale oferuje także dostęp tylko do odczytu do danych w lokalizacji pomocniczej.

W poniższej tabeli przedstawiono krótkie podsumowanie różnic między typami replikacji magazynu:

| Strategia replikacji | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Dane są replikowane między wieloma obiektami. |Nie |Tak |Tak |Tak |
| Dane mogą być odczytywane z lokalizacji pomocniczej i z lokalizacji podstawowej. |Nie |Nie |Nie |Tak |
| Liczba kopii danych obsługiwanych w osobnych węzłach. |3 |3 |6 |6 |

Aby uzyskać więcej informacji, zobacz [opcje replikacji magazynu Azure Storage tutaj](../articles/storage/common/storage-redundancy.md). Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Koszty magazynowania
Ceny różnią się w zależności od wybranego typu magazynu i dostępności.

**Azure Managed Disks**
* Zarządzane dyski Premium bazują na Solid-State dysków (SSD) i zarządzane dyski standardowe bazują na regularne Obracająca dysków. Opłaty za dyski Managed Disks w warstwach Premium i Standardowa są naliczane zgodnie z aprowizowaną pojemnością dysku.

**Dyski niezarządzane**
* Magazyn w warstwie Premium nie jest obsługiwana przez Solid-State dysków (SSD) i rozliczany w oparciu o pojemności dysku.
* Magazyn w warstwie Standardowa opiera się na zwykłych dyskach obrotowych, a opłaty są naliczane na podstawie używanej pojemności i żądanej dostępności magazynu.
  * W przypadku magazynów RA-GRS istnieje dodatkowa opłata za transfer danych replikacji geograficznej związana z przepustowością wykorzystywaną do replikowania tych danych do innego regionu platformy Azure.

Zobacz [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/), aby uzyskać informacje na temat różnych typów magazynów i opcji dostępności.

## <a name="availability-sets"></a>Zestawy dostępności
Zestaw dostępności to logiczne grupowanie maszyn wirtualnych w centrum danych, który umożliwia platformie Azure zrozumieć, jak aplikacja jest wbudowana w celu zapewnienia nadmiarowości i dostępności. Zaleca się, że co najmniej dwie maszyny wirtualne są tworzone w ramach zestawu do zapewnienia wysokiej dostępności aplikacji i w celu spełnienia dostępności [99,95% umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Jeśli pojedyncza maszyna wirtualna korzysta z usługi [Azure Premium Storage](../articles/virtual-machines/windows/premium-storage.md), w przypadku zdarzeń nieplanowanej konserwacji obowiązuje umowa SLA platformy Azure. 

Zestaw dostępności składa się z dwóch dodatkowych grup, które chronić przed awariami sprzętu i zezwolić na aktualizacje, które można bezpiecznie można zastosować — fault domeny (FDs) i aktualizację domeny (UDs). Zapoznaj się z dodatkowymi informacjami na temat zarządzania dostępnością [maszyn wirtualnych z systemem Linux](../articles/virtual-machines/linux/manage-availability.md) lub [maszyn wirtualnych z systemem Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domeny błędów
Domena błędów to logiczne grupowanie odpowiednich elementów sprzętu, które współdzielą źródła zasilania i przełącznik sieciowy, podobnie jak w przypadku regału w lokalnym centrum danych. Podczas tworzenia maszyn wirtualnych w zestawie dostępności platforma Azure automatycznie rozdziela maszyny wirtualne między domeny błędów. To podejście ogranicza wpływ potencjalnych awarii sprzętu fizycznego, przestojów sieci lub przerw w dostawie prądu.

### <a name="update-domains"></a>Domeny aktualizacji
Domena aktualizacji to logiczne grupowanie odpowiednich elementów sprzętu, które mogą być w tym samym czasie poddawane konserwacji lub ponownie uruchamiane. Podczas tworzenia maszyn wirtualnych w zestawie dostępności platforma Azure automatycznie rozdziela maszyny wirtualne między domeny aktualizacji. To podejście zapewnia, że zawsze działa co najmniej jedno wystąpienie aplikacji, gdy platforma Azure jest poddawana okresowej konserwacji. Podczas planowanej konserwacji domeny aktualizacji mogą nie być ponownie uruchamiane kolejno, ale w danym momencie tylko jedna domena aktualizacji jest uruchamiana ponownie.

### <a name="managed-disk-fault-domains"></a>Zarządzane domenach awarii dysku
Maszyny wirtualne korzystające z usługi [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md) są przydzielane do domen błędów dysków zarządzanych w przypadku korzystania z zarządzanego zestawu dostępności. Dzięki takiemu dopasowaniu wszystkie dyski zarządzane dołączone do maszyny wirtualnej działają w tej samej domenie błędów dysku zarządzanego. W zarządzanym zestawie dostępności można tworzyć tylko maszyny wirtualne z użyciem dysków zarządzanych. Liczba domen błędów dysku zarządzanego zależy od regionu — dwie lub trzy domeny błędów dysku zarządzanego na region. Możesz przeczytać dodatkowe informacje dotyczące tych zarządzanych domen błędów dysku dla [maszyn wirtualnych systemu Linux](../articles/virtual-machines/linux/manage-availability.md?#use-managed-disks-for-vms-in-an-availability-set) lub [maszyn wirtualnych systemu Windows](../articles/virtual-machines/linux/manage-availability.md?#use-managed-disks-for-vms-in-an-availability-set).

## <a name="availability-zones"></a>Dostępność strefy

[Dostępność strefy](../articles/availability-zones/az-overview.md) ustawia zamiast dostępności (wersja zapoznawcza), rozwiń poziom kontroli należy zachować dostępność aplikacje i dane maszyn wirtualnych. Strefa dostępności jest fizycznie oddzielnych stref w obrębie regionu platformy Azure. Istnieją trzy strefy dostępności na obsługiwany region platformy Azure. Każdej strefy dostępności ma oddzielny zasilania źródła, sieci i chłodzenia i jest logicznie oddzielona od innych stref dostępności w obrębie regionu Azure. Przez projektowania rozwiązań do użycia w strefach replikowanych maszyn wirtualnych, można chronić aplikacji i danych z utraty możliwości Centrum danych. W przypadku złamania zabezpieczeń jednego strefy, następnie replikowanych aplikacje i dane są dostępne natychmiast w innej strefie. 

![Dostępność strefy](./media/virtual-machines-common-regions-and-availability/three-zones-per-region.png)

[!INCLUDE [availability-zones-preview-statement.md](availability-zones-preview-statement.md)]

Dowiedz się więcej o wdrażaniu [Windows](../articles/virtual-machines/windows/create-powershell-availability-zone.md) lub [Linux](../articles/virtual-machines/linux/create-cli-availability-zone.md) maszyny Wirtualnej w strefie dostępności.

## <a name="next-steps"></a>Następne kroki
Możesz teraz rozpocząć korzystanie z tych funkcji dostępności i nadmiarowości podczas kompilowania środowiska platformy Azure. Aby uzyskać informacje o najlepszych rozwiązaniach, zobacz [Azure availability best practices](../articles/best-practices-availability-checklist.md) (Najlepsze rozwiązania dotyczące dostępności platformy Azure).

