### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>Czy niestandardowe zasady protokołu IPsec/IKE są obsługiwane na wszystkich jednostkach SKU bramy sieci VPN platformy Azure?
Niestandardowe zasady protokołu IPsec/IKE są obsługiwane na bramach sieci VPN **VpnGw1, VpnGw2, VpnGw3, Standard** i **HighPerformance** na platformie Azure. **Podstawowa** jednostka SKU **nie** jest obsługiwana.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Ile zasad można określić dla połączenia?
Można określić tylko ***jedną*** kombinację zasad dla danego połączenia.

### <a name="can-i-specify-a-partial-policy-on-a-connection-for-example-only-ike-algorithms-but-not-ipsec"></a>Czy można określić dla połączenia zasady częściowe (np. tylko algorytmy IKE, ale nie IPsec)
Nie, należy określić wszystkie algorytmy i parametry zarówno dla protokołu IKE (tryb główny), jak i protokołu IPsec (tryb szybki). Określenie zasad częściowych nie jest dozwolone.

### <a name="what-are-the-algorithms-and-key-strengths-supported-in-the-custom-policy"></a>Jakie algorytmy i siły klucza są obsługiwane w zasadach niestandardowych?
W poniższej tabeli wymieniono obsługiwane algorytmy kryptograficzne i siły klucza konfigurowalne przez klientów. Należy wybrać jedną opcję dla każdego pola.

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
> 1. DHGroup2048 i PFS2048 są takie same jak grupa Diffie’ego-Hellmana**14** w funkcji PFS protokołów IKE i IPsec. Pełną listę mapowań można znaleźć w sekcji dotyczącej [grup Diffie’ego-Hellmana](#DH).
> 2. W przypadku algorytmów GCMAES należy określić ten sam algorytm GCMAES i długość klucza na potrzeby integralności i szyfrowania IPsec.
> 3. Okres istnienia skojarzenia zabezpieczeń trybu głównego protokołu IKEv2 jest ustalony na 28 800 sekund na bramach sieci VPN platformy Azure
> 4. Okresy istnienia skojarzeń zabezpieczeń QM to parametry opcjonalne. Jeśli żaden nie został określony, są używane wartości domyślne 27 000 sekund (7,5 godz.) i 102400000 KB (102 GB).
> 5. UsePolicyBasedTrafficSelector to parametr opcji połączenia. Zobacz kolejny element często zadawanych pytań dla elementu „UsePolicyBasedTrafficSelectors”

### <a name="does-everything-need-to-match-between-the-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Czy konfiguracja zasad bramy sieci VPN platformy Azure musi być w pełni zgodna z konfiguracją lokalnego urządzenia sieci VPN?
Konfiguracja lokalnego urządzenia sieci VPN musi być zgodna z następującymi algorytmami (lub je zawierać) oraz z następującymi parametrami określonymi w zasadach protokołu IPsec/IKE platformy Azure (lub je zawierać):

* Algorytm szyfrowania IKE
* Algorytm integralności IKE
* Grupa DH
* Algorytm szyfrowania IPsec
* Algorytm integralności IPsec
* Grupa PFS
* Selektor ruchu (*)

Okresy istnienia skojarzenia zabezpieczeń są tylko specyfikacjami lokalnymi i nie muszą być zgodne.

Po włączeniu **UsePolicyBasedTrafficSelectors** należy się upewnić, że urządzenie sieci VPN ma pasujące selektory ruchu zdefiniowane przy użyciu wszystkich kombinacji prefiksów sieci lokalnej (bramy sieci lokalnej) do/z prefiksów sieci wirtualnej platformy Azure, a nie sieci typu dowolna-dowolna. Na przykład jeśli prefiksy sieci lokalnej to 10.1.0.0/16 i 10.2.0.0/16, a prefiksy sieci wirtualnej to 192.168.0.0/16 i 172.16.0.0/16, trzeba określić następujące selektory ruchu:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Aby uzyskać więcej informacji, zobacz [Connect multiple on-premises policy-based VPN devices (Łączenie wielu lokalnych urządzeń sieci VPN opartych na zasadach)](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md).

### <a name ="DH"></a>Które grupy Diffie'ego-Hellmana są obsługiwane?
W poniższej tabeli przedstawiono listę obsługiwanych grup Diffie'ego-Hellmana dla protokołów IKE (DHGroup) i IPsec (PFSGroup):

| **Grupa Diffie’ego-Hellmana**  | **DHGroup**              | **PFSGroup** | **Długość klucza** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP, 768-bitowy   |
| 2                         | DHGroup2                 | PFS2         | MODP, 1024-bitowy  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP, 2048-bitowy  |
| 19                        | ECP256                   | ECP256       | ECP, 256-bitowy    |
| 20                        | ECP384                   | ECP284       | ECP, 384-bitowy    |
| 24                        | DHGroup24                | PFS24        | MODP, 2048-bitowy  |
|                           |                          |              |                |

Aby uzyskać więcej informacji, zobacz [RFC3526](https://tools.ietf.org/html/rfc3526) i [RFC5114](https://tools.ietf.org/html/rfc5114).

### <a name="does-the-custom-policy-replace-the-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Czy zasady niestandardowe zastępują domyślne zestawy zasad protokołu IPsec/IKE dla bram sieci VPN platformy Azure?
Tak, po określeniu zasad niestandardowych dla połączenia brama sieci VPN platformy Azure będzie korzystać tylko z zasad połączenia — zarówno jako inicjator IKE, jak i obiekt odpowiadający IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-the-connection-become-unprotected"></a>Czy jeśli usunę niestandardowe zasady protokołu IPsec/IKE, połączenie stanie się niechronione?
Nie, połączenie będzie nadal chronione przez protokół IPsec/IKE. Po usunięciu zasad niestandardowych z połączenia brama Azure VPN Gateway jest przywracana do [domyślnej listy propozycji protokołu IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) i jest ponownie uruchomiane uzgadnianie IKE za pomocą lokalnego urządzenia sieci VPN.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Czy dodanie lub aktualizacja zasad protokołu IPsec/IKE zakłóci moje połączenie sieci VPN?
Tak, może to spowodować niewielkie zakłócenie (trwające kilka sekund), ponieważ brama Azure VPN Gateway usuwa istniejące połączenie i uruchamia ponownie uzgadnianie IKE, aby ponownie ustanowić tunel IPsec za pomocą nowych algorytmów kryptograficznych i parametrów. Pamiętaj, aby również skonfigurować swoje lokalne urządzenie sieci VPN za pomocą pasujących algorytmów i sił klucza, aby zminimalizować zakłócenie.

### <a name="can-i-use-different-policies-on-different-connections"></a>Czy można użyć różnych zasad dla różnych połączeń?
Tak. Dla poszczególnych połączeń są stosowane zasady niestandardowe. Można utworzyć i zastosować różne zasady protokołu IPsec/IKE dla różnych połączeń. Można również zastosować zasady niestandardowe dla podzestawu połączeń. Pozostałe połączenia korzystają z domyślnych zestawów zasad protokołu IPsec/IKE platformy Azure.

### <a name="can-i-use-the-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Czy można używać zasad niestandardowych również dla połączenia między sieciami wirtualnymi?
Tak, można stosować zasady niestandardowe zarówno dla połączeń obejmujących wiele lokalizacji protokołu IPsec, jak i połączeń między sieciami wirtualnymi.

### <a name="do-i-need-to-specify-the-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Czy trzeba określić te same zasady dla obu zasobów połączenia między sieciami wirtualnymi?
Tak. Tunel połączenia między sieciami wirtualnymi zawiera dwa zasoby połączenia na platformie Azure, po jednym dla każdego kierunku. Upewnij się, że oba zasoby połączenia mają te same zasady. W przeciwnym razie połączenie między sieciami wirtualnymi nie zostanie ustanowione.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>Czy niestandardowe zasady protokołu IPsec/IKE działają dla połączenia ExpressRoute?
Nie. Zasady protokołu IPsec/IKE działają tylko dla połączeń sieci VPN S2S i połączeń między sieciami wirtualnymi za pośrednictwem bram sieci VPN platformy Azure.