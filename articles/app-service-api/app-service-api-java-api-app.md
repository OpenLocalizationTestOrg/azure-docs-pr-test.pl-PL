---
title: "aaaBuild i wdrażanie aplikacji interfejsu API języka Java w usłudze Azure App Service"
description: "Dowiedz się, jak toocreate aplikacji interfejsu API języka Java pakietu, a następnie wdrożyć go tooAzure usługi aplikacji."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Tworzenie i wdrażanie aplikacji interfejsu API języka Java w usłudze Azure App Service
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Ten samouczek pokazuje, jak toocreate aplikacji Java i wdrożyć ją przy użyciu tooAzure App Service API Apps [Git]. Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić oprogramowanie Java. Kod Hello w tym samouczku jest utworzony przy użyciu [Maven]. [JAX-RS] jest używane toocreate hello usługi RESTful i jest generowany w oparciu o hello [Swagger] specyfikacji metadanych za pomocą hello [edytora programu Swagger].

## <a name="prerequisites"></a>Wymagania wstępne
1. [Java Developer's Kit 8] \(lub nowszy)
2. [Maven] zainstalowane na komputerze deweloperskim
3. [Git] zainstalowany na komputerze deweloperskim
4. Płatna lub [bezpłatnej wersji próbnej] subskrypcji zbyt[Microsoft Azure]
5. Aplikacja testowa HTTP, taka jak [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>Interfejs API hello szkieletu przy użyciu narzędzia Swagger.IO
Hello edytora online swagger.io można wprowadzić kod JSON programu Swagger lub yaml programu reprezentujący hello strukturę interfejsu API. Po utworzeniu hello zaprojektowaniu powierzchni interfejsu API, można wyeksportować kod dla różnych platform i struktur. W następnej sekcji hello hello szkieletu kodu będzie zmodyfikowanych tooinclude funkcji testowych. 

Ten pokaz rozpocznie się o treści JSON programu Swagger, zostanie wklejona do edytora swagger.io hello, który zostanie następnie można toogenerate używany kod korzystający z tooaccess JAX-RS punkt końcowy interfejsu API REST. Następnie będzie edytowanie kodu hello szkieletu tooreturn danych testowych, co stanowi symulację interfejsu API REST stworzona mechanizmu stanu trwałego danych.  

1. Skopiuj następujące Schowka tooyour kodu JSON programu Swagger hello:
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. Przejdź toohello [edytora Online programu Swagger]. Wyświetlonym edytorze kliknij hello **Plik -> Wklej dane JSON** elementu menu.
   
    ![Element menu Paste JSON (Wklej dane JSON)][paste-json]
3. Wklej hello kontaktów listy interfejsu API JSON programu Swagger wcześniej zostały skopiowane. 
   
    ![Wklejanie kodu JSON do programu Swagger][pasted-swagger]
4. Wyświetl hello stron z dokumentacją oraz podsumowanie interfejsu API wyświetlone w edytorze hello. 
   
    ![Wyświetlanie dokumentów wygenerowanych przez program Swagger][view-swagger-generated-docs]
5. Wybierz hello **Generuj serwer -> JAX-RS** menu opcji tooscaffold powitania po stronie serwera kodu zostanie zmodyfikowany w późniejszym tooadd implementację testową. 
   
    ![Element menu umożliwiający generowanie kodu][generate-code-menu-item]
   
    Wygenerowany kod hello zostanie udostępniony toodownload pliku ZIP. Ten plik zawiera szkielet przez generator kodu programu Swagger hello kodu hello i wszystkie skojarzone skrypty kompilacji. Rozpakuj hello całej biblioteki tooa katalogu na deweloperskiej stacji roboczej. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Edytuj hello kodu tooadd implementacji interfejsu API
W tej sekcji implementacja po stronie serwera hello struktury Swagger generowane kodu będzie Zamień niestandardowy kod. Witaj nowy kod zwróci toohello jednostek ArrayList kontaktu dla klienta wywołującego. 

1. Otwórz hello *Contact.java* pliku modelu, który znajduje się w hello *src/gen/java/io/swagger/model* folderu, za pomocą [Visual Studio Code] lub w ulubionym edytorze tekstów. 
   
    ![Otwieranie pliku modelu kontaktów][open-contact-model-file]
2. Dodaj następującego konstruktora w hello hello **skontaktuj się z** klasy. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Otwórz hello *ContactsApiServiceImpl.java* plik implementacji usługi, który znajduje się w hello *src/main/java/io/swagger/interfejsu api/impl* folderu, za pomocą [Visual Studio Code]lub w ulubionym edytorze tekstów.
   
    ![Otwieranie pliku kodu usługi kontaktów][open-contact-service-code-file]
4. Zastąp kod hello w pliku hello tego nowego kodu tooadd kodu usługi toohello implementację testową. 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. Otwórz wiersz polecenia i zmień folder główny toohello katalogu aplikacji.
6. Wykonanie następującego kodu hello toobuild polecenie narzędzia Maven hello i uruchom lokalnie przy użyciu powitania serwera aplikacji Jetty. 
   
        mvn package jetty:run
7. Powinny pojawić się hello w oknie wiersza polecenia Jetty została uruchomiona kodu na porcie 8080. 
   
    ![Otwieranie pliku kodu usługi kontaktów][run-jetty-war]
8. Użyj [Postman] toomake interfejs API "pobrania wszystkich kontaktów" toohello żądania metody pod adresem http://localhost: 8080/api/contacts.
   
    ![Witaj wywołania interfejsu API kontaktów][calling-contacts-api]
9. Użyj [Postman] toomake interfejs API "pobrania określonego kontaktu" toohello żądania metody znajdujący się pod adresem http://localhost: 8080/api/contacts/2.
   
    ![Witaj wywołania interfejsu API kontaktów][calling-specific-contact-api]
10. Na koniec Utwórz plik WAR języka Java (archiwum sieci Web) hello, wykonując następujące polecenie narzędzia Maven w konsoli hello. 
    
         mvn package war:war
11. Po utworzeniu pliku WAR hello zostaną umieszczone w hello **docelowej** folderu. Przejdź do hello **docelowej** folder i Zmień nazwę hello pliku WAR zbyt**ROOT.war**. (Upewnij się, że hello liter jest istotna).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Następnie uruchom następujące polecenia z folderu głównego hello toocreate Twojej aplikacji hello **wdrażanie** folderu toouse toodeploy hello WAR pliku tooAzure. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Publikowanie hello dane wyjściowe tooAzure usługi aplikacji
W tej sekcji dowiesz się, jak toocreate nowej aplikacji interfejsu API przy użyciu hello portalu Azure, przygotować ją do hostowania aplikacji języka Java i wdrażanie hello nowo utworzony plik WAR pliku tooAzure toorun usługi aplikacji w nowej aplikacji interfejsu API. 

1. Utwórz nową aplikację interfejsu API w hello [portalu Azure], klikając hello **nowy -> sieci Web i mobilność -> Aplikacja interfejsu API** element menu, wprowadzając informacje dotyczące aplikacji, a następnie klikając **Utwórz**.
   
    ![Tworzenie nowej aplikacji interfejsu API][create-api-app]
2. Po utworzeniu aplikacji interfejsu API, otwórz aplikacji **ustawienia** bloku, a następnie kliknij przycisk hello **ustawienia aplikacji** elementu menu. Wybierz hello najnowsze wersje oprogramowania Java z hello dostępne opcje, a następnie wybierz hello najnowszą wersję serwera Tomcat z hello **kontener sieci Web** menu, a następnie kliknij przycisk **zapisać**.
   
    ![Konfigurowanie oprogramowania Java w hello bloku aplikacji interfejsu API][set-up-java]
3. Kliknij przycisk hello **poświadczenia wdrażania** menu Ustawienia i podaj nazwę użytkownika i hasło mają toouse publikowania plików tooyour aplikacji interfejsu API. 
   
    ![Konfigurowanie poświadczeń wdrożenia][deployment-credentials]
4. Kliknij przycisk hello **źródło wdrożenia** element menu Ustawienia. Wyświetlonym edytorze kliknij hello **wybierz źródło** przycisku, wybierz hello **lokalnego repozytorium Git** , a następnie kliknij przycisk **OK**. Spowoduje to utworzenie repozytorium Git działającego na platformie Azure, które jest skojarzone z aplikacją interfejsu API. Każdy razem, gdy zatwierdzisz kod toohello *wzorca* gałęzi repozytorium Git kodu zostaną opublikowane na żywo uruchomione wystąpienie aplikacji interfejsu API. 
   
    ![Konfigurowanie nowego lokalnego repozytorium Git][select-git-repo]
5. Skopiuj Schowka tooyour adres URL hello nowego repozytorium Git. Zapisz ten adres, ponieważ będzie on potrzebny później. 
   
    ![Konfigurowanie nowego repozytorium Git dla aplikacji][copy-git-repo-url]
6. Wypychania hello WAR pliku toohello online repozytorium Git. toodo, przejdź do hello **wdrażanie** folderu utworzonego wcześniej, aby móc łatwo zatwierdzić kod hello zapasowej repozytorium toohello uruchomionych w usłudze App Service. Po pracy w oknie konsoli hello i przejście do hello folder zawierający hello webapps folder, wystawiać powitania po procesie hello toolaunch polecenia Git i szybko włączyć wdrożenie. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Po wysłaniu hello **wypychania** żądania, zostanie wyświetlony monit o hasło hello wcześniej utworzony dla poświadczenia wdrożenia hello. Po wprowadzeniu poświadczeń powinien pojawić się na ekranie portalu, który hello aktualizacji została wdrożona.
7. Jeśli ponownie użyjesz Postman toohit hello nowo wdrożonej aplikacji interfejsu API uruchomionej w usłudze Azure App Service, zobaczysz, że zachowanie hello jest spójne, a aplikacja zwraca dane kontaktowe zgodnie z oczekiwaniami, a za pomocą prostego kodu zmiany toohello Swagger.io szkieletu kodu języka Java. 
   
    ![Używanie interfejsu API REST kontaktów języka Java uruchomionego na platformie Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Następne kroki
W tym artykule było możliwe toostart z plikiem JSON programu Swagger i uzyskane z edytora Swagger.io hello szkieletu kodu języka Java. W efekcie wprowadzenia prostych zmian i zastosowania procesu wdrażania narzędzia Git utworzono funkcjonalną aplikację interfejsu API napisaną w języku Java. Witaj następny samouczek pokazuje, jak za[z klientów języka JavaScript przy użyciu mechanizmu CORS aplikacji interfejsu API][App Service API CORS]. W kolejnych samouczkach z hello Pokaż serii jak tooimplement uwierzytelniania i autoryzacji.

toobuild w tym przykładzie, użytkownik może dowiedzieć się więcej o hello [Storage SDK for Java] obiekty BLOB JSON hello toopersist. Można użyć hello [Document DB Java SDK] toosave Twojego skontaktuj się z danych tooAzure w bazie danych dokumentów. 

<a name="see-also"></a>

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portalu Azure]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[bezpłatnej wersji próbnej]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer's Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[JAX-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[edytora Online programu Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK for Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[edytora programu Swagger]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
