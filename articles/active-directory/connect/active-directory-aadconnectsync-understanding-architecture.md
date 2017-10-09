---
title: 'Synchronizacja programu Azure AD Connect: opis architektury hello | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano architekturę hello synchronizacja programu Azure AD Connect i opisano hello terminów używanych."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Synchronizacja programu Azure AD Connect: opis architektury hello
W tym temacie opisano podstawową architekturę hello do synchronizacji Azure AD Connect. W wielu aspektach jest podobne poprzednikami tooits MIIS 2003, ILM 2007 i FIM 2010. Synchronizacja programu Azure AD Connect jest hello rozwój tych technologii. Jeśli znasz za pomocą dowolnego z tych starszych technologii, hello zawartość tego tematu będzie również znane tooyou. W przypadku nowych toosynchronization ten temat jest dla Ciebie. Jednak nie jest wymaganie tooknow hello szczegóły dotyczące tego tematu toobe pomyślnie w podejmowaniu dostosowania tooAzure AD Connect synchronizacji (aparatu synchronizacji o nazwie w tym temacie).

## <a name="architecture"></a>Architektura
Aparat synchronizacji Hello tworzy zintegrowany widok obiektów, które są przechowywane w wielu połączonych źródeł danych i zarządza nimi informacji o tożsamości w tych źródeł danych. Ten widok zintegrowane zależy od informacji o tożsamości hello pobierane z połączonych źródeł danych i zestaw reguł, które określają sposób tooprocess te informacje.

### <a name="connected-data-sources-and-connectors"></a>Łączników i połączonych źródeł danych
Aparat synchronizacji Hello przetwarza informacje o tożsamości z repozytoria różne dane, takie jak usługi Active Directory lub bazy danych programu SQL Server. Każdy repozytorium danych, która organizuje dane w postaci bazy danych i zapewnia dostęp do danych standardowych metod jest potencjalnych candidate źródła danych dla aparatu synchronizacji hello. Witaj repozytoria danych, które są synchronizowane przez aparat synchronizacji są nazywane **połączone źródła danych** lub **połączone katalogów** (CD).

Aparat synchronizacji Hello hermetyzuje interakcji z połączonego źródła danych modułu o nazwie **łącznik**. Każdy typ połączonego źródła danych ma określony łącznik. Witaj łącznika tłumaczy wymaganej operacji na format hello hello połączonych danych rozumie źródła.

Łączniki wywołań interfejsu API tooexchange (odczytu i zapisu) informacje o tożsamości z połączonego źródła danych. Możliwe jest również możliwe tooadd niestandardowego łącznika przy użyciu platformy extensible łączności hello. Witaj poniższej ilustracji przedstawiono sposób łącznik łączy z aparatem synchronizacji toohello źródła danych połączonych.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Przepływ danych w żadnym kierunku, ale nie można go jednocześnie przepływać w obu kierunkach. Innymi słowy łącznik może być skonfigurowany tooallow danych tooflow z aparatu toosync źródła danych połączonych hello lub synchronizacji aparat toohello połączonego źródła danych, ale tylko jeden z tych operacji może wystąpić w dowolnym momencie dla jednego obiektu, jak i atrybutu. Kierunek Hello mogą być różne dla różnych obiektów, jak i dla różnych atrybutów.

tooconfigure łącznika Określ obiektu hello typy, które mają toosynchronize. Określanie typów obiektu hello definiuje hello zakres obiektów, które są uwzględnione w procesie synchronizacji hello. Witaj następnym krokiem jest tooselect hello atrybutów toosynchronize, znany jako atrybut Lista dołączania. Te ustawienia można zmienić w dowolnym momencie, w przypadku reguł biznesowych tooyour toochanges odpowiedzi. Korzystając z Kreatora instalacji hello Azure AD Connect, te ustawienia są skonfigurowane dla Ciebie.

tooexport obiektów tooa połączonego źródła danych, lista dołączania atrybutu hello musi zawierać co najmniej minimalną hello atrybuty wymagane toocreate obiektu określonego typu w połączonego źródła danych. Na przykład Witaj **sAMAccountName** atrybutu musi być uwzględniony w tooexport listy dołączania atrybutu hello użytkownika obiektu tooActive katalogu, ponieważ wszystkie obiekty użytkowników w usłudze Active Directory musi mieć **sAMAccountName**  zdefiniowanego atrybutu. Kreator instalacji hello jest ponownie, konfigurację za Ciebie.

