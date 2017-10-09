---
title: aaaMicrosoft danych Azure szyfrowania na Rest | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie szyfrowania danych Microsoft Azure w rest, hello ogólne możliwości i zagadnienia ogólne."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Danych Azure szyfrowania na Rest
Istnieje wiele narzędzi w Microsoft Azure toosafeguard danych zgodnie z potrzebami firmy tooyour zabezpieczeń i zgodności. Ten dokument koncentruje się na jak danych jest chroniony w stanie spoczynku w Microsoft Azure, w tym artykule omówiono hello różnych składników biorących udział w implementacji ochrony danych hello i przegląda zalet i wad metod ochrony różnych zarządzania kluczami hello. 

Szyfrowanie Rest jest typowe wymagania dotyczące zabezpieczeń. Zaletą Microsoft Azure jest organizacji można osiągnąć szyfrowanie magazynowanych bez konieczności hello koszt wdrożenia i zarządzania i hello ryzyko niestandardowe klucza rozwiązania do zarządzania. Organizacje mają opcja hello Azure całkowicie Zarządzanie szyfrowaniem przechowywane przez. Ponadto organizacje mają różne tooclosely opcje zarządzania szyfrowania i klucze szyfrujące.

## <a name="what-is-encryption-at-rest"></a>Co to jest szyfrowanie magazynowanych?
Szyfrowanie magazynowanych odwołuje się toohello kryptograficznych kodowania (szyfrowanie) danych podczas zapisania. Witaj szyfrowanie projektów Rest w usłudze Azure tooencrypt szyfrowania symetrycznego i używać odszyfrować dużych ilości danych szybko zgodnie z prostego modelu koncepcyjnego tooa:

- Klucza szyfrowania symetrycznego jest tooencrypt używanych danych, ponieważ jest on trwały 
- Witaj sam klucz szyfrowania jest używane toodecrypt tych danych jest ona readied do użycia w pamięci
- Dane mogą być podzielone na partycje i może być używane różne klucze dla każdej partycji
- Klucze muszą być przechowywane w bezpiecznej lokalizacji z zasady kontroli dostępu, ograniczając dostęp toocertain tożsamości i rejestrowanie użycia klucza. Klucze szyfrowania danych często są szyfrowane przy użyciu szyfrowanie asymetryczne toofurther limit dostępu (omówiona w hello *hierarchii klucza*w dalszej części tego artykułu)

Hello powyżej w tym artykule opisano hello wspólne elementy wysokiego poziomu szyfrowania w stanie spoczynku. W praktyce najważniejsze scenariusze zarządzania i kontroli, jak również skalowalność i dostępność gwarancji, wymagają dodatkowych konstrukcje. Microsoft Azure szyfrowanie Rest pojęcia i składniki są opisane poniżej.

## <a name="hello-purpose-of-encryption-at-rest"></a>cel Hello szyfrowania magazynowane
Szyfrowanie przechowywanych jest ochrona danych tooprovide przeznaczone dla danych na rest (jak opisano powyżej.) Ataki danych na rest obejmują prób tooobtain dostęp fizyczny toohello sprzętu na powitania, które dane są przechowywane i następnie hello naruszenia zabezpieczeń zawiera dane. W przypadku ataków dysk twardy serwera może mieć zostały niewłaściwego stosowania podczas konserwacji, co pozwala osobie atakującej dysku twardym powitania tooremove. Nowsze atakująca hello spowodowałaby hello dysk twardy do komputera w obszarze danych hello tooaccess tooattempt kontroli. 

Szyfrowanie rest jest zaprojektowana tooprevent atakująca hello uzyskanie dostępu do danych hello bez szyfrowania, zapewniając hello, którego dane są szyfrowane, gdy na dysku. Osoba atakująca tooobtain szyfrowany dysk twardy z takich danych i kluczy szyfrowania toohello dostępu, osoba atakująca hello nie może naruszać hello danych bez ogromne trudności. W takiej sytuacji osoba atakująca tooattempt ataków zaszyfrowane dane, które są bardziej złożone i korzystanie z zasobów niż dostęp do bez szyfrowania danych na dysku twardym. Z tego powodu szyfrowania magazynowane zdecydowanie zaleca się i jest wymagany w przypadku wielu organizacji o wysokim priorytecie. 

