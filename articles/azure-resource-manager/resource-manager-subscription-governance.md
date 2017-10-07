---
title: "aaaBest rozwiązania dla przedsiębiorstw przenoszenie tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano szkieletu przedsiębiorstwa za pomocą tooensure bezpieczne i łatwe w zarządzaniu środowisko."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Szkieletu Azure enterprise — ładu przetestowanego subskrypcji
Przedsiębiorstwa są coraz bardziej przyjmowanie hello chmury publicznej, elastyczność i elastyczność. One są przy użyciu chmury hello sile toogenerate przychodu lub optymalizacji zasobów dla firm hello. Microsoft Azure udostępnia wiele różnych usług czy przedsiębiorstwa można grupować jak tooaddress bloków konstrukcyjnych szerokiej gamy obciążeń i aplikacji. 

Ale wiedząc, gdzie toobegin często jest trudne. Po podjęciu decyzji toouse Azure, często wystąpić na kilka pytań:

* "Jak spełniają naszych wymagania prawne suwerenności danych w niektórych krajach?"
* "Jak zapewnić, że ktoś nie mogą przypadkowo zmieniają krytyczne systemu?"
* "Jak sprawdzić, co każdy zasób obsługuje tak może I uwzględnić go i Utwórz kopię dokładnie rachunku?"

Perspektywa Hello pusty subskrypcji z nie szyny guard jest czasochłonnym zadaniem. Ta puste miejsce mogą utrudniać tooAzure Twojego przenoszenia.

Ten artykuł zawiera punkt początkowy dla specjalistów tooaddress hello konieczność zarządzania i saldo za pomocą hello potrzebę elastyczność. Podaj hello koncepcji szkieletu przedsiębiorstwa, który przeprowadzi organizacji w wdrażanie i zarządzanie nim swoje subskrypcje platformy Azure. 

## <a name="need-for-governance"></a>Potrzebę ładu
Podczas przenoszenia tooAzure, muszą spełnić hello tematem Zarządzanie wczesnego tooensure hello skuteczne użycie chmury hello w obrębie przedsiębiorstwa hello. Niestety czas hello i biurokracji tworzenia systemu kompleksowe zarządzanie oznacza, że niektóre grup biznesowych przejdź bezpośrednio toovendors nie angażując rozwiązaniami INFORMATYCZNYMI dla firm. Takie podejście może pozostać toovulnerabilities Otwórz hello przedsiębiorstwa, jeśli hello zasobów nie są właściwie zarządzane. Właściwości chmury publicznej hello elastyczności, elastyczność i wyceny opartej na zużycie — Hello są istotne toobusiness grup, które wymagają tooquickly spełnienia wymagań hello klientów (wewnętrznych i zewnętrznych). Jednak przedsiębiorstwa IT musi tooensure skutecznie chronionych danych i systemów.

W świecie rzeczywistym szkieletów stanowi podstawę hello używane toocreate hello struktury. szkieletu Hello przeprowadzi postać ogólną hello i zapewnia bardziej trwałego toobe systemy zainstalowane punktów kontrolnych. Szkieletu przedsiębiorstwa jest sama hello: zestaw elastyczne opcje kontroli i funkcji platformy Azure, zawierających środowiska toohello struktury i kotwice usług oparty na powitania chmury publicznej. Zapewnia hello konstruktorów (IT i grup biznesowych) foundation toocreate i Dołącz nowe usługi.

szkieletu Hello jest oparta na rozwiązania, które firma Microsoft zostały zebrane z wielu korzystają z klientami o różnych rozmiarach. Tych klientów w zakresie od małe firmy tworzenia rozwiązań w hello chmury tooFortune 500 przedsiębiorstwa i niezależnym dostawcom oprogramowania migracji i projektowania rozwiązań w chmurze hello. Witaj szkieletu przedsiębiorstwa jest elastyczny toosupport toobe "dedykowanym" zarówno w przypadku tradycyjnych obciążeń IT, jak i obciążeń agile; takie jak deweloperom tworzenie aplikacji oprogramowania — jako — usługa (SaaS) są oparte na funkcji platformy Azure.

