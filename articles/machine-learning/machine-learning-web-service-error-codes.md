---
title: "kody błędów aaaAzure Machine Learning REST API | Dokumentacja firmy Microsoft"
description: "Te kody błędów mogą być zwracane przez operację usługi sieci web uczenie maszynowe Azure."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Kody błędów interfejsu API REST uczenia maszynowego
 
Witaj następujące kody błędów mogą być zwracane przez operację usługi sieci web uczenie maszynowe Azure.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (kod stanu HTTP 400)
 
Podano nieprawidłowy argument.
 
Ta klasa błędy oznacza, że udostępniane innym argument był nieprawidłowy. Może to być poświadczeń lub lokalizacji magazynu Azure toosomething przekazany toohello usługi sieci web. Zapoznaj się pole "błąd" hello w sekcji toodiagnose "szczegóły" hello, które określonych argument był nieprawidłowy.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| BadParameterValue | Podana wartość parametru Hello nie spełnia hello reguły parametru dla parametru hello |
| BadSubscriptionId | Subskrypcja Hello identyfikator, który jest używany tooscore nie jest hello jedną obecne w zasobie hello |
| BadVersionCall | Przekazano nieprawidłową wersję parametr podczas wywołania interfejsu API hello: {0}. Sprawdź hello pomocy strony może być przekazywany hello poprawną wersję interfejsu API i spróbuj ponownie. |
| BatchJobInputsNotSpecified | nie określono Hello następujące wymagane input(s) z żądaniem hello: {0}. Upewnij się, że wszystkie dane wejściowe jest określona, a następnie spróbuj ponownie. |
| BatchJobInputsTooManySpecified | Żądanie hello określony wejść więcej niż zdefiniowana w usłudze hello. Lista input(s) zaakceptowane: {0}. Upewnij się, że wszystkie dane wejściowe został podany poprawnie, a następnie spróbuj ponownie. |
| BlobNameTooLong | Ścieżki do magazynu obiektów blob platformy Azure podana diagnostycznych danych wyjściowych jest za długa: {0}. Skróć ścieżkę hello i spróbuj ponownie. |
| BlobNotFound | Witaj tooaccess nie można podać obiektów blob platformy Azure — {0}.  Komunikat o błędzie platformy Azure: {1}. |
| ContainerIsEmpty | Podano bez nazwy kontenera magazynu systemu Azure. Podaj nazwę kontenera prawidłowe i spróbuj ponownie. |
| ContainerSegmentInvalid | Nazwa nieprawidłowym kontenerem. Podaj nazwę kontenera prawidłowe i spróbuj ponownie. |
| ContainerValidationFailed | Obiekt blob kontenera nie można sprawdzić poprawności z powodu następującego błędu: {0}. |
| DataTypeNotSupported | Nieobsługiwany typ danych pod warunkiem. Podaj prawidłowe dane typów i spróbuj ponownie. |
| DuplicateInputInBatchCall | żądanie wsadowe Hello jest nieprawidłowy. Nie można określić w jednym i wieloma woluminami danych wejściowych na powitania sam czas. Usuń jeden z tych elementów z hello żądania i spróbuj ponownie. |
| ExpiryTimeInThePast | Podany czas wygaśnięcia jest w przeszłości hello: {0}. Podaj czas wygaśnięcia w przyszłości, w formacie UTC, a następnie spróbuj ponownie. toonever wygaśnie, ustaw tooNULL czasu wygaśnięcia. |
| IncompleteSettings | Ustawienia diagnostyczne są niekompletne. |
| InputBlobRelativeLocationInvalid | Nie podano nazwy obiektu blob magazynu Azure. Podaj nazwę nieprawidłowy obiekt blob, a następnie spróbuj ponownie. |
| InvalidBlob | Nieprawidłowy obiekt blob specyfikacji dla obiekt blob: {0}. Sprawdź tego ciągu połączenia / ścieżkę względną lub specyfikacji tokenu sygnatury dostępu Współdzielonego jest poprawna i spróbuj ponownie. |
| InvalidBlobConnectionString | Witaj określonym dla jednego z obiektów blob wejścia/wyjścia hello nieprawidłowe parametry połączenia: {0}. Rozwiązać ten problem i spróbuj ponownie. |
| InvalidBlobExtension | Witaj odwołanie obiektu blob: {0} ma nieprawidłowe lub brakujące rozszerzenie. Obsługiwane rozszerzenia plików dla tego typu danych wyjściowych to: "{1}". |
| InvalidInputNames | Usługi danych wejściowych nazwy określony w żądaniu hello: {0}. Mapowanie hello danych wejściowych toohello prawidłowe usługi wejść i spróbuj ponownie. |
| InvalidOutputOverrideName | Nieprawidłowe dane wyjściowe zastąpić nazwę: {0}. Usługa Hello nie ma danych wyjściowych węzła o tej nazwie. Przekaż toooverride nazwa węzła poprawne dane wyjściowe (dotyczy rozróżniania wielkości liter). |
| InvalidQueryParameter | Nieprawidłowy parametr zapytania "{0}". {1} |
| MissingInputBlobInformation | Brak informacji o obiektu blob magazynu Azure. Podaj prawidłowe parametry połączenia i ścieżkę względną lub identyfikator URI, a następnie spróbuj ponownie. |
| MissingJobId | Brak podany identyfikator zadania. Zadanie identyfikator jest zwracany, gdy zadanie zostało przesłane do powitania po raz pierwszy. Sprawdź zadanie hello identyfikator jest poprawny i spróbuj ponownie. |
| MissingKeys | Brak kluczy dostarczona lub nie podano podstawowego lub dodatkowego klucza. |
| MissingModelPackage | Nie identyfikator pakietu modelu lub podać pakietu modelu. Podaj identyfikator pakietu prawidłowego modelu lub modelu pakietu i spróbuj ponownie. |
| MissingOutputOverrideSpecification | Żądanie hello Brak specyfikacji obiektu blob powitania dla danych wyjściowych zastąpienia {0}. Określ lokalizację nieprawidłowy obiekt blob z żądaniem hello lub usuń specyfikację wyjściową hello, jeśli żadne przesłonięcie lokalizacji. |
| MissingRequestInput | Usługa sieci web Hello oczekuje danych wejściowych, ale nie dane wejściowe nie został podany. Upewnij się, prawidłowe wartości wejściowe są udostępniane na powitania publikowanych danych wejściowych portów w modelu hello i spróbuj ponownie. |
| MissingRequiredGlobalParameters | Nie wszystkie wymagane podane parametry usługi sieci web. Sprawdź parametry hello oczekiwanego przez hello moduły są prawidłowe i spróbuj ponownie. |
| MissingRequiredOutputOverrides | Podczas wywoływania metody punktu końcowego usługi zaszyfrowane, jest obowiązkowy toopass w danych wyjściowych powoduje zastąpienie hello usługi wszystkie dane wyjściowe. Brak zastąpienia w tej chwili uzyskać te dane wyjściowe: {0} |
| MissingWebServiceGroupId | Podany identyfikator nie grupy usługi sieci web. Podaj identyfikator grupy usługi sieci web prawidłowe i spróbuj ponownie. |
| MissingWebServiceId | Podany identyfikator nie usługi sieci web. Usługi sieci web prawidłowy identyfikator i spróbuj ponownie. |
| MissingWebServicePackage | Nie podano pakiet usługi sieci web. Podaj pakiet usługi sieci web prawidłowe i spróbuj ponownie. |
| MissingWorkspaceId | Podany identyfikator nie obszaru roboczego. Podaj prawidłowy identyfikator obszaru roboczego, a następnie spróbuj ponownie. |
| ModelConfigurationInvalid | Nieprawidłowy model konfiguracji w pakiecie modelu hello. Upewnij się, Konfiguracja modelu hello zawiera definicję punktów końcowych danych wyjściowych, standardowy punkt końcowy błędu, i std punktu końcowego i spróbuj ponownie. |
| ModelPackageIdInvalid | Nieprawidłowy model pakietu identyfikatora. Sprawdź, czy ten identyfikator pakietu modelu hello jest poprawny i spróbuj ponownie. |
| RequestBodyInvalid | Nie podano treści żądania lub wystąpił błąd podczas deserializacji treści żądania hello. |
| RequestIsEmpty | Nie podano żądania. Podaj prawidłowy żądania i spróbuj ponownie. |
| UnexpectedParameter | Podane parametry nieoczekiwany. Sprawdź wszystkie nazwy parametrów są poprawne, tylko oczekiwane parametry są przekazywane, a następnie spróbuj ponownie. |
| Nieznany | Wystąpił nieznany błąd. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Nie można zmienić wymagania równoczesnych żądań dla usługi sieci web {0}. |
| WebServiceIdInvalid | Podany identyfikator usługi sieci web nieprawidłowy. Identyfikator usługi sieci Web powinna być prawidłowym identyfikatorem guid. |
| WebServiceTooManyConcurrentRequestRequirement | Nie można ustawić równoczesnych żądań wymaganie toomore niż {0}. |
| WebServiceTypeInvalid | Nieprawidłowy typ sieci web usługi udostępniane. Sprawdź, czy typ usługi sieci web prawidłowy hello jest prawidłowa i spróbuj ponownie. Nieprawidłowe typy usług: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (kod stanu HTTP 400)
 