Jeśli hello połączonego źródła danych używa strukturalnych składniki, takie jak partycje lub kontenerów obiektów tooorganize, można ograniczyć obszarów hello hello połączonego źródła danych, które są używane dla danego rozwiązania.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Wewnętrzna struktura przestrzeni nazw aparatu synchronizacji hello
przestrzeń nazw aparatu synchronizacji całego Hello składa się z dwóch przestrzeni nazw, do których są przechowywane informacje o tożsamości hello. Witaj dwie przestrzenie nazw są:

* Obszar łączników Hello (CS)
* metaverse Hello (MV)

Witaj **przestrzeni łącznika** jest obszar tymczasowy zawierający reprezentacje Witaj wyznaczone obiektów z połączonych danych źródła i hello atrybutów określonych na liście dołączania hello atrybutu. Aparat synchronizacji Hello używa toodetermine przestrzeni łącznika hello co się zmieniło w hello połączone źródła i toostage przychodzących zmian danych. Aparat synchronizacji Hello używa również toostage przestrzeni łącznika hello wychodzące zmian eksportu toohello połączonego źródła danych. Aparat synchronizacji Hello przechowuje przestrzeni łącznika różne jako obszaru przemieszczania dla poszczególnych łączników.

Przy użyciu obszaru przemieszczania, aparat synchronizacji hello pozostaje niezależnie od hello połączone źródła danych i nie ma wpływu na ich dostępności i dostępności. W związku z tym może przetworzyć informacji o tożsamości w dowolnej chwili za pomocą hello danych w obszarze tymczasowym hello. Aparat synchronizacji Hello mogą żądać tylko hello zmian wewnątrz hello połączonego źródła danych od chwili zakończenia ostatniej sesji komunikacji hello lub wypychanej limit hello zmiany tooidentity informacje hello połączonego źródła danych nie otrzymał jeszcze, co zmniejsza Witaj ruchu sieciowego między aparatem synchronizacji hello i hello połączonego źródła danych.

Ponadto aparat synchronizacji przechowuje informacje o stanie dotyczące wszystkich obiektów, że poziomach hello przestrzeni łącznika. Po odebraniu nowych danych aparatu synchronizacji zawsze ocenia, czy dane hello już zostały zsynchronizowane.

Witaj **metaverse** to obszar pamięci masowej, zawierający informacje o tożsamości hello agregowane z wielu połączonych źródeł danych, zapewni jeden widok globalnej, zintegrowane wszystkich połączonych obiektów. Metaverse obiekty są tworzone w oparciu o informacje o tożsamości hello, które są pobierane z hello połączone źródła danych i zestaw reguł, które pozwalają toocustomize hello w procesie synchronizacji.

Witaj poniższej ilustracji przedstawiono hello łącznika przestrzeni nazw i przestrzeni nazw metaverse hello w hello aparatu synchronizacji.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Obiekty tożsamości aparatu synchronizacji
Obiekt Hello aparatu synchronizacji hello reprezentacje albo obiektów w hello połączonego źródła danych lub hello zintegrowane widoku, który aparat synchronizacji został tych obiektów. Każdy obiekt aparatu synchronizacji musi mieć unikatowy identyfikator globalny (GUID). Identyfikatory GUID zapewniają integralność danych i express relacje między obiektami.

### <a name="connector-space-objects"></a>Obiekty łączników miejsca
Gdy aparat synchronizacji komunikuje się z połączonego źródła danych, odczytuje informacje o tożsamości hello w hello połączonego źródła danych i korzysta z tej informacji toocreate reprezentację hello tożsamości obiektu przestrzeni łącznika hello. Nie można utworzyć lub usunąć tych obiektów pojedynczo. Można jednak ręcznie usuń wszystkie obiekty w przestrzeni łącznika.

Wszystkie obiekty w przestrzeni łącznika hello ma dwa atrybuty:

* Unikatowy identyfikator globalny (GUID)
* Nazwa wyróżniająca (DN)

Jeśli połączenie hello obiektu toohello unikatowy atrybut przypisuje źródła danych, a następnie obiekty w przestrzeni łącznika hello również mogą mieć atrybut zakotwiczenia. Atrybut zakotwiczenia Hello w sposób unikatowy identyfikuje obiekt w hello połączonego źródła danych. Aparat synchronizacji Hello używa hello zakotwiczenia toolocate hello odpowiedniego reprezentację tego obiektu w hello połączonego źródła danych. Aparat synchronizacji zakłada tego hello zakotwiczenia obiektu nigdy nie zmiany okresu istnienia hello hello obiektu.

