# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiony i dostępność maszyn wirtualnych na platformie Azure
Azure działa w wielu centrach danych wokół hello world. Tych centrach danych są pogrupowane w toogeographic regionach, zapewniając elastyczność podczas wybierania, gdzie toobuild aplikacji. Jest ważne toounderstand sposób i gdzie maszyn wirtualnych (VM) działają na platformie Azure, wraz z opcji toomaximize wydajności, dostępności i nadmiarowość. Ten artykuł zawiera omówienie hello dostępności i nadmiarowość funkcje platformy Azure.

## <a name="what-are-azure-regions"></a>Co to są regiony platformy Azure?
W określonych regionach geograficznych, takimi jak zachodnie stany USA, "Europa Północna" lub "Azja południowo-wschodnia" jest utworzenie zasobów platformy Azure. Możesz przejrzeć hello [lista regionów i ich lokalizacje](https://azure.microsoft.com/regions/). W każdym regionie wiele centrów danych istnieje tooprovide nadmiarowości i dostępności. To podejście zapewnia elastyczność podczas projektowania aplikacji toocreate maszyn wirtualnych najbliższego tooyour użytkowników i toomeet żadnych prawnych, zgodności lub podatku celów.

## <a name="special-azure-regions"></a>Specjalne regiony platformy Azure
Platforma Azure ma niektóre regiony specjalne, że możesz toouse podczas tworzenia Twojej aplikacji dla celów prawnych lub zgodności. Te regiony specjalne to:

* **Administracja USA — Wirginia** i **Administracja USA — Iowa**
  * Wystąpienie platformy Azure odizolowane fizycznie i na poziomie sieci logicznej dla instytucji rządowych oraz obsługiwane przez sprawdzony pod kątem bezpieczeństwa personel z obywatelstwem Stanów Zjednoczonych. Uwzględnia dodatkowe certyfikaty zgodności, takie jak [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) i [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Dowiedz się więcej o [platformie Azure Government](https://azure.microsoft.com/features/gov/).
* **Chiny Północne** i **Chiny Wschodnie**
  * Te regiony są dostępne za pośrednictwem unikatowe powiązanie między firmą Microsoft a 21Vianet, zgodnie z którymi Microsoft nie przechowuje bezpośrednio hello centrów danych. Dowiedz się więcej na temat [platformy Microsoft Azure w Chinach](http://www.windowsazure.cn/).
* **Niemcy Środkowe** i **Niemcy Północno-Wschodnie**
  * Te regiony są dostępne za pośrednictwem modelu zarządca danych zgodnie z którymi dane klienta pozostaje w Niemczech pod kontrolą systemów T, firma Telekom marki, działający jako hello zarządca niemieckim danych.

## <a name="region-pairs"></a>Pary regionów
Każdy region platformy Azure jest łączyć się z innego regionu w hello tej samej lokalizacji geograficznej (takich jak USA, Europa lub Azja). Takie podejście umożliwia hello replikacji zasoby, takie jak magazyn maszyny Wirtualnej w lokalizacji geograficznej, należy zmniejszyć prawdopodobieństwo hello klęski żywiołowej, unrest cywilnego, awarie zasilania lub awarie sieci fizycznej wpływających na obu regionów jednocześnie. Dodatkowe korzyści wynikające z tworzenia par regionów:

* W przypadku hello szersze awarii Azure jeden region jest priorytety poza każdej pary toohelp zmniejszyć hello toorestore czasu dla aplikacji. 
* Planowane aktualizacji platformy Azure są rozwijane regionów toopaired jeden na czas przestoju toominimize i ryzyko awarii aplikacji.
* Dane nadal tooreside w hello tej samej lokalizacji geograficznej, jako jego pary (z wyjątkiem Brazylia Południowa) dla celów właściwość wymuszania podatku i prawa.

Przykłady par regionów:

| Podstawowy | Pomocniczy |
|:--- |:--- |
| Zachodnie stany USA |Wschodnie stany USA |
| Europa Północna |Europa Zachodnia |
| Azja Południowo-Wschodnia |Azja Wschodnia |

Widać hello pełne [listy regionalnych pary tutaj](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Dostępność funkcji
Niektóre usługi lub funkcje maszyn wirtualnych, takie jak określone rozmiary maszyn wirtualnych lub typy magazynu, są dostępne tylko w określonych regionach. Są także niektóre globalnego usług Azure, które nie wymagają tooselect określonego regionu, takich jak [usługi Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), lub [usługi Azure DNS](../articles/dns/dns-overview.md). tooassist możesz Projektowanie środowiska aplikacji, można sprawdzić hello [dostępności usług platformy Azure w każdym regionie](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Dostępność magazynu
Opis regiony platformy Azure i lokalizacji geograficznych staje się ważne podczas należy wziąć pod uwagę hello opcji replikacji dostępny magazyn. W zależności od typu magazynu hello dostępne są opcje replikacji innej.

**Azure Managed Disks**
* Magazyn lokalnie nadmiarowy (LRS)
  * Replikuje dane trzy razy w regionie hello, w którym utworzono konto magazynu.

**Dyski oparte na koncie magazynu**
* Magazyn lokalnie nadmiarowy (LRS)
  * Replikuje dane trzy razy w regionie hello, w którym utworzono konto magazynu.
* Magazyn strefowo nadmiarowy (ZRS)
  * Replikuje dane trzy razy w dwóch lokalizacjach toothree, w jednym lub dwóch regionach.
* Magazyn geograficznie nadmiarowy (GRS)
  * Replikuje regionu dodatkowej tooa danych będącego setki odległości od regionu podstawowego hello.
* Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)
  * Replikuje obszar dodatkowej tooa danych, tak jak w przypadku GRS, ale także następnie dostarcza dane toohello dostęp tylko do odczytu w lokalizacji dodatkowej hello.

Witaj Poniższa tabela zawiera krótki przegląd hello różnic między typami replikacji magazynu hello:

| Strategia replikacji | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Dane są replikowane między wieloma obiektami. |Nie |Tak |Tak |Tak |
| Dane mogą zostać odczytane z lokalizacji dodatkowej hello i hello lokalizacji głównej. |Nie |Nie |Nie |Tak |
| Liczba kopii danych obsługiwanych w osobnych węzłach. |3 |3 |6 |6 |

Aby uzyskać więcej informacji, zobacz [opcje replikacji magazynu Azure Storage tutaj](../articles/storage/common/storage-redundancy.md). Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [Omówienie usługi Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Koszty magazynowania
Ceny różnią się w zależności od typu magazynu hello i dostępności, który można wybrać.

**Azure Managed Disks**
* Zarządzane dyski Premium bazują na Solid-State dysków (SSD) i zarządzane dyski standardowe bazują na regularne Obracająca dysków. Zarówno Premium i standardowa dysków zarządzanych są naliczane na podstawie hello elastycznie pojemności dysku hello.

**Dyski niezarządzane**
* Magazyn w warstwie Premium nie jest obsługiwana przez Solid-State dysków (SSD) i rozliczany w zależności od pojemności hello hello dysku.
* Magazynu w warstwie standardowa nie jest obsługiwana przez dyski Obracająca regularnych i rozliczany w zależności od pojemności w użyciu hello i potrzeby dostępność magazynu.
  * RA-GRS jest dodatkowe opłaty Transfer danych — replikacja geograficzna hello przepustowości replikacji tego tooanother danych region platformy Azure.

Zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) o cenach informacji na temat hello różnymi typami magazynów i opcji dostępności.

## <a name="availability-sets"></a>Zestawy dostępności
Zestaw dostępności będzie logiczne grupowanie maszyn wirtualnych, który umożliwia Azure toounderstand jak aplikacja jest wbudowana tooprovide nadmiarowości i dostępności. Zaleca się, że co najmniej dwie maszyny wirtualne są tworzone w ramach tooprovide zestaw dostępności dla wysokiej dostępności aplikacji i toomeet hello [99,95% umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Gdy używa jednej maszyny Wirtualnej [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md), hello umowy SLA platformy Azure stosuje nieplanowana konserwacja zdarzeń. 

Zestaw dostępności składa się z dwóch dodatkowych grupowania, które chronić przed awariami sprzętu i zezwolić na aktualizacje toosafely można zastosować — fault domeny (FDs) i Aktualizacja domeny (UDs).

![Rysunek koncepcyjny hello aktualizacji domeny i odporność domeny konfiguracji](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Uzyskać więcej informacji jak toomanage hello dostępności [maszyn wirtualnych systemu Linux](../articles/virtual-machines/linux/manage-availability.md) lub [maszyn wirtualnych systemu Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domeny błędów
Domeny błędów jest logiczną grupą sprzętu źródłowego, które używają wspólne źródło zasilania i przełącznik sieci, podobne tooa stojaku w obrębie centrum danych lokalnych. Podczas tworzenia maszyn wirtualnych w zestawie dostępności, hello platformy Azure automatycznie dystrybuuje maszyn wirtualnych w tych domenach awarii. Takie podejście ogranicza wpływ hello potencjalnych awarii sprzętu fizycznego, awarii sieci lub przerw w działaniu zasilania.

### <a name="update-domains"></a>Domeny aktualizacji
Domena aktualizacji to logiczne grupy używany sprzęt, który może zostać poddane konserwacji lub ponownego uruchomienia na powitania tym samym czasie. Podczas tworzenia maszyn wirtualnych w zestawie dostępności, hello platformy Azure automatycznie dystrybuuje maszyny wirtualne na tych domen aktualizacji. Ta metoda gwarantuje, że co najmniej jedno wystąpienie aplikacji zawsze pozostaje uruchomiona jako hello platformy Azure ulega okresowej konserwacji. kolejność Hello domen aktualizacji, które trwa ponowne uruchamianie nie można kontynuować sekwencyjnie podczas zaplanowanej konserwacji, ale tylko jedna aktualizacja domeny ponownego uruchomienia w czasie.

### <a name="managed-disk-fault-domains"></a>Zarządzane domenach awarii dysku
Maszyny wirtualne korzystające z usługi [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md) są przydzielane do domen błędów dysków zarządzanych w przypadku korzystania z zarządzanego zestawu dostępności. Zapewnia to wyrównanie wszystkich tekst hello zarządzanych dysków dołączonych tooa maszyny Wirtualnej znajdują się w hello tej samej domenie błędów dysków zarządzanych. W zarządzanym zestawie dostępności można tworzyć tylko maszyny wirtualne z użyciem dysków zarządzanych. Hello liczba domen błędów dysków zarządzanych jest zależna od regionu — dwóch lub trzech domen błędów dysków zarządzanych na region.

![Domeny błędów dysku zarządzanego](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> Hello liczba domen błędów dla zestawów zarządzanych dostępności jest zależna od regionu - dwóch lub trzech dla regionu. Witaj poniższej tabeli przedstawiono numer hello na region

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Następne kroki
Można teraz uruchomić toouse te dostępność i nadmiarowość funkcji toobuild środowisku platformy Azure. Aby uzyskać informacje o najlepszych rozwiązaniach, zobacz [Azure availability best practices](../articles/best-practices-availability-checklist.md) (Najlepsze rozwiązania dotyczące dostępności platformy Azure).

