Azure maszynach wirtualnych (VM) może czasem ponownego uruchomienia bez widocznego powodu bez dokumentów użytkownika, o zainicjował hello operacji ponownego rozruchu. W tym artykule wymieniono hello działań i zdarzeń, które mogą powodować tooreboot maszyn wirtualnych i zapewnia wgląd w sposób tooavoid nieoczekiwany ponowny rozruch problemy lub zmniejszyć wpływ hello takich problemów.

## <a name="configure-hello-vms-for-high-availability"></a>Konfigurowanie maszyn wirtualnych hello wysokiej dostępności
Uruchamia Hello najlepsze sposób tooprotect aplikacji, która działa na platformie Azure dla maszyny Wirtualnej, a czas przestoju jest tooconfigure hello maszyn wirtualnych wysokiej dostępności.

tooprovide ten poziom nadmiarowości tooyour aplikacji, zalecamy grupowanie co najmniej dwóch maszyn wirtualnych w zestawie dostępności. Ta konfiguracja zapewnia, że podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jedna maszyna wirtualna jest dostępna, i spełnia hello 99,95% [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Aby uzyskać więcej informacji na temat zestawów dostępności zobacz następujące artykuły hello:

- [Zarządzanie hello dostępność maszyn wirtualnych](../articles/virtual-machines/windows/manage-availability.md)
- [Konfigurowanie dostępności maszyn wirtualnych](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Informacje o kondycji zasobów 
Kondycja zasobów platformy Azure to usługa, która przedstawia kondycję hello poszczególnych zasobów platformy Azure i zawiera możliwością wykonania akcji wskazówki dotyczące rozwiązywania problemów. W środowisku chmury, których nie jest możliwe toodirectly serwery dostępu lub elementy infrastruktury celem hello kondycja zasobu jest tooreduce hello czas poświęcony na rozwiązywanie problemów. W szczególności celem hello jest czas hello tooreduce spędzają określającą, czy główny hello hello problemu znajduje się w aplikacji hello lub zdarzenia wewnątrz hello platformy Azure. Aby uzyskać więcej informacji, zobacz [opis i użyj kondycja zasobów](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Akcje i zdarzenia, które mogą spowodować hello tooreboot maszyny Wirtualnej

### <a name="planned-maintenance"></a>Planowana konserwacja
Microsoft Azure wykonuje okresowo aktualizacje Witaj świecie tooimprove hello niezawodności, wydajności i zabezpieczeń infrastruktury hosta hello, źródłową maszyn wirtualnych. Wiele z tych aktualizacji, w tym zachowaniu pamięci aktualizacji są wykonywane bez wpływu na maszyn wirtualnych lub usług w chmurze.

Jednak niektóre aktualizacje wymagają ponownego uruchomienia. W takich przypadkach hello maszyny wirtualne są zamknięte podczas możemy poprawka hello infrastruktury, a następnie hello maszyny wirtualne zostaną ponownie uruchomione.

toounderstand, jakie Azure planowanej konserwacji i jak to wpłynąć na dostępność hello maszyn wirtualnych systemu Linux, zobacz artykuły hello wymienione w tym miejscu. Witaj artykuły zawierają ogólne informacje o hello Azure zaplanowanej konserwacji procesu i jak tooschedule zaplanowanej konserwacji toofurther zmniejszyć wpływ hello.

- [Planowana Konserwacja maszyn wirtualnych na platformie Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Jak tooschedule zaplanowanej konserwacji na maszynach wirtualnych Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Aktualizacje pozwalające zachować stan pamięci   
Dla tej klasy aktualizacji w programie Microsoft Azure podczas korzystania bez wpływu na ich uruchomionych maszyn wirtualnych. Wiele z tych aktualizacji jest toocomponents lub usług, które mogą być aktualizowane bez zakłócania hello uruchomione wystąpienie. Niektóre są aktualizacji infrastruktury platformy w systemie operacyjnym hosta hello, który można zastosować bez ponownego uruchomienia hello maszyn wirtualnych.

Te aktualizacje zachowywania pamięci są realizowane za pomocą technologii, która umożliwia migrację na żywo w miejscu. Gdy jest on aktualizowany, hello maszyna wirtualna jest umieszczona w *wstrzymana* stanu. Ten stan zachowuje hello pamięci RAM, a system operacyjny hosta źródłowego hello otrzymuje hello niezbędne aktualizacje i poprawki. Witaj maszyny Wirtualnej zostanie wznowione w ciągu 30 sekund jest wstrzymana. Po powitalne maszyny Wirtualnej zostanie wznowione jego zegara zostanie automatycznie zsynchronizowana.

Ze względu na powitania Wstrzymaj krótki okres wdrażania aktualizacji za pomocą ten mechanizm znacznie zmniejsza wpływ hello na powitania maszyn wirtualnych. Jednak nie wszystkie aktualizacje można wdrożyć w ten sposób. 

Aktualizacje wielu wystąpień (dla maszyn wirtualnych w zestawie dostępności) są stosowane jednej domeny aktualizacji w czasie.

> [!NOTE]
> Maszyny z systemem Linux, które mają stare wersje jądra dotyczy alarm jądra podczas tej metody aktualizacji. tooavoid ten problem, aktualizacja tookernel wersji 3.10.0-327.10.1 lub nowszej. Aby uzyskać więcej informacji, zobacz [panics maszyny Wirtualnej systemu Linux platformy Azure na podstawie 3.10 jądra po uaktualnieniu węzła hosta](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Akcje ponownego uruchomienia lub zamknięcia zainicjowanego przez użytkownika
 
Po wykonaniu ponowny rozruch komputera z hello portalu Azure, programu Azure PowerShell, interfejsu wiersza polecenia lub zresetować interfejsu API zdarzenia hello można znaleźć w hello [dziennika aktywności platformy Azure](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Po wykonaniu akcji hello systemu operacyjnego hello maszyny Wirtualnej można znaleźć hello zdarzeń w dziennikach systemu hello.

Inne scenariusze, które zazwyczaj powodują hello tooreboot maszyny Wirtualnej obejmują wiele operacji zmiany konfiguracji. Zazwyczaj zobaczysz komunikat ostrzegawczy wskazujący, że wykonywanie określonej akcji spowoduje ponowne uruchomienie hello maszyny Wirtualnej. Przykłady obejmują wszystkie zmiany rozmiaru operacje maszyny Wirtualnej, a zmiana hello hasło konta administratora hello i ustawiania statycznego adresu IP.

### <a name="azure-security-center-and-windows-update"></a>Centrum zabezpieczeń Azure i usługi Windows Update
Centrum zabezpieczeń Azure monitoruje codzienne systemu Windows i maszyn wirtualnych systemu Linux dla brakujących aktualizacji systemu operacyjnego. Centrum zabezpieczeń pobiera listę dostępnych zabezpieczeń i krytycznych aktualizacji z witryny Windows Update lub Windows Server Update Services (WSUS), w zależności od tego, który usługa jest skonfigurowana na maszynie Wirtualnej systemu Windows. Centrum zabezpieczeń sprawdza również hello najnowsze aktualizacje dla systemów Linux. Jeśli maszyna wirtualna jest Brak aktualizacji systemu, Centrum zabezpieczeń zaleca się zastosowanie aktualizacji systemu. Aplikacja Hello tych aktualizacji systemu są kontrolowane poprzez hello Centrum zabezpieczeń w hello portalu Azure. Po zastosowaniu niektóre aktualizacje, ponowne uruchomienie maszyny Wirtualnej może być wymagane. Aby uzyskać więcej informacji, zobacz [stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure](../articles/security-center/security-center-apply-system-updates.md).

Takich jak serwery lokalne Azure nie umieszczaj aktualizacje z usługi Windows Update tooWindows maszynach wirtualnych platformy Azure, ponieważ te komputery są zamierzone toobe zarządzane przez użytkowników. Jesteś, jednak zaleca tooleave hello automatycznej aktualizacji systemu Windows ustawienie jest włączone. Automatyczne instalowanie aktualizacji z witryny Windows Update może również spowodować toooccur ponowne uruchomienia, po zastosowaniu aktualizacji hello. Aby uzyskać więcej informacji, zobacz [aktualizacji systemu Windows — często zadawane pytania](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Innych sytuacjach wpływu na dostępność hello maszyny wirtualnej
Istnieją inne przypadki, w których Azure może aktywnie zawiesić stosowanie hello maszyny wirtualnej. Otrzymasz powiadomień e-mail przed wykonaniem tej akcji, więc będziesz mieć tooresolve szansy hello podstawowej problemy. Przykładami problemy, które mają wpływ na dostępność maszyn wirtualnych naruszenia zabezpieczeń i wygaśnięcie hello metody płatności.

### <a name="host-server-faults"></a>Błędy serwera hosta 
Witaj maszyny Wirtualnej jest hostowany na serwerze fizycznym, który jest używany w centrum danych Azure. Uruchamia serwer fizyczny Hello usługi agenta o nazwie hello Agent hosta w tooa dodanie kilka składników platformy Azure. Gdy te składniki oprogramowania platformy Azure na serwerze fizycznym hello przestać odpowiadać, hello system monitorowania wyzwala ponowne uruchomienie hello hosta serwera tooattempt odzyskiwania. Witaj maszyny Wirtualnej jest zwykle dostępne ponownie w ciągu pięciu minut i kontynuuje toolive na powitania takie same jak wcześniej hosta.

Serwer błędy są zazwyczaj spowodowane awarii sprzętu, takich jak hello awarii dysku twardego lub dysk SSD. Azure stale monitoruje tych zdarzeń, identyfikuje hello usterki podstawowej i zbiera i wydaje aktualizacje po hello środki zaradcze, zostały wdrożone i przetestowane.

Ponieważ niektóre błędy serwera hosta mogą być toothat określonego serwera, powtarzane sytuacji ponownego uruchomienia maszyny Wirtualnej może zwiększona wdrażając ręcznie hello wirtualna tooanother hosta serwera. Ta operacja może być uruchomiona za pomocą hello **ponownie wdrożyć** opcji na stronie szczegółów hello hello maszyny Wirtualnej lub zatrzymując i uruchamiając ponownie hello maszyny Wirtualnej w hello portalu Azure.

### <a name="auto-recovery"></a>Automatyczne odzyskiwanie
Jeśli serwer hosta hello nie ponowny rozruch jakiejkolwiek przyczyny, hello platformy Azure inicjuje serwera hosta błędny automatycznego odzyskiwania Akcja tootake hello poza obrót w celu dokładniejszego zbadania. 

Wszystkie maszyny wirtualne na tym hoście są automatycznie przeniesione tooa serwera hosta innych, dobrej kondycji. Ten proces jest zwykle ukończone w ciągu 15 minut. Zobacz toolearn więcej informacji na temat procesu automatycznego odzyskiwania hello [automatycznego odzyskiwania maszyn wirtualnych](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Nieplanowana konserwacja
W rzadkich przypadkach hello zespół operacyjny Azure może być konieczne tooensure działania obsługi tooperform hello ogólną kondycję hello platformy Azure. To zachowanie może mieć wpływ na dostępność maszyny Wirtualnej i jej zazwyczaj wynikiem hello sama akcja odzyskiwania automatycznego zgodnie z wcześniejszym opisem.  

Nieplanowane maintenances Uwzględnij hello następujące elementy:

- Defragmentacja pilnych węzła
- Aktualizacje przełącznik sieci pilnych

### <a name="vm-crashes"></a>Maszyna wirtualna awarii (Crash)
Maszyny wirtualne mogą ponownie z powodu problemów dotyczących w ramach hello samej maszyny Wirtualnej. Obciążenie Hello lub rolę, która działa na powitania maszyny Wirtualnej może wyzwolić sprawdzanie błędów w systemie operacyjnym gościa hello. Pomoc dotyczącą określania hello Przyczyna awarii hello Sprawdź dzienniki systemu i aplikacji hello dla maszyn wirtualnych systemu Windows, a hello serial dzienniki dla maszyn wirtualnych systemu Linux.

### <a name="storage-related-forced-shutdowns"></a>Związane z magazynowaniem wymuszone zamknięcia systemu
Maszyny wirtualne na platformie Azure polegają na dyski wirtualne dla systemu operacyjnego i magazynu danych, który znajduje się na powitania infrastruktury magazynu Azure. Zawsze, gdy łączność między hello maszyny Wirtualnej i hello skojarzone dyski wirtualne lub dostępności hello ma to wpływ na więcej niż 120 sekund, hello platformy Azure wykonuje wymuszone zamknięcie hello uszkodzenie danych tooavoid maszyn wirtualnych. maszyny wirtualne Hello automatycznie są zasilane ponownie po przywróceniu łączności magazynu. 

czas trwania Hello zamknięcia hello może składać się z pięciu minut, ale może być znacznie dłuższe. następujące Hello jest jednym z hello szczególnych przypadkach skojarzonych z magazynowaniem wymuszone zamknięcia: 

**Ogranicza przekraczającej we/wy**

Maszyny wirtualne mogą zostać tymczasowo zamknięcie żądań We/Wy są stale ograniczane, ponieważ hello liczby operacji We/Wy na sekundę (IOPS) przekracza limity hello We/Wy dysku hello. (Standardowe dysku magazynu jest ograniczona too500 IOPS.) toomitigate ten problem, użyj rozkładanie lub skonfigurować miejsca do magazynowania hello wewnątrz hello gościa maszyny Wirtualnej, w zależności od obciążenia hello. Aby uzyskać więcej informacji, zobacz [Konfigurowanie maszyn wirtualnych platformy Azure do uzyskania optymalnej wydajności magazynu](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Wyższe limity liczby dostępnych za pośrednictwem usługi Azure Premium Storage z się too80, 000 IOPS. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium wysokiej wydajności](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Inne zdarzenia
W rzadkich przypadkach powszechnie problem może mieć wpływ na wiele serwerów w centrum danych Azure. Jeśli ten problem występuje, hello Azure zespołu wysyła wiadomość e-mail powiadomienia subskrypcji toohello, których to dotyczy. Możesz sprawdzić hello [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/) i hello portal Azure hello stan trwającej awarii i poza zdarzenia.