Wiele łączników hello toogenerate znane Unikatowy identyfikator elementu zakotwiczenia automatycznie używać dla każdego obiektu po jego zaimportowaniu. Na przykład hello łącznika usługi Active Directory używa hello **objectGUID** atrybutu zakotwiczenia. Połączonych źródeł danych, które nie udostępniają jasno określone Unikatowy identyfikator można określić generację zakotwiczenia w ramach konfiguracji łącznika hello.

W tym przypadku zakotwiczenia hello składa się z jednego lub więcej atrybutów unikatowy obiektu typ, ani, które zmiany, oraz że jednoznacznie identyfikuje obiekt hello w hello przestrzeni łącznika (na przykład numer pracownika lub identyfikator użytkownika).

Obiekt miejsca łącznika może być jedną z następujących hello:

* Obiekt przemieszczania
* Symbol zastępczy

### <a name="staging-objects"></a>Obiekty tymczasowe
Obiekt przemieszczania reprezentuje wystąpienie Witaj wyznaczone typy obiektów z hello połączonego źródła danych. Ponadto toohello identyfikator GUID i nazwa wyróżniająca hello przemieszczania obiekt zawsze ma wartość, która wskazuje typ obiektu hello.

Obiekty tymczasowe, które zostały zaimportowane zawsze mieć wartość dla atrybutu zakotwiczenia hello. Obiekty tymczasowe, które zostały nowo udostępnione przez aparat synchronizacji i są w procesie hello tworzony w hello połączonego źródła danych nie mają wartości dla atrybutu zakotwiczenia hello.

Obiekty tymczasowe również zawierać bieżące wartości atrybutów biznesowych i informacje operacyjne wymagane przez proces synchronizacji hello tooperform aparatu synchronizacji. Informacje o działaniu zawiera flagi wskazujące typ hello aktualizacji, które są umieszczane na powitania przemieszczania obiektu. Jeśli obiekt przemieszczania otrzymał nowe informacje o tożsamości z hello połączonego źródła danych, które nie zostały jeszcze przetworzone, obiekt hello jest oznaczony jako **importu oczekujących**. Jeśli obiekt przemieszczania zawiera nowe informacje o tożsamości, która nie została jeszcze wyeksportowanego toohello połączonego źródła danych, jest oznaczone jako **oczekujących eksportu**.

Obiekt przemieszczania można obiektu importu lub eksportu. Aparat synchronizacji Hello tworzy obiekt importu za pomocą informacji o obiekcie otrzymanych od hello połączonego źródła danych. Aparat synchronizacji odebrania informacji o istnieniu hello nowy obiekt, który pasuje do jednego z typów obiektów hello wybrany w hello łącznika tworzy obiekt importu w przestrzeni łącznika hello jako reprezentacji obiektu hello w hello połączonego źródła danych.

Witaj następującej ilustracji przedstawiono obiektu import, który reprezentuje obiekt w hello połączonego źródła danych.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

Aparat synchronizacji Hello tworzy obiekt eksportu przy użyciu informacji o obiekcie w magazynie metaverse hello. Obiekty eksportu są wyeksportowanego toohello połączonego źródła danych podczas następnej sesji komunikacji hello. Z perspektywy hello aparatu synchronizacji hello eksportu obiekty nie istnieją w hello połączonego źródła danych jeszcze. W związku z tym hello atrybutu zakotwiczenia obiektu eksportu nie jest dostępna. Po otrzymaniu hello obiektu z aparatu synchronizacji hello połączonego źródła danych tworzy unikatową wartość dla atrybutu zakotwiczenia hello hello obiektu.

Witaj poniższej ilustracji przedstawiono sposób tworzenia obiektu eksportu przy użyciu informacji o tożsamości w magazynie metaverse hello.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

Aparat synchronizacji Hello potwierdza eksportu hello obiektu hello przez ponownie zaimportować hello obiektu hello połączonego źródła danych. Eksportowanie obiektów stają się importowanie obiektów odebrania aparatu synchronizacji ich podczas importowania dalej hello z tego źródła danych połączenia.

### <a name="placeholders"></a>Symbole zastępcze
Aparat synchronizacji Hello używa obiektów toostore prosty obszar nazw. Jednak niektóre połączonych źródeł danych takich jak usługi Active Directory użyj hierarchicznej przestrzeni nazw. tootransform informacji z hierarchicznej przestrzeni nazw w prosty obszar nazw, aparat synchronizacji używa symbole zastępcze toopreserve hello hierarchii.

