---
title: "Opis klastra Menedżera zasobów aaaCluster | Dokumentacja firmy Microsoft"
description: "Określając domen błędów, uaktualnienia domen, właściwości węzła i pojemności węzła dla hello Menedżera zasobów klastra, opisujący klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Opisujące klastra sieci szkieletowej usług
Hello zasobu klastra sieci szkieletowej programu Service Manager zapewnia kilka mechanizmów opisujące klastra. W czasie wykonywania hello Cluster Resource Manager korzysta z tej informacji tooensure wysoką dostępność usług hello uruchomionych w klastrze hello. Wymuszając te reguły ważne również podejmie zużycie zasobów hello toooptimize w ramach klastra hello.

## <a name="key-concepts"></a>Kluczowe pojęcia
Witaj Menedżera zasobów klastra obsługuje kilka funkcji, które opisują klastra:

* Domen błędów
* Domen uaktualnienia
* Właściwości węzła
* Możliwości węzła

## <a name="fault-domains"></a>Domeny błędów
Domeny błędów jest części skoordynowanego awarii. Jedna maszyna jest domeny błędów (od momentu jego może zakończyć się niepowodzeniem na jego własnej dla różnych powodów, power dostaw błędów toodrive błędów toobad kart oprogramowania układowego). Maszyny połączonych toohello są tego samego przełącznika Ethernet w hello tej samej domenie błędów, jak są maszyny udostępniania jednego źródła zasilania lub w pojedynczej lokalizacji. Ponieważ jest to fizyczne dla toooverlap błędów sprzętu domen błędów są z założenia hierarchiczna i są reprezentowane jako identyfikatory URI w sieci szkieletowej usług.

Należy pamiętać, że domen błędów są poprawnie skonfigurowane, ponieważ usługi Service Fabric korzysta z tej informacji toosafely miejsce usług. Usługi sieć szkieletowa nie ma tooplace usługi tak, aby hello utraty domeny błędów (spowodowany awarią hello niektórych składnika) powoduje, że toogo usług w dół. W hello środowiska platformy Azure w sieci szkieletowej usług używa hello domeny błędów informacji dostarczonych przez toocorrectly środowiska hello skonfigurować hello węzłów w klastrze hello w Twoim imieniu. Dla usługi sieci szkieletowej autonomiczny, domen błędów są zdefiniowane w czasie hello klastra hello jest skonfigurowany 

