---
title: "aaaAzure przykład DMZ — Tworzenie prostego DMZ z grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Przykład 1 — Tworzenie prostego DMZ, za pomocą grup NSG z szablonem usługi Azure Resource Manager
[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]

> [!div class="op_single_selector"]
> * [Szablon usługi Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classic — PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

W tym przykładzie tworzy DMZ pierwotnych z czterech serwerów z systemem Windows i grupy zabezpieczeń sieci. W tym przykładzie przedstawiono każdy hello odpowiedni szablon sekcje tooprovide głębsze zrozumienie każdego kroku. Istnieje również tooprovide sekcji scenariusza ruchu krok po kroku omówiono sposób obejmującego hello warstw zabezpieczeń w strefie DMZ hello ruchu. Na koniec w sekcji odwołań hello jest pełny szablon hello toobuild kodu i instrukcje tego tootest środowiska i doświadczenia z różnych scenariuszy. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Przychodzący DMZ z grupy NSG][1]

## <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie subskrypcja zawiera hello następujące zasoby:

* Pojedyncza grupa zasobów
* Sieć wirtualną z dwiema podsieciami; "FrontEnd" i "Wewnętrzna"
* Grupy zabezpieczeń sieci jest stosowane tooboth podsieci
* Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwóch systemów windows Server, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")
* Publiczny adres IP skojarzone z serwerem sieci web aplikacji hello

W sekcji odwołań hello ma szablonu usługi Azure Resource Manager tooan link, który tworzy środowisko hello opisane w tym przykładzie. Maszyny wirtualne hello budynku i sieciami wirtualnymi, mimo że wykonywane przez szablon przykład Witaj, nie opisano szczegółowo w tym dokumencie. 

**toobuild to środowisko** (szczegółowe instrukcje znajdują się w sekcji odwołań hello tego dokumentu);

1. Wdrażanie hello szablon Menedżera zasobów Azure w: [szablonów Szybki Start Azure][Template]
2. Zainstaluj hello przykładową aplikację w: [przykładowy skrypt aplikacji][SampleApp]

>[!NOTE]
>serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku". Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS. Alternatywnie publicznego adresu IP może być skojarzony z każdym serwerem kart interfejsu Sieciowego protokołu RDP łatwiejsze.
> 
>

Witaj poniższe sekcje zawierają szczegółowy opis hello sieciowej grupy zabezpieczeń i jak działa w tym przykładzie przez Instruktaż klucza wierszy hello szablon Menedżera zasobów Azure.

## <a name="network-security-groups-nsg"></a>Sieciowe grupy zabezpieczeń (NSG)
Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł. 

>[!TIP]
>Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny". Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze. Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane. Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).
>
>

Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:

1. Wewnętrzny ruch DNS (port 53) jest dozwolony
2. Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny Wirtualnej jest dozwolony
3. Ruch HTTP (port 80) z serwera tooweb internetowej hello (IIS01) jest dozwolony
4. Cały ruch (wszystkie porty) z IIS01 tooAppVM1 jest dozwolona
5. Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (obie podsieci)
6. Cały ruch (wszystkie porty) z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello jest zabroniony

Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry. W związku z tym żądania HTTP hello mogliby toohello serwera sieci web. Jeśli ten sam ruch próbował tooreach hello DNS01 serwer, reguła 5 (odmowa) mogą być hello pierwszy tooapply hello ruch w sieci i nie będzie dozwolone toopass toohello serwera. Reguła 6 (Odmów) blokuje hello podsieci frontonu z mówić toohello podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), ten zestaw reguł chroni hello sieci wewnętrznej bazy danych w przypadku, gdy osoba atakująca dokonywania hello aplikacji sieci web na powitania serwera sieci Web, osoba atakująca hello czy ograniczona toohello dostępu do sieci (tylko tooresources udostępniane na serwerze AppVM01 hello) wewnętrznej bazy danych "protected".

Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet. Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących. tooapply tootraffic zasad zabezpieczeń w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagany i jest przedstawione w "W przykładzie 3" na powitania [strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME].

Każda reguła omówiono bardziej szczegółowo w następujący sposób:

