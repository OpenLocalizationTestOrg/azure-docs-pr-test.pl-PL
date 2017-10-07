---
title: "tooconfigure aaaHow toouse aplikacji serwera Proxy aplikacji ograniczone delegowanie protokołu Kerberos | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure ograniczone delegowanie protokołu Kerberos dla aplikacji serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Jak tooconfigure toouse aplikacji serwera Proxy aplikacji ograniczone delegowanie protokołu Kerberos

Witaj dostępnych metod na osiągnięcie toopublished logowania jednokrotnego, które aplikacje może różnić się nieco od tooapplication aplikacji i jedną z opcji hello, że serwer Proxy aplikacji Azure oferuje prawa fabrycznej hello, jest delegowanie ograniczone protokołu Kerberos (KCD). Jest to, gdzie hosta łącznik jest skonfigurowany tooperform ograniczonego protokołu kerberos uwierzytelniania toobackend aplikacji, w imieniu użytkowników.

rzeczywiste procedura Hello włączania KCD jest stosunkowo prosta i zwykle wymaga nie więcej niż ogólną wiedzą hello różnymi składnikami i przebieg uwierzytelniania, która ułatwia obsługę logowania jednokrotnego. Znajdowania dobre źródła informacji toohelp Rozwiązywanie problemów z scenariuszy, w którym KCD logowania jednokrotnego nie działać zgodnie z oczekiwaniami, może być rozrzedzony.

Tak w tym artykule prób tooprovide pojedynczy punkt odniesienia, które powinny pomóc w Rozwiązywanie problemów i samodzielnie rozwiązać niektóre hello najbardziej typowe problemy, które widzimy. Witaj tym samym czasie oferta dodatkowe wskazówki dotyczące diagnozowania hello bardziej złożone i plików implementacji.

należy pamiętać, że w tym artykule sprawia, że następujące założenia hello:

-   Serwera Proxy aplikacji Azure została wdrożona jako na naszych [dokumentacji](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) i aplikacje KCD toonon dostępu działa zgodnie z oczekiwaniami.

-   Witaj aplikacji docelowej opublikowanych zależy od usług IIS i przez firmę Microsoft implementacja protokołu kerberos.