> [!WARNING]
> Jest ważne, że hello informacji o domenie błędów pod warunkiem, że tooService sieci szkieletowej są dokładne. Na przykład załóżmy, że węzły klastra usługi sieć szkieletowa działają wewnątrz 10 maszyn wirtualnych na hostach fizycznych pięć. W takim przypadku mimo 10 maszyn wirtualnych, jest tylko 5 różnych (najwyższego poziomu) domeny błędów. Udostępnianie hello, w tym samym hoście fizycznym powoduje, że tooshare maszyn wirtualnych hello tej samej domenie błędów głównego, ponieważ hello obsługi maszyn wirtualnych koordynowane błąd, jeśli nie powiedzie się ich hosta fizycznego.  
>
> Ponieważ sieci szkieletowej usług oczekuje hello domenie awarii węzła nie toochange. Inne mechanizmy zapewniania wysokiej dostępności hello maszyn wirtualnych, takie jak [maszyn wirtualnych wysokiej dostępności](https://technet.microsoft.com/en-us/library/cc967323.aspx), użyj przezroczystego migracji maszyn wirtualnych z jednego hosta tooanother. Te mechanizmy ponowne konfigurowanie lub nie Powiadamiaj hello uruchamiania kodu wewnątrz hello maszyny Wirtualnej. Tak, są one **nieobsługiwane** jako środowiska do uruchamiania usługi sieć szkieletowa klastrów. Usługa sieci szkieletowej powinna być stosowanej technologii tylko wysokiej dostępności hello. Mechanizmy, takie jak migracja maszyny Wirtualnej sieci SAN, lub inne osoby nie są konieczne. Jeśli używany w połączeniu z usługi Service Fabric tych mechanizmów _zmniejszyć_ aplikacji dostępność i niezawodność, ponieważ ich wprowadzenie dodatkowej złożoności, Dodaj scentralizowane źródła błędu i wykorzystania niezawodność i Strategie dostępności, które powodują konflikt z aliasami w sieci szkieletowej usług. 
>
>

Hello rysunku poniżej możemy kolor wszystkich jednostek hello wchodzących w skład domeny tooFault i listy wszystkich hello różnych domen błędów, które powoduje. W tym przykładzie mamy centrów danych ("DC"), stojakami ("R") i bloki ("B"). Powrotne Jeśli każdy blok zawiera więcej niż jednej maszyny wirtualnej, mogą występować innej warstwy w hello hierarchii domeny błędów.

<center>
![Węzły zorganizowane za pośrednictwem domen błędów][Image1]
</center>

W czasie wykonywania hello zasobu klastra sieci szkieletowej programu Service Manager uwzględnia hello domen błędów w klastrze hello i planów układów. Witaj stanowe repliki lub bezstanowych wystąpień dla danej usługi są dystrybuowane, dzięki czemu są one w oddzielnych domen błędów. Dystrybucję usługi hello domen błędów gwarantuje, że dostępność hello hello usługi nie zostanie naruszony, gdy domeny błędów nie powiodło się na dowolnym poziomie hierarchii hello.

Menedżer zasobów klastra usługi sieć szkieletowa nie szczególną uwagę liczbę warstw w hello hierarchii domeny błędów. Jednak spróbuje tooensure, który hello utraty jednej części hierarchii hello bez wpływu na usługi uruchomione w nim. 

Najlepiej, jeśli istnieją hello samą liczbę węzłów na każdym poziomie hierarchii w hello hierarchii domeny błędów. Jeśli hello "drzewa" domen błędów jest niezrównoważone w klastrze, utrudni dla hello toofigure Menedżera zasobów klastra limit alokacji najlepsze hello usług. Imbalanced układów domen błędów oznacza hello stratę niektórych domen wpływ hello dostępności usług więcej niż innych domen. W związku z tym rozerwana hello Menedżera zasobów klastra między dwa cele: chce toouse hello komputerów w domenie "duże" przez umieszczenie na nich usługi i chce tooplace usług w innych domenach, dzięki czemu utrata hello domeny nie powoduje problemów. 

Jak wyglądają imbalanced domen? W poniższym diagramie hello zostanie przedstawiony dwóch układów innego klastra. W pierwszym przykładzie hello hello węzły są rozmieszczane równomiernie między hello domen błędów. W drugim przykładzie hello jednej domenie błędów ma wiele więcej węzłów niż hello innych domen błędów. 

<center>
![Dwa układów innego klastra][Image2]
</center>

Na platformie Azure wybór hello domeny błędów zawiera węzeł odbywa się. Jednak w zależności od hello liczba węzłów, które należy udostępnić można nadal na końcu domen błędów z większą liczbę węzłów w je od innych. Na przykład, że masz pięć domen błędów w klastrze hello, ale udostępniać siedmiu węzłów dla danego NodeType. W takim przypadku hello dwóch pierwszych domen błędów końcowa więcej węzłów. Jeśli będziesz kontynuować toodeploy więcej elementów NodeType z tylko kilka wystąpień, pogarsza się wraz z pobiera hello problem. Z tego powodu zaleca tego hello liczby węzłów w każdy typ węzła jest wielokrotnością liczby hello liczba domen błędów.

## <a name="upgrade-domains"></a>Domen uaktualnienia
Domeny uaktualnienia są kolejnej funkcji, która pomaga hello zasobu klastra sieci szkieletowej programu Service Manager zrozumieć układu hello hello klastra. Zestawy węzłów, które są uaktualniane na powitania Definiowanie domen uaktualnienia tym samym czasie. Informacje o uaktualnienia domen hello Pomoc Menedżera zasobów klastra i organizowania operacje zarządzania, takie jak uaktualnienia.

Domen uaktualnienia są znacznie, takich jak domen błędów, jednak z kilku podstawowych różnic. Najpierw obszarów awarie sprzętowe skoordynowanego Definiowanie domen błędów. Uaktualnienia domen, na hello drugiej strony, są zdefiniowane przez zasady. Pobierz toodecide ile mają, zamiast go dyktowanie hello środowisko. Może mieć dowolną liczbę domen uaktualnienia, jak węzłów. Inna różnica między domenach awarii i uaktualniania domen jest uaktualnienia domen nie są hierarchicznej. Zamiast tego są one bardziej przypominają prostych tagów. 

Hello Poniższy diagram przedstawia trzy domen uaktualnienia są rozkładane na trzy domen błędów. Przedstawia on także jeden możliwe umieszczania dla trzech różnych repliki usługi stanowej, gdzie każdy kończy się w różnych usterek i domen uaktualnienia. Ta umieszczania umożliwia hello utraty domeny błędów w hello środka uaktualnieniu usługi i jeszcze jedna kopia hello kodu i danych.  

<center>
![Umieszczanie o domenach awarii i uaktualniania][Image3]
</center>

Brak zalet i wad toohaving dużej liczby domen uaktualnienia. Więcej domen uaktualnienia oznacza, że każdy krok uaktualniania hello jest bardziej szczegółowe i w związku z tym wpływa na mniejszą liczbę węzłów lub usług. W związku z tym usług mniej ma toomove jednocześnie, wprowadzenie do systemu hello mniejsza ilość danych churn. Zwykle niezawodności tooimprove, ponieważ jest mniejsza usługi hello wpływ jakikolwiek problem wprowadzone podczas uaktualnienia hello. Więcej domen uaktualnienia oznacza również wymagają mniej dostępne buforu na innych węzłach toohandle hello skutków hello uaktualnienie. Na przykład jeśli masz pięć domen uaktualnienia węzłów hello w każdym są Obsługa około 20% ruchu. Jeśli potrzebujesz tootake dół tej domeny uaktualnienia do uaktualnienia, aby obciążenie zwykle musi toogo innym. Ponieważ masz cztery pozostałe domeny uaktualnienia, każdy musi mieć miejsce na około 5% Całkowity ruch związany z hello. Więcej domen uaktualnienia oznacza, że należy mniej buforu hello węzłach klastra hello. Rozważmy na przykład, jeśli zamiast tego masz 10 domen uaktualnienia. W takim przypadku każdy UD czy tylko obsługiwał około 10% Całkowity ruch związany z hello. Podczas uaktualniania kroki do klastra hello, każdej domeny, będzie potrzebny tylko toohave miejsce na około 1.1% hello ruch związany z. Więcej domen uaktualnienia zwykle pozwalają toorun węzły na zwiększenie użycia, ponieważ należy pojemności mniejszej zastrzeżone. Witaj dotyczy to także domen błędów.  

Wadą Hello podwyższonego posiadanie wielu domen uaktualnienia jest, że uaktualnień często tootake dłużej. Sieć szkieletowa usług oczekuje krótkim czasie po zakończeniu uaktualnienia domeny i sprawdza przed rozpoczęciem powitalne tooupgrade kolejnego. Te opóźnienia włączyć wykrywanie problemów wprowadzone przez hello uaktualnienia, aby mogła być kontynuowana hello uaktualnienia. zależnościami Hello jest dopuszczalne, ponieważ uniemożliwia nieprawidłowych zmian w czasie wpływających na zbyt dużej ilości hello usługi.

Za mało domen uaktualnienia ma wiele ujemna efekty uboczne — podczas każdej poszczególne domeny uaktualnienia nie działa i uaktualniany duża część ogólną wydajność jest niedostępny. Na przykład jeśli masz tylko trzy domeny uaktualnienia są tworzone w dół około 1/3 ogólnej usługi lub wydajność klastra naraz. Jednocześnie o tak wiele usług w dół nie pożądane, ponieważ mają wystarczającą wydajność toohave w hello reszty obciążenie hello toohandle klastra. Obsługa tego buforu oznacza, że podczas normalnego działania te węzły są załadowane mniejsze niż w przeciwnym razie. Powoduje to zwiększenie kosztów hello uruchomienia usługi.

Brak nie rzeczywistych limit toohello całkowitą liczbę błędów lub domen uaktualnienia w środowisku lub ograniczeń jak zachodziły na siebie. Inaczej mówiąc, istnieje kilka typowych wzorców:

- Domena awarii oraz domen uaktualnienia mapowane 1:1
- Jedną domenę uaktualnienia na węzeł (fizycznych lub wirtualnych wystąpienie systemu operacyjnego)
- Model "rozłożone" lub "macierzy" gdzie hello błędów domen i domen uaktualnienia formularz macierzy z zwykle maszynami ukośne podziały hello w dół

<center>
![Błąd i układy domena uaktualnienia][Image4]
</center>

Istnieje nie najlepsze odpowiedzi które toochoose układu, każdy ma kilka zalet i wad. Na przykład hello 1FD:1UD model działa tooset proste. Hello jest najbliższe osób, które są używane do 1 domeny uaktualnień na węzeł modelu. Podczas uaktualniania każdego węzła jest aktualizowana niezależnie. Jest to podobne toohow małych zestawów maszyn zostały uaktualnione ręcznie w przeszłości hello. 

najbardziej typowe model Hello jest hello FD/UD macierzy, gdzie hello FDs i UDs tabeli i węzły są umieszczane uruchamianie wzdłuż hello ukośnych. To jest model hello używany domyślnie w klastrach usługi sieć szkieletowa na platformie Azure. W przypadku klastrów z węzłami wiele wszystko, co kończy się wyszukiwanie like wzór dense macierzy hello powyżej.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Ograniczenia usterek i domeny uaktualnienia i efekty
Witaj Menedżera zasobów klastra traktuje desire hello tookeep usługi równoważone awarii i uaktualniania domeny jako ograniczenia. Można znaleźć więcej informacji na temat ograniczeń [w tym artykule](service-fabric-cluster-resource-manager-management-integration.md). Witaj usterek i domeny uaktualnienia stanu ograniczenia: "dla partycji dana usługa nigdy nie należy różnica *więcej niż jeden* hello wiele obiektów usługi (wystąpień usługi bezstanowej lub usługi stanowej repliki) między dwiema domenami." Zapobiega to niektórych przenosi lub zasady, które naruszają to ograniczenie.

Oto przykład. Załóżmy, że mamy klastra z sześciu węzłów skonfigurowany z pięciu domen błędów i pięć domen uaktualnienia.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Teraz załóżmy, że firma Microsoft Tworzenie usługi z TargetReplicaSetSize (lub dla usługi bezstanowej jako wartość InstanceCount) pięć. Witaj replik ziemi na N1 N5. W rzeczywistości N6 nie jest nigdy używane niezależnie od tego, ile usługi, takie jak ta, którą utworzysz. Ale Dlaczego? Przyjrzyjmy się hello różnica między hello bieżący układ i co się stanie, jeśli wybrano opcję N6.

Oto układu hello firma Microsoft uzyskano i hello całkowitej liczby replik na usterek i domeny uaktualnienia:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Ten układ jest równoważony pod względem węzłów na domenie błędów i domeny uaktualnienia. Jest również ze zrównoważonym pod względem hello liczby replik na usterek i domeny uaktualnienia. Każda domena ma hello tej samej liczby węzłów i hello tej samej liczby replik.

Teraz Przyjrzyjmy się co się stanie, jeśli ma użyliśmy N6 zamiast N2. Jak będzie replik hello rozdzielona następnie?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Ten układ narusza naszych definicji hello ograniczenia domeny błędów. FD0 ma dwie repliki podczas FD1 ma wartość 0, wprowadzania hello rozróżnia FD0 i FD1 całkowitej liczby dwa. Witaj Menedżera zasobów klastra nie zezwala na to rozmieszczenie. Podobnie jeśli mamy pobrane N2 i N6 (zamiast N1, jak i N2) możemy uzyskać:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Ten układ jest równoważony pod względem domen błędów. Jednak obecnie go narusza ograniczenie domeny uaktualnienia hello. Jest to spowodowane UD0 nie zero replik UD1 ma dwa. W związku z tym ten układ również jest nieprawidłowy i nie można pobrać przez hello Menedżera zasobów klastra. 

## <a name="configuring-fault-and-upgrade-domains"></a>Konfigurowanie usterek i domen uaktualnienia
Definiowanie domen błędów i uaktualnienia domeny odbywa się automatycznie w Azure obsługiwane wdrożenia usługi sieć szkieletowa usług. Sieć szkieletowa usług przejmuje i używa informacji o środowisku hello z platformy Azure.

Jeśli tworzenia własnego klastra (lub mają toorun określonego topologii w rozwoju) możesz podać informacje o domenie błędów i domeny uaktualnienia hello samodzielnie. W tym przykładzie definiujemy dziewięć węzła lokalnego klastra projektowego obejmującej trzy "centrów danych" (każdy z trzech stojakami). Ten klaster ma również trzy domeny uaktualnienia rozłożone na tych trzech centrów danych. Przykład Witaj konfiguracji znajduje się poniżej: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

za pomocą pliku ClusterConfig.json we wdrożeniach autonomicznych

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Podczas definiowania klastrów za pomocą usługi Azure Resource Manager, domenach awarii i uaktualniania domeny są przypisywane przez platformę Azure. W związku z tym definicja hello typy węzłów i zestawy skalowania maszyny wirtualnej w szablonie usługi Azure Resource Manager nie obejmuje domena awarii lub uaktualnienia domeny.
>

## <a name="node-properties-and-placement-constraints"></a>Właściwości węzła i ograniczenia dotyczące umieszczania
Czasami (w rzeczywistości w większości przypadków hello), który ma tooensure toowant, który niektórych obciążeń Uruchom tylko dla niektórych typów węzłów w klastrze hello. Na przykład niektóre obciążenie może wymagać GPU lub dyski SSD, a niektóre nie. Doskonałe przykład docelowych obciążeń tooparticular sprzętu jest niemal każdego tam n warstwowa architektury. Niektórych maszyn i służyć jako hello frontonu lub interfejsu API obsługujący strony aplikacji hello są uwidocznione toohello klientów lub hello internet. Różnych maszynach, często z zasoby sprzętowe obsługi zadań hello hello warstw obliczeń lub magazynu. Są to zazwyczaj _nie_ bezpośrednio widoczne tooclients lub hello internet. Sieci szkieletowej usług oczekuje, że istnieją przypadki, w której obciążeń w szczególności muszą toorun w konfiguracjach konkretnego sprzętu. Na przykład:

* istniejącą aplikację n warstwowa został "unosiło i przesunięte" w środowisku sieci szkieletowej usług
* Obciążenie potrzebuje toorun na temat sprzętu dla wydajności, skala lub ze względów bezpieczeństwa izolacji
* Obciążenia powinna zostać odizolowana od innych obciążeń powodów przez zasady lub zasobów

Usługi konfiguracji, tego rodzaju toosupport pierwszej klasie pojęcie tagi, które mogą być zastosowane toonodes ma sieci szkieletowej. Tagi te są nazywane **— właściwości węzła**. **Ograniczenia dotyczące umieszczania** są instrukcje hello dołączony tooindividual usług, które wybierz dla co najmniej jednej właściwości węzła. Ograniczenia dotyczące umieszczania zdefiniować, gdzie mają być uruchamiane usługi. zestaw ograniczeń Hello jest otwarty — wszystkie pary klucz/wartość można pracować. 

<center>
![Układ różnych obciążeń klastra][Image5]
</center>

### <a name="built-in-node-properties"></a>Wbudowane właściwości węzła
Sieć szkieletowa usług definiuje właściwości węzła niektóre domyślne, które mogą być używane automatycznie bez hello użytkownika mającego toodefine je. Witaj domyślne właściwości zdefiniowane w każdym węźle to hello **NodeType** i hello **NodeName**. Tak na przykład można zapisać jako ograniczenia umieszczania `"(NodeType == NodeType03)"`. Ogólnie rzecz biorąc znaleźliśmy NodeType toobe jedna z właściwości hello najczęściej używane. Jest przydatne, ponieważ odpowiada ona 1:1 z typem maszyny. Każdy typ maszyny odpowiada tooa typu obciążenia w tradycyjny n poziomowej aplikacji.

<center>
![Ograniczenia dotyczące umieszczania i właściwości węzła][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Ograniczenia umieszczania i składni właściwości węzła 
wartość Hello określony we właściwości węzła hello może być typu string, bool, lub podpisany za długo. Instrukcja Hello usługa hello jest nazywany położenia *ograniczenia* ponieważ ogranicza, gdzie hello usługa może zostać uruchomiona w klastrze hello. ograniczenie Hello można wszystkie logiczne instrukcji, która działa na powitania właściwości innego węzła w klastrze hello. selektory prawidłowy Hello w tych instrukcjach logiczne są:

1) warunkowe sprawdza, czy tworzenie konkretnego instrukcje

| — Instrukcja | Składnia |
| --- |:---:|
| "równe" | "==" |
| "nie równa się" | "!=" |
| "większe niż" | ">" |
| "większe lub równe" | ">=" |
| "mniejsze niż" | "<" |
| "mniejsze niż lub równe" | "<=" |

2) wartość logiczna instrukcje dla operacji grupowania i logicznych

