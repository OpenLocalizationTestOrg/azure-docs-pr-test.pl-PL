---
title: "aaaDMZ przykład — tworzenie DMZ tooprotect aplikacji z zaporą i grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z zaporą i grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Przykład 2 — Tworzenie DMZ tooprotect aplikacji z zaporą i grupy NSG
[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]

W tym przykładzie utworzy strefą DMZ z zaporą, windows czterech serwerów i grup zabezpieczeń sieci. On również przeprowadzi każdego tooprovide odpowiednich poleceń hello głębsze zrozumienie każdego kroku. Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ. Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy. 

![Przychodzący DMZ NVA i grupy NSG][1]

## <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie jest subskrypcji, która zawiera następujące hello:

* Dwie usługi w chmurze: "FrontEnd001" i "BackEnd001"
* Sieć wirtualna "CorpNetwork", z dwoma podsieciami: "FrontEnd" i "Wewnętrzna"
* Jednej grupy zabezpieczeń sieci jest stosowane tooboth podsieci
* Urządzenie wirtualne sieci, w tym przykładzie zapora NextGen Barracuda, podłączone podsieci frontonu toohello
* Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwa okna serwerów, które reprezentują aplikacji z powrotem kończyć serwery ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")

> [!NOTE]
> Mimo że w tym przykładzie użyto zapory NextGen Barracuda, wiele hello różnych urządzeń wirtualnych sieci może być używane w tym przykładzie.
> 
> 

W sekcji odwołań hello poniżej jest skrypt programu PowerShell, który zostanie skompilowany większość środowiska hello opisane powyżej. Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie.

toobuild hello środowiska:

1. Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)
2. Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi itp.)
3. Uruchom skrypt hello w programie PowerShell

**Uwaga**: region hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.

Po pomyślnym uruchomieniu skryptu hello można podjąć następujące kroki po skryptu hello:

1. Konfigurowanie reguł zapory hello, to jest objęte hello sekcji poniżej: reguł zapory.
2. Opcjonalnie w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.

Hello następnej sekcji opisano większość hello skrypty instrukcje względną tooNetwork grup zabezpieczeń.

## <a name="network-security-groups-nsg"></a>Sieciowe grupy zabezpieczeń (NSG)
Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł. 

> [!TIP]
> Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny". Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze. Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane. Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).
> 
> 

Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:

1. Wewnętrzny ruch DNS (port 53) jest dozwolony
2. Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny Wirtualnej jest dozwolony
3. Ruch HTTP (port 80) z hello Internet toohello NVA (zapory) jest dozwolony
4. Cały ruch (wszystkie porty) z IIS01 tooAppVM1 jest dozwolona
5. Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (obie podsieci)
6. Cały ruch (wszystkie porty) z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello jest zabroniony

Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry. W związku z tym żądaniu hello HTTP będzie dozwolone toohello zapory. Jeśli ten sam ruch próbował tooreach hello DNS01 serwer, reguła 5 (odmowa) mogą być hello pierwszy tooapply hello ruch w sieci i nie będzie dozwolone toopass toohello serwera. Reguły 6 (Odmów) bloki hello frontonu podsieci z mówić toohello podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), chroni sieć zaplecze hello, w przypadku, gdy osoba atakująca dokonywania hello aplikacji sieci web na powitania serwera sieci Web, hello musi ograniczony dostęp toohello wewnętrznej bazy danych "protected" sieci (tylko tooresources udostępniane na serwerze AppVM01 hello).

Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet. Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących. toolock dół ruchu w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagana, jest to przedstawione w przykładzie różnych, który można znaleźć w hello [dokumentu granic zabezpieczeń głównego][HOME].

reguły NSG powyżej Hello omówione są bardzo podobne reguły NSG toohello w [przykład 1 — Tworzenie prostego DMZ z grup NSG][Example1]. Zapoznaj się z tematem hello NSG opis w tym dokumencie, aby uzyskać szczegółowy widok każdej reguły NSG i jego atrybuty.

