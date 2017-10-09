---
title: "usługi sieci web aaaRetrain istniejące predykcyjnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aktualizacja i tooretrain modelu hello sieci web usługi toouse hello nowo uczonego modelu w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Ponownie ucz istniejącej usługi sieci web predykcyjnej
W tym dokumencie opisano hello ponownego trenowania proces hello następujących scenariuszy:

* Masz eksperyment uczenia i eksperyment predykcyjny, która została wdrożona jako usługi sieci web operationalized.
* Masz nowe dane, które mają tooperform toouse usługi sieci web predykcyjnej jego oceniania.

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Począwszy od istniejącej usługi sieci web, a eksperymentów, należy toofollow następujące kroki:

1. Model hello aktualizacji.
   1. Modyfikowanie użytkownika tooallow eksperymentu uczenia dla sieci web usługi wejścia i wyjścia.
   2. Wdróż eksperyment uczenia hello jako usługę sieci web ponownego trenowania.
   3. Użyj eksperyment uczenia hello usługi wykonywania wsadowego (BES) tooretrain hello modelu.
2. Użyj hello Azure Machine Learning PowerShell polecenia cmdlet tooupdate hello predykcyjnej eksperymentu.
   1. Zaloguj się tooyour konta usługi Azure Resource Manager.
   2. Pobierz definicję usługi sieci web hello.
   3. Eksportowanie definicji usługi sieci web hello formacie JSON.
   4. Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.
   5. Zaimportuj hello JSON do definicji usługi sieci web.
   6. Zaktualizuj usługę sieci web hello z nowej definicji usługi sieci web.

## <a name="deploy-hello-training-experiment"></a>Wdrażanie eksperyment uczenia hello
toodeploy hello eksperyment uczenia ponownego trenowania Usługa sieci web, należy dodać modelu usług sieci web wejściami i wyjściami toohello. Łącząc *wyjście usługi sieci Web* modułu toohello eksperymentu  *[Train Model] [ train-model]*  moduł, możesz włączyć hello szkolenia eksperymentu tooproduce nową uczenia modelu używanego w eksperymencie predykcyjnej. Jeśli masz *Evaluate Model* moduł, możesz również dołączyć wyniki oceny hello tooget wyjście usługi sieci web jako dane wyjściowe.

tooupdate eksperymentu uczenia:

1. Połącz *wejściowego usługi sieci Web* modułu tooyour danych wejściowych (na przykład *Clean Missing Data* modułu). Zazwyczaj mają tooensure przetwarzanego w danych wejściowych hello takie same jak oryginalne dane szkolenia.
2. Połącz *wyjście usługi sieci Web* dane wyjściowe toohello modułu z *Train Model* modułu.
3. Jeśli masz *Evaluate Model* modułu, a wyniki oceny hello toooutput, Połącz *wyjście usługi sieci Web* dane wyjściowe toohello modułu z *Evaluate Model* Moduł.

Uruchamianie eksperymentu.

Następnie należy wdrożyć eksperyment uczenia hello jako usługę sieci web, który spowoduje utworzenie uczonego modelu i wyniki oceny modelu.  

U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web**, a następnie wybierz **wdrażanie usługi sieci Web [New]**. portal usługi sieci Web systemu Azure Machine Learning Hello otwiera toohello **wdrażanie usługi sieci Web** strony. Wpisz nazwę usługi sieci web, wybierz plan płatności, a następnie kliknij przycisk **Wdróż**. Metody wykonywania wsadowego usługi hello można używać tylko do tworzenia modeli przeszkolone.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Ponownie ucz modelu hello nowymi danymi za pomocą usługi BES
W tym przykładzie używamy C# hello toocreate ponownego trenowania aplikacji. Umożliwia także Python lub R tooaccomplish kod przykładowy tego zadania.

Witaj toocall ponownego trenowania interfejsów API:

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio: **nowy** > **projektu** > **Visual C#** > **Windows Desktop klasycznego** > **aplikacji konsoli (.NET Framework)**.
2. Zaloguj się toohello portal usługi sieci Web usługi Machine Learning.
3. Kliknij opcję usługi sieci web hello, z którymi pracujesz.
4. Kliknij przycisk **korzystać**.
5. U dołu hello hello **Consume** strony w hello **przykładowy kod** kliknij **partii**.
6. Skopiuj hello próbki kodu C# dla wykonywania wsadowego i wklej go do pliku Program.cs hello. Upewnij się, że w tej przestrzeni nazw hello pozostanie niezmieniona.

Dodaj hello pakiet NuGet Microsoft.AspNet.WebApi.Client, jak określono w komentarzach hello. tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania hello, być może konieczne tooinstall hello [biblioteki klienta usługi Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage).

Witaj Poniższy zrzut ekranu przedstawia hello **Consume** w portalu usługi sieci Web systemu Azure Machine Learning hello na stronie.

![Korzystanie ze strony][1]

### <a name="update-hello-apikey-declaration"></a>Zaktualizuj hello apikey deklaracji
Zlokalizuj hello **apikey** deklaracji:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

W hello **zużycie podstawowe informacje o** sekcji hello **Consume** strony Znajdź klucz podstawowy hello i skopiuj go toohello **apikey** deklaracji.

### <a name="update-hello-azure-storage-information"></a>Zaktualizuj informacje magazynie Azure hello
Hello BES przykładowy kod operacji przekazywania plików z tooAzure dysk lokalny (na przykład "C:\temp\CensusIpnput.csv"), magazynu, procesy i zapisuje hello wyników wstecz tooAzure magazynu.  

