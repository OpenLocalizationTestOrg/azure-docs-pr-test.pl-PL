---
title: "Samouczek aaaC ++ dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Samouczek języka C++, który pokazuje tworzenie bazy danych w języku C++ i aplikacji konsolowej przy użyciu zatwierdzonego dla usługi Azure Cosmos DB zestawu SDK języka C++. Azure Cosmos DB to skalowana w skali globalnej usługa bazy danych."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Azure DB rozwiązania Cosmos: Samouczek aplikacji konsoli C++ dla hello interfejsu API usługi DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js dla MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Zapraszamy toohello C++ samouczek dotyczący hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB zatwierdzone zestawu SDK dla języka C++! W ramach tego samouczka utworzysz aplikację konsolową, która tworzy zasoby usługi Azure Cosmos DB, w tym bazę danych w języku C++, oraz wykonuje względem nich zapytania.

Omówione zostaną następujące czynności:

* Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos
* Instalowanie aplikacji
* Tworzenie bazy danych usługi Azure Cosmos DB dla języka C++
* Tworzenie kolekcji
* Tworzenie dokumentów JSON
* Wykonywanie zapytania hello kolekcji
* Zastępowanie dokumentu
* Usuwanie dokumentu
* Usuwanie bazy danych DB rozwiązania Cosmos Azure C++ hello

