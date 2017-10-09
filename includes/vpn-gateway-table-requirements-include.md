Witaj następującej tabeli list hello wymagania dla bram PolicyBased i RouteBased sieci VPN. Ta tabela odnosi się hello tooboth Resource Manager i klasycznych modeli wdrażania. Hello modelu klasycznego bramy sieci VPN PolicyBased są takie same hello jak bramy statyczne, a bramy oparte na trasach są takie same hello jak bramy dynamiczne.

|  | **PolicyBased Basic bramy sieci VPN** | **RouteBased Basic bramy sieci VPN** | **RouteBased Standard bramy sieci VPN** | **Brama sieci VPN RouteBased wysokiej wydajności** |
| --- | --- | --- | --- | --- |
| **Połączenie lokacja-lokacja (S2S)** |Konfiguracja sieci VPN PolicyBased |Konfiguracja sieci VPN z siecią typu RouteBased |Konfiguracja sieci VPN z siecią typu RouteBased |Konfiguracja sieci VPN z siecią typu RouteBased |
| **Łączność typu „punkt do lokacji” (Point-to-Site, P2S**) |Nieobsługiwane |Obsługiwane (może współistnieć z S2S) |Obsługiwane (może współistnieć z S2S) |Obsługiwane (może współistnieć z S2S) |
| **Metoda uwierzytelniania** |Klucz wstępny |Klucz wstępny dla połączeń S2S, certyfikaty dla łączności P2S |Klucz wstępny dla połączeń S2S, certyfikaty dla łączności P2S |Klucz wstępny dla połączeń S2S, certyfikaty dla łączności P2S |
| **Maksymalna liczba połączeń S2S** |1 |10 |10 |30 |
| **Maksymalna liczba połączeń P2S** |Nieobsługiwane |128 |128 |128 |
| **Aktywna Obsługa routingu (BGP)** |Nieobsługiwane |Nieobsługiwane |Obsługiwane |Obsługiwane |

