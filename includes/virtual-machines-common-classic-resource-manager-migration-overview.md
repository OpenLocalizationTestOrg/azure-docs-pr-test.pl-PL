# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Obsługiwane platformy migracji zasobów IaaS z klasycznym tooAzure Resource Manager
W tym artykule opisano sposób jest włączenie migracji infrastruktury jako zasoby usługi (IaaS), z hello Classic tooResource Menedżera wdrażania modeli. Możesz przeczytać dodatkowe informacje [funkcje usługi Azure Resource Manager i korzyści](../articles/azure-resource-manager/resource-group-overview.md). Firma Microsoft szczegółowo sposób tooconnect zasobów z hello dwóch modeli wdrażania, które dostępne w ramach subskrypcji, za pomocą wirtualnej sieci bramy lokacja lokacja.

## <a name="goal-for-migration"></a>Cel dla migracji
Menedżer zasobów umożliwia wdrażanie złożonych aplikacji za pomocą szablonów, konfiguruje maszyn wirtualnych przy użyciu rozszerzeń maszyny Wirtualnej i dołącza zarządzania dostępem i znakowanie. Usługa Azure Resource Manager obejmuje skalowalne, równoległe wdrażanie maszyn wirtualnych do zestawów dostępności. nowy model wdrażania Hello także zarządzanie cyklem życia obliczeniowych, sieci i pamięci masowej niezależnie. Na koniec jest nacisk na włączenie zabezpieczeń domyślnie z wymuszania hello maszyn wirtualnych w sieci wirtualnej.

Prawie wszystkie funkcje hello z hello klasycznego modelu wdrażania są obsługiwane dla zasobów obliczeniowych, sieci i magazynu w obszarze usługi Azure Resource Manager. toobenefit z hello nowe możliwości usługi Azure Resource Manager, można migrować istniejące wdrożenia z hello klasycznego modelu wdrożenia.

## <a name="supported-resources-for-migration"></a>Obsługiwane zasobów do migracji
Te zasoby klasyczne IaaS są obsługiwane podczas migracji

* Maszyny wirtualne
* Zestawy dostępności
* Cloud Services
* Konta magazynu
* Sieci wirtualne
* Bramy VPN Gateway
* Express Route bram _(w hello tej samej subskrypcji co sieć wirtualna tylko)_
* Grupy zabezpieczeń sieci 
* Tabele tras 
* Zastrzeżone adresy IP 

## <a name="supported-scopes-of-migration"></a>Obsługiwane zakresy migracji
Istnieją różne sposoby 4 toocomplete migracji zasobów obliczeniowych, sieci i magazynu. Są to 

* Migracja maszyn wirtualnych (nie w sieci wirtualnej)
* Migracja maszyn wirtualnych (w sieci wirtualnej)
* Migracja kont magazynu
* Odłączyć zasobów (grup zabezpieczeń sieci, tabele tras i zastrzeżonych adresów IP)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migracja maszyn wirtualnych (nie w sieci wirtualnej)
W modelu wdrażania usługi Resource Manager hello zabezpieczenia są realizowane aplikacji domyślnie. Wszystkie maszyny wirtualne muszą toobe w sieci wirtualnej w hello modelu Resource Manager. Witaj ponowne uruchomienie platformy Azure (`Stop`, `Deallocate`, i `Start`) hello maszyn wirtualnych w ramach migracji hello. Dostępne są dwie opcje dla hello sieci wirtualnych, które hello maszyn wirtualnych, które będą migrowane do:

* Można zażądać hello platformy toocreate nowej sieci wirtualnej i przeprowadź migrację maszyny wirtualnej hello na powitania nowej sieci wirtualnej.
* Należy przeprowadzić migrację maszyny wirtualnej hello w istniejącej sieci wirtualnej w Menedżerze zasobów.

> [!NOTE]
> W tym zakresie migracji zarówno hello operacje zarządzania płaszczyzny i hello operacji płaszczyzna danych może nie być dozwolone w danym okresie czasu podczas migracji hello.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migracja maszyn wirtualnych (w sieci wirtualnej)
W przypadku większości konfiguracji maszyny Wirtualnej tylko metadane hello jest migrowana między modelami wdrażania hello Classic i Menedżera zasobów. Witaj podstawowej maszyny wirtualne są uruchomione na powitania sam sprzęt w hello sam sieci i z hello sam magazynu. operacje zarządzania płaszczyzny Hello niedozwolony przez wybrany okres czasu, podczas migracji hello. Jednak płaszczyzna danych hello nadal toowork. Oznacza to, że aplikacje uruchomione na maszynach wirtualnych (klasyczne) nie pociągnąć za sobą przestoju podczas migracji hello.