tooupdate hello Azure Storage informacji, należy pobrać hello konta magazynu, że nazwa, klucz i kontenera informacji dla konta magazynu z hello klasycznego portalu Azure, a następnie correspondi hello aktualizacji po uruchomieniu eksperymentu, Witaj, co przepływ pracy powinny być podobne toohello następujące czynności:

![Wynikowa przepływu pracy po uruchomieniu][4]wartości ng w kodzie hello.

1. Zaloguj się toohello klasycznego portalu Azure.
2. W kolumnie nawigacji po lewej stronie powitania kliknij **magazynu**.
3. Z listy hello kont magazynu wybierz jeden toostore hello retrained modelu.
4. U dołu hello hello strony, kliknij przycisk **Zarządzaj kluczami dostępu**.
5. Skopiuj i Zapisz hello **podstawowy klucz dostępu** hello Zamknij okno dialogowe i.
6. U góry hello hello strony, kliknij przycisk **kontenery**.
7. Wybierz istniejącego kontenera, lub Utwórz nową i Zapisz nazwę hello.

Zlokalizuj hello *StorageAccountName*, *StorageAccountKey*, i *StorageContainerName* deklaracje i Aktualizuj hello wartości zapisane w portalu klasycznym hello .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Ponadto musisz zapewnić, że tego pliku wejściowego hello jest dostępna w lokalizacji hello w kodzie hello.

### <a name="specify-hello-output-location"></a>Określ lokalizację danych wyjściowych hello
Po określeniu lokalizacji wyjściowej hello w ładunku żądania hello hello rozszerzenie pliku hello, który jest określony w *RelativeLocation* muszą być określone jako `ilearner`. Zobacz poniższy przykład hello:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Witaj poniżej przedstawiono przykład ponownego trenowania dane wyjściowe: ![ponownego trenowania danych wyjściowych][6]

## <a name="evaluate-hello-retraining-results"></a>Witaj ponownego trenowania wyników oceny
Po uruchomieniu aplikacji hello hello danych wyjściowych zawiera adres URL hello i tokenu sygnatury dostępu współdzielonego, który wyniki oceny hello tooaccess niezbędne są.

Można wyświetlić wyniki wydajności hello modelu hello retrained łącząc hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik Aby uzyskać *output2* (jak pokazano w poprzednim ponownego trenowania obrazu wyjściowego hello) i wklejanie hello pełny adres URL do hello na pasku adresu przeglądarki.  

Witaj toodetermine wyników należy sprawdzić, czy nowo uczonego modelu hello wykonuje również za mało hello tooreplace jedną istniejącą.

Kopiuj hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik.

## <a name="retrain-hello-web-service"></a>Ponownie ucz hello usługi sieci web
Gdy retrain nową usługę sieci web, należy zaktualizować hello predykcyjnego modelu usług sieci web definicji tooreference hello nowe przeszkolone. definicji usługi sieci web Hello jest wewnętrznej reprezentacji hello uczonego modelu hello usługi sieci web i nie można bezpośrednio modyfikować. Upewnij się, czy są pobierania definicji usługi sieci web hello predykcyjnej eksperymentu, a nie eksperyment uczenia.

## <a name="sign-in-tooazure-resource-manager"></a>Zaloguj się tooAzure Resource Manager
Konto platformy Azure w środowisku PowerShell hello tooyour musi pierwszy raz logujesz się przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.

## <a name="get-hello-web-service-definition-object"></a>Pobierz obiekt definicji usługi sieci Web hello
Następnie Pobierz obiekt definicji usługi sieci Web hello przez wywołanie hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, uruchom polecenie cmdlet Get-AzureRmMlWebService hello bez żadnych parametrów toodisplay hello sieci web usług w Twojej subskrypcji. Zlokalizuj hello usługi sieci web, a następnie sprawdź jej identyfikatora usługi sieci web Witaj Nazwa grupy zasobów hello jest czwartym elementem hello w identyfikatorze hello zaraz po hello *resourceGroups* elementu. W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Alternatywnie toodetermine hello Nazwa grupy zasobów istniejącej usługi sieci web, należy się zalogować w portalu usługi sieci Web systemu Azure Machine Learning toohello. Wybierz usługę sieci web hello. Nazwa grupy zasobów Hello jest hello elementu piątym powitania adres URL usługi sieci web hello, zaraz po hello *resourceGroups* elementu. W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Eksport obiektu definicji usługi sieci Web hello w formacie JSON
Definicja hello toomodify hello uczonego modelu toouse hello nowo uczenia modelu, należy najpierw użyć hello [AzureRmMlWebService eksportu](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport polecenia cmdlet go plik tooa formatu JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Obiekt blob ilearner toohello odwołania hello aktualizacji
Zasoby hello odszukaj hello [uczonego modelu] hello aktualizacji *uri* wartość hello *locationInfo* węzeł z identyfikatora URI obiektu hello ilearner blob hello. Witaj identyfikatora URI jest generowany przez połączenie hello *BaseLocation* i hello *RelativeLocation* z wyników hello hello BES Wywołanie ponownego trenowania.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Importowanie hello JSON do obiektu definicji usługi sieci Web
Należy użyć hello [AzureRmMlWebService importu](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert polecenia cmdlet zmodyfikowany plik JSON do obiektu definicji usługi sieci Web z użyciem eksperymentu predicative hello tooupdate.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Usługi sieci web hello aktualizacji
Na koniec użyj hello [AzureRmMlWebService aktualizacji](https://msdn.microsoft.com/library/azure/mt767922.aspx) eksperyment predykcyjny hello tooupdate polecenia cmdlet.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
