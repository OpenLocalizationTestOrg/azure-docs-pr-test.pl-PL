punkty końcowe tooAzure podejście Hello działa w sposób nieco inaczej między modelami wdrażania hello Classic i Menedżera zasobów. W modelu wdrażania usługi Resource Manager hello jest teraz dostępna hello elastyczność toocreate sieci filtry, które przepływ hello ruch do i z maszyn wirtualnych. Filtry te pozwalają toocreate złożonych środowiskach sieci poza proste punktu końcowego, tak jak hello klasycznego modelu wdrożenia. Ten artykuł zawiera omówienie grup zabezpieczeń sieci oraz sposób ich różnią się od przy użyciu klasycznego punktów końcowych, tworzenia tych reguł filtrowania i przykładowe scenariusze wdrażania.

## <a name="overview-of-resource-manager-deployments"></a>Omówienie wdrożenia usługi Resource Manager
Punkty końcowe w hello klasycznego modelu wdrożenia są zastępowane przez grup zabezpieczeń sieci i reguły listę kontroli dostępu (ACL) kontroli dostępu. Szybkie kroki stosowania reguły listy ACL grupy zabezpieczeń sieci są:

* Utwórz grupę zabezpieczeń sieci.
* tooallow lub Odmów ruchu, definiowania reguł listy ACL grupy zabezpieczeń sieci.
* Przypisz z interfejsem sieciowym tooa sieciowej grupy zabezpieczeń lub podsieć sieci wirtualnej.

Jeśli są pożądane tooalso wykonania przekierowania portów, należy tooplace modułu równoważenia obciążenia przed maszyny Wirtualnej i użyj reguł NAT. Szybkie kroki wdrażania usługi równoważenia obciążenia i reguł NAT, należy w następujący sposób:

* Tworzenie modułu równoważenia obciążenia.
* Tworzenie puli wewnętrznej bazy danych, a następnie dodaj pulę toohello maszyn wirtualnych.
* Definiowanie reguł NAT dla przekierowania portów hello wymagane.
* Przypisz reguł NAT tooyour maszyn wirtualnych.