| — Instrukcja | Składnia |
| --- |:---:|
| "i" | "&&" |
| "lub" | "&#124;&#124;" |
| "nie" | "!" |
| "grupy jako pojedynczej instrukcji" | "()" |

Oto kilka przykładów podstawowy warunek ograniczający instrukcji.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Tylko węzły, w którym hello ogólne instrukcji ograniczenia umieszczania ocenia zbyt "True" może mieć usługi hello umieścić na nim. Węzły, które nie mają właściwość zdefiniowaną są niezgodne z wszystkich ograniczeń umieszczania zawierającą tej właściwości.

Załóżmy, że hello następującego węzła, które właściwości zostały zdefiniowane dla typu węzła:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów. 

> [!NOTE]
> W węźle hello szablonu usługi Azure Resource Manager jest zwykle parametry typu. Jego wygląd "[parameters('vmNodeType1Name')]" zamiast "NodeType01".
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

Można utworzyć usługi umieszczania *ograniczenia* usług, takich jak następujące:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Jeśli wszystkie węzły NodeType01 są prawidłowe, możesz też wybrać ten typ węzła z ograniczeniem hello "(NodeType == NodeType01)".

Jest z hello chłodnych czynności dotyczących ograniczenia umieszczania usług, że mogą być aktualizowane dynamicznie w czasie wykonywania. Dlatego jeśli zajdzie potrzeba, można przenosić usługi klastrowania hello, dodawać i usuwać wymagania, np. Sieć szkieletowa usług odpowiada on za zapewnienie, że usługa hello pozostaje w górę i dostępne nawet wtedy, gdy tego rodzaju zmiany zostały wprowadzone.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Środowiska PowerShell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Ograniczenia dotyczące umieszczania są określone dla każdego wystąpienia usługi o nazwie innej. Zawsze przeprowadzać aktualizacje hello z (Zastąp) co został wcześniej określony.