szkieletu enterprise Hello jest toobe zamierzonej foundation hello każdej nowej subskrypcji w ramach platformy Azure. Umożliwia on Administratorzy tooensure obciążeń hello spełniają minimalne ładu wymagań organizacji bez uniemożliwia grup biznesowych i deweloperom szybkie osiągnięcia własnych celów.

> [!IMPORTANT]
> Zarządzanie jest istotne toohello Powodzenie Azure. Cele tego artykułu hello implementacji technicznej szkieletu przedsiębiorstwa, ale tylko dotyka na powitania szerszego procesu i relacje między składnikami hello. Zasady zarządzania wypływających z góry hello w dół i jest określany przez jaki hello firm chce tooachieve. Oczywiście hello tworzenia modelu ładu dla platformy Azure obejmuje przedstawicieli IT, ale co ważniejsze powinien mieć silne reprezentacja z liderów grupy biznesowej oraz zabezpieczeń i zarządzanie ryzykiem. W celu hello szkieletu przedsiębiorstwa jest o ograniczaniu toofacilitate ryzyka firm misji i celów organizacji.
> 
> 

powitania po obrazu w tym artykule opisano składniki hello szkieletu hello. Hello foundation polega na stałe planu dla działów, konta i subskrypcji. słupków Hello składają się z zasad Menedżera zasobów i silne Standardy nazewnictwa. Hello reszty szkieletu hello funkcjach tej Włącz bezpieczne i łatwe w zarządzaniu środowisko i pochodzi z podstawowych funkcji platformy Azure.

