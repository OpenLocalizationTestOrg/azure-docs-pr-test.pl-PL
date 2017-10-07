---
title: "wprowadzenie do usługi Azure Search w środowisku Node.js aaaGet | Dokumentacja firmy Microsoft"
description: "Zapoznaj się z procesem tworzenia aplikacji wyszukiwania w hostowanej usłudze wyszukiwania w chmurze na platformie Azure przy użyciu języka programowania Node.js."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Wprowadzenie do usługi Azure Search w środowisku Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Dowiedz się, jak toobuild niestandardowych Node.js Wyszukaj aplikację, która używa usługi Azure Search jako środowiska wyszukiwania. W tym samouczku używana hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello obiekty i operacje używane w tym ćwiczeniu.

My używamy [Node.js](https://Nodejs.org) i NPM, [Sublime Text 3](http://www.sublimetext.com/3)i środowiska Windows PowerShell na toodevelop Windows 8.1 i przetestowania tego kodu.

toorun tej próbki, musi mieć usługi Azure Search, której możesz zarejestrować się w hello [portalu Azure](https://portal.azure.com). Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje krok po kroku.

## <a name="about-hello-data"></a>Dane hello — informacje
Ta przykładowa aplikacja korzysta z danych z hello [Stanów Zjednoczonych Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)zawężonych hello stanu Rhode Island tooreduce hello dataset rozmiaru. Użyjemy tego toobuild danych aplikacji wyszukiwania, która zwraca punkty orientacyjne, takie jak szpitale i szkoły, jak również geologiczne, takie jak strumienie, jeziora i szczyty.

W tej aplikacji hello **DataIndexer** budowania i obciążeń hello indeksu przy użyciu [indeksatora](https://msdn.microsoft.com/library/azure/dn798918.aspx) konstrukcja pobierania hello filtrowane danych agencji USGS z publicznej usługi Azure SQL Database. Poświadczenia i połączenia źródło danych w trybie online toohello informacji znajduje się w kodzie programu hello. Nie jest konieczna żadna dodatkowa konfiguracja.

> [!NOTE]
> Zastosowaliśmy filtr na toostay tego zestawu danych w obszarze hello 10 000 dokumentów limit hello warstwy cenowej bezpłatna. Jeśli używasz hello warstwy standardowa, ten limit nie ma zastosowania. Aby uzyskać szczegółowe informacje o pojemności dla każdej warstwy cenowej, zobacz [Search service limits](search-limits-quotas-capacity.md) (Limity usługi wyszukiwania).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Znajdź hello nazwę usługi i klucza interfejsu api usługi Azure Search
Po utworzeniu usługi hello adres zwrotny URL hello portalu tooget toohello lub `api-key`. Tooyour połączenia usługi wyszukiwania wymagają zarówno adresu URL hello i `api-key` tooauthenticate hello wywołania.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na pasku skok hello, kliknij przycisk **usługi wyszukiwania** toolist wszystkie usługi Azure Search aprowizowanych dla subskrypcji.
3. Wybierz usługę hello ma toouse.
4. Na pulpicie nawigacyjnym usługi hello i powinna zostać wyświetlona Kafelki z istotnymi informacjami, takich jak ikonę klucza hello dla uzyskiwania dostępu do kluczy administratora hello.
5. Skopiuj adres URL usługi hello, klucz administratora i klucz zapytania. Należy wszystkie trzy później podczas dodawania ich toohello pliku config.js.

## <a name="download-hello-sample-files"></a>Pobieranie plików przykładowych hello
Za pomocą jednej z hello następujące przykładowe hello toodownload podejścia.

1. Przejdź za[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Kliknij przycisk **Pobierz ZIP**, Zapisz plik zip hello, a następnie Wyodrębnij wszystkie pliki hello zawiera.

Wszystkie kolejne modyfikacje plików i instrukcje uruchamiania będą wykonywane względem plików w tym folderze.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Zaktualizuj hello config.js. przy użyciu adresu URL usługi wyszukiwania i klucza api-key
Przy użyciu hello adresu URL i klucza api-key skopiowanego wcześniej, podaj adres URL hello, klucz administratora i klucz zapytania w pliku konfiguracji.

Klucze administratora przyznają pełną kontrolę nad operacjami usługi, w tym nad tworzeniem i usuwaniem indeksu oraz ładowaniem dokumentów. Z kolei klucze zapytania są dla operacji tylko do odczytu, zwykle używanych przez aplikacje klienckie, łączących tooAzure wyszukiwania.

W tym przykładzie uwzględniamy zapytania hello klucza toohelp zapamiętaniu najlepszego rozwiązania hello przy użyciu klucza zapytania hello w aplikacjach klienckich.

Zrzut ekranu przedstawia następujące Hello **config.js** otwarty w edytorze tekstów, z hello odpowiednimi wpisami tak aby były widoczne, gdy plik hello tooupdate o hello wartości, które są prawidłowe dla usługi wyszukiwania.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Hostowanie środowiska uruchomieniowego dla przykładu hello
przykład Witaj wymaga serwera HTTP, które można zainstalować globalnie za pomocą programu npm.

Okno programu PowerShell dla hello następujące polecenia.

1. Przejdź do folderu toohello, który zawiera hello **package.json** pliku.
2. Wpisz polecenie `npm install`.
3. Wpisz polecenie `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Tworzenie indeksu hello i uruchamianie aplikacji hello
1. Wpisz polecenie `npm run indexDocuments`.
2. Wpisz polecenie `npm run build`.
3. Wpisz polecenie `npm run start_server`.
4. Za pomocą przeglądarki przejdź do strony `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Przeszukiwanie danych agencji USGS
zestaw danych agencji USGS Hello zawiera rekordy, które są odpowiednie toohello stanu Rhode Island. Jeśli klikniesz przycisk **wyszukiwania** na pole wyszukiwania puste, możesz uzyskać hello 50 pierwszych wpisów, który jest domyślnym hello.

Wprowadzenie terminu zapewnia aparat wyszukiwania hello coś toogo na. Spróbuj wprowadzić nazwę regionalną. "Roger Williams" był pierwszym gubernatorem stanu Rhode Island hello. Liczne parki, budynki i szkoły są nazwane jego imieniem.

![][9]

Możesz też wprowadzić jeden z poniższych terminów:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Następne kroki
To jest pierwszy samouczek usługi Azure Search hello, na podstawie Node.js i hello danych agencji USGS. Wraz z upływem czasu będziemy rozszerzać ten samouczek toodemonstrate dodatkowe funkcje wyszukiwania może być toouse w rozwiązaniach niestandardowych.

Jeśli masz już jakieś doświadczenie z usługą Azure Search, możesz użyć tego przykładu jako punktu wyjścia do wypróbowania sugestorów (uzupełnianie przy wpisywaniu lub autouzupełnianie zapytań), filtrów i nawigacji aspektowej. Możesz również ulepszyć stronę wyników wyszukiwania hello przez dodanie liczników i łączenie dokumentów w partie, dzięki czemu użytkownicy mogą przeglądania wyników hello.

TooAzure nowego wyszukiwania? Zaleca się podjęcie próby toodevelop innych samouczków zrozumienia można utworzyć. Można znaleźć w naszych [stronę dokumentacji](https://azure.microsoft.com/documentation/services/search/) toofind więcej zasobów. Można również wyświetlić hello łącza w naszym [listy filmów wideo i samouczków](search-video-demo-tutorial-list.md) tooaccess więcej informacji.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
