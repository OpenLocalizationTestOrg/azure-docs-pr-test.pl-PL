Hello wirtualnymi — często zadawane pytania dotyczą tooVPN połączenia bramy. Jeśli potrzebujesz wirtualnych sieci równorzędnych, zobacz [Wirtualne sieci równorzędne](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Czy w ramach platformy Azure są naliczane opłaty za ruch danych między sieciami wirtualnymi?

Do wirtualnymi ruchu w ramach hello sam region jest bezpłatna dla obu kierunków, gdy połączenie bramy sieci VPN. Krzyżowe wyjście wirtualnymi do regionu ruchu jest obciążana hello ruchu wychodzącego między-sieć wirtualna danych szybkości transferu oparta na powitania źródła regionach. Zobacz toohello [bramy sieci VPN, na stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/vpn-gateway/) szczegółowe informacje. Jeśli łączysz się z sieci wirtualnych za pomocą komunikacji równorzędnej sieci wirtualnej, a nie bramy sieci VPN, zobacz hello [sieci wirtualnej, na stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>Ruch do wirtualnymi przenoszona na powitania Internet?

Nie. Wirtualnymi do ruchu przechodzącego przez hello szkieletu Microsoft Azure, hello Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Czy ruch sieciowy w ramach połączenia między sieciami wirtualnymi jest bezpieczny?

Tak, jest zabezpieczony z użyciem szyfrowania IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>Należy tooconnect urządzenia sieci VPN, sieci wirtualnych jednocześnie?

Nie. Łączenie wielu sieci wirtualnych platformy Azure nie wymaga urządzenia sieci VPN, chyba że jest wymagana łączność między wieloma lokalizacjami.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>Czy Moje sieci wirtualnych muszą toobe w hello tym samym regionie?

Nie. sieci wirtualne Hello może znajdować się w hello tych samych lub różnych regionach platformy Azure (lokalizacja).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Jeśli hello sieci wirtualne nie należą do hello sam subskrypcji, subskrypcje hello muszą toobe skojarzone z dzierżawcą hello tego samego AD?

Nie.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Czy połączenia między sieciami wirtualnymi można używać wraz z połączeniami obejmującymi wiele lokacji?

Tak. Połączenie sieci wirtualnej może być używane równocześnie z sieciami VPN obejmującymi wiele lokacji.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Z iloma lokacjami lokalnymi i sieciami wirtualnymi może połączyć się jedna sieć wirtualna?

Zobacz tabelę [Wymagania dotyczące bramy](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>Można użyć do wirtualnymi tooconnect maszyn wirtualnych lub usług spoza sieci wirtualnej w chmurze?

Nie. Połączenie między sieciami wirtualnymi obsługuje sieci wirtualne. Nie obsługuje połączeń maszyn wirtualnych ani usług w chmurze, które nie należą do sieci wirtualnej.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Czy usługa w chmurze lub punkt końcowy z równoważeniem obciążenia może obejmować sieci wirtualne?

Nie. Usługa w chmurze ani punkt końcowy z równoważeniem obciążenia nie mogą rozciągać się na sieci wirtualne, nawet jeśli są one ze sobą połączone.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Czy można używać typu sieci VPN PolicyBased na potrzeby połączeń między sieciami wirtualnymi lub połączeń obejmujących wiele lokacji?

Nie. Połączenia między sieciami wirtualnymi i połączenia obejmujące wiele lokacji wymagają bram sieci VPN platformy Azure z sieciami typu VPN RouteBased (nazywanymi wcześniej sieciami obsługującymi routing dynamiczny).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>Można podłączyć sieci wirtualnej z tooanother RouteBased sieci VPN typu sieci wirtualnej o typie PolicyBased sieci VPN?

Nie, obie sieci wirtualne MUSZĄ korzystać z sieci VPN opartych na trasach (nazywanych wcześniej sieciami obsługującymi routing dynamiczny).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Czy tunele VPN współdzielą przepustowość?

Tak. Wszystkie tuneli VPN sieć wirtualna hello Udostępnij hello dostępnej przepustowości dla bramy sieci VPN platformy Azure hello i hello tego samego SLA czas działania bramy sieci VPN w systemie Azure.

### <a name="are-redundant-tunnels-supported"></a>Czy nadmiarowe tunele są obsługiwane?

Nadmiarowe tunele między dwiema sieciami wirtualnymi są obsługiwane, jeśli jedna brama sieci wirtualnej jest w konfiguracji aktywne-aktywne.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Czy w konfiguracjach połączeń między sieciami wirtualnymi mogą występować nakładające się przestrzenie adresowe?

Nie. Nakładające się przestrzenie adresowe nie są dopuszczalne.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Czy wśród połączonych sieci wirtualnych i lokacji lokalnych mogą występować nakładające się przestrzenie adresowe?

Nie. Nakładające się przestrzenie adresowe nie są dopuszczalne.



