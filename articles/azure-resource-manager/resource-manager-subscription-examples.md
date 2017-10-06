---
title: "aaaScenarios i przykłady dotyczące ładu subskrypcji | Dokumentacja firmy Microsoft"
description: "Zawiera przykłady tooimplement ładu subskrypcji platformy Azure dla typowych scenariuszy."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Przykłady stosowania szkieletu Azure enterprise
W tym temacie przedstawiono przykłady sposobu przedsiębiorstwa można zaimplementować hello zalecenia dotyczące [szkieletu Azure enterprise](resource-manager-subscription-governance.md). Używa fikcyjnej firmy o nazwie Contoso tooillustrate najlepsze rozwiązania dla typowych scenariuszy.

## <a name="background"></a>Tła
Contoso to firma na całym świecie, która zapewnia rozwiązania łańcucha dostaw dla klientów w wszystkie elementy z modelu spakowanych tooa modelu "Oprogramowanie jako usługa" wdrożonych lokalnie.  Między Witaj świecie z produkcyjnymi znaczących Programowanie w Indie hello Stany Zjednoczone i Kanada opracowywania oprogramowania.

Hello niezależnego dostawcy oprogramowania część firmy hello jest podzielona na kilka jednostek biznesowych niezależne, zarządzających produktów w znaczący biznesowych. Poszczególnych jednostek biznesowych ma własną deweloperów, menedżerów produktu i architektów.

jednostki biznesowej usługi technologii przedsiębiorstwa (ETS) Hello zapewnia scentralizowane możliwości IT i zarządza kilka centrach danych, w których jednostki biznesowe host swoich aplikacji. Wraz z zarządzania centrami danych hello, hello organizacji ETS zawiera i zarządza scentralizowane współpracy (np. poczty e-mail i witryn sieci Web) i usług sieciowych/telefonii. Mniejszych jednostek biznesowych, którzy nie mają personel operacyjny one również zarządzać obciążeń skierowane do klienta.

następujące osoby Hello są używane w tym temacie:

* Dave jest hello ETS Azure administratora.
* Alicja jest programowanie z Dyrektor firmy Contoso w jednostce biznesowej łańcucha dostaw hello.

Contoso musi toobuild Linia biznesowych aplikacji i aplikacji dostępnych dla klienta. Przyjęła toorun aplikacji hello na platformie Azure. Dave odczytuje hello [ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md) tematu, i jest teraz gotowy tooimplement hello zalecenia.

## <a name="scenario-1-line-of-business-application"></a>Scenariusz 1: aplikacji biznesowych —
Contoso jest kompilowanie kodu źródłowego zarządzania toobe systemu (BitBucket) używany przez deweloperów w hello world.  Aplikacja Hello wykorzystuje infrastrukturę jako usługę (IaaS) do obsługi i składa się z serwerami sieci web a serwerem bazy danych. Deweloperzy uzyskać dostępu do serwerów w swoich środowiskach programistycznych, ale nie wymagają dostępu serwerów toohello na platformie Azure. Contoso ETS chce właściciela aplikacji hello tooallow i aplikacja hello toomanage team. Aplikacja Hello jest dostępna tylko podczas firmy Contoso w sieci firmowej. Dave musi tooset się hello subskrypcji dla tej aplikacji. Subskrypcja Hello będzie obsługiwać także innego oprogramowania związane z programowaniem w przyszłości hello.  

### <a name="naming-standards--resource-groups"></a>Standardy nazewnictwa & grup zasobów
Dave tworzy subskrypcję toosupport narzędzia deweloperskie, które są wspólne dla wszystkich jednostek biznesowych hello. Musi on łatwy do rozpoznania nazwy toocreate hello subskrypcji i grup zasobów (w przypadku aplikacji hello i hello sieci). Tworzy hello następujące grupy subskrypcji i zasobu:

| Element | Nazwa | Opis |
| --- | --- | --- |
| Subskrypcja |Contoso ETS DeveloperTools produkcji |Obsługuje typowych narzędzi deweloperskich |
| Grupa zasobów |rgBitBucket |Zawiera serwer sieci web aplikacji hello i serwer bazy danych |
| Grupa zasobów |rgCoreNetworks |Zawiera hello sieci wirtualnych i połączenie bramy lokacja lokacja |

