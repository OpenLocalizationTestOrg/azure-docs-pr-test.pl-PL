---
title: "jak toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania aaaLearn | Dokumentacja firmy Microsoft"
description: "Przewodnik pokazujący sposób toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania."
keywords: "uczenia maszynowego, zarządzanie interfejsami api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Dowiedz się, jak toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania
## <a name="overview"></a>Omówienie
W tym przewodniku przedstawiono sposób tooquickly rozpoczęcie pracy z toomanage zarządzanie interfejsami API usług sieci web uczenie maszynowe Azure.

## <a name="what-is-azure-api-management"></a>Co to jest usługa Azure API Management?
Zarządzanie interfejsami API Azure jest usługą platformy Azure, która umożliwia zarządzanie punktami końcowymi interfejsu API REST, definiując dostępu użytkownika, ograniczenie i pulpit nawigacyjny monitorowania. Kliknij przycisk [tutaj](https://azure.microsoft.com/services/api-management/) szczegółowe informacje na temat usługi Azure API Management. Kliknij przycisk [tutaj](../api-management/api-management-get-started.md) przewodnik, w jaki sposób tooget wprowadzenie do usługi Azure API Management. Inne w tym przewodniku, na podstawie tego przewodnika, dotyczą więcej tematy, w tym konfiguracji powiadomień, warstwy cenowej, Obsługa odpowiedzi, uwierzytelnianie użytkowników, tworzenie produktów, subskrypcji dewelopera i dashboarding użycia.

## <a name="what-is-azureml"></a>Co to jest uczenie maszynowe Azure?
Uczenie maszynowe Azure jest usługą platformy Azure do uczenia maszynowego, umożliwiający tooeasily kompilacji, wdrażanie i Udostępnianie zaawansowane metody analizy rozwiązania. Kliknij przycisk [tutaj](https://azure.microsoft.com/services/machine-learning/) szczegółowe informacje na temat uczenie maszynowe Azure.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego przewodnika należy:

* Konto platformy Azure. Jeśli nie masz konta platformy Azure, kliknij przycisk [tutaj](https://azure.microsoft.com/pricing/free-trial/) szczegółowe informacje na temat toocreate bezpłatne konto próbne.
* Konto uczenie maszynowe Azure. Jeśli nie masz konta uczenie maszynowe Azure, kliknij przycisk [tutaj](https://studio.azureml.net/) szczegółowe informacje na temat toocreate bezpłatne konto próbne.
* obszar roboczy Hello, usługi i api_key do eksperymentu uczenie maszynowe Azure wdrożyć jako usługę sieci web. Kliknij przycisk [tutaj](machine-learning-create-experiment.md) szczegółowe informacje na temat sposobu eksperymentu toocreate uczenie maszynowe Azure. Kliknij przycisk [tutaj](machine-learning-publish-a-machine-learning-web-service.md) szczegółowe informacje na temat sposobu toodeploy uczenie maszynowe Azure eksperymentu jako usługę sieci web. Alternatywnie dodatek a. zawiera instrukcje dotyczące sposobu toocreate i testowania proste uczenie maszynowe Azure eksperymentu i go wdrożyć jako usługę sieci web.

## <a name="create-an-api-management-instance"></a>Tworzenie wystąpienia usługi API Management
Poniżej przedstawiono kroki hello przy użyciu interfejsu API zarządzania toomanage usługi sieci web uczenie maszynowe Azure. Najpierw utwórz wystąpienie usługi. Zaloguj się za toohello [klasyczny Portal](https://manage.windowsazure.com/) i kliknij przycisk **nowy** > **usługi aplikacji** > **zarządzanie interfejsami API**  >  **Utworzyć**.

![Tworzenie wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Określ unikatową **adres URL**. Ten przewodnik po używa **demoazureml** — należy toochoose coś innego. Wybierz żądaną hello **subskrypcji** i **Region** wystąpienia usługi. Po wprowadzeniu wybrane opcje, kliknij przycisk Dalej hello.

![Utwórz usług-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Określ wartość hello **nazwa organizacji**. Ten przewodnik po używa **demoazureml** — należy toochoose coś innego. Wprowadź adres e-mail w hello **e-mail administratora** pola. Ten adres e-mail jest używany dla powiadomień z hello system zarządzania interfejsu API.

![Utwórz usług-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Kliknij przycisk toocreate pole wyboru hello wystąpienia usługi. *Zajmowała toothirty minut nowe toobe usługi utworzone*.

## <a name="create-hello-api"></a>Utwórz interfejs API hello
Po utworzeniu wystąpienia usługi hello hello następnym krokiem jest toocreate hello API. Interfejs API składa się z zestawu operacji, które mogą być wywoływane z poziomu aplikacji klienckiej. Operacje interfejsu API są tooexisting serwerem proxy usługi sieci web. W tym przewodniku tworzy interfejsów API toohello tego serwera proxy, istniejące rekordy zasobów uczenie maszynowe Azure i usługi BES usług sieci web.

Interfejsy API są tworzone i skonfigurowana z hello interfejsu API wydawcy portalu, który jest dostępny za pośrednictwem hello klasycznego portalu Azure. tooreach hello wydawcy portalu, wybierz wystąpienia usługi.

![Wybierz usługę wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Kliknij przycisk **Zarządzaj** w hello portalu klasycznego Azure dla usługi interfejsu API zarządzania.

![Usługa zarządzania](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać interfejsu API**.

![Interfejs API zarządzania menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Typ **API pokaz uczenie maszynowe Azure** jako hello **Nazwa interfejsu API sieci Web**. Typ **https://ussouthcentral.services.azureml.net** jako hello **adres URL usługi sieci Web**. Typ **pokaz uczenie maszynowe Azure** jako hello **sufiks adresu URL interfejsu API sieci Web**. Sprawdź **HTTPS** jako hello **adres URL interfejsu API sieci Web** schematu. Wybierz **Starter** jako **produkty**. Gdy skończysz, kliknij przycisk **zapisać** hello toocreate interfejsu API.

![Dodaj — nowy — interfejs api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Dodaj hello operacji
Kliknij przycisk **operacji dodawania** tooadd toothis operacje interfejsu API.

![Dodaj operację](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Witaj **nowej operacji** oknie będą wyświetlane i hello **podpisu** będzie domyślnie wybierany kartę.

## <a name="add-rrs-operation"></a>Dodaj operację rekordy zasobów
Najpierw utwórz operację na powitania usługi uczenie maszynowe Azure rekordy zasobów. Wybierz **POST** jako hello **zlecenie HTTP**. Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / execute? api-version = {apiversion} & szczegóły = {szczegóły}** jako hello **szablon adresu URL**. Typ **wykonania rekordy zasobów** jako hello **Nazwa wyświetlana**.

![Dodawanie rekordów zasobów operacji podpisu](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**. Kliknij przycisk **zapisać** toosave tej operacji.

![Dodawanie rekordów zasobów operacji odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Dodaj BES operacji
Zrzuty ekranu nie są włączone dla hello operacji usługi BES są one bardzo podobne toothose hello RR operacji dodawania.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Przesyłanie (ale nie start) zadanie wsadowe
Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API. Wybierz **POST** dla hello **zlecenie HTTP**. Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / zadania? api-version = {apiversion}** dla hello **szablon adresu URL**. Typ **przesłać BES** dla hello **Nazwa wyświetlana**. Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**. Kliknij przycisk **zapisać** toosave tej operacji.

### <a name="start-a-batch-execution-job"></a>Uruchom zadanie wsadowe
Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API. Wybierz **POST** dla hello **zlecenie HTTP**. Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid} / start? api-version = {apiversion}** dla hello **szablon adresu URL**. Typ **BES Start** dla hello **Nazwa wyświetlana**. Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**. Kliknij przycisk **zapisać** toosave tej operacji.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Pobierz stan hello lub wyniku zadania wsadowe
Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API. Wybierz **UZYSKAĆ** dla hello **zlecenie HTTP**. Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla hello **szablon adresu URL**. Typ **stanu usługi BES** dla hello **Nazwa wyświetlana**. Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**. Kliknij przycisk **zapisać** toosave tej operacji.

### <a name="delete-a-batch-execution-job"></a>Usuń zadanie wsadowe
Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API. Wybierz **usunąć** dla hello **zlecenie HTTP**. Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla hello **szablon adresu URL**. Typ **usunąć BES** dla hello **Nazwa wyświetlana**. Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**. Kliknij przycisk **zapisać** toosave tej operacji.

## <a name="call-an-operation-from-hello-developer-portal"></a>Wywołaj operację z hello portalu dla deweloperów
Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello, która zapewnia tooview wygodny sposób i przetestować hello operacje interfejsu API. W tym kroku przewodnik będzie wywoływać hello **wykonania rekordy zasobów** metody, która została dodana toohello **API pokaz uczenie maszynowe Azure**. Kliknij przycisk **portalu dla deweloperów** menu hello w hello górnego prawego hello klasycznego portalu.

![portalu dla deweloperów](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **API pokaz uczenie maszynowe Azure** toosee hello operacje dostępne.

![Interfejs api demoazureml](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Wybierz **wykonania rekordy zasobów** hello operacji. Kliknij przycisk **wypróbuj**.

![try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Żądanie parametru, wpisz sieci **obszaru roboczego**, **usługi**, **2.0** dla hello **apiversion**, i **true**dla hello **szczegóły**. Można znaleźć sieci **obszaru roboczego** i **usługi** w pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure systemu hello (zobacz **testowanie usługi sieci web hello** w dodatku A).

Dla nagłówków żądań, kliknij przycisk **Dodaj nagłówek** i typ **Content-Type** i **application/json**, następnie kliknij przycisk **Dodaj nagłówek** i typ **autoryzacji** i **elementu nośnego <YOUR AZUREML SERVICE API-KEY>** . Można znaleźć sieci **klucz interfejsu api** w pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure systemu hello (zobacz **testowanie usługi sieci web hello** w dodatku A).

Typ **{"Dane wejściowe": {"input1": {"ColumnNames": ["Col2"] "wartości": [["jest to dobry dzień"]]}}, "GlobalParameters": {}}** hello treści żądania.

![uczenie maszynowe Azure pokaz api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Kliknij przycisk **wysyłania**.

![Wyślij](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Po wywołaniu operacji portalu dla deweloperów hello Wyświetla hello **żądany adres URL** z hello usługi zaplecza, hello **stanu odpowiedzi**, hello **nagłówki odpowiedzi**, natomiast dla ustawienia **zawartości odpowiedzi**.

![Stan odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Dodatek A — tworzenie i testowanie prostego uczenie maszynowe Azure usługi sieci web
### <a name="creating-hello-experiment"></a>Tworzenie eksperymentu hello
Poniżej przedstawiono kroki hello Tworzenie prostego eksperymentu uczenie maszynowe Azure i wdrażania go w postaci usługi sieci web. Witaj przyjmuje usługi sieci web jako danych wejściowych z kolumną zawierającą dowolnego tekstu i zwraca zestaw funkcji reprezentowane jako wartości całkowite. Na przykład:

| Tekst | Tekst w formie skrótu |
| --- | --- |
| Jest to dobry dzień |1 1 2 2 0 2 0 1 |

Po pierwsze, za pomocą przeglądarki wybranych przez użytkownika, przejdź do: [https://studio.azureml.net/](https://studio.azureml.net/) , a następnie wprowadź toolog Twoje poświadczenia w. Następnie należy utworzyć nowy eksperyment puste.

![Wyszukiwanie — eksperymentu — szablony](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Zmień nazwę zbyt**SimpleFeatureHashingExperiment**. Rozwiń węzeł **zapisane zestawów danych** i przeciągnij **przeglądami książki z Amazon** na eksperymentu.

![prosty — funkcja mieszania eksperymentu](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Rozwiń węzeł **transformacji danych** i **manipulowania** i przeciągnij **Select Columns in Dataset** na eksperymentu. Połącz **przeglądami książki z Amazon** za**Select Columns in Dataset**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Kliknij przycisk **Select Columns in Dataset** , a następnie kliknij przycisk **Uruchom selektor kolumn** i wybierz **Col2**. Kliknij przycisk tooapply znacznikiem wyboru hello tych zmian.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Rozwiń węzeł **Analiza tekstu** i przeciągnij **Tworzenie skrótu funkcji** na powitania eksperymentu. Połącz **Select Columns in Dataset** za**Tworzenie skrótu funkcji**.

![Connect--kolumny projektu](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Typ **3** dla hello **mieszania bitsize**. Spowoduje to utworzenie 8 (23) kolumny.

![Tworzenie skrótów bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

W tym momencie możesz tooclick **Uruchom** tootest hello eksperymentu.

![Uruchom](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Tworzenie usługi sieci Web
Teraz Utwórz usługę sieci web. Rozwiń węzeł **usługi sieci Web** i przeciągnij **dane wejściowe** na eksperymentu. Połącz **dane wejściowe** za**Tworzenie skrótu funkcji**. Przeciągnij również **dane wyjściowe** na eksperymentu. Połącz **dane wyjściowe** za**Tworzenie skrótu funkcji**.

![dane wyjściowe do-— Tworzenie skrótu funkcji](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Kliknij przycisk **opublikować usługi sieci web**.

![Publikowanie — Usługa sieci web](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Kliknij przycisk **tak** toopublish hello eksperymentu.

![tak aby opublikować](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Usługa sieci web hello testu
Usługi sieci web uczenie maszynowe Azure składa się z punktów końcowych (usługi wykonywania wsadowego) BES i RSS (żądania/odpowiedzi usługi). Funkcja RSS jest synchroniczne wykonywania. BES jest do wykonywania zadań asynchronicznych. usługi sieci web ze źródłem Python próbki hello poniżej tootest, konieczne może toodownload i hello Zainstaluj zestaw Azure SDK dla języka Python (zobacz: [jak tooinstall Python](../python-how-to-install.md)).

Należy również hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu źródła próbki hello poniżej. Hello obszaru roboczego i usługi można znaleźć, klikając opcję **żądanie/odpowiedź** lub **Batch Execution** swojego eksperymentu w pulpicie nawigacyjnym usługi sieci web hello.

![Znajdź obszar roboczy i usługi](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Można znaleźć hello **api_key** , klikając na pulpicie nawigacyjnym usługi sieci web hello eksperymentu.

![Znajdź api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Punkt końcowy RR testu
##### <a name="test-button"></a>Przycisk Testuj
Punkt końcowy łatwy sposób tootest hello rekordy zasobów jest tooclick **testu** na pulpicie nawigacyjnym usługi sieci web hello.

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Typ **to dobry dzień** dla **col2**. Kliknij znacznik wyboru hello.

![Wprowadź dane](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Zobaczysz ekran podobny do

![Przykładowe wyniki](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Przykładowy kod
Inny sposób tootest Twojego rekordy zasobów jest z kodu klienta. Jeśli klikniesz przycisk **żądania/odpowiedzi** na hello pulpitu nawigacyjnego i przewiń w dół toohello, zostanie wyświetlone przykładowego kodu dla C#, Python i R. Widoczne będzie także składni hello żądania RR hello, włącznie z identyfikatora URI żądania hello, nagłówki i treść.

Ten przewodnik zawiera pracy przykład Python. Konieczne będzie toomodify go przy użyciu hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Punkt końcowy usługi BES testu
Kliknij przycisk **wykonywanie wsadowe** na dole toohello hello pulpitu nawigacyjnego i przewijania. Zostanie wyświetlone przykładowego kodu dla C#, Python i R. Widoczne będzie także hello składnia hello BES żądań toosubmit zadania, uruchomić zadanie, Pobierz stan hello lub wyniki zadania i usuwanie zadania.

Ten przewodnik zawiera pracy przykład Python. Należy toomodify za pomocą hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu. Ponadto należy toomodify hello **nazwy konta magazynu**, **klucz konta magazynu**, i **nazwa kontenera magazynu**. Ponadto należy toomodify lokalizację hello hello **pliku wejściowego** i lokalizację hello hello **pliku wyjściowego**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
