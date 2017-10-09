---
title: modeli aaaRetrain Machine Learning | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooprogrammatically retrain modelu i aktualizacji hello web toouse hello nowo uczonego modelu usług w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Programowe ponowne trenowanie modeli usługi Machine Learning
W tym przewodniku dowiesz się, jak tooprogrammatically retrain Azure Machine Learning usługi sieci Web przy użyciu języka C# i hello usługi wykonywania wsadowego usługi Machine Learning.

Po ma retrained hello modelu, hello następujące wskazówki pokazują, jak tooupdate hello modelu w usłudze sieci web predykcyjnej:

* Jeśli wdrożono klasycznym usługi sieci web w portalu usługi sieci Web usługi Machine Learning hello, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md). 
* Jeśli wdrożono nową usługę sieci web, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).

Omówienie hello ponownego trenowania procesu, zobacz [Retrain modelu uczenia maszynowego](machine-learning-retrain-machine-learning-model.md).

Jeśli chcesz toostart z istniejącą nowej usługi Azure Resource Manager na podstawie usługi sieci web, zobacz [Retrain istniejącej usługi sieci web predykcyjnej](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Tworzenie eksperymentu szkolenia
Na przykład użyjesz "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" hello Microsoft Azure Machine Learning próbek. 

toocreate eksperymentu hello:

1. Zaloguj się do tooMicrosoft Azure Machine Learning Studio. 
2. Na powitania prawym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **nowy**.
3. Wybierz przykład 5 z hello Samples firmy Microsoft.
4. toorename hello eksperymentu, u góry hello hello kanwy eksperymentu, wybierz nazwę eksperymentu hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych".
5. Typ modelu spisu.
6. U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.
7. Kliknij przycisk **Konfiguruj usługę sieci web** i wybierz **ponownego trenowania usługi sieci web**. 

Oto Hello hello początkowej eksperymentu.
   
   ![Początkowa eksperymentu.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Utworzyć eksperyment predykcyjny i Opublikuj jako usługi sieci web
Następnie należy utworzyć eksperyment Predicative.

1. U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web**. Ten hello model jest zapisywany jako Uczonego modelu i dodaje modułów wejścia i wyjścia usługi sieci web. 
2. Kliknij pozycję **Run** (Uruchom). 
3. Po eksperymentu hello zakończył działanie, kliknij przycisk **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]**.

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Wdrażanie eksperyment uczenia hello jako usługę sieci web szkolenia
tooretrain hello trenowanego modelu, należy wdrożyć eksperyment uczenia hello utworzony jako usługę sieci web Retraining. Ta usługa sieci web musi *wyjście usługi sieci Web* modułu połączone toohello  *[Train Model] [ train-model]*  modułu, toobe stanie tooproduce nowy modele przeszkolone.

1. eksperyment uczenia toohello tooreturn, kliknij ikonę eksperymenty hello w okienku po lewej stronie powitania, a następnie kliknij eksperyment hello o nazwie modelu spisu.  
2. W polu wyszukiwania elementów eksperymentu wyszukiwania hello wpisz usługi sieci web. 
3. Przeciągnij *wprowadzania usługi sieci Web* modułu na powitania obszaru roboczego eksperymentu i połącz toohello jego dane wyjściowe *Clean Missing Data* modułu.  Dzięki temu, że dane ponownego trenowania jest przetwarzany hello takie same jak oryginalne dane szkolenia.
4. Przeciągnij dwa *wyjście usługi sieci web* modułów na powitania eksperymentu kanwy. Połącz dane wyjściowe hello hello *Train Model* modułu tooone i hello dane wyjściowe hello *Evaluate Model* modułu toohello innych. Witaj wyjście usługi sieci web dla **Train Model** daje hello nowe trenowanego modelu. Hello dane wyjściowe dołączony zbyt**Evaluate Model** zwraca wyjściowy ten moduł, który jest hello wyniki.
5. Kliknij pozycję **Run** (Uruchom). 

Następnie należy wdrożyć eksperyment uczenia hello jako usługę sieci web, który spowoduje utworzenie uczonego modelu i wyniki oceny modelu. tooaccomplish to dalej zestawu działań są zależne od tego, czy użytkownik pracuje z usługą sieci web klasycznego lub nową usługę sieci web.  

**Usługa sieci web klasycznego**

U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**. Usługi sieci Web Hello **pulpitu nawigacyjnego** zostanie wyświetlony z strona pomocy hello klucz interfejsu API i hello interfejsu API dla wykonywania wsadowego usługi. Witaj metody wykonywania wsadowego usługi może służyć do tworzenia modeli przeszkolone.

**Nowa usługa sieci web**

U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**. portal usługi sieci Web sieci Web usługi Azure Machine Learning Hello otwiera stronę usługi sieci web Deploy toohello. Wpisz nazwę usługi sieci web i wybierz plan płatności, a następnie kliknij przycisk **Wdróż**. Hello metody wsadowe mogą służyć do tworzenia modeli przeszkolone

W obu przypadkach po obejmuje działania ukończone hello wynikowy przepływu pracy powinna wyglądać następująco:

![Wynikowa przepływu pracy, po uruchomieniu.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Ponownie ucz modelu hello nowymi danymi za pomocą usługi BES
Na przykład używasz C# hello toocreate ponownego trenowania aplikacji. Umożliwia także hello Python lub R przykładowy kod tooaccomplish to zadanie.

toocall hello ponownego trenowania interfejsów API:

1. Tworzenie aplikacji konsolowej C# w programie Visual Studio: **nowy** > **projektu** > **Visual C#** > **Windows Desktop klasycznego** > **aplikacji konsoli (.NET Framework)**.
2. Zaloguj się toohello portalu Usługa sieci Web usługi Machine Learning.
3. Podczas pracy z usługą sieci web klasycznego, kliknij przycisk **klasycznym usługi sieci Web**.
   1. Kliknij przycisk hello usługi sieci web, którą użytkownik pracuje z.
   2. Kliknij przycisk hello domyślnego punktu końcowego.
   3. Kliknij przycisk **korzystać**.
   4. U dołu hello hello **Consume** strony w hello **przykładowy kod** kliknij **partii**.
   5. Nadal toostep 5 tej procedury.
4. Jeśli pracujesz z nową usługę sieci web, kliknij przycisk **usług sieci Web**.
   1. Kliknij przycisk hello usługi sieci web, którą użytkownik pracuje z.
   2. Kliknij przycisk **korzystać**.
   3. U dołu strony Consume hello w hello hello **przykładowy kod** kliknij **partii**.
5. Skopiuj hello próbki kodu C# dla wykonywania wsadowego i wklej go do pliku Program.cs hello, upewniając się, że przestrzeń nazw hello pozostanie niezmieniona.

Dodaj hello pakiet Nuget Microsoft.AspNet.WebApi.Client określonych w hello komentarze. tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania hello, być może konieczne tooinstall powitania klienta biblioteki dla usług magazynu Microsoft Azure. Aby uzyskać więcej informacji, zobacz [usługi magazynu systemu Windows](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Zaktualizuj hello apikey deklaracji
Zlokalizuj hello **apikey** deklaracji.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

W hello **zużycie podstawowe informacje o** sekcji hello **Consume** strony Znajdź klucz podstawowy hello i skopiuj go toohello **apikey** deklaracji.

### <a name="update-hello-azure-storage-information"></a>Zaktualizuj informacje magazynie Azure hello
Hello BES przykładowy kod operacji przekazywania plików z dysku (na przykład "C:\temp\CensusIpnput.csv") tooAzure magazynu, procesy i zapisuje hello wyników wstecz tooAzure magazynu.  

tooaccomplish to zadanie, należy pobrać hello nazwę, klucz oraz kontenera informacji o koncie magazynu dla konta magazynu z hello klasycznego portalu Azure i zaktualizuj hello odpowiednie wartości w kodzie hello. 

1. Zaloguj się toohello klasycznego portalu Azure.
2. W kolumnie nawigacji po lewej stronie powitania kliknij **magazynu**.
3. Z listy hello kont magazynu wybierz jeden toostore hello retrained modelu.
4. U dołu hello hello strony, kliknij przycisk **Zarządzaj kluczami dostępu**.
5. Skopiuj i Zapisz hello **podstawowy klucz dostępu** hello Zamknij okno dialogowe i. 
6. U góry hello hello strony, kliknij przycisk **kontenery**.
7. Wybierz istniejącego kontenera lub Utwórz nową i Zapisz nazwę hello.

Zlokalizuj hello *StorageAccountName*, *StorageAccountKey*, i *StorageContainerName* deklaracje i zapisany w wartości hello aktualizacji hello portalu Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Ponadto musisz zapewnić, że plik wejściowy hello jest dostępna w lokalizacji hello, które określisz w kodzie hello. 

### <a name="specify-hello-output-location"></a>Określ lokalizację danych wyjściowych hello
Podczas określania lokalizacji wyjściowej hello na powitania ładunku żądania, hello rozszerzenie określone w pliku hello *RelativeLocation* muszą być określone jako ilearner. 

Zobacz poniższy przykład hello:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> Witaj nazwy lokalizacji danych wyjściowych mogą być inne niż te, w tym przewodniku oparte na powitania kolejności, w której są dodawane modułów wyjście usługi sieci web hello hello. Ponieważ skonfigurowaniu tego eksperymentu uczenia z danych wyjściowych dwóch hello wyniki obejmują informacje o lokalizacji magazynu dla obu z nich.  
> 
> 

![Ponownego trenowania danych wyjściowych][6]

Diagram 4: Ponownego trenowania danych wyjściowych.

## <a name="evaluate-hello-retraining-results"></a>Ocena wyników ponownego trenowania hello
Po uruchomieniu aplikacji hello hello danych wyjściowych zawiera adres URL hello i tooaccess niezbędne tokenu sygnatury dostępu Współdzielonego hello wyniki oceny.

Można wyświetlić wyniki wydajności hello modelu hello retrained łącząc hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik Aby uzyskać *output2* (jak pokazano w poprzednim ponownego trenowania obrazu wyjściowego hello) i wklejanie hello pełny adres URL na pasku adresu przeglądarki hello.  

Witaj toodetermine wyników należy sprawdzić, czy nowo uczonego modelu hello wykonuje również za mało hello tooreplace jedną istniejącą.

Kopiuj hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik użyjesz ich podczas hello ponownego trenowania procesu.

## <a name="next-steps"></a>Następne kroki
Jeśli wdrożono usługę sieci web predykcyjnej hello, klikając **wdrażanie usługi sieci Web [klasyczny]**, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md).

Jeśli wdrożono usługę sieci web predykcyjnej hello, klikając **wdrażanie usługi sieci Web [New]**, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
