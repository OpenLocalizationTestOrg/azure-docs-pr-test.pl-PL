---
title: "toouse aaaHow kontroli dostępu (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop i korzystania z kontroli dostępu Java na platformie Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure
W tym przewodniku opisano sposób toouse hello Azure usługi kontroli dostępu (ACS) w ramach hello zestawu narzędzi platformy Azure dla programu Eclipse. Aby uzyskać więcej informacji dotyczących usług ACS, zobacz hello [następne kroki](#next_steps) sekcji.

> [!NOTE]
> Hello Azure dostęp do usług formant filtru jest podgląd technologii społeczności. Jako wydaniu wstępnym oprogramowania go nie jest oficjalnie obsługiwana przez firmę Microsoft.
> 
> 

## <a name="what-is-acs"></a>Co to jest usługa ACS?
Większość deweloperów nie są ekspertów tożsamości i zazwyczaj nie powinny być poświęcić czas tworzenie mechanizmów uwierzytelniania i autoryzacji dla usług i aplikacji. Usługi ACS jest usługa Azure, która zapewnia łatwy sposób uwierzytelniania użytkowników, którzy potrzebują tooaccess aplikacji sieci web i usług bez konieczności toofactor uwierzytelniania złożonego logiki do kodu.

Witaj, następujące funkcje są dostępne w ACS:

* Integracja z systemem Windows Identity Foundation (WIF).
* Obsługa dostawców tożsamości popularnych sieci web (IP) w tym identyfikator Windows Live ID, Google, Facebook i Yahoo!.
* Obsługa usługi Active Directory Federation Services (AD FS) 2.0.
* Open Data Protocol (OData) — na podstawie usługi zarządzania, która zapewnia dostęp programistyczny tooACS ustawienia.
* Portalu zarządzania, który pozwala na dostęp administracyjny toohello ACS ustawienia.

Aby uzyskać więcej informacji na temat usług ACS, zobacz [2.0 usługi kontroli dostępu][Access Control Service 2.0].

## <a name="concepts"></a>Pojęcia
Azure ACS jest oparty na powitania podmiotów zabezpieczeń na podstawie oświadczeń tożsamości - spójnego podejścia toocreating mechanizmów uwierzytelniania dla aplikacji uruchomionych lokalnie lub w chmurze hello. Tożsamość oparta na oświadczeniach umożliwia wspólne dla aplikacji i usług tooacquire tożsamości potrzebne informacje o użytkownikach w organizacjach, w innych organizacjach, a na powitania Internet.

toocomplete hello zadania w tym przewodniku, należy zrozumieć następujące pojęcia hello:

**Klient** — w kontekście hello to tooguide jak, to jest przeglądarka, która próbuje aplikacji sieci web tooyour dostępu toogain.

**Jednostki uzależnionej (RP) aplikacji** -RP aplikacji jest witryny sieci Web lub usługi, która outsources uwierzytelniania tooone zewnętrznego urzędu. W żargonu tożsamości możemy Załóżmy, że w tym hello RP zaufanie tego urzędu. W tym przewodniku objaśniono sposób tooconfigure Twojego tootrust aplikacji ACS.

**Token** -tokenu to kolekcja danych zabezpieczeń, które jest zwykle wydawane po pomyślnym uwierzytelnieniu użytkownik. Zawiera zestaw *oświadczeń*, atrybuty hello uwierzytelnianego użytkownika. Oświadczenie może reprezentować nazwę użytkownika, identyfikator dla roli użytkownika, do której należy wiek użytkownika i tak dalej. Token jest zwykle podpisane cyfrowo, co oznacza zawsze może być pochodzące z wyszukiwania wstecznego tooits wystawcy, a nie dało się zmodyfikować jego zawartości. Uzyskują dostęp do tooa RP aplikację użytkownika z uwzględnieniem prawidłowy token wystawiony przez urząd certyfikacji, któremu ufa hello RP aplikacji.

**Dostawca tożsamości (IP)** -IP jest urząd, który służy do uwierzytelniania tożsamości użytkownika i wystawia tokeny zabezpieczające. faktyczną pracę Hello wystawianie tokenów jest zaimplementowana, chociaż specjalne usługi o nazwie zabezpieczeń usługi tokenów (STS). Typowe przykłady adresy IP, które obejmują Identyfikatora Windows Live, Facebook, business repozytoria użytkownika (na przykład usługi Active Directory) i tak dalej.
Gdy ACS jest tootrust skonfigurowanego adresu IP, hello system zaakceptować i sprawdzanie poprawności tokenów wystawionych przez tego adresu IP. Usługi ACS może ufać wielu adresów IP, która oznacza, że w przypadku aplikacji, relacje zaufania usług ACS, można natychmiast oferują, Twojej aplikacji hello tooall uwierzytelnionych użytkowników z powitalne wszystkie adresy IP ACS tej relacji zaufania w Twoim imieniu.

**Dostawcy federacyjnego (FP)** -adresów IP bezpośredniego znają użytkowników i ich przy użyciu swoich poświadczeń uwierzytelniania i wystawiać oświadczenia dotyczące wiedzieli o nich. Dostawcy federacyjnego (FP) jest inny rodzaj urzędu: zamiast bezpośrednio uwierzytelniania użytkowników, działa jako pośrednik i brokerów uwierzytelnianie między jednego planu odzyskiwania i jeden lub więcej adresów IP. Zarówno adresy IP i klatek na sekundę wystawiać tokeny zabezpieczające, dlatego za pomocą tokenu usługi zabezpieczenia (STS). Usługi ACS jest jedną FP.

**Aparat reguł ACS** -reguły przekształcania oświadczeń logikę hello przychodzące tokeny tootransform używanych z zaufanych adresów IP tootokens przeznaczone toobe używane przez hello planu odzyskiwania są oznaczone w postaci plików prostych. Usługi ACS funkcjami aparat reguł, który zajmuje się stosowanie dowolną logikę przekształcania określony dla Twojego planu odzyskiwania.

**Namespace ACS** — przestrzeń nazw jest partycją najwyższego poziomu usług ACS, używanej do organizowania ustawień. Przestrzeń nazw zawiera listę zaufanych adresów IP, aplikacje RP hello ma tooserve, hello reguł, które można spodziewać się hello reguły aparatu tooprocess przychodzące tokeny i tak dalej. Przestrzeń nazw przedstawia różne punkty końcowe, które będą używane przez aplikacji hello i tooperform tooget ACS developer jej funkcji.

Witaj przedstawiony na poniższym rysunku współdziałania ACS uwierzytelniania z aplikacji sieci web:

![Diagram przepływu ACS][acs_flow]

1. powitania klienta (w tym przypadku przeglądarki) żąda strony z hello planu odzyskiwania.
2. Ponieważ hello żądania nie jest jeszcze uwierzytelniony, hello RP przekierowuje hello użytkownika toohello urzędu zaufaną, czyli ACS. Witaj ACS przedstawia hello użytkownika z wyborem hello adresy IP, które zostały określone dla tego planu odzyskiwania. Witaj użytkownik wybiera hello odpowiedniego adresu IP.
3. powitania klienta umożliwia wyszukanie strony uwierzytelniania toohello IP i wyświetla monit o toolog użytkownika hello na.
4. Po uwierzytelnieniu powitania klienta (na przykład hello tożsamości, którego poświadczenia wprowadzono) hello IP wystawia token zabezpieczający.
5. Po wystawieniu tokenu zabezpieczającego, hello IP przekierowuje powitania klienta tooACS i powitania klienta wysyła hello tokenu zabezpieczającego wydane przez hello IP tooACS.
6. Usługi ACS weryfikuje hello tokenu zabezpieczającego wydanego przez hello IP, dane wejściowe hello tożsamości oświadczeń w tym tokenie do aparatu reguł hello ACS, oblicza oświadczeń tożsamości hello danych wyjściowych i generuje nowy token zabezpieczający, który zawiera te dane wyjściowe oświadczenia.
7. Usługi ACS przekierowuje powitania klienta toohello planu odzyskiwania. Witaj, klient wysyła hello wystawione przez usługi ACS toohello RP nowy token zabezpieczający. Hello RP sprawdza podpis hello na powitania tokenu zabezpieczającego wydane przez usługi ACS, sprawdza poprawność hello oświadczeń w tym tokenie i zwraca stronę hello, pierwotnie żądany.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete hello zadania w tym przewodniku, trzeba będzie hello poniżej:

* Java Developer Kit (JDK), wersji 1.6 lub nowszej.
* Zaćmienie-IDE for Java EE Developers indygo lub nowszej. Ten można pobrać z <http://www.eclipse.org/downloads/>. 
* Dystrybucja serwera sieci web opartych na języku Java lub serwera aplikacji, takich jak Apache Tomcat, GlassFish, serwer aplikacji JBoss lub Jetty.
* subskrypcję platformy Azure, która może zostać pobrany z <http://www.microsoft.com/windowsazure/offers/>.
* Hello zestawu narzędzi platformy Azure dla programu Eclipse, kwietnia 2014 wersji lub nowszym. Aby uzyskać więcej informacji, zobacz [hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Toouse certyfikatu X.509 z aplikacją. Należy ten certyfikat w publicznego certyfikatu (.cer) i wymiana informacji osobistych (. Format PFX). (Opcje tworzenia ten certyfikat zostanie opisane w dalszej części tego samouczka).
* Znajomość hello Azure obliczeniowe emulatora i wdrażania techniki omówione w [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Utwórz Namespace ACS
toobegin przy użyciu usługi kontroli dostępu (ACS) na platformie Azure, należy utworzyć przestrzeń nazw usług ACS. przestrzeń nazw Hello zawiera unikatowy zakres na potrzeby adresowania zasobów usługi ACS od w aplikacji.

1. Zaloguj się do hello [portalu zarządzania Azure][Azure Management Portal].
2. Kliknij przycisk **usługi Active Directory**. 
3. toocreate nowej przestrzeni nazw kontroli dostępu, kliknij przycisk **nowy**, kliknij przycisk **usługi aplikacji**, kliknij przycisk **kontroli dostępu**, a następnie kliknij przycisk **szybkie tworzenie** . 
4. Wprowadź nazwę dla hello przestrzeni nazw. Azure sprawdza, czy nazwa hello jest unikatowy.
5. Wybierz region hello, w których hello przestrzeni nazw jest używana. Aby uzyskać najlepszą wydajność hello Użyj hello regionu, w której wdrażana jest aplikacja.
6. Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello mają toouse hello ACS przestrzeni nazw.
7. Kliknij przycisk **Utwórz**.

Azure tworzy i włącza hello przestrzeni nazw. Poczekaj, aż stan hello hello nowej przestrzeni nazw jest **Active** przed kontynuowaniem. 

## <a name="add-identity-providers"></a>Dodaj dostawców tożsamości
To zadanie możesz dodać toouse adresów IP z aplikacją RP do uwierzytelniania. Dla celów demonstracyjnych to zadanie pokazuje, jak tooadd Windows Live jako adresu IP, ale można użyć dowolnego powitalne adresy IP na liście hello portalu zarządzania usługi ACS.

1. W hello [portalu zarządzania Azure][Azure Management Portal], kliknij przycisk **usługi Active Directory**wybierz przestrzeń nazw kontroli dostępu, a następnie kliknij przycisk **Zarządzaj**. Otwiera Hello portalu zarządzania usługi ACS.
2. W okienku nawigacji po lewej stronie powitania hello portalu zarządzania usługi ACS, kliknij przycisk **dostawców tożsamości**.
3. Identyfikator Windows Live ID jest domyślnie włączona i nie można go usunąć. Do celów tego samouczka tylko identyfikator Windows Live ID jest używany. Ten ekran jest jednak, którym można dodać inne adresy IP, klikając hello **Dodaj** przycisku.

Identyfikator Windows Live ID jest teraz włączony jako adresu IP dla przestrzeni nazw usługi ACS. Następnie określ aplikację sieci web Java (toobe utworzyć później) jako planu odzyskiwania.

## <a name="add-a-relying-party-application"></a>Dodawanie jednostki uzależnionej strony aplikacji
W tym zadaniu skonfigurujesz ACS toorecognize aplikacji sieci web w języku Java jako prawidłową aplikację planu odzyskiwania.

1. W portalu zarządzania usługi ACS hello, kliknij polecenie **aplikacje firm jednostki uzależnionej**.
2. Na powitania **jednostki uzależnionej aplikacje firm** kliknij przycisk **Dodaj**.
3. Na powitania **Dodaj aplikację jednostki uzależnionej strony** pozycję hello następujące:
   
   1. W **nazwa**, nazwa typu hello hello planu odzyskiwania. Do celów tego samouczka, wpisz **aplikacji sieci Web Azure**.
   2. W **tryb**, wybierz pozycję **wprowadź ustawienia ręcznie**.
   3. W **obszaru**, zastosowanie typu hello URI toowhich hello tokenu zabezpieczającego wydane przez usługi ACS. Dla tego zadania, wpisz **adresem http://localhost: 8080 /**.
      ![Jednostki uzależnionej obszar strony do użycia w emulatorze obliczeń][relying_party_realm_emulator]
   4. W **zwrotny adres URL** typu hello adresu URL toowhich ACS zwraca hello tokenu zabezpieczającego. Dla tego zadania, wpisz **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![jednostki uzależnionej strony zwrotnego adresu URL do użycia w emulatorze obliczeń][relying_party_return_url_emulator]
   5. Zaakceptuj wartości domyślne hello w rest hello hello pól.
4. Kliknij pozycję **Zapisz**.

Teraz pomyślnie skonfigurowano aplikację sieci web Java uruchamianych w emulatorze obliczeń platformy Azure hello (pod adresem http://localhost: 8080 /) toobe RP w przestrzeni nazw usługi ACS. Reguły hello następnie należy utworzyć, który ACS korzysta z oświadczeń tooprocess dla hello planu odzyskiwania.

## <a name="create-rules"></a>Tworzenie reguł
To zadanie służy do definiowania reguł hello, które określają, jak oświadczenia są przekazywane z adresów IP tooyour planu odzyskiwania. W celu hello tego przewodnika możemy po prostu skonfiguruje typy oświadczeń przychodzących hello toocopy ACS i wartości bezpośrednio w token wyjściowy hello, bez filtrowania i modyfikowania ich.

1. Na stronie głównej portalu zarządzania usługi ACS hello, kliknij przycisk **reguły grupy**.
2. Na powitania **grup reguł** kliknij przycisk **domyślne grupy reguł dla aplikacji sieci Web Azure**.
3. Na powitania **Edytuj grupę reguł** kliknij przycisk **Generuj**.
4. Na powitania **generowania reguł: domyślne grupy reguł dla aplikacji sieci Web Azure** strony, upewnij się, identyfikator Windows Live ID jest zaznaczony, a następnie kliknij przycisk **Generuj**.    
5. Na powitania **Edytuj grupę reguł** kliknij przycisk **zapisać**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Przekazywanie certyfikatu przestrzeni nazw tooyour ACS
W tym zadaniu przekazywania. Certyfikat PFX, które będzie używane toosign żądań tokenów utworzonych przez usługi ACS przestrzeni nazw.

1. Na stronie głównej portalu zarządzania usługi ACS hello, kliknij przycisk **certyfikaty i klucze**.
2. Na powitania **certyfikaty i klucze** kliknij przycisk **Dodaj** powyżej **podpisywania tokenu**.
3. Na powitania **certyfikat podpisywania tokenu dodać lub klucza** strony:
   1. W hello **używany do** , kliknij przycisk **aplikację jednostki uzależnionej** i wybierz **aplikacji sieci Web Azure** (który wcześniej ustawiony jako nazwa hello aplikację jednostki uzależnionej strony).
   2. W hello **typu** zaznacz **certyfikatu X.509**.
   3. W hello **certyfikatu** sekcji, kliknij przycisk Przeglądaj hello i przejdź do pliku certyfikatu X.509 toohello, które mają toouse. Są to. Plik PFX. Wybierz plik hello, kliknij przycisk **Otwórz**, a następnie wprowadź hasło certyfikatu hello w hello **hasło** pola tekstowego. Pamiętaj, że do celów testowych, mogą używać niezależne-signed certyfikatu. toocreate certyfikatu z podpisem własnym, użyj hello **nowy** przycisku na powitania **Biblioteka filtru ACS** okna dialogowego (opisana dalej), lub użyj hello **encutil.exe** narzędzie z hello [projektu witryny sieci Web] [ project website] z hello Azure Starter Kit for Java.
   4. Upewnij się, że **jako główny** jest zaznaczony. Twoje **certyfikat podpisywania tokenu dodać lub klucza** strony powinien wyglądać podobnie następujące toohello.
       ![Dodaj certyfikat podpisywania tokenu][add_token_signing_cert]
   5. Kliknij przycisk **zapisać** toosave ustawienia i zamknij hello **certyfikat podpisywania tokenu dodać lub klucza** strony.

Następnie przejrzyj informacje hello w hello integracji aplikacji strony i skopiuj hello URI trzeba tooconfigure Twojego toouse aplikacji sieci web Java ACS.

## <a name="review-hello-application-integration-page"></a>Strona integracji aplikacji hello przeglądu
Można znaleźć wszystkie hello informacje i niezbędne tooconfigure kodu hello programu Java sieci web aplikacji (hello aplikacji RP) toowork z usług ACS na stronie powitania integracji aplikacji hello portalu zarządzania usługi ACS. Informacje te będą potrzebne podczas konfigurowania aplikacji sieci web Java uwierzytelniania federacyjnego.

1. W portalu zarządzania usługi ACS hello, kliknij polecenie **integracji aplikacji**.  
2. W hello **integracji aplikacji** kliknij przycisk **strony logowania**.
3. W hello **integracji strony logowania** kliknij przycisk **aplikacji sieci Web Azure**.

W hello **integracji strony logowania: aplikacji sieci Web Azure** strony hello adres URL na liście **opcja 1: strony logowania hostowanych przez usługi ACS tooan łącze** będzie używany w aplikacji sieci web w języku Java. Po dodaniu hello filtr usługi kontroli dostępu platformy Azure biblioteki tooyour aplikacji Java, należy tę wartość.

## <a name="create-a-java-web-application"></a>Tworzenie aplikacji sieci web w języku Java
1. W środowisku Eclipse w menu powitania kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**. (Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku**, **nowy**, następnie hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu**, rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk  **Następnie**.) Do celów tego samouczka, nazwa projektu hello **MyACSHelloWorld**. (Upewnij się, możesz użyć tej nazwy, kolejne kroki w tym samouczku oczekiwać Twojej toobe pliku WAR o nazwie MyACSHelloWorld). Na ekranie pojawi się podobne toohello następujące:
   
    ![Utwórz projekt Hello World ACS exampple][create_acs_hello_world]
   
    Kliknij przycisk **Zakończ**.
2. W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyACSHelloWorld**. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).
3. W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**. Zachowaj folder nadrzędny hello MyACSHelloWorld/WebContent, jak pokazano poniżej hello:
   
    ![Dodaj plik JSP, na przykład ACS][add_jsp_file_acs]
   
    Kliknij przycisk **Dalej**.
4. W hello **wybierz szablon JSP** zaznacz pozycję **New JSP File (html)** i kliknij przycisk **Zakończ**.
5. Po otwarciu pliku index.jsp hello w środowisku Eclipse Dodaj w toodisplay tekst **Hello ACS World!** w ramach istniejącego hello `<body>` elementu. Zaktualizowana `<body>` zawartość powinna być widoczna jako hello następujące czynności:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Zapisz index.jsp.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Dodaj filtr ACS biblioteki tooyour aplikacji hello
1. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyACSHelloWorld**, kliknij przycisk **ścieżkę kompilacji**, a następnie kliknij przycisk **Konfiguruj ścieżkę kompilacji**.
2. W hello **ścieżka kompilacji języka Java** okna dialogowego, kliknij przycisk hello **biblioteki** kartę.
3. Kliknij przycisk **Dodaj bibliotekę**.
4. Kliknij przycisk **filtr usługi kontroli dostępu platformy Azure (za pomocą technologii Otwórz MS)** , a następnie kliknij przycisk **dalej**. Witaj **filtr usługi kontroli dostępu platformy Azure** zostanie wyświetlone okno dialogowe.  (hello **lokalizacji** pole może mieć inną ścieżkę, w zależności od tego, w którym zainstalowano Eclipse, a numer wersji hello może być różne w zależności od aktualizacji oprogramowania.)
   
    ![Dodaj bibliotekę filtru ACS][add_acs_filter_lib]
5. Przy użyciu przeglądarki otworzyć toohello **integracji strony logowania** strony hello portalu zarządzania, na liście hello URL hello kopii **opcja 1: strony logowania hostowanych przez usługi ACS tooan łącze** pola i wklej go do hello **Punktu końcowego ACS uwierzytelniania** pole hello Eclipse w oknie dialogowym.
6. Przy użyciu przeglądarki otworzyć toohello **Edytowanie aplikacji jednostki uzależnionej strony** strony hello portalu zarządzania, na liście hello URL hello kopii **obszaru** pól i wklej go do hello **jednostki uzależnionej obszar strony**  pole hello Eclipse w oknie dialogowym.
7. W ramach hello **zabezpieczeń** sekcji hello Eclipse okna dialogowego, jeśli chcesz, aby toouse istniejącego certyfikatu, kliknij przycisk **Przeglądaj**, toohello certyfikat ma toouse, zaznacz go i kliknij Przejdź  **Otwórz**. Lub toocreate nowy certyfikat, kliknij przycisk **nowy** toodisplay hello **nowego świadectwa** okna dialogowego, następnie podaj hasło hello, nazwa pliku .cer hello i nazwa pliku PFX hello hello nowy certyfikat.
8. Sprawdź **osadzania hello certyfikatu w pliku WAR hello**. Osadzanie hello certyfikatu w ten sposób obejmuje on w danym wdrożeniu bez konieczności toomanually Dodaj go jako składnik. (Jeśli zamiast tego muszą być przechowywane certyfikat zewnętrznie z pliku WAR, można dodać certyfikatu hello jako części roli i usuń zaznaczenie pola wyboru **osadzania hello certyfikatu w pliku WAR hello**.)
9. [Opcjonalnie] Zachowaj **połączeń HTTPS wymagają** zaznaczone. Jeśli ustawisz tę opcję, musisz tooaccess aplikacji przy użyciu protokołu HTTPS hello. Jeśli nie chcesz toorequire połączeń HTTPS, usuń zaznaczenie tej opcji.
10. Wdrożenia emulator, obliczeń toohello Twojego **filtru ACS Azure** ustawienia będzie wyglądać podobnie toohello następujące.
    
    ![Emulator obliczeń platformy Azure ustawień filtru ACS dla toohello wdrożenia][add_acs_filter_lib_emulator]
11. Kliknij przycisk **Zakończ**.
12. Kliknij przycisk **tak** przedstawionej z pola z okna dialogowego informacją, że zostanie utworzony plik web.xml.
13. Kliknij przycisk **OK** tooclose hello **ścieżka kompilacji języka Java** okna dialogowego.

## <a name="deploy-toohello-compute-emulator"></a>Wdrażanie toohello emulatora obliczeń
1. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyACSHelloWorld**, kliknij przycisk **Azure**, a następnie kliknij przycisk **pakietu dla platformy Azure**.
2. Dla **Nazwa projektu**, typ **MyAzureACSProject** i kliknij przycisk **dalej**.
3. Wybierz JDK i serwera aplikacji. (Te kroki są tu szczegółowo hello [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) samouczka).
4. Kliknij przycisk **Zakończ**.
5. Kliknij przycisk hello **uruchamianie w emulatorze Azure** przycisku.
6. Po uruchomieniu aplikacji sieci web Java w emulatorze obliczeń hello, zamknij wszystkie wystąpienia przeglądarki (tak, aby wszystkie bieżące sesje przeglądarki nie zakłóca test logowania ACS).
7. Uruchom aplikację, otwierając <adresem http://localhost: 8080/MyACSHelloWorld/> w przeglądarce (lub <https://localhost:8080/MyACSHelloWorld/> , gdy zaznaczono **połączenia wymagają protokołu HTTPS** ). Powinien być wyświetlany monit o logowania usługi Windows Live ID, a następnie należy podjąć zwrotny adres URL toohello określony dla jednostki uzależnionej strony aplikacji.
8. Po zakończeniu przeglądania aplikacji, kliknij przycisk hello **zresetować emulatora usługi Azure** przycisku.

## <a name="deploy-tooazure"></a>Wdrażanie tooAzure
toodeploy tooAzure należy toochange hello jednostki uzależnionej strony obszaru i przywracać adres URL dla przestrzeni nazw usługi ACS.

1. W ramach hello portalu zarządzania Azure, w hello **Edytowanie aplikacji jednostki uzależnionej strony** strony, zmodyfikuj **obszaru** toobe hello adres URL witryny wdrożone. Zastąp **przykład** o nazwie DNS hello określone dla danego wdrożenia.
   
    ![Jednostki uzależnionej obszar strony do użycia w produkcji][relying_party_realm_production]
2. Modyfikowanie **zwrotny adres URL** toobe hello adres URL aplikacji. Zastąp **przykład** o nazwie DNS hello określone dla danego wdrożenia.
   
    ![Jednostki uzależnionej zwrotny adres URL strony do użycia w produkcji][relying_party_return_url_production]
3. Kliknij przycisk **zapisać** toosave Twojego zaktualizowane odpowiedzieć strony obszaru i przywrócenie zmiany adresu URL.
4. Zachowaj hello **integracji strony logowania** strony Otwórz w przeglądarce, musisz toocopy z niego wkrótce.
5. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyACSHelloWorld**, kliknij przycisk **ścieżkę kompilacji**, a następnie kliknij przycisk **Konfiguruj ścieżkę kompilacji**.
6. Kliknij hello **biblioteki** , kliknij pozycję **filtr usługi kontroli dostępu platformy Azure**, a następnie kliknij przycisk **Edytuj**.
7. Przy użyciu przeglądarki otworzyć toohello **integracji strony logowania** strony hello portalu zarządzania, na liście hello URL hello kopii **opcja 1: strony logowania hostowanych przez usługi ACS tooan łącze** pola i wklej go do hello **Punktu końcowego ACS uwierzytelniania** pole hello Eclipse w oknie dialogowym.
8. Przy użyciu przeglądarki otworzyć toohello **Edytowanie aplikacji jednostki uzależnionej strony** strony hello portalu zarządzania, na liście hello URL hello kopii **obszaru** pól i wklej go do hello **jednostki uzależnionej obszar strony**  pole hello Eclipse w oknie dialogowym.
9. W ramach hello **zabezpieczeń** sekcji hello Eclipse okna dialogowego, jeśli chcesz, aby toouse istniejącego certyfikatu, kliknij przycisk **Przeglądaj**, toohello certyfikat ma toouse, zaznacz go i kliknij Przejdź  **Otwórz**. Lub toocreate nowy certyfikat, kliknij przycisk **nowy** toodisplay hello **nowego świadectwa** okna dialogowego, następnie podaj hasło hello, nazwa pliku .cer hello i nazwa pliku PFX hello hello nowy certyfikat.
10. Zachowaj **osadzania hello certyfikatu w pliku WAR hello** zaznaczone, przy założeniu ma tooembed hello certyfikatu w pliku WAR hello.
11. [Opcjonalnie] Zachowaj **połączeń HTTPS wymagają** zaznaczone. Jeśli ustawisz tę opcję, musisz tooaccess aplikacji przy użyciu protokołu HTTPS hello. Jeśli nie chcesz toorequire połączeń HTTPS, usuń zaznaczenie tej opcji.
12. Dla tooAzure wdrożenia ustawienia filtra ACS Azure będzie wyglądać podobnie następujące toohello.
    
    ![Ustawienia usługi Azure ACS filtru w przypadku wdrożenia produkcyjnego][add_acs_filter_lib_production]
13. Kliknij przycisk **Zakończ** tooclose hello **Edytuj biblioteki** okna dialogowego.
14. Kliknij przycisk **OK** tooclose hello **właściwości MyACSHelloWorld** okna dialogowego.
15. W programie Eclipse kliknij hello **publikowania tooAzure chmury** przycisku. Odpowiadanie toohello monitów, podobnie jak w hello **toodeploy tooAzure Twojej aplikacji** sekcji hello [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tematu. 

Po wdrożeniu aplikacji sieci web, zamknij wszystkie sesje Otwórz przeglądarkę, uruchom aplikację sieci web i powinien być wyświetlany monit toosign się przy użyciu poświadczeń usługi Windows Live ID, a następnie wysyłane toohello adres zwrotny URL jednostki uzależnionej strony aplikacji.

Gdy wszystko będzie gotowe przy użyciu aplikacji ACS Witaj świecie, pamiętaj toodelete hello wdrożenia (Dowiedz się jak toodelete wdrożenia w hello [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) tematu).

## <a name="next_steps"></a>Następne kroki
Do badania hello Assertion Markup języka SAML (Security) zwrócony przez aplikację tooyour ACS, zobacz [jak tooview SAML zwrócony przez hello usłudze kontroli dostępu platformy Azure][How tooview SAML returned by hello Azure Access Control Service]. toofurther poznać funkcje usług ACS i tooexperiment z bardziej zaawansowanych scenariuszy, zobacz [2.0 usługi kontroli dostępu][Access Control Service 2.0].

Ponadto ta hello przykład używane **osadzania hello certyfikatu w pliku WAR hello** opcji. Ta opcja umożliwia proste toodeploy hello certyfikatu. Jeśli zamiast tego chcesz tookeep certyfikatu podpisywania niezależnie od pliku WAR, możesz użyć hello następujące techniki:

1. W ramach hello **zabezpieczeń** sekcji hello **filtr usługi kontroli dostępu platformy Azure** okno dialogowe, typ **${env. JAVA_HOME}/MyCert.cer** i usuń zaznaczenie pola wyboru **osadzania hello certyfikatu w pliku WAR hello**. (Dostosuj mycert.cer, jeśli różni się nazwy pliku certyfikatu). Kliknij przycisk **Zakończ** tooclose hello w oknie dialogowym.
2. Kopia certyfikatu hello jako składnik we wdrożeniu: W Eksploratorze projektu w środowisku Eclipse, rozwiń węzeł **MyAzureACSProject**, kliknij prawym przyciskiem myszy **WorkerRole1**, kliknij przycisk **właściwości** , rozwiń węzeł **roli Azure**i kliknij przycisk **składniki**.
3. Kliknij pozycję **Dodaj**.
4. W ramach hello **Dodaj składnik** okna dialogowego:
   
   1. W hello **importu** sekcji:
      1. Użyj hello **pliku** przycisk toonavigate toohello certyfikatów, które mają toouse. 
      2. Dla **metody**, wybierz pozycję **kopiowania**.
   2. Aby uzyskać **jako nazwę**, kliknij pole tekstowe hello i zaakceptuj nazwę domyślną hello.
   3. W hello **Wdróż** sekcji:
      1. Dla **metody**, wybierz pozycję **kopiowania**.
      2. Aby uzyskać **toodirectory**, typ **JAVA_HOME %**.
   4. Twoje **Dodaj składnik** okna dialogowego powinna wyglądać podobnie następujące toohello.
      
       ![Dodaj składnik certyfikatu][add_cert_component]
   5. Kliknij przycisk **OK**.

W tym momencie certyfikat będzie uwzględnione w danym wdrożeniu. Należy pamiętać, że niezależnie od tego, czy osadzić hello certyfikatu w pliku WAR hello lub dodanie go jako wdrożenia tooyour składników, należy tooupload hello tooyour przestrzeni nazw zgodnie z opisem w hello [przekazaćprzestrzeninazwtooyourACScertyfikatu] [ Upload a certificate tooyour ACS namespace] sekcji.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

