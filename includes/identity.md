Zarządzanie tożsamościami są równie ważne w chmurze publicznej, ponieważ istnieje lokalnie. Aby ułatwić z tym, Azure obsługuje kilku technologii tożsamości w innej chmurze. Te obejmują:

* Windows Server Active Directory (często nazywany po prostu AD) można uruchomić w chmurze przy użyciu maszyn wirtualnych utworzonych z maszynami wirtualnymi Azure. Takie podejście ma sens, podczas korzystania z usługi Azure rozszerzenie lokalnego centrum danych do chmury.
* Azure Active Directory umożliwia zapewniają Twojej użytkownikom logowanie jednokrotne do [oprogramowanie jako usługa (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) aplikacji. Firmy Microsoft Office 365 używa tej technologii, na przykład i aplikacje działające na platformie Azure lub innych platform chmury można jej również użyć.
* Aplikacje działające w chmurze lub lokalnie umożliwia Pozwalanie użytkownikom logowanie się za pomocą tożsamości z usługi Facebook, Google, Microsoft i innych dostawców tożsamości usługi Azure Active Directory kontroli dostępu.

W tym artykule opisano wszystkie trzy z tych opcji.

## <a name="table-of-contents"></a>Spis treści
* [Systemem Windows Server Active Directory w przypadku maszyn wirtualnych](#adinvm)
* [Za pomocą usługi Azure Active Directory](#ad)
* [Za pomocą kontroli dostępu w usłudze Azure Active Directory](#ac)

## <a name="adinvm"></a>Systemem Windows Server Active Directory w przypadku maszyn wirtualnych
System Windows Server AD w maszynach wirtualnych platformy Azure są podobne jak uruchomić je lokalnie. [Rysunek 1](#fig1) pokazuje typowym przykładem, jak wygląda.

![Azure Active Directory w maszynie wirtualnej](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>Rysunek 1: Usługi Active Directory systemu Windows Server można uruchomić na maszynach wirtualnych Azure podłączone do organizacji lokalnego centrum danych przy użyciu sieci wirtualnej platformy Azure.

W tym przykładzie AD systemu Windows Server jest uruchomiony na maszynach wirtualnych utworzonych przy użyciu maszyn wirtualnych platformy Azure, platformy technologię IaaS. Te maszyny wirtualne i kilka innych są pogrupowane w sieci wirtualnej podłączone do lokalnego centrum danych przy użyciu sieci wirtualnej platformy Azure. Wycina sieć wirtualną out grupy chmury maszyn wirtualnych, które współdziałają z sieci lokalnej za pośrednictwem połączenia wirtualnej sieci prywatnej (VPN). To umożliwia wykonanie tych maszyn wirtualnych platformy Azure wygląda jak po prostu inną podsieć w lokalnym centrum danych. Jak pokazano na rysunku, działają dwa z tych maszyn wirtualnych kontrolerów domeny systemu Windows Server AD. Innych maszyn wirtualnych w sieci wirtualnej może być uruchomiona aplikacji, takich jak SharePoint lub używane w inny sposób, takich jak do projektowania i testowania. W lokalnym centrum danych jest uruchomiona dwa kontrolery domeny systemu Windows Server AD.

Dostępnych jest kilka opcji nawiązywania połączeń z kontrolerami domeny w chmurze z uruchomione lokalnie:

* Wszystkie z nich należą do jednej domeny usługi Active Directory.
* Utwórz oddzielne AD domeny lokalnej i w chmurze, które są częścią tego samego lasu.
* Utwórz oddzielne lasów usługi AD w chmurze i lokalnie, a następnie połącz lasach przy użyciu relacji zaufania między lasami lub Windows Server Active Directory Federation Services (AD FS), które można również uruchomić na maszynach wirtualnych na platformie Azure.

Niezależnie od domyślny wybór, administrator upewnij się, że żądania uwierzytelniania od użytkowników lokalnych przejdź do chmury kontrolery domeny tylko wtedy, gdy jest to konieczne, ponieważ może być mniejsza niż sieci lokalnej jest łącze do chmury. Innym czynnikiem wziąć pod uwagę w chmurze łączenia i kontrolery domeny lokalnej jest ruch generowany przez funkcję replikacji. Kontrolery domeny w chmurze zazwyczaj są w ich własnej lokacji AD, dzięki czemu administrator można zaplanować, jak często odbywa się replikacja. Azure opłaty za ruch wysyłany poza centrum danych Azure, chociaż nie bajtów wysłanych w, które mogą wpłynąć na wybór replikacji administratora. Warto również wskazujące, że podczas Azure zapewniają obsługę własnego systemu nazw domen (DNS, Domain Name System), ta usługa nie ma funkcje wymagane przez usługę Active Directory (takich jak Obsługa rekordów dynamicznych DNS i SRV). W związku z tym systemem Windows Server AD na platformie Azure wymaga ustawienia własne serwery DNS w chmurze.

Systemem Windows Server AD w maszynach wirtualnych platformy Azure może być uzasadniona w kilku różnych sytuacjach. Oto kilka przykładów:

* Jeśli używasz usługi Azure Virtual Machines jako rozszerzenie własnego centrum danych, można uruchamiać aplikacje w chmurze, które wymagają lokalnych kontrolerów domeny do obsługi rzeczy, takich jak żądania zintegrowanego uwierzytelniania systemu Windows lub zapytań LDAP. Programu SharePoint, na przykład współdziała często z usługi Active Directory, a więc jest możliwość uruchamiania farmy programu SharePoint na platformie Azure przy użyciu lokalnego katalogu, konfigurowanie kontrolerów domeny w chmurze będzie znacznie poprawić wydajność. (Jest zdawać sobie sprawę, czy nie jest zawsze wymagane, jednak; dużo aplikacji można uruchomić pomyślnie w chmurze przy użyciu tylko kontrolery domeny z lokalnymi.)
* Załóżmy, że w biurze oddziału odległych brakuje zasobów, aby uruchomić własnych kontrolerów domeny. Obecnie jego użytkownicy muszą uwierzytelnić się na kontrolerach domeny z drugiej strony świecie — logowania są przetwarzane wolno. Uruchamianie usługi Active Directory na platformie Azure w bliżej centrum danych firmy Microsoft można przyspieszyć to bez konieczności więcej serwerów w biurze oddziału.
* Organizacja, która używa usługi Azure do odzyskiwania po awarii może obsługiwać niewielki zestaw aktywnych maszyn wirtualnych w chmurze, w tym kontrolerze domeny. Następnie można go przygotować można rozszerzyć tę lokację, w razie potrzeby przejąć błędów w innym miejscu.

Istnieją także inne możliwości. Na przykład nie masz wymagane do nawiązania połączenia lokalnego centrum danych systemu Windows Server AD w chmurze. Jeśli chcesz uruchomić farmy programu SharePoint, który obsłużył określonego zbioru użytkowników, na przykład wszystkich z nich będzie zalogować się wyłącznie z tożsamościami oparte na chmurze, lasu autonomiczny można utworzyć na platformie Azure. Jak użyć tej technologii, zależy od tego, jakie są cele. (Aby uzyskać szczegółowe wskazówki na temat używania systemu Windows Server AD z platformy Azure, [widoczną w tym miejscu](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx).)

## <a name="ad"></a>Za pomocą usługi Azure Active Directory
Jak aplikacje SaaS staną się bardziej popularne, pobierają one oczywistym pytaniem: jakiego rodzaju usługi katalogowej należy używać tych aplikacji opartej na chmurze? Odpowiedź firmy Microsoft na to pytanie jest usługa Azure Active Directory.

Istnieją dwie główne opcje dotyczące korzystania z tej usługi katalogowej w chmurze:

* Azure Active Directory osób i organizacji, które używają tylko aplikacji SaaS można traktować jako ich usługa katalogowa wyłącznie.
* Organizacje z systemem Windows Server Active Directory można połączyć katalog lokalny, ich do usługi Azure Active Directory, a następnie umożliwia zapewniają ich użytkownikom logowanie jednokrotne do aplikacji SaaS.

[Rysunek 2](#fig2) przedstawiono pierwszy te dwie opcje usługi Azure Active Directory w przypadku wszystkich, która jest wymagana.

![Azure Active Directory w maszynie wirtualnej](./media/identity/identity_02_AD.png)

<a name="fig2"></a>Rysunek 2: Usługi Azure Active Directory umożliwia organizacji użytkownikom logowanie jednokrotne do aplikacji SaaS, w tym usługi Office 365.

Jak pokazano na rysunku, usługi Azure AD to usługa wielodostępnej. Oznacza to, że jednocześnie może obsługiwać wiele różnych organizacji, przechowywania katalogu informacji o użytkownikach w każdej z nich. W tym przykładzie użytkownik w organizacji, A próbuje uzyskać dostęp do aplikacji SaaS. Ta aplikacja może być częścią usługi Office 365, takich jak SharePoint Online lub może być inny — aplikacje firmy Microsoft można również użyć tej technologii. Ponieważ usługi Azure AD obsługuje protokół SAML 2.0, wszystkie punkty, które wymaga od aplikacji jest możliwość interakcji przy użyciu tego branżowymi. (W rzeczywistości aplikacji, które używają usługi Azure AD można uruchomić w dowolnego centrum danych, a nie tylko centrum danych Azure.)

Proces rozpoczyna się, gdy użytkownik uzyskuje dostęp do aplikacji SaaS (krok 1). Aby używać tej aplikacji, użytkownik musi przedstawić token wystawiony przez usługę Azure AD.

Token ten zawiera informacje umożliwiające identyfikację użytkownika, i jest podpisany cyfrowo przez usługę Azure AD. Do uzyskania tokenu, użytkownik uwierzytelnia się do usługi Azure AD przez podanie nazwy użytkownika i hasła (krok 2). Następnie usługi Azure AD zwraca token on musi (krok 3).

Token ten zostanie przesłany do aplikacji SaaS (krok 4), który sprawdza podpis tokenu i używa jej zawartość (krok 5). Zwykle aplikacja będzie używać informacji o tożsamości, które zawiera token decyzji o tym, jakie informacje, które użytkownik ma zezwolenie na dostęp i być może w inny sposób.

Jeśli aplikacja wymaga więcej informacji na temat użytkownika niż to, co jest zawartych w tokenie, go to żądanie bezpośrednio z usługi Azure AD przy użyciu interfejsu API Azure AD Graph (krok 6). W pierwotnej wersji usługi Azure AD jest bardzo proste schematu katalogu: zawiera tylko użytkowników i grup oraz relacji między nimi. Aplikacje mogą używać tych informacji, aby dowiedzieć się więcej na temat połączeń między użytkownikami. Na przykład załóżmy, że aplikacja musi wiedzieć, który Menedżer tego użytkownika jest podjęcie decyzji, czy ma on mieć dostęp do niektórych fragmentów danych. Go to informacje, badając Azure AD za pomocą interfejsu API programu Graph.

Interfejsu API programu Graph używa zwykłej protokołu RESTful, dzięki czemu prostego do użycia z większości klientów, w tym urządzeń przenośnych. Interfejs API obsługuje również rozszerzenia zdefiniowane przez OData, dodanie czynności takich jak język kwerendy, aby umożliwić klientom dostęp do danych w sposób bardziej użyteczne. (Aby uzyskać więcej informacji na temat OData, zobacz [wprowadzenie OData](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf).) Ponieważ mogą zostać użyte interfejsu API programu Graph, aby dowiedzieć się więcej na temat relacji między użytkownikami, umożliwia aplikacji zrozumieć społecznościowych wykresu, który jest osadzony w schemacie usługi Azure AD dla konkretnej organizacji (czyli Dlaczego została wywołana interfejsu API programu Graph). I do samodzielnego uwierzytelnienia usługi Azure AD żądań interfejsu API programu Graph, aplikacja korzysta z protokołu OAuth 2.0.

Jeśli organizacja nie korzysta z usługi Active Directory systemu Windows Server — nie ma lokalnych serwerów ani domeny -, a jedynie zależy od aplikacji w chmurze, które używają usługi Azure AD, za pomocą tylko tej katalogiem w chmurze pozwoli uzyskać firmy użytkownicy logowania jednokrotnego do wszystkich z nich. Jeszcze podczas tego scenariusza pobiera częściej codziennie, większość organizacji używa nadal domenami lokalnymi utworzone za pomocą usługi Active Directory systemu Windows Server. Usługa Azure AD ma rolę przydatne do odtwarzania tutaj również jako [rysunek 3](#fig3) zawiera.

![Azure Active Directory w maszynie wirtualnej](./media/identity/identity_03_AD.png)
<a id="fig3"></a>rysunek 3: organizacja może tworzyć federacje Windows Server Active Directory z usługi Azure Active Directory, aby zapewnić jego użytkownikom logowanie jednokrotne do aplikacji SaaS.

W tym scenariuszu użytkownik w organizacji B chce uzyskać dostęp do aplikacji SaaS. Przed to zrobi, Administratorzy katalogu organizacji należy ustanowić relację federacji z usługą Azure AD za pomocą usług AD FS, jak przedstawiono na rysunku. Administratorzy te należy również skonfigurować synchronizację danych między organizacji lokalnego systemu Windows Server AD i Azure AD. To automatycznie kopiuje użytkowników i grupy informacji z katalogu lokalnego do usługi Azure AD. Zwróć uwagę, dzięki temu: W rzeczywistości organizacji stanowi rozszerzenie jego katalogu lokalnego do chmury. Połączenie systemu Windows Server AD i Azure AD w ten sposób zapewnia organizacji usługi katalogowej, którymi można zarządzać w pojedynczą jednostkę, przy zachowaniu wpływ zarówno lokalnie, jak i w chmurze.

Aby korzystać z usługi Azure AD, użytkownik najpierw loguje się do swojej lokalnej domeny usługi Active Directory w zwykły sposób (krok 1). Kiedy użytkownik próbuje uzyskać dostęp do aplikacji SaaS (krok 2), wyniki procesu federacji w usłudze Azure AD wystawiania jej tokenu dla tej aplikacji (krok 3). (Aby uzyskać więcej informacji na temat działania federacyjnego zobacz [tożsamości opartego na oświadczeniach dla systemu Windows: technologii i scenariuszy](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx).) Ponieważ przed, token zawiera informacje umożliwiające identyfikację użytkownika, które jest podpisany cyfrowo przez usługę Azure AD. Token ten zostanie przesłany do aplikacji SaaS (krok 4), który sprawdza podpis tokenu i używa jej zawartość (krok 5). I jest w poprzednim scenariuszu SaaS aplikacji można użyć interfejsu API programu Graph, aby dowiedzieć się więcej informacji na temat tego użytkownika, jeśli to konieczne (krok 6).

Obecnie usługi Azure AD nie jest całkowite zastąpienie lokalnej w systemie Windows Server AD. Jak już wspomniano katalogiem w chmurze ma znacznie prostsze schemat, a także brakuje elementy, takie jak zasady grupy, możliwość przechowywania informacji o maszynach i obsługę protokołu LDAP. (W rzeczywistości maszynę z systemem Windows nie można skonfigurować tak, aby umożliwić użytkownikom zalogowanie się do niego przy użyciu żadnej zawartości ale usługi Azure AD — nie jest obsługiwanym scenariuszem.) Zamiast tego początkowe cele usługi Azure AD obejmują, umożliwiając enterprise użytkownikom dostępu do aplikacji w chmurze bez zachowania oddzielne logowania i zwalnianie lokalnych administratorów katalogu ręcznie synchronizacją ich katalogu lokalnego z każdym Ich organizacja korzysta z aplikacji SaaS. Wraz z upływem czasu jednak oczekiwać, że ta usługa katalogowa chmury w celu rozwiązania szerszego zakresu scenariuszy.

## <a name="ac"></a>Za pomocą kontroli dostępu w usłudze Azure Active Directory
Tożsamość oparta na chmurze technologii może służyć do rozwiązuje wiele problemów z. Azure Active Directory pozwala organizacji użytkowników logowania jednokrotnego do wielu aplikacji SaaS, na przykład. Ale można też używać technologii tożsamości w chmurze w inny sposób.

Załóżmy na przykład, aplikacja chce zezwolić użytkownikom na jego Zaloguj się za pomocą tokenów wystawionych przez wiele *dostawcy tożsamości (IdPs)*. Wielu dostawców tożsamości różnych istnieje już dziś, Facebook, Google, Microsoft i innych osób, w tym i aplikacje często powiadomić użytkowników, zaloguj się przy użyciu jednej z tych tożsamości. Dlaczego należy odblokowane aplikacji do obsługi własną listę użytkowników i hasła, gdy zamiast tego mogą polegać na tożsamości, które już istnieją? Akceptowanie istniejącej tożsamości sprawia, że życia prostsze zarówno dla użytkowników, którzy mają jedną nazwę użytkownika i hasło do zapamiętania i dla użytkowników, którzy tworzenia aplikacji, które nie są już potrzebne do obsługi własnych list nazwy użytkowników i hasła.

Jednak podczas każdego dostawcy tożsamości problemy z określonego rodzaju token, tokeny te nie są standardowe — IdP każdy ma własny format. Ponadto informacje w tych tokenów również nie jest standard. Aplikacja, która pragnie zaakceptować tokeny wystawione przez, powiedz, Facebook, Google i Microsoft stoi z żądaniem zapisu unikatowy kod do obsługi każdego z tych formatach.

Ale Dlaczego warto to zrobić? Dlaczego nie zamiast tego utworzyć pośrednik mogą generować jeden format tokenu z reprezentację typowych informacji o tożsamości? Takie podejście spowodowałoby życia prostsze dla deweloperów, którzy tworzą aplikacje, ponieważ teraz muszą obsługiwać tylko jeden rodzaj tokenu. Azure kontroli dostępu Active Directory działanie dokładnie, zapewniając pośrednik w chmurze do pracy z różnymi tokenów. [Rysunek 4](#fig4) pokazuje, jak to działa

![Azure Active Directory w maszynie wirtualnej](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>rysunek 4: Azure Active Directory kontrola dostępu ułatwia dla aplikacji, aby akceptować tożsamości tokenów wystawionych przez dostawców innej tożsamości.

Proces rozpoczyna się, gdy użytkownik próbuje uzyskać dostęp do aplikacji z przeglądarki. Aplikacja przekierowuje jej IdP jej wybór (i aplikacji również zaufania). Użytkownik jest uwierzytelniany sobie tego IdP takich jak przez wprowadzenie nazwy użytkownika i hasła (krok 1) i IdP zwraca token zawierający informacje o jego (krok 2).

Jak pokazano na rysunku, kontroli dostępu obsługuje wiele różnych IdPs oparte na chmurze, w tym kont utworzonych przez Google, Yahoo, Facebook, Microsoft (znanego wcześniej jako identyfikator Windows Live ID) i dowolnego dostawcy uwierzytelniania OpenID. Obsługuje ona również tożsamości utworzone za pomocą usługi Azure Active Directory i przy użyciu federacji z usługami AD FS, Windows Server Active Directory. Celem jest, aby pokrywał tożsamości najczęściej używanych dzisiaj, czy są one wystawiony przez IdPs w chmurze lub lokalnie.

Po przeglądarki użytkownika ma token IdP z jej wybranych dostawców tożsamości, wysyła ten token do kontroli dostępu (krok 3). Kontrola dostępu weryfikuje token, upewniając się, że jej naprawdę został wystawiony przez ten dostawców tożsamości, a następnie tworzy nowy token zgodnie z regułami, które zostały zdefiniowane dla tej aplikacji. Podobnie jak Azure Active Directory kontroli dostępu jest usługą wielodostępne, ale dzierżawcami są aplikacje, a nie w organizacji klienta. Każdej aplikacji można uzyskać jego własnej przestrzeni nazw, jak przedstawiono na rysunku, a następnie można określić różne zasady dotyczące autoryzacji i inne.

Te zasady umożliwiają definiowanie sposobu transformacji tokeny od różnych IdPs w tokenie kontroli dostępu administratora każdej aplikacji. Na przykład użycie różnych IdPs różne typy służący do reprezentowania nazwy użytkownika, zasady kontroli dostępu można przekształcać wszystkich tych do typowych wpisz nazwę użytkownika. Kontrola dostępu następnie wysyła ten nowy token z powrotem do przeglądarki (krok 4), który przesyła do aplikacji (krok 5). Gdy ma token kontroli dostępu, aplikacji sprawdza, czy ten token naprawdę został wystawiony przez kontroli dostępu, a następnie używa tych informacji, że zawiera on (krok 6).

Podczas tego procesu może wydawać się nieco skomplikowany, faktycznie umożliwia życia znacznie prostsze Twórca aplikacji. Zamiast obsługi różnych tokenów zawierających różne informacje, aplikacja może akceptować tożsamości wystawiony przez wielu dostawców tożsamości podczas odbierania nadal tylko jednego tokenu znanych informacji. Ponadto, a nie wymagają każdej aplikacji można skonfigurować różne IdPs zaufania, te relacje zaufania zamiast tego są obsługiwane przez funkcję Kontrola dostępu — aplikacji tylko muszą ufać.

Warto wskazujące, że nie ma kontroli dostępu jest powiązany z systemu Windows - równie dobrze może zostać wykorzystana przez aplikację systemu Linux, akceptowane tylko tożsamości Google i Facebook. A nawet kontroli dostępu jest częścią rodziny usługi Azure Active Directory, można traktować go jako całkowicie różne usługi z co zostało opisane w poprzedniej sekcji. Podczas pracy obu tych technologii z tożsamością, odnoszą się do zupełnie różne problemy (chociaż Microsoft ma dana oczekuje zintegrować dwa w pewnym momencie).

Praca z tożsamości jest ważne dla niemal każdej aplikacji. Celem kontroli dostępu jest ułatwia deweloperom tworzenie aplikacji, które akceptować tożsamości z tożsamości różnych dostawców. Umieszczenie tej usługi w chmurze, firma Microsoft udostępniła go do aplikacji działających na dowolnej platformie.

## <a name="about-the-author"></a>Informacje o autorze
Chappell Dominik jest główną Chappell z & stowarzyszonych [www.davidchappell.com](http://www.davidchappell.com) w Warszawie, Polski.