### <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach
Po utworzeniu jego subskrypcji, Dave chce tooensure, który hello odpowiednie zespoły i właściciele aplikacji mogą uzyskiwać dostęp do ich zasobów. Dave rozpoznaje, że każdy zespół ma inne wymagania. ADAM korzysta z hello grup, które zostały zsynchronizowane z firmy Contoso lokalnej usługi Active Directory (AD) tooAzure usługi Active Directory i zapewnia odpowiedni poziom dostępu toohello zespołów hello.

Następujące role dla subskrypcji hello hello przypisuje Dave:

| Rola | Zbyt przypisany| Opis |
| --- | --- | --- |
| [Właściciel](../active-directory/role-based-access-built-in-roles.md#owner) |Zarządzane identyfikator z firmy Contoso AD |Ten identyfikator jest kontrolowany przy użyciu tylko w czasie (JIT) dostęp za pomocą narzędzia do zarządzania tożsamościami firmy Contoso i zapewnia, że pełni podlega inspekcji dostępu do właściciela subskrypcji. |
| [Menedżer zabezpieczeń](../active-directory/role-based-access-built-in-roles.md#security-manager) |Bezpieczeństwo i ryzyka działu zarządzania |Ta rola umożliwia toolook użytkowników na powitania Centrum zabezpieczeń Azure i stan hello hello zasobów. |
| [Współautor sieci](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Zespół sieci |Ta rola umożliwia toomanage zespołu sieci firmy Contoso hello tooSite witryny sieci VPN i hello sieci wirtualnych. |
| *Rola niestandardowa* |Właściciel aplikacji |Dave tworzy rolę, która udziela hello możliwości toomodify zasoby w grupie zasobów hello. Aby uzyskać więcej informacji, zobacz [niestandardowych ról w Azure RBAC](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Zasady
Dave ma następujące wymagania dotyczące zarządzania zasobami subskrypcji hello hello:

* Ponieważ narzędzi programistycznych hello obsługiwać deweloperzy między Witaj świecie, on nie mają tooblock użytkownikom tworzenia zasobów w dowolnym regionie. Jednak potrzebuje tooknow, gdy zasoby są tworzone.
* Jest on dane z kosztami. W związku z tym Maciej chce właściciele aplikacji tooprevent tworzenia niepotrzebnie kosztowne maszyn wirtualnych.  
* Ponieważ ta aplikacja obsługuje deweloperów w wiele jednostek biznesowych, chce tootag każdego zasobu z hello właściciela jednostki i aplikacji biznesowych. Przy użyciu tych tagów, ETS można naliczać opłaty hello odpowiednie zespołów.

Tworzy następujące hello [zasad Menedżera zasobów](resource-manager-policy.md):

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |Inspekcji |Przeprowadź inspekcję tworzenia hello hello zasobów w dowolnym regionie |
| type |Odmów |Tworzenie maszyn wirtualnych serii G Odmów |
| tags |Odmów |Wymagaj tag właściciel aplikacji |
| tags |Odmów |Wymagaj tag Centrum kosztu |
| tags |Dołącz |Dołącz nazwy tagu **jednostką biznesową** , wartość tagu **ETS** tooall zasobów |

### <a name="resource-tags"></a>Tagi zasobów
Dave rozumie potrzebuje toohave informacje szczegółowe dotyczące Centrum kosztu hello hello rachunku tooidentify hello BitBucket implementacji. Ponadto Dave chce tooknow hello wszystkie zasoby należące do ETS.

Dodaje następujące hello [tagi](resource-group-using-tags.md) toohello grup zasobów i zasobów.

| Nazwa tagu | Wartość tagu |
| --- | --- |
| ApplicationOwner |Nazwa Hello hello osoby, która zarządza tej aplikacji. |
| CostCenter |Centrum kosztów Hello hello grupy, która jest płatność za hello wykorzystania platformy Azure. |
| Jednostką biznesową |**ETS** (skojarzone z subskrypcją hello jednostki biznesowej hello) |

### <a name="core-network"></a>Sieci podstawowej
Hello ETS Contoso proponowane informacji zabezpieczeń i ryzyka kadra kierownicza sprawdza w Dave planowanie tooAzure aplikacji hello toomove. Mają tooensure, która aplikacja hello nie jest widoczne toohello internet.  Dave ma również developer aplikacje, które w przyszłości hello zostaną przeniesione tooAzure. Te aplikacje wymagają interfejsów publicznych.  toomeet tych wymagań, dostarcza wewnętrznych i zewnętrznych sieci wirtualnych oraz toorestrict grupy zabezpieczeń sieci dostęp.

Tworzy hello następujące zasoby:

| Typ zasobu | Nazwa | Opis |
| --- | --- | --- |
| Virtual Network |vnInternal |Używane z hello BitBucket aplikacji i jest połączony za pośrednictwem sieci firmowej ExpressRoute tooContoso.  Podsieć (sbBitBucket) udostępnia aplikacji hello z określonych przestrzeni adresów IP. |
| Virtual Network |vnExternal |Dostępne dla przyszłych aplikacji, które wymagają publicznych punktów końcowych. |
| Grupy zabezpieczeń sieci |nsgBitBucket |Zapewnia, że hello ataku to obciążenie jest zminimalizowany przez zezwala na połączenia tylko na porcie 443 dla podsieci hello aplikacji hello, w którym znajduje się (sbBitBucket). |

### <a name="resource-locks"></a>Blokowania zasobów
Dave rozpoznaje, że hello łączności z wewnętrznej sieci wirtualnej firmy Contoso sieci firmowej toohello musi być zabezpieczony przed dowolny skrypt wayward lub przypadkowym usunięciem.

Tworzy następujące hello [Blokada zasobu](resource-group-lock-resources.md):

| Typ blokady: | Zasób | Opis |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Uniemożliwia usuwanie hello sieci wirtualnej i podsieci, ale nie uniemożliwia hello dodanie nowych podsieci. |

### <a name="azure-automation"></a>Azure Automation
Dave nie ma nic tooautomate dla tej aplikacji. Mimo że utworzył konto usługi Automatyzacja Azure on nie będzie początkowo go używać.

### <a name="azure-security-center"></a>Azure Security Center
Zarządzanie usługami IT firmy Contoso musi tooquickly identyfikowania i obsługi zagrożeń. Chcą także toounderstand jakie problemy mogą występować.  

toofulfill tych wymagań, hello umożliwia Dave [Centrum zabezpieczeń Azure](../security-center/security-center-intro.md), zawiera rola zabezpieczeń Menedżer toohello dostępu.

## <a name="scenario-2-customer-facing-app"></a>Scenariusz 2: uwzględniającym klienta aplikacji
Hello kierowniczej biznesowych w jednostce biznesowej łańcucha dostaw hello zidentyfikował różnych możliwości tooincrease zaangażowania klientów firmy Contoso za pomocą karty lojalność. Zespół Alicji należy utworzyć tę aplikację i decyduje o tym, że Azure zwiększa ich toomeet możliwości hello potrzeb biznesowych. Alicja współpracuje z Dave ETS tooconfigure dwóch Subskrypcje dotyczące tworzenia i obsługi tej aplikacji.

### <a name="azure-subscriptions"></a>Subskrypcje platformy Azure
Dave loguje toohello Azure Enterprise Portal i widzi działu łańcucha dostaw hello już istnieje.  Jednak ten projekt jest hello pierwszy opracowywanego projektu team łańcucha dostaw hello na platformie Azure, Dave rozpoznaje hello potrzebę nowego konta, aby zespół deweloperów Alicji.  ADAM tworzy konto "R & D" hello dla swojego zespołu i przypisuje tooAlice dostępu. Alicja zaloguje się za pośrednictwem portalu Azure hello i tworzy dwa subskrypcje: jeden toohold hello programowanie serwerów i serwerów produkcyjnych hello toohold jeden.  Standardy nazewnictwa hello wcześniej ustanowione ona zgodna podczas tworzenia hello następujących subskrypcji:

| Użyj subskrypcji | Nazwa |
| --- | --- |
| Opracowywanie zawartości |Programowanie LoyaltyCard SupplyChain ResearchDevelopment |
| Produkcji |SupplyChain operacji LoyaltyCard produkcji |

### <a name="policies"></a>Zasady
Dave Alicja omówiono w nim aplikacji hello i zidentyfikować, że ta aplikacja służy tylko klienci w Ameryce Północnej regionie hello.  Alicja i jej zespół Planowanie środowiska usługi aplikacji toouse Azure i aplikacja hello toocreate Azure SQL. Podczas tworzenia potrzebnych toocreate maszyn wirtualnych.  Alicja chce tooensure hello zasobów potrzebnych tooexplore i badanie problemów bez ściąganie w ETS zainstalowanego jej deweloperów.

Dla hello **subskrypcji programowanie**, tworzenia hello następujące zasady:

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |Inspekcji |Przeprowadź inspekcję tworzenia hello hello zasobów w dowolnym regionie. |

Nie ograniczaj hello typ jednostki sku utworzone przez użytkownika w rozwoju i nie wymagają tagi dla wszystkich grup zasobów lub zasobów.

Dla hello **subskrypcji produkcji**, tworzenia hello następujące zasady:

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |Odmów |Odmów hello tworzenia zasobów poza hello USA centrach danych. |
| tags |Odmów |Wymagaj tag właściciel aplikacji |
| tags |Odmów |Wymagaj tag działu. |
| tags |Dołącz |Dołącz grupy zasobów tooeach tag wskazuje środowiska produkcyjnego. |

Nie ograniczaj hello typ jednostki sku utworzone przez użytkownika w środowisku produkcyjnym.

### <a name="resource-tags"></a>Tagi zasobów
Dave rozumie potrzebuje grupach hello tooidentify toohave określonych informacji w firmie poprawne rozliczeń i użytkowania. Definiuje znaczniki zasobu dla grupy zasobów i zasoby.

| Nazwa tagu | Wartość tagu |
| --- | --- |
| ApplicationOwner |Nazwa Hello hello osoby, która zarządza tej aplikacji. |
| Dział |Centrum kosztów Hello hello grupy, która jest płatność za hello wykorzystania platformy Azure. |
| EnvironmentType |**Produkcji** (nawet jeśli hello Subskrypcja obejmuje **produkcji** w nazwie hello, łącznie z tym znacznikiem umożliwia łatwą identyfikację podczas przeglądania zasobów w portalu hello lub na rachunku hello.) |

### <a name="core-networks"></a>Sieci podstawowej
Hello ETS Contoso proponowane informacji zabezpieczeń i ryzyka kadra kierownicza sprawdza w Dave planowanie tooAzure aplikacji hello toomove. Mają one tooensure, która karta lojalność aplikacji hello jest poprawnie izolowane i chronione w sieci Obwodowej.  toofulfill to wymaganie Dave i Alicja utworzyć zewnętrzną sieć wirtualną i sieć zabezpieczeń grupy tooisolate hello karty lojalność aplikacji z sieci firmy Contoso hello.  

Dla hello **subskrypcji programowanie**, tworzenia:

| Typ zasobu | Nazwa | Opis |
| --- | --- | --- |
| Virtual Network |vnInternal |Środowisko projektowe karty lojalność Contoso hello służy i jest połączony za pośrednictwem sieci firmowej ExpressRoute tooContoso. |

Dla hello **subskrypcji produkcji**, tworzenia:

| Typ zasobu | Nazwa | Opis |
| --- | --- | --- |
| Virtual Network |vnExternal |Obsługuje hello karty lojalność aplikacji i nie jest podłączony bezpośrednio tooContoso obiektu ExpressRoute. Kod spoczywa za pośrednictwem ich systemu kodu źródłowego bezpośrednio toohello PaaS usług. |
| Grupy zabezpieczeń sieci |nsgBitBucket |Zapewnia, że hello ataku to obciążenie jest zminimalizowany, zezwalając tylko komunikatu przychodzącego na porcie TCP 443.  Contoso bada również dodatkową ochronę za pomocą zapory aplikacji sieci Web. |

### <a name="resource-locks"></a>Blokowania zasobów
Dave Alicja przyznaje i zdecyduj, tooadd blokowania zasobów na niektóre z kluczowych zasobów hello hello środowiska tooprevent przypadkowego usunięcia podczas wypychania wadliwe kodu.

Tworzenia hello następującej blokady:

| Typ blokady: | Zasób | Opis |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |osoby tooprevent usunięcie sieci wirtualnej hello lub podsieci. Zablokuj Hello nie zapobiega hello dodanie nowych podsieci. |

### <a name="azure-automation"></a>Azure Automation
Alicja i jej zespół deweloperów mają środowiska hello toomanage szeroką gamę elementów runbook dla tej aplikacji. elementy runbook Hello umożliwiają hello dodanie/usunięcie węzłów dla aplikacji hello i innych zadań DevOps.

toouse te elementy runbook pozwalają [automatyzacji](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Azure Security Center
Zarządzanie usługami IT firmy Contoso musi tooquickly identyfikowania i obsługi zagrożeń. Chcą także toounderstand jakie problemy mogą występować.  

toofulfill tych wymagań, Dave umożliwia Centrum zabezpieczeń Azure. Zapewnia on, Centrum zabezpieczeń Azure hello jest monitorowanie zasobów hello i zapewnia dostęp toohello zespołów DevOps i zabezpieczeń.

## <a name="next-steps"></a>Następne kroki
* toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).

