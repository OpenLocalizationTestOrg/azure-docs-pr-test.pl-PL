---
title: "aaaRegister dane z usługi Data Lake Store w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Zarejestruj dane z usługi Data Lake Store w wykazie danych Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Zarejestruj dane z usługi Data Lake Store w wykazie danych Azure
W tym artykule dowiesz się, jak toointegrate Azure Data Lake z usługą Azure Data Catalog toomake dane przechowywane wykrywalny w organizacji integrując z wykazu danych. Aby uzyskać więcej informacji na skatalogowania danych, zobacz [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md). Zobacz toounderstand scenariusze, w których można używać usługi Data Catalog [typowych scenariuszy Azure Data Catalog](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Włączenie subskrypcji platformy Azure** dla publicznej wersji zapoznawczej Data Lake Store. Zobacz [instrukcje](data-lake-store-get-started-portal.md).
* **Konto usługi Azure Data Lake Store**. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md). W tym samouczku, możemy utworzyć konto usługi Data Lake Store o nazwie **datacatalogstore**.

    Po utworzeniu konta hello przekazać tooit zestawu danych przykładowych. W tym samouczku, Daj nam przekazać wszystkie pliki CSV hello hello **AmbulanceData** folderu w hello [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Można użyć różnych klientów, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/), tooupload danych tooa obiektów blob kontenera.
* **Wykaz danych Azure**. Twoja organizacja musi mieć już Azure Data Catalog utworzony dla Twojej organizacji. Tylko jeden katalog jest dozwolona dla każdej organizacji.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Register Data Lake Store jako źródło dla usługi Data Catalog

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Przejdź za`https://azure.microsoft.com/services/data-catalog`i kliknij przycisk **wprowadzenie**.
2. Zaloguj się do portalu usługi Azure Data Catalog hello, a następnie kliknij przycisk **publikowania danych**.

    ![Zarejestruj źródło danych](./media/data-lake-store-with-data-catalog/register-data-source.png "rejestracji źródła danych")
3. Na następnej stronie powitania kliknij **uruchamianie aplikacji**. To pobierze plik manifestu aplikacji hello na tym komputerze. Kliknij dwukrotnie aplikacji hello toostart hello w pliku manifestu.
4. Na stronie powitalnej powitania kliknij **Zaloguj**i wprowadź swoje poświadczenia.

    ![Ekran powitalny](./media/data-lake-store-with-data-catalog/welcome.screen.png "ekranu powitalnego")
5. Na powitania wybierz stronę źródła danych, wybierz **usługi Azure Data Lake**, a następnie kliknij przycisk **dalej**.

    ![Wybierz źródło danych](./media/data-lake-store-with-data-catalog/select-source.png "wybierz źródło danych")
6. Na następnej stronie powitania Podaj hello nazwa konta usługi Data Lake Store, które mają tooregister w wykazie danych. Pozostaw hello inne opcje domyślne, a następnie kliknij przycisk **Connect**.

    ![Połącz źródła toodata](./media/data-lake-store-with-data-catalog/connect-to-source.png "źródła toodata Connect")
7. Hello na następnej stronie można podzielić na powitania po segmentów.

    a. Witaj **hierarchii serwerów** pole reprezentuje strukturę folderów konta usługi Data Lake Store hello. **$Root** reprezentuje hello głównego konta usługi Data Lake Store, i **AmbulanceData** reprezentuje hello folder utworzony w katalogu głównym hello hello konta usługi Data Lake Store.

    b. Witaj **dostępne obiekty** wyświetlane hello pliki i foldery w obszarze hello **AmbulanceData** folderu.

    c. **Pole zarejestrowane obiekty toobe** list hello pliki i foldery, które mają tooregister w wykazie danych Azure.

    ![Wyświetlanie struktury danych](./media/data-lake-store-with-data-catalog/view-data-structure.png "wyświetlanie struktury danych")
8. W tym samouczku należy zarejestrować wszystkie pliki hello w katalogu hello. W tym kliknij hello (![przenieść obiekty](./media/data-lake-store-with-data-catalog/move-objects.png "przenieść obiekty")) toomove przycisk hello wszystkie pliki zbyt**toobe obiektów w zarejestrowany** pole.

    Ponieważ hello danych zostanie zarejestrowany w wykazie danych organizacji, jest zalecane podejścia tooadd niektóre metadane, który mógł później użyć tooquickly zlokalizować hello danych. Można na przykład Dodaj adres e-mail właściciela danych hello (na przykład, jeden, który jest przekazywanie danych hello) lub dodać tag tooidentify hello danych. Przechwytywanie ekranu Hello poniżej zawiera tag czy dodamy toohello danych.

    ![Wyświetlanie struktury danych](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "wyświetlanie struktury danych")

    Kliknij przycisk **zarejestrować**.
9. Witaj następujące przechwytywania ekranu oznacza, że hello danych zostanie pomyślnie zarejestrowana w hello wykazu danych.

    ![Zakończono rejestrację](./media/data-lake-store-with-data-catalog/registration-complete.png "wyświetlanie struktury danych")
10. Kliknij przycisk **Wyświetl Portal** toogo toohello portalu wykazu danych kopii i sprawdź, czy można teraz access hello zarejestrowane danych z portalu hello. toosearch hello danych, można użyć znaczników hello, używanego podczas rejestrowania danych hello.

     ![Wyszukiwanie danych w katalogu](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "wyszukiwanie danych w katalogu")
11. Można teraz wykonywać operacje, takie jak dodawać adnotacje i dokumentacji toohello danych. Aby uzyskać więcej informacji zobacz następujące linki hello.

    * [Adnotuj źródła danych w katalogu danych](../data-catalog/data-catalog-how-to-annotate.md)
    * [Źródła danych dokumentów w wykazie danych](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Zobacz też
* [Adnotuj źródła danych w katalogu danych](../data-catalog/data-catalog-how-to-annotate.md)
* [Źródła danych dokumentów w wykazie danych](../data-catalog/data-catalog-how-to-documentation.md)
* [Integracja z innymi usługami Azure Data Lake Store](data-lake-store-integrate-with-other-services.md)