![składniki szkieletu](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure szybko zwiększył się od czasu jego wprowadzenia 2008. Rozwój tego wymaganego Microsoft engineering zespoły toorethink ich podejście do zarządzania i wdrażania usług. model usługi Azure Resource Manager Hello został wprowadzony w 2014 i zastępuje hello klasycznego modelu wdrażania. Menedżer zasobów pozwala organizacjom toomore łatwe wdrażanie, organizować i kontrolowania zasobów platformy Azure. Menedżer zasobów zawiera paralelizacja podczas tworzenia zasobów dla szybsze wdrażanie złożonych, współzależne rozwiązań. Zawiera także precyzyjną kontrolę dostępu i hello możliwości tootag zasobów przy użyciu metadanych. Firma Microsoft zaleca utworzenie wszystkich zasobów za pomocą modelu usługi Resource Manager hello. Witaj enterprise szkieletu jawnie jest przeznaczona dla hello modelu Resource Manager.
> 
> 

## <a name="define-your-hierarchy"></a>Zdefiniuj hierarchii
podstawę Hello szkieletu hello jest rejestracja Enterprise Azure hello (i hello Enterprise Portal). Rejestracja enterprise Hello określa kształt hello i korzystają z usług Azure w obrębie firmy oraz strukturę zarządu hello core. W ramach umowy enterprise agreement hello, klienci są w stanie toofurther podzielić hello środowiska do działów, kont, a na końcu subskrypcji. Subskrypcja platformy Azure to podstawowa jednostka hello, gdzie znajdują się wszystkie zasoby. Definiuje również kilka ograniczeń w obrębie platformy Azure, takich jak liczba rdzeni, zasoby itd.

![Hierarchii](./media/resource-manager-subscription-governance/agreement.png)

Co przedsiębiorstwa jest inna i hello hierarchii w poprzedniej ilustracji hello umożliwia dużą swobodę w sposób organizowania Azure w ramach hello firmy. Przed wdrożeniem hello wskazówki zawarte w tym dokumencie, możesz modelu hierarchii i zrozumieć wpływ hello na rozliczenia, dostęp do zasobów i złożoności.

Hello trzy wspólne wzorce dla rejestracji Azure są:

* Witaj **funkcjonalności** wzorca
  
    ![funkcjonalności](./media/resource-manager-subscription-governance/functional.png)
* Witaj **jednostki biznesowej** wzorca 
  
    ![firmy](./media/resource-manager-subscription-governance/business.png)
* Witaj **geograficzne** wzorca
  
    ![geograficzne](./media/resource-manager-subscription-governance/geographic.png)

Należy zastosować szkieletu hello na powitania subskrypcji poziomu tooextend hello wymagania ładu dotyczące hello Enterprise do subskrypcji hello.

## <a name="naming-standards"></a>Standardy nazewnictwa
pierwszy słupka Hello z szkieletu hello jest nazewnictwa standardów. Dobrze zaprojektowanego Standardy nazewnictwa Włącz tooidentify zasobów w portalu hello na rachunek i w ramach skryptów. Prawdopodobnie już nazewnictwo standardy dotyczące infrastruktury lokalnej. Podczas dodawania środowiska Azure tooyour, powinny rozszerzać tych nazw tooyour standardów zasobów platformy Azure. Standard nazewnictwa ułatwienia bardziej efektywne zarządzanie środowiskiem hello na wszystkich poziomach.

> [!TIP]
> Dla konwencji nazewnictwa:
> * Przejrzyj i przyjęcie w miarę możliwości hello [wskazówki Patterns and Practices](../guidance/guidance-naming-conventions.md). W tych wskazówkach ułatwia podejmowanie decyzji o znaczący standard nazewnictwa.
> * Użyj camelCasing dla nazw zasobów (takich jak myResourceGroup i vnetNetworkName). Uwaga: Dostępne są niektóre zasoby, takie jak kont magazynu, gdzie opcją tylko hello jest toouse małe litery (i innych znaków specjalnych).
> * Należy rozważyć użycie usługi Azure Resource Manager (opisany w następnej sekcji hello) zasady tooenforce standardami nazewnictwa.
> 
> Witaj poprzedniego wskazówki ułatwiające implementację spójnej konwencji nazewnictwa.

## <a name="policies-and-auditing"></a>Zasady i inspekcji
drugi słupka Hello z szkieletu hello obejmuje utworzenie [zasady usługi Azure Resource Manager](resource-manager-policy.md) i [inspekcji dziennik aktywności hello](resource-group-audit.md). Zasady usługi Resource Manager zapewniają ryzyka toomanage możliwości hello na platformie Azure. Można zdefiniować zasady, zapewniając suwerenności danych przez ograniczenie, wymuszanie lub inspekcji pewne akcje. 

* Zasada jest domyślnie **Zezwalaj** systemu. Kontrolowanie akcji przy definiowanie i przypisywanie tooresources zasady, odmowa lub inspekcję akcji na zasobach.
* Zasady są opisane w definicjach zasad w języku definicji zasad (warunki, jeżeli to).
* Możesz utworzyć zasady z JSON (Javascript Object Notation) sformatowany plików. Po zdefiniowaniu zasad, należy przypisać mu określonego zakresu tooa: zasobu, grupy zasobów lub subskrypcji.

Zasady mają wiele akcji, które umożliwiają scenariusze tooyour podejście szczegółowych. dostępne są następujące akcje Hello:

* **Odmów**: żądanie zasobu hello bloków
* **Inspekcji**: umożliwia żądania hello ale dodaje dziennik aktywności toohello wiersza, (która może być używane tooprovide alertów lub elementy runbook tootrigger)
* **Dołącz**: dodaje określony zasób toohello informacji. Na przykład jeśli do zasobu nie jest tag "CostCenter", należy dodać tagu z wartością domyślną.

### <a name="common-uses-of-resource-manager-policies"></a>Najczęstsze zastosowania zasad Menedżera zasobów
Zasady usługi Azure Resource Manager są zaawansowane narzędzie w hello Azure toolkit. Umożliwiają one tooavoid nieoczekiwany kosztów, tooidentify koszt Centrum dla zasobów za pomocą znakowania i tooensure zgodności, że zostały spełnione wymagania. Gdy zasady są połączone z hello wbudowane funkcje inspekcji, możesz fashion złożone i elastycznych rozwiązań. Zasady pozwalają firm formanty tooprovide obciążeń "Tradycyjnych IT" i "Agile" obciążenia; takie jak tworzenie aplikacji klienta. są Hello najbardziej typowych wzorców, które przedstawiono w zasadach:

* **Suwerenności danych geograficznie zgodności** — platforma Azure udostępnia regionów między hello world. Przedsiębiorstwa często mają toocontrol, gdy zasoby są tworzone (czy tooensure danych suwerenności lub po prostu tooensure zasoby są tworzone użytkowników końcowych toohello Zamknij hello zasobów).
* **Koszt zarządzania** -subskrypcji platformy Azure może obejmować zasoby wiele typów i skali. Firmy często mają tooensure standardzie subskrypcje unikać niepotrzebnie zasoby, które mogą kosztem setki kwoty miesiąc lub więcej.
* **Domyślna ładu za pomocą wymaganych tagów** -wymagające tagów jest jednym z hello najbardziej typowe i wysoce żądanej funkcji. Za pomocą usługi Azure Resource Manager zasad przedsiębiorstwa mają tooensure możliwe, że zasób jest odpowiednio oznakowane. Witaj najbardziej typowe tagi są: działu, właściciel zasobu i środowisko typu (na przykład - produkcji, testu, rozwoju)

**Przykłady**

"Tradycyjnych IT" subskrypcji dla aplikacji biznesowych z

* Właściciel znaczniki wszystkich zasobów i wymusić dział
* Ograniczenia zasobów tworzenia toohello w Ameryce Północnej, regionie
* Ograniczanie hello możliwości toocreate G serii maszyn wirtualnych i klastry usługi HDInsight

Środowisko "Agile" dla jednostki biznesowej, tworzenie aplikacji w chmurze

* wymagania suwerenności danych toomeet, Zezwalaj na tworzenie hello zasobów tylko w określonym regionie.
* Wymuś tag środowiska wszystkich zasobów. Jeśli zasób jest tworzona bez tagu, Dołącz hello **środowiska: nieznany** tagu toohello zasobów.
* Inspekcja, gdy zasoby są tworzone poza Ameryce Północnej, ale nie uniemożliwiają.
* Inspekcja podczas tworzenia zasobów wysokich kosztów.

> [!TIP]
> Witaj najczęściej zasad Menedżera zasobów między organizacjami jest toocontrol *gdzie* zasoby mogą być tworzone i *co* typów zasobów, które mogą być tworzone. Ponadto tooproviding formantów na *gdzie* i *co*, toobill odpowiednie metadane hello wstecz do użycia przez ma wiele przedsiębiorstw użycia zasad tooensure zasobów. Firma Microsoft zaleca stosowanie zasad na poziomie subskrypcji hello:
> 
> * Suwerenności danych geograficznie zgodności
> * Zarządzanie kosztami
> * Wymagane tagi (powodowane potrzeb biznesowych, takich jak adres rachunku, właściciel aplikacji)
> 
> Można zastosować dodatkowe zasady na niższych poziomach zakresu.
> 
> 

### <a name="audit---what-happened"></a>Inspekcji - co się stało?
jak działa środowisko tooview, należy tooaudit aktywności użytkownika. Większość typów zasobów w systemie Azure utworzyć dzienników diagnostycznych, które można analizować przy użyciu narzędzia dziennika lub w usłudze Azure Operations Management Suite. Możesz zbierać Dzienniki aktywności w wielu działów tooprovide subskrypcji lub widok przedsiębiorstwa. Rekordy inspekcji są zarówno ważne narzędzie diagnostyczne kluczową rolę mechanizmu tootrigger zdarzeń i w hello środowiska platformy Azure.

Dzienniki aktywności z wdrożenia usługi Resource Manager Włącz toodetermine hello **operacji** które miało miejsce i kto wykonał. Dzienniki aktywności mogą być zbierane i zagregowane za pomocą narzędzi takich jak analizy dzienników.

## <a name="resource-tags"></a>Tagi zasobów
Jak użytkownicy w Twojej organizacji Dodaj subskrypcję toohello zasobów, staje się coraz bardziej ważne tooassociate zasoby z hello odpowiednie dział, klientów i środowisko. Możesz dołączyć tooresources metadanych za pośrednictwem [tagi](resource-group-using-tags.md). Możesz użyć tagów tooprovide informacje dotyczące zasobów hello lub hello właściciela. Znaczniki umożliwiają toonot tylko agregacji i grupy zasobów na różne sposoby, ale użyć tych danych na potrzeby hello obciążenia zwrotnego. Można oznaczyć zasoby z zapasowej too15 pary klucz: wartość. 

Tagi zasobów są elastyczne i powinien być dołączony toomost zasobów. Przykłady typowych tagi zasobów są:

* Adres rachunku
* Dział (lub jednostki biznesowej)
* Środowiska (Programowanie produkcji, etap)
* Warstwy (warstwa sieci Web, warstwy aplikacji)
* Właściciel aplikacji
* ProjectName

![tags](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Więcej przykładów tagów, zobacz [konwencje nazewnictwa dla zasobów platformy Azure zalecane](../guidance/guidance-naming-conventions.md).

> [!TIP]
> Należy rozważyć zmianę zasad, które ma znakowanie dla:
> 
> * Grupy zasobów
> * Magazyn
> * Maszyny wirtualne
> * Serwery środowisk/sieci web usługi aplikacji
> 
> Ta strategia znakowania identyfikuje wszystkich subskrypcji, jakie metadanych jest wymagany dla firm hello, not, zabezpieczeń, zarządzania ryzykiem i pełne zarządzanie środowiskiem hello. 

## <a name="resource-group"></a>Grupa zasobów
Menedżer zasobów umożliwia tooput zasobów w łatwy do rozpoznania grupy zarządzania, koligacji rozliczeń lub fizycznych. Jak wspomniano wcześniej, platforma Azure ma dwa modele wdrażania. W hello wcześniejszych modelu Klasyczny hello podstawową jednostką zarządzania było hello subskrypcji. Był trudny toobreak dół zasobów w ramach subskrypcji, które spowodowało utworzenie toohello dużą liczbę subskrypcji. Z modelu Resource Manager hello widzieliśmy wprowadzenie hello grup zasobów. Grupy zasobów to kontenery zasoby, które mają wspólne cykl lub udostępnić atrybut, taki jak "wszystkie serwery SQL" lub "Aplikacja A".

Grupy zasobów nie może być zawarty w sobie nawzajem i zasoby mogą należeć tylko tooone grupy zasobów. Pewne akcje można stosować na wszystkie zasoby w grupie zasobów. Na przykład usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów hello. Zwykle, umieść całą aplikację lub powiązane system w hello tej samej grupie zasobów. Na przykład aplikacji trzy warstwy o nazwie aplikacji sieci Web firmy Contoso zawierałoby powitania serwera sieci web, serwera aplikacji i programu SQL server w hello tej samej grupie zasobów.

> [!TIP]
> Sposób organizowania grup zasobów mogą się różnić od obciążeń "Tradycyjnych IT" za "Agile IT" obciążenia:
> 
> * "Tradycyjnych IT" obciążeń najczęściej są pogrupowane według elementów w obrębie hello sam cykl życia, takie jak aplikacja. Umożliwia grupowanie przez aplikację do zarządzania aplikacjami w poszczególnych.
> * "Agile IT" obciążeń często toofocus na aplikacje chmury zewnętrznej skierowane do klienta. grupy zasobów Hello powinien odzwierciedlać warstwy hello wdrożenia (na przykład warstwa sieci Web warstwy aplikacji) i zarządzania.
> 
> Opis obciążenie pomocne w opracowywaniu strategii grupy zasobów.

## <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach
Użytkownik prawdopodobnie prośbę o sobie "kto ma dostęp tooresources?" "jak kontrolować dostęp?" Stosowanie lub brak zezwolenia toohello dostęp do portalu Azure i kontrolowanie dostępu tooresources w portalu hello odgrywa kluczową rolę. 

Gdy Azure pierwotnie został wydany, dostęp do formantów tooa subskrypcji zostały podstawowe: administratorem ani Współadministratorem. Dostęp do subskrypcji tooa hello klasycznego modelu niejawnego dostępu tooall hello zasobów w portalu hello. Ten brak szczegółową kontrolę przeprowadzony toohello mnożenie tooprovide subskrypcje poziom kontroli dostępu uzasadnione rejestracji Azure.

Mnożenie tej subskrypcji nie jest już potrzebne. Przy użyciu kontroli dostępu opartej na rolach można przypisywać użytkowników ról toostandard (na przykład typowe "czytnika" i "writer" typy ról). Można również zdefiniować role niestandardowe.

> [!TIP]
> Kontrola dostępu oparta na rolach tooimplement:
> * Połącz swoją tożsamość firmy magazynu (najczęściej Active Directory) tooAzure usługi Active Directory przy użyciu hello narzędzie AD Connect.
> * Formant hello Admin/Współadministratora subskrypcji za pomocą tożsamości zarządzanych. **Nie** przypisać administratora/współadministratora tooa nowego właściciela subskrypcji. Zamiast tego należy użyć tooprovide role RBAC **właściciela** lub grupy tooa praw.
> * Dodaj grupę tooa Azure użytkownicy (na przykład właściciele X aplikacji) w usłudze Active Directory. Użyj hello zsynchronizowanej grupy tooprovide grupy członków hello odpowiednie prawa toomanage hello grupy zasobów zawierające aplikacji hello.
> * Postępuj zgodnie z zasadą hello przyznawania hello **najniższych uprawnień** hello wymagane toodo oczekiwano pracy. Na przykład:
>   * Grupa wdrożenia: Grupa, która jest tylko toodeploy stanie zasobów.
>   * : Maszyna wirtualna A Grupa zarządzania To znaczy maszyn wirtualnych mogli toorestart (dla operacji)
> 
> Te wskazówki ułatwiają zarządzanie dostępem użytkowników w Twojej subskrypcji.

## <a name="azure-resource-locks"></a>Blokad zasobów platformy Azure
Jak organizacji dodaje core services toohello subskrypcji, staje się coraz bardziej ważne tooensure, czy te usługi są dostępne tooavoid firm przerw w działaniu. [Blokowania zasobów](resource-group-lock-resources.md) pozwalają operacji toorestrict zasobów wysokiej wartości, których modyfikowania lub usuwania ich miałoby znaczący wpływ na aplikacje lub infrastruktury chmury. Możesz zastosować blokad tooa subskrypcji, grupy zasobów lub zasobów. Zazwyczaj należy zastosować blokad toofoundational zasoby, takie jak sieci wirtualnych, bramy i kont magazynu. 

Blokowania zasobów obsługuje obecnie dwie wartości: CanNotDelete i tylko do odczytu. CanNotDelete oznacza, że użytkownikom (hello odpowiednie prawa) można nadal odczytywać lub zmodyfikuj zasobu, ale nie można go usunąć. Tylko do odczytu oznacza, że autoryzowani użytkownicy nie można usunąć ani zmodyfikować zasobu.

toocreate lub usunięcia blokady zarządzania, należy mieć dostęp zbyt`Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje.
Witaj wbudowanych ról tylko właściciel i Administrator dostępu użytkowników są przyznawane te akcje.

> [!TIP]
> Opcje sieci podstawowej powinny być chronione przy użyciu blokad. Przypadkowego usunięcia Brama VPN lokacja lokacja będą Fatalne tooan subskrypcji platformy Azure. Azure nie zezwala toodelete sieci wirtualnej, który jest używany, ale stosowanie więcej ograniczeń, jest przydatne środki ostrożności. 
> 
> * Sieć wirtualna: CanNotDelete
> * Sieciowa grupa zabezpieczeń: CanNotDelete
> * Zasady: CanNotDelete
> 
> Zasady również są kluczowe toohello konserwacji właściwych kontroli. Firma Microsoft zaleca stosowanie **CanNotDelete** zablokować toopolices, które są używane.

## <a name="core-networking-resources"></a>Podstawowe zasoby sieciowe
Tooresources dostępu może być (w ramach sieci hello corporation) wewnętrznych lub zewnętrznych (za pośrednictwem Internetu hello). Przez użytkowników w organizacji zasobów put tooinadvertently w miejscu niewłaściwy hello i potencjalnie je otworzyć toomalicious dostępu. Podobnie jak w przypadku urządzeń lokalnych, przedsiębiorstwa należy dodać odpowiednie formanty tooensure czy użytkownicy Azure decyzje hello prawo. Zarządzanie subskrypcją nazywamy zasobów podstawowych, które zapewniają podstawowy kontrolę dostępu. Witaj core — zasoby obejmują:

* **Sieci wirtualne** obiektów kontenera podsieci. Chociaż nie niezbędne, często jest używana podczas łączenia zasobów firmowych toointernal aplikacji.
* **Sieciowe grupy zabezpieczeń** są podobne tooa zapory i reguł dla jak zasobu można "rozmawiać" hello sieci. Zapewniają szczegółową kontrolę nad jak / hello na takie same Jeśli podsieci (lub maszyny wirtualnej) można połączyć toohello Internet lub innych podsieci w sieci wirtualnej.

![Podstawowe operacje sieciowe](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Praca w sieci:
> * Utwórz dedykowane obciążeń tooexternal uwzględniającym sieci wirtualnych i wewnętrzny uwzględniającym obciążeń. Takie podejście zmniejsza ryzyko hello przypadkowo umieszczania maszyn wirtualnych, które są przeznaczone dla wewnętrznych obciążeń w zewnętrznych połączonej przestrzeni.
> * Skonfiguruj dostęp toolimit grup zabezpieczeń sieci. Co najmniej zablokować toohello dostęp do Internetu za pomocą wewnętrznej sieci wirtualnych i sieci firmowej toohello dostępu bloku z zewnętrzne sieci wirtualne.
> 
> Te wskazówki ułatwiające implementację zabezpieczania zasobów sieciowych.

### <a name="automation"></a>Automatyzacja
Zarządzanie zasobami indywidualnie jest czasochłonne i potencjalnie podatna dla niektórych operacji. Platforma Azure oferuje różne możliwości automatyzacji, w tym usługi Automatyzacja Azure Logic Apps i usługi Azure Functions. [Automatyzacja Azure](../automation/automation-intro.md) umożliwia administratorom toocreate oraz zdefiniowania elementów runbook toohandle typowych zadań zarządzania zasobami. Możesz utworzyć elementy runbook za pomocą edytora kodu programu PowerShell lub edytora graficznego. Służy do tworzenia złożonych wieloetapowym przepływów pracy. Automatyzacja Azure jest często używane toohandle typowych zadań, takich jak zamykanie nieużywanych zasobów lub tworzenia zasobów w odpowiedzi tooa określonego wyzwalacza bez udziału człowieka.

> [!TIP]
> Do automatyzacji:
> * Utwórz konto usługi Automatyzacja Azure i przejrzyj hello dostępne elementy runbook (zarówno graficznego i polecenia wiersza) dostępna w hello [galerię elementów Runbook](../automation/automation-runbook-gallery.md).
> * Importowanie i dostosować klucza elementów runbook na własny użytek.
> 
> Typowy scenariusz obejmuje maszyny wirtualne tooStart/Shutdown możliwości hello zgodnie z harmonogramem. Brak przykładowe elementy runbook, które są dostępne w galerii hello zarówno obsługi tego scenariusza i jak omawiające tooexpand go.
> 
> 

## <a name="azure-security-center"></a>Azure Security Center
Możliwe, że jedną z największych przyjęcia toocloud blockers hello została dotyczy hello za pośrednictwem zabezpieczeń. Kierownicy ryzyka i działu zabezpieczeń muszą tooensure czy zasobami na platformie Azure są bezpieczne. 

Witaj [Centrum zabezpieczeń Azure](../security-center/security-center-intro.md) udostępnia centralną widok hello stan zabezpieczeń zasobów w subskrypcji hello i zawiera zalecenia, które ułatwiają ochronę zasobów ze złamanymi zabezpieczeniami. Bardziej szczegółowe zasady (na przykład stosowania zasad toospecific grupy zasobów, które umożliwia hello enterprise tootailor ich ryzyko toohello zbierane są one adresowania) można ją włączyć. Wreszcie Centrum zabezpieczeń Azure jest otwartej platformie, która umożliwia partnerom firmy Microsoft i niezależnych dostawców toocreate oprogramowanie podłączane do Centrum zabezpieczeń Azure tooenhance jego możliwości. 

> [!TIP]
> Centrum zabezpieczeń Azure jest domyślnie włączone w każdej subskrypcji. Jednak należy włączyć zbieranie danych z maszyn wirtualnych tooallow Centrum zabezpieczeń Azure tooinstall jego agenta i rozpocząć zbieranie danych.
> 
> ![Zbieranie danych](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Następne kroki
* Teraz, kiedy znasz dotyczących ładu subskrypcji, jest czas toosee te zalecenia w praktyce. Zobacz [przykłady stosowania ładu subskrypcji platformy Azure](resource-manager-subscription-examples.md).

