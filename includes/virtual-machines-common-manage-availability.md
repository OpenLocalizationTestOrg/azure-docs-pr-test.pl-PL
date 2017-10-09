## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Omówienie ponownych rozruchów maszyn wirtualnych — konserwacja a przestój
Istnieją trzy scenariusze, które może prowadzić maszyny toovirtual na platformie Azure, są w pełni funkcjonalne: sprzęt nieplanowana konserwacja, nieoczekiwane przestoje i zaplanowanej konserwacji.

* **Nieplanowanego zdarzenia konserwacji sprzętu** występuje, gdy hello platformy Azure prognozuje sprzętem hello lub żadnych platform składnika tooa skojarzone komputer fizyczny, jest o toofail. Gdy platforma hello prognozuje awarii, wystawi nieplanowane sprzętu obsługi zdarzeń tooreduce hello wpływ toohello maszyn wirtualnych hostowanych na sprzętem. Platforma Azure korzysta hello toomigrate technologii migracji na żywo maszyn wirtualnych z hello awarii sprzętu tooa dobrej kondycji komputera fizycznego. Migracja na żywo jest operacji, czy tylko pauzy hello maszyny wirtualnej przez krótki czas zachowywania maszyny Wirtualnej. Pamięci, otwartych plików i połączenia sieciowe, które są obsługiwane, ale wydajność może ulec zmniejszeniu przed i/lub po zdarzeniu hello. W przypadkach, gdy nie można użyć migracji na żywo hello maszyny Wirtualnej może wystąpić nieoczekiwane przestoje, zgodnie z poniższym opisem.


* **Nieoczekiwane przestoje** rzadko występuje, gdy sprzęt hello lub hello infrastruktury fizycznej podstawowej maszyny wirtualnej wystąpił błąd w określony sposób. Mogą być to awarie sieci lokalnej, błędy na dysku lokalnym lub inne awarie na poziomie regału. W przypadku wykrycia takiej awarii hello platformy Azure automatycznie zmigrowane (heals) sieci maszyny wirtualnej tooa dobrej kondycji komputera fizycznego. Podczas hello naprawianie procedury, maszyny wirtualne przestój (ponowny rozruch), a w niektórych przypadkach utraty hello tymczasowej stacji. Witaj dołączony systemu operacyjnego i dysków z danymi zawsze są zachowywane. 