## <a name="network-security-group-overview"></a>Grupy zabezpieczeń sieci — omówienie
Grupy zabezpieczeń sieci Podaj warstwę zabezpieczeń dla Ciebie tooallow określonych portów i tooaccess podsieci maszyn wirtualnych. Zwykle zawsze masz sieciowej grupy zabezpieczeń, zapewniając tej warstwy zabezpieczeń między maszynami wirtualnymi i hello poza world. Grup zabezpieczeń sieci może być zastosowane tooa podsieć sieci wirtualnej lub karty sieciowej określonej dla maszyny Wirtualnej. Zamiast tworzenia reguły listy ACL punktu końcowego, możesz teraz utworzyć reguły listy ACL grupy zabezpieczeń sieci. Te reguły listy ACL zapewniają znacznie większą kontrolę niż po prostu tworzenie tooforward punktu końcowego danego portu. Aby uzyskać więcej informacji, zobacz [co to jest grupa zabezpieczeń sieci?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Można przypisać podsieci toomultiple grup zabezpieczeń sieci lub do interfejsów sieciowych. Nie istnieje żadne mapowanie 1:1. Można utworzyć grupę zabezpieczeń sieci ze wspólnego zestawu reguł listy ACL i stosować toomultiple podsieci lub do interfejsów sieciowych. Co więcej, grupy zabezpieczeń sieci może być zastosowane tooresources między subskrypcją (na podstawie [kontroli dostępu na podstawie roli](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Omówienie usługi równoważenia obciążenia
W hello klasycznego modelu wdrożenia Azure będzie wykonywać wszystkie hello translatora adresów sieciowych (NAT) i portu przekazywanie na usługi w chmurze dla Ciebie. Podczas tworzenia punktu końcowego, należy określić tooexpose portu zewnętrznego hello wraz z hello wewnętrznego portu toodirect ruchu. Grupy zabezpieczeń sieci samodzielnie nie wykonuj tej samej NAT i przekazywania portu. 

tooallow toocreate reguł NAT dla takich portu przekazywania, tworzenia usługi równoważenia obciążenia Azure w grupie zasobów. Ponownie, usługi równoważenia obciążenia hello jest szczegółowym za mało tooonly zastosować toospecific maszyn wirtualnych, w razie potrzeby. Hello Azure załadować pracy reguły NAT modułu równoważenia obok tooprovide reguły listy ACL grupy zabezpieczeń sieci większą elastyczność i kontrolę niż osiągalne za pomocą punktów końcowych usługi w chmurze. Aby uzyskać więcej informacji, zobacz hello [Podgląd usługi równoważenia obciążenia](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Reguły listy ACL grupy zabezpieczeń sieci
Reguły listy ACL umożliwiają zdefiniowanie, jaki ruch mógł przepływać do i z maszyną Wirtualną na podstawie określonych portów, zakresy portów lub protokołów. Reguły są przypisywane tooindividual maszyn wirtualnych lub tooa podsieci. Przykładem reguły list kontroli dostępu dla typowych serwer sieci Web jest powitania po zrzut ekranu:

![Reguły listy ACL listy sieciowej grupy zabezpieczeń](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Reguły listy ACL są stosowane na wskazanym - metrykę priorytet hello wyższa wartość hello, niższy priorytet hello hello podstawie. Każda grupa zabezpieczeń sieci ma trzy domyślne zasady, które są zaprojektowane toohandle przepływu hello Azure ruchu sieciowego z jawnym `DenyAllInbound` hello końcowego reguły. Domyślne reguły listy ACL są podany toonot o niskim priorytecie zakłócać utworzone reguły.

## <a name="assigning-network-security-groups"></a>Przypisywanie sieciowej grupy zabezpieczeń
Można przypisać podsieci tooa sieciowej grupy zabezpieczeń lub karty sieciowej. Takie podejście pozwala toobe szczegółowe, zgodnie z potrzebami, po zastosowaniu Twojej listy ACL zasady tooonly określonej maszyny Wirtualnej lub upewnij się, wspólnego zestawu listy kontroli dostępu reguły są stosowane tooall maszyn wirtualnych należy do podsieci:

![Stosowanie grup NSG toonetwork interfejsów lub podsieci](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

zachowanie Hello hello sieciowej grupy zabezpieczeń nie zmienia się w zależności od przypisywane tooa podsieci lub karty sieciowej. Typowy scenariusz wdrażania zawiera powitalne sieciowej grupy zabezpieczeń przypisane tooa podsieci tooensure zgodności wszystkich podsieci dołączonych toothat maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [stosowania zabezpieczeń sieciowych grup tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Domyślne zachowanie grup zabezpieczeń sieci
W zależności od tego, jak i kiedy należy utworzyć swojej grupy zabezpieczeń sieci można tworzyć reguły domyślne dla maszyn wirtualnych systemu Windows toopermit RDP dostęp do portu 3389 protokołu TCP. Reguły domyślne dla maszyn wirtualnych systemu Linux zezwolenie na dostęp SSH na porcie TCP 22. Te reguły automatycznego listy ACL zostały utworzone na podstawie hello następujące warunki:

* Jeśli tworzenie maszyny Wirtualnej systemu Windows za pośrednictwem portalu hello i zaakceptować hello domyślna akcja toocreate sieciowej grupy zabezpieczeń, zostanie utworzony ACL reguły tooallow portu 3389 protokołu TCP (RDP).
* Jeśli tworzenie maszyny Wirtualnej systemu Linux za pośrednictwem portalu hello i zaakceptować hello domyślna akcja toocreate sieciowej grupy zabezpieczeń, tworzona jest port TCP tooallow reguły listy ACL 22 (SSH).

Te reguły listy ACL domyślne nie są tworzone w innych warunkach. Nie można połączyć tooyour maszyny Wirtualnej bez tworzenia hello odpowiednie reguły list kontroli dostępu. Te warunki są następujące typowe akcje hello:

* Tworzenie grupy zabezpieczeń sieci za pośrednictwem portalu hello jako osobną akcję toocreating hello maszyny Wirtualnej.
* Tworzenie grupy zabezpieczeń sieci programowo przy użyciu programu PowerShell, interfejsu wiersza polecenia Azure, interfejsów API Rest,... itd.
* Tworzenie maszyny Wirtualnej i przypisywania go tooan istniejącą sieciową grupę zabezpieczeń, który nie ma jeszcze hello odpowiednie reguły listy ACL zdefiniowane.

W wszystkich hello poprzedzających przypadków należy toocreate reguły list kontroli dostępu dla połączeń odpowiednie zdalne zarządzanie hello tooallow maszyny Wirtualnej.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Domyślne zachowanie maszyny wirtualnej bez grupy zabezpieczeń sieci
Można utworzyć Maszynę wirtualną bez tworzenia grupy zabezpieczeń sieci. W takich przypadkach możesz połączyć tooyour maszyny Wirtualnej za pomocą protokołu RDP lub SSH bez tworzenia reguł listy ACL. Podobnie jeśli zainstalowano usługę sieci web na porcie 80 tej usługi jest automatycznie dostępny zdalnie. Witaj maszyna wirtualna ma wszystkie porty.

> [!NOTE]
> Nadal potrzebujesz toohave publicznego adresu IP adres przypisany tooa maszyny Wirtualnej w kolejności dla każdego połączenia zdalnego. Nie ma grupy zabezpieczeń sieci dla interfejsu podsieci lub sieci hello nie ujawnia hello ruch zewnętrzny tooany maszyny Wirtualnej. Akcja domyślna Hello podczas tworzenia maszyny Wirtualnej za pośrednictwem portalu hello jest toocreate nowego publicznego adresu IP. Dla wszystkich pozostałych rodzajów tworzenia maszyny Wirtualnej, takie jak środowiska PowerShell, interfejsu wiersza polecenia Azure lub szablonu usługi Resource Manager publiczny adres IP nie jest tworzony automatycznie, chyba że jawnie żądanie. Akcja domyślna Hello za pośrednictwem portalu hello jest również toocreate grupy zabezpieczeń sieci. Ta akcja domyślna oznacza, że nie należy na końcu w sytuacji z narażonych maszynę Wirtualną, która nie ma sieci filtrowanie w miejscu.

## <a name="understanding-load-balancers-and-nat-rules"></a>Opis usługi równoważenia obciążenia i reguł NAT
W hello klasycznego modelu wdrożenia można utworzyć punkty końcowe, które również wykonać przekierowania portów. Po utworzeniu maszyny Wirtualnej w hello klasycznego modelu wdrożenia reguły list kontroli dostępu dla protokołu RDP lub SSH zostałyby utworzone automatycznie. Zasady te nie pozwala portu 3389 protokołu TCP lub portu TCP 22 odpowiednio toohello poza world. Zamiast tego portu TCP wysokiej wartości może być narażone mapujący toohello odpowiedni port wewnętrzny. Można również utworzyć własne reguły listy ACL w podobny sposób, takie jak Uwidacznianie serwer sieci Web na TCP port 4280 toohello poza world. Możesz zobaczyć te reguły list kontroli dostępu i mapowania portów w poniższych zrzut ekranu z portalu klasycznego hello hello:

![Przekierowania portów z punktami końcowymi Classic](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Z grup zabezpieczeń sieci ta funkcja przekierowania portów jest obsługiwany przez usługi równoważenia obciążenia. Aby uzyskać więcej informacji, zobacz [załadować siecią Azure](../articles/load-balancer/load-balancer-overview.md). Witaj poniższy przykład przedstawia usługę równoważenia obciążenia z NAT reguły tooperform przekierowania portów TCP port 4222 toohello wewnętrznego portu TCP 22 maszyny Wirtualnej:

![Reguły NAT modułu równoważenia dla przekierowania portów obciążenia](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Podczas implementowania usługi równoważenia obciążenia, zwykle nie zostaną przydzielone hello samej maszyny Wirtualnej publiczny adres IP. Zamiast tego modułu równoważenia obciążenia hello ma publiczny tooit przypisany adres IP. Nadal potrzebujesz toocreate Twojego sieciowej grupy zabezpieczeń i listy ACL reguły toodefine hello przepływu ruchu do i z maszyną Wirtualną. Witaj reguły NAT modułu równoważenia obciążenia są po prostu toodefine jakie porty są dozwolone za pośrednictwem usługi równoważenia obciążenia hello i jak uzyskać dystrybuowana zaplecza hello maszyn wirtualnych. Tak należy toocreate reguły NAT dla ruchu tooflow za pośrednictwem usługi równoważenia obciążenia hello. tooallow hello ruchu tooreach hello maszynę Wirtualną, Utwórz regułę listy ACL grupy zabezpieczeń sieci.