1. Zasób grupy zabezpieczeń sieci musi być skonkretyzowanym toohold hello reguł:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. Pierwsza reguła Hello w tym przykładzie zezwala na ruch DNS między wszystkich serwerów DNS toohello sieciach wewnętrznych hello podsieci wewnętrznej bazy danych. Reguła Hello zawiera niektóre ważne parametry:
  * "destinationAddressPrefix" - reguły można używać specjalnego typu o nazwie "Domyślna Tag" prefiksu adresu, tagi te są dostarczane przez system identyfikatorów, które umożliwia tooaddress łatwy sposób większych kategorii prefiksy adresów. Ta zasada domyślna Tag "Internet" hello używa toosignify żadnego adresu poza hello sieci wirtualnej. Inne etykiety prefiks są VirtualNetwork i AzureLoadBalancer.
  * "Direction" oznacza, że w kierunku przepływu ruchu obowiązuje tej reguły. Kierunek Hello jest z punktu widzenia hello hello podsieci lub maszyny wirtualnej (w zależności od tego, gdzie jest powiązany ten NSG). W związku z tym jeśli "Przychodzącego" jest skierowany i ruchu jest wprowadzanie hello podsieci, powinna zostać zastosowana reguła hello i ruchu wychodzącego hello podsieci nie może niekorzystnie wpływać tej reguły.
  * "Priority" Ustawia kolejność hello, w jakiej są oceniane przepływu ruchu. Witaj niższe hello numer hello wyższy hello priorytet. Jeśli reguła ma zastosowanie tooa przepływu ruchu, żadne dalsze reguły są przetwarzane. W związku z tym jeśli reguła o priorytecie 1 zezwala na ruch i reguły o priorytecie 2 nie zezwala na ruch i tootraffic mają zastosowanie zarówno reguły, a następnie hello ruch będzie dozwolony tooflow (ponieważ reguła 1 ma wyższy priorytet trwało efektu i żadne dodatkowe reguły zostały zastosowane).
  * "Access" oznacza, że jeśli wpływ ta reguła jest zablokowane ("Deny") lub dozwolonych ("Zezwalaj").

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Ta zasada umożliwia tooflow ruchu protokołu RDP z portem RDP toohello internet hello na dowolnym serwerze na powitania powiązany podsieci. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Ta zasada umożliwia przychodzący serwera sieci web hello toohit internet ruchu. Ta zasada nie zmienia hello zachowanie routingu. zasada Hello umożliwia tylko ruch kierowany do IIS01 toopass. W związku z tym jeśli ruch z hello Internet miał powitania serwera sieci web jako miejsca docelowego tej reguły spowoduje zezwolenie i zatrzymać dalsze przetwarzanie reguł. (W regule hello priorytetem 140 wszystkich innych przychodzącego ruchu internetowego jest zablokowane). Jeśli jest tylko przetwarzania ruchu HTTP, ta zasada może być dalsze ograniczeniami tooonly Zezwalaj docelowy Port 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Ta zasada umożliwia toopass ruchu z serwera IIS01 powitania serwera AppVM01 toohello, nowsze reguła blokuje cały ruch tooBackend frontonu. tooimprove tej reguły, jeśli znane jest hello portu, który powinien zostać dodane. Na przykład, jeśli serwer IIS hello jest naciśnięcie tylko programu SQL Server na AppVM01, zakres portów docelowych hello należy zmienić "*" (Any) too1433 (hello SQL port) dzięki czemu mniejsze przychodzących ataki AppVM01 aplikacji sieci web hello kiedykolwiek zagrożenia bezpieczeństwa.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Ta reguła nie zezwala na ruch z hello internet tooany serwerów w sieci hello. Przy użyciu reguł hello priorytetem 110 i 120 efekt hello jest tooallow tylko dla ruchu przychodzącego ruchu toohello zapory internetowej i porty protokołu RDP na serwerach i blokuje wszystkie inne elementy. Ta reguła jest "awaryjnie" reguły tooblock wszystkie przepływy nieoczekiwany.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. Reguła końcowego Hello nie zezwala na ruch z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello. Ponieważ ta reguła jest tylko regułę ruchu przychodzącego, odwrotnej ruch jest dozwolony (od toohello zaplecza hello frontonu).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Scenariusze ruchu
#### <a name="allowed-internet-tooweb-server"></a>(*Dozwolone*) Internet tooweb serwera
1. Użytkownik internet zażąda strony HTTP od hello publicznego adresu IP karty Sieciowej skojarzonych z hello kart IIS01 powitalne
2. Hello publicznego adresu IP przekazuje ruch toohello sieci wirtualnej kierunku IIS01 (powitania serwera sieci web)
3. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
  1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
  2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
  3. Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP serwera sieci web hello IIS01 (10.0.1.5)
5. IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello
6. IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji
7. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
8. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
  1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
  2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
  3. Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę
  4. Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania
9. AppVM01 odbiera hello zapytanie SQL i odpowiada
10. Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona
11. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
  1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
  2. Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.
12. Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello. strona żądająca
13. Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu hello, odpowiedź hello jest dozwolone i hello Internet użytkownik otrzymuje hello strona sieci web.

#### <a name="allowed-rdp-tooiis-server"></a>(*Dozwolone*) serwera tooIIS RDP
1. TooIIS01 sesji protokołu RDP na powitania publicznego adresu IP karty Sieciowej skojarzonych z hello IIS01 karty Sieciowej (ten publiczny adres IP znajduje się za pośrednictwem hello portalu lub programu PowerShell) powitalne żąda uprawnień administratora serwera w Internecie
2. Hello publicznego adresu IP przekazuje ruch toohello sieci wirtualnej kierunku IIS01 (powitania serwera sieci web)
3. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
  1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
  2. Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania
4. Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony
5. Włączono sesji protokołu RDP
6. IIS01 monit o podanie hello nazwy użytkownika i hasła