* **Planowana konserwacja zdarzenia** okresowej aktualizacji przez Microsoft toohello bazowy tooimprove platformy Azure ogólną niezawodność, wydajność i bezpieczeństwo infrastruktury platformy hello, które są uruchamiane maszyny wirtualne. Większość tych aktualizacji jest przeprowadzana bez żadnego wpływu na działanie maszyn wirtualnych ani usług w chmurze (zobacz [konserwacja zachowująca maszyny wirtualne](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Chociaż hello platformy Azure w przypadkach możliwe wszystkie próby toouse zachowania obsługi maszyny Wirtualnej, istnieją rzadkich przypadkach gdy te aktualizacje wymagają ponownego uruchomienia maszyny wirtualnej tooapply hello wymagane aktualizacje toohello podstawowej infrastruktury. W takim przypadku można wykonać Azure planowanych konserwacji operację ponownego wdrażania konserwacji inicjując hello konserwacji dla ich maszyn wirtualnych w przedziale czasu odpowiedniego hello. Aby uzyskać więcej informacji, zobacz [Planned maintenance for virtual machines in Azure (Planowana konserwacja maszyn wirtualnych na platformie Azure)](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


wpływ hello tooreduce przestoju tooone lub jeden z tych zdarzeń, zalecamy hello następujące najlepsze rozwiązania wysokiej dostępności dla maszyn wirtualnych:

* [Konfigurowanie wielu maszyn wirtualnych w zestawie dostępności w celu zapewnienia nadmiarowości]
* [Używanie dysków zarządzanych dla maszyn wirtualnych w zestawie dostępności]
* [[Użyj tooVM odpowiedź tooproactively zaplanowane zdarzenia wpływające na zdarzenia] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Konfigurowanie każdej warstwy aplikacji w osobnych zestawach dostępności]
* [Łączenie modułu równoważenia obciążenia z zestawami dostępności]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Konfigurowanie wielu maszyn wirtualnych w zestawie dostępności w celu zapewnienia nadmiarowości
tooprovide nadmiarowość tooyour aplikacji zalecamy grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności. Ta konfiguracja zapewnia, że podczas albo planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jednej maszyny wirtualnej jest dostępna, i spełnia hello 99,95% umowy SLA platformy Azure. Aby uzyskać więcej informacji, zobacz hello [umowy SLA dla maszyn wirtualnych](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Unikaj pozostawiania pojedynczego wystąpienia maszyny wirtualnej w zestawie dostępności. Maszyny wirtualne w tej konfiguracji nie są objęte gwarancją umowy SLA. Podczas zdarzeń planowanej konserwacji platformy Azure może wystąpić przestój, z wyjątkiem sytuacji, gdy pojedyncza maszyna wirtualna korzystania z usługi [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md). Dla pojedynczego maszyn wirtualnych przy użyciu magazyn w warstwie premium stosuje hello umowy SLA platformy Azure.

Przypisano każdej maszyny wirtualnej w zestawie dostępności **domeny aktualizacji** i **domeny błędów** przez hello podstawowej platformy Azure. Dla zestawu dostępności danego pięć domeny użytkownika niekonfigurowalne aktualizacji są domyślnie przypisane (wdrożenia usługi Resource Manager będzie zwiększona tooprovide się domen aktualizacji too20) tooindicate grupy maszyn wirtualnych i używany sprzęt fizyczny który ponownego uruchomienia na powitania tym samym czasie. Gdy więcej niż pięć maszyny wirtualne są skonfigurowane w ramach zestawu dostępności pojedynczego, hello szóstego maszyny wirtualnej jest umieszczany w hello sama aktualizacja domeny jako hello pierwszej maszynie wirtualnej, hello siódme w hello hello drugiej maszyny wirtualnej, a więc same aktualizacji domeny na serwerze. kolejność Hello domen aktualizacji, które trwa ponowne uruchamianie nie można kontynuować sekwencyjnie podczas zaplanowanej konserwacji, ale tylko jedna aktualizacja domeny ponownego uruchomienia w czasie. Domeny aktualizacji po ponownym rozruchu otrzymuje toorecover 30 minut przed konserwacji jest inicjowane w domenie innej aktualizacji.

Witaj grupę maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania można zdefiniować domen błędów. Domyślnie skonfigurowany w zestawie dostępności maszyn wirtualnych hello są rozdzielone przez się toothree domen błędów w przypadku wdrożenia usługi Resource Manager (dwie fault domen klasycznego). Podczas umieszczenia maszyn wirtualnych w zbiorze dostępności nie chroni aplikacji z systemu operacyjnego lub w przypadku awarii specyficzne dla aplikacji, ogranicza wpływ hello potencjalnych awarii sprzętu fizycznego, awarii sieci lub przerw w działaniu zasilania.

<!--Image reference-->
   ![Rysunek koncepcyjny hello aktualizacji domeny i odporność domeny konfiguracji](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Używanie dysków zarządzanych dla maszyn wirtualnych w zestawie dostępności
Jeśli obecnie używasz maszyny wirtualne z dyskami niezarządzane, zdecydowanie zalecamy [przekonwertować maszyny wirtualne w zestawie dostępności dysków zarządzanych toouse](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Dyski zarządzane](../articles/virtual-machines/windows/managed-disks-overview.md) zapewniają większą niezawodność zestawów dostępności przez zapewnienie im hello dyski maszyn wirtualnych w zestawie dostępności są wystarczająco odizolowane od siebie tooavoid pojedynczych punktów awarii. Robi to automatycznie umieszczając hello dysków w klastrach innego magazynu. Jeśli klastra magazynów zakończy się niepowodzeniem ze względu na błąd toohardware lub oprogramowania, nie tylko hello wystąpień maszyny Wirtualnej z dyskami tych sygnatur.

![Domeny błędów dysku zarządzanego](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> Hello liczba domen błędów dla zestawów zarządzanych dostępności jest zależna od regionu - dwóch lub trzech dla regionu. Witaj poniższej tabeli przedstawiono numer hello na region

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Jeśli planujesz maszyn wirtualnych toouse o [niezarządzanych dysków](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), wykonaj poniżej najlepsze rozwiązania dotyczące kont magazynu, gdy wirtualne dyski twarde (VHD) maszyn wirtualnych są przechowywane jako [stronicowe](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Zachowaj wszystkie dyski (systemu operacyjnego i danych) skojarzone z maszyną Wirtualną w hello tego samego konta magazynu**
2. **Przejrzyj hello [limity](../articles/storage/common/storage-scalability-targets.md) hello liczby niezarządzanych dysków na koncie magazynu** przed dodaniem więcej konta magazynu tooa wirtualne dyski twarde
3. **Używaj oddzielnego konta magazynu dla każdej maszyny wirtualnej w zestawie dostępności.** Nie udostępniaj kont magazynu z wieloma maszynami wirtualnymi w hello tego samego zestawu dostępności. Dopuszczalne są maszyny wirtualne wielu różnych kont magazynu tooshare zestawów dostępności Jeśli powyżej najlepsze rozwiązania zostaną wykonane

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Konfigurowanie każdej warstwy aplikacji w osobnych zestawach dostępności
Jeśli maszyny wirtualne są wszystkie niemal identyczne i służą hello sam cel dla aplikacji, firma Microsoft zaleca, aby skonfigurować zbiór dostępności dla każdej warstwy aplikacji.  Jeśli umieścisz dwóch różnych tiers w hello sam zestawu dostępności wszystkich maszyn wirtualnych w tej samej warstwie aplikacji zostanie ponownie uruchomiony od razu hello. Skonfigurowanie co najmniej dwóch maszyn wirtualnych w zestawie dostępności dla każdej warstwy gwarantuje, że co najmniej jedna maszyna wirtualna w każdej warstwie jest dostępna.

Na przykład można umieścić wszystkich maszyn wirtualnych hello w hello fronton aplikacji uruchomionej w zestawie dostępności pojedynczego usług IIS, Apache, Nginx. Upewnij się, że tylko frontonu maszyny wirtualne są umieszczane w hello sam zestaw dostępności. Upewnij się również, że tylko maszyny wirtualne warstwy danych, takie jak replikowane maszyny wirtualne programu SQL Server lub maszyny wirtualne języka MySQL, są umieszczane we własnym zestawie dostępności.

<!--Image reference-->
   ![Warstwy aplikacji](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Łączenie modułu równoważenia obciążenia z zestawami dostępności
Łączenie hello [modułu równoważenia obciążenia Azure](../articles/load-balancer/load-balancer-overview.md) dostępności ustawić tooget hello odporność większości aplikacji. Witaj modułu równoważenia obciążenia Azure dystrybuuje ruch między wieloma maszynami wirtualnymi. Dla naszych maszyn wirtualnych w warstwie standardowa hello modułu równoważenia obciążenia Azure jest dołączony. Nie wszystkie warstwy maszyny wirtualnej obejmują hello modułu równoważenia obciążenia Azure. Aby uzyskać więcej informacji na temat równoważenia obciążenia maszyn wirtualnych, zobacz [Load Balancing virtual machines](../articles/virtual-machines/virtual-machines-linux-load-balance.md) (Równoważenie obciążenia maszyn wirtualnych).

Jeśli moduł równoważenia obciążenia hello nie jest skonfigurowany toobalance ruchu między wieloma maszynami wirtualnymi hello tylko obsługi ruchu maszyny wirtualnej, powodując warstwy aplikacji tooyour awarii wpływa na wszystkie zdarzenia zaplanowanej konserwacji. Umieszczenia wielu maszyn wirtualnych z hello same warstwy w obszarze hello same obciążenia równoważenia i dostępność zestawu umożliwia ruch toobe stale obsługiwanych przez co najmniej jedno wystąpienie.


<!-- Link references -->
[Konfigurowanie wielu maszyn wirtualnych w zestawie dostępności w celu zapewnienia nadmiarowości]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Konfigurowanie każdej warstwy aplikacji w osobnych zestawach dostępności]: #configure-each-application-tier-into-separate-availability-sets
[Łączenie modułu równoważenia obciążenia z zestawami dostępności]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Używanie dysków zarządzanych dla maszyn wirtualnych w zestawie dostępności]: #use-managed-disks-for-vms-in-an-availability-set
