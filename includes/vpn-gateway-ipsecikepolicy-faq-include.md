### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>Czy niestandardowe zasady protokołu IPsec/IKE są obsługiwane na wszystkich jednostkach SKU bramy sieci VPN platformy Azure?
Niestandardowe zasady protokołu IPsec/IKE są obsługiwane na bramach sieci VPN **VpnGw1, VpnGw2, VpnGw3, Standard** i **HighPerformance** na platformie Azure. **Podstawowa** jednostka SKU nie jest obsługiwana.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Ile zasad można określić dla połączenia?
Można określić tylko ***jedną*** kombinację zasad dla danego połączenia.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Czy można określić dla połączenia zasady częściowe (np. tylko algorytmy IKE, ale nie IPsec)?
Nie, należy określić wszystkie algorytmy i parametry zarówno dla protokołu IKE (tryb główny), jak i protokołu IPsec (tryb szybki). Określenie zasad częściowych nie jest dozwolone.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Co to są algorytmy hello i klucza sile obsługiwane w zasadach niestandardowych hello?
Witaj w poniższej tabeli wymieniono hello obsługiwanych algorytmów kryptograficznych i kluczy sile można konfigurować i klientom Witaj. Należy wybrać jedną opcję dla każdego pola.

| **IPsec/IKEv2**  | **Opcje**                                                                   |
| ---              | ---                                                                           |
| Szyfrowanie IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Integralność IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Grupa DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, Brak |
| Szyfrowanie IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Brak      |
| Integralność IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Grupa PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Brak                              |
| Okres istnienia skojarzeń zabezpieczeń QM   | Sekundy (liczba całkowita; **min. 300**/wartość domyślna 27 000 sekund)<br>KB (liczba całkowita; **min. 1024**/wartość domyślna to 102 400 000 KB)           |
| Selektor ruchu | UsePolicyBasedTrafficSelectors ($True/$False; wartość domyślna $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 są hello takie same jak grupa Diffie-Hellman **14** IKE i PFS protokołu IPsec. Zobacz [grupy Diffie-Hellmana](#DH) dla hello wykonaj mapowania.
> 2. Algorytmy GCMAES, należy określić hello samą długość GCMAES algorytm i klucz do szyfrowania IPsec i integralności.
> 3. Okres istnienia skojarzenia zabezpieczeń trybu głównego protokół IKEv2 jest ustalony na 28 800 sekund na powitania bram sieci VPN platformy Azure
> 4. Okresy istnienia skojarzeń zabezpieczeń QM to parametry opcjonalne. Jeśli żaden nie został określony, są używane wartości domyślne 27 000 sekund (7,5 godz.) i 102 400 000 KB (102 GB).
> 5. UsePolicyBasedTrafficSelector jest parametrem opcja hello połączenia. Zobacz często Zadawanych hello elementu "UsePolicyBasedTrafficSelectors"

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Czy wszystko wymaga toomatch między hello zasad bramy sieci VPN platformy Azure i konfiguracji urządzeń moje lokalnej sieci VPN?
Muszą być zgodne i zawierają następujące algorytmy hello konfiguracji urządzenia sieci VPN między lokalnymi i parametrów, które określają na hello Azure IPsec/IKE zasad:

* Algorytm szyfrowania IKE
* Algorytm integralności IKE
* Grupa DH
* Algorytm szyfrowania IPsec
* Algorytm integralności IPsec
* Grupa PFS
* Selektor ruchu (*)

okresy istnienia Hello skojarzenia zabezpieczeń są tylko lokalne specyfikacje, nie trzeba toomatch.

Po włączeniu **UsePolicyBasedTrafficSelectors**, należy tooensure hello dopasowania selektorów ruchu zdefiniowane z wszystkich kombinacji prefiksów (bramy sieci lokalnej) sieci lokalnej, tak z hello ma urządzenie sieci VPN Prefiksy sieci wirtualnej platformy Azure, zamiast dowolny z każdym. Na przykład jeśli są Twoje prefiksy sieci lokalnej, 10.1.0.0/16 i 10.2.0.0/16, a prefiksy Twojej sieci wirtualnej są 192.168.0.0/16 i 172.16.0.0/16, należy hello toospecify po selektorów ruchu:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Odwołuje się zbyt[połączyć wiele urządzeń lokalnych, na podstawie zasad sieci VPN](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) Aby uzyskać więcej informacji na temat toouse tej opcji.

### <a name ="DH"></a>Które grupy Diffie'ego-Hellmana są obsługiwane?
w poniższej tabeli Hello Wyświetla listę grup Diffie-Hellman hello obsługiwane IKE (DHGroup) i IPsec (PFSGroup):

| **Grupa Diffie’ego-Hellmana**  | **DHGroup**              | **PFSGroup** | **Długość klucza** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP, 768-bitowy   |
| 2                         | DHGroup2                 | PFS2         | MODP, 1024-bitowy  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP, 2048-bitowy  |
| 19                        | ECP256                   | ECP256       | ECP, 256-bitowy    |
| 20                        | ECP384                   | ECP284       | ECP, 384-bitowy    |
| 24                        | DHGroup24                | PFS24        | MODP, 2048-bitowy  |
|                           |                          |              |                |

Odwołuje się zbyt[RFC3526](https://tools.ietf.org/html/rfc3526) i [RFC5114](https://tools.ietf.org/html/rfc5114) więcej szczegółów.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Zasady niestandardowe hello zastępuje zestawów zasad IPsec i IKE hello domyślny dla bram sieci VPN platformy Azure?
Tak, po niestandardowych zasad jest określony dla połączenia, bramy sieci VPN platformy Azure będzie używana tylko zasady hello na powitania połączenia, zarówno jako IKE Inicjator i obiekt odpowiadający IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Usunięcie niestandardowych zasad IPsec i IKE, połączenie hello staje się niechronione?
Nie, połączenie hello nadal będą chronione za pomocą protokołu IPsec/IKE. Po usunięciu zasad niestandardowych hello połączenie bramy sieci VPN platformy Azure hello spowoduje przywrócenie wstecz toohello [domyślnej listy propozycje IPsec i IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) i ponownie uruchom hello uzgadnianie IKE ponownie, używając lokalnego urządzenia sieci VPN.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Czy dodanie lub aktualizacja zasad protokołu IPsec/IKE zakłóci moje połączenie sieci VPN?
Tak, może spowodować zakłócenia małe (kilka sekund), jak bramy sieci VPN platformy Azure hello spowoduje zerwanie hello istniejące połączenie i ponownie uruchom hello toore uzgadniania IKE-ustanowienie tunelu IPsec hello hello nowych algorytmów kryptograficznych i parametry. Upewnij się, że lokalnego urządzenia sieci VPN jest również konfigurowany za hello zgodnych algorytmów i zakłóceń hello toominimize sile klucza.

### <a name="can-i-use-different-policies-on-different-connections"></a>Czy można użyć różnych zasad dla różnych połączeń?
Tak. Dla poszczególnych połączeń są stosowane zasady niestandardowe. Można utworzyć i zastosować różne zasady protokołu IPsec/IKE dla różnych połączeń. Możesz również tooapply zasad niestandardowych w podzestawie połączenia. Hello tych pozostałych użyje hello Azure domyślne IPsec i IKE zasad zestawy.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Czy za pomocą zasad niestandardowych hello także połączenia między wirtualnymi do?
Tak, można stosować zasady niestandardowe zarówno dla połączeń obejmujących wiele lokalizacji protokołu IPsec, jak i połączeń między sieciami wirtualnymi.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Należy toospecify hello te same zasady na oba zasoby połączenia do wirtualnymi?
Tak. Tunel połączenia między sieciami wirtualnymi zawiera dwa zasoby połączenia na platformie Azure, po jednym dla każdego kierunku. Należy tooensure oba zasoby połączenia mają hello jednych zasad hello othereise połączenia do wirtualnymi nie zostanie nawiązane.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>Czy niestandardowe zasady protokołu IPsec/IKE działają dla połączenia ExpressRoute?
Nie. Zasady protokołu IPsec/IKE działa tylko na połączenia VPN S2S i wirtualnymi do połączeń za pośrednictwem bramy sieci VPN platformy Azure hello.
