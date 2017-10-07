---
title: "aaaAzure przykład DMZ — Tworzenie prostego DMZ z grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Przykład 1 — Tworzenie prostego DMZ, za pomocą grup NSG z klasycznego środowiska PowerShell
[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]

> [!div class="op_single_selector"]
> * [Szablon usługi Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classic — PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

W tym przykładzie tworzy DMZ pierwotnych z czterech serwerów z systemem Windows i grupy zabezpieczeń sieci. W tym przykładzie przedstawiono każdy hello odpowiednich PowerShell poleceń tooprovide głębsze zrozumienie każdego kroku. Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ. Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy. 

![Przychodzący DMZ z grupy NSG][1]

## <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie subskrypcja zawiera hello następujące zasoby:

* Dwie usługi w chmurze: "FrontEnd001" i "BackEnd001"
* Sieć wirtualną "CorpNetwork", z dwoma podsieciami; "FrontEnd" i "Wewnętrzna"
* Grupy zabezpieczeń sieci jest stosowane tooboth podsieci
* Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwóch systemów windows Server, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")

W sekcji odwołań hello jest skrypt programu PowerShell, która tworzy większość środowiska hello opisane w tym przykładzie. Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie. 

toobuild hello środowiska;

1. Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)
2. Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi, itp.)
3. Uruchom skrypt hello w programie PowerShell

>[!Note]
>region Hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.
>
>

Po hello skrypt zostanie uruchomiony pomyślnie dodatkowe opcjonalne kroki mogą zostać podjęte, w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.

Witaj poniższe sekcje zawierają szczegółowy opis grup zabezpieczeń sieci i ich działania w tym przykładzie przez Instruktaż wierszy kluczy hello skryptu programu PowerShell.

## <a name="network-security-groups-nsg"></a>Sieciowe grupy zabezpieczeń (NSG)
Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł. 

> [!TIP]
> Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny". Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze. Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane. Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).
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

Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet. Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących. toolock dół ruchu w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagany i jest przedstawione w "W przykładzie 3" na powitania [strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME].

Każda reguła omówiono bardziej szczegółowo w następujący sposób (**Uwaga**: dowolny element w hello następujące listy rozpoczynający się od znaku dolara (na przykład: $NSGName) jest zmienną użytkownika ze skryptu hello hello odwołanie sekcji tego dokumentu):

1. Najpierw sieciowej grupy zabezpieczeń muszą zostać skompilowane toohold hello reguł:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. Pierwsza reguła Hello w tym przykładzie zezwala na ruch DNS między wszystkich serwerów DNS toohello sieciach wewnętrznych hello podsieci wewnętrznej bazy danych. Reguła Hello zawiera niektóre ważne parametry:
   
   * "Typ" oznacza, że w kierunku przepływu ruchu obowiązuje tej reguły. Kierunek Hello jest z punktu widzenia hello hello podsieci lub maszyny wirtualnej (w zależności od tego, gdzie jest powiązany ten NSG). W związku z tym jeśli typ to "Przychodzącego" i ruchu jest wprowadzanie hello podsieci, powinna zostać zastosowana reguła hello i ruchu wychodzącego hello podsieci nie może niekorzystnie wpływać tej reguły.
   * "Priority" Ustawia kolejność hello, w jakiej są oceniane przepływu ruchu. Witaj niższe hello numer hello wyższy hello priorytet. Jeśli reguła ma zastosowanie tooa przepływu ruchu, żadne dalsze reguły są przetwarzane. W związku z tym jeśli reguła o priorytecie 1 zezwala na ruch i reguły o priorytecie 2 nie zezwala na ruch i tootraffic mają zastosowanie zarówno reguły, a następnie hello ruch będzie dozwolony tooflow (ponieważ reguła 1 ma wyższy priorytet trwało efektu i żadne dodatkowe reguły zostały zastosowane).
   * "Akcja" oznacza, że jeśli ruch wpływ ta reguła jest zablokowane lub dozwolone.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Ta zasada umożliwia tooflow ruchu protokołu RDP z portem RDP toohello internet hello na dowolnym serwerze na powitania powiązany podsieci. Ta zasada wykorzystuje dwa typy specjalne prefiksy adresów; "VIRTUAL_NETWORK" i "INTERNET". Tagi te są łatwo tooaddress większych kategorii prefiksy adresów.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Ta zasada umożliwia przychodzący serwera sieci web hello toohit internet ruchu. Ta zasada nie zmienia hello zachowanie routingu. zasada Hello umożliwia tylko ruch kierowany do IIS01 toopass. W związku z tym jeśli ruch z hello Internet miał powitania serwera sieci web jako miejsca docelowego tej reguły spowoduje zezwolenie i zatrzymać dalsze przetwarzanie reguł. (W regule hello priorytetem 140 wszystkich innych przychodzącego ruchu internetowego jest zablokowane). Jeśli jest tylko przetwarzania ruchu HTTP, ta zasada może być dalsze ograniczeniami tooonly Zezwalaj docelowy Port 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Ta zasada umożliwia toopass ruchu z serwera IIS01 powitania serwera AppVM01 toohello, nowsze reguła blokuje cały ruch tooBackend frontonu. tooimprove tej reguły, jeśli znane jest hello portu, który powinien zostać dodane. Na przykład, jeśli serwer IIS hello jest naciśnięcie tylko programu SQL Server na AppVM01, zakres portów docelowych hello należy zmienić "*" (Any) too1433 (hello SQL port) dzięki czemu mniejsze przychodzących ataki AppVM01 aplikacji sieci web hello kiedykolwiek zagrożenia bezpieczeństwa.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Ta reguła nie zezwala na ruch z hello internet tooany serwerów w sieci hello. Przy użyciu reguł hello priorytetem 110 i 120 efekt hello jest tooallow tylko dla ruchu przychodzącego ruchu toohello zapory internetowej i porty protokołu RDP na serwerach i blokuje wszystkie inne elementy. Ta reguła jest "awaryjnie" reguły tooblock wszystkie przepływy nieoczekiwany.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. Reguła końcowego Hello nie zezwala na ruch z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello. Ponieważ ta reguła jest tylko regułę ruchu przychodzącego, odwrotnej ruch jest dozwolony (od toohello zaplecza hello frontonu).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Scenariusze ruchu