Nie masz czasu? Nie martw się! Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/stalker314314/DocumentDBCpp). Zobacz [uzyskać kompletne rozwiązanie hello](#GetSolution) Aby uzyskać krótkie instrukcje.

Po ukończeniu samouczka C++ hello, proszę Użyj hello przyciski do głosowania u dołu tej strony toogive hello nam opinii. 

Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach lub [dotrzeć tutaj toous](https://www.research.net/r/8BKRJ3Z). 

Teraz do dzieła!

## <a name="prerequisites-for-hello-c-tutorial"></a>Wymagania wstępne dotyczące samouczka hello C++
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/), z zainstalowanymi składnikami języka hello C++.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Krok 1. Tworzenie konta usługi Azure Cosmos DB
Utwórzmy konto usługi Azure Cosmos DB. Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[instalowanie aplikacji C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Krok 2. Konfigurowanie aplikacji języka C++
1. Otwórz program Visual Studio, a następnie na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**. 
2. W hello **nowy projekt** okna na powitania **zainstalowana** okienku rozwiń **Visual C++**, kliknij przycisk **Win32**, a następnie kliknij przycisk  **Aplikacji konsoli Win32**. Nazwa hello hellodocumentdb projektu, a następnie kliknij przycisk **OK**. 
   
    ![Zrzut ekranu przedstawiający Kreator nowego projektu hello](media/documentdb-cpp-get-started/hello.png)
3. Po uruchomieniu hello Kreator aplikacji Win32, kliknij przycisk **Zakończ**.
4. Po utworzeniu projektu hello, otwórz Menedżera pakietów NuGet hello, klikając prawym przyciskiem myszy hello **hellodocumentdb** projektu w **Eksploratora rozwiązań** i klikając **Zarządzaj pakietami NuGet**. 
   
    ![Zrzut ekranu przedstawiający menu Projekt hello Zarządzanie pakietem NuGet](media/documentdb-cpp-get-started/nuget.png)
5. W hello **NuGet: hellodocumentdb** , kliknij pozycję **Przeglądaj**, a następnie wyszukaj *documentdbcpp*. W wynikach hello wybierz DocumentDbCPP, jak pokazano w hello następującego zrzutu ekranu. Ten pakiet instaluje odwołania tooC c++ REST SDK, który jest zależność hello DocumentDbCPP.  
   
    ![Zrzut ekranu przedstawiający hello DocumentDbCpp pakietu, wyróżniony](media/documentdb-cpp-get-started/cpp.png)
   
    Po dodaniu pakietów hello tooyour projektu, możemy wszystkie toostart zestaw pisanie kodu.   

## <a id="Config"></a>Krok 3. Kopiowanie szczegółów połączenia z witryny Azure Portal dla bazy danych Azure Cosmos DB
Wywołaj [portalu Azure](https://portal.azure.com) i przechodzić między nimi utworzonego konta bazy danych dla bazy danych Azure rozwiązania Cosmos toohello. Wkrótce skontaktujemy hello URI oraz primary key hello z portalu Azure w hello następny krok tooestablish połączenie z naszych fragment kodu w języku C++. 

![Azure rozwiązania Cosmos DB URI i klucze w hello portalu Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Krok 4: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos
1. Dodaj hello następującego kodu źródłowego tooyour nagłówki i przestrzenie nazw, po `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Następnie dodać hello następujący kod tooyour main — funkcja i zastąpienie hello konfiguracji konta i toomatch klucza podstawowego ustawień bazy danych Azure rozwiązania Cosmos w kroku 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Teraz, gdy masz klienta usługi documentdb hello tooinitialize kodu hello Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.

## <a id="CreateDBColl"></a>Krok 5. Tworzenie bazy danych i kolekcji w języku C++
Zanim możemy wykonać ten krok, przejdź na interakcje bazy danych, kolekcji i dokumentów dla osób, które kim są nowe tooAzure DB rozwiązania Cosmos. [Baza danych](documentdb-resources.md#databases) jest kontenerem logicznym magazynu dokumentów podzielonym na kolekcje. A [kolekcji](documentdb-resources.md#collections) jest kontenerem dokumentów JSON i hello skojarzone logiki aplikacji JavaScript. Aby dowiedzieć się więcej o hello Azure DB rozwiązania Cosmos hierarchiczna pojęcia i model zasobów w [pojęcia i model zasobów hierarchiczna bazy danych Azure rozwiązania Cosmos](documentdb-resources.md).

toocreate a bazy danych i odpowiedniej kolekcji dodać hello kod zakończenia toohello funkcji main. Spowoduje to utworzenie bazy danych o nazwie "FamilyRegistry" i kolekcję o nazwie "FamilyCollection" przy użyciu konfiguracji klienta hello zadeklarowany w poprzednim kroku hello.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Krok 6. Tworzenie dokumentu
[Dokumenty](documentdb-resources.md#documents) są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Teraz można wstawić dokument do usługi Azure Cosmos DB. Można utworzyć dokumentu, kopiując powitania po kod na końcu hello hello main — funkcja. 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

toosummarize, ten kod tworzy bazy danych Azure rozwiązania Cosmos bazy danych, kolekcji i dokumentów, które można zbadać w Eksploratora dokumentów w portalu Azure. 

![Samouczek C++ — Diagram pokazujący hello hierarchiczną relację między hello konta, hello bazy danych, kolekcji hello i hello dokumentów](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB
Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji. Witaj następujący przykładowy kod przedstawia zapytanie zostało nawiązane przy użyciu składni SQL, który można uruchomić względem dokumentów hello utworzony w poprzednim kroku hello.

Funkcja Hello przyjmuje jako argumenty hello unikatowego identyfikatora lub identyfikator zasobu hello bazy danych i kolekcji hello wraz z powitania klienta dokumentu. Dodaj następujący kod przed funkcją main.

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Replace"></a>Krok 8. Zastępowanie dokumentu
Azure DB rozwiązania Cosmos obsługuje zastępowanie dokumentów JSON, jak pokazano w hello następującego kodu. Dodaj ten kod po hello executesimplequery funkcji.

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <a id="Delete"></a>Krok 9. Usuwanie dokumentu
Azure DB rozwiązania Cosmos obsługuje usuwanie dokumentów JSON, możesz to zrobić przez kopiowanie i wklejanie hello następującego kodu po hello replacedocument funkcji. 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="DeleteDB"></a>Krok 10. Usuwanie bazy danych
Trwa usuwanie hello utworzone bazy danych usuwa hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).

Skopiuj i Wklej hello następującego fragmentu kodu (Funkcja oczyszczania) po bazy danych hello deletedocument funkcja tooremove hello i wszystkie zasoby podrzędne hello.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Krok 11. Uruchamianie całej aplikacji w języku C++!
Firma Microsoft zostało dodane toocreate kodu, zapytania, modyfikowanie i usuwanie różnymi zasobami Azure DB rozwiązania Cosmos.  Poinformuj nas teraz okablować to się przez dodanie wywołania toothese różne funkcje z naszym głównym funkcji w hellodocumentdb.cpp oraz niektóre komunikaty diagnostyczne.

Można to zrobić, zastępując hello główną funkcją aplikacji hello następującego kodu. Ten zapisy za pośrednictwem hello account_configuration_uri i primary_key skopiowane do kodu hello w kroku 3, więc tej wartości hello wiersza lub kopiowanie w ponownie zapisać hello portalu. 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

Powinny teraz toobuild może być i uruchamianie kodu w programie Visual Studio, naciskając klawisz F5 lub też w hello okno terminalu lokalizowania aplikacji hello i uruchamiając hello pliku wykonywalnego. 

Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy hello. Witaj dane wyjściowe powinny odpowiadać hello następującego zrzutu ekranu.

![Dane wyjściowe aplikacji usługi Azure Cosmos DB w języku C++](media/documentdb-cpp-get-started/console.png)

Gratulacje! Po ukończeniu samouczka C++ hello i ma swoją pierwszą aplikację konsoli bazy danych rozwiązania Cosmos Azure!

## <a id="GetSolution"></a>Pobierz kompletnego rozwiązania samouczka hello C++
rozwiązania GetStarted hello toobuild, który zawiera wszystkie przykłady hello w tym artykule, potrzebne są następujące hello:

* [Konto usługi Azure Cosmos DB][create-account].
* Witaj [GetStarted](https://github.com/stalker314314/DocumentDBCpp) rozwiązanie jest dostępne w witrynie GitHub.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


