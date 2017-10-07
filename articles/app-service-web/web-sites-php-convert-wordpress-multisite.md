---
title: "aaaConvert tooMultisite WordPress w usłudze Azure App Service"
description: "Dowiedz się, jak tootake istniejącą aplikację sieci web WordPress została utworzona za pośrednictwem galerii hello na platformie Azure i przekonwertować go tooWordPress wdrożenia w wielu lokacjach"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Konwertuj tooMultisite WordPress w usłudze Azure App Service
## <a name="overview"></a>Omówienie
*Przez [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

Z tego samouczka dowiesz się, jak tootake istniejącą aplikację sieci web WordPress została utworzona za pośrednictwem galerii hello Azure i przekonwertować go do wdrożenia w wielu lokacjach WordPress instalacji. Ponadto dowiesz się, jak tooassign tooeach domeny niestandardowej z hello witryny podrzędne w ramach instalacji.

Zakłada się, że masz istniejącą instalację programu WordPress. W przeciwnym razie wykonaj hello wskazówki zamieszczone w [utworzyć witrynę sieci web WordPress z galerii hello na platformie Azure][website-from-gallery].

Konwertowanie istniejących WordPress tooMultisite instalacji lokacja zazwyczaj jest dość proste i wiele hello tutaj początkowe kroki pochodzi bezpośrednio z hello [Utwórz sieć A] [ wordpress-codex-create-a-network] strony na powitania [Kodeksu WordPress](http://codex.wordpress.org).

Zacznijmy od początku.

## <a name="allow-multisite"></a>Zezwalaj na wdrożenie w wielu lokacjach
Należy najpierw tooenable wdrożenia w wielu lokacjach przy użyciu hello `wp-config.php` pliku z hello **WP\_Zezwalaj\_wdrożenia w wielu LOKACJACH** stałej. Istnieją dwie metody tooedit pliki aplikacji sieci web: hello najpierw odbywa się za pośrednictwem FTP i hello drugi przy użyciu programu Git. Jeśli użytkownik nie zna jak toosetup żadnej z tych metod można znaleźć toohello następujące samouczki:

* [Witryny sieci web PHP z MySQL i FTP.][website-w-mysql-and-ftp-ftp-setup]
* [Witryny sieci web PHP, MySQL i Git][website-w-mysql-and-git-git-setup]

Otwórz hello `wp-config.php` z edytorem hello wybrane i dodaj następujące hello powyżej hello `/* That's all, stop editing! Happy blogging. */` wiersza.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Można się, że plik hello toosave i przekaż go serwera zapasowego toohello!

## <a name="network-setup"></a>Konfiguracja sieci
Zaloguj się za toohello *wp-admin* obszar aplikacji sieci web i powinien zostać wyświetlony nowy element pod hello **narzędzia** menu o nazwie **konfiguracja sieci**. Kliknij przycisk **konfiguracja sieci** i wypełnij szczegóły hello sieci.

![Ekran konfiguracji sieci][wordpress-network-setup]

W tym samouczku używana hello *podkatalogów* lokacji schematu, ponieważ zawsze powinny działać i będą możemy Trwa konfigurowanie domen niestandardowych dla każdej witryny podrzędnej później w samouczku hello. Jednak powinno być możliwe toosetup poddomeny Zainstaluj Jeśli zamapować domenę za pośrednictwem hello [Azure Portal](https://portal.azure.com) i skonfiguruj poprawnie symboli wieloznacznych DNS.

Aby uzyskać więcej informacji na domeny podrzędne vs podkatalogu konfiguracje Zobacz hello [typów sieci z wieloma lokacjami] [ wordpress-codex-types-of-networks] artykuł na powitania Kodeksu WordPress.

## <a name="enable-hello-network"></a>Włącz hello sieci
sieci Hello jest teraz skonfigurowane w bazie danych hello, ale nie ma jednego pozostałych krok tooenable hello sieci funkcji. Finalizuj hello `wp-config.php` ustawienia i upewnij się, `web.config` prawidłowo kieruje każdej lokacji.

Po kliknięciu przycisku hello **zainstalować** przycisk na powitania *konfiguracja sieci* strony, WordPress podejmie tooupdate hello `wp-config.php` i `web.config` plików. Jednak należy zawsze sprawdzić, hello pliki tooensure hello aktualizacje zostały pomyślnie. Jeśli nie, spowoduje wyświetlenie tego ekranu z hello niezbędne aktualizacje. Edytuj i zapisuj pliki hello.

Po wykonaniu tych aktualizacji należy toolog się i zaloguj z powrotem do hello wp — administrator z pulpitu nawigacyjnego.

Powinno być teraz dodatkowe menu na pasku admin hello etykietą **witryny**. To menu umożliwia toocontrol sieci za pośrednictwem hello **administratora sieci** pulpitu nawigacyjnego.

## <a name="adding-custom-domains"></a>Dodawanie domeny niestandardowe
Witaj [WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] wtyczki ułatwia błyskawicznie tooadd domen niestandardowych tooany lokacji w sieci. Aby toooperate wtyczki hello prawidłowo, należy toodo niektóre dodatkowe ustawienia na powitania portalu, a także u rejestratora domen.

## <a name="enable-domain-mapping-toohello-web-app"></a>Włączanie aplikacji sieci web toohello mapowania domeny
Witaj **wolne** [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) planu trybu nie obsługuje dodawania domen niestandardowych tooWeb aplikacji. Konieczne będzie tooswitch zbyt**Shared** lub **standardowe** tryb. toodo to:

* Zaloguj się za toohello portalu Azure i Znajdź aplikację sieci web. 
* Polecenie hello **skalowanie w górę** karcie **ustawienia**.
* W obszarze **ogólne**, wybierz opcję *SHARED* lub *standardowe*
* Kliknij przycisk **Zapisz**

Może otrzymywać komunikat z pytaniem o zmianę hello tooverify i potwierdzić aplikacji sieci web teraz może pociągnąć za sobą koszt, w zależności od użycia i hello inna konfiguracja, które można ustawić.

Trwa kilka sekund tooprocess hello nowe ustawienia, więc teraz jest odpowiedni moment toostart konfigurowania domeny.

## <a name="verify-your-domain"></a>Sprawdź domenę
Przed Azure Web Apps zezwolić toomap lokacji toohello domeny, należy najpierw tooverify, że masz hello autoryzacji toomap hello domeny. toodo tak, należy dodać nowy wpis DNS tooyour rekordu CNAME.

* Zaloguj się w Menedżerze DNS domeny tooyour
* Tworzenie nowego rekordu CNAME *awverify*
* Punkt *awverify* zbyt*awverify. YOUR_DOMAIN.azurewebsites.NET*

Może trochę potrwać hello DNS zmiany toogo obowiązywać pełne, więc jeśli hello następujące kroki nie działają, przejdź filiżanki kawy, a następnie wróć i spróbuj ponownie.

## <a name="add-hello-domain-toohello-web-app"></a>Dodawanie aplikacji sieci web toohello domeny hello
Zwracany tooyour aplikacji sieci web za pośrednictwem hello portalu Azure, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **domen niestandardowych i SSL**.

Gdy hello *ustawienia protokołu SSL* są wyświetlane, zobaczysz hello pól, których możesz wpisać wszystkie domeny hello, które mają aplikacji sieci web tooyour tooassign. Jeśli domeny nie ma na liście, nie będzie dostępna dla mapowania wewnątrz WordPress, niezależnie od tego, jak hello domeny DNS jest skonfigurowana.

![Zarządzanie domenami niestandardowymi okna dialogowego][wordpress-manage-domains]

Po wpisaniu domenę, w polu tekstowym hello, Azure zweryfikuje hello rekord CNAME, który utworzono wcześniej. Jeśli hello DNS nie została w pełni propagowane, wyświetli się czerwone wskaźnika. Jeśli go zakończyło się pomyślnie, zostanie wyświetlony zielony znacznik wyboru. 

Zwróć uwagę na powitania wyświetlana u dołu okna dialogowego hello hello adresu IP. Należy to hello toosetup rekord dla danej domeny.

## <a name="setup-hello-domain-a-record"></a>Skonfigurować rekord A hello domeny
Jeśli hello inne czynności nie zakończy się powodzeniem, mogą teraz przypisać hello domeny tooyour aplikacji sieci web Azure za pośrednictwem rekord A systemu DNS. 

Jest ważne toonote tutaj że aplikacje sieci web Azure akceptuje zarówno CNAME i, jednak możesz *musi* używać mapowania domeny tooenable rekordów A. Rekord CNAME nie można przesłać dalej tooanother CNAME, który jest Azure utworzone automatycznie, o YOUR_DOMAIN.azurewebsites.net.

Przy użyciu adresu IP hello hello w poprzednim kroku, zwróć tooyour Menedżera DNS i hello konfiguracji IP toothat toopoint rekordów.

## <a name="install-and-setup-hello-plugin"></a>Zainstaluj i skonfiguruj wtyczkę hello
WordPress wdrożenia w wielu lokacjach nie ma obecnie domen niestandardowych toomap wbudowana metoda. Istnieje jednak dodatek o nazwie [WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] dodaje funkcjonalność hello za Ciebie. Zaloguj się w części Administracja sieci toohello witryny i zainstaluj hello **WordPress MU domeny mapowania** wtyczki.

Po instalacji i aktywowanie wtyczki hello, odwiedź stronę **ustawienia** > **mapowania domeny** tooconfigure hello wtyczki. W pierwszym polu tekstowym hello *adres IP serwera*, wejściowych hello adres IP używany toosetup hello rekord hello domeny. Ustaw dowolne *opcje domeny* chcesz (domyślne hello często są poprawnie) i kliknij przycisk **zapisać**.

## <a name="map-hello-domain"></a>Mapa hello domeny
Odwiedź hello **pulpitu nawigacyjnego** hello lokacji mają toomap hello domeny do. Polecenie **narzędzia** > **mapowania domeny** i typ hello nowej domeny w pole tekstowe hello i kliknij przycisk **Dodaj**.

Domyślnie hello nowej domeny będzie ponownie zapisane toohello wygenerowana automatycznie lokacji domeny. Jeśli chcesz toohave wszystkie ruch wysyłany toohello nowej domeny, sprawdź hello *domeny podstawowej ten blog* pole przed zapisaniem. Można dodać dowolną liczbę domen tooa lokacji, ale może zawierać tylko jeden podstawowy.

## <a name="do-it-again"></a>Należy go ponownie
Aplikacje sieci Web platformy Azure pozwala tooadd nieograniczoną liczbę aplikacji sieci web tooa domen. tooadd innej domeny, konieczne będzie tooexecute hello **Sprawdź domenę** i **skonfigurować rekord A domeny hello** sekcje dla każdej domeny.    

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


