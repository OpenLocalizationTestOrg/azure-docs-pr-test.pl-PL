### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Których systemów operacyjnych klienta można używać z połączeniami typu punkt-lokacja?

obsługiwane są następujące systemy operacyjne klienta Hello:

* Windows 7 (32-bitowy i 64-bitowy)
* Windows Server 2008 R2 (tylko 64-bitowy)
* Windows 8 (32-bitowy i 64-bitowy)
* Windows 8.1 (32-bitowy i 64-bitowy)
* Windows Server 2012 (tylko 64-bitowy)
* Windows Server 2012 R2 (tylko 64-bitowy)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Czy można użyć dowolnego oprogramowania klienta VPN do połączenia punkt-lokacja obsługującego protokół SSTP?

Nie. Pomoc techniczna jest ograniczona tylko toohello wersje systemu operacyjnego Windows wymienionych powyżej.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Ile punktów końcowych klienta sieci VPN może obejmować konfiguracja punkt-lokacja?

Firma Microsoft obsługuje konto too128 VPN klientów toobe stanie tooconnect tooa sieci wirtualnej z hello sam czas.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Czy w przypadku połączenia punkt-lokacja można użyć własnego głównego urzędu certyfikacji PKI?

Tak. Wcześniej można było używać tylko certyfikatów głównych z podpisem własnym. Nadal można przesłać 20 certyfikatów głównych.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Czy można pominąć serwery proxy i zapory, korzystając z funkcji punkt-lokacja?

Tak. Używamy tootunnel SSTP (Secure Socket Tunneling Protocol) za pośrednictwem zapór. Ten tunel zostanie wyświetlony jako połączenie HTTPs.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Jeśli I ponownie uruchom komputer kliencki skonfigurowany dla lokacji punktu, zostaną hello VPN automatycznie ponownie zestawione?

Domyślnie komputer kliencki hello nie przywróci połączenia sieci VPN hello automatycznie.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Lokacji punktu obsługi automatycznie wznowić połączenia i DDNS na hello klientów sieci VPN?

Automatyczne ponowne nawiązywanie połączenia i DDNS nie są obecnie obsługiwane w przypadku połączeń VPN typu punkt-lokacja.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Może mieć lokacja-lokacja i konfiguracje lokacji punktu współdziałały dla hello sama sieć wirtualną?

Tak. Oba te rozwiązania będą działać, o ile zastosowana zostanie brama sieci VPN typu RouteBased. Witaj klasycznego modelu wdrażania należy bramy dynamiczne. Jak nie obsługi punkt-lokacja dla statycznymi bramami routingu w sieci VPN lub bramy przy użyciu hello `-VpnType PolicyBased` polecenia cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Można skonfigurować punkt-lokacja klienta tooconnect toomultiple sieci wirtualnych na powitania jednocześnie?

Tak, jest to możliwe. Ale hello sieci wirtualne nie mają nakładające się prefiksy IP i hello punkt-lokacja przestrzenie adresowe nie mogą się pokrywać między sieciami wirtualnymi hello.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Jakiej przepływności można oczekiwać w przypadku połączeń typu lokacja-lokacja lub punkt-lokacja?

Jest trudne toomaintain hello dokładne przepływności hello tuneli VPN. Protokoły IPsec i SSTP należą do niejawnie ciężkich protokołów sieci VPN. Przepływność również jest ograniczona przez hello opóźnienia i przepustowość między lokalnym a hello Internet.
