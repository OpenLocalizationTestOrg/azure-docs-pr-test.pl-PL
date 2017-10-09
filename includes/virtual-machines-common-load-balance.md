

Dostępne są dwa poziomy równoważenia obciążenia dla usług infrastruktury platformy Azure:

* **Poziom DNS**: równoważenia obciążenia dla usług w chmurze toodifferent ruchu znajduje się w różnych danych centrów, toodifferent witryn sieci Web Azure znajduje się w różnych centrach danych lub tooexternal punktów końcowych. Jest to realizowane z usługi Azure Traffic Manager i hello okrężnego metoda równoważenia obciążenia.
* **Sieci poziom**: równoważenie przychodzące Internet ruchu toodifferent maszyn wirtualnych usługi w chmurze, lub załadować równoważenie ruchu między maszynami wirtualnymi w sieci wirtualnej lub usługi w chmurze. Można to zrobić z modułem równoważenia obciążenia Azure hello.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Menedżer ruchu równoważenia obciążenia dla usług w chmurze i witryn sieci Web
Menedżer ruchu umożliwia rozpowszechnianie hello toocontrol tooendpoints ruchu użytkownika, która może obejmować usługi w chmurze, witryn sieci Web, witryny zewnętrzne i innych profilów usługi Traffic Manager. Menedżer ruchu polega na stosowanie zasad inteligentnego aparatu tooDomain Name System (DNS) zapytania hello nazwy domen zasobów internetowych. Z usługi w chmurze lub witryny sieci Web mogą być uruchomione w różnych centrach danych między hello world.

Musisz użyć REST lub programu Windows PowerShell tooconfigure zewnętrzne punkty końcowe lub profilów usługi Traffic Manager jako punktów końcowych.

Menedżer ruchu używa trzech równoważenia obciążenia ruchu toodistribute metod:

* **Tryb failover**: Użyj tej metody, gdy mają toouse podstawowy punkt końcowy dla całego ruchu, ale zawiera kopie zapasowe, w przypadku hello podstawowy jest niedostępny.
* **Wydajność**: Użyj tej metody, gdy masz punktów końcowych w różnych lokalizacjach geograficznych i chcesz żądania klientów toouse hello "najbliższy" punktu końcowego pod względem hello można uzyskać najmniejsze opóźnienia.
* **Działanie okrężne:** tej metody należy użyć obciążenia toodistribute zestawu chmury usług w hello sam centrum danych lub usługi w chmurze lub witryny sieci Web w różnych centrach danych.

Aby uzyskać więcej informacji, zobacz [o ruchu Menedżera obciążenia równoważenia metody](../articles/traffic-manager/traffic-manager-routing-methods.md).

powitania po diagramie przedstawiono przykład hello okrężnego metoda równoważenia obciążenia dla Dystrybucja ruchu między usługami inną chmurę.

![obciążenia](./media/virtual-machines-common-load-balance/TMSummary.png)

Witaj podstawowy proces przebiega hello następujące czynności:

1. Internet klient wysyła zapytanie do domeny nazwę odpowiedniego tooa usługi sieci web.
2. DNS przekazuje hello nazwę zapytania żądania tooTraffic menedżera.
3. Menedżera ruchu wybiera hello dalej usługi w chmurze w hello listy działanie okrężne i wysyła ponownie hello nazwy DNS. Serwer DNS klienta internetowego Hello jest rozpoznawany jako adres IP tooan nazwa hello i wysyła je z klienta internetowego toohello.
4. powitania klienta internetowego nawiązuje połączenie z usługą w chmurze hello wybierany przez Menedżera ruchu.