Każdy symbol zastępczy odpowiada (na przykład jednostki organizacyjnej) część nazwy hierarchiczna obiektu nie został zaimportowany do aparatu synchronizacji, ale nazwa hierarchiczna hello tooconstruct wymagane. Wypełniania luk utworzone przez odwołań w tooobjects hello połączone źródła danych, które nie są przemieszczania obiekty w przestrzeni łącznika hello.

Aparat synchronizacji Hello używa również symbole zastępcze toostore odwołuje się do obiektów, które nie zostały zaimportowane. Na przykład, jeśli synchronizacja jest atrybut Menedżera hello tooinclude skonfigurowanych dla hello *Abbie Spencer* obiektu i hello odebranej wartości jest obiekt, który nie został jeszcze zaimportowany, takich jak *CN Lewandowski Sperry, CN = = Użytkownicy, DC = Firma fabrikam, DC = com*, hello Menedżera informacje są przechowywane jako symbole zastępcze w hello przestrzeni łącznika. Jeśli obiekt menedżera hello później jest importowany, obiekt symbol zastępczy hello jest zastępowana przez hello przemieszczania obiekt, który reprezentuje hello menedżera.

### <a name="metaverse-objects"></a>Obiekty metaverse
Obiektu metaverse zawiera widok hello zagregowane tego aparat synchronizacji ma hello przemieszczania obiektów w hello przestrzeni łącznika. Aparat synchronizacji tworzy obiekty metaverse przy użyciu informacji hello w Importowanie obiektów. Niektóre obiekty przestrzeni łącznika może być obiektu metaverse pojedynczego połączonego tooa, ale obiekt miejsca łącznika nie może być połączone toomore niż jednego obiektu metaverse.

Obiekty metaverse nie można ręcznie utworzyć ani usunąć. Aparat synchronizacji Hello automatycznie usuwa metaverse obiektów, które nie mają obiektu łącza tooany łącznika miejsca w hello przestrzeni łącznika.

toomap obiektach połączonych tooa odpowiedni typ obiektu źródła danych w magazynie metaverse hello aparatu synchronizacji zapewnia rozszerzony schemat z zestaw wstępnie zdefiniowanych typów obiektów i skojarzonych z nimi atrybutów. Można tworzyć nowe typy obiektów i atrybuty obiektów metaverse. Atrybuty mogą być jednowartościowe lub wielowartościowe i typy atrybutów hello może być ciągów, odwołań, cyfry i wartościami logicznymi.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relacje między obiektami przemieszczania i metaverse
W obszarze nazw aparatu synchronizacji hello hello przepływu danych jest włączana przez hello łącze relacji między obiektami przemieszczania i metaverse. Przemieszczania obiekt nosi nazwę obiektu metaverse połączonego tooa **dołączonego do obiektu** (lub **obiekt łącznika**). Obiekt przemieszczania, który nie jest połączony tooa obiektu metaverse jest wywoływana **odłączony obiekt** (lub **obiektu izolacyjny**). częścią Hello warunków, a następnie odłączony są preferowane toonot należy mylić z hello łączniki odpowiedzialny za importowania i eksportowania danych z połączonego katalogu.

Symbole zastępcze nigdy nie są połączone tooa obiektu metaverse

Dołączonego do obiektu obejmuje przemieszczania obiekt i jego obiektu metaverse pojedynczego tooa relacji. Połączone obiekty są wartości atrybutów używanych toosynchronize między obiektem przestrzeni łącznika i obiektu metaverse.

Gdy obiekt przemieszczania staje się dołączonego do obiektu podczas synchronizacji, między hello przemieszczania obiektu i obiektu metaverse hello przepływ atrybutów. Przepływ atrybutów jest dwukierunkowy i jest skonfigurowany przy użyciu reguł atrybutu importowania i eksportowania reguł atrybutu.

Obiekt miejsca pojedynczy łącznik może być tooonly połączonego obiektu metaverse jeden. Jednak każdego obiektu metaverse może być połączone toomultiple łącznika miejsca obiektów w hello tej samej lub różnych łącznika spacje, pokazane na następującej ilustracji hello.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Witaj połączony relacji między hello przemieszczania obiektu i obiektu metaverse jest trwałe i mogą być usunięte tylko przez zasady, które określisz.

