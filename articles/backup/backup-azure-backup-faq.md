---
title: "aaaAzure Backup — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na pytania toocommon o: funkcji Kopia zapasowa Azure, w tym usług odzyskiwania magazynów, co go może tworzyć kopie zapasowe, jak to działa, szyfrowania i limity. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "tworzenie kopii zapasowej i odzyskiwanie po awarii; usługa kopii zapasowej"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Pytania dotyczące hello usługi Kopia zapasowa Azure
Ten artykuł zawiera toohelp pytania toocommon odpowiedzi szybko poznać hello składniki usługi Kopia zapasowa Azure. W niektórych hello odpowiedzi są artykuły toohello łącza, zawierające szczegółowe informacje. Można zadawać pytania dotyczące usługi Azure Backup, klikając **komentarze** (toohello do prawej). Komentarze są wyświetlane u dołu hello w tym artykule. Konto Livefyre jest wymagane toocomment. Można również zadawać pytania dotyczące usługi Azure Backup hello w hello [forum dyskusyjne](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly skanowania hello sekcje w tym artykule użyć hello łącza toohello prawo, w obszarze **w tym artykule**.


## <a name="recovery-services-vault"></a>Magazyn usługi Recovery Services

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Znajduje wszystkie limit liczby hello magazynów, które mogą zostać utworzone w każdej subskrypcji platformy Azure? <br/>
Tak. Od września 2016 r. w każdej subskrypcji można utworzyć 25 magazynów usługi Recovery Services lub magazynów kopii zapasowych. Można utworzyć usług odzyskiwania too25 magazynów na obsługiwany region usługi Azure Backup na subskrypcję. Jeśli potrzebna jest większa liczba magazynów, należy utworzyć dodatkową subskrypcję.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Czy istnieją ograniczenia dotyczące hello liczbę serwerów/maszyn, które mogą być rejestrowane przed każdym magazynu? <br/>
Tak, możesz zarejestrować się maszyn too50 dla magazynu. W przypadku maszyn wirtualnych Azure IaaS hello limit wynosi 200 maszyn wirtualnych na magazynie. Tooregister więcej komputerów, należy utworzyć inny magazyn.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Jeśli organizacja ma jeden magazyn, to w jaki sposób można odizolować dane z jednego serwera od danych z innego serwera podczas przywracania danych?<br/>
Wszystkie serwery, które są zarejestrowane toohello można odzyskać tego samego magazynu hello danych kopii zapasowej przez inne serwery *używające hello samo hasło*. Jeśli masz serwery których dane kopii zapasowej chcesz tooisolate między serwerami w organizacji, użycie wyznaczonych hasła dla tych serwerów. Na przykład serwery zarządzania zasobami ludzkimi mogą korzystać z jednego hasła szyfrowania, serwery księgowości z drugiego, a serwery pamięci masowej z trzeciego.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Czy można „migrować” magazyn lub dane kopii zapasowej między subskrypcjami? <br/>
Nie. Magazyn Hello jest tworzony na poziomie subskrypcji i nie można przypisywać ich tooanother subskrypcji, po jego utworzeniu.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Magazyny usług Recovery Services są oparte na usłudze Resource Manager. Czy magazyny usługi Backup (tryb klasyczny) są nadal obsługiwane? <br/>
Wszystkie istniejące magazyny kopii zapasowych w hello [klasyczny portal](https://manage.windowsazure.com) kontynuować toobe obsługiwane. Jednak nie są już używane hello klasycznego portalu toodeploy nowymi magazynami kopii zapasowych. Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich wdrożeń, ponieważ przyszłe ulepszenia zastosowania Magazyny usług tooRecovery, tylko. Przy próbie toocreate magazynu kopii zapasowych w portalu klasycznym hello będzie przekierowany toohello [portalu Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Czy można migrować magazynu usług odzyskiwania tooa magazynu kopii zapasowej? <br/>
Niestety nie, nie można migrować zawartość hello tooa magazynu kopii zapasowej, które Magazyn usług odzyskiwania. Pracujemy nad dodaniem tej funkcji, ale nie jest ona obecnie dostępna.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Mam utworzone kopie zapasowe moich klasycznych maszyn wirtualnych w magazynie usługi Backup. Można I migracji maszyn wirtualnych z trybu klasycznego tooResource menedżera trybu i chronić je w magazynie usług odzyskiwania?
Klasycznym punktów odzyskiwania maszyny Wirtualnej w magazynie kopii zapasowych nie automatycznie zostanie przeprowadzona migracja magazynu usług odzyskiwania tooa po przeniesieniu hello maszyny Wirtualnej z tooResource klasycznym trybie menedżera. Wykonaj te kroki tootransfer kopii zapasowych maszyny Wirtualnej:

1. W magazynie kopii zapasowych hello, przejdź do pozycji toohello **chronione elementy** i wybierz hello maszyny Wirtualnej. Kliknij pozycję [Zatrzymaj ochronę](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Pozostaw opcję *Usuń powiązane dane kopii zapasowych* **niezaznaczoną**.
2. Usuń rozszerzenie kopii zapasowej/migawki hello z hello maszyny Wirtualnej.
3. Migruj maszynę wirtualną hello z trybu Menedżera tooResource trybu klasycznego. Upewnij się, że hello magazynu i sieci jest również odpowiedniego maszyny wirtualnej toohello poddane migracji informacje o trybie Menedżera tooResource.
4. Tworzenie magazynu usług odzyskiwania i konfigurowanie tworzenia kopii zapasowej na powitania migracji maszyny wirtualnej przy użyciu **kopii zapasowej** akcji na pulpicie nawigacyjnym magazynu. Szczegółowe informacje na temat tworzenia kopii zapasowej usług odzyskiwania maszyny Wirtualnej tooa magazynu, zobacz artykuł hello [ochrony maszyn wirtualnych platformy Azure w magazynie usług odzyskiwania](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agent usługi Azure Backup
Szczegółową listę pytań możesz znaleźć w temacie [FAQ on Azure file-folder backup (Często zadawane pytania dotyczące kopii zapasowych folderów plików na platformie Azure)](backup-azure-file-folder-backup-faq.md)

## <a name="azure-vm-backup"></a>Kopia zapasowa maszyny wirtualnej platformy Azure
Szczegółową listę pytań możesz znaleźć w temacie [FAQ on Azure VM backup (Często zadawane pytania dotyczące kopii zapasowych maszyn wirtualnych platformy Azure)](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>Tworzenie kopii zapasowych serwerów VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Można wykonywać kopie zapasowe programu VMware vCenter serwerów tooAzure?

Tak. Można użyć serwera kopii zapasowej Azure tooback VMware vCenter i ESXi tooAzure. Uzyskać informacji o wersji VMware obsługiwane hello, zobacz artykuł hello [macierzy ochrona serwer kopii zapasowej Azure](backup-mabs-protection-matrix.md). Aby uzyskać instrukcje, zobacz [tooback serwer kopii zapasowej Azure Użyj serwera VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Programy Azure Backup Server i System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Czy można użyć serwera kopii zapasowej Azure toocreate kopii zapasowej odzyskiwania systemu operacyjnego systemu od zera (BMR) dla serwera fizycznego? <br/>
Tak.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Można zarejestrować Mój serwer DPM toomultiple magazynów? <br/>
Nie. Serwer DPM lub MABS może być zarejestrowany tooonly jeden magazyn.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Która wersja programu System Center Data Protection Manager jest obsługiwana? <br/>
Zaleca się zainstalowanie hello [najnowsze](http://aka.ms/azurebackup_agent) agenta usługi Kopia zapasowa Azure na powitania najnowszego pakietu zbiorczego aktualizacji (UR) dla System Center Data Protection Manager (DPM). Począwszy od sierpnia 2016 roku 11 pakiet zbiorczy aktualizacji jest hello najnowszej aktualizacji.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Zainstalowano tooprotect agenta usługi Kopia zapasowa Azure pliki i foldery. Można teraz zainstalować programu System Center DPM toowork z Azure Backup agent tooprotect lokalnymi obciążeń aplikacji/wirtualna tooAzure? <br/>
toouse kopia zapasowa Azure z System Center Data Protection Manager (DPM), najpierw zainstaluj program DPM, a następnie zainstaluj agenta usługi Kopia zapasowa Azure. Instalowanie składników usługi Kopia zapasowa Azure hello w następującej kolejności gwarantuje, że agent usługi Kopia zapasowa Azure hello działa z programem DPM. Instalowanie agenta usługi Kopia zapasowa Azure hello przed zainstalowaniem programu DPM nie jest zalecana lub jest obsługiwana.


## <a name="how-azure-backup-works"></a>Jak działa usługa Azure Backup
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Jeśli zadanie tworzenia kopii zapasowej I anulować po jego uruchomieniu, hello przeniesione dane kopii zapasowej usunięciu? <br/>
Nie. Wszystkich danych przesyłanych w magazynie hello przed hello zadanie tworzenia kopii zapasowej zostało anulowane, pozostaje w magazynie hello. Azure używa kopii zapasowej toooccasionally mechanizmu punkt kontrolny Dodaj punkty kontrolne toohello kopii zapasowej danych podczas hello kopii zapasowej. Ponieważ w danych kopii zapasowej hello są punkty kontrolne, hello następny proces tworzenia kopii zapasowej można zweryfikować hello integralności plików hello. następne zadanie tworzenia kopii zapasowej Hello będzie danych toohello przyrostowa kopia zapasowa. Przyrostowe kopie zapasowe transfer tylko nowe lub zmienione dane, które oznacza toobetter wykorzystanie przepustowości.

Jeśli anulujesz zadanie kopii zapasowej dla maszyny wirtualnej platformy Azure, wszelkie przesłane dane zostaną zignorowane. następne zadanie tworzenia kopii zapasowej Hello przesyła dane przyrostowe z hello ostatnie zadanie tworzenia kopii zapasowych powiodło się.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Czy istnieją ograniczenia dotyczące czasu wykonywania zadań tworzenia kopii zapasowej i ich liczby?<br/>
Tak. Można uruchomić zadania tworzenia kopii zapasowej na serwerze z systemem Windows lub stacji roboczych systemu Windows w górę toothree razy dziennie. Można uruchomić zadania tworzenia kopii zapasowej w programie System Center DPM się tootwice dziennie. Zadanie tworzenia kopii zapasowej maszyn wirtualnych IaaS można uruchamiać jeden raz w ciągu dnia. Umożliwia planowanie zasad dla systemu Windows Server lub toospecify stacji roboczej systemu Windows hello harmonogramy codziennie lub co tydzień. Za pomocą programu System Center DPM można określić dzienne, tygodniowe, miesięczne i roczne harmonogramy.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Dlaczego jest rozmiar hello hello toohello przesyłane dane, które mniejszego niż I kopie zapasowe danych hello magazyn usług odzyskiwania?<br/>
 Wszystkie dane hello jest wykonywana kopia zapasowa Azure Backup Agent lub SCDPM lub serwer kopii zapasowej Azure jest skompresowany i szyfrowane przed ich przesyłania. Po zastosowaniu hello kompresji i szyfrowania danych hello w magazynie kopii zapasowych hello jest 30-40% mniejsze.

## <a name="what-can-i-back-up"></a>Dla jakich danych mogę utworzyć kopię zapasową
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Jakie systemy operacyjne są obsługiwane przez usługę Azure Backup? <br/>
Kopia zapasowa Azure obsługuje powitania po listę systemów operacyjnych do wykonywania kopii zapasowych: pliki i foldery i aplikacji obciążenia chronione za pomocą serwera usługi Kopia zapasowa Azure i System Center Data Protection Manager (DPM).

| System operacyjny | Platforma | SKU |
|:--- | --- |:--- |
| Windows 8 i najnowsze dodatki Service Pack |64-bitowa |Enterprise, Pro |
| Windows 7 i najnowsze dodatki Service Pack |64-bitowa |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 i najnowsze dodatki Service Pack |64-bitowa |Enterprise, Pro |
| Windows 10 |64-bitowa |Enterprise, Pro, Home |
| Windows Server 2016 |64-bitowa |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 i najnowsze dodatki Service Pack |64-bitowa |Standard, Datacenter, Foundation |
| Windows Server 2012 i najnowsze dodatki Service Pack |64-bitowa |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 i najnowsze dodatki Service Pack |64-bitowa |Standard, Workgroup | 
| Windows Storage Server 2012 R2 i najnowsze dodatki Service Pack |64-bitowa |Standard, Workgroup |
| Windows Storage Server 2012 i najnowsze dodatki Service Pack |64-bitowa |Standard, Workgroup |
| Windows Server 2012 R2 i najnowsze dodatki Service Pack |64-bitowa |Essential |
| Windows Server 2008 R2 SP1 |64-bitowa |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64-bitowa |Standard, Enterprise, Datacenter, Foundation |

**W przypadku usługi kopii zapasowych maszyny wirtualnej platformy Azure:**

* **Linux**: usługa Azure Backup obsługuje [dystrybucje zalecane dla platformy Azure](../virtual-machines/linux/endorsed-distros.md) z wyjątkiem systemu operacyjnego Linux Core.  Innych Bring-Your-właścicielem — dystrybucje systemu Linux mogą również działać, dopóki agent maszyny Wirtualnej hello jest dostępne na maszynie wirtualnej hello i obsługę języka Python istnieje.
* **Windows Server**: wersje starsze niż Windows Server 2008 R2 nie są obsługiwane.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Istnieje limit na rozmiar hello każdego źródła danych, w których powstaje kopia zapasowa? <br/>
Nie ma żadnego limitu na powitania ilość danych, które można tworzyć kopie zapasowe tooa magazynu. Kopia zapasowa Azure ogranicza maksymalny rozmiar hello hello źródła danych, jednak te limity są duże. Począwszy od sierpnia 2015 r. jest hello maksymalnego rozmiaru dla źródła danych dla hello obsługiwane systemy operacyjne:

| L.p. | System operacyjny | Maksymalny rozmiar źródła danych |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 lub nowszy |54 400 GB |
| 2 |Windows 8 lub nowszy |54 400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Hello w poniższej tabeli opisano, jak każdy rozmiar źródła danych jest określana.

| Źródło danych | Szczegóły |
|:---:|:--- |
| Wolumin |Witaj ilość danych, których powstaje kopia zapasowa z jednego woluminu komputera klienta lub serwera |
| Maszyna wirtualna z funkcją Hyper-V |Suma wszystkich hello wirtualne dyski twarde maszyny wirtualnej hello tworzona kopia zapasowa danych |
| Baza danych Microsoft SQL Server |Rozmiar pojedynczej bazy danych SQL, której kopia zapasowa jest wykonywana |
| Microsoft SharePoint |Suma hello zawartości i konfiguracji baz danych w farmie programu SharePoint, w których powstaje kopia zapasowa |
| Microsoft Exchange |Suma wszystkich baz danych programu Exchange w serwerze Exchange, którego kopia zapasowa jest wykonywana |
| Stan systemu/BMR |Każda poszczególnych kopia stanu systemu lub BMR maszyny hello tworzona kopia zapasowa |

Do utworzenia kopii zapasowej maszyny Wirtualnej platformy Azure każda maszyna wirtualna może zawierać maksymalnie too16 dysków z danymi z każdym danych dysku jest rozmiar 1023GB lub mniej. 

## <a name="retention-policy-and-recovery-points"></a>Zasady przechowywania i punkty odzyskiwania
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Znajduje różnicę między hello zasad przechowywania dla programu DPM, a klient serwera systemu Windows (to znaczy w systemie Windows Server bez programu DPM)?<br/>
Nie, zarówno program DPM, jak i system Windows Server/klient systemu Windows mają dzienne, tygodniowe, miesięczne i roczne zasady przechowywania.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Czy można skonfigurować zasady przechowywania selektywnie, na przykład skonfigurować zasady tygodniowe i dziennie, ale nie roczne i miesięczne?<br/>
Tak, hello struktury przechowywania kopii zapasowej Azure umożliwia toohave pełną elastyczność podczas definiowania zasad przechowywania hello zgodnie z wymaganiami.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Czy można „zaplanować utworzenie kopii zapasowej” o godzinie 18:00 i określić zasady przechowywania na inną godzinę?<br/>
Nie. Zasady przechowywania mogą być stosowane wyłącznie w punktach kopii zapasowej. W hello po obrazu zasad przechowywania hello jest określona dla kopii zapasowych wykonanych na 00: 00 i 18: 00. <br/>

![Harmonogram tworzenia i przechowywania kopii zapasowych](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Jeśli kopia zapasowa jest przechowywane przez długi czas trwania, wymaga więcej czasu toorecover starsze punktu danych? <br/>
Nie — jest hello sam czas hello toorecover hello najstarsze lub hello najnowszego punktu. Każdy punkt odzyskiwania zachowuje się jak pełny punkt.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>W przypadku każdego punktu odzyskiwania jak Pełna punktu, ma ona wpływu hello całkowita magazynu kopii zapasowych rozliczeniowy?<br/>
Typowe produkty punktów długoterminowego przechowywania przechowują dane kopii zapasowych jako pełne punkty. pełne punkty Hello są magazynu *nieefektywne* , ale są łatwiejsze i szybsze toorestore. Przyrostowe kopie są magazynu *wydajne* , ale wymagają toorestore łańcuch danych, co ma wpływ na czas odzyskiwania. Azure Backup magazynu architektura zapewnia hello najlepsze cechy obu tych środowisk optymalnie przechowywania danych szybkiego przywracania i ponoszenia kosztów magazynowania niski. Takie podejście do magazynu danych zapewnia efektywne wykorzystanie przepustowości ruchu przychodzącego i wychodzącego. Zarówno hello ilość czasu, magazynu i hello danych potrzebnych danych hello toorecover, pozostaje tooa minimalne. Dowiedz się więcej o tym, dlaczego [przyrostowe kopie zapasowe](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/) są wydajne.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Istnieje limit hello liczby punktów odzyskiwania, które można utworzyć?<br/>
Można utworzyć too9999 punktów odzyskiwania dla każdego chronionego wystąpienia. Wystąpienia chronione jest komputera, serwera (wirtualny lub fizyczny) lub tooback obciążenia skonfigurowane się tooAzure danych. Aby uzyskać więcej informacji, zobacz objaśnienia hello [kopii zapasowej i przechowywania](./backup-introduction-to-azure-backup.md#backup-and-retention), i [co to jest chronione wystąpienia](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Jak wiele odzysk mogą wykonywać na hello danych, która została skopiowana tooAzure?<br/>
Nie ma żadnego limitu hello liczby operacji odzyskiwania z kopii zapasowej Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Podczas przywracania danych, będę płacić za hello ruch wychodzący z platformy Azure? <br/>
Nie. Twoje odzyskiwania są wolnego i nie są naliczane opłaty hello wyjście ruchu.

## <a name="azure-backup-encryption"></a>Szyfrowanie w usłudze Azure Backup
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Hello danych są wysyłane zaszyfrowane tooAzure? <br/>
Tak. Dane są szyfrowane na komputerze serwera/klienta/SCDPM lokalne powitania za pomocą AES256 i hello dane są przesyłane za pośrednictwem bezpiecznego łącza HTTPS.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Jest hello kopii zapasowej danych na platformie Azure, również szyfrowane?<br/>
Tak. wysłane dane Hello tooAzure pozostaną zaszyfrowane (magazynowane). Microsoft nie powoduje odszyfrowania hello dane kopii zapasowej w dowolnym momencie. Podczas tworzenia kopii zapasowej maszyny Wirtualnej platformy Azure, kopia zapasowa Azure korzysta z szyfrowania hello maszyny wirtualnej. Na przykład jeśli maszyna wirtualna jest zaszyfrowany przy użyciu szyfrowania dysków Azure lub innej technologii szyfrowania, kopia zapasowa Azure korzysta z tego toosecure szyfrowania danych.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Co to jest hello minimalną długość klucza szyfrowania używane dane kopii zapasowej tooencrypt? <br/>
klucz szyfrowania Hello musi mieć co najmniej 16 znaków, gdy używasz agenta kopii zapasowej systemu Azure. Dla maszyn wirtualnych platformy Azure istnieje nie toolength limit kluczy używanych przez Azure KeyVault. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Co się stanie, jeśli misplace po klucz szyfrowania hello? Witaj, dane można odzyskać (lub) firmy Microsoft dane można odzyskać hello? <br/>
dane kopii zapasowej hello kluczy używanych tooencrypt Hello jest obecny tylko lokalnie powitania klienta. Firma Microsoft nie przechowuje kopii na platformie Azure i nie ma żadnych klucza toohello dostępu. Jeśli powitania klienta misplaces hello klucza, Microsoft nie można odzyskać dane kopii zapasowej hello.
