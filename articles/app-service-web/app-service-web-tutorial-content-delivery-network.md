---
title: "aaaAdd tooan CDN usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dodaj toocache usłudze Azure App Service tooan sieci dostarczania zawartości (CDN) i dostarczanie plików statycznych z serwerów klientów Zamknij tooyour wokół hello world."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Dodaj tooan sieci dostarczania zawartości (CDN) usługi Azure App Service

[Usługa Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) buforuje zawartość statyczną sieci web w strategicznie rozmieszczonych lokalizacjach tooprovide maksymalnej przepływności dostarczania zawartości toousers. Hello CDN również zmniejsza obciążenie serwera w aplikacji sieci web. Ten samouczek pokazuje, jak tooa Azure CDN tooadd [aplikacji sieci web w usłudze Azure App Service](app-service-web-overview.md). 

Oto strony głównej hello hello próbki statycznego HTML lokacji, która będzie współpracować:

![Strona główna przykładowej aplikacji](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Zawartość:

> [!div class="checklist"]
> * Tworzenie punktu końcowego usługi CDN.
> * Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.
> * Użyj zapytania ciągi wersji toocontrol w pamięci podręcznej.
> * Użyj domeny niestandardowej dla punktu końcowego CDN hello.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

- [Zainstaluj oprogramowanie Git](https://git-scm.com/)
- [Zainstaluj interfejs wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Tworzenie aplikacji sieci web hello

Aplikacja sieci web hello toocreate, który będzie działać z hello wykonaj [statycznych Szybki Start — HTML](app-service-web-get-started-html.md) za pośrednictwem hello **przeglądania toohello aplikacji** krok.

### <a name="have-a-custom-domain-ready"></a>Przygotowywanie domeny niestandardowej

krok domeny niestandardowej hello toocomplete tego samouczka należy tooown niestandardową domenę i mają dostęp tooyour DNS rejestru dla dostawcy domeny (na przykład GoDaddy). Na przykład tooadd wpisów DNS dla `contoso.com` i `www.contoso.com`, musi mieć ustawienia DNS hello tooconfigure dostępu dla hello `contoso.com` domeny głównej.

Jeśli nie masz jeszcze nazwy domeny, należy wziąć pod uwagę następujące hello [usługi aplikacji — samouczek domeny](custom-dns-web-site-buydomains-web-app.md) toopurchase domeny przy użyciu hello portalu Azure. 

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Otwórz przeglądarkę i przejdź toohello [portalu Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Tworzenie profilu i punktu końcowego usługi CDN

Hello lewy pasek nawigacyjny, wybierz **usługi aplikacji**, a następnie wybierz aplikacji hello, który został utworzony w hello [statycznych Szybki Start — HTML](app-service-web-get-started-html.md).

![Wybierz aplikację usługi aplikacji w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

W hello **usługi aplikacji** strony w hello **ustawienia** zaznacz **sieci > Konfigurowanie usługi Azure CDN aplikacji**.

![Wybierz sieci CDN w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

W hello **Azure Content Delivery Network** Podaj hello **nowy punkt końcowy** ustawień określonych w tabeli hello.

![Tworzenie profilu i punktu końcowego w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Ustawienie | Sugerowana wartość | Opis |
| ------- | --------------- | ----------- |
| **Profil CDN** | myCDNProfile | Wybierz **Utwórz nowy** toocreate profilu CDN. Profil CDN jest kolekcją punktów końcowych usługi CDN z hello samą warstwę cenową. |
| **Warstwa cenowa** | Standard Akamai | Witaj [warstwy cenowej](../cdn/cdn-overview.md#azure-cdn-features) określa hello dostawcy i dostępnych funkcji. W tym samouczku używamy Akamai standardowa. |
| **Nazwa punktu końcowego usługi CDN** | Dowolną nazwę, która jest unikatowa w domenie azureedge.net hello | Możesz uzyskać dostępu do buforowanych zasobów w domenie hello  *\<endpointname >. azureedge.net*.

Wybierz pozycję **Utwórz**.

Platforma Azure tworzy hello profilu i punktu końcowego. Witaj nowy punkt końcowy jest wyświetlany w hello **punkty końcowe** listy na hello tej samej stronie, a jego obsługa została zainicjowana hello stan to **systemem**.

![Nowy punkt końcowy na liście](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Test hello punktu końcowego CDN

W przypadku wybrania warstwy cenowej Verizon propagacja punktu końcowego trwa zwykle około 90 minut. W przypadku warstwy Akamai propagacja zajmuje kilka minut.

Witaj Przykładowa aplikacja ma `index.html` pliku i *css*, *img*, i *js* foldery, które zawierają inne zasoby statyczne. Hello zawartości ścieżki wszystkie te pliki są takie same hello na powitania punktu końcowego CDN. Na przykład dostęp zarówno hello następujące adresy URL hello *bootstrap.css* pliku w hello *css* folderu:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Przejdź toohello przeglądarki, następującego adresu URL:

```
http://<endpointname>.azureedge.net/index.html
```

![Strona główna aplikacji przykładowej udostępnianej przez usługę CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Zostanie wyświetlony hello sama strona uruchomiono wcześniej w aplikacji sieci web platformy Azure. Usługi Azure CDN ma pobrać zasoby aplikacji hello pochodzenia sieci web i obsługujący z hello punktu końcowego CDN

tooensure, że ta strona jest buforowany w hello CDN, strona hello odświeżania. Dwa żądania dla hello zasobów tego samego są czasami wymagane dla hello CDN toocache hello żądanej zawartości.

Aby uzyskać więcej informacji o sposobie tworzenia profilów i punktów końcowych usługi Azure CDN, zobacz [Wprowadzenie do usługi Azure CDN](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Przeczyść hello CDN

Witaj CDN okresowo odświeża jej zasobach z aplikacji sieci web pochodzenia hello na podstawie hello time to live (TTL) konfiguracji. Witaj, domyślny czas wygaśnięcia wynosi siedem dni.

W czasie należy toorefresh hello CDN przed hello wygaśnięcia TTL — na przykład podczas wdrażania aplikacji sieci web zaktualizowane toohello zawartości. tootrigger odświeżania, można ręcznie przeczyścić hello CDN zasobów. 

W tej sekcji samouczka hello wdrażanie aplikacji sieci web toohello zmiany i przeczyścić hello CDN tootrigger hello CDN toorefresh pamięci podręcznej.

### <a name="deploy-a-change-toohello-web-app"></a>Wdrażanie aplikacji sieci web toohello zmiany

Otwórz hello `index.html` i Dodaj "-V2" toohello H1 nagłówka, jak pokazano w hello poniższy przykład: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Zatwierdź zmiany i wdróż je toohello aplikacji sieci web.

```bash
git commit -am "version 2"
git push azure master
```

Po zakończeniu wdrażania URL aplikacji sieci web toohello przeglądania i zostanie wyświetlony hello zmienić.

```
http://<appname>.azurewebsites.net/index.html
```

![Ciąg V2 w tytule aplikacji sieci Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Adres URL punktu końcowego CDN toohello przeglądania dla strony głównej hello, a nie widzisz hello zmienić, ponieważ wersja buforowana hello w hello CDN nie jeszcze wygasł. 

```
http://<endpointname>.azureedge.net/index.html
```

![Brak ciągu V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Przeczyść hello sieci CDN w portalu hello

tootrigger hello CDN tooupdate jego wersja buforowana, Przeczyść hello CDN.

W nawigacji po lewej stronie portalu hello, wybierz **grup zasobów**, a następnie wybierz grupę zasobów hello, który został utworzony dla aplikacji sieci web (myResourceGroup).

![Wybieranie grupy zasobów](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Hello listy zasobów wybierz punkt końcowy CDN.

![Wybieranie punktu końcowego](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

U góry hello hello **punktu końcowego** kliknij przycisk **przeczyścić**.

![Wybieranie pozycji Przeczyść](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Wprowadź hello ścieżek zawartości mają toopurge. Można przekazywać toopurge ścieżka całego pliku pojedynczego pliku lub toopurge segmentu ścieżki i Odśwież całą zawartość w folderze. Ponieważ zmieniono `index.html`, upewnij się, że jest jedna ze ścieżek hello.

U dołu hello strony hello, zaznacz pole wyboru **przeczyścić**.

![Strona przeczyszczania](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Sprawdź, że hello CDN jest aktualizowany

Poczekaj, aż żądanie przeczyszczenia hello zakończy przetwarzanie zwykle kilka minut. toosee hello bieżący stan, hello wybierz ikonę dzwonka na początku hello hello strony. 

![Powiadomienie o przeczyszczaniu](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Przeglądaj URL punktu końcowego CDN toohello `index.html`, i teraz zobaczyć hello dodane toohello tytuł na stronie głównej hello V2. Ta operacja wyświetla odświeżeniu pamięci podręcznej CDN hello.

```
http://<endpointname>.azureedge.net/index.html
```

![Ciąg V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Aby uzyskać więcej informacji, zobacz [Przeczyszczanie punktu końcowego usługi Azure CDN](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Korzystać z zawartości tooversion ciągi zapytania

Hello Azure CDN oferuje następujące opcje zachowanie buforowania hello:

* Ignoruj ciągi zapytań
* Pomiń buforowanie dla ciągów zapytań
* Buforuj każdy unikatowy adres URL 

Witaj pierwszy z nich jest hello domyślnej, co oznacza, że istnieje tylko jedna wersja buforowanych zasobów, niezależnie od hello ciągu zapytania w adresie URL hello. 

W tej sekcji samouczka hello zmienisz hello buforowanie toocache zachowanie każdy unikatowy adres URL.

### <a name="change-hello-cache-behavior"></a>Należy zmienić to zachowanie pamięci podręcznej hello

W portalu Azure hello **punktu końcowego CDN** wybierz pozycję **pamięci podręcznej**.

Wybierz **Buforuj każdy unikatowy adres URL** z hello **zachowanie buforowania ciągu kwerendy** listy rozwijanej.

Wybierz pozycję **Zapisz**.

![Wybieranie zachowania buforowania ciągów zapytań](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Sprawdzanie, czy unikatowe adresy URL są buforowane osobno

W przeglądarce przejdź do strony głównej toohello na punkt końcowy CDN hello, ale zawierają ciąg zapytania: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Witaj CDN zwraca hello bieżącej zawartości sieci web aplikacji, w tym "V2" hello nagłówka. 

tooensure, że ta strona jest buforowany w hello CDN, strona hello odświeżania. 

Otwórz `index.html` i zmień "V2" za "3" i wdrażanie zmiany hello. 

```bash
git commit -am "version 3"
git push azure master
```

W przeglądarce Przejdź takie jak adres URL punktu końcowego CDN toohello z nowego ciągu zapytania `q=2`. Witaj CDN pobiera hello bieżącego `index.html` plików i wyświetla "3".  Ale jeśli oddalisz się punkt końcowy CDN toohello z hello `q=1` ciągu, zapytania zobacz "2".

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 w tytule w usłudze CDN, ciąg zapytania 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 w tytule w usłudze CDN, ciąg zapytania 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Te dane wyjściowe pokazuje, czy każdy ciąg zapytania jest traktowane inaczej:

* q = 1 był używany przed, więc zawartości z pamięci podręcznej są zwracane (V2).
* q = 2 jest nowy, więc hello najnowszą zawartość aplikacji sieci web są pobierane i zwracane (V3).

Aby uzyskać więcej informacji, zobacz [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md) (Sterowanie zachowaniem buforowania usługi CDN za pomocą ciągów zapytań).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Mapa punktu końcowego usługi CDN tooa domeny niestandardowej

Twoje domeny niestandardowej tooyour punktu końcowego CDN będzie mapy przez utworzenie rekordu CNAME. Rekord CNAME jest funkcją DNS, która mapuje domeny docelowej tooa domeny źródłowej. Na przykład mogą być mapowane `cdn.contoso.com` lub `static.contoso.com` zbyt`contoso.azureedge.net`.

Jeśli nie masz domenę niestandardową, należy wziąć pod uwagę następujące hello [usługi aplikacji — samouczek domeny](custom-dns-web-site-buydomains-web-app.md) toopurchase domeny przy użyciu hello portalu Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Znajdź hello toouse nazwy hosta z hello CNAME

W portalu Azure hello **punktu końcowego** upewnij się, że **omówienie** wybrano hello pozostałych nawigacji, a następnie wybierz opcję hello **+ domeny niestandardowe** przycisk u góry hello hello strony.

![Wybieranie opcji dodawania domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

W hello **dodać niestandardową domenę** strony, zobacz hello punktu końcowego host name toouse utworzyć rekord CNAME. Nazwa hosta Hello jest pochodną adres URL punktu końcowego CDN:  **&lt;EndpointName >. azureedge.net**. 

![Strona dodawania domeny](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Skonfiguruj hello CNAME u rejestratora domen

Przejdź do witryny sieci web rejestratora domen tooyour, a następnie zlokalizuj hello sekcji do tworzenia rekordów DNS. Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).

Znajdź sekcję hello zarządzania CNAME. Może mieć toogo tooan Zaawansowane ustawienia strony i poszukaj słowa hello CNAME, aliasu lub poddomeny.

Utwórz rekord CNAME mapujący z wybranym domeny podrzędnej (na przykład **statycznych** lub **cdn**) toohello **nazwę hosta punktu końcowego** pokazano wcześniej w portalu hello. 

### <a name="enter-hello-custom-domain-in-azure"></a>Wprowadź domenę niestandardową hello na platformie Azure

Zwraca toohello **dodać niestandardową domenę** strony, a następnie wprowadź domenę niestandardową, w tym poddomeny hello, w oknie dialogowym hello. Na przykład wprowadź wartość `cdn.contoso.com`.   
   
Azure sprawdza, czy istnieje rekord CNAME powitania dla hello nazwy domeny, który został wprowadzony. Jeśli hello CNAME jest poprawny, domeny niestandardowej jest weryfikowana.

Może upłynąć czasu dla serwerów tooname toopropagate rekordów CNAME z hello na powitania Internet. Jeśli domena nie została zweryfikowana natychmiast, zaczekaj kilka minut i spróbuj ponownie.

### <a name="test-hello-custom-domain"></a>Domena niestandardowa hello testu

W przeglądarce Przejdź toohello `index.html` pliku używania domeny niestandardowej (na przykład `cdn.contoso.com/index.html`) tooverify będący wynikiem hello hello takie same jak przejściu bezpośrednio za`<endpointname>azureedge.net/index.html`.

![Strona główna przykładowej aplikacji wyświetlona przy użyciu adresu URL domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Aby uzyskać więcej informacji, zobacz [domeny niestandardowej tooa zawartości mapy usługi Azure CDN](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Następne kroki

Wiadomości:

> [!div class="checklist"]
> * Tworzenie punktu końcowego usługi CDN.
> * Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.
> * Użyj zapytania ciągi wersji toocontrol w pamięci podręcznej.
> * Użyj domeny niestandardowej dla punktu końcowego CDN hello.

Dowiedz się, jak toooptimize wydajność sieci CDN w hello następujące artykuły:

> [!div class="nextstepaction"]
> [Poprawianie wydajności poprzez kompresowanie plików w usłudze Azure CDN](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN](../cdn/cdn-preload-endpoint.md)
