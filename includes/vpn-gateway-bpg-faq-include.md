### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>Czy protokół BGP jest obsługiwany na wszystkich jednostkach SKU bramy sieci VPN platformy Azure?
Nie, protokół BGP jest obsługiwany przez **standardową** i **wysokowydajną** bramę sieci VPN. **Podstawowa** jednostka SKU nie jest obsługiwana.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Czy można użyć protokołu BGP z bramą sieci VPN platformy Azure opartej na zasadach?
Nie, protokół BGP jest obsługiwany tylko przez bramy sieci VPN opartych na trasach.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Czy można użyć prywatnych numerów ASN (numery systemu autonomicznego)?
Tak, można użyć własnych publicznych lub prywatnych numerów ASN dla sieci lokalnych i sieci wirtualnych platformy Azure.

### <a name="are-there-asns-reserved-by-azure"></a>Czy istnieją numery ASN zarezerwowane przez platformę Azure?
Tak, hello następujące numery ASN są zastrzeżone przez platformę Azure dla komunikacji równorzędnych zarówno wewnętrznych i zewnętrznych:

* Publiczne numery ASN: 8075, 8076, 12076
* Prywatne numery ASN: 65515, 65517, 65518, 65519, 65520

Nie można określić tych numerów ASN dla w lokalnej urządzenia sieci VPN, łącząc tooAzure bramy sieci VPN.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Czy istnieją inne numery ASN, których nie mogę używać?
Tak, są następujące numerów ASN hello [zarezerwowane przez organizację IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) i nie można skonfigurować dla bramy sieci VPN platformy Azure:

23456, 64496-64511, 65535–65551 i 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>Witaj można użyć tego samego numeru ASN zarówno dla lokalnych sieci VPN i sieci wirtualnych platformy Azure?
Nie, należy przypisać różne numery ASN sieciom lokalnym i sieciom wirtualnym platformy Azure, jeśli są łączone za pomocą protokołu BGP. Bramy sieci VPN platformy Azure mają przypisany domyślny numer ASN 65515, niezależnie od tego, czy protokół BGP jest włączony dla łączności między różnymi lokalizacjami firmy. Można zastąpić to ustawienie domyślne, przypisując inny numer ASN podczas tworzenia bramy sieci VPN hello, lub zmień hello numeru ASN po utworzeniu bramy hello. Konieczne będzie tooassign Twojego toohello numerów ASN lokalnymi odpowiadającego bramy sieci lokalnej platformy Azure.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>Jakiego adresu prefiksy będzie toome anonsowanie bram sieci VPN platformy Azure?
Brama sieci VPN będzie anonsować hello następujące trasy tooyour lokalnymi BGP urządzeń:

* Prefiksy adresów sieci wirtualnej użytkownika
* Prefiksy adresów dla każdej bramy sieci VPN platformy Azure toohello połączenia bramy sieci lokalnej
* Trasy zostały uzyskane z innych BGP komunikacji równorzędnej sesji toohello połączenia sieci VPN platformy Azure bramy, **z wyjątkiem domyślne trasy lub tras nakładających się dowolnego prefiksu sieci wirtualnej**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Czy może anonsować bramy sieci VPN tooAzure (0.0.0.0/0) trasy domyślnej?
Tak.

Należy pamiętać, to zostanie wymuszone cały ruch wychodzący sieci wirtualnej do lokacji lokalnej i uniemożliwi maszyny wirtualne sieci wirtualnej hello akceptowanie komunikacji publicznej z hello Internet bezpośrednio, takie połączenie RDP lub SSH z hello Internet toohello maszyn wirtualnych.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>Prefiksy dokładne hello może być anonsować jako Mój prefiksy sieci wirtualnej?

Nie, hello reklamy prefiksy takie same jak Twoje prefiksy adresów sieci wirtualnej zostanie zablokowane lub filtrowane według hello platformy Azure. Można jednak anonsować prefiks, który jest podzbiorem tego, co znajduje się wewnątrz sieci wirtualnej. 