Podany argument nieprawidłowego użytkownika.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| InputMismatchError | Dane wejściowe jest niezgodna z portu wejściowego schematu. |
| InputParseError | Analizowanie wektor wejściowy nie powiodło się.  Sprawdź, czy hello wektor wejściowy ma hello poprawnej liczby kolumn i typy danych.  Dodatkowe szczegóły: {0}. |
| MissingRequiredGlobalParameters | Brak oczekiwanej przez usługę sieci web hello parametrów. Sprawdź, czy wszystkie parametry hello wymagane oczekiwane przez usługę sieci web hello są poprawne i spróbuj ponownie. |
| UnexpectedParameter | Sprawdź, czy tylko hello wymagane parametry oczekiwane przez usługę sieci web hello są przekazywane, a następnie spróbuj ponownie. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (kod stanu HTTP 400)
 
Żądanie hello jest nieprawidłowy w bieżącym kontekście hello.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| CannotStartJob | Nie można uruchomić zadania Hello, ponieważ jest w stanie {0}. |
| IncompatibleModel | Hello model jest niezgodna z wersją żądania hello. Wersja żądania Hello obsługuje tylko modele danych wyjściowych jednego elementu datatable. |
| MultipleInputsNotAllowed | Hello model nie zezwala na wielu danych wejściowych. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (kod stanu HTTP 400)
 