Witaj następujące konfiguracje nie są obecnie obsługiwane. Jeśli w przyszłości hello jest dodać obsługę, niektóre maszyny wirtualne w tej konfiguracji może pociągnąć za sobą przestoju (Przejdź do zatrzymania, deallocate i ponownego uruchamiania działania maszyny Wirtualnej).

* Masz więcej niż jeden zestaw w usłudze w chmurze jednej dostępności.
* Masz jeden lub więcej zestawów dostępności i maszyn wirtualnych, które nie są dostępne w zestawie w usłudze w chmurze jednej dostępności.

> [!NOTE]
> W tym zakresie migracji płaszczyzny zarządzania hello niedozwolony w danym okresie czasu podczas migracji hello. Dla niektórych konfiguracji opisanych wcześniej, płaszczyzna danych wystąpienia.
>
>

### <a name="storage-accounts-migration"></a>Migracja kont magazynu
tooallow bezproblemowe migracji, można wdrożyć maszyn wirtualnych Menedżera zasobów na koncie magazynu klasycznego. Dzięki tej możliwości obliczeniowych i zasobów sieciowych można i powinny być migrowane niezależnie od konta magazynu. Po migracji za pośrednictwem sieci maszyn wirtualnych i sieci wirtualnej, należy toomigrate za pośrednictwem procesu migracji hello toocomplete kont magazynu.

> [!NOTE]
> model wdrażania usługi Resource Manager Hello nie ma koncepcji hello Classic obrazy i dyski. Jeśli hello konta magazynu jest zmigrowane, klasycznym obrazy i dyski nie są widoczne w stosie usługi Resource Manager hello, ale hello kopii wirtualne dyski twarde pozostają w hello konta magazynu.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Odłączyć zasobów (grup zabezpieczeń sieci, tabele tras i zastrzeżonych adresów IP)
Sieciowe grupy zabezpieczeń, tabele tras i zastrzeżonych adresów IP, które nie są dołączone tooany, który maszyn wirtualnych i sieci wirtualne można migrować niezależnie.

<br>

## <a name="unsupported-features-and-configurations"></a>Nieobsługiwane funkcje i konfiguracji
Firma Microsoft aktualnie nie obsługują niektórych funkcjach i konfiguracjach. Witaj następujące sekcje opisują Nasze zalecenia wokół nich.

### <a name="unsupported-features"></a>Nieobsługiwane funkcje
Witaj, następujące funkcje nie są obecnie obsługiwane. Można opcjonalnie usunąć te ustawienia, Migrowanie maszyn wirtualnych hello i następnie ponownie Włącz ustawienia hello w modelu wdrażania usługi Resource Manager hello.