Definicja klastra Hello definiuje właściwości hello w węźle. Zmiana właściwości węzła wymaga uaktualnienia konfiguracji klastra. Uaktualnienie właściwości węzła wymaga tooreport toorestart każdego węzła dotyczy nowej właściwości. Te uaktualnienia stopniowego są zarządzane przez sieć szkieletowa usług.

## <a name="describing-and-managing-cluster-resources"></a>Opisu i zarządzanie zasobami klastra
Jedną z najważniejszych zadań żadnych orchestrator jest toohelp hello Zarządzanie zużycie zasobów w klastrze hello. Zarządzanie zasobami klastra może oznaczać kilka różnych rzeczy. Po pierwsze jest zapewnienie maszyny nie są przeciążone. Oznacza to, upewniając się, że maszyny nie są uruchomione usługi więcej niż ich może obsłużyć. Po drugie istnieje równoważenia i optymalizacji, czyli usług krytycznych toorunning wydajnie. Kosztu oferty usługi poufnych wprowadzenia ani wydajności nie może dopuścić toobe niektóre węzły gorących a inne zimnych. Węzły gorących prowadzić rywalizacji tooresource i pogorszenie wydajności i zimnych węzły reprezentują niewykorzystana zasobów i wyższe koszty. 

Sieć szkieletowa usług reprezentuje zasoby jako `Metrics`. Metryki są dowolnego zasobu logiczną lub fizyczną, które mają tooService toodescribe sieci szkieletowej. Przykłady metryki to np. "WorkQueueDepth" lub "MemoryInMb". Uzyskać informacji o zasoby fizyczne hello rządzących sieci szkieletowej usług w węzłach, zobacz [ładu zasobów](service-fabric-resource-governance.md). Aby uzyskać informacje na temat konfigurowania niestandardowych metryk i ich zastosowań, zobacz [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)

