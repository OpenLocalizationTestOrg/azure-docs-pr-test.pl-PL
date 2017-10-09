---
title: "usługi sieci web klasycznego aaaRetrain | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprogrammatically retrain modelu i aktualizacji hello web toouse hello nowo uczonego modelu usług w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Ponowne szkolenie klasycznej usługi internetowej
Hello wdrożono predykcyjnej usługi sieci Web jest domyślnym hello punktu końcowego oceniania. Domyślne punkty końcowe są synchronizowana z hello oryginalnego celów szkoleniowych i oceniania eksperymentów, a w związku z tym hello uczonego modelu do hello domyślny punkt końcowy nie można zastąpić. Usługa sieci web hello tooretrain, należy dodać nową usługę sieci web toohello punktu końcowego. 

## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć skonfigurowaniu eksperyment uczenia i eksperyment predykcyjny jak pokazano w [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> eksperyment predykcyjny Hello należy wdrożyć jako usługę sieci web uczenia maszynowego klasycznego. 
> 
> 

Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Dodaj nowy punkt końcowy
Witaj predykcyjnej usługi sieci Web, która została wdrożona zawiera domyślne oceniania punktu końcowego, który jest synchronizowana z hello oryginalnego szkolenia i oceniania eksperymenty trenowanego modelu. tooupdate Twojego toowith nowy nauczony model usługi sieci web należy utworzyć nowy punkt końcowy oceniania. 

toocreate nowy oceniania punkt końcowy, na powitania predykcyjnej usługi sieci Web, który może zostać zaktualizowana przy użyciu hello uczonego modelu:

> [!NOTE]
> Upewnij się, że w przypadku dodawania hello toohello punkt końcowy usługi sieci Web predykcyjnych, hello usługi sieci Web szkolenia. Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwie usługi WWW, na liście. Hello predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".
> 
> 

Istnieją trzy sposoby, w których można dodać nową usługę sieci web tooa punktu końcowego:

1. Programistycznie
2. Za pomocą portalu usługi sieci Web platformy Microsoft Azure hello
3. Witaj Użyj klasycznego portalu Azure

### <a name="programmatically-add-an-endpoint"></a>Programowe Dodawanie punktu końcowego
Możesz dodać oceniania punktów końcowych przy użyciu hello przykładowy kod podany w tym [repozytorium github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Użyj portalu tooadd usługi sieci Web platformy Microsoft Azure hello punktu końcowego
1. W usłudze Machine Learning Studio kolumny nawigacji po lewej stronie powitania kliknij usług sieci Web.
2. U dołu hello hello pulpit nawigacyjny z usługi sieci web, kliknij przycisk **Zarządzaj punktami końcowymi Podgląd**.
3. Kliknij pozycję **Dodaj**.
4. Wpisz nazwę i opis dla nowego punktu końcowego hello. Wybierz poziom rejestrowania hello i czy jest włączone przykładowych danych. Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi sieci web uczenie maszynowe](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Witaj Użyj klasycznego portalu Azure tooadd punktu końcowego
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. W menu po lewej stronie powitania kliknij **uczenia maszynowego**.
3. W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.
4. W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .
5. U dołu hello hello strony, kliknij przycisk **Dodawanie punktu końcowego**. Aby uzyskać więcej informacji dotyczących dodawania punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Aktualizacja hello dodać punktu końcowego Uczonego modelu
proces ponownego trenowania hello toocomplete, należy zaktualizować hello nauczony model hello nowy punkt końcowy, który został dodany.

* Jeśli dodano nowy punkt końcowy hello przy użyciu klasycznego portalu Azure hello, możesz kliknąć nazwę hello nowego punktu końcowego w portalu hello, a następnie hello **operacja UpdateResource** adres URL hello tooget będzie potrzebny modelu tooupdate hello punktu końcowego łącza.
* Jeśli dodano hello punktu końcowego za pomocą hello przykładowy kod, w tym lokalizacji adres URL pomocy hello identyfikowane przez hello *HelpLocationURL* wartość w danych wyjściowych hello.

adres URL ścieżki hello tooretrieve:

1. Skopiuj i wklej adres URL hello w przeglądarce.
2. Kliknij łącze aktualizacji zasobów hello.
3. Skopiuj hello adresu URL przesyłania żądania PATCH hello. Na przykład:
   
     ADRES URL POPRAWKI: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2

Można teraz używać hello tooupdate uczonego modelu hello oceniania punktu końcowego, który został utworzony wcześniej.

Witaj następującego przykładowego kodu pokazuje sposób toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*i punktu końcowego hello tooupdate poprawka adresu URL.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Witaj *apiKey* i hello *endpointUrl* dla wywołania hello można uzyskać z poziomu pulpitu nawigacyjnego punktu końcowego.

Witaj wartość hello *nazwa* parametru w *zasobów* ma hello dopasowania nazwy zasobu hello zapisany Uczonego modelu w eksperyment predykcyjny hello. Witaj tooget Nazwa zasobu:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. W menu po lewej stronie powitania kliknij **uczenia maszynowego**.
3. W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.
4. W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .
5. Kliknij przycisk hello nowy punkt końcowy, dodane.
6. Na powitania punktu końcowego pulpitu nawigacyjnego, kliknij przycisk **aktualizacji zasobów**.
7. Na stronie dokumentacji interfejsu API zasobów aktualizacji hello hello usługi sieci web, można znaleźć hello **Nazwa zasobu** w obszarze **nadaje się do aktualizacji zasobów**.

Jeśli token sygnatury dostępu Współdzielonego wygasa przed zakończeniem Trwa aktualizowanie punktu końcowego hello, należy wykonać GET z hello tooobtain zadania o identyfikatorze nowego tokenu.

Gdy kod hello został uruchomiony pomyślnie, hello nowy punkt końcowy należy zacząć przy użyciu modelu hello retrained około 30 sekund.

## <a name="summary"></a>Podsumowanie
Przy użyciu hello ponownego trenowania interfejsów API, można zaktualizować hello uczonego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:

* Model okresowego ponownego trenowania nowymi danymi.
* Dystrybucja toocustomers modelu hello celem jest umożliwienie je ponownie ucz hello modelu, używając własnych danych.

## <a name="next-steps"></a>Następne kroki
[Rozwiązywanie problemów z hello ponownego trenowania usługi sieci web klasycznego Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md)