Obiekt odłączonym jest przemieszczania obiektu, który nie jest połączony tooany obiektu metaverse. Atrybut Hello, wartości odłączonym obiektu nie są przetwarzane wszelkie dodatkowe w hello metaverse. Witaj atrybut, który wartości hello odpowiedni obiekt w hello połączonego źródła danych nie są aktualizowane przez aparat synchronizacji.

Za pomocą obiektów odłączonym, można przechowywać informacje o tożsamości w aparacie synchronizacji i przetworzyć go później. Utrzymywanie przemieszczania obiektu jako obiektu odłączonym przestrzeni łącznika hello ma wiele zalet. Ponieważ hello system już przemieszczeniu hello wymaganych informacji dotyczących tego obiektu nie jest konieczne toocreate reprezentację tego obiektu ponownie podczas hello obok importowanego hello połączonego źródła danych. W ten sposób aparat synchronizacji zawsze ma pełnej migawki hello połączonego źródła danych, nawet jeśli nie istnieje źródło danych połączonych toohello bieżącego połączenia. Obiekty odłączonym może zostać przekonwertowany na połączone obiekty i odwrotnie, w zależności od hello reguł, które określisz.

Obiekt importu jest tworzony jako odłączonym obiektu. Obiekt eksportu musi być przyłączony do obiektu. logiki systemu Hello wymusza tę regułę i usuwa każdy obiekt eksportu, który nie jest przyłączony do obiektu.

## <a name="sync-engine-identity-management-process"></a>Proces zarządzania tożsamościami aparatu synchronizacji
proces zarządzania tożsamościami Hello określa sposób aktualizowania informacji o tożsamości między różnych połączonych źródeł danych. Zarządzanie tożsamościami występuje w trzech procesów:

* Import
* Synchronizacja
* Eksportowanie

Podczas procesu importowania hello aparatu synchronizacji oblicza hello przychodzące informacje o tożsamości z połączonego źródła danych. Po wykryciu zmiany jego tworzy nowe obiekty tymczasowe albo aktualizuje istniejące obiekty tymczasowe w przestrzeni łącznika hello synchronizacji.

W procesie synchronizacji hello aparatu synchronizacji aktualizuje hello metaverse tooreflect zmiany, które wystąpiły w hello przestrzeni łącznika i aktualizuje hello łącznika miejsca tooreflect zmiany, które wystąpiły w magazynie metaverse hello.

W procesie eksportu hello aparatu synchronizacji wypycha zmiany, które są umieszczane na tymczasowej obiektów i które są oznaczone jako oczekujące eksportu.

Hello następującej ilustracji przedstawiono, gdzie poszczególne procesów hello występują jako tożsamość przepływ informacji z jednego połączenia danych tooanother źródła.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Proces importowania
Podczas procesu importowania hello aparatu synchronizacji ocenia aktualizacje tooidentity informacje. Aparat synchronizacji porównuje informacje o tożsamości hello otrzymanych od hello połączonego źródła danych z informacjami o tożsamości hello o tymczasowych obiektach i określa, czy hello przemieszczania obiekt wymaga aktualizacji. Jeśli jest konieczne tooupdate hello przemieszczania obiektu o nowe dane, importu oczekujących oflagowane hello przemieszczania obiektu.

Dzięki obiekty w przestrzeni łącznika hello przed synchronizacją, aparat synchronizacji może przetwarzać tylko hello informacji o tożsamości o zmianie. Ten proces obejmuje hello następujące korzyści:

* **Wydajność synchronizacji**. Witaj ilości danych przetwarzanych podczas synchronizacji jest zminimalizowany.
* **Ponowna synchronizacja wydajne**. Możesz zmienić sposób aparatu synchronizacji przetwarza informacje o tożsamości bez ponownie nawiązującego połączenie źródła danych toohello aparat hello synchronizacji.
* **Możliwość synchronizacji toopreview**. Można wyświetlić podgląd tooverify synchronizacji czy założeń dotyczących procesu zarządzania tożsamościami hello są poprawne.

Dla każdego obiektu określonego w hello łącznika aparatu synchronizacji powitania po raz pierwszy próbuje toolocate reprezentacja obiektu hello w przestrzeni łącznika hello hello łącznika. Aparat synchronizacji sprawdza wszystkich tymczasowych obiektów w przestrzeni łącznika hello i próbuje toofind odpowiedniego obiektu przemieszczania, który ma pasującego atrybutu zakotwiczenia. Jeśli nie istniejącego obiektu przemieszczania ma odpowiadającego mu atrybutu zakotwiczenia, synchronizować toofind prób aparat odpowiedniego tymczasowego obiektu o hello rozróżnianych takie same nazwy.

