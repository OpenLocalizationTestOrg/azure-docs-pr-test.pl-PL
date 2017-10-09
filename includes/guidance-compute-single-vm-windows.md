W tym artykule opisano zestaw sprawdzonych rozwiązań dotyczących uruchamiania maszyny wirtualnej systemu Windows (VM) na platformie Azure, zwracając uwagę tooscalability, dostępności, możliwości zarządzania i zabezpieczeń.

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania: [usługi Azure Resource Manager] [ resource-manager-overview] i klasycznym. W tym artykule jest używana usługa Resource Manager, którą firma Microsoft zaleca w przypadku nowych wdrożeń.
>
>

Nie zalecamy używania pojedynczej maszyny wirtualnej dla obciążeń o znaczeniu krytycznym, ponieważ powoduje to powstanie pojedynczego punktu awarii. Aby uzyskać wyższą dostępność, należy wdrożyć wiele maszyn wirtualnych w postaci [zestawu dostępności][availability-set]. Aby uzyskać więcej informacji, zobacz [Running multiple VMs on Azure][multi-vm] (Uruchamianie wielu maszyn wirtualnych na platformie Azure).

## <a name="architecture-diagram"></a>Diagram architektury

Inicjowanie obsługi administracyjnej maszyny Wirtualnej na platformie Azure obejmuje części przenoszenie więcej niż tylko hello samej maszyny Wirtualnej. Brak elementów obliczeniowych, sieci i magazynu.

> Dokument programu Visio, który zawiera ten diagram architektury jest dostępny do pobrania z hello [Centrum pobierania Microsoft][visio-download]. Ten diagram znajduje się na powitania "Obliczeń - jednej maszyny Wirtualnej" strony.
>
>

![[0]][0]

* **Grupa zasobów.** [*Grupa zasobów*][resource-manager-overview] to kontener, który zawiera powiązane zasoby. Utwórz zasób grupy toohold hello zasoby dla tej maszyny Wirtualnej.
* **Maszyna wirtualna**. Można udostępnić Maszynę wirtualną z listy obrazów opublikowanych lub z pliku wirtualnego dysku twardego (VHD) przekazanie tooAzure magazynu obiektów Blob.
* **Dysk systemu operacyjnego.** dysk systemu operacyjnego Hello jest plik VHD przechowywany w [usługi Azure Storage][azure-storage]. Oznacza to, że istnieje, nawet wtedy, gdy komputer hosta hello przestanie działać.
* **Dysk tymczasowy.** Witaj utworzeniu maszyny Wirtualnej z dysku tymczasowym (hello `D:` dysku w systemie Windows). Ten dysk jest przechowywana na dysku fizycznego na komputerze-hoście hello. *Nie* jest on zapisany w usłudze Azure Storage i może zostać usunięty podczas ponownego uruchamiania i innych zdarzeń cyklu życia maszyny wirtualnej. Używaj tego dysku tylko dla danych tymczasowych, takich jak plik stronicowania lub plik wymiany.
* **Dyski danych.** [Dysk danych][data-disk] to trwały plik VHD używany na potrzeby danych aplikacji. Dyski danych są przechowywane w usłudze Azure Storage, takie jak dysk hello systemu operacyjnego.
* **Sieć wirtualna i podsieci.** Każda maszyna wirtualna na platformie Azure jest wdrażana w sieci wirtualnej, która jest podzielona na podsieci.
* **Publiczny adres IP.** Publiczny adres IP jest wymagane toocommunicate z hello wirtualna&mdash;na przykład za pośrednictwem pulpitu zdalnego (RDP).
* **Interfejs sieciowy (karta sieciowa)**. Witaj kart interfejsu Sieciowego umożliwia hello toocommunicate maszyny Wirtualnej z siecią wirtualną hello.
* **Sieciowa grupa zabezpieczeń**. Witaj [NSG] [ nsg] jest używane tooallow/niezezwalania podsieci toohello ruchu w sieci. Możesz skojarzyć sieciową grupę zabezpieczeń z konkretną kartą sieciową lub z podsiecią. Jeśli skojarzona z podsiecią, reguły NSG hello zastosować tooall maszyn wirtualnych, w tej podsieci.
* **Diagnostyka.** Rejestrowanie diagnostyczne jest niezwykle ważny do zarządzania i rozwiązywania problemów hello maszyny Wirtualnej.

