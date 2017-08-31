

Dostępne są dwa poziomy równoważenia obciążenia dla usług infrastruktury platformy Azure:

* **Poziom DNS**: równoważenia obciążenia dla ruchu do usługi w chmurze różnych znajdujących się w różnych danych centrów do innej witryny sieci Web Azure znajduje się w różnych centrach danych lub zewnętrzne punkty końcowe. Jest to zrobić za pomocą usługi Azure Traffic Manager i okrężnego metody równoważenia obciążenia.
* **Sieci poziom**: przychodzący ruch internetowy do różnych maszyn wirtualnych usługi w chmurze Równoważenie obciążenia lub załadować równoważenie ruchu między maszynami wirtualnymi w sieci wirtualnej lub usługi w chmurze. Jest to zrobić za pomocą usługi równoważenia obciążenia Azure.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Menedżer ruchu równoważenia obciążenia dla usług w chmurze i witryn sieci Web
Traffic Manager pozwala kontrolować dystrybucję ruchu użytkowników do punktów końcowych, które mogą obejmować usługi w chmurze, witryn sieci Web, witryny zewnętrzne i innych profilów usługi Traffic Manager. Menedżer ruchu polega na stosowanie inteligentnego aparatu zasad do systemu nazw domen (DNS, Domain Name System) zapytania dotyczące nazw domen zasobów internetowych. Z usługi w chmurze lub witryny sieci Web mogą być uruchomione w różnych centrach danych całym świecie.

Aby skonfigurować punkty końcowe zewnętrznych lub profilów usługi Traffic Manager jako punktów końcowych musi użyć REST lub programu Windows PowerShell.

Menedżer ruchu używa trzech metod równoważenia obciążenia do dystrybucji ruchu:

* **Tryb failover**: Użyj tej metody można używać podstawowy punkt końcowy dla całego ruchu, ale Podaj kopii zapasowych w przypadku, gdy podstawowy jest niedostępny.
* **Wydajność**: Użyj tej metody, gdy masz punktów końcowych w różnych lokalizacjach geograficznych i żądania klienci mają używać "najbliższy" punktu końcowego pod względem najniższym opóźnieniu.
* **Działanie okrężne:** ta metoda umożliwia rozłożenie obciążenia na zbiór usług w chmurze w tym samym centrum danych lub usługi w chmurze lub witryny sieci Web w różnych centrach danych.

Aby uzyskać więcej informacji, zobacz [o ruchu Menedżera obciążenia równoważenia metody](../articles/traffic-manager/traffic-manager-routing-methods.md).

Na poniższym diagramie przedstawiono przykład metody dla Dystrybucja ruchu między usługi w chmurze innego równoważenia obciążenia okrężnego.

![obciążenia](./media/virtual-machines-common-load-balance/TMSummary.png)

Podstawowy proces jest następujący:

1. Internet klient wysyła zapytanie do nazwy domeny odpowiadający usługi sieci web.
2. DNS przesyła dalej żądanie nazwę zapytania do usługi Traffic Manager.
3. Menedżer ruchu wybiera następny usługi w chmurze na liście działanie okrężne i odsyła nazwy DNS. Klienta internetowego serwera DNS rozpoznaje nazwę na adres IP i wysyła go do klienta w sieci Internet.
4. Klienta internetowego nawiązuje połączenie z usługą w chmurze wybierany przez Menedżera ruchu.

Aby uzyskać więcej informacji, zobacz [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure równoważenia obciążenia dla maszyn wirtualnych
Usługi w chmurze maszyn wirtualnych w tej samej lub sieci wirtualnej mogą komunikować się ze sobą adresy bezpośrednio za pomocą ich prywatnego adresu IP. Komputerom i usługom poza usługą w chmurze lub sieci wirtualnej mogą komunikować się tylko z maszynami wirtualnymi w sieci wirtualnej ze skonfigurowanego punktu końcowego lub usługi w chmurze. Punkt końcowy jest mapowanie publicznego adresu IP i portu na prywatny adres IP i port maszyny wirtualnej lub roli sieci web w ramach usługi w chmurze Azure.

Moduł równoważenia obciążenia Azure losowo dystrybuuje określonego typu ruchu przychodzącego wielu maszyn wirtualnych lub usług w konfiguracji, znany jako zestaw o zrównoważonym obciążeniu. Na przykład mogą rozprzestrzeniać się obciążenie ruchu w sieci web żądania wielu serwerów sieci web lub role sieci web.

Na poniższym diagramie przedstawiono punktu końcowego równoważeniem obciążenia dla ruchu sieci web (niezaszyfrowany) standard, współużytkowany trzech maszyn wirtualnych dla publicznych i prywatnych port TCP 80. Te trzy maszyny wirtualne są w zestawie o zrównoważonym obciążeniu.

![obciążenia](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Aby uzyskać więcej informacji, zobacz [modułu równoważenia obciążenia Azure](../articles/load-balancer/load-balancer-overview.md). Aby uzyskać instrukcje dotyczące tworzenia zestawu z równoważeniem obciążenia, zobacz [skonfigurować zestawu z równoważeniem obciążenia](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure można również zrównoważeniu nakładu w ramach usługi w chmurze lub sieci wirtualnej. Jest on znany jako równoważenia obciążenia wewnętrznego i mogą być używane w następujący sposób:

* Ładowanie równowagi między serwerami w różnych warstw wielowarstwową aplikację (na przykład między warstwami sieci web i bazy danych).
* Ładowanie saldo — biznesowych (LOB) hostowanych w Azure bez konieczności dodatkowego obciążenia równoważenia sprzętu lub oprogramowania.
* Aby objąć serwerów lokalnych zestaw komputerów, których ruch jest obciążenia zrównoważone.

Podobnie jak Azure obciążenia równoważenia, wewnętrzny równoważenia obciążenia jest umożliwiają konfigurowanie wewnętrzny zestawu z równoważeniem obciążenia.

Na poniższym diagramie przedstawiono przykład wewnętrzny równoważeniem obciążenia punktu końcowego dla aplikacji biznesowych (LOB), współużytkowany trzech maszyn wirtualnych w sieci wirtualnej między lokalizacjami.

![obciążenia](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Zagadnienia dotyczące usługi równoważenia obciążenia
Moduł równoważenia obciążenia jest domyślnie skonfigurowany do limitu czasu usługi 4 minut bezczynności sesji. Jeśli nie ma konfiguracji Keep-Alive aplikacji za modułem równoważenia obciążenia pozostawia połączenie bezczynne przez więcej niż 4 minut, połączenie zostanie usunięty. Można zmienić zachowanie usługi równoważenia obciążenia umożliwiają [dłużej ustawienia limitu czasu dla usługi równoważenia obciążenia Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Inne zagadnieniem jest typ tryb dystrybucji obsługiwany przez usługi równoważenia obciążenia Azure. Można skonfigurować koligację IP źródła (źródłowy adres IP, docelowy adres IP) lub protokołu IP źródła (źródłowy adres IP, docelowy adres IP i protocol). Zapoznaj się z [tryb dystrybucji modułu równoważenia obciążenia Azure (źródłowego adresu IP koligacja)](../articles/load-balancer/load-balancer-distribution-mode.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać instrukcje dotyczące tworzenia zestawu z równoważeniem obciążenia, zobacz [skonfigurować wewnętrzny zestawu z równoważeniem obciążenia](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Aby uzyskać więcej informacji na temat usługi równoważenia obciążenia, zobacz [równoważenia obciążenia wewnętrznego](../articles/load-balancer/load-balancer-internal-overview.md).