Jeśli aparat synchronizacji znajdzie przemieszczania obiekt, który odpowiada nazwie wyróżniającej, ale nie zakotwiczenia, hello następujące specjalne zachowanie:

* Jeśli obiekt hello znajdujący się w przestrzeni łącznika hello nie ma żadnych punktów kontrolnych, to aparat synchronizacji usuwa ten obiekt z hello przestrzeni łącznika i znaczniki hello obiektu metaverse jest połączone tooas **ponów inicjowania obsługi administracyjnej na uruchomienie w ramach następnej synchronizacji**. Następnie tworzy nowy obiekt importu hello.
* Jeśli obiekt hello znajdujący się w przestrzeni łącznika hello zakotwiczenie, aparat synchronizacji założono, że tego obiektu albo został przeniesiony lub usunięty z hello połączonego katalogu. Przypisuje tymczasowego, nowe nazwy wyróżniającej obiektu przestrzeni łącznika hello, dzięki czemu można umieścić hello przychodzące obiektu. Witaj stary obiekt staje się **przejściowa**, oczekiwanie hello łącznika tooimport hello zmiany nazwy lub usunięciu tooresolve hello sytuacji.

Jeśli aparat synchronizacji lokalizuje przemieszczania obiekt, który odpowiada toohello obiektu określonego w hello łącznika, określa rodzaj tooapply zmiany. Na przykład aparatu synchronizacji może Zmień lub Usuń obiekt hello w hello połączonego źródła danych lub może aktualizować tylko wartości atrybutu hello obiektów.

Obiekty tymczasowe o zaktualizowanych danych są oznaczone jako oczekujące na import. Dostępne są różne typy oczekującego importowania. W zależności od wyniku hello hello proces importowania obiekt przemieszczania przestrzeni łącznika hello może mieć jeden hello następujące typy oczekującego importowania:

* **Brak**. Nie tooany zmiany atrybutów hello hello przemieszczania obiektu są dostępne. Aparat synchronizacji nie Flaga ten typ importu oczekujących.
* **Dodaj**. Witaj przemieszczania obiektu jest nowy obiekt importu w przestrzeni łącznika hello. Aparat synchronizacji flagi tego typu jako oczekujące importu dla dodatkowego przetwarzania w magazynie metaverse hello.
* **Aktualizacja**. Aparat synchronizacji znajduje odpowiedni obiekt przemieszczania przestrzeni łącznika hello i flagi tego typu jako importu oczekujących, tak aby atrybuty toohello aktualizacje mogą być przetwarzane w magazynie metaverse hello. Aktualizacje obejmują, zmiana nazwy obiektu.
* **Usuń**. Aparat synchronizacji znajduje odpowiedni obiekt przemieszczania przestrzeni łącznika hello i flagi tego typu jako importu oczekujących, dzięki czemu hello dołączonego do obiektu można go usunąć.
* **Dodaj/Usuń**. Aparat synchronizacji znalezieniu odpowiedni obiekt przemieszczania hello przestrzeni łącznika, ale typy obiektów hello są niezgodne. W takim przypadku usuń dodawania są przygotowywane modyfikacji. A delete dodawania toohello aparatu synchronizacji, który musi występować pełnej ponownej synchronizacji tego obiektu, ponieważ różne zestawy reguł zastosować obiektu toothis po zmianie typu obiektu hello wskazuje modyfikacji.

Ustawienie hello oczekujących stan importu obiektu przemieszczania, istnieje możliwość tooreduce znacznie Witaj ilości danych przetwarzanych podczas synchronizacji, ponieważ to pozwala na powitania systemu tooprocess tylko te obiekty, które zostały zaktualizowane dane.

### <a name="synchronization-process"></a>Proces synchronizacji
Synchronizacja składa się z dwóch powiązanych z nim procesów:

* Synchronizacji ruchu przychodzącego, po zaktualizowaniu zawartości hello hello metaverse przy użyciu danych hello w hello przestrzeni łącznika.
* Synchronizacji ruchu wychodzącego, podczas aktualizowania zawartości hello przestrzeni łącznika hello przy użyciu danych w magazynie metaverse hello.

Przy użyciu informacji hello umieszczone w przestrzeni łącznika hello, hello procesu synchronizacji ruchu przychodzącego tworzy w widoku hello zintegrowane metaverse hello hello danych przechowywanych w źródłach danych hello połączony. Wszystkie obiekty tymczasowe lub tylko te informacje oczekującego importowania są agregowane w zależności od tego, jak reguły hello są skonfigurowane.

