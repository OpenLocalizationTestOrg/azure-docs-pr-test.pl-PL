[!INCLUDE [P2S FAQ All](vpn-gateway-faq-p2s-all-include.md)]

### <a name="is-radius-authentication-supported-on-all-azure-vpn-gateway-skus"></a>Czy uwierzytelnianie za pomocą protokołu RADIUS jest obsługiwane na wszystkich jednostkach SKU bramy Azure VPN Gateway?

Uwierzytelnianie za pomocą protokołu RADIUS jest obsługiwane dla jednostek SKU VpnGw1, VpnGw2 i VpnGw3. Jeśli używasz starszych jednostek SKU, uwierzytelnianie za pomocą protokołu RADIUS jest obsługiwane w przypadku standardowych jednostek SKU i jednostek SKU o wysokiej wydajności. Nie jest obsługiwane dla podstawowych jednostek SKU bramy. 
 
### <a name="is-radius-authentication-supported-for-the-classic-deployment-model"></a>Czy uwierzytelnianie za pomocą protokołu RADIUS jest obsługiwane dla klasycznego modelu wdrażania ?
 
Nie. Uwierzytelnianie za pomocą protokołu RADIUS nie jest obsługiwane dla klasycznego modelu wdrażania.
 
### <a name="are-3rd-party-radius-servers-supported"></a>Czy są obsługiwane serwery RADIUS innych firm?

Tak, serwery RADIUS innych firm są obsługiwane.
 
### <a name="what-are-the-connectivity-requirements-to-ensure-that-the-azure-gateway-is-able-to-reach-an-on-premises-radius-server"></a>Jakie wymagania w zakresie łączności należy spełnić, aby mieć pewność, że brama platformy Azure może komunikować się z lokalnym serwerem RADIUS?

Wymagane jest połączenie typu lokacja-lokacja z lokacją lokalną przez sieć VPN. Połączenie to musi mieć właściwie skonfigurowane trasy.  
 
### <a name="can-traffic-to-an-on-premises-radius-server-from-the-azure-vpn-gateway-be-routed-over-an-expressroute-connection"></a>Czy ruch sieciowy do lokalnego serwera RADIUS (z bramy Azure VPN Gateway) może być kierowany przez połączenie usługi ExpressRoute?

Nie. Może być kierowany wyłącznie przez połączenie typu lokacja-lokacja.
 
### <a name="is-there-a-change-in-the-number-of-sstp-connections-supported-with-radius-authentication-what-is-the-maximum-number-of-sstp-and-ikev2-connections-supported"></a>Czy liczba połączeń SSTP obsługiwanych z użyciem uwierzytelniania za pomocą protokołu RADIUS uległa zmianie? Jaka jest maksymalna liczba obsługiwanych połączeń SSTP i IKEv2?

Maksymalna liczba połączeń SSTP obsługiwanych na bramie z uwierzytelnianiem za pomocą protokołu RADIUS nie zmieniła się. Nadal jest to 128. Maksymalna liczba obsługiwanych połączeń to 128, niezależnie od tego, czy brama jest skonfigurowana dla protokołu SSTP, protokołu IKEv2 czy obu z nich.
 
### <a name="what-is-the-difference-between-doing-certificate-authentication-using-a-radius-server-vs-using-azure-native-certificate-authentication-by-uploading-a-trusted-certificate-to-azure"></a>Jaka jest różnica między uwierzytelnianiem certyfikatu przy użyciu serwera RADIUS a natywnym uwierzytelnianiem certyfikatu platformy Azure (przez przekazanie zaufanego certyfikatu na platformę Azure).

W przypadku uwierzytelniania certyfikatu za pomocą protokołu RADIUS żądanie uwierzytelnienia jest przekazywane do serwera RADIUS, który obsługuje faktyczną weryfikację certyfikatu. Ta opcja jest przydatna, gdy chce się przeprowadzić integrację za pośrednictwem protokołu RADIUS z już posiadaną infrastrukturą uwierzytelniania certyfikatów.
  
Gdy do uwierzytelniania certyfikatów używana jest platforma Azure, weryfikację certyfikatu przeprowadza brama Azure VPN Gateway. Swój klucz publiczny certyfikatu trzeba przekazać do bramy. Można również określić listy odwołanych certyfikatów, dla których nie powinno być zgody na nawiązywanie połączenia.

### <a name="does-radius-authentication-work-with-both-ikev2-and-sstp-vpn"></a>Czy uwierzytelnianie za pomocą protokołu RADIUS działa z sieciami VPN z protokołem IKEv2 i SSTP?

Tak, uwierzytelnianie za pomocą protokołu RADIUS jest obsługiwane dla sieci z protokołem IKEv2 i protokołem SSTP.  