Aby uzyskać więcej informacji, zobacz [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure równoważenia obciążenia dla maszyn wirtualnych
Maszyny wirtualne w hello tej samej usługi w chmurze lub sieci wirtualnej mogą komunikować się ze sobą bezpośrednio przy użyciu swoich prywatnych adresów IP. Usługi w chmurze komputerom i usługom poza hello lub sieci wirtualnej mogą komunikować się tylko z maszynami wirtualnymi w sieci wirtualnej ze skonfigurowanego punktu końcowego lub usługi w chmurze. Punkt końcowy jest mapowanie publicznego adresu IP i portu toothat prywatnego adresu IP i portu maszyny wirtualnej lub roli sieci web w ramach usługi w chmurze Azure.

Hello Azure Load Balancer losowo dystrybuuje określonego typu ruchu przychodzącego wielu maszyn wirtualnych lub usług w konfiguracji, znany jako zestaw o zrównoważonym obciążeniu. Na przykład wielu serwerów sieci web lub role sieci web można rozmieścić hello obciążenia ruchu żądania sieci web.

Witaj Poniższy diagram przedstawia punktu końcowego równoważeniem obciążenia dla ruchu sieci web (niezaszyfrowany) standard, współużytkowany trzech maszyn wirtualnych do hello publiczne i prywatne port TCP 80. Te trzy maszyny wirtualne są w zestawie o zrównoważonym obciążeniu.

![obciążenia](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Aby uzyskać więcej informacji, zobacz [modułu równoważenia obciążenia Azure](../articles/load-balancer/load-balancer-overview.md). Aby hello kroki toocreate zestawu z równoważeniem obciążenia, zobacz [skonfigurować zestawu z równoważeniem obciążenia](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure można również zrównoważeniu nakładu w ramach usługi w chmurze lub sieci wirtualnej. Jest on znany jako równoważenia obciążenia wewnętrznego i mogą być używane w hello następujące sposoby:

* tooload równowagi między serwerami w różnych warstwach wielowarstwową aplikację (na przykład między warstwami sieci web i bazy danych).
* tooload saldo — biznesowych (LOB) aplikacje hostowane na platformie Azure, bez konieczności dodatkowego obciążenia równoważenia sprzętu lub oprogramowania.
* tooinclude serwery lokalne powitania zestawu komputerów, których ruch jest równoważone.

Podobne tooAzure równoważenia obciążenia, wewnętrzny równoważenia obciążenia jest umożliwiają konfigurowanie wewnętrzny zestawu z równoważeniem obciążenia.

powitania po diagramie przedstawiono przykład wewnętrzny równoważeniem obciążenia punktu końcowego dla aplikacji biznesowych (LOB), współużytkowany trzech maszyn wirtualnych w sieci wirtualnej między lokalizacjami.

![obciążenia](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Zagadnienia dotyczące usługi równoważenia obciążenia
Moduł równoważenia obciążenia jest domyślnie konfigurowana tootimeout jako 4 minut bezczynności sesji. Jeśli nie ma konfiguracji Keep-Alive aplikacji za modułem równoważenia obciążenia pozostawia połączenie bezczynne przez więcej niż 4 minut, hello połączenia zostaną usunięte. Możesz zmienić tooallow zachowanie usługi równoważenia obciążenia hello [dłużej ustawienia limitu czasu dla usługi równoważenia obciążenia Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Inne zagadnieniem jest typ hello trybu dystrybucji obsługiwanych przez usługi równoważenia obciążenia Azure. Można skonfigurować koligację IP źródła (źródłowy adres IP, docelowy adres IP) lub protokołu IP źródła (źródłowy adres IP, docelowy adres IP i protocol). Zapoznaj się z [tryb dystrybucji modułu równoważenia obciążenia Azure (źródłowego adresu IP koligacja)](../articles/load-balancer/load-balancer-distribution-mode.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
Aby hello kroki toocreate zestawu z równoważeniem obciążenia, zobacz [skonfigurować wewnętrzny zestawu z równoważeniem obciążenia](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Aby uzyskać więcej informacji na temat usługi równoważenia obciążenia, zobacz [równoważenia obciążenia wewnętrznego](../articles/load-balancer/load-balancer-internal-overview.md).