W niektórych przypadkach szyfrowanie magazynowanych jest również wymagane przez organizacji muszą uzyskać dane zarządzania i zgodności działań. Branżowych i rządowych przepisy, takie jak HIPAA, PCI i FedRAMP i międzynarodowych przepisów wymagania, układ zabezpieczenia określonego przez procesy i zasady dotyczące wymagania dotyczące ochrony i szyfrowania danych. Dla wielu z tych rozporządzeń szyfrowanie magazynowanych jest miarą obowiązkowe wymagane do zarządzania i ochrony danych zgodne. 

Ponadto toocompliance i przepisami dotyczącymi działalności, szyfrowanie magazynowanych powinien traktowany jako możliwości platformy obrony zabezpieczeń. Firma Microsoft udostępnia platformy zgodne w przypadku aplikacji, usług i danych, kompleksowe funkcje i zabezpieczenia fizyczne, inspekcji i kontroli dostępu do danych, jest ważne tooprovide dodatkowych "nakładające się" środki bezpieczeństwa w przypadku jednego z hello zabezpieczenia innych środków kończy się niepowodzeniem. Szyfrowanie magazynowane zapewnia dodatkową ochronę mechanizm.

Firma Microsoft dokłada szyfrowanie tooproviding zadeklarowanej w opcji rest przez usługi w chmurze i tooprovide klientów odpowiedniej możliwości zarządzania kluczy szyfrowania i toologs dostępu po klucze szyfrowania są używane. Ponadto firma Microsoft współpracuje drodze celu hello dokonywania szyfrowane, gdy domyślnie wszystkich danych klientów.

## <a name="azure-encryption-at-rest-components"></a>Szyfrowanie Azure w pozostałej części

Jak opisano wcześniej, celem hello szyfrowanie magazynowanych jest, czy jest utrwalony na dysku dane są szyfrowane przy użyciu klucza tajnego szyfrowania. ten cel tooachieve bezpiecznego tworzenia klucza, magazynu, kontroli dostępu i zarządzania należy podać klucze szyfrowania hello. Chociaż może się różnić szczegóły, usług Azure szyfrowania w implementacji Rest można opisać pod względem hello poniżej pojęcia, które następnie przedstawiono powitania po diagramu.