#### <a name="allowed-internet-tooweb-server"></a>(*Dozwolone*) Internet tooweb serwera
1. Użytkownik internet zażąda strony HTTP z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. W chmurze usługi przekazuje ruch przez otwarty punkt końcowy na porcie 80 kierunku IIS01 (powitania serwera sieci web)
3. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP serwera sieci web hello IIS01 (10.0.1.5)
5. IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello
6. IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji
7. Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
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
12. Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello obiektu żądającego
13. Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu hello hello odpowiedzi jest dozwolone, a hello internet użytkownik otrzymuje hello strona sieci web.

#### <a name="allowed-rdp-toobackend"></a>(*Dozwolone*) toobackend protokołu RDP
1. Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP w przypadku xxxxx hello losowo przypisany numer portu dla protokołu RDP tooAppVM01 BackEnd001.CloudApp.Net:xxxxx (hello przypisany port znajduje się na powitania portalu Azure lub za pomocą programu PowerShell)
2. Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania
3. Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony
4. Włączono sesji protokołu RDP
5. AppVM01 monit o podanie hello nazwy użytkownika i hasła

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

#### <a name="denied-web-toobackend-server"></a>(*Odmowa*) serwera sieci Web toobackend
1. Użytkownik internet próbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dostęp powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Odmowa*) wyszukiwanie nazwy DNS w sieci Web na serwerze DNS
1. Użytkownik internet próbuje toolook się wewnętrzny rekord DNS na DNS01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla serwera DNS, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dostęp powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu (Uwaga: nie ma zastosowania tej reguły 1 (DNS) z dwóch przyczyn, pierwszy adres źródłowy hello jest hello internet, ta zasada ma zastosowanie tylko toohello również lokalnej sieci wirtualnej jako hello źródła Ta reguła jest Reguła zezwalająca, nigdy nie będzie go odmówić ruchu)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Odmowa*) tooSQL dostęp za pośrednictwem zapory w sieci Web
1. Użytkownik internet żąda danych SQL z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dotrzeć hello zapory
3. Jeśli punkty końcowe zostały otwarte jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę
   3. Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania
4. Ruch trafienia wewnętrzny adres IP hello IIS01 (10.0.1.5)
5. IIS01 nie nasłuchuje na porcie 1433, więc nie ma odpowiedzi toohello żądania

## <a name="conclusion"></a>Podsumowanie
W tym przykładzie jest stosunkowo proste i bezpośrednio do przodu sposobem izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.

Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].

## <a name="references"></a>Dokumentacja
### <a name="main-script-and-network-config"></a>Główne config skryptu i sieci
Zapisz hello pełne skryptu w pliku skryptu programu PowerShell. Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf1.xml."
Modyfikuj zmienne zdefiniowane przez użytkownika hello jako hello potrzebne i uruchom skrypt.

#### <a name="full-script"></a>Pełny skrypt
Ten skrypt zostanie, na podstawie zmiennych zdefiniowanych przez użytkownika hello;

1. Połącz tooan subskrypcji platformy Azure
2. Tworzenie konta magazynu
3. Tworzenie sieci wirtualnej z dwoma podsieciami, zgodnie z definicją w pliku konfiguracji sieci hello
4. Tworzenie maszyn wirtualnych serwera cztery systemu windows
5. Skonfiguruj grupy NSG w tym:
   * Utworzenie grupy NSG
   * Zapełnianie reguły
   * Powiązanie hello NSG toohello odpowiednie podsieci

Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.

> [!IMPORTANT]
> Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell. Tylko komunikaty o błędach na czerwono są przyczyną problemu.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Plik konfiguracji sieci
Zapisz ten plik xml z lokalizacji zaktualizowane i dodawać hello łącze toothis pliku toohello $NetworkConfigFile zmiennej hello poprzedzających skryptu.

```XML
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
```

#### <a name="sample-application-scripts"></a>Przykładowe skrypty aplikacji
Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]

## <a name="next-steps"></a>Następne kroki
* Aktualizowanie i Zapisz plik XML
* Uruchom hello — środowiska hello toobuild skryptu PowerShell
* Zainstaluj hello przykładowej aplikacji
* Testowanie różnych ruch za pośrednictwem tego DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Przychodzący DMZ z grupy NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