Metryki różnią się od ograniczenia rozmieszczanie i właściwości węzła. Właściwości węzła są statyczne deskryptorów hello w poszczególnych węzłach. Metryki opisano zasoby, które mają węzłów i że korzystać z usług uruchamianych w węźle. Właściwość węzła może być "HasSSD" i można ustawić tootrue, lub FAŁSZ. Witaj ilość dostępnego miejsca na tym dysków SSD i jaka jest używane przez usługi będą metrykę, takie jak "DriveSpaceInMb". 

Jest ważne toonote, który podobnie jak ograniczenia dotyczące umieszczania i właściwości węzła hello zasobu klastra sieci szkieletowej programu Service Manager nie zrozumieć, jakie nazwy hello hello metryki średniej. Nazwy metryki są tylko ciągi. Należy dobrze toodeclare jednostki jako część nazwy metryki hello, które są tworzone podczas może być niejednoznaczna.

## <a name="capacity"></a>Pojemność
Jeśli wyłączysz wszystkich zasobów *równoważenia*, Menedżer zasobów klastra usługi sieć szkieletowa będzie nadal upewnij się, że żaden węzeł nie zakończył za pośrednictwem jego pojemność. Zarządzanie przepełnienia pojemności jest możliwa, chyba że klaster hello jest zapełniony lub obciążenia hello jest większy niż dowolnego węzła. Pojemność jest inny *ograniczenia* tego hello Menedżera zasobów klastra używa toounderstand ilości zasobów, a węzeł ma. Pozostała pojemność jest również śledzona hello klastra jako całość. Zarówno hello pojemności, jak i zużycia hello na poziomie usługi hello są wyrażone w metryki. Tak na przykład metryka hello może być "ClientConnections" i podany węzeł może mieć pojemność "ClientConnections" z 32768. Inne węzły mogą mieć inne ograniczenia niektórych usługa jest uruchomiona w tym może węzła powiedz go obecnie zajmuje 32256 hello metryki "ClientConnections".