## <a name="firewall-rules"></a>Reguły zapory
Klienta zarządzania należy toobe zainstalowany w zaporze hello toomanage komputera, a następnie utwórz wymagane konfiguracje hello. Zobacz hello dostawcy dokumentacji zapory (lub inne NVA) w sposób toomanage hello urządzenia. Hello pozostałej części tej sekcji opisano konfigurację hello hello zapory, za pośrednictwem powitania klienta zarządzania dostawców (tj. hello portalu Azure lub programu PowerShell).

Instrukcje dotyczące pobierania klienta i łączenia toohello Barracuda używana w tym przykładzie można znaleźć tutaj: [Barracuda NG administratora](https://techlib.barracuda.com/NG61/NGAdmin)

W zaporze hello przekazywania zasady należy toobe utworzony. Ponieważ w tym przykładzie tylko trasy toohello przychodzącego ruchu zaporę, a następnie toohello serwera sieci web, przekazywanie tylko jedną regułę NAT jest wymagane. Na powitania zapory NextGen Barracuda używane w tym hello przykład reguły byłoby NAT docelowy reguły toopass ("NAT czasu letniego") tego ruchu.

toocreate hello następujących reguł (lub sprawdź istniejących reguł domyślnych), zaczynając od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello w hello konfigurację operacyjną sekcji kliknij pozycję zestaw reguł. Wywołuje siatkę, "Main reguły" wyświetli hello istniejących active i zdezaktywowane reguły zapory hello. W hello prawego górnego rogu tej siatki jest mały, zielony "+", kliknij ten toocreate nową regułę (Uwaga: Zapora może być "zablokowana" zmian, jeśli przycisk oznaczony jako "Lock" i są toocreate lub Edytuj reguły, kliknij ten przycisk zbyt "odblokować" hello zestaw reguł i Zezwól na edytowanie). Jeśli chcesz, aby tooedit istniejącą regułę, wybierz tej reguły, kliknij prawym przyciskiem myszy i wybierz edytowanie reguły.

Utwórz nową regułę i podaj nazwę, na przykład "WebTraffic". 

Ikona reguł NAT docelowego Hello wygląda następująco: ![docelowym translacji adresów Sieciowych ikony][2]

Reguła Hello, sam będzie wyglądać mniej więcej tak:

![Reguły zapory][3]

W tym miejscu dowolnego adresu dla ruchu przychodzącego, że trafień hello zapory w trakcie tooreach HTTP (port 80 i 443 dla protokołu HTTPS) będą wysyłane hello interfejsu "DHCP1 lokalny adres IP" i przekierowanego toohello serwera sieci Web z hello 10.0.1.5 adres IP zapory. Ponieważ przychodzącym hello ruch na porcie 80 i serwer sieci web toohello będzie na porcie 80 zostało niezbędne nie zmiany portu. Jednak powitalne listy docelowej mogło być 10.0.1.5:8080 jeśli nasłuch serwera sieci Web na porcie 8080 w związku z tym tłumaczenia hello przychodzący port 80 hello zapory tooinbound portu 8080 na powitania serwera sieci web.

Metodę połączenia powinien również być oznaczony, dla hello docelowy reguły z hello Internet, "Dynamiczne SNAT" jest najbardziej odpowiednia. 

Mimo że tylko jedna reguła została utworzona ważne jest jej priorytet została poprawnie ustawiona. Jeśli w siatce hello wszystkich reguł zapory hello nowe znajdzie się na dole hello (poniżej reguła "BLOCKALL" hello) nigdy nie będą wchodzić w grę. Upewnij się, że hello nowo utworzona reguła dla ruchu w sieci web jest powyżej hello BLOCKALL reguły.

Po utworzeniu reguły hello musi być przypisany toohello zapory, a następnie aktywowany, jeśli nie zostanie to zrobione reguły hello zmiana nie zacznie obowiązywać. Hello procesu wypychania i aktywacji jest opisany w następnej sekcji hello.

## <a name="rule-activation"></a>Reguły aktywacji
Z hello ruleset zmodyfikowane tooadd tej reguły, hello ruleset musi być przekazywane toohello zapory i aktywowane.

![Aktywacja reguły zapory][4]

W prawym górnym narożniku hello powitania klienta zarządzania są klastra przycisków. Kliknij przycisk hello "Wyślij zmiany" przycisk toosend hello zmodyfikowane zasady toohello zapory, a następnie kliknij przycisk "Uaktywnij" hello.

Z aktywacji hello zestaw reguł zapory hello tej kompilacji w środowisku przykładzie zostanie zakończona. Opcjonalnie hello post kompilacji w hello odwołuje się do sekcji można uruchamiać skryptów tooadd aplikacji toothis środowiska tootest hello poniżej scenariusze ruchu.

> [!IMPORTANT]
> Jest krytyczne toorealize, że nie nastąpi trafienie powitania serwera sieci web bezpośrednio. Gdy przeglądarka żąda strony HTTP z FrontEnd001.CloudApp.Net, przekazuje (port 80) punktu końcowego HTTP hello Zapora toohello ruchu nie hello serwer sieci web. Witaj zapory, a następnie, zgodnie z toohello reguły utworzone powyżej translatory adresów sieciowych, które żądają toohello serwera sieci Web.
> 
> 

## <a name="traffic-scenarios"></a>Scenariusze ruchu
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Dozwolone) TooWeb Web Server przez zaporę
1. Strony internetowe użytkownika żądania HTTP z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. Chmury usługi przekazuje ruch przez otwarty punkt końcowy na interfejsie lokalnym toofirewall port 80 na 10.0.1.4:80
3. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. Zastosować grupy NSG zasady 3 (Internet tooFirewall), ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)
5. Reguła zapory przekazywania Zobacz to jest ruch na porcie 80, go przekierowuje serwera sieci web toohello IIS01
6. IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello
7. IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji
8. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
9. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę
   4. Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania
10. AppVM01 odbiera hello zapytanie SQL i odpowiada
11. Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone
12. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
    1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
    2. Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.
13. Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello obiektu żądającego
14. Ponieważ jest to sesji translatora adresów Sieciowych z zapory hello, miejsce docelowe odpowiedzi hello (początkowo) dotyczy hello zapory
15. zapory Hello odbiera odpowiedź hello z powitania serwera sieci Web i przekazuje wstecz toohello użytkowników Internetu
16. Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci frontonu jest dozwolona, i hello Internet użytkownik otrzymuje hello strona sieci web.

#### <a name="allowed-rdp-toobackend"></a>(Dozwolone) TooBackend protokołu RDP
1. Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP w przypadku xxxxx hello losowo przypisany numer portu dla protokołu RDP tooAppVM01 BackEnd001.CloudApp.Net:xxxxx (hello przypisany port znajduje się na powitania portalu Azure lub za pomocą programu PowerShell)
2. Ponieważ hello zapory tylko nasłuchuje na powitania FrontEnd001.CloudApp.Net adres nie uczestniczy z tego przepływu ruchu
3. Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania
4. Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony
5. Włączono sesji protokołu RDP
6. AppVM01 wyświetli monit o hasło nazwy użytkownika

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Dozwolone) Wyszukiwania DNS serwera sieci Web na serwerze DNS
1. Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.
2. Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello
3. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
4. Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:
   1. Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania
5. Serwer DNS odbiera żądanie hello
6. Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet
7. Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony
8. DNS w Internecie serwer odpowiada, ponieważ ta sesja została zainicjowana wewnętrznie, odpowiedź hello jest dozwolone.
9. Serwer DNS będzie buforować odpowiedź hello i odpowiada tooIIS01 wstecz toohello żądania początkowego
10. Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony
11. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
    1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
    2. Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony
12. IIS01 odbiera odpowiedź hello z DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Dozwolone) Plik dostępu do serwera sieci Web na AppVM01
1. IIS01 żąda pliku na AppVM01
2. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
3. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę
   4. Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania
4. AppVM01 odbiera żądanie hello i wysyła plik (przy założeniu, że autoryzacji dostępu)
5. Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone
6. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
   1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
   2. Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.
7. Serwer usług IIS Hello odbiera hello pliku

#### <a name="denied-web-direct-tooweb-server"></a>(Odmowa) Bezpośrednie tooWeb sieci Web serwera
Ponieważ powitania serwera sieci Web, IIS01 i hello zapory są w hello mają tej samej usługi w chmurze hello sam publiczny adres IP połączonej. W związku z tym cały ruch HTTP będą kierowane toohello zapory. Podczas żądania hello czy można pomyślnie obsłużył operację, go nie można przejść bezpośrednio toohello serwera sieci Web, jest przekazywany, zgodnie z założeniami, za pośrednictwem hello najpierw zapory. Zobacz hello pierwszego scenariusza, w tej sekcji hello ruchu.

#### <a name="denied-web-toobackend-server"></a>(Odmowa) TooBackend sieci Web serwera
1. Internet użytkownik spróbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Odmowa) Wyszukiwania DNS w sieci Web na serwerze DNS
1. Internet użytkownik spróbuje toolookup wewnętrzny rekord DNS na DNS01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla serwera DNS, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu (Uwaga: nie ma zastosowania tej reguły 1 (DNS) z dwóch przyczyn, pierwszy adres źródłowy hello jest hello internet, ta zasada ma zastosowanie tylko toohello również lokalnej sieci wirtualnej jako hello źródła jest to Reguła zezwalająca, nigdy nie będzie go odmówić ruchu)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Odmowa) Dostęp w sieci Web tooSQL przez zaporę
1. Internet użytkownik żąda danych SQL z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, to nie przejdzie hello usługi w chmurze i nie osiągnąć hello zapory
3. Jeśli punkty końcowe zostały otwarte jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. 2 reguły NSG (Internet tooFirewall) mają zastosowanie, ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)
5. Zapora nie ma przekazywanie reguł dla bazy danych SQL i porzucania hello ruchu

## <a name="conclusion"></a>Podsumowanie
Jest to stosunkowo proste do przodu sposób ochrony aplikacji za pomocą zapory i izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.

Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].

## <a name="references"></a>Dokumentacja
### <a name="main-script-and-network-config"></a>Skrypt głównego i konfiguracji sieci
Zapisz hello pełne skryptu w pliku skryptu programu PowerShell. Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf2.xml".
Modyfikuj zmienne zdefiniowane przez użytkownika hello, zgodnie z potrzebami. Uruchom skrypt hello, a następnie postępuj zgodnie z powyższych instrukcji instalacji reguły zapory hello.

#### <a name="full-script"></a>Pełna skryptu
Ten skrypt zostanie, na podstawie hello zmiennych zdefiniowanych przez użytkownika:

1. Połącz tooan subskrypcji platformy Azure
2. Utwórz nowe konto magazynu
3. Utwórz nową sieć wirtualną z dwoma podsieciami, zgodnie z definicją w pliku konfiguracji sieci hello
4. Tworzenie maszyn wirtualnych serwera 4 windows
5. Skonfiguruj grupy NSG w tym:
   * Tworzenie grupy NSG
   * Zapełnianie reguły
   * Powiązanie hello NSG toohello odpowiednie podsieci

Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.

> [!IMPORTANT]
> Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell. Tylko komunikaty o błędach na czerwono są przyczyną problemu.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Plik konfiguracji sieci
Zapisz ten plik xml z lokalizacji zaktualizowane i Dodaj hello łącze toothis pliku toohello $NetworkConfigFile zmiennej w skrypcie hello powyżej.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Przykładowe skrypty aplikacji
Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Przychodzący DMZ z grupy NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Ikona NAT docelowego"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Reguły zapory"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Aktywacja reguły zapory"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
