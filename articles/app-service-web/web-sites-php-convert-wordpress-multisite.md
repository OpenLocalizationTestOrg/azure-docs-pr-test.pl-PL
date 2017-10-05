---
title: "Konwertuj WordPress do wdrożenia w wielu lokacjach w usłudze aplikacji Azure"
description: "Dowiedz się, jak wykonać istniejącej aplikacji sieci web WordPress została utworzona za pośrednictwem galerii na platformie Azure i przekształcić ją w wielu lokacjach WordPress"
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
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a>Konwertuj WordPress do wdrożenia w wielu lokacjach w usłudze aplikacji Azure
## <a name="overview"></a>Omówienie
*Przez [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

Z tego samouczka dowiesz się, jak wykonać istniejącej aplikacji sieci web WordPress została utworzona za pośrednictwem galerii na platformie Azure oraz przekształcać je do instalacji WordPress wdrożenia w wielu lokacjach. Ponadto dowiesz jak przypisać niestandardową domenę, wszystkie lokacje podrzędne w ramach instalacji.

Zakłada się, że masz istniejącą instalację programu WordPress. W przeciwnym razie wykonaj wskazówki zamieszczone w [utworzyć witrynę sieci web WordPress z poziomu galerii na platformie Azure][website-from-gallery].

Konwertowanie istniejących WordPress instalacji jednej lokacji do wdrożenia w wielu lokacjach ogólnie jest dość proste i wiele początkowe kroki pochodzi bezpośrednio z [Utwórz sieć A] [ wordpress-codex-create-a-network] strony na [Kodeksu WordPress](http://codex.wordpress.org).

Zacznijmy od początku.

## <a name="allow-multisite"></a>Zezwalaj na wdrożenie w wielu lokacjach
Należy najpierw włączyć wdrożenie w wielu lokacjach przy użyciu `wp-config.php` pliku z **WP\_Zezwalaj\_wdrożenia w wielu LOKACJACH** stałej. Istnieją dwie metody, aby edytować pliki aplikacji sieci web: pierwszy odbywa się za pośrednictwem FTP, a drugi przy użyciu programu Git. Jeśli znasz konfiguracji każdej z tych metod, przeczytaj następujące samouczki:

* [Witryny sieci web PHP z MySQL i FTP.][website-w-mysql-and-ftp-ftp-setup]
* [Witryny sieci web PHP, MySQL i Git][website-w-mysql-and-git-git-setup]

Otwórz `wp-config.php` plik w edytorze wybrane i dodaj następującą powyżej `/* That's all, stop editing! Happy blogging. */` wiersza.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Pamiętaj zapisać plik i przekaż go do serwera!

## <a name="network-setup"></a>Konfiguracja sieci
Zaloguj się do *wp-admin* obszar aplikacji sieci web i powinien zostać wyświetlony nowy element pod **narzędzia** menu o nazwie **konfiguracja sieci**. Kliknij przycisk **konfiguracja sieci** i uzupełnij informacje dotyczące sieci.

![Ekran konfiguracji sieci][wordpress-network-setup]

W tym samouczku używana *podkatalogów* lokacji schematu, ponieważ zawsze powinny działać i będą możemy Trwa konfigurowanie domen niestandardowych dla każdej witryny podrzędnej później w samouczku. Jednak powinno być możliwe Instalatorowi na zainstalowanie poddomeny, jeśli mapowanie domeny przy użyciu [Azure Portal](https://portal.azure.com) i skonfiguruj poprawnie symboli wieloznacznych DNS.

Więcej informacji na temat wersji programu vs domenę podrzędną podkatalogu konfiguracje dla [typów sieci z wieloma lokacjami] [ wordpress-codex-types-of-networks] artykuł na temat Kodeksu WordPress.

## <a name="enable-the-network"></a>Włącz sieci
Sieć jest teraz skonfigurowane w bazie danych, ale jest jednym z pozostałych etapów do włączenia funkcji sieci. Finalizuj `wp-config.php` ustawienia i upewnij się, `web.config` prawidłowo kieruje każdej lokacji.

Po kliknięciu przycisku **zainstalować** znajdującego się na *konfiguracja sieci* strony zaktualizować podejmie WordPress `wp-config.php` i `web.config` plików. Jednak należy zawsze sprawdzić pliki, aby upewnić się, że aktualizacje zostały pomyślnie. Jeśli nie, spowoduje wyświetlenie tego ekranu z niezbędne aktualizacje. Edytuj i zapisuj pliki.

Po wykonaniu tych aktualizacji, musisz się wylogować i zalogować z powrotem do pulpitu nawigacyjnego wp administratora.

Powinny teraz istnieć dodatkowe menu na pasku administratora z etykietą **witryny**. To menu pozwala na kontrolowanie sieci za pomocą **administratora sieci** pulpitu nawigacyjnego.

## <a name="adding-custom-domains"></a>Dodawanie domeny niestandardowe
[WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] wtyczki ułatwia błyskawicznie do dodawania niestandardowych domen do dowolnej lokacji w sieci. Dodatek plug-in, aby działać prawidłowo, należy wykonać pewne dodatkowe ustawienia w portalu, a także u rejestratora domen.

## <a name="enable-domain-mapping-to-the-web-app"></a>Włącz mapowanie domeny aplikacji sieci web
**Wolne** [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) planu trybu nie obsługuje dodawania niestandardowych domen do aplikacji sieci Web. Musisz przełączyć się do **Shared** lub **standardowe** tryb. W tym celu:

* Zaloguj się do portalu Azure i Znajdź aplikację sieci web. 
* Polecenie **skalowanie w górę** karcie **ustawienia**.
* W obszarze **ogólne**, wybierz opcję *SHARED* lub *standardowe*
* Kliknij przycisk **Zapisz**

Użytkownik może zostać wyświetlony komunikat z pytaniem, aby zweryfikować zmiany i potwierdzić, że aplikacja sieci web teraz może pociągnąć za sobą koszt, w zależności od użycia i konfiguracji, które można ustawić.

Trwa kilka sekund przetworzył nowe ustawienia, więc teraz jest odpowiedni moment, aby rozpocząć konfigurowanie domeny.

## <a name="verify-your-domain"></a>Sprawdź domenę
Przed Azure aplikacje sieci Web będzie można zamapować domenę do witryny, należy najpierw sprawdź, czy masz autoryzację do mapowania do domeny. Aby to zrobić, należy dodać nowy rekord CNAME do wpisu DNS.

* Zaloguj się do Twojej domeny Menedżera DNS
* Tworzenie nowego rekordu CNAME *awverify*
* Punkt *awverify* do *awverify. YOUR_DOMAIN.azurewebsites.NET*

Może upłynąć trochę czasu, zanim zmiany DNS zaczynają obowiązywać pełne, więc jeśli poniższe kroki nie działają, przejdź filiżanki kawy, a następnie wróć i spróbuj ponownie.

## <a name="add-the-domain-to-the-web-app"></a>Dodawanie domeny do aplikacji sieci web
Powrót do aplikacji sieci web za pośrednictwem portalu Azure, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **domen niestandardowych i SSL**.

Gdy *ustawienia protokołu SSL* są wyświetlane, zobaczysz pola, w którym możesz wpisać wszystkie domeny, które chcesz przypisać do aplikacji sieci web. Jeśli domeny nie ma na liście, nie będzie dostępna dla mapowania wewnątrz WordPress, niezależnie od tego, jak domena DNS jest skonfigurowana.

![Zarządzanie domenami niestandardowymi okna dialogowego][wordpress-manage-domains]

Po wpisaniu domenę, w polu tekstowym, Azure zweryfikuje rekord CNAME, który utworzono wcześniej. Jeśli DNS nie została w pełni propagowane, wyświetli się czerwone wskaźnika. Jeśli go zakończyło się pomyślnie, zostanie wyświetlony zielony znacznik wyboru. 

Zanotuj adres IP wyświetlane w dolnej części okna dialogowego. Będzie on potrzebny można skonfigurować rekordu A dla domeny.

## <a name="setup-the-domain-a-record"></a>Konfiguracja domeny rekordu
Jeśli inne czynności zakończy się powodzeniem, mogą teraz przypisać domeny do aplikacji sieci web platformy Azure za pośrednictwem rekord A systemu DNS. 

Jest w tym miejscu należy pamiętać, że aplikacje sieci web Azure akceptuje zarówno CNAME i, jednak możesz *musi* umożliwiają rekord A Mapowanie domeny. Rekord CNAME nie można przesłać dalej do innego CNAME, czyli co Azure utworzony z YOUR_DOMAIN.azurewebsites.net.

Przy użyciu adresu IP z poprzedniego kroku, wróć do Menedżera DNS i skonfigurować rekord A, aby wskazywał tego adresu IP.

## <a name="install-and-setup-the-plugin"></a>Zainstaluj i skonfiguruj wtyczki
Wdrożenie w wielu lokacjach WordPress aktualnie nie ma wbudowane metodę mapowania domen niestandardowych. Istnieje jednak dodatek o nazwie [WordPress MU domeny mapowania] [ wordpress-plugin-wordpress-mu-domain-mapping] dodaje funkcjonalność dla Ciebie. Zaloguj się do administratora sieci część witryny i zainstaluj **WordPress MU domeny mapowania** wtyczki.

Po zainstalowaniu i aktywowanie wtyczki, odwiedź stronę **ustawienia** > **mapowania domeny** do skonfigurowania wtyczki. W pierwszym polu tekstowym *adres IP serwera*, wprowadź adres IP używany można skonfigurować rekordu A dla domeny. Ustaw dowolne *opcje domeny* można desire (wartości domyślne są często poprawnie), a następnie kliknij przycisk **zapisać**.

## <a name="map-the-domain"></a>Mapa domeny
Odwiedź stronę **pulpitu nawigacyjnego** chcesz mapy domeny do witryny. Polecenie **narzędzia** > **mapowania domeny** i wpisz nazwę nowej domeny w pliku tekstowym i kliknij przycisk **Dodaj**.

Domyślnie nowej domeny będzie ponownie zapisać do domeny lokacji wygenerowana automatycznie. Jeśli chcesz, aby cały ruch wysyłany do nowej domeny, sprawdź *domeny podstawowej ten blog* pole przed zapisaniem. Można dodać dowolną liczbę domen do lokacji, ale może zawierać tylko jeden podstawowy.

## <a name="do-it-again"></a>Należy go ponownie
Aplikacje sieci Web platformy Azure umożliwiają dodawanie nieograniczoną liczbę domen aplikacji sieci web. Aby dodać do innej domeny, konieczne będzie wykonanie **Sprawdź domenę** i **ustawienia domeny rekord** sekcje dla każdej domeny.    

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

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