## <a name="recommendations"></a>Zalecenia

Zastosuj Hello następujące zalecenia dla większości scenariuszy. Należy się do nich stosować, jeśli nie ma konkretnych wymagań, które byłyby z nimi sprzeczne.

### <a name="vm-recommendations"></a>Zalecenia dotyczące maszyny wirtualnej

Platforma Azure oferuje wiele rozmiary inną maszynę wirtualną, ale zalecamy hello i GS-serii DS, ponieważ obsługuje rozmiary maszyny [magazyn w warstwie Premium][premium-storage]. Wybierz jeden z tych rozmiarów maszyny, chyba że obciążenie ma specyficzne wymagania, tak jak w przypadku obliczeń o wysokiej wydajności. Aby uzyskać szczegółowe informacje, zobacz [Virtual machine sizes][virtual-machine-sizes] (Rozmiary maszyny wirtualnej).

Jeśli przenosisz istniejących tooAzure obciążenia start hello najbliższego dopasowania tooyour ma rozmiar maszyny Wirtualnej hello serwery lokalne. Następnie wydajność hello miary rzeczywistej obciążenia z przestrzegania tooCPU, pamięci i dysku operacje wejścia/wyjścia na sekundę (IOPS) i Dostosuj rozmiar hello w razie potrzeby. Jeśli potrzebujesz wielu kart sieciowych dla sieci maszyny Wirtualnej, należy pamiętać, że hello maksymalną liczbę kart sieciowych jest funkcją hello [rozmiar maszyny Wirtualnej][vm-size-tables].   

Podczas obsługi administracyjnej hello maszyny Wirtualnej i innych zasobów, należy określić region. Ogólnie rzecz biorąc, wybierz region najbliższy tooyour użytkowników wewnętrznych lub klientów. Jednak nie wszystkie rozmiarów maszyn wirtualnych mogą być dostępne we wszystkich regionach. Aby uzyskać więcej informacji, zobacz [usług według regionu][services-by-region]. toosee listę hello rozmiarów maszyn wirtualnych dostępnych w danym regionie, uruchom hello następujące polecenia Azure interfejsu wiersza polecenia (CLI):

```
azure vm sizes --location <location>
```