aktualizacje procesu synchronizacji ruchu wychodzącego Hello wyeksportować obiekty, obiekty metaverse zmiany.

Synchronizacji ruchu przychodzącego tworzy widok hello zintegrowane w magazynie metaverse hello informacji o tożsamości hello odebrane z hello połączone źródła danych. Aparat synchronizacji może przetworzyć informacji o tożsamości w dowolnym momencie przy użyciu hello najnowsze informacje o tożsamości on ma z hello podłączony źródła danych.

**Synchronizacji ruchu przychodzącego**

Synchronizacji ruchu przychodzącego obejmuje następujące procesy hello:

* **Należy** (nazywane również **projekcji** Jeśli jest ważne toodistinguish ten proces z synchronizacji ruchu wychodzącego inicjowania obsługi administracyjnej). Aparat synchronizacji Hello tworzy nowy obiekt metaverse oparte na obiekt przemieszczania i łączy je. Zainicjuj obsługę jest operacją na poziomie obiektu.
* **Dołącz**. Aparat synchronizacji Hello łączy przemieszczania obiektu tooan istniejącego obiektu metaverse. Sprzężenia jest operacją na poziomie obiektu.
* **Importuj przepływ atrybutów**. Aparat synchronizacji aktualizacji wartości atrybutu hello nazywanych przepływ atrybutów obiektu hello w magazynie metaverse hello. Przepływ atrybutów Import jest operacją poziom atrybutu, która wymaga połączenia między obiektu przemieszczania i obiektu metaverse.

Postanowienie jest hello tylko procesu, który tworzy obiekty w magazynie metaverse hello. Zainicjuj obsługę wpływa na importu tylko te obiekty, które są obiektami odłączonym. Podczas udostępniania aparat synchronizacji tworzy obiekt metaverse, który odpowiada toohello obiektu typu obiektu import hello i nawiązuje połączenie między zarówno do obiektów, w związku z tym tworzenia dołączonego do obiektu.

Proces dołączania Hello również nawiązuje połączenie między Importowanie obiektów i obiektu metaverse. Hello różnica między sprzężenia i dostarczanie polega na tym, że proces dołączania hello wymaga obiektu import hello są połączone tooan istniejącego obiektu metaverse, których proces udostępniania hello tworzy nowy obiekt metaverse.

Aparat synchronizacji próbuje toojoin obiektu metaverse tooa obiekt importu za pomocą kryteriów, które jest określone w konfiguracji reguły synchronizacji hello.

Podczas udostępniania hello i procesów sprzężenia aparat synchronizacji łączy odłączonym tooa metaverse dla obiektu, dzięki czemu przyłączone do. Po zakończeniu tych operacji na poziomie obiektu aparatu synchronizacji można zaktualizować wartości atrybutów hello hello metaverse skojarzonego obiektu. Ten proces jest nazywany importowania przepływu atrybutów.

Przepływ atrybutów Import występuje na wszystkie obiekty importu przenoszenia nowe dane, które są połączone tooa obiektu metaverse.

**Synchronizacji ruchu wychodzącego**

Aktualizacje synchronizacji ruchu wychodzącego wyeksportować obiekty, gdy obiektu metaverse zmiany, ale nie zostanie usunięta. Witaj celem synchronizacji ruchu wychodzącego jest tooevaluate, czy obiekty toometaverse zmiany wymagają aktualizacji toostaging obiektów w hello — obszary łączników. W niektórych przypadkach można zaktualizować powitalne zmiany mogą wymagać, że tymczasowe obiekty w samych spacji łącznika. Obiekty tymczasowe, które są zmieniane są oznaczone jako oczekujące eksportu, dzięki czemu można je wyeksportować obiekty. Obiekty są później wypychani toohello połączonego źródła danych podczas procesu eksportowania hello eksportu.

Synchronizacji ruchu wychodzącego ma trzy procesy:

* **Aprowizacja**
* **Cofanie zastrzegania**
* **Eksportowanie przepływu atrybutów**

Alokowania i anulowania alokowania są operacjami na poziomie obiektu. Cofanie zastrzegania zależy od tego, inicjowania obsługi, ponieważ tylko inicjowania obsługi administracyjnej może inicjować ją. Cofanie zastrzegania jest wyzwalane, gdy Inicjowanie obsługi administracyjnej usuwa hello powiązanie obiektu metaverse i obiektu eksportu.