Podczas wykonywania modułu Napotkano błąd wewnętrzny biblioteki.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (kod stanu HTTP 400)
 
Operacja uruchamiania modułu wystąpił błąd.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (kod stanu HTTP 400)
 
Pakiet usługi sieci web nieprawidłowy. Sprawdź poprawność pakiet usługi sieci web hello pod warunkiem i spróbuj ponownie.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| FormatError | pakiet usługi sieci web Hello jest nieprawidłowo sformułowany. Szczegóły: {0} |
| RuntimesError | Wykres pakietu usługi sieci web Hello jest nieprawidłowy. Szczegóły: {0} |
| ValidationError | Wykres pakietu usługi sieci web Hello jest nieprawidłowy. Szczegóły: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Nieautoryzowane (kod stanu HTTP 401)
 
Żądanie jest nieautoryzowanego tooaccess zasobów.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| AdminRequestUnauthorized | Brak autoryzacji |
| ManagementRequestUnauthorized | Brak autoryzacji |
| ScoreRequestUnauthorized | Podano nieprawidłowe poświadczenia. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (kod stanu HTTP 404)
 
Nie znaleziono zasobu.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| ModelPackageNotFound | Nie znaleziono pakietu modelu. Sprawdź pakietu modelu hello identyfikator jest poprawny i spróbuj ponownie. |
| WebServiceIdNotFoundInWorkspace | Usługi sieci Web w ramach tego obszaru roboczego nie można odnaleźć. Wystąpiła niezgodność między hello webServiceId i hello workspaceId. Sprawdź podane usługi sieci web hello jest częścią obszaru roboczego hello i spróbuj ponownie. |
| WebServiceNotFound | Nie można odnaleźć usługi sieci Web. Sprawdź usługę sieci web hello identyfikator jest poprawny i spróbuj ponownie. |
| WorkspaceNotFound | Nie można odnaleźć obszaru roboczego. Sprawdź roboczym hello identyfikator jest poprawny i spróbuj ponownie. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (kod stanu HTTP 408)
 
