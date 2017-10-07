---
title: "Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania Xamarin z uwierzytelnianiem serwisu Facebook | Microsoft Docs"
description: "Przedstawia przykładowy kod .NET, można użyć tooconnect tooand zapytania bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: Budowanie aplikacji sieci Web za pomocą oprogramowania .NET, Xamarin i uwierzytelniania serwisu Facebook

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Będzie tworzenie i wdrażanie aplikacji sieci web listy todo oparty na powitania [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)i hello Azure DB rozwiązania Cosmos autoryzacji aparatu. Aplikacja sieci web listy rzeczy do zrobienia Hello implementuje wzorzec danych użytkownika, który umożliwia toologin użytkowników przy użyciu uwierzytelniania serwisu Facebook i zarządzaj nimi własnych elementów toodo.

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Następnie otwórz plik DocumentDBTodo.sln hello z folderu samples/xamarin/UserItems/xamarin.forms hello w programie Visual Studio. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Witaj w folderze Xamarin hello w kodzie:

* Aplikacja platformy Xamarin. Aplikacja Hello przechowuje elementy hello użytkownika w podzielonym na partycje kolekcję o nazwie UserItems.
* Interfejs API brokera tokenu zasobów. Proste zasobów bazy danych Azure rozwiązania Cosmos toobroker ASP.NET Web API tokeny toohello zalogowani użytkownicy aplikacji hello. Tokeny zasobu to tokeny dostępu krótkim okresie udostępnianie aplikacji hello hello toohello dostęp zalogowany danych użytkownika.

Przepływ uwierzytelniania i danych Hello przedstawiono na poniższym diagramie hello.

* Witaj UserItems kolekcji jest tworzony z kluczem partycji hello "/ Nazwa użytkownika". Określanie klucza partycji dla kolekcji umożliwia tooscale bazy danych Azure rozwiązania Cosmos nieograniczonej jako hello wielu użytkowników oraz elementy rozwoju.
* Aplikacja Xamarin Hello umożliwia toologin użytkowników przy użyciu poświadczeń usługi Facebook.
* Aplikacja Xamarin Hello używa tooauthenticate token dostępu usługi Facebook z interfejsem API ResourceTokenBroker
* broker tokenu Hello zasobu interfejsu API uwierzytelnia hello żądania przy użyciu funkcji uwierzytelniania usługi aplikacji i żądania tokenu zasobów bazy danych Azure rozwiązania Cosmos z dokumentami tooall dostęp do odczytu/zapisu udostępniania klucza partycji hello uwierzytelnionego użytkownika.
* Zasób brokera tokenu zwraca hello zasobów toohello tokenu klienta aplikacji.
* Aplikacja Hello uzyskuje dostęp do elementów todo hello użytkownika za pomocą hello token zasobu.

![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. W pliku Web.config hello w następnym kroku hello użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania identyfikatora URI oraz Primary Key.

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-xamarin-dotnet/keys.png)

2. W programie Visual Studio 2017 r Otwórz plik Web.config hello hello azure-documentdb-dotnet/przykłady/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folderu. 

3. Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość accountUrl hello w pliku Web.config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość accountKey hello w Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 

## <a name="build-and-deploy-hello-web-app"></a>Tworzenie i wdrażanie aplikacji sieci web hello

1. Tworzenie aplikacji witryny sieci Web toohost hello zasobów tokenu brokera usług interfejsu API hello portalu Azure.
2. Hello portalu Azure Otwórz blok ustawień aplikacji hello brokera tokenu hello zasobów witryny sieci Web interfejsu API. Wypełnij następujące ustawienia aplikacji hello:

    * accountUrl — adres URL konta bazy danych Azure rozwiązania Cosmos hello klucze hello na karcie Konto bazy danych Azure rozwiązania Cosmos.
    * accountKey - klucza głównego konta bazy danych Azure rozwiązania Cosmos hello klucze hello na karcie Konto bazy danych Azure rozwiązania Cosmos.
    * Identyfikatory databaseId i collectionId utworzonej bazy danych oraz kolekcji.

3. Opublikuj hello tooyour rozwiązania ResourceTokenBroker utworzyć witryny sieci Web.

4. Otwórz projekt Xamarin hello, a następnie przejdź tooTodoItemManager.cs. Podaj wartości hello accountURL, collectionId, databaseId, a także resourceTokenBrokerURL jako adres url https podstawowej hello hello zasobu brokera tokenu witryny sieci Web.

5. Pełną hello [jak tooconfigure logowanie Facebook toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup samouczka uwierzytelniania serwisu Facebook i konfigurować witrynę ResourceTokenBroker hello.

    Uruchamianie aplikacji platformy Xamarin hello.

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki: 

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello właśnie utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos Utwórz kolekcję przy użyciu hello Eksploratora danych i tworzenia i wdrażania aplikacji platformy Xamarin. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)