Na przykład jeśli sieci wirtualne używane 10.0.0.0/16 przestrzeni adresowej hello, można ogłosić 10.0.0.0/8. Nie można jednak anonsować przestrzeni 10.0.0.0/16 ani 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>Czy można użyć protokołu BGP do połączeń między sieciami wirtualnymi użytkownika?
Tak, protokołu BGP można użyć do połączeń zarówno między różnymi lokalizacjami, jak i połączeń między sieciami wirtualnymi.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Czy można mieszać połączenia BGP z połączeniami protokołów innych niż BGP dla bram sieci VPN użytkownika platformy Azure?
Tak, można mieszać zarówno protokołu BGP i połączenia z systemem innym niż BGP dla hello tej samej bramy sieci VPN platformy Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Czy brama sieci VPN platformy Azure obsługuje routing tranzytowy protokołu BGP?
Tak, routing tranzytowy protokołu BGP jest obsługiwany, z wyjątkiem hello, który będzie bram sieci VPN platformy Azure **nie** anonsowanie elementów równorzędnych BGP tooother trasy domyślnej. przesyłania tooenable routing przez wielu bram sieci VPN platformy Azure, należy włączyć protokół BGP dla wszystkich pośrednich połączeń sieci wirtualnej do sieci wirtualnej.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Czy można mieć więcej niż jeden tunel między bramą sieci VPN platformy Azure i lokalną siecią użytkownika?
Tak, można utworzyć więcej niż jeden tunel VPN S2S między bramą sieci VPN platformy Azure i siecią lokalną. Należy pamiętać, że wszystkie te tunele będą uwzględniane hello łącznej liczbie tuneli dla bram sieci VPN platformy Azure, sieci i należy włączyć protokół BGP dla obu tuneli.

Na przykład jeśli dwa nadmiarowe tunele między bramy sieci VPN platformy Azure i jedną z sieci lokalnej, będą wymagały 2 tuneli spoza łącznego limitu przydziału hello bramy sieci VPN platformy Azure (10 dla standardowej) i 30 dla wysokowydajnej.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>Czy można mieć wiele tuneli między dwiema sieciami wirtualnymi platformy Azure z protokołem BGP?
Tak, ale co najmniej jedną z bram sieci wirtualnej hello musi być w konfiguracji aktywny aktywny.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>Czy można użyć protokołu BGP dla sieci VPN S2S w konfiguracji współistnienia sieci ExpressRoute i sieci VPN S2S?
Tak. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Jakiego adresu używa brama sieci VPN platformy Azure dla adresu IP elementu równorzędnego protokołu BGP?
Brama sieci VPN platformy Azure Hello przyzna pojedynczego adresu IP z zakresu podsieci bramy zdefiniowanego dla sieci wirtualnej hello hello. Domyślnie jest hello przedostatni adres zakresu hello. Na przykład, jeśli jest 10.12.255.0/27, począwszy od 10.12.255.0 too10.12.255.31, hello adres IP elementu równorzędnego protokołu BGP na powitania bramy sieci VPN platformy Azure będzie 10.12.255.30. Te informacje można znaleźć wśród informacji dotyczących bramy sieci VPN platformy Azure hello.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Jakie są wymagania hello hello adresów IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN?
Adresu elementu równorzędnego protokołu BGP lokalnymi **nie może** można hello takie same jak hello publiczny adres IP urządzenia sieci VPN. Użyj innego adresu IP urządzenia sieci VPN powitania dla Twojego adresu IP elementu równorzędnego protokołu BGP. Może być adres przypisany toohello interfejsu sprzężenia zwrotnego na urządzeniu hello. Ten adres należy określić w hello odpowiedniego bramy sieci lokalnej reprezentująca hello lokalizacji.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>Co należy określić jako prefiksy adresów użytkownika dla bramy sieci lokalnej hello podczas korzystania z protokołu BGP?
Bramy sieci lokalnej platformy Azure określa hello początkowe prefiksy adresów dla sieci lokalne powitania. Z obsługą protokołu BGP, należy przydzielić prefiks hosta hello (prefiks / 32) adresu IP elementu równorzędnego protokołu BGP jako przestrzeń adresowa powitania dla tej sieci lokalnej. Jeśli IP elementu równorzędnego protokołu BGP jest 10.52.255.254, należy określić "10.52.255.254/32" jako przestrzeń adresów hello hello bramy sieci lokalnej reprezentującej tę sieć lokalną. Jest to tooensure, który hello sieci VPN platformy Azure hello sesję protokołu BGP przez tunel S2S VPN hello ustanawia bramy.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>Co należy dodać toomy lokalnego urządzenia sieci VPN dla sesji komunikacji równorzędnej BGP hello?
Na urządzeniu sieci VPN, wskazując toohello tunel VPN S2S protokołu IPsec, należy dodać trasę hosta dla hello adres IP elementu równorzędnego protokołu BGP platformy Azure. Na przykład hello IP elementu równorzędnego sieci VPN platformy Azure jest "10.12.255.30", należy dodać trasę hosta dla adresu "10.12.255.30" z interfejsem następnego skoku hello pasującego interfejsu tunelu protokołu IPsec na urządzeniu sieci VPN.