Nie można ukończyć operacji Hello w ramach dozwolone czasu hello.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| RequestCanceled | Żądanie zostało anulowane przez powitania klienta. |
| ScoreRequestTimeout | Upłynął limit czasu żądania wykonania. |
 
## <a name="conflict-http-status-code-409"></a>Konflikt (kod stanu HTTP 409)
 
Zasób już istnieje.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Nazwa parametru nieprawidłowe dane wyjściowe. Spróbuj użyć hello metadanych Edytor modułu toorename kolumn i spróbuj ponownie. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (kod stanu HTTP 413)
 
Hello model przekroczył przydziału pamięci hello przypisane tooit.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| OutOfMemoryLimit | Hello model używane więcej pamięci niż była przeznaczona dla niego. Maksymalna dozwolona ilość pamięci dla modelu hello jest {0} MB. Sprawdź, czy model problemów. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (kod stanu HTTP 500)
 
Wykonanie napotkał błąd wewnętrzny.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | awaria Hello kontenera procesu z powodu błędu systemu |
| ContainerProcessTerminatedWithUnknownError | awaria Hello kontenera procesu z powodu nieznanego błędu |
| ContainerValidationFailed | Obiekt blob kontenera nie można sprawdzić poprawności z powodu następującego błędu: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Nie podano żadnych argumentów. Sprawdź, czy prawidłowe argumenty zostały przesłane i spróbuj ponownie. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Identyfikator portów = {0} ma nieobsługiwany typ danych: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Generowanie swagger nie powiodło się, szczegóły: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| Nieznany |  |
| UnknownJobStatusCode | Kod stanu zadania nieznany {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, szczegóły: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (kod stanu HTTP 500)
 
Wykonanie napotkał błąd wewnętrzny. Mało pamięci systemu. Spróbuj ponownie.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (kod stanu HTTP 500)
 
Nieprawidłowy model pakietu. Sprawdź podane pakietu modelu hello jest poprawna i spróbuj ponownie.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (kod stanu HTTP 500)
 
Pakiet usługi sieci web nieprawidłowy. Sprawdź podany pakiet sieci web hello jest poprawna i spróbuj ponownie.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| ModuleError | Wykres pakietu usługi sieci web Hello jest nieprawidłowy. Szczegóły: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (kod stanu HTTP 503)
 
Witaj żądania nie można wykonać jako powitalne kontenery jest inicjowany.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (kod stanu HTTP 503)
 
Usługa jest tymczasowo niedostępna.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| NoMoreResources | Brak dostępnych zasobów do żądania. |
| RequestThrottled | Żądanie zostało ograniczenie dla punktu końcowego {0}. Hello maksymalną współbieżności dla punktu końcowego hello jest {1}. |
| TooManyConcurrentRequests | Za dużo współbieżnych żądań wysyłane. |
| TooManyHostsBeingInitialized | Zbyt wiele hostów został zainicjowany w hello sam czas. Należy rozważyć ograniczenie / ponawianie próby. |
| TooManyHostsBeingInitializedPerModel | Zbyt wiele hostów został zainicjowany w hello sam czas. Należy rozważyć ograniczenie / ponawianie próby. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (kod stanu HTTP 504)
 
Nie można ukończyć operacji Hello w ramach dozwolone czasu hello.
 
| Kod błędu: | Komunikat użytkownika |
| ---------- |--------------|
| BackendInitializationTimeout | Nie można ukończyć inicjowania usługi sieci web Hello w ramach dozwolone czasu hello. |
| BackendScoreTimeout | Nie można ukończyć wykonywania żądania usługi sieci web Hello w ramach dozwolone czasu hello. |
 