>[!NOTE]
>serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku". Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Dozwolone*) wyszukiwanie nazwy DNS serwera sieci Web na serwerze DNS
1. Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.
2. Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello
3. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
4. Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:
  * Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Dozwolone*) pliku dostępu do serwera sieci Web na AppVM01
1. IIS01 żąda pliku na AppVM01
2. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
3. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
  1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
  2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
  3. Grupa NSG zasady 3 (Internet tooIIS01) nie ma zastosowania, przenieść toonext regułę
  4. Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania
4. AppVM01 odbiera żądanie hello i wysyła plik (przy założeniu, że autoryzacji dostępu)
5. Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona
6. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
  1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
  2. Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.
7. Serwer usług IIS Hello odbiera hello pliku

#### <a name="denied-rdp-toobackend"></a>(*Odmowa*) toobackend protokołu RDP
1. Użytkownik internet próbuje tooRDP tooserver AppVM01
2. Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera
3. Jednak jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 2 (RDP) umożliwiałyby ten ruch

>[!NOTE]
>serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku". Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Odmowa*) serwera sieci Web toobackend
1. Użytkownik internet próbuje tooaccess pliku na AppVM01
2. Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera
3. Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet tooVNet) czy zablokować ruch

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Odmowa*) wyszukiwanie nazwy DNS w sieci Web na serwerze DNS
1. Użytkownik internet próbuje toolook się wewnętrzny rekord DNS na DNS01
2. Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera
3. Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet tooVNet) czy zablokować ruch (Uwaga: Aby reguła 1 (DNS) nie będą miały zastosowania ponieważ hello żądania adresu źródłowego jest hello internet i 1 reguła ma zastosowanie tylko toohello lokalnej sieci wirtualnej jako źródło hello)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Odmowa*) dostępu SQL na serwerze sieci web hello
1. Użytkownik internet żąda danych SQL z IIS01
2. Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera
3. Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:
  1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
  2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
  3. Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP hello IIS01 (10.0.1.5)
5. IIS01 nie nasłuchuje na porcie 1433, więc nie ma odpowiedzi toohello żądania

## <a name="conclusion"></a>Podsumowanie
W tym przykładzie jest stosunkowo proste i bezpośrednio do przodu sposobem izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.

Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].

## <a name="references"></a>Dokumentacja
### <a name="azure-resource-manager-template"></a>Szablon usługi Azure Resource Manager
W tym przykładzie używa wstępnie zdefiniowanych szablonów usługi Azure Resource Manager w repozytorium GitHub obsługiwanego przez firmę Microsoft i otworzyć toohello społeczności. Tego szablonu można wdrożyć bezpośrednio z witryny GitHub, lub pobrane i zmodyfikować toofit potrzeb. 

Szablon głównego Hello znajduje się w pliku hello o nazwie "azuredeploy.json." Ten szablon może zostać przesłane za pomocą programu PowerShell lub interfejsu wiersza polecenia (z plikiem skojarzone "azuredeploy.parameters.json" hello) toodeploy tego szablonu. Mogę znaleźć hello najprostszą metodą jest hello toouse przycisku "Wdróż tooAzure" na stronie README.md hello w witrynie GitHub.

toodeploy hello szablon, który tworzy w tym przykładzie z serwisu GitHub i hello portalu Azure, wykonaj następujące kroki:

1. W przeglądarce Przejdź toohello [szablonu][Template]
2. Kliknij przycisk "Wdróż tooAzure" hello (lub toosee przycisk "Wizualizacja" hello graficzną reprezentację tego szablonu)
3. Wprowadź w bloku parametrów hello hello konta magazynu, nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**
5. Utwórz grupę zasobów dla tego wdrożenia (można użyć istniejącego, ale zalecane jest nowy, aby uzyskać najlepsze wyniki)
6. W razie potrzeby zmień ustawienia subskrypcji i lokalizacji hello sieci wirtualnej.
7. Kliknij przycisk **Przejrzyj postanowienia prawne**, przeczytaj warunki hello i kliknij przycisk **zakupu** tooagree.
8. Kliknij przycisk **Utwórz** toobegin hello wdrożenia tego szablonu.
9. Po hello wdrożenie zakończy się pomyślnie, przejdź toohello utworzone dla tego wdrożenia zasobów hello toosee skonfigurowane wewnątrz grupy zasobów.

>[!NOTE]
>Ten szablon umożliwia RDP toohello IIS01 serwera tylko (hello Znajdź publicznego adresu IP dla IIS01 na powitania portalu). serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku". Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.
>
>

tooremove tego wdrożenia, Usuń hello grupy zasobów i wszystkie zasoby podrzędne zostaną również usunięte.

#### <a name="sample-application-scripts"></a>Przykładowe skrypty aplikacji
Po pomyślnym uruchomieniu szablonu hello, musisz skonfigurować powitania serwera sieci web i serwera aplikacji tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ. tooinstall przykładowej aplikacji to i inne przykłady DMZ jedną dostarczono na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]

## <a name="next-steps"></a>Następne kroki

* W tym przykładzie wdrożenia
* Tworzenie hello przykładowej aplikacji
* Testowanie różnych ruch za pośrednictwem tego DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Przychodzący DMZ z grupy NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md