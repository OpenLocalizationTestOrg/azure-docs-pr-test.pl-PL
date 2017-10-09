## <a name="load-balancer-differences"></a>Różnice między modułami równoważenia obciążenia

Istnieją różne opcje ruchu sieciowego dla toodistribute przy użyciu programu Microsoft Azure. Działanie tych opcji różni się między sobą, a same opcje wykorzystują różny zbiór funkcji i obsługują różne scenariusze. Można korzystać z nich osobno lub używać ich łącznie.

* **Moduł równoważenia obciążenia Azure** działa w warstwie transportu hello (warstwy 4 w stosie odwołanie sieci OSI hello). Zapewnia poziom sieci Dystrybucja ruchu między wystąpieniami aplikacji uruchomionej w hello tym samym centrum danych Azure.
* **Brama aplikacji w** działa w warstwie aplikacji hello (warstwy 7 w stosie odwołanie sieci OSI hello). Działa ona jako usługi serwera proxy wstecznego, przerywa połączenie klienta hello i przekazywania żądań punkty końcowe tooback-end.
* **Menedżer ruchu** działa na powitania poziom DNS.  Używa odpowiedzi DNS toodirect ruchu przez użytkownika końcowego tooglobally rozproszonych punktów końcowych. Następnie łączyć klienci punkty końcowe toothose bezpośrednio.

Witaj w poniższej tabeli przedstawiono funkcje hello oferowane przez poszczególnych usług:

| Usługa | Azure Load Balancer | Application Gateway | Traffic Manager |
| --- | --- | --- | --- |
| Technologia |Poziom transportu (warstwa 4) |Poziom aplikacji (warstwa 7) |Poziom DNS |
| Obsługiwane protokoły aplikacji |Dowolne |Protokoły HTTP, HTTPS i WebSockets |Dowolne (do monitorowania punktu końcowego jest wymagany punkt końcowy HTTP) |
| Punkty końcowe |Wystąpienia roli maszyn wirtualnych i usług w chmurze Azure |Dowolny wewnętrzny adres IP platformy Azure, publiczny adres IP, maszyna wirtualna platformy Azure lub usługa w chmurze platformy Azure |Azure Virtual Machines, Cloud Services, Azure Web Apps i zewnętrzne punkty końcowe |
| Obsługa sieci wirtualnej |Możliwe użycie zarówno z aplikacjami połączonymi z Internetem, jak i aplikacjami wewnętrznymi (w sieci wirtualnej) |Możliwe użycie zarówno z aplikacjami połączonymi z Internetem, jak i aplikacjami wewnętrznymi (w sieci wirtualnej) |Obsługuje tylko aplikacje łączące się z Internetem |
| Monitorowanie punktu końcowego |Obsługiwane z użyciem sond |Obsługiwane z użyciem sond |Obsługiwane z użyciem żądania GET protokołu HTTP/HTTPS |

Azure usługi równoważenia obciążenia i tooendpoints ruchu sieciowego trasy bramy aplikacji, ale te mają użycia różnych scenariuszy toowhich ruchu toohandle. Hello poniższej tabeli ułatwiają zrozumienie hello różnica między usługi równoważenia obciążenia dwóch hello:

| Typ | Azure Load Balancer | Application Gateway |
| --- | --- | --- |
| Protokoły |UDP/TCP |Protokoły HTTP, HTTPS i WebSockets |
| Rezerwacja adresu IP |Obsługiwane |Nieobsługiwane |
| Tryb równoważenia obciążenia |5-krotka (źródłowy adres IP, port źródłowy, docelowy adres IP, port docelowy, typ protokołu) |Działanie okrężne<br>Routing na podstawie adresu URL |
| Tryb równoważenia obciążenia (źródłowy adres IP / sesje umocowane) |2-krotka (źródłowy adres IP i docelowy adres IP), 3-krotka (źródłowy adres IP, docelowy adres IP i port). Można skalować w górę lub w dół na podstawie hello liczby maszyn wirtualnych |Koligacja na podstawie pliku cookie<br>Routing na podstawie adresu URL |
| Sondy kondycji |Wartość domyślna: interwał sondowania — 15 sekund. Wykluczenie z rotacji: dwa powtarzające się niepowodzenia. Obsługa sond zdefiniowanych przez użytkownika |Interwał bezczynności sondy — 30 sekund. Usunięta po pięciu kolejnych niepowodzeniach obsługi ruchu lub po pojedynczym niepowodzeniu sondy w trybie bezczynności. Obsługa sond zdefiniowanych przez użytkownika |
| Odciążanie protokołu SSL |Nieobsługiwane |Obsługiwane |
| Routing oparty na adresach URL | Nieobsługiwane | Obsługiwane|
| Zasady SSL | Nieobsługiwane | Obsługiwane|