-   host serwera i aplikacji Hello znajdują się w jednej domenie usługi Active Directory. Szczegółowe informacje dotyczące wielu domen i lasów scenariusze można znaleźć w naszych [oficjalny dokument KCD](http://aka.ms/KCDPaper).

-   Witaj podmiotu jest publikowana w Azure dzierżawcy z wstępne uwierzytelnianie jest włączone, a użytkownicy są oczekiwano uwierzytelniania opartego na tooAzure tooauthenticate za pomocą formularzy. Scenariusze uwierzytelniania klienta sformatowanego nie są objęte w tym artykule, ale można dodać w pewnym momencie w przyszłości hello.

## <a name="prerequisites"></a>Wymagania wstępne

Serwer Proxy aplikacji Azure można wdrożyć do niemal każdego rodzaju infrastruktury lub architektury środowiska i hello bez wątpienia się różnić od tooorganization organizacji. Jedną z najbardziej typowych przyczyn KCD hello powiązanych problemy nie jest hello, ale zamiast prostego niewłaściwa konfiguracje lub w środowiskach ogólne nadzoru.

Z tego powodu informacjami jest zawsze toostart przy tym upewnić się, czy zostały spełnione wszystkie wymagania wstępne hello, którego układ określa się w naszym głównym [przy użyciu logowania jednokrotnego KCD z artykułem serwera Proxy aplikacji hello](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) przed rozpoczęciem rozwiązywania problemów.

Szczególnie hello sekcję na temat konfigurowania KCD na 2012 R2, jak to wykorzystuje tooconfiguring zasadniczo różne podejścia KCD w poprzednich wersjach systemu Windows, ale także będąc w trosce o kilka innych kwestii:

-   Nie jest nietypowe dla domeny tooopen serwera członkowskiego okno dialogowe bezpiecznego kanału z określonego kontrolera domeny. Następnie przenieś okno tooanother w danym momencie, więc hostów łącznika zazwyczaj nie powinno być możliwe toocommunicate toobeing ograniczone z kontrolerów domeny tylko do określonej lokacji lokalnej.

-   Podobne toohello powyżej, scenariusze obejmujące różne domeny korzystają z odwołań, które bezpośrednie łącznika tooDCs hosta, które mogą znajdować się poza hello lokalnej sieci obwodowej. W tym scenariuszu, który jest równie ważne toomake się, że także umożliwi ruchu lub nowszej tooDCs reprezentujące innych domen, w przeciwnym razie delegowania zakończyć się niepowodzeniem.

-   Jeśli to możliwe, należy unikać wprowadzania żadnych aktywnych urządzeń adresy IP/Identyfikatory między hostami łącznika i kontrolery domeny, jak te są czasami za pośrednictwem niepożądanych i zakłócić ruch RPC core

Tyle szybko chcielibyśmy tooresolve problemów i ostatecznie może trwać, dlatego w miarę możliwości należy spróbuj i przetestować delegowania w najprostszym scenariuszy hello. Witaj więcej zmiennych, które należy wprowadzić, hello więcej może być toocontend z. Na przykład ograniczenie testowania pojedynczy łącznik tooa można zapisać cenny czas, a po rozwiązaniu problemów hello można dodać dodatkowe łączników.

Pewne czynniki środowiska może również być przyczyną tooan problem, więc ponownie Jeśli to możliwe spróbuj i zminimalizować hello architektura tooa bez systemu operacyjnego co najmniej do testowania. Na przykład nie są rzadko nieprawidłowej konfiguracji zapory wewnętrznej listy kontroli dostępu, więc jeśli to możliwe mieć cały ruch z łącznika może bezpośrednio za pomocą toohello kontrolerów domeny i wewnętrznej bazy danych aplikacji. 

Faktycznie hello bezwzględną najlepsze miejsce tooposition łączników jest możliwie cele tootheir jako może być. Wbudowany zapory nas o podczas testowania, po prostu dodaje niepotrzebne złożoność i właśnie przedłużyć czas badania sieci.

Tak co stanowi KCD problem mimo to? Dobrze istnieje kilka klasycznego oznaczenia logowania jednokrotnego KCD się niepowodzeniem i hello pierwszy oznaki problemu zwykle pojawiają się w hello przeglądarki.

   ![Błąd konfiguracji KCD niepoprawne](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Autoryzacja nie powiodła z powodu uprawnień toomissing](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

wszystkie, które posiadają hello objawem tego samego niepowodzeniem tooperform logowania jednokrotnego i w związku z tym odmawia hello aplikacji toohello dostępu użytkownika.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

W jaki sposób można następnie Rozwiąż ten problem są zależne od hello problem i obserwowanych objawów. Przed każdym przechodzi dalej czy Sugerujemy hello następującego łącza, ponieważ zawierają one przydatne informacje, które użytkownik może nie ma wszedł w:

-   [Rozwiązywanie problemów z serwera Proxy aplikacji i komunikaty o błędach](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Błędy protokołu Kerberos i objawy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Praca z logowania jednokrotnego podczas lokalnej i w chmurze tożsamości nie są identyczne](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Jeśli masz to znacznie, a następnie hello głównego ostatecznie występuje problem. Należy toodig głębiej, więc start oddzielając przepływu hello w trzech etapach distinct, które można rozwiązywać problemy.

**Wstępne uwierzytelnienie klienta** -hello użytkownika zewnętrznego uwierzytelniania tooAzure za pośrednictwem przeglądarki.

Trwa stanie toopre-uwierzytelniania jest tooAzure dla toofunction KCD logowania jednokrotnego. Powinno to przetestowane i skierowana najpierw, jeśli występują problemy. Należy pamiętać, że hello etapu uwierzytelniania wstępnego nie ma relacji tooKCD ani hello opublikowana aplikacja. Powinien być dość proste toocorrect niezgodności przez związane z poprawnością sprawdzanie hello podmiotu konto istnieje w systemie Azure i nie jest wyłączone/zablokowany. odpowiedzi na błąd Hello w przeglądarce hello jest zazwyczaj dość opisowa toounderstand hello przyczyna. Jeśli nie masz pewności, można również sprawdzić naszych innych tooverify docs Rozwiązywanie problemów.

**Delegowanie usługi** — Witaj łącznika serwera Proxy Azure uzyskania biletu usługi kerberos w Centrum dystrybucji KLUCZY (Centrum dystrybucji protokołu Kerberos), w imieniu użytkowników.

komunikację zewnętrzną Hello między powitania klienta i hello Azure frontonu powinny nie ma wpływu na KCD, inne niż zapewnienia jego działanie. Jest to tak hello usługi serwera Proxy Azure można podać prawidłowy identyfikator, którego można używane tooobtain biletu protokołu kerberos. Bez tego KCD nie jest możliwe, a nie powiedzie się.

Jak wspomniano wcześniej, komunikaty o błędach przeglądarki hello zwykle zawierają niektóre dobrej wskazówek Dlaczego rzeczy kończą się niepowodzeniem. Upewnij się, że toonote hello identyfikator działania i sygnatura czasowa w odpowiedzi hello, jak dzięki temu można toocorrelate hello zachowanie tooactual zdarzenia w dzienniku zdarzeń serwera Proxy Azure hello.

   ![Błąd konfiguracji KCD niepoprawne](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

I dziennik zdarzeń widziany hello odpowiednie wpisy hello będzie widoczne jako zdarzenia 13019 lub 12027. Możesz znaleźć hello łącznika dzienniki zdarzeń w **Dzienniki aplikacji i usług** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Łącznik**&gt;**Admin**.

   ![Zdarzenie 13019 z dziennika zdarzeń serwera Proxy aplikacji](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Zdarzenie 12027 z dziennika zdarzeń serwera Proxy aplikacji](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Na użytek rekord A w systemie DNS wewnętrznych aplikacji hello adresów, a nie rekordu CName

-   Ponownie Potwierdź obsługujących łącznik hello udzielono toohello toodelegate prawa Witaj wyznaczone konto docelowe głównej nazwy usługi, a **Użyj dowolnego protokołu uwierzytelniania** jest zaznaczone. Ten temat znajdują się w naszym głównym [artykułu konfiguracji logowania jednokrotnego](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)

-   Sprawdź, czy jest tylko jedno wystąpienie hello SPN istniejących w AD przez wystawienie **setspn - x** z wiersza polecenia na żadnym hoście członek domeny

-   Sprawdź toosee, jeśli zasady domeny jest wymuszane toolimit hello [maksymalny rozmiar kerberos wystawionych tokenów](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), ponieważ ten łącznik hello uniemożliwianie uzyskania tokenu, jeśli znaleziono toobe nadmiernego

Przechwytywanie hello wymiany między hello łącznika hosta i domeny Centrum dystrybucji KLUCZY śledzenia sieci będzie wówczas hello następnego kroku najlepsze w uzyskaniu więcej niski poziom szczegółów na powitania problemy. Można je znaleźć w [nowości papieru rozwiązywanie](https://aka.ms/proxytshootpaper).

Jeśli biletów wygląda dobrze, powinny pojawić się zdarzenia w dziennikach hello podając uwierzytelniania nie powiodła z powodu aplikacji toohello zwracającej 401. Oznacza to przeważnie tej aplikacji docelowej hello odrzucenia biletu, więc kontynuować powitania po kolejnego etapu.

**Aplikacji docelowej** -konsumenta hello biletu kerberos hello podał hello łącznika

Ten łącznik hello etap są oczekiwanego toohave przesyłane protokołu kerberos usługa biletu toohello wewnętrznej bazie danych, jako nagłówek w pierwsze żądanie aplikacji hello.

-   Przy użyciu aplikacji hello wewnętrzny adres URL zdefiniowany w portalu hello, sprawdzić, czy aplikacja hello jest dostępny bezpośrednio z przeglądarki hello na powitania łącznika hosta. Następnie możesz zalogować się pomyślnie. Szczegóły w ten sposób można znaleźć na stronie Rozwiązywanie problemów dotyczących łącznika hello.

-   Nadal na hoście łącznika hello, potwierdź hello uwierzytelniania między hello przeglądarki, a aplikacja hello używa protokołu kerberos, wykonując jedną z następujących hello:

1.  Uruchamianie narzędzi dla deweloperów (**F12**) w programie Internet Explorer lub użyj [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) z hello łącznika hosta. Przejdź toohello aplikacji przy użyciu wewnętrznego adresu URL hello i inspekcję hello oferowane nagłówki autoryzacji WWW zwracany w odpowiedzi hello z aplikacji hello, występuje tooensure, który albo negocjowania lub kerberos. Obiektu blob kolejnych kerberos zwracany w odpowiedzi hello z toohello przeglądarki hello aplikacji zaczynają się zwykle **YII**, więc jest dobrym wskaźnikiem w play protokołu kerberos. NTLM na powitania drugiej zawsze rozpoczynają się **TlRMTVNTUAAB**, która odczytuje NTLMSSP podczas zdekodować z formatu Base64. Jeśli widzisz **TlRMTVNTUAAB** na początku hello hello obiektów blob, oznacza to, że protokół Kerberos jest **nie** dostępne. Jeśli widzisz, prawdopodobnie Kerberos dostępne.

  * Uwaga: Jeśli przy użyciu programu Fiddler, ta metoda wymaga czasowo wyłączyć ochrona rozszerzona na konfiguracji aplikacji hello w usługach IIS.

     ![Przeglądarce inspekcji sieci](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Rysunek:* ponieważ to nie rozpoczyna się od TIRMTVNTUAAB, jest to przykład, że protokół Kerberos jest dostępne. To jest przykład obiektu Blob protokołu Kerberos, który nie zaczyna się od YII.

2.  Tymczasowo usunąć NTLM, z listy dostawców hello w lokacji i dostępu do aplikacji IIS bezpośrednio z programu Internet Explorer na hoście łącznika. NTLM nie jest już na liście dostawców hello użytkownik powinien być aplikacji hello tooaccess możliwe tylko przy użyciu protokołu Kerberos. Jeśli to się nie powiedzie, następnie które sugeruje, że występuje problem z konfiguracją aplikacji hello i uwierzytelnianie Kerberos nie działa.

Jeśli protokołu Kerberos nie jest dostępna, uwierzytelniania aplikacji hello wyboru negocjowania ustawienia w IIS toomake się, że jest wyświetlane najwyżej z NTLM tuż poniżej. (Nie Negotiate: kerberos lub Negotiate: protokołu PKU2U). Nadal tylko, jeśli protokół Kerberos jest funkcjonalności.

   ![Dostawców uwierzytelniania systemu Windows](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Z protokołu Kerberos i NTLM w miejscu umożliwia teraz tymczasowo wyłączyć wstępnego uwierzytelniania dla aplikacji hello w portalu hello. Zobacz, czy można do niego dostęp z hello Internetem przy użyciu hello zewnętrznego adresu URL. Powinny być tooauthenticate zostanie wyświetlony monit o i powinna być toodo może więc z hello tego samego konta hello używany w poprzednim kroku. Jeśli nie, to oznacza problem z hello zaplecza aplikacji i nie KCD w ogóle.

-   Teraz ponownie włączyć wstępnego uwierzytelniania w portalu hello i uwierzytelniania za pośrednictwem platformy Azure przez podejmowanie próby tooconnect toohello aplikacji za pomocą jego zewnętrznego adresu URL. Logowanie Jednokrotne nie powiodło się, należy Zobacz niedozwolonych komunikat w przeglądarce hello, a także zdarzenia 13022 w dzienniku hello:

    *Łącznik serwera Proxy aplikacji usługi Microsoft AAD nie może uwierzytelnić użytkownika hello, ponieważ powitania serwera wewnętrznej bazy danych odpowiada tooKerberos prób uwierzytelnienia z powodu błędu HTTP 401.*

    ![Dostęp zabroniony błąd 401 HTTTP](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Sprawdź, pula aplikacji hello skonfigurowane tooensure hello usług IIS aplikacji hello toouse skonfigurowany, tego samego konta, które hello SPN zostały skonfigurowane przed w usłudze AD, przechodząc w usługach IIS, jak przedstawiono poniżej

    ![Okno konfiguracji aplikacji usług IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Znając tożsamości hello, należy wydać następujące powitania od cmd monitu toomake się, że to konto jest konfigurowana ostatecznie hello SPN w. Na przykład **setspn – q http/spn.wacketywack.com**

    ![Okno polecenia SetSPN](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Sprawdź, że hello SPN zdefiniowane w odniesieniu do ustawień aplikacji hello w portalu hello jest hello tej samej nazwy SPN skonfigurowanego przed hello docelowe AD konto używane przez pulę aplikacji hello aplikacji

   ![Konfiguracja SPN w portalu Azure](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Przejdź do usług IIS i wybierz hello **edytora konfiguracji** opcję dla aplikacji hello, a następnie przejdź zbyt**system.webServer/security/authentication/windowsAuthentication** toomake się tym **UseAppPoolCredentials** ustawiono tootrue

   ![Opcja credential pul aplikacji konfiguracji usług IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Podczas jest przydatny do zwiększania wydajności hello operacji protokołu Kerberos, pozostawiając włączono obsługę trybu jądra powoduje także, że bilet hello na powitania żądanej usługi toobe odszyfrować za pomocą konta komputera. Jest to również hello systemu lokalnego, więc o tego podziału tootrue zestaw KCD, gdy aplikacja hello jest obsługiwana na wielu serwerach w farmie.

-   Jako dodatkową kontrolę, można również toodisable hello **rozszerzone** ochrony zbyt. Było napotkano scenariuszy, w którym okazało toobreak KCD po włączeniu w bardzo określonej konfiguracji, gdy aplikacja jest publikowany jako podfolderem folderu hello domyślnej witryny sieci Web. Ten sam jest skonfigurowany do uwierzytelniania anonimowego, pozostawiając całego okna dialogowe hello nieaktywna co sugeruje, że obiekty podrzędne nie będzie dziedziczy wszystkie aktywne ustawienia. Jednak gdy możliwości zawsze zalecamy posiadanie to włączone, więc wszelkimi środkami testu, ale nie zapomnij toorestore to tooenabled.

Te dodatkowe kontrole powinny umieszczono należy na toostart Śledź przy użyciu opublikowanych aplikacji. Można przejść od razu pokrętła się dodatkowe łączniki, które są również skonfigurowana toodelegate, ale jeśli nie musisz kwestie następnie będzie Sugerujemy odczytu naszych bardziej szczegółowym opisem technicznym [hello kompletny przewodnik po Rozwiązywanie problemów z usługi Azure AD aplikacji Serwer proxy](https://aka.ms/proxytshootpaper)

Jeśli nadal tooprogress problemu, pomocy technicznej może być większa niż tooassist wszystkiego i kontynuować w tym miejscu. Tworzenie biletu pomocy technicznej bezpośrednio z poziomu portalu hello i naszych inżynierów będzie dotrzeć tooyou.

## <a name="other-scenarios"></a>Inne scenariusze

-   Serwera Proxy aplikacji Azure żądania biletu Kerberos przed wysłaniem jej stosowania tooan żądania. Niektóre 3 aplikacje firm, takich jak Tableau serwera nie chcesz, aby ta metoda uwierzytelniania, a raczej oczekuje więcej z konwencjonalnej hello miejsce tootake negocjacji. pierwsze żądanie Hello jest anonimowy, dzięki czemu toorespond aplikacji hello hello typów uwierzytelniania, które obsługuje za pośrednictwem 401.

-   Podwójny przeskok uwierzytelnianie — często używane w scenariuszach, w którym warstwy aplikacji z wewnętrznej bazy danych i front end wymagające uwierzytelniania, takich jak SQL Reporting Services.

## <a name="next-steps"></a>Następne kroki
[Skonfiguruj ograniczone delegowanie protokołu kerberos (KCD) do domeny zarządzanej](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