Inicjowanie obsługi administracyjnej jest zawsze wyzwalane, gdy zmiany zostaną zastosowane tooobjects w magazynie metaverse hello. Podczas wprowadzania zmian obiektów toometaverse, aparatu synchronizacji można wykonać jedną z następujących zadań w ramach procesu udostępniania hello hello:

* Utwórz połączone obiekty, gdzie obiektu metaverse jest połączone tooa nowo utworzony obiekt eksportu.
* Zmień dołączonego do obiektu.
* Odłączenie łącza między obiektu metaverse i przejściowych obiekty, tworzenie odłączonym obiektu.

Jeśli Inicjowanie obsługi administracyjnej wymaga toocreate aparat synchronizacji jest nowy obiekt łącznika, hello przemieszczania obiektu metaverse hello toowhich obiektu jest połączony jest zawsze obiektu export, ponieważ hello obiekt nie istnieje jeszcze w hello połączonego źródła danych.

W przypadku inicjowania obsługi administracyjnej wymaga toodisjoin aparatu synchronizacji obiektu dołączonego do tworzenia obiektu odłączonym anulowania obsługi zostanie wywołany. Witaj anulowania obsługi procesu usuwa hello obiektu.

Podczas anulowania obsługi, usunięcie obiektu eksportu nie fizycznie usunąć hello obiektu. Witaj obiekt jest oznaczony jako **usunięte**, co oznacza operację usuwania tego hello są przygotowywane na powitania obiektu.

Przepływ atrybutu eksportu występuje także w procesie synchronizacji ruchu wychodzącego hello podobny sposób toohello importowania przepływu atrybutów występuje podczas synchronizacji ruchu przychodzącego. Przepływ atrybutu eksportu nastąpi tylko między metaverse i eksportowanie obiektów, które są połączone.

### <a name="export-process"></a>Proces eksportowania
W procesie eksportu hello aparatu synchronizacji sprawdza, czy wszystkie obiekty eksportu, które są oznaczone jako oczekujące eksportu w przestrzeni łącznika hello, a następnie wysyła aktualizacje toohello połączone źródła danych.

Hello aparatu synchronizacji można określić Powodzenie hello eksportu, ale wystarczająco nie może ustalić o ukończeniu procesu zarządzania tożsamościami hello. Zawsze można zmienić obiektów w hello połączonego źródła danych przez inne procesy. Ponieważ aparat synchronizacji nie ma trwałego połączenia toohello połączonego źródła danych, nie jest wystarczające toomake założenia dotyczące hello właściwości obiektu w hello połączonego źródła danych w oparciu jedynie powiadomienia pomyślnego eksportu.

Na przykład procesu w hello połączone źródła danych, można utworzyć kopię atrybutów obiektu hello zmiany tootheir oryginalnych wartości (to znaczy hello połączonego źródła danych można zastąpić wartości hello natychmiast po danych hello spoczywa limit aparatu synchronizacji i pomyślnie stosowane w hello połączonego źródła danych).

Magazyny aparatu synchronizacji Hello eksportować i importować informacje dotyczące każdego obiektu przemieszczania stanu. Jeśli wartości atrybutów hello, które są określone na liście dołączania atrybutu hello uległy zmianie od czasu ostatniego eksportu hello, hello magazynu importu i eksportu odpowiednio tooreact aparatu synchronizacji umożliwia stanu. Aparat synchronizacji używa hello importu procesu tooconfirm wartości atrybutów, które zostały wyeksportowane toohello połączonego źródła danych. Porównanie hello zaimportowane i wyeksportowane informacje opisane w następującej ilustracji hello umożliwia toodetermine aparatu synchronizacji czy eksportu hello zakończyła się powodzeniem lub jeśli wymaga toobe powtarzany.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Na przykład jeśli aparat synchronizacji eksportuje atrybutu C, która ma wartość 5, tooa połączone źródła danych, C = 5 są przechowywane w pamięci stan eksportu. Każdy dodatkowego eksportu dla tego obiektu wynikiem próby tooexport C = 5 toohello połączonego źródła danych ponownie, ponieważ aparat synchronizacji przyjęto założenie, że ta wartość nie została trwale zastosowane toohello obiektu (jeśli ostatnio zaimportowano inną wartość z hello połączone źródła danych). Hello eksportu pamięci są czyszczone po odebraniu podczas operacji importowania dla obiekt hello C = 5.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