| Dostawca zasobów | Funkcja | Zalecenie |
| --- | --- | --- |
| Wystąpienia obliczeniowe |Dyski nieskojarzone maszyny wirtualnej. | obiekty BLOB dysków VHD Hello za te dyski zostaną uzyskać migracji w przypadku migrowania hello konta magazynu |
| Wystąpienia obliczeniowe |Obrazy maszyny wirtualnej. | obiekty BLOB dysków VHD Hello za te dyski zostaną uzyskać migracji w przypadku migrowania hello konta magazynu |
| Sieć |Listy ACL punktu końcowego. | Usuń listy ACL punktu końcowego, a następnie ponów próbę wykonania migracji. |
| Sieć |Sieć wirtualna zarówno bramę usługi ExpressRoute, jak i bramy sieci VPN  | Usuń hello bramy sieci VPN, przed rozpoczęciem migracji, a następnie utwórz ponownie hello bramy sieci VPN, po zakończeniu migracji. Dowiedz się więcej o [migracji ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Sieć |Usługi ExpressRoute z łączami autoryzacji  | Usuń połączenie sieciowe toovirtaul obwodu ExpressRoute hello przed rozpoczęciem migracji, a następnie utwórz ponownie połączenie hello, po zakończeniu migracji. Dowiedz się więcej o [migracji ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Sieć |Application Gateway | Usuń bramę aplikacji hello przed rozpoczęciem migracji, a następnie utwórz ponownie hello bramy aplikacji, po zakończeniu migracji. |
| Sieć |Sieci wirtualne przy użyciu sieci wirtualnej komunikacji równorzędnej. | Migracja sieci wirtualnej tooResource Manager, a następnie elementu równorzędnego. Dowiedz się więcej o [sieci wirtualnej komunikacji równorzędnej](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Nieobsługiwane konfiguracje
Witaj następujące konfiguracje nie są obecnie obsługiwane.

| Usługa | Konfiguracja | Zalecenie |
| --- | --- | --- |
| Resource Manager |Na podstawie dostępu kontroli ról (RBAC) w przypadku klasycznych zasobów |Ponieważ hello URI zasobów hello jest zmodyfikowane po migracji, zaleca się zaplanowanie hello RBAC zasad aktualizacji, które wymagają toohappen po migracji. |
| Wystąpienia obliczeniowe |Wiele podsieci skojarzone z maszyny Wirtualnej |Zaktualizuj hello podsieci konfiguracji tooreference tylko podsieci. |
| Wystąpienia obliczeniowe |Maszyny wirtualne, które należą tooa sieci wirtualnej, ale nie ma jawnego podsieci przypisane |Opcjonalnie można usunąć hello maszyny Wirtualnej. |
| Wystąpienia obliczeniowe |Maszyny wirtualne, które mają alertów, zasad automatycznego skalowania |Migracja Hello przechodzi przez i te ustawienia są usuwane. Zdecydowanie zaleca się dokonanie oceny środowiska przed hello migracji. Alternatywnie po zakończeniu migracji można ponownie skonfigurować ustawienia alertów hello. |
| Wystąpienia obliczeniowe |Rozszerzenia maszyny Wirtualnej XML (BGInfo 1.*, debuger programu Visual Studio Web Deploy i zdalnego debugowania) |Jest to nieobsługiwane. Zaleca się, że te rozszerzenia należy usunąć z hello toocontinue podczas migracji maszyny wirtualnej lub ich zostaną usunięte automatycznie podczas procesu migracji hello. |
| Wystąpienia obliczeniowe |Diagnostyki rozruchu z magazyn w warstwie Premium |Wyłącz funkcję diagnostyki rozruchu dla hello maszyn wirtualnych przed kontynuowaniem migracji. Można ponownie włączyć diagnostyki rozruchu w stosie usługi Resource Manager powitania po zakończeniu migracji hello. Ponadto obiektów blob, które są używane dla zrzut ekranu i serial dzienniki powinien zostać usunięty, więc nie są naliczane opłaty dla tych obiektów blob. |
| Wystąpienia obliczeniowe |Usługi w chmurze, zawierające role sieć web/proces roboczy. |To nie jest obecnie obsługiwane. |
| Sieć |Sieci wirtualne, które zawierają maszyny wirtualne i role sieć web/proces roboczy |To nie jest obecnie obsługiwane. |
| Azure App Service |Sieci wirtualne, które zawierają środowiska usługi aplikacji |To nie jest obecnie obsługiwane. |
| Usługa Azure HDInsight |Sieci wirtualne, które zawierają usługi HDInsight |To nie jest obecnie obsługiwane. |
| Usługi cyklu życia Microsoft Dynamics |Sieci wirtualne, które zawierają maszyny wirtualne, które są zarządzane przez usługi cyklu życia Dynamics |To nie jest obecnie obsługiwane. |
| Azure AD Domain Services |Sieci wirtualne, które zawierają usługi domenowe Azure AD |To nie jest obecnie obsługiwane. |
| Azure RemoteApp |Sieci wirtualne zawierające wdrożenia usługi Azure RemoteApp |To nie jest obecnie obsługiwane. |
| Usługa Azure API Management |Sieci wirtualne zawierające wdrożenia usługi Azure API Management |To nie jest obecnie obsługiwane. Witaj toomigrate IaaS sieci Wirtualnej, zmień hello VNET hello wdrożenia API Management, czyli żadna operacja przestoju. |
| Wystąpienia obliczeniowe |Centrum zabezpieczeń Azure rozszerzeń o sieć Wirtualną, która ma bramy sieci VPN w łączności przesyłania lub bramę usługi ExpressRoute z lokalnego serwera DNS |Centrum zabezpieczeń Azure automatycznie jest instalowana rozszerzeń na toomonitor sieci maszyn wirtualnych ich zabezpieczeń i zgłaszanie alertów. Rozszerzenia te zwykle uzyskać zainstalowana automatycznie, jeśli hello zasadami Centrum zabezpieczeń Azure jest włączona na powitania subskrypcji. Migracja bramy ExpressRoute nie jest obecnie obsługiwany, a bramy sieci VPN z połączeniem przesyłania utracenia dostępu lokalnego. Usuwanie ExpressRoute bramy lub Migrowanie bramy sieci VPN z połączeniem przesyłania powoduje, że internet access tooVM magazynu konta toobe utracone podczas kontynuowanie zatwierdzania hello migracji. w takim przypadku, ponieważ nie można wypełnić blob stan agenta gościa hello migracji Hello jest niemożliwa. Zalecane jest toodisable zasadami Centrum zabezpieczeń Azure w subskrypcji hello 3 godziny przed kontynuowaniem migracji. |