W czasie wykonywania hello Menedżera zasobów klastra śledzi pozostałe zasoby w klastrze hello i na węzłach. W kolejności tootrack hello pojemności Menedżera zasobów klastra odejmuje użycia każdej usługi, z którym jest uruchomiona usługa hello pojemność węzła. Dzięki tym informacjom hello zasobu klastra sieci szkieletowej programu Service Manager można dowiedzieć się, gdzie tooplace lub przenieść repliki tak, aby węzły nie przekazywane pojemności.

<center>
![Węzły klastra i pojemności][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Możesz sprawdzić możliwości zdefiniowane w manifeście klastra hello:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

Zazwyczaj usługa załadować zmiany dynamicznie. Załóżmy, że obciążenie repliki "ClientConnections" zmieniła się z 1024 too2048, ale węzła hello była uruchomiona na następnie tylko była dostępna dla tej metryki wydajność 512. Teraz ta replika lub położenia wystąpienia jest nieprawidłowa, ponieważ nie ma wystarczającej ilości miejsca, w tym węźle. Witaj Menedżera zasobów klastra ma tookick w i uzyskać węzła hello niż pojemność. Zmniejsza obciążenie hello węzeł, który znajduje się nad pojemności przenosząc przynajmniej jednej z replik hello lub wystąpień z węzłów tooother tego węzła. Podczas przenoszenia replik, hello Menedżera zasobów klastra próbuje koszt hello toominimize tych przepływów. Koszt przeniesienia została szczegółowo opisana w [w tym artykule](service-fabric-cluster-resource-manager-movement-cost.md) i bardziej o hello Menedżera zasobów klastra na ponowne równoważenie strategie i opisano reguły [tutaj](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Pojemność klastra
W jaki sposób hello ogólną hello keep Menedżera zasobów klastra sieci szkieletowej usług klastra jest zapełniony? Również z dynamicznego obciążenia nie istnieje wiele go wykonać. Usługi mogą mieć ich kolekcji obciążenia niezależnie od akcje wykonywane przez hello Menedżera zasobów klastra. W związku z tym klastra za pomocą szerokie możliwości rozbudowy dzisiaj może być za słaby, gdy stanie się Słynne jutro. Inaczej mówiąc, brak niektórych formantów, które są rozszerzania tooprevent problemy. Witaj najpierw możemy jest zapobiec hello tworzeniu nowych obciążeń, które mogłoby spowodować pełne toobecome klastra hello.

Powiedz tworzenia usługi bezstanowej, a ma niektóre obciążenia skojarzone z nim. Załóżmy, że usługa hello dba o metryki "DiskSpaceInMb" hello. Załóżmy również, że jest będzie tooconsume pięciu jednostek "DiskSpaceInMb" dla każdego wystąpienia usługi hello. Ma trzy wystąpienia usługi hello toocreate. Wspaniale! Tak, aby oznacza, że potrzebujemy 15 jednostek toobe "DiskSpaceInMb" istnieje w klastrze hello abyśmy tooeven być stanie toocreate wystąpień tych usług. Hello Menedżera zasobów klastra stale oblicza hello pojemność i użycie wszystkie metryki, dzięki czemu można określić hello pojemności pozostałych w klastrze hello. Jeśli nie ma wystarczającej ilości miejsca, wywołanie usługi tworzenia hello hello odrzuca Menedżera zasobów klastra.

Ponieważ wymaganie hello jest tylko być dostępne jednostki 15, ten obszar może zostać przydzielony wiele różnych sposobów. Przykładowo może istnieć pozostałe jednostki pojemności w różnych węzłach 15 lub trzy pozostałe jednostki pojemności w pięciu różnych węzłach. Jeśli hello Menedżera zasobów klastra można rozmieszczanie rzeczy, dlatego na trzy węzły jest dostępna pięciu jednostek, umieszcza hello usługi. Zmienianie rozmieszczenia klastra hello jest zwykle możliwe, chyba że klastra hello jest prawie pełna lub hello istniejących usług nie mogą być konsolidowane jakiegoś powodu.

## <a name="buffered-capacity"></a>Buforowany pojemności
Pojemność buforowany jest inna funkcja hello Menedżera zasobów klastra. Umożliwia rezerwacji część hello ogólną pojemność węzła. Ten bufor pojemności jest usług tooplace używane tylko podczas uaktualniania i awarii węzła. Globalny określony buforowanego pojemności na metryki dla wszystkich węzłów. Wybierz pojemności hello zastrzeżone wartości Hello jest funkcją hello liczby awarii i domen uaktualnienia w klastrze hello. Więcej awarii i uaktualniania domeny oznacza, że z buforowanego pojemności może wybrać mniejszą liczbę. Jeśli masz więcej domen, można oczekiwać, że mniejszych ilości toobe Twojego klastra niedostępne podczas uaktualniania i awarii. Określanie buforowane pojemności ma sens tylko jeśli masz także hello określonego węzła wydajności dla metryki.

Poniżej przedstawiono przykład sposobu toospecify buforowane pojemności:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

za pomocą pliku ClusterConfig.json dla autonomicznych wdrożeniach lub Template.json dla platformy Azure hostowanej klastrów:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

Witaj tworzenia nowych usług nie powiedzie się, gdy hello klastra jest poza buforowanego wydajności dla metryki. Zapobieganie hello tworzenia nowych usług toopreserve hello buforu zapewnia, że błędy i uaktualnienia nie spowodują toogo węzłów przeciążone. Pojemność buforowany jest opcjonalne, ale jest zalecane w przypadku dowolnego klastra, który definiuje wydajności dla metryki.

Witaj Menedżera zasobów klastra uwidacznia informacje dotyczące tego obciążenia. Dla każdego metryki informacje te obejmują: 
  - Witaj buforowane ustawień możliwości
  - łączna pojemność Hello
  - Bieżące użycie Hello
  - Określa, czy jest uznawany za wszystkie metryki równoważenia lub nie
  - Statystyka hello odchylenie standardowe
  - Witaj węzły, które mają hello większość i najmniejszego obciążenia  
  
Poniżej przedstawiono przykład te dane wyjściowe:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać informacje dotyczące architektury i informacje przepływu hello w hello Menedżera zasobów klastra, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-architecture.md)
* Definiowanie metryki defragmentacji jest jednym ze sposobów tooconsolidate obciążenie węzłów zamiast go rozkładanie. toolearn jak tooconfigure defragmentacji, zapoznaj się zbyt[w tym artykule](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)
* toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
