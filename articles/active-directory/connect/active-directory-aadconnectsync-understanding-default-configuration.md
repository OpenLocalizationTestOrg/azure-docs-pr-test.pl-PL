---
title: "Synchronizacja programu Azure AD Connect: opis hello domyślnej konfiguracji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello domyślnej konfiguracji synchronizacji Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Synchronizacja programu Azure AD Connect: opis hello domyślnej konfiguracji
W tym artykule opisano reguły konfiguracji out-of-box hello. Dokumenty go hello zasady i wpływ hello konfiguracji tych reguł. On również przeprowadzi Cię przez hello domyślnej konfiguracji synchronizacji usługi Azure AD Connect. Celem Hello jest czytnika hello rozumie, jak model konfiguracji hello, o nazwie aprowizacją deklaratywną działa w przykładzie rzeczywistych. W tym artykule założono, że zainstalowano i skonfiguruj synchronizację programu Azure AD Connect przy użyciu Kreatora instalacji hello.

Szczegóły hello toounderstand model konfiguracji hello, przeczytaj [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Out-of-box reguły z lokalnymi tooAzure AD
Witaj następujących wyrażeń znajduje się w konfiguracji out-of-box hello.

### <a name="user-out-of-box-rules"></a>Reguły out-of-box użytkownika
Te zasady mają zastosowanie również typ obiektu iNetOrgPerson toohello.

Obiekt user muszą spełniać powitania po toobe synchronizowane:

* Musi mieć sourceAnchor.
* Po hello obiekt został utworzony w usłudze Azure AD, a następnie sourceAnchor nie można zmienić. Jeśli wartość hello jest zmienione lokalnymi, obiekt hello zatrzymuje synchronizowanie do momentu zmiany hello sourceAnchor wstecz tooits poprzedniej wartości.
* Musi mieć atrybut accountEnabled (userAccountControl) hello wypełnione. Z lokalnej usługi Active Directory ten atrybut jest zawsze obecne i wypełnione.

następujące obiekty użytkownika Hello są **nie** synchronizowane tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Upewnij się, wiele obiektów out-of-box w usłudze Active Directory, takie jak hello wbudowanego konta administratora, nie są zsynchronizowane.
* `IsPresent([sAMAccountName]) = False`. Upewnij się, że obiekty użytkownika z atrybutem nie sAMAccountName nie są zsynchronizowane. Ten przypadek tylko praktycznie się stanie w domenie uaktualnienia z NT4.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Nie Synchronizuj hello konto usługi używane przez synchronizacja programu Azure AD Connect i jego wcześniejsze wersje.
* Nie Synchronizuj kont serwera Exchange, które nie będzie działać w programie Exchange Online.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Nie są synchronizowane obiekty, które nie będzie działać w programie Exchange Online.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Ta maska bitowa (& H21C07000) czy odfiltrowywania hello następujące obiekty:
  * Folder publiczny z włączoną obsługą poczty
  * System towarzyszącej skrzynki pocztowej
  * Skrzynka pocztowa bazy danych skrzynki pocztowej (Skrzynka pocztowa systemu)
  * Uniwersalna grupa zabezpieczeń (nie odnoszą się do użytkownika, ale jest stosowany w przypadku starszych powodów)
  * Grupa uniwersalna inne niż (nie odnoszą się do użytkownika, ale jest stosowany w przypadku starszych powodów)
  * Plan skrzynki pocztowej
  * Skrzynka pocztowa odnajdywania
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Nie Synchronizuj wszystkie obiekty ofiara replikacji.

Zastosuj reguły atrybutu Hello:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. Atrybut sourceAnchor Hello nie przyczynił się on z połączoną skrzynkę pocztową. Zakłada się, że jeśli znaleziono połączoną skrzynkę pocztową hello własnego konta jest dołączony później.
* Exchange powiązane atrybuty są synchronizowane tylko, jeśli hello atrybutu **mailNickName** ma wartość.
* W przypadku wielu lasów, w następującej kolejności hello są używane atrybuty:
  1. Atrybuty powiązane w toosign (na przykład userPrincipalName) są tworzone z lasu hello z włączonym kontem.
  2. Atrybuty, które znajdują się w wymiany usługi GAL (globalna lista adresów) są tworzone z lasu hello ze skrzynką pocztową programu Exchange.
  3. W przypadku nieodnalezienia nie skrzynek pocztowych, te atrybuty mogą pochodzić z dowolnym lesie.
  4. Exchange dotyczące atrybutów (techniczne atrybutów nie są widoczne w hello usługi GAL) są tworzone z lasu hello gdzie `mailNickname ISNOTNULL`.
  5. Jeśli istnieje wiele lasów, które będą spełniać jeden z tych zasad, a następnie hello tworzenia kolejności (Data/godzina) hello łączników (lasów) jest używane toodetermine las, który wspiera hello atrybutów.

### <a name="contact-out-of-box-rules"></a>Skontaktuj się z reguł out-of-box
Skontaktuj się z pomocą obiektów muszą spełniać powitania po toobe synchronizacji:

* Skontaktuj się z Hello musi być włączoną obsługą poczty. Sprawdza z hello następujące reguły:
  * `IsPresent([proxyAddresses]) = True)`. Atrybut proxyAddresses Hello powinno zostać zapełnione.
  * Atrybut proxyAddresses hello lub atrybut poczty hello można znaleźć podstawowego adresu e-mail. Witaj obecności @ jest używane tooverify, że zawartość hello jest adres e-mail. Jeden z tych dwóch reguł musi być ocenione tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. Istnieje już wpis z "SMTP:", a jeśli istnieje, można @ można znaleźć w ciągu hello?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. Witaj atrybut poczty wypełnione i jeśli tak jest, można @ można znaleźć w ciągu hello?

następujące obiekty kontaktów Hello są **nie** synchronizowane tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Upewnij się, skontaktuj się z pomocą obiektów oznaczone jako krytyczne są synchronizowane. Nie powinny być dowolny z konfiguracji domyślnej.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Te obiekty nie działają w usłudze Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Nie Synchronizuj wszystkie obiekty ofiara replikacji.

### <a name="group-out-of-box-rules"></a>Grupa reguł out-of-box
Obiekt grupy muszą spełniać powitania po toobe synchronizacji:

* Musi mieć mniej niż 50 000 członków. Ta liczba jest hello liczby elementów członkowskich grupy lokalne powitania.
  * Jeśli przed synchronizacji hello rozpoczyna się po raz pierwszy, ma więcej członków, hello grupy nie jest zsynchronizowany.
  * Jeśli z rosnąć hello liczby elementów członkowskich, gdy został utworzony, następnie po osiągnięciu 50 000 członków, zatrzymuje, synchronizowanie, dopóki liczba członkostwa hello jest ponownie niższy niż 50 000.
  * Uwaga: liczba 50 000 członkostwa hello również są wymuszane przez usługę Azure AD. Nie masz grupy może toosynchronize o większej liczby elementów członkowskich nawet wtedy, gdy zmodyfikować lub usunąć tę regułę.
* Jeśli grupa hello jest **grupy dystrybucji**, a następnie włączoną obsługę poczty musi mieć również. Zobacz [skontaktuj się z reguł out-of-box](#contact-out-of-box-rules) dla tej reguły jest wymuszana.

następujące obiekty grupy Hello są **nie** synchronizowane tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Upewnij się, wiele obiektów out-of-box w usłudze Active Directory, takie jak hello wbudowanej grupy Administratorzy, nie są zsynchronizowane.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Starsze grupy używane przez narzędzie DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Grupa roli.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Nie Synchronizuj wszystkie obiekty ofiara replikacji.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>Reguły out-of-box ForeignSecurityPrincipal
FSP są sprzężone za "any" (\*) obiektu hello metaverse. W rzeczywistości tego przyłączenia odbywa się tylko dla użytkowników i grup zabezpieczeń. Ta konfiguracja temu członkostwa w różnych lasach są rozwiązany i poprawnie reprezentowana w usłudze Azure AD.

### <a name="computer-out-of-box-rules"></a>Reguły out-of-box komputera
Obiekt komputera musi spełniać powitania po toobe synchronizacji:

* `userCertificate ISNOTNULL`. Tylko komputery z systemem Windows 10 wypełniania tego atrybutu. Wszystkie obiekty komputerów z wartością w tym atrybucie są synchronizowane.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Opis scenariusza reguły out-of-box hello
W tym przykładzie użyto wdrożenie z jednym lesie konta (A), jeden las zasobów (R) i jeden katalog usługi Azure AD.

![Obraz z opis scenariusza](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

W tej konfiguracji zakłada się, że jest włączone konto w lesie konta hello i wyłączonych kont w lesie zasobów hello z połączoną skrzynkę pocztową.

Naszym celem z konfiguracji domyślnej hello jest:

* Atrybuty powiązane toosign w są synchronizowane z lasu hello z kontem hello włączone.
* Atrybuty, które znajdują się w hello usługi GAL (globalna lista adresów) są synchronizowane z lasu hello z hello skrzynki pocztowej. W przypadku nieodnalezienia nie skrzynkę pocztową, jest używany innym lesie.
* Jeśli zostanie znaleziony połączoną skrzynkę pocztową, hello połączonego konta włączone musi zostać znaleziony na powitania obiektu toobe wyeksportowane tooAzure AD.

### <a name="synchronization-rule-editor"></a>Edytor reguł synchronizacji
Hello konfiguracji można było wyświetlać i modyfikować narzędziem hello Edytor reguł synchronizacji (SRE) i tooit skrótów znajduje się w hello start menu.

![Ikona Edytor reguł synchronizacji](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Witaj SRE jest narzędziem do zestawu zasobów i zainstalować go z synchronizacji Azure AD Connect. toostart stanie toobe, musi być członkiem grupy ADSyncAdmins hello. Podczas uruchamiania, zobacz podobny do następującego:

![Reguły synchronizacji ruchu przychodzącego](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

W tym okienku zobacz temat wszystkie reguły synchronizacji utworzone dla danej konfiguracji. Każdy wiersz w tabeli hello jest jedna reguła synchronizacji. toohello pozostanie w obszarze typów reguł, hello są wyświetlane dwa różne typy: przychodzących i wychodzących. Ruchu przychodzącego i wychodzącego jest z widoku hello hello metaverse. Są głównie będzie toofocus na powitania reguły w tym omówieniu dla ruchu przychodzącego. Hello właściwą listę reguł synchronizacji jest zależna od hello wykryto schematu w usłudze AD. Witaj ilustracji powyżej hello konta lasu (fabrikamonline.com) nie ma żadnych usług, takich jak Exchange i Lync, a żadne reguły synchronizacji zostały utworzone dla tych usług. Jednak w lesie zasobów hello (res.fabrikamonline.com) można znaleźć reguły synchronizacji dla tych usług. zawartość Hello reguł hello jest różne w zależności od wersji hello wykryte. Na przykład w przypadku wdrożenia z programu Exchange 2013 istnieje więcej przepływów atrybutów skonfigurowane niż w Exchange 2010 2007.

### <a name="synchronization-rule"></a>Reguły synchronizacji
Reguła synchronizacji jest obiekt konfiguracji przy użyciu zestawu atrybutów przepływu po spełnieniu warunku. Możliwe jest również używane toodescribe jak obiektu w przestrzeni łącznika jest obiektem tooan powiązane w magazynie metaverse hello, znany jako **sprzężenia** lub **odpowiada**. Witaj reguły synchronizacji mają pierwszeństwo wskazujące, jak są one powiązane tooeach innych. Reguła synchronizacji z niższą wartość liczbową ma wyższy priorytet i powoduje konflikt przepływu atrybutu, wyższy priorytet wins hello rozwiązywania konfliktów.

Na przykład przyjrzeć się hello reguły synchronizacji **w z usługi Active Directory — AccountEnabled użytkownika**. Oznacz ten wiersz w hello SRE i wybierz **Edytuj**.

Ponieważ ta reguła jest regułą out-of-box, pojawi się ostrzeżenie podczas otwierania hello reguły. Nie należy wprowadzać dowolne [zmiany reguły tooout-of-box](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), więc użytkownik jest pytany, czy zamiaru. W takim przypadku tylko ma tooview hello reguła. Wybierz **nr**.

![Synchronizacja ostrzeżenia reguły](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Reguła synchronizacji ma cztery sekcje konfiguracji: opis zakresu filtru, reguły sprzężenia i przekształcenia.

#### <a name="description"></a>Opis
Pierwsza sekcja Hello zawiera podstawowe informacje, takie jak nazwa i opis.

![Opis elementu karcie Edytor reguł synchronizacji ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

Można również znaleźć informacje o tym, które system połączony, ta zasada jest powiązany, którego typu obiektu w hello połączony system, w których on obowiązuje i hello typ obiektu metaverse. Typ obiektu metaverse Hello jest zawsze osoby niezależnie od tego, gdy typ obiektu źródłowego hello jest użytkownik, iNetOrgPerson lub skontaktuj się z pomocą. Typ obiektu metaverse Hello nigdy nie należy zmieniać, aby została utworzona jako typu ogólnego. tooJoin, StickyJoin lub udostępnić można ustawić Hello typu łącza. To ustawienie działa razem z sekcji dołączyć reguły hello i jest objęte później.

Można również sprawdzić, czy ta reguła synchronizacji jest używana do synchronizacji haseł. Jeśli użytkownik jest w zakresie dla tej reguły synchronizacji, hello hasła są synchronizowane z lokalną toocloud (przy założeniu, że została włączona funkcja synchronizacji hasła hello).

#### <a name="scoping-filter"></a>Filtr zakresów
Hello filtru zakresu dla sekcji jest tooconfigure używane, gdy ma zostać zastosowana reguła synchronizacji. Ponieważ nazwę hello hello reguły synchronizacji poszukujesz wskazuje powinny być stosowane tylko włączonych użytkowników, zakres hello jest skonfigurowany tak atrybutu hello AD **userAccountControl** może nie mieć hello bitu 2. Aparat synchronizacji hello znajduje użytkownika w usłudze AD, zastosowanie tej synchronizacji regułę, gdy **userAccountControl** ustawiono wartość dziesiętna toohello 512 (włączone zwykłego użytkownika). Nie ma zastosowania reguły hello, gdy użytkownik hello ma **userAccountControl** ustawić too514 (wyłączone zwykłego użytkownika).

![Określanie zakresu kartę w edytorze reguły synchronizacji ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

Filtr zakresu Hello ma grup i klauzule, które mogą być zagnieżdżone. Wszystkie klauzule wewnątrz grupy muszą być spełnione tooapply reguły synchronizacji. Po zdefiniowaniu wiele grup co najmniej jedną grupę, muszą być spełnione dla hello tooapply reguły. Oznacza to operatora logicznego OR jest obliczane między grupami i logicznych i jest obliczane w grupie. Przykładem takiej konfiguracji można znaleźć w hello reguła synchronizacji ruchu wychodzącego **się tooAAD — Join grupy**. Istnieje kilka grup filtru synchronizacji, na przykład jeden dla grup zabezpieczeń (`securityEnabled EQUAL True`) i jeden dla grup dystrybucyjnych (`securityEnabled EQUAL False`).

![Określanie zakresu kartę w edytorze reguły synchronizacji ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Ta reguła jest używana toodefine, które grupy powinny być elastycznie tooAzure AD. Grupy dystrybucji muszą być zsynchronizowane z usługą Azure AD toobe włączoną obsługę poczty, ale dla grup zabezpieczeń wiadomości e-mail nie jest wymagana.

#### <a name="join-rules"></a>Dołącz zasady
sekcja trzeci Hello jest używany tooconfigure powiązań tooobjects w magazynie metaverse hello obiektów w hello przestrzeni łącznika. Witaj reguła sprawdzono wcześniej nie ma żadnej konfiguracji w przypadku dołączenia reguł, dlatego zamiast tego są toolook będzie w **w z usługi Active Directory — użytkownik przyłączyć**.

![Dołącz kartę reguły w edytorze reguły synchronizacji ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

zawartość Hello hello sprzężenia reguły zależy od hello dopasowania opcji wybranej w Kreatorze instalacji hello. Reguła ruchu przychodzącego oceny hello rozpoczyna się od obiektu w przestrzeni łącznika źródła hello i każdej grupy w regułach sprzężenia hello są oceniane w sekwencji. Jeśli obiekt źródłowy jest obliczane toomatch, dokładnie jeden obiekt w hello metaverse przy użyciu jednej reguły sprzężenia hello, obiekty hello są przyłączone. Jeśli zostały ocenione wszystkie reguły i nie ma dopasowania, hello typu łącza na stronie z opisem hello jest używany. Jeśli ta konfiguracja jest ustawiona zbyt**udostępniania**, a następnie w celu hello, hello metaverse jest tworzony nowy obiekt. tooprovision nowe metaverse toohello obiektu jest nazywane również zbyt**projektu** metaverse toohello obiektu.

raz oceniane są tylko Hello sprzężenia reguły. Obiekt miejsca łącznika i obiektu metaverse są połączone, pozostają połączone tak długo, jak zakres hello hello reguła synchronizacji jest nadal spełnione.

Podczas oceny zasad synchronizacji, tylko jedna reguła synchronizacji z zdefiniowanych reguł sprzężenia musi być w zakresie. W przypadku znalezienia wielu reguł synchronizacji przy użyciu reguł sprzężenia dla jednego obiektu, jest zgłaszany błąd. Z tego powodu hello najlepszym rozwiązaniem jest zdefiniowana tylko jedna reguła synchronizacji z sprzężenia, jeśli wiele reguł synchronizacji znajdują się w zakresie dla obiekt toohave. W konfiguracji out-of-box hello synchronizacji usługi Azure AD Connect, te reguły można można znaleźć, sprawdzając nazwę hello i znaleźć wyrazem hello **Join** końcu hello hello nazwy. Reguła synchronizacji nie zdefiniowano żadnych reguł sprzężenia stosuje przepływów atrybutów hello innych reguł synchronizacji połączone obiekty hello lub udostępniane nowego obiektu w celu hello.

Jeśli przyjrzymy się obraz powitania powyżej, można wyświetlić tej regule hello próbuje toojoin **objectSID** z **msExchMasterAccountSid** (Exchange) i **msRTCSIP-OriginatorSid** () Lync), która jest Oczekujemy w topologii lasu zasobów dla konta. Znajdź hello regułę tej samej we wszystkich lasach. Witaj zakłada się, że w każdym lesie może być lasu konto lub zasobu. Ta konfiguracja działa także jeśli kont na żywo w jednym lesie, które nie mają toobe przyłączony.

#### <a name="transformations"></a>Przekształcenia
Witaj przekształcania sekcja definiuje wszystkie przepływy atrybutów stosowane toohello obiektu docelowego w przypadku obiektów hello są łączone i spełnieniu hello zakresu filtru. Cofnięcie toohello **w z usługi Active Directory — AccountEnabled użytkownika** reguły synchronizacji, można znaleźć hello następujące przekształcenia:

![Przekształcenia karcie Edytor reguł synchronizacji ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput tej konfiguracji w kontekście we wdrożeniu lasu zasobów konta jest oczekiwany toofind włączone konto w lesie konta hello i wyłączonych kont w zasobie hello lasu z ustawieniami programu Exchange i usługi Lync. Hello reguły synchronizacji poszukujesz zawiera atrybuty hello wymagane do logowania i te atrybuty powinny przepływać z hello lasu w przypadku, gdy jest włączone konto. Te przepływy atrybutów są umieszczane razem w jednej reguły synchronizacji.

Przekształcenie może mieć różne typy: stała, bezpośredni i wyrażenie.

* Stały przepływ zawsze przepływ wartości zapisane na stałe. W przypadku hello powyżej, zawsze ustawia wartości hello **True** atrybut metaverse hello o nazwie **accountEnabled**.
* Bezpośrednie przepływu zawsze przepływa hello wartość atrybutu hello w atrybut target toohello hello źródła jako — jest.
* trzeci typ przepływu Hello jest wyrażeniem i umożliwia bardziej zaawansowane konfiguracje.

Język wyrażeń Hello jest VBA (Visual Basic for Applications), to osoby z doświadczeniem pakietu Microsoft Office lub VBScript rozpozna hello formatu. Atrybuty są ujęte w nawiasy kwadratowe, [attributeName]. Atrybut nazwy i nazwy funkcji jest rozróżniana wielkość liter, ale hello Edytor reguł synchronizacji ocenia wyrażenia hello i podaj ostrzeżenie, jeśli wyrażenie hello jest nieprawidłowe. Wszystkie wyrażenia są wyrażane w jednym wierszu z zagnieżdżonych funkcji. tooshow hello power hello konfiguracji języka, w tym miejscu jest hello przepływu dla pwdLastSet, ale dodatkowe komentarze wstawione:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Zobacz [opis deklaratywne inicjowania obsługi administracyjnej wyrażenia](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) uzyskać więcej informacji na temat hello język wyrażeń dla przepływów atrybutów.

### <a name="precedence"></a>Priorytet
Teraz przeglądał niektórych poszczególne reguły synchronizacji, ale zasady hello współdziałają ze sobą w konfiguracji hello. W niektórych przypadkach wartość atrybutu jest składa się z wielu toohello reguły synchronizacji tego samego atrybutu docelowego. W takim przypadku pierwszeństwo atrybutów jest używane toodetermine atrybut, którego wins. Na przykład sprawdzić hello atrybut sourceAnchor. Ten atrybut jest ważne atrybutu toobe stanie toosign w tooAzure AD. Dla tego atrybutu w dwie różne reguły synchronizacji, można znaleźć przepływu atrybutu **w z usługi Active Directory — AccountEnabled użytkownika** i **w z usługi Active Directory — typowe użytkownika**. Powodu tooSynchronization pierwszeństwo atrybutu sourceAnchor hello jest przyczyniły się do lasu hello z włączonym kontem najpierw w przypadku kilku obiektu metaverse toohello połączone obiekty. Jeśli nie ma żadnych kont włączone, a następnie używa aparatu synchronizacji hello hello reguły synchronizacji wychwytywania **w z usługi Active Directory — typowe użytkownika**. Taka konfiguracja powoduje, że nawet w przypadku konta, które są wyłączone, jest nadal sourceAnchor.

![Reguły synchronizacji ruchu przychodzącego](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Witaj pierwszeństwa reguły synchronizacji jest ustawiona w grupach przez Kreatora instalacji hello. Wszystkie reguły w grupie mają hello tej samej nazwy, ale są połączone toodifferent połączone katalogami. Kreator instalacji Hello daje reguły hello **w z usługi Active Directory — użytkownik przyłączyć** najwyższy priorytet i iteracje przez wszystkie połączone AD katalogów. Następnie kontynuuje hello dalej grup reguł w preferowanej kolejności. W grupie reguły hello są dodawane w powitalne kolejności hello łączników zostały dodane w Kreatorze hello. Jeśli innego łącznika zostanie dodany za pomocą Kreatora hello, zostaną ponownie uporządkowane hello reguły synchronizacji i reguły hello nowego łącznika są wstawiane ostatnio w każdej grupie.

### <a name="putting-it-all-together"></a>Składanie wszystkiego razem
Teraz wiemy wystarczająco o toobe toounderstand stanie reguły synchronizacji, jak konfiguracji hello współpracuje z hello różne reguły synchronizacji. Podczas przeglądania użytkownika i hello atrybuty, które są zamieszczone toohello metaverse, hello reguły są stosowane w następującej kolejności hello:

| Nazwa | Komentarz |
|:--- |:--- |
| W z usługi Active Directory — sprzężenia użytkownika |Reguła łączenia obiektów miejsca metaverse łącznika. |
| W z usługi Active Directory — UserAccount włączone |Atrybuty wymagane do logowania tooAzure AD i Office 365. Chcemy tych atrybutów z konta hello włączone. |
| W z usługi Active Directory — typowe użytkownika z programu Exchange |Atrybuty w hello globalnej liście adresowej. Przyjęto założenie, że jakości danych hello jest najlepsze w lesie hello, gdzie ma znaleźć hello skrzynki pocztowej użytkownika. |
| W z usługi Active Directory — typowe użytkownika |Atrybuty w hello globalnej liście adresowej. W przypadku, gdy nie znaleziono skrzynki pocztowej, dowolnego dołączonego do obiektu może przyczynić się wartość atrybutu hello. |
| W z usługi Active Directory — Exchange użytkownika |Istnieje tylko jeśli wykryto programu Exchange. Przepływ wszystkie atrybuty Exchange infrastruktury. |
| W z usługi Active Directory — Lync użytkownika |Istnieje tylko jeśli wykryto Lync. Przepływ wszystkie atrybuty Lync infrastruktury. |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o model konfiguracji hello w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Dowiedz się więcej o hello język wyrażeń w [opis deklaratywne inicjowania obsługi administracyjnej wyrażenia](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Kontynuuj czytanie, jak działa hello out-of-box konfiguracji w [opis użytkowników i kontaktów](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Zobacz, jak zmienić przy użyciu aprowizacją deklaratywną w toomake praktyczny [jak toomake toohello zmiany domyślną konfigurację](active-directory-aadconnectsync-change-the-configuration.md).

**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