![Składniki](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>W usłudze Azure Key Vault

Lokalizacja magazynu Hello hello kluczy szyfrowania i klucze toothose kontroli dostępu jest szyfrowanie tooan centralnej w modelu rest. klucze Hello muszą toobe wysokiej zabezpieczone ale zarządzane przez określonych użytkowników i usług dostępnych toospecific. W przypadku usług Azure usługi Azure Key Vault jest hello zalecane rozwiązania magazynu kluczy i udostępnia typowe możliwości zarządzania w usługach. Klucze są przechowywane i zarządzane w magazynów kluczy, a magazyn kluczy dostępu tooa można przydzielić toousers lub usług. Usługa Azure Key Vault obsługuje tworzenie odbiorcy kluczy lub importowanie kluczy odbiorcy w scenariuszach klucza szyfrowania zarządzany przez klienta.

### <a name="azure-active-directory"></a>Usługa Azure Active Directory

Uprawnienia toouse hello klucze przechowywane w usłudze Azure Key Vault, toomanage lub tooaccess je do szyfrowania w Rest szyfrowania i odszyfrowywania, może mieć tooAzure kont usługi Active Directory. 

### <a name="key-hierarchy"></a>Hierarchia klucza

Zazwyczaj więcej niż jeden klucz szyfrowania jest używany podczas szyfrowania w implementacji rest. Szyfrowanie asymetryczne jest używany do tworzenia zaufania hello i uwierzytelniania wymagany dostęp do kluczy i zarządzania. Szyfrowanie symetryczne jest bardziej wydajny zbiorczego szyfrowania i odszyfrowywania, co zapewnia lepszą wydajność i silniejszego szyfrowania. Ponadto ograniczanie użycia hello klucza spadku pojedynczego szyfrowania hello ryzyko, że hello klucz zostanie naruszony i hello koszt ponownego szyfrowania po klucz muszą zostać zastąpione. Zalety hello tooleverage szyfrowanie asymetryczne i symetrycznego i użyj hello limit i zagrożeń jednego klucza, Azure szyfrowanie w modelach rest Użyj klucza hierarchii składają się z hello następujące typy kluczy:

- **Dane klucza szyfrowania** — klucza symetrycznego AES256 używane tooencrypt partycji lub bloku danych.  Pojedynczy zasób może mieć wiele partycji i wiele kluczy szyfrowania danych. Szyfrowanie każdy blok danych za pomocą innego klucza utrudnia ataków kryptograficznych analizy. TooDEKs dostępu są wymagane przez hello dostawcy lub aplikacji wystąpienia zasobu szyfrowania i odszyfrowywania określonego bloku. Po klucz szyfrowania danych zostanie zastąpiony przy użyciu nowego klucza tylko hello dane w jego skojarzony blok muszą być ponownie szyfrować przy hello nowego klucza.
- **Klucz szyfrowania klucza (KEK)** — klucza asymetrycznego szyfrowania używany hello tooencrypt klucze szyfrowania danych. Klucz szyfrowania klucza umożliwiają hello klucze szyfrowania danych, same toobe zaszyfrowane i kontrolowane. Witaj jednostki, która ma dostęp toohello KEK mogą różnić się od hello jednostki, która wymaga hello klucza szyfrowania danych. Dzięki temu jednostka toobroker dostępu toohello klucza szyfrowania danych hello w celu zapewnienia ograniczony dostęp do każdej partycji toospecific klucza szyfrowania danych. Ponieważ hello KEK jest wymagane toodecrypt hello DEKs, hello KEK skutecznie jest pojedynczym punktem za pomocą którego DEKs mogą być skutecznie usuwane przez usunięcie hello KEK.

Klucze szyfrowania danych Hello zaszyfrowane za pomocą kluczy szyfrowania klucza hello są przechowywane osobno i tylko jednostki z toohello dostępu, które klucza szyfrowania klucza można uzyskać klucze szyfrowania danych zaszyfrowanych za pomocą tego klucza. Obsługiwane są różne modele magazynu kluczy. Omówimy każdego modelu bardziej szczegółowo w dalszej części hello następnej sekcji.

## <a name="data-encryption-models"></a>Modele szyfrowania danych

Opis hello różne modele szyfrowania, a ich zalet i wad jest istotne dla zrozumienia sposobu hello różnych dostawców zasobów w szyfrowania Azure wdrożenie w stanie spoczynku. Te definicje są współdzielone przez wszystkich dostawców zasobów Azure tooensure CLR i taksonomii. 

Istnieją trzy scenariusze szyfrowania po stronie serwera:

- Szyfrowanie po stronie serwera przy użyciu usługi zarządzania kluczami
    - Dostawcy zasobów platformy Azure operacji hello szyfrowania i odszyfrowywania
    - Firma Microsoft zarządza hello kluczy
    - Chmura pełna funkcjonalność

- Szyfrowanie po stronie serwera za pomocą kluczy zarządzany przez klienta w usłudze Azure Key Vault
    - Dostawcy zasobów platformy Azure operacji hello szyfrowania i odszyfrowywania
    - Klient kontroluje klucze za pomocą usługi Azure Key Vault
    - Chmura pełna funkcjonalność

- Szyfrowanie po stronie serwera za pomocą klawiszy zarządzany przez klienta na sprzęcie komputerowym kontrolowane
    - Dostawcy zasobów platformy Azure operacji hello szyfrowania i odszyfrowywania
    - Klucze kontroli klienta na klienta kontrolowane sprzętu
    - Chmura pełna funkcjonalność

Szyfrowanie po stronie klienta należy wziąć pod uwagę następujące hello:

- Usługi platformy Azure nie widzi odszyfrowane dane
- Klienci zarządzania i przechowywanie kluczy lokalnie (lub w innych secure magazynów). Klucze nie są dostępne tooAzure usług
- Funkcje zmniejszenie chmury

modele szyfrowania Hello obsługiwane na platformie Azure, podzielić na dwie główne grupy: "Szyfrowania klienta" i "po stronie serwera szyfrowania" jak wspomniano powyżej. Należy pamiętać, że niezależnie od szyfrowania hello model rest używanych usług Azure zawsze zaleca się użycie hello bezpiecznego transportu, takich jak protokołu TLS lub HTTPS. W związku z tym szyfrowanie transportu powinny być kierowane przez protokół transportu hello i nie powinien być głównych czynnikiem umożliwiającym określenie które szyfrowanie toouse modelu rest.

### <a name="client-encryption-model"></a>Model szyfrowania klienta

Model szyfrowania klienta odwołuje się tooencryption, które jest przeprowadzane poza hello dostawcy zasobów lub Azure przez hello usługa lub aplikacja wywołująca. Aplikacja usługi hello na platformie Azure lub aplikacja działająca w centrum danych klienta hello można wykonać Hello szyfrowania. W obu przypadkach podczas korzystania z tego modelu szyfrowania hello Azure dostawcy zasobów otrzyma zaszyfrowany obiekt blob danych bez hello możliwości toodecrypt hello danych w żaden sposób lub mieć klucze szyfrowania toohello dostępu. W tym modelu hello zarządzania kluczami polega na powitania wywoływania aplikacji/usługi i jest całkowicie nieprzezroczysta toohello usługi Azure.

![Klient](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Model szyfrowania po stronie serwera

Modele szyfrowania po stronie serwera można znaleźć tooencryption wykonywanego przez hello usługi Azure. W tym modelu hello dostawcy zasobów wykonuje hello szyfrowania i odszyfrowywania operacji. Na przykład usługi Azure Storage może odbierać dane w postaci zwykłego tekstu operacjach i wykona hello szyfrowania i odszyfrowywania wewnętrznie. Witaj dostawcy zasobów może używać kluczy szyfrowania, które są zarządzane przez firmę Microsoft lub powitania klienta w zależności od hello podane konfiguracji. 

![Serwer](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modele zarządzania kluczami szyfrowania po stronie serwera

Każdy z hello szyfrowanie po stronie serwera w modelach rest oznacza cechy charakterystyczne zarządzania kluczami. Zawierają i jak klucze szyfrowania są tworzone i przechowywane jako także hello modele dostępu i hello procedury rotacją kluczy. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Szyfrowanie po stronie serwera za pomocą kluczy usługi zarządzania

Dla wielu klientów wymóg zasadniczy hello jest tooensure, który hello dane są szyfrowane, zawsze, gdy jest w stanie spoczynku. Przy użyciu usługi zarządzane klucze szyfrowania po stronie serwera umożliwia ten model umożliwia klientom toomark hello określonego zasobu (konto magazynu, bazy danych SQL, itp.) do szyfrowania i pozostawienie wszystkie aspekty zarządzania kluczami, takie jak publikowania klucza, obracanie i tworzenia kopii zapasowej tooMicrosoft. Większość usług Azure, które obsługują szyfrowanie magazynowanych zwykle obsługuje odciążanie hello zarządzania tooAzure klucze szyfrowania hello tego modelu. dostawcy zasobów platformy Azure Hello tworzy hello klucze, umieszcza je w bezpiecznym magazynie i pobiera je w razie potrzeby. Oznacza to, że hello usługi ma pełny dostęp toohello kluczy i usługa hello ma pełną kontrolę nad zarządzania cyklem życia poświadczeń hello.

![Zarządzane](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Szyfrowanie po stronie serwera za pomocą kluczy usługi zarządzania w związku z tym szybko adresów hello potrzeby toohave szyfrowanie magazynowanych przy niskim obciążeniu toohello klienta. Jeśli jest dostępna klient zazwyczaj otwiera hello portalu Azure dla subskrypcji docelowej hello i dostawcy zasobów i sprawdza pole wskazujący, że chciałby hello toobe dane zaszyfrowane. W niektórych menedżerowie zasobów szyfrowania po stronie serwera z usługą zarządzanych kluczy jest domyślnie włączone. 

Szyfrowanie po stronie serwera za pomocą kluczy zarządzany przez firmę Microsoft oznaczać hello usługi ma pełny dostęp toostore i zarządza hello kluczy. Gdy jest kilku klientów może być toomanage hello kluczy, ponieważ uważają, że ich zapewnienia lepszych zabezpieczeń, hello koszt i ryzyko związane z rozwiązaniem do magazynu kluczy niestandardowych należy uwzględnić podczas szacowania tego modelu. W wielu przypadkach organizacji mogą określić ograniczenia zasobów lub zagrożenia związane z rozwiązania lokalnego może większe ryzyko hello zarządzania chmurą szyfrowania hello na klucze rest.  Jednak ten model nie może być wystarczający do organizacji, które mają wymagania toocontrol hello tworzenia lub cyklem życia kluczy szyfrowania hello lub personel różnych toohave zarządzać kluczami szyfrowania usługi niż zarządzanie usługą hello (tj. podział zarządzania kluczami z hello ogólny model zarządzania dla usługi hello).

##### <a name="key-access"></a>Dostęp do klucza

Gdy jest używane szyfrowanie po stronie serwera z usługi zarządzania kluczami, hello tworzenie kluczy dostępu do magazynu i usługi są zarządzane przez usługę hello. Zazwyczaj hello dostawców podstawowych zasobów platformy Azure będą przechowywane klucze szyfrowania danych hello w magazynie, który jest Zamknij toohello danych i szybko dostępne i jest dostępny podczas kluczy szyfrowania klucza hello są przechowywane w bezpiecznym magazynie wewnętrznej.

**Zalety**

- Prosta konfiguracja
- Firma Microsoft zarządza obrotu klucza, tworzenia kopii zapasowej i nadmiarowość
- Odbiorca nie ma hello koszt związany z implementacji lub hello ryzyko schemat niestandardowy zarządzania kluczami.

**Wady**

- Odbiorcy nie kontroluje klucze szyfrowania hello (Specyfikacja klucza cyklu życia, odwołania, itp.)
- Nie możliwości toosegregate zarządzania kluczami z ogólną model zarządzania dla usługi hello

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Szyfrowanie po stronie serwera przy użyciu klienta zarządzane klucze w usłudze Azure Key Vault 

W scenariuszach, w którym hello wymaganiem tooencrypt hello dane przechowywane w i kontroli hello szyfrowania kluczy klienci mogą używać szyfrowania po stronie serwera za pomocą klienta zarządzanych kluczy w magazynie kluczy. Niektóre usługi mogą być przechowywane tylko hello głównego klucza szyfrowania kluczy w magazynie kluczy Azure i hello magazynu szyfrowane klucza szyfrowania danych w wewnętrznej bliżej toohello ilości danych lokalizacji. W czy klientów scenariusz niesie własnych kluczy tooKey magazynu (BYOK — Bring Your Own Key), lub wygenerować nowe i używać ich tooencrypt hello potrzeby zasobów. Gdy hello dostawcy zasobów wykonuje operacje szyfrowania i odszyfrowywania hello używa klucza hello skonfigurowany jako hello klucz główny dla wszystkich operacji szyfrowania. 

##### <a name="key-access"></a>Dostęp do klucza

Witaj modelu szyfrowania po stronie serwera za pomocą kluczy klientów zarządzanych w magazynie kluczy Azure obejmuje tooencrypt klucze hello podczas uzyskiwania dostępu do usługi hello i odszyfrowywania zgodnie z potrzebami. Szyfrowanie pozostałe klucze zostały wprowadzone usługi tooa dostępny za pośrednictwem zasad kontroli dostępu, udzielanie klucza tożsamości hello tooreceive dostępu tej usługi. Uruchomione w imieniu skojarzona subskrypcja usługi Azure można skonfigurować przy użyciu tożsamości dla tej usługi w ramach danej subskrypcji. Hello usługi można wykonać uwierzytelniania usługi Azure Active Directory i odbierać tokenu uwierzytelniania zidentyfikowania się jako działający w imieniu hello subskrypcji usługi. Tokenu można następnie przedstawioną tooKey magazynu tooobtain klucza można go ma dostęp do.

Dla operacji przy użyciu kluczy szyfrowania, tożsamości usługi może zostać przydzielony tooany dostępu z hello następujące operacje: odszyfrować, szyfrowania, unwrapKey, wrapKey, sprawdź, zaloguj się, get, listy, aktualizacji, utworzyć, zaimportować, Usuń, kopii zapasowej i przywracania.

tooobtain klucza do użycia w szyfrowania lub odszyfrowywania danych w tożsamości usługi rest hello tego hello Menedżera zasobów będzie uruchomione wystąpienie usługi, musi mieć UnwrapKey (tooget hello klucz odszyfrowywania) i WrapKey (tooinsert klucz do magazynu kluczy podczas tworzenia nowego klucza).


>[!NOTE] 
>Aby uzyskać więcej szczegółów na Key Vault autoryzacji Zobacz hello bezpiecznego magazynu kluczy strony w hello [dokumentacji usługi Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Zalety**

- Pełną kontrolę nad kluczami hello używany — w magazynie kluczy powitania klienta pod kontrolą powitania klienta zarządzania kluczami szyfrowania.
- Tooencrypt możliwości wielu usług tooone wzorca
- Może też oddzielić zarządzania kluczami z ogólną model zarządzania dla usługi hello
- Można zdefiniować usługi i lokalizacji klucza w regionach

**Wady**

- Klient ma pełną odpowiedzialność za zarządzanie klucza dostępu
- Klient ma pełną odpowiedzialność za zarządzanie cyklem życia klucza
- Dodatkowe obciążenie instalacji i konfiguracji

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Szyfrowanie po stronie serwera za pomocą usługi zarządzane klucze w sprzęcie komputerowym kontrolowane

W scenariuszach, w którym wymaganie hello tooencrypt hello danych magazynowanych i zarządzać nimi klucze hello w repozytorium zastrzeżonych poza kontrolą firmy Microsoft niektóre usługi Azure modelu hello hosta swój własny klucz (HYOK) zarządzania kluczami. W tym modelu usługi hello hello klucza muszą zostać pobrane z witryny zewnętrznej w związku z tym wpływ na wydajność i dostępność gwarancje i konfiguracja jest bardziej złożony. Ponadto operacji odszyfrowywania hello ogólną gwarancje bezpieczeństwa tego modelu, ponieważ usługa hello ma toohello dostępu do klucza szyfrowania danych podczas szyfrowania hello są podobne powitalne toowhen klucze są zarządzane przez klienta w usłudze Azure Key Vault.  W związku z tym tego modelu nie jest odpowiedni dla większości organizacji, chyba że mają wymagania dotyczące zarządzania określonymi klucza wymagających go. Ze względu na ograniczenia toothese większość usług Azure nie obsługują szyfrowanie po stronie serwera za pomocą kluczy serwer zarządzany w sprzęcie komputerowym pod kontrolą.

##### <a name="key-access"></a>Dostęp do klucza

Gdy jest używane szyfrowanie po stronie serwera za pomocą kluczy usługi zarządzania w sprzęcie komputerowym kontrolowane hello klucze są obsługiwane w systemie, skonfigurowane przez powitania klienta. Usług Azure, które obsługują ten model zapewniają oznacza ustanowienia bezpiecznego połączenia klienta tooa dostarczony magazynu kluczy.

**Zalety**

- Pełną kontrolę nad hello klucz główny używany — szyfrowania kluczy są zarządzane przez sklep dostarczanych przez klienta
- Tooencrypt możliwości wielu usług tooone wzorca
- Może też oddzielić zarządzania kluczami z ogólną model zarządzania dla usługi hello
- Można zdefiniować usługi i lokalizacji klucza w regionach

**Wady**

- Pełną odpowiedzialność za magazynu kluczy, zabezpieczeń, wydajności i dostępności
- Pełną odpowiedzialność za zarządzanie klucza dostępu
- Pełną odpowiedzialność za zarządzanie cyklem życia klucza
- Znaczące instalacji, konfiguracji i kosztów rutynowej konserwacji
- Zwiększona zależność od dostępności sieci między powitania klienta w centrum danych i centrach danych platformy Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Szyfrowanie przechowywanych w usług chmurowych firmy Microsoft

Microsoft Cloud services są używane we wszystkich trzech chmury modelach: IaaS i PaaS, SaaS. Poniżej dostępne są przykłady sposób dopasowania na każdym modelu:

- Oprogramowanie usług tooas określonego oprogramowania jako serwer lub SaaS, którego aplikacja podał hello chmury, takich jak usługi Office 365.
- Usług platformy, którzy wykorzystać hello chmury w swoich aplikacjach przy użyciu chmury hello elementów, takich jak magazyn, analizy i Usługa funkcji magistrali.
- Infrastruktura usług lub infrastruktura jako usługa (IaaS) w którego odbiorcy wdrażania systemów operacyjnych i aplikacji, które znajdują się w hello chmury i prawdopodobnie wykorzystaniu innych usług w chmurze.

### <a name="encryption-at-rest-for-saas-customers"></a>Szyfrowanie przechowywanych dla klientów SaaS

Oprogramowanie jako usługa (SaaS) klienci zwykle mają szyfrowania magazynowane włączone lub dostępne w poszczególnych usługach. Usługi Office 365 ma kilka opcji szyfrowania tooverify lub Włącz dla klientów w stanie spoczynku. Informacje dotyczące usług Office 365 dla technologii szyfrowania danych dla usługi Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Szyfrowanie przechowywanych dla klientów PaaS

Platforma jako usługa (PaaS) odbiorcy danych zazwyczaj znajduje się w środowisku wykonywania aplikacji i wszystkich dostawców zasobów Azure używane toostore danych klienta. szyfrowanie hello toosee tooyou dostępne opcje rest zbadać hello tabelę poniżej dla platform magazynu i aplikacji hello, których używasz. Jeśli są obsługiwane, tooinstructions łącza na włączenie szyfrowania magazynowane są dostępne dla każdego dostawcy zasobów. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Szyfrowanie magazynowanych klientom IaaS

Infrastruktura jako usługa (IaaS) klienci mogą mieć różnych usług i aplikacji w użyciu. Usługi IaaS można włączyć szyfrowanie przechowywanych w ich Azure hostowanej maszyny wirtualne i wirtualne dyski twarde przy użyciu szyfrowania dysków Azure. 

#### <a name="encrypted-storage"></a>Zaszyfrowane magazynu

Podobnie jak PaaS innymi usługami Azure, które przechowują dane szyfrowane, gdy mogą korzystać z rozwiązań IaaS. W takich przypadkach można włączyć hello szyfrowania w witrynie pomocy technicznej Rest zgodnie z każdym wykorzystanych usługi Azure. Witaj w poniższej tabeli wylicza główne magazynu hello, usług i aplikacji platformy i modelu hello szyfrowania, gdy nie są obsługiwane. Jeśli są obsługiwane, linki znajdują się tooinstructions na włączenie szyfrowania w stanie spoczynku. 

#### <a name="encrypted-compute"></a>Zaszyfrowane obliczeń

Kompleksowe rozwiązania Rest wymaga tego powitalne dane nigdy nie jest utrwalona w niezaszyfrowanej postaci. Znajduje się w użyciu, na powitania ładowania serwera, które dane w pamięci, danych może być utrwalona lokalnie na różne sposoby, w tym plik stronicowania systemu Windows hello, zrzutu awaryjnego i wszelkie hello rejestrowania aplikacja może wykonywać. te dane są szyfrowane tooensure magazynowane IaaS aplikacje mogą używać szyfrowania dysków Azure na maszynie wirtualnej Azure IaaS (Windows lub Linux) i dysku wirtualnego. 

#### <a name="custom-encryption-at-rest"></a>Szyfrowanie niestandardowe przechowywane

Zaleca się, że jeśli to możliwe, IaaS aplikacje korzystać z szyfrowania dysków Azure i szyfrowania w opcji Rest dostarczanych przez dowolnego wykorzystanych usług platformy Azure. W niektórych przypadkach takich jak wymagania dotyczące szyfrowania nieregularne lub magazynu opartego na innych niż Azure, Deweloper aplikacji IaaS może być konieczne szyfrowanie tooimplement rest samodzielnie. Deweloperzy rozwiązań można lepiej IaaS zintegrować z platformy Azure, zarządzania i klienta oczekiwania dzięki wykorzystaniu niektóre składniki platformy Azure. W szczególności Programiści powinni używać hello Azure Key Vault tooprovide usługi bezpiecznego magazynu kluczy, a także zapewnić klientom opcji zarządzania kluczami spójne usług platformy Azure najbardziej. Ponadto kluczy szyfrowania tooaccess kont usługi tooenable tożsamości zarządzanych usług Azure należy używać w niestandardowych rozwiązań. Aby uzyskać informacje dla deweloperów usługi Azure Key Vault i zarządzane tożsamości usługi Zobacz ich odpowiednich zestawów SDK.

## <a name="azure-resource-providers-encryption-model-support"></a>Obsługa modelu szyfrowania dostawcy zasobów platformy Azure

Usługi Microsoft Azure każdego obsługuje co najmniej jeden szyfrowanie hello w modelach rest. W przypadku niektórych usług, co najmniej jeden hello modeli szyfrowania nie można stosować. Ponadto usługi może zwolnić obsługę tych scenariuszy, w różne harmonogramy. W tej sekcji opisano hello szyfrowania w witrynie pomocy technicznej rest w czasie hello pisania tego dokumentu dla każdego z usług magazynu hello najważniejszych danych Azure.

### <a name="azure-disk-encryption"></a>Szyfrowanie dysków Azure

Każdy klient jako usługa (IaaS) przy użyciu infrastruktury platformy Azure funkcji można osiągnąć szyfrowanie przechowywanych maszyn wirtualnych IaaS i dysków za pomocą szyfrowania dysków Azure. Aby uzyskać więcej informacji na dysku Azure szyfrowania Zobacz hello [dokumentacji szyfrowania dysków Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Azure Storage

Obiektów Blob platformy Azure i plików obsługuje szyfrowanie przechowywanych dla scenariuszy zaszyfrowany po stronie serwera, a także klienta zaszyfrowanych danych (szyfrowanie po stronie klienta).

- Po stronie serwera: klientów przy użyciu magazynu obiektów blob platformy Azure można włączyć szyfrowanie przechowywanych na każdym koncie zasobów magazynu Azure. Raz włączone szyfrowanie po stronie serwera odbywa się przezroczysty toohello aplikacji. Zobacz [szyfrowanie usługi Magazyn Azure dla danych magazynowanych](https://docs.microsoft.com/azure/storage/storage-service-encryption) Aby uzyskać więcej informacji.
- Po stronie klienta: szyfrowanie po stronie klienta obiektów blob Azure jest obsługiwane. Po za pomocą szyfrowania po stronie klienta klientów szyfrowania danych hello i przekazywanie danych hello jako obiekt blob zaszyfrowany. Zarządzanie kluczami polega na powitania klienta. Zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) Aby uzyskać więcej informacji.


#### <a name="sql-azure"></a>Usługi SQL Azure

Usługi SQL Azure obecnie obsługuje szyfrowanie przechowywanych dla scenariuszy szyfrowania po stronie klienta i po stronie usługi zarządzany przez firmę Microsoft.

Obsługa sever szyfrowanie jest obecnie obsługiwane za pomocą funkcji SQL hello o nazwie przezroczystego szyfrowania danych. Po klienta SQL Azure umożliwia klucz funkcji TDE automatycznie są tworzone i zarządzane dla nich. Można włączyć szyfrowanie przechowywanych na poziomach hello bazy danych i serwera. Począwszy od czerwca 2017 r. [funkcji przezroczystego szyfrowania danych (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) zostanie włączona domyślnie na nowo utworzone bazy danych.

Szyfrowanie po stronie klienta danych SQL Azure jest obsługiwane przez hello [zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx) funkcji. Zawsze zaszyfrowane używa klucza tworzone i przechowywane przez powitania klienta. Klientów można przechowywać hello klucza głównego magazynu certyfikatów systemu Windows, usługi Azure Key Vault lub lokalnego sprzętowego modułu zabezpieczeń. Za pomocą programu SQL Server Management Studio, SQL użytkowników wybierz, co klucza chciałby toouse tooencrypt kolumna.

|                                  |                |                     | **Model szyfrowania**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Klienta** |
|                                  | **Zarządzanie kluczami** | **Usługa zarządzania klucza** | **Klientów zarządzanych w magazynie kluczy** | **Klient zarządzany lokalnie** |        |
| **Magazyn i baz danych**            |                |                     |                              |                              |        |
| Dysku (IaaS)                      |                | -                   | Tak                          | Tak*                         | -      |
| Program SQL Server (IaaS)                |                | Tak                 | Tak                          | Tak                          | Tak    |
| Azure SQL (PaaS)                 |                | Tak                 | Wersja zapoznawcza                      | -                            | Tak    |
| Usługa Azure Storage (bloku/stronicowych obiektów blob) |                | Tak                 | Wersja zapoznawcza                      | -                            | Tak    |
| Magazyn Azure (pliki)            |                | Tak                 | -                            | -                            | -      |
| Usługa Azure Storage (tabel, kolejek)   |                | -                   | -                            | -                            | Tak    |
| Rozwiązania cosmos bazy danych (dokument DB)          |                | Tak                 | -                            | -                            | -      |
| Magazyn StorSimple                       |                | Tak                 | -                            | -                            | Tak    |
| Tworzenie kopii zapasowych                           |                | -                   | -                            | -                            | Tak    |
| **Analiza i analiza**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Tak                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Wersja zapoznawcza                      | -                            | -      |
| Usługa Azure Stream Analytics           |                | Tak                 | -                            | -                            | -      |
| HDInsights (magazyn obiektów Blob platformy Azure)  |                | Tak                 | -                            | -                            | -      |
| HDInsights (Data Lake Storage)   |                | Tak                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | Tak                 | Tak                          | -                            | -      |
| Azure Data Catalog               |                | Tak                 | -                            | -                            | -      |
| Power BI                         |                | Tak                 | -                            | -                            | -      |
| **Usługi IoT**                     |                |                     |                              |                              |        |
| Usługa IoT Hub                          |                | -                   | -                            | -                            | Tak    |
| Service Bus                      |                | -              | -                            | -                            | Tak    |
| Usługa Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Podsumowanie

Ochrona danych klienta przechowywanych w usługach Azure jest tooMicrosoft kluczowe znaczenie. Hostowana Azure wszystkie usługi są zatwierdzone tooproviding szyfrowania w pozostałych opcji. Podstawowych usług, takich jak usługi Azure Storage, SQL Azure i analiza klucza i usług analizy już zapewnia szyfrowanie na pozostałe opcje. Niektóre z tych usług obsługi klienta kontrolowane kluczy i szyfrowania po stronie klienta jak i usługi zarządzanych kluczy i szyfrowania. Usług Microsoft Azure są szeroko udoskonalanie szyfrowania na dostępność Rest i planowane nowe opcje podglądu i ogólnej dostępności w kolejnych miesięcy hello.