Aby uzyskać informacje dotyczące wybierania opublikowanego obrazu maszyny Wirtualnej, zobacz [Nawigacja i wybierz obrazy maszyny wirtualnej systemu Windows Azure Powershell lub interfejsu wiersza polecenia][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Zalecenia dotyczące dysku i magazynu

Aby uzyskać najlepszą wydajność We/Wy dysku, zalecamy [magazyn w warstwie Premium][premium-storage], która przechowuje dane na dyskach półprzewodnikowych (SSD). Koszt jest oparta na powitania rozmiar dysku elastycznie hello. IOPS i przepływności, również są zależne od rozmiaru dysku, dlatego podczas obsługi administracyjnej dysku, należy rozważyć trzech czynników (pojemności, IOPS i przepływność).

Utwórz konta oddzielny magazyn Azure dla każdej maszyny Wirtualnej toohold hello wirtualnych dysków twardych (VHD) w kolejności tooavoid naciśnięcie hello limity liczby kont magazynu.

Dodaj co najmniej jeden dysk danych. Podczas tworzenia nowego wirtualnego dysku twardego jest niesformatowany. Zaloguj się do hello wirtualna tooformat hello dysku. Jeśli masz dużą liczbę dysków danych należy pamiętać o hello całkowita limity wejścia/wyjścia hello konta magazynu. Aby uzyskać więcej informacji, zobacz [Virtual machine disk limits][vm-disk-limits] (Limity dysku maszyny wirtualnej).

Jeśli to możliwe, należy zainstalować aplikacje na dysk z danymi, nie hello dysku systemu operacyjnego. Jednak niektóre starsze aplikacje mogą wymagać tooinstall składników na powitania dysku C:. W takim przypadku można [zmiana rozmiaru dysku systemu operacyjnego hello] [ resize-os-disk] przy użyciu programu PowerShell.

Aby uzyskać najlepszą wydajność należy utworzyć oddzielnego konta magazynu toohold dzienników diagnostycznych. Standardowe konto magazynu lokalnie nadmiarowego (LRS, locally redundant storage) jest wystarczające dla dzienników diagnostycznych.

### <a name="network-recommendations"></a>Zalecenia dotyczące sieci

Witaj publicznego adresu IP może być dynamicznej lub statycznej. domyślne Hello jest dynamiczny.

* Rezerwacja [statyczny adres IP] [ static-ip] konieczne będzie stałego adresu IP, który nie zmieni się &mdash; na przykład, jeśli potrzebujesz toocreate A rejestrowania w systemie DNS lub wymagają hello listy bezpiecznych dodano tooa toobe adresu IP.
* Istnieje również możliwość utworzenia w pełni kwalifikowaną nazwą domeny (FQDN) dla adresu IP hello. Następnie możesz zarejestrować [rekord CNAME] [ cname-record] w systemie DNS wskazujący toohello nazwy FQDN. Aby uzyskać więcej informacji, zobacz [utworzenia w pełni kwalifikowaną nazwą domeny w portalu Azure hello][fqdn].

Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw [domyślnych reguł][nsg-default-rules], tym regułę blokującą cały ruch przychodzący z Internetu. Nie można usunąć reguły domyślne Hello, ale inne zasady można zastąpić je. tooenable ruch internetowy, utworzyć reguły zezwalające na ruch przychodzący porty toospecific &mdash; np. port 80 dla protokołu HTTP.  

tooenable RDP, Dodaj regułę grupy NSG, która zezwala na ruch przychodzący tooTCP portu 3389.

## <a name="scalability-considerations"></a>Zagadnienia dotyczące skalowalności

Można skalować Maszynę wirtualną w górę lub w dół przez [zmieniania rozmiaru maszyny Wirtualnej hello](../articles/virtual-machines/windows/sizes.md). tooscale się poziomo, poddane co najmniej dwie maszyny wirtualne dostępności ustawiona za modułem równoważenia obciążenia. Aby uzyskać więcej informacji, zobacz [uruchomienia wielu maszyn wirtualnych na platformie Azure skalowalność i dostępność][multi-vm].

## <a name="availability-considerations"></a>Zagadnienia dotyczące dostępności

Aby uzyskać wyższą dostępność, wdróż wiele maszyn wirtualnych w postaci zestawu dostępności. Zapewnia również wyższej [umowę dotyczącą poziomu usług] [ vm-sla] (SLA).

Na maszynę wirtualną może mieć wpływ [zaplanowana konserwacja][planned-maintenance] lub [nieplanowana konserwacja][manage-vm-availability]. Można użyć [dzienniki reboot wirtualna] [ reboot-logs] toodetermine czy ponowny rozruch maszyny Wirtualnej spowodowane przez zaplanowanej konserwacji.

Pliki VHD są przechowywane w usłudze [Azure Storage][azure-storage], która jest replikowana w celu zapewnienia trwałości i dostępności.

tooprotect przed przypadkowej utracie danych podczas wykonywania normalnych operacji (na przykład ze względu na błąd użytkownika), należy również zaimplementować w chwili tworzenia kopii zapasowych, przy użyciu [migawki obiektu blob] [ blob-snapshot] lub innego narzędzia.

## <a name="manageability-considerations"></a>Zagadnienia dotyczące możliwości zarządzania

**Grupy zasobów.** Umieść ściśle powiązane zasoby tego hello udziału cyklu życia tej samej do hello sam [grupy zasobów][resource-manager-overview]. Grupy zasobów umożliwiają toodeploy i monitorowania zasobów w grupie i rzutowanie rozliczeń koszty według grupy zasobów. Można również usunąć zasoby jako zestaw, co jest bardzo przydatne w przypadku wdrożeń testowych. Zasobom należy nadawać opisowe nazwy. Czy umożliwia łatwiejsze toolocate określonego zasobu i zrozumieć, jego rolą. Zobacz [Zalecane konwencje nazewnictwa dla zasobów platformy Azure][naming conventions].

**Diagnostyka maszyny wirtualnej.** Włącz monitorowanie i diagnostykę, w tym podstawowe metryki kondycji, dzienniki infrastruktury diagnostyki i [diagnostykę rozruchu][boot-diagnostics]. Diagnostyki rozruchu ułatwia diagnozowanie awarii rozruchu, jeśli maszyny Wirtualnej pobiera stan nonbootable. Aby uzyskać więcej informacji, zobacz [Włączanie monitorowania i diagnostyki][enable-monitoring]. Użyj hello [zbierania dzienników Azure] [ log-collector] toocollect rozszerzenia platformy Azure dzienniki i przekazać je tooAzure magazynu.   

Witaj następujące polecenia interfejsu wiersza polecenia umożliwia diagnostyki:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Zatrzymywanie maszyny wirtualnej.** Platforma Azure rozróżnia między stanami „zatrzymana” i „cofnięty przydział”. Naliczane są opłaty po zatrzymaniu hello stanu maszyny Wirtualnej, ale nie po deallocated hello maszyny Wirtualnej.

Użyj powitania po toodeallocate polecenia interfejsu wiersza polecenia maszyny Wirtualnej:

```
azure vm deallocate <resource-group> <vm-name>
```

W portalu Azure hello, hello **zatrzymać** przycisk cofa alokację hello maszyny Wirtualnej. Jednak Jeśli wyłączysz się za pośrednictwem hello systemu operacyjnego, logując się hello maszyny Wirtualnej jest zatrzymana, ale *nie* alokację, więc możesz nadal będą naliczane.

**Usuwanie maszyny wirtualnej.** Po usunięciu maszyny Wirtualnej hello wirtualne dyski twarde nie są usuwane. Oznacza to, że można bezpiecznie usunąć hello maszyny Wirtualnej bez utraty danych. Jednak opłaty za magazyn będą w dalszym ciągu naliczane. Witaj toodelete wirtualnego dysku twardego, usuń plik hello z [magazynu obiektów Blob][blob-storage].

tooprevent przypadkowego usunięcia, użyj [Blokada zasobu] [ resource-lock] toolock hello zasobów całej grupy lub blokady poszczególne zasoby, takie jak hello maszyny Wirtualnej.

## <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami

Użyj [Centrum zabezpieczeń Azure] [ security-center] tooget centralnej widok hello stan zabezpieczeń zasobów platformy Azure. Centrum zabezpieczeń monitoruje potencjalnych problemów z zabezpieczeniami i zapewnia zaawansowany przegląd kondycji zabezpieczeń hello wdrożenia. Centrum zabezpieczeń jest skonfigurowany dla subskrypcji platformy Azure. Włącz zbieranie danych zabezpieczeń, zgodnie z opisem w [korzystanie z Centrum zabezpieczeń]. Po włączeniu funkcji zbierania danych Centrum zabezpieczeń automatycznie skanuje wszystkie maszyny wirtualne utworzone w ramach tej subskrypcji.

**Zarządzanie poprawkami.** Jeśli opcja jest włączona, Centrum zabezpieczeń sprawdza, czy aktualizacje zabezpieczeń i krytyczne są Brak. Użyj [ustawień zasad grupy] [ group-policy] na aktualizacje automatyczne systemu tooenable wirtualna hello.

**Ochrony przed złośliwym oprogramowaniem.** Jeśli opcja jest włączona, Centrum zabezpieczeń sprawdza, czy zainstalowano oprogramowanie chroniące przed złośliwym kodem. Można również użyć Centrum zabezpieczeń tooinstall ochrony przed złośliwym oprogramowaniem z wewnątrz hello portalu Azure.

**Operacje.** Użyj [kontroli dostępu opartej na rolach] [ rbac] (RBAC) toocontrol dostępu toohello Azure zasoby wdrażane. RBAC można przypisać autoryzacji ról toomembers Twojego zespołu DevOps. Na przykład rolę czytelnika hello można wyświetlać zasoby platformy Azure, ale nie tworzenia, zarządzania lub je usunąć. Niektóre role są tooparticular określonych typów zasobów platformy Azure. Na przykład hello roli współautora maszyny wirtualnej można ponownie uruchomić lub Cofnij Przydział maszyny Wirtualnej, zresetować hasła administratora hello, tworzenie nowej maszyny Wirtualnej itd. Inne [wbudowane role kontroli RBAC][rbac-roles] potencjalnie przydatne w przypadku tej architektury referencyjnej to [Użytkownik usługi DevTest Labs][rbac-devtest] i [Współautor sieci][rbac-network]. Użytkownika można przypisać role toomultiple i można tworzyć role niestandardowe dla jeszcze bardziej szczegółowe uprawnienia.

> [!NOTE]
> RBAC nie ogranicza hello akcje, które może wykonywać użytkownik zalogowany do maszyny Wirtualnej. Te uprawnienia są określane przez typ konta hello na system operacyjny gościa hello.   
>
>

hasło administratora lokalnego hello tooreset Uruchom hello `vm reset-access` polecenia wiersza polecenia platformy Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Użyj [dzienniki inspekcji] [ audit-logs] toosee inicjowania obsługi administracyjnej akcje oraz inne zdarzenia maszyny Wirtualnej.

**Szyfrowanie danych.** Należy wziąć pod uwagę [szyfrowania dysków Azure] [ disk-encryption] Jeśli potrzebujesz hello tooencrypt systemu operacyjnego i dysków z danymi.

## <a name="solution-deployment"></a>Wdrażanie rozwiązania

Wdrożenia dla tej architektury dokumentacja jest dostępna w [GitHub][github-folder]. Obejmuje ono sieć wirtualną, sieciową grupę zabezpieczeń i pojedynczą maszynę wirtualną. toodeploy hello architektury, wykonaj następujące kroki:

1. Kliknij prawym przyciskiem myszy przycisk hello poniżej i wybierz albo "link Otwórz na nowej karcie" lub "Otwórz łącze w nowym oknie."  
   [![Wdrażanie tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Po otwarciu hello łącze w hello portalu Azure, należy wprowadzić wartości dla niektórych ustawień hello:

   * Witaj **grupy zasobów** nazwa jest już zdefiniowana w pliku parametrów hello, dlatego wybierz **Utwórz nowy** , a następnie wprowadź `ra-single-vm-rg` w polu tekstowym hello.
   * Wybierz hello region z hello **lokalizacji** listy rozwijanej.
   * Nie należy edytować hello **szablonu głównego Uri** lub hello **parametr Uri głównego** pól tekstowych.
   * Wybierz **windows** w hello **typ systemu operacyjnego** listy rozwijanej.
   * Przejrzyj hello warunków i postanowień, a następnie kliknij przycisk hello **zgadzam się toohello warunki i postanowienia, o których wspomniano** wyboru.
   * Polecenie hello **zakupu** przycisku.
3. Poczekaj na powitania toocomplete wdrożenia.
4. pliki parametrów Hello obejmują ustalony administratora nazwę użytkownika i hasło i zdecydowanie zaleca się natychmiast zmianę jednocześnie. Polecenie hello maszyny Wirtualnej o nazwie `ra-single-vm0 `w hello portalu Azure. Następnie kliknij **resetowania hasła** w hello **pomocy technicznej i rozwiązywania problemów** bloku. Wybierz **resetowania hasła** w hello **tryb** pole listy rozwijanej, następnie wybierz nową **nazwy użytkownika** i **hasło**. Kliknij przycisk hello **aktualizacji** przycisk toopersist hello nową nazwę użytkownika i hasło.

Dla informacji na temat innych sposobów toodeploy to odwołanie architektury, zobacz plik readme hello w hello [wskazówki jednym vm][github-folder]] folderu GitHub.

## <a name="customize-hello-deployment"></a>Dostosowywanie hello wdrożenia
Toochange hello wdrożenia toomatch potrzeb, należy wykonaj instrukcje hello hello [readme][github-folder].

## <a name="next-steps"></a>Następne kroki
Aby uzyskać wyższą dostępność, należy wdrożyć co najmniej dwie maszyny wirtualne za modułem równoważenia obciążenia. Aby uzyskać więcej informacji, zobacz [Running multiple VMs on Azure][multi-vm] (Uruchamianie wielu maszyn wirtualnych na platformie Azure).

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[korzystanie z Centrum zabezpieczeń]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Pojedynczy Architektura maszyny Wirtualnej systemu Windows na platformie Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
