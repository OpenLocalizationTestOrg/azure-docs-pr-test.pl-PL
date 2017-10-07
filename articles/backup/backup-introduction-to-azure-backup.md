---
title: aaaWhat jest kopia zapasowa Azure? | Microsoft Docs
description: "Użyj tooback kopia zapasowa Azure i przywracanie danych i obciążeń z serwerów z systemem Windows, stacji roboczych systemu Windows, serwery programu System Center DPM i maszyn wirtualnych platformy Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "tworzenie i przywracanie kopii zapasowej; recovery services; rozwiązania kopii zapasowych"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Omówienie funkcji hello w usłudze Kopia zapasowa Azure
Kopia zapasowa Azure to hello bazujących na platformie Azure usługa może zużywać tooback (lub ochrona) i przywracanie danych w hello firmy Microsoft w chmurze. Usługa Azure Backup pozwala zastąpić dotychczasowe rozwiązania tworzenia kopii zapasowych, istniejące lokalnie lub poza siedzibą firmy, rozwiązaniem opartym na chmurze, które jest niezawodne, bezpieczne i konkurencyjne cenowo. Kopia zapasowa Azure oferuje wiele składników, które można pobrać i zainstalować na komputerze, odpowiednie hello, serwera, lub w chmurze hello. składnik Hello lub agenta, który można wdrożyć zależy od co tooprotect. Wszystkie składniki usługi Kopia zapasowa Azure (niezależnie od tego, czy są one chronione danych w sieci lokalnej lub w chmurze hello) mogą być używane tooback zapasowej magazyn usług odzyskiwania tooa danych na platformie Azure. Zobacz hello [tabeli składników usługi Kopia zapasowa Azure](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (dalszej części tego artykułu) informacji o którym składnik toouse tooprotect określonych danych, aplikacji lub obciążeń.

[Obejrzyj wideo z omówieniem usługi Azure Backup](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Dlaczego warto używać usługi Azure Backup?
Tradycyjnych rozwiązań usprawnionych tootreat hello chmurze jako punktu końcowego lub miejscem docelowym magazynu statyczne, podobne toodisks lub z taśmą. Gdy ta metoda jest proste, jest ograniczona i nie w pełni korzystać z możliwości platformy chmury, który tłumaczy tooan kosztowne, nieefektywne rozwiązanie. Innych rozwiązań jest dość kosztowna, ponieważ przechodzili płatności dla niewłaściwego typu hello magazynu lub magazynu, który nie jest potrzebny. Innych rozwiązań często są mało wydajne, ponieważ nie oferują możesz typu hello lub ilość miejsca w magazynie, które są potrzebne, lub zadania administracyjne wymagają zbyt dużo czasu. Natomiast usługa Azure Backup oferuje następujące kluczowe korzyści:

**Automatyczne zarządzanie** — środowisk hybrydowych często wymagają magazynu heterogenicznego - niektórych lokalnych i hello niektórych w chmurze. W usłudze Azure Backup nie płaci się za korzystanie z lokalnych urządzeń magazynujących. Usługa Azure Backup automatycznie przydziela pojemność i zarządza magazynem kopii zapasowych, przy czym użytkownik płaci tylko za faktyczne użycie. Płatności jako — użytkownik użycia oznacza, że płacisz za magazyn hello, które zostaną zużyte. Aby uzyskać więcej informacji, zobacz hello [Azure artykuł](https://azure.microsoft.com/pricing/details/backup).

**Skalowanie nieograniczone** — kopia zapasowa Azure korzysta hello bazowy zasilania i nieograniczone skali hello Azure cloud toodeliver wysokiej dostępności — nie obsługi lub monitorowania obciążenia. Możesz skonfigurować alerty tooprovide informacji o zdarzeniach, ale nie ma potrzeby tooworry o wysokiej dostępności dla danych w chmurze hello.

**Wiele opcji magazynowania** — aspektem wysokiej dostępności jest replikacja magazynu. Usługa Azure Backup oferuje dwa typy replikacji: [magazyn lokalnie nadmiarowy](../storage/common/storage-redundancy.md#locally-redundant-storage) i [magazyn geograficznie nadmiarowy](../storage/common/storage-redundancy.md#geo-redundant-storage). Wybierz opcję magazynu kopii zapasowych hello zależności od potrzeb:

* Magazyn lokalnie nadmiarowy (LRS) są replikowane trzy razy (tworzy trzy kopie danych) w parach centrum danych w hello tego samego regionu. Magazyn LRS to ekonomiczna opcja ochrony danych przed awariami sprzętu lokalnego.

* Magazyn geograficznie nadmiarowy (GRS) replikuje regionu pomocniczego tooa danych (setki mil od lokalizacji głównej hello hello źródła danych). Magazyn GRS kosztuje więcej niż LRS, ale zapewnia wyższy poziom trwałości danych nawet w przypadku wystąpienia awarii regionalnej.

**Transfer danych nieograniczone** — kopia zapasowa Azure nie istnieje limit hello ilość ruchu przychodzącego lub transfer danych wychodzących. Kopia zapasowa Azure nie również pobierać dla hello przesyłanych danych. Jeśli używasz hello Import/Eksport Azure usługa tooimport dużych ilości danych, istnieje jednak koszt związany z danymi dla ruchu przychodzącego. Aby uzyskać więcej informacji o tym koszcie, zobacz [Offline-backup workflow in Azure Backup](backup-azure-backup-import-export.md) (Przepływ pracy tworzenia kopii zapasowej offline w usłudze Azure Backup). Wychodzące danych odwołuje się toodata przekazywane z magazynu usług odzyskiwania podczas operacji przywracania.

**Szyfrowanie danych** — umożliwia szyfrowanie danych bezpiecznego transmisji i przechowywania danych w chmurze publicznej hello. Hello lokalnie hasło szyfrowania są przechowywane i nigdy nie jest przekazywane lub przechowywane na platformie Azure. Jeśli jest konieczne toorestore żadnych danych hello tylko masz hasło szyfrowania, lub klucza.

**Kopia zapasowa spójna w aplikacji** — czy wykonywanie kopii zapasowej serwera plików, maszyny wirtualnej lub bazy danych SQL, nie trzeba tooknow punkt odzyskiwania zawiera wszystkie wymagane dane kopii zapasowej hello toorestore. Kopia zapasowa Azure stanowi spójnych z aplikacją kopii zapasowych, które zapewniają dodatkowe poprawki nie są wymagane toorestore hello danych. Przywracanie spójności danych aplikacji skraca czas przywracania hello, umożliwiając tooquickly tooa zwracany w stanie uruchomienia.

**Przechowywania długoterminowego** — zamiast przełączania kopie zapasowe z tootape dysku i przenoszenie hello tooan poza nim lokalizacji taśm, możesz użyć Azure do przechowywania krótko- i długoterminowej. Azure nie ograniczają hello długość czasu danych pozostaje w magazynie usług odzyskiwania lub kopii zapasowej. Dane możesz przechowywać w magazynie tak długo, jak chcesz. Usługa Azure Backup ma limit 9999 punktów odzyskiwania dla każdego chronionego wystąpienia. Zobacz hello [kopii zapasowej i przechowywania](backup-introduction-to-azure-backup.md#backup-and-retention) w tym artykule wyjaśnienie sposobu ten limit może mieć wpływ na potrzeby tworzenia kopii zapasowej.  

## <a name="which-azure-backup-components-should-i-use"></a>Jakich składników usługi Azure Backup mam użyć?
Jeśli nie masz pewności, który składnik kopia zapasowa Azure działa Twoje potrzeby, zobacz hello w poniższej tabeli informacji o to, co może chronić każdego składnika. Hello Azure portal udostępnia kreatora, jest wbudowana hello portalu, tooguide przez wybranie hello toodownload składnika i wdrożyć. Kreator Hello, który jest częścią hello Tworzenie magazynu usług odzyskiwania, poprowadzi Cię przez kroki hello wybierając celu kopii zapasowej i wybierając pozycję hello tooprotect danych lub aplikacji.

| Składnik | Korzyści | Limity | Co jest chronione? | Gdzie są przechowywane kopie zapasowe? |
| --- | --- | --- | --- | --- |
| Agent usługi Azure Backup (MARS) |<li>Tworzy kopię zapasową plików i folderów w fizycznym lub wirtualnym systemie operacyjnym Windows (maszyny wirtualne mogą być lokalne lub na platformie Azure)<li>Nie jest wymagany oddzielny serwer kopii zapasowych. |<li>Tworzenie kopii zapasowej 3 razy dziennie <li>Brak zależności od aplikacji; przywracanie tylko na poziomie plików, folderów i woluminów, <li>  Brak obsługi systemu Linux. |<li>Pliki, <li>Foldery |Magazyn usługi Recovery Services |
| System Center DPM |<li>Migawki z uwzględnieniem aplikacji (usługa VSS)<li>Pełne elastyczność program tootake kopii zapasowych<li>Poziom szczegółowości odzyskiwania (wszystkie)<li>Możliwość użycia magazynu usługi Recovery Services<li>Obsługa systemu Linux na maszynach wirtualnych programu VMware i funkcji Hyper-V <li>Wykonywanie kopii zapasowych i przywracanie maszyn wirtualnych VMware za pomocą programu DPM 2012 R2 |Nie można tworzyć kopii zapasowych obciążeń Oracle.|<li>Pliki, <li>Foldery,<li> Woluminy, <li>Maszyny wirtualne,<li> Aplikacje,<li> Obciążenia |<li>Magazyn usługi Recovery Services,<li> Dysk dołączony lokalnie,<li>  Taśmy (tylko lokalnie) |
| Azure Backup Server |<li>Migawki z uwzględnieniem aplikacji (usługa VSS)<li>Pełne elastyczność program tootake kopii zapasowych<li>Poziom szczegółowości odzyskiwania (wszystkie)<li>Możliwość użycia magazynu usługi Recovery Services<li>Obsługa systemu Linux na maszynach wirtualnych programu VMware i funkcji Hyper-V<li>Wykonywanie kopii zapasowych i przywracanie maszyn wirtualnych VMware <li>Nie wymaga licencji programu System Center |<li>Nie można tworzyć kopii zapasowych obciążeń Oracle.<li>Zawsze wymaga aktywnej subskrypcji platformy Azure<li>Brak obsługi tworzenia kopii zapasowej na taśmie |<li>Pliki, <li>Foldery,<li> Woluminy, <li>Maszyny wirtualne,<li> Aplikacje,<li> Obciążenia |<li>Magazyn usługi Recovery Services,<li> Dysk dołączony lokalnie |
| Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |<li>Natywne kopie zapasowe w systemach Windows/Linux<li>Nie ma konieczności instalowania określonego agenta<li>Tworzenie kopii zapasowych na poziomie sieci szkieletowej nie wymaga infrastruktury kopii zapasowej |<li>Tworzenie kopii zapasowych maszyn wirtualnych raz dziennie <li>Przywracanie maszyn wirtualnych tylko na poziomie dysku<li>Nie można utworzyć kopii zapasowych lokalnie |<li>Maszyny wirtualne, <li>Wszystkie dyski (przy użyciu programu PowerShell) |<p>Magazyn usługi Recovery Services</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Co to są hello scenariusze wdrażania poszczególnych składników?
| Składnik | Czy można wdrożyć w systemie Azure? | Czy można wdrożyć lokalnie? | Obsługiwany magazyn docelowy |
| --- | --- | --- | --- |
| Agent usługi Azure Backup (MARS) |<p>**Tak**</p> <p>agent usługi Kopia zapasowa Azure Hello może zostać wdrożony w żadnej maszyny Wirtualnej serwera systemu Windows, który działa na platformie Azure.</p> |<p>**Tak**</p> <p>agent usługi Kopia zapasowa Hello można wdrożyć maszyny Wirtualnej systemu Windows Server lub komputera fizycznego.</p> |<p>Magazyn usługi Recovery Services</p> |
| System Center DPM |<p>**Tak**</p><p>Dowiedz się więcej o [jak tooprotect obciążeń na platformie Azure przy użyciu programu System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Tak**</p> <p>Dowiedz się więcej o [jak tooprotect obciążeń i maszyn wirtualnych w centrum danych](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Dysk dołączony lokalnie,</p> <p>Magazyn usługi Recovery Services,</p> <p>taśmy (tylko lokalnie)</p> |
| Azure Backup Server |<p>**Tak**</p><p>Dowiedz się więcej o [jak tooprotect obciążeń na platformie Azure za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>**Tak**</p> <p>Dowiedz się więcej o [jak tooprotect obciążeń na platformie Azure za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>Dysk dołączony lokalnie,</p> <p>Magazyn usługi Recovery Services</p> |
| Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |<p>**Tak**</p><p>Część sieci szkieletowej Azure</p><p>Składnik przeznaczony do [tworzenia kopii zapasowych maszyn wirtualnych platformy Azure w modelu infrastruktura jako usługa (IaaS) ](backup-azure-vms-introduction.md).</p> |<p>**Nie**</p> <p>Użyj programu System Center DPM tooback zapasowych maszyn wirtualnych w centrum danych.</p> |<p>Magazyn usługi Recovery Services</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Dla których aplikacji i obciążeń można tworzyć kopie zapasowe?
w poniższej tabeli Hello zawiera macierz hello danych i obciążeń, które mogą być chronione przy użyciu usługi Kopia zapasowa Azure. Witaj kopia zapasowa Azure rozwiązania kolumna ma linki toohello wdrożenia dokumentacji dla tego rozwiązania. Każdy składnik usługi Azure Backup można wdrożyć w środowisku klasycznym (wdrożenie programu Service Manager) lub modelu wdrożenia Menedżera zasobów.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Dane lub obciążenie | Środowisko źródłowe | Rozwiązanie Azure Backup |
| --- | --- | --- |
| Pliki i foldery |Windows Server |<p>[Agent usługi Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Pliki i foldery |Komputer z systemem Windows |<p>[Agent usługi Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Maszyna wirtualna funkcji Hyper-V (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Maszyna wirtualna funkcji Hyper-V (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure Backup agent),</p> <p>[Serwer kopii zapasowej systemu Azure](backup-azure-microsoft-azure-backup.md) (w tym hello Azure Backup agent)</p> |
| Maszyny wirtualne IaaS platformy Azure (Windows) |uruchomione na platformie Azure |[Azure Backup (rozszerzenie maszyny wirtualnej)](backup-azure-vms-introduction.md) |
| Maszyny wirtualne IaaS platformy Azure (Linux) |uruchomione na platformie Azure |[Azure Backup (rozszerzenie maszyny wirtualnej)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Obsługa systemu Linux
Witaj poniższej tabeli przedstawiono składniki usługi Kopia zapasowa Azure hello, o obsługę systemu Linux.  

| Składnik | Obsługa w systemie Linux (zatwierdzonym przez Azure) |
| --- | --- |
| Agent usługi Azure Backup (MARS) |Nie (tylko agent oparty na systemie Windows) |
| System Center DPM |<li> Spójna na poziomie plików kopia zapasowa maszyn wirtualnych gościa z systemem Linux dla funkcji Hyper-V i programu VMWare<br/> <li> Przywracanie maszyn wirtualnych gościa z systemem Linux dla funkcji Hyper-V i programu VMWare </br> </br>  *Spójna na poziomie plików kopia zapasowa nie jest dostępna dla maszyny wirtualnej platformy Azure* <br/> |
| Azure Backup Server |<li>Spójna na poziomie plików kopia zapasowa maszyn wirtualnych gościa z systemem Linux dla funkcji Hyper-V i programu VMWare<br/> <li> Przywracanie maszyn wirtualnych gościa z systemem Linux dla funkcji Hyper-V i programu VMWare </br></br> *Spójna na poziomie plików kopia zapasowa nie jest dostępna dla maszyny wirtualnej platformy Azure*  |
| Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |Spójna na poziomie aplikacji kopia zapasowa korzystająca ze [struktury skryptów uruchamianych przed utworzeniem i po utworzeniu kopii zapasowej](backup-azure-linux-app-consistent.md)<br/> [Szczegółowe odzyskiwanie plików](backup-azure-restore-files-from-vm.md)<br/> [Przywracanie wszystkich dysków maszyn wirtualnych](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Przywracanie maszyny wirtualnej](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Korzystanie z maszyn wirtualnych usługi Premium Storage przy użyciu usługi Azure Backup
Usługa Azure Backup chroni maszyny wirtualne usługi Premium Storage. Usługa Azure Premium Storage jest dysków półprzewodnikowych (SSD) — na podstawie magazynu zaprojektowane toosupport/O wykonujących obciążeń. Usługa Premium Storage jest atrakcyjna dla obciążeń maszyn wirtualnych. Aby uzyskać więcej informacji na temat magazyn w warstwie Premium, zobacz artykuł hello [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Tworzenie kopii zapasowej maszyn wirtualnych usługi Premium Storage
Podczas tworzenia kopii zapasowych maszyn wirtualnych z magazynu Premium, hello usługi Kopia zapasowa tworzy tymczasowej lokalizacji tymczasowej, o nazwie "AzureBackup-", w hello konta Premium Storage. rozmiar Hello hello lokalizacji wystawiania jest rozmiar równy toohello migawki punktu odzyskiwania hello. Upewnij się, że hello konta Premium Storage jest odpowiednia ilość wolnego miejsca tooaccommodate hello tymczasowej lokalizacji tymczasowej. Aby uzyskać więcej informacji, zobacz artykuł hello [ograniczenia magazynu premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Po zakończeniu zadania tworzenia kopii zapasowej hello hello lokalizacji wystawiania jest usuwany. Witaj cen magazynu używane do tymczasowej lokalizacji hello jest zgodne ze wszystkimi [cennik usługi Premium storage](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Nie wolno modyfikować ani edytować hello lokalizacji przejściowej.
>
>

### <a name="restore-premium-storage-vms"></a>Przywracanie maszyn wirtualnych usługi Premium Storage
Maszyny wirtualne magazynu Premium można przywróconej tooeither magazyn w warstwie Premium lub toonormal magazynu. Przywracanie Premium magazynu z maszyny Wirtualnej odzyskiwania punktu wstecz tooPremium magazynu jest hello typowy proces przywracania. Można go jednak ekonomiczne toorestore magazynu toostandard punktu odzyskiwania maszyny Wirtualnej magazynu Premium. Można tego typu przywracania, jeśli potrzebujesz podzbiór plików z hello maszyny Wirtualnej.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Korzystanie z maszyn wirtualnych dysku zarządzanego z usługą Azure Backup
Usługa Azure Backup chroni maszyny wirtualne dysku zarządzanego. Dzięki dyskom zarządzanym nie musisz zarządzać kontami magazynu maszyn wirtualnych, a aprowizowanie maszyny wirtualnej jest znacznie prostsze.

### <a name="back-up-managed-disk-vms"></a>Tworzenie kopii zapasowej maszyn wirtualnych dysku zarządzanego
Proces tworzenia kopii zapasowych maszyn wirtualnych na dyskach zarządzanych nie różni się niczym od tworzenia kopii zapasowych maszyn wirtualnych w usłudze Resource Manager. Hello portalu Azure należy skonfigurować hello zadanie tworzenia kopii zapasowej bezpośrednio z hello widok maszyny wirtualnej lub z usług odzyskiwania hello magazynu widoku. Kopie zapasowe maszyn wirtualnych możesz tworzyć na dyskach zarządzanych za pomocą kolekcji RestorePoint tworzonych na tych dyskach. Usługa Azure Backup obsługuje także tworzenie kopii zapasowych maszyn wirtualnych z dyskami zarządzanymi zaszyfrowanymi za pomocą usługi Azure Disk Encryption (ADE).

### <a name="restore-managed-disk-vms"></a>Przywracanie maszyn wirtualnych dysku zarządzanego
Kopia zapasowa Azure umożliwia toorestore pełną maszyny Wirtualnej z dyskami zarządzanych lub przywracania zarządzanego konta magazynu tooa dysków. Azure zarządza dysków hello zarządzane podczas procesu przywracania hello. (Powitania klienta) do zarządzania utworzona w ramach procesu przywracania hello konta magazynu hello. Podczas przywracania zarządzanych zaszyfrowanych maszyn wirtualnych, hello kluczy i kluczy tajnych maszyny Wirtualnej powinna istnieć podczas operacji przywracania hello hello magazynu kluczy toostarting wcześniejszych.

## <a name="what-are-hello-features-of-each-backup-component"></a>Co to są funkcje hello każdego składnika kopii zapasowej?
Witaj następujące sekcje zawierają tabele podsumowujące dostępności hello lub obsługi różnych funkcji w poszczególnych składników usługi Kopia zapasowa Azure. Zobacz hello informacje w poniższej tabeli, każdy dodatkowego pomocy technicznej lub szczegóły.

### <a name="storage"></a>Magazyn
| Funkcja | Agent usługi Azure Backup | System Center DPM | Azure Backup Server | Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |
| --- | --- | --- | --- | --- |
| Magazyn usługi Recovery Services |![Tak][green] |![Tak][green] |![Tak][green] |![Tak][green] |
| Przechowywanie na dysku | |![Tak][green] |![Tak][green] | |
| Przechowywanie na taśmie | |![Tak][green] | | |
| Kompresja <br/>(w magazynie usługi Recovery Services) |![Tak][green] |![Tak][green] |![Tak][green] | |
| Przyrostowa kopia zapasowa |![Tak][green] |![Tak][green] |![Tak][green] |![Tak][green] |
| Deduplikacja dysku | |![Częściowo][yellow] |![Częściowo][yellow] | | |

![klucz tabeli](./media/backup-introduction-to-azure-backup/table-key.png)

Magazyn usług odzyskiwania Hello jest obiektem docelowym magazynu preferowanych hello dotyczące wszystkich składników. System Center DPM i serwer kopii zapasowej Azure udostępniają toohave opcji hello kopii dysku lokalnym. Tylko program System Center DPM zapewnia jednak hello opcja toowrite danych tooa magazynu taśmowego.

#### <a name="compression"></a>Kompresja
Kopie zapasowe są kompresowane tooreduce hello wymaganego miejsca do magazynowania. Witaj tylko składnik, który nie korzysta z kompresji jest hello rozszerzenia maszyny Wirtualnej. Witaj kopii rozszerzenia maszyny Wirtualnej, które wszystkie dane kopii zapasowej z programu toohello konta magazynu usług odzyskiwania magazynu w hello tego samego regionu. Kompresja nie jest używana podczas transferu danych hello. Transferowanie danych hello bez kompresji nieco nadyma hello Magazyn używany. Przechowywanie danych hello bez kompresji umożliwia szybsze przywracania, należy jednak tego punktu odzyskiwania.


#### <a name="disk-deduplication"></a>Deduplikacja dysku
Możesz skorzystać z funkcji deduplikacji podczas wdrażania programu System Center DPM lub serwera Azure Backup Server [na maszynie wirtualnej funkcji Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server wykonuje deduplikacji danych (na poziomie hosta hello) na wirtualnych dyskach twardych (VHD), które są dołączone toohello maszyny wirtualnej jako magazynu kopii zapasowej.

> [!NOTE]
> Funkcja deduplikacji nie jest dostępna na platformie Azure dla żadnego składnika usługi Backup. W przypadku programu System Center DPM i Utwórz kopię zapasową serwera są wdrażane na platformie Azure, hello magazynu dysków dołączonych toohello, które maszyna wirtualna nie może być deduplikowane.
>
>

### <a name="incremental-backup-explained"></a>Informacje na temat przyrostowej kopii zapasowej
Każdy składnik kopia zapasowa Azure obsługuje przyrostowej kopii zapasowej niezależnie od hello docelowy magazyn (dysk, taśma, Magazyn usług odzyskiwania). Przyrostowej kopii zapasowej temu kopie zapasowe są pamięci i czasu wydajne, przekazując tylko zmiany wprowadzone od ostatniej kopii zapasowej hello.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Porównanie pełnej, różnicowej i przyrostowej kopii zapasowej

Użycie magazynu, cel czasu odzyskiwania (RTO, recovery time objective) oraz użycie sieci są różne w przypadku każdego typu metody wykonywania kopii zapasowej. tookeep hello kopii zapasowej całkowity koszt posiadania (TCO) w dół, należy toounderstand jak toochoose hello najlepsze rozwiązanie tworzenia kopii zapasowej. następujące obraz powitania porównuje pełnej kopii zapasowej, różnicowej kopii zapasowej i przyrostowej kopii zapasowej. W obrazie hello źródła danych, które A składa się z 10 magazynu blokuje A1 A10, którego kopię zapasową co miesiąc. Bloki A2, A3 i A4 oraz A9 zmiana hello pierwszy miesiąc i blokowanie A5 zmiany hello następnego miesiąca.

![Obraz przedstawiający porównanie metod wykonywania kopii zapasowej](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Z **pełnej kopii zapasowej**, każda kopia zapasowa zawiera hello całego źródła danych. Pełna kopia zapasowa używa dużej ilości przepustowości sieci i magazynu przy każdym transferze kopii zapasowej.

**Różnicowej kopii zapasowej** przechowuje tylko hello blokuje zmianie od czasu hello początkowej pełną kopię zapasową, która powoduje mniejszą ilość użycie sieci i magazynu. Różnicowe kopie zapasowe nie zawierają nadmiarowych kopii niezmienionych danych. Ponieważ jednak hello bloki danych, które zmieniają się między kolejne kopie zapasowe są przekazywane i przechowywane, różnicowe kopie zapasowe są mało wydajne. W hello drugiego miesiąca zmienione bloki A2, A3 i A4 oraz A9 kopię zapasową. W hello trzeciego miesiąca te bloki tego samego kopie zapasowe są tworzone ponownie, wraz z bloku zmienione A5. Witaj zmienione bloki nadal toobe kopii dopóki sytuacji hello dalej pełnej kopii zapasowej.

**Przyrostowa kopia zapasowa** osiągnięcie wysokiej wydajności magazynu i sieci przez zapisanie tylko hello bloki zmienione od czasu poprzedniej kopii zapasowej hello danych. Przy użyciu przyrostowej kopii zapasowej nie istnieje potrzeba tootake regularne pełnych kopii zapasowych. W przykładzie powitania po hello pełnej kopii zapasowej jest wykonywane dla hello pierwszy miesiąc zmienione bloki A2, A3 i A4 oraz A9 są oznaczane jako zmienione i przetransferowanych hello drugiego miesiąca. W hello trzeciego miesiąca, zmienić tylko bloku A5 jest oznaczony jako i przeniesione. Przenoszenie mniejszej ilości danych oszczędza zasoby magazynu i sieci, co zmniejsza całkowity koszt posiadania.   

### <a name="security"></a>Bezpieczeństwo
| Funkcja | Agent usługi Azure Backup | System Center DPM | Azure Backup Server | Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |
| --- | --- | --- | --- | --- |
| Bezpieczeństwo sieci<br/> (tooAzure) |![Tak][green] |![Tak][green] |![Tak][green] |![Częściowo][yellow] |
| Bezpieczeństwo danych<br/> (na platformie Azure) |![Tak][green] |![Tak][green] |![Tak][green] |![Częściowo][yellow] |

![klucz tabeli](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Bezpieczeństwo sieci
Cały ruch kopii zapasowej z programu toohello serwerów, które Magazyn usług odzyskiwania są szyfrowane przy użyciu szyfrowania 256 standardowe zaawansowane. dane kopii zapasowej Hello jest przesyłany przez bezpieczne połączenie HTTPS. Hello dane kopii zapasowej również są przechowywane w magazynie usług odzyskiwania hello w postaci zaszyfrowanej. Tylko, powitania klienta platformy Azure, masz hello hasło toounlock tych danych. Microsoft nie może odszyfrować dane kopii zapasowej hello w dowolnym momencie.

> [!WARNING]
> Po utworzeniu magazynu usług odzyskiwania hello tylko Ty masz dostęp toohello szyfrowania klucza. Firma Microsoft nigdy nie przechowuje kopię klucza szyfrowania i nie ma dostępu do klucza toohello. Jeśli klucz hello jest zagubione, Microsoft nie można odzyskać dane kopii zapasowej hello.
>
>

#### <a name="data-security"></a>Bezpieczeństwo danych
Tworzenie kopii zapasowych maszyn wirtualnych Azure wymaga skonfigurowania szyfrowania *w* hello maszyny wirtualnej. W przypadku maszyn wirtualnych systemu Windows należy użyć funkcji BitLocker, a w przypadku maszyn wirtualnych systemu Linux programu **dm-crypt**. Usługa Azure Backup nie szyfruje automatycznie danych kopii zapasowych, które przechodzą przez tę ścieżkę.

### <a name="network"></a>Sieć
| Funkcja | Agent usługi Azure Backup | System Center DPM | Azure Backup Server | Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |
| --- | --- | --- | --- | --- |
| Kompresja sieci <br/>(zbyt**Utwórz kopię zapasową serwera**) | |![Tak][green] |![Tak][green] | |
| Kompresja sieci <br/>(zbyt**magazyn usług odzyskiwania i**) |![Tak][green] |![Tak][green] |![Tak][green] | |
| Protokół sieciowy <br/>(zbyt**Utwórz kopię zapasową serwera**) | |TCP |TCP | |
| Protokół sieciowy <br/>(zbyt**magazyn usług odzyskiwania i**) |HTTPS |HTTPS |HTTPS |HTTPS |

![klucz tabeli](./media/backup-introduction-to-azure-backup/table-key-2.png)

Hello rozszerzenia maszyny Wirtualnej (na powitania maszyn wirtualnych IaaS) odczytuje hello dane bezpośrednio z hello kontem magazynu platformy Azure za pośrednictwem sieci magazynowania hello, więc nie jest konieczne toocompress ten ruch.

Jeśli używasz programu System Center DPM serwera lub serwera kopii zapasowej Azure jako serwer pomocniczy kopii zapasowej Kompresuj hello danych z serwera podstawowego hello toohello Utwórz kopię zapasową serwera. Kompresowanie danych przed utworzeniem jej kopii zapasowej tooDPM lub serwer kopii zapasowej Azure, ogranicza wykorzystanie przepustowości.

#### <a name="network-throttling"></a>Ograniczanie przepustowości sieci
agent usługi Kopia zapasowa Azure Hello oferuje ograniczania sieci, co pozwala toocontrol wykorzystaniem przepustowości sieci podczas transferu danych. Ograniczanie może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy. Ograniczanie danych transfer stosuje tooback zapasowej i przywracanie działania.

## <a name="backup-and-retention"></a>Tworzenie kopii zapasowej i przechowywanie

W usłudze Azure Backup obowiązuje limit wynoszący 9999 punktów odzyskiwania, znanych także jako kopie zapasowe lub migawki, na *chronione wystąpienie*. Wystąpienia chronione jest komputera, serwera (wirtualny lub fizyczny) lub tooback obciążenia skonfigurowane się tooAzure danych. Aby uzyskać więcej informacji, zobacz sekcję hello [co to jest chronione wystąpienia](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Wystąpienie jest chronione po zapisaniu kopii zapasowej danych. Hello kopię zapasową danych jest ochrona powitalnych. Jeśli hello źródło danych zostało utracone lub stała się uszkodzony, hello kopii zapasowej można przywrócić hello źródła danych. Witaj poniższej tabeli przedstawiono hello maksymalną częstotliwość wykonywania kopii zapasowych dla każdego składnika. Konfigurację zasad tworzenia kopii zapasowej Określa, jak szybko wykorzystać hello punktów odzyskiwania. Jeśli na przykład tworzysz punkt odzyskiwania codziennie, to możesz zachować punkty odzyskiwania przez 27 lat, zanim wyczerpie się ich liczba. Jeśli nie podejmiesz miesięcznego punktu odzyskiwania, można zachować punktów odzyskiwania 833 lat przed uruchomieniem. Hello usługi Kopia zapasowa nie ustawia limit czasu wygaśnięcia w punkcie odzyskiwania.

|  | Agent usługi Azure Backup | System Center DPM | Azure Backup Server | Usługa Backup dla maszyn wirtualnych IaaS platformy Azure |
| --- | --- | --- | --- | --- |
| Częstotliwość wykonywania kopii zapasowych<br/> (tooRecovery usług magazynu) |Trzy kopie zapasowe dziennie |Dwie kopie zapasowe dziennie |Dwie kopie zapasowe dziennie |Jedna kopia zapasowa dziennie |
| Częstotliwość wykonywania kopii zapasowych<br/> (toodisk) |Nie dotyczy |<li>Co 15 minut dla programu SQL Server <li>Co godzinę dla innych obciążeń |<li>Co 15 minut dla programu SQL Server <li>Co godzinę dla innych obciążeń</p> |Nie dotyczy |
| Opcje przechowywania |Codziennie, co tydzień, co miesiąc, co rok |Codziennie, co tydzień, co miesiąc, co rok |Codziennie, co tydzień, co miesiąc, co rok |Codziennie, co tydzień, co miesiąc, co rok |
| Maksymalna liczba punktów odzyskiwania na chronione wystąpienie |9999|9999|9999|9999|
| Maksymalny okres przechowywania |Zależnie od częstotliwości wykonywania kopii zapasowych |Zależnie od częstotliwości wykonywania kopii zapasowych |Zależnie od częstotliwości wykonywania kopii zapasowych |Zależnie od częstotliwości wykonywania kopii zapasowych |
| Punkty odzyskiwania na dysku lokalnym |Nie dotyczy |<li>64 dla serwerów plików,<li>448 dla serwerów aplikacji |<li>64 dla serwerów plików,<li>448 dla serwerów aplikacji |Nie dotyczy |
| Punkty odzyskiwania na taśmie |Nie dotyczy |Nieograniczona liczba |Nie dotyczy |Nie dotyczy |

## <a name="what-is-a-protected-instance"></a>Co to jest chronione wystąpienie
Wystąpienia chronione jest komputerem z systemem Windows tooa odwołanie do ogólnego, serwera (wirtualny lub fizyczny) lub baza danych SQL, który został skonfigurowany tooback się tooAzure. Wystąpienie jest chronione po Skonfiguruj zasady tworzenia kopii zapasowej hello komputera, serwera lub bazy danych, a tworzenie kopii zapasowej danych hello. Kolejne kopie hello danych kopii zapasowej dla tego wystąpienia chronione (nazywane są punkty odzyskiwania), zwiększyć hello liczba zużywane. Można utworzyć too9999 punktów odzyskiwania dla chronionych wystąpienia. Jeśli usuniesz punkt odzyskiwania z magazynu nie liczy się przed ilość punktów odzyskiwania 9999 hello.
Typowe przykłady wystąpienia chronione są maszyny wirtualne, serwery aplikacji oraz osobistymi komputerami z systemem operacyjnym Windows hello bazy danych. Na przykład:

* Maszynę wirtualną działającą hello funkcji Hyper-V lub Azure IaaS funkcji hypervisor sieci szkieletowej. Witaj systemy operacyjne gościa dla maszyny wirtualnej hello można systemu Windows Server lub Linux.
* Serwer aplikacji: serwer aplikacji hello mogą być fizyczne lub maszyny wirtualnej z systemem Windows Server i obciążeń z danymi, które wymaga toobe kopii zapasowej. Typowe obciążenia są programu Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server i hello roli serwera plików w systemie Windows Server. tooback się te obciążenia potrzebny jest System Center Data Protection Manager (DPM) lub serwer kopii zapasowej Azure.
* Komputer, stacji roboczej lub przenośnym systemem operacyjnym Windows hello.


## <a name="what-is-a-recovery-services-vault"></a>Co to jest magazyn usługi Recovery Services?
Magazyn usług odzyskiwania ma wartość jednostki magazynu online na platformie Azure używać toohold dane, takie jak kopii zapasowych, punkty odzyskiwania, a zasady tworzenia kopii zapasowej. Dane kopii zapasowej toohold Magazyny usług odzyskiwania można użyć dla platformy Azure usługi i lokalnych serwerach i stacjach roboczych. Magazyny usług odzyskiwania był łatwy tooorganize danych kopii zapasowych, przy jednoczesnym zmniejszeniu obciążenia administracyjnego. W ramach subskrypcji można utworzyć dowolną liczbę magazynów usługi Recovery Services.

Magazynów kopii zapasowych, które są oparte na platformie Azure Service Manager, zostały hello pierwszej wersji hello magazynu. Magazyny usług odzyskiwania, które dodają funkcje modelu usługi Azure Resource Manager hello, są hello druga wersja hello magazynu. Zobacz hello [artykuł z omówieniem magazyn usług odzyskiwania](backup-azure-recovery-services-vault-overview.md) pełen opis hello różnice w funkcjach. Możesz już tworzyć toocreate portalu hello Użyj magazyny kopii zapasowych, ale magazyny kopii zapasowych nadal są obsługiwane.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> **15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie. <br/> **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Czym różni się usługa Azure Backup od usługi Azure Site Recovery?
Usługi Azure Backup i Azure Site Recovery są zbliżone do siebie w tym sensie, że obie tworzą kopie zapasowe danych i mogą je przywracać. Jednak te usługi służą do innych celów związanych z zapewnianiem ciągłości działalności biznesowej oraz odzyskiwaniem po awarii. Użyj tooprotect kopia zapasowa Azure i przywrócić dane na bardziej szczegółowym poziomie. Na przykład jeśli prezentacji na komputerze przenośnym uległa uszkodzeniu, użyj prezentacji hello toorestore kopia zapasowa Azure. Jeśli potrzebujesz tooreplicate hello konfiguracji i danych na maszynie Wirtualnej w centrum danych w innym użyć usługi Azure Site Recovery.

Kopia zapasowa Azure zapewnia ochronę danych w sieci lokalnej i w chmurze hello. Usługa Azure Site Recovery koordynuje replikację maszyn wirtualnych i serwerów fizycznych, pracę w trybie failover i powrót po awarii. Obie te usługi są ważne, ponieważ rozwiązanie do odzyskiwania po awarii wymaga tookeep dane możliwe do odzyskania (kopia zapasowa) *i* zachować dostępne obciążenia (lokacji odzyskiwania), po awarii.

Witaj następujące pojęcia ułatwiają podjęcie istotnych decyzji wokół kopii zapasowej i odzyskiwanie po awarii.

| Pojęcie | Szczegóły | Tworzenie kopii zapasowych | Odzyskiwanie awaryjne (DR) |
| --- | --- | --- | --- |
| Cel punktu odzyskiwania (recovery point objective, RPO) |Hello ilości utraconych danych, jeśli odzyskiwania musi wykonać toobe. |Rozwiązania tworzenia kopii zapasowych charakteryzują się dużą zmiennością dopuszczalnej wartości RPO. Kopie zapasowe maszyny wirtualnej mają zwykle RPO na poziomie jednego dnia, natomiast kopie zapasowe bazy danych mają RPO o wartości 15 minut. |Rozwiązania odzyskiwania awaryjnego mają niską wartość RPO. Hello kopiowania odzyskiwania po awarii może być za kilka sekund lub kilka minut. |
| Cel czasu odzyskiwania (recovery time objective, RTO) |Hello ilość czasu potrzebnego toocomplete odzyskiwania lub przywracania. |Z powodu hello większy cel punktu odzyskiwania, hello ilość danych wymagane przez mechanizm tworzenia kopii zapasowych tooprocess jest zwykle znacznie wyższa, która prowadzi Objective, RTO toolonger. Na przykład może potrwać dni toorestore dane z taśmy, w zależności od hello czas tootransport hello taśmę z lokalizacji poza nim. |Rozwiązania w zakresie odzyskiwania po awarii ma mniejszy Objective, RTO, ponieważ są one bardziej zsynchronizowane ze źródłem hello. Mniej zmiany muszą toobe przetworzone. |
| Przechowywanie |Jak długo dane muszą toobe przechowywane |W przypadku scenariuszy wymagających odzyskiwania operacyjnego (uszkodzenie danych, nieumyślne usunięcie pliku, błąd systemu operacyjnego) dane kopii zapasowej są zwykle zachowywane przez 30 dni lub mniej.<br>Z punktu widzenia zgodności danych może być konieczne toobe przechowywanych dla miesięcy, a nawet lata. Dane z kopii zapasowej doskonale nadają się do archiwizacji w takich przypadkach. |Odzyskiwanie po awarii wymaga tylko danych operacyjnych dotyczących odzyskiwania, które zwykle trwa kilka godzin lub w górę tooa dnia. Ze względu na powitania przechwytywania szczegółowych danych używany w rozwiązaniach odzyskiwania po awarii nie zaleca się przy użyciu danych odzyskiwania po awarii w celu przechowywania długoterminowego. |

## <a name="next-steps"></a>Następne kroki
Użyj jednej z hello następujące samouczki dla szczegółowych instrukcji krok po kroku, ochrony danych w systemie Windows Server lub ochrony maszyny wirtualnej (VM) na platformie Azure:

* [Tworzenie kopii zapasowych plików i folderów](backup-try-azure-backup-in-10-mins.md)
* [Tworzenie kopii zapasowej maszyn wirtualnych platformy Azure](backup-azure-vms-first-look-arm.md)

Szczegółowe informacje na temat ochrony innych obciążeń możesz uzyskać w jednym z następujących artykułów:

* [Tworzenie kopii zapasowej systemu Windows Server](backup-configure-vault.md)
* [Tworzenie kopii zapasowej obciążeń aplikacji](backup-azure-microsoft-azure-backup.md)
* [Tworzenie kopii zapasowej maszyn wirtualnych IaaS platformy Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
