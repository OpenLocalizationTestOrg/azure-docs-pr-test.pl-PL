---
title: "aaaUse parametry usługi sieci Web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toomodify parametry usługi sieci Web Azure Machine Learning toouse hello zachowanie modelu podczas uzyskiwania dostępu do usługi sieci web hello."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Używanie parametrów usługi sieci Web Azure Machine Learning
Usługi sieci web Azure Machine Learning jest tworzony przez publikowanie eksperymentu, która zawiera moduły można skonfigurować parametrów. W niektórych przypadkach może być zachowanie modułu hello toochange hello usługi sieci web jest uruchomiona. *Parametry usługi sieci Web* pozwalają toodo to zadanie. 

Typowym przykładem jest konfigurowanie hello [i zaimportuj dane] [ reader] moduł, tak że użytkownik hello hello opublikowane usługi sieci web można określić innego źródła danych podczas uzyskiwania dostępu do usługi sieci web hello. Lub konfigurowania hello [eksportowanie danych] [ writer] modułu, dzięki czemu można określić inną lokalizację docelową. Inne przykłady zmiana hello liczby bitów na powitania [Tworzenie skrótu funkcji] [ feature-hashing] modułu lub hello liczba żądanych funkcji dla hello [na podstawie filtru wybór funkcji] [ filter-based-feature-selection] modułu. 

Można ustawić parametry usługi sieci Web i skojarz je z jednego lub więcej parametrów modułu w eksperymencie i czy są one wymagane lub opcjonalne. Hello użytkownika usługi sieci web hello można następnie podanie wartości tych parametrów przy wywoływaniu hello usługi sieci web. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Jak tooset i użyj parametry usługi sieci Web
Parametr usługi sieci Web należy zdefiniować przez kliknięcie przycisku hello ikona dalej toohello parametru modułu i wybierając polecenie "Ustaw jako parametr usługi sieci web". Tworzy nowy parametr usługi sieci Web i łączy go toothat parametru modułu. Następnie podczas uzyskiwania dostępu do usługi sieci web hello hello użytkownika można określić wartość dla hello parametr usługi sieci Web i jest stosowane toohello parametr modułu.

Po zdefiniowaniu parametr usługi sieci Web jest dostępna tooany innych parametrów modułu w eksperymencie hello. Po zdefiniowaniu parametr usługi sieci Web skojarzony z parametrem dla jednego modułu można użyć tego samego parametru usługi sieci Web dla inny moduł, tak długo, jak parametr hello oczekuje hello tego samego typu wartości. Na przykład jeśli hello parametr usługi sieci Web jest wartość liczbowa, następnie tylko umożliwia dla modułu parametrów, które oczekują wartość liczbową. Gdy użytkownik hello ustawia wartość hello parametr usługi sieci Web, będzie zastosowane tooall skojarzone parametry modułu.

Można zdecydować, czy tooprovide domyślną wartość hello parametr usługi sieci Web. Jeśli następnie hello parametr jest opcjonalny dla użytkownika hello hello usługi sieci web. Jeśli nie podasz wartość domyślną, następnie hello użytkownika jest wymagane tooenter wartość podczas uzyskiwania dostępu do usługi sieci web hello.

Witaj dokumentacji interfejsu API usługi sieci web hello zawiera informacje o użytkowniku usługi sieci web hello na jak toospecify hello parametr usługi sieci Web programowo podczas uzyskiwania dostępu do usługi sieci web hello.

> [!NOTE]
> Witaj dokumentacji interfejsu API dla usługi sieci web klasycznego jest zapewniana za pomocą hello **strona pomocy interfejsu API** łącze usługi sieci web hello **pulpitu NAWIGACYJNEGO** w usłudze Machine Learning Studio. Witaj dokumentacji interfejsu API dla nowej usługi sieci web jest zapewniana za pomocą hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net/Quickstart) portalu na powitania **Consume** i **interfejsu API programu Swagger** stron dla użytkownika Usługa sieci Web.
> 
> 

## <a name="example"></a>Przykład
Na przykład załóżmy, że mamy doświadczenia z [eksportowanie danych] [ writer] moduł, który wysyła magazynu obiektów blob tooAzure informacji. Zdefiniujemy parametr usługi sieci Web o nazwie "Ścieżka obiektu Blob" umożliwiająca hello sieci web usługi użytkownik toochange hello ścieżki toohello magazynu obiektów blob podczas uzyskiwania dostępu do usługi hello.

1. W usłudze Machine Learning Studio, kliknij przycisk hello [eksportowanie danych] [ writer] tooselect modułu go. Jego właściwości są wyświetlane w toohello okienko właściwości hello rogu hello kanwy eksperymentu.
2. Określ typ magazynu hello:
   
   * W obszarze **określ miejsce docelowe danych**, wybierz pozycję "Magazyn obiektów Blob Azure".
   * W obszarze **Określ typ uwierzytelniania**, wybierz "Konto".
   * Wprowadź informacje o koncie hello na powitania magazynu obiektów blob platformy Azure. 
     <p />
3.Kliknij toohello ikona hello rogu hello **ścieżki tooblob, począwszy od parametru kontenera**. Wygląda następująco:
   
   ![Ikona parametr usługi sieci Web][icon]
   
   Wybierz "Ustaw jako parametr usługi sieci web".
   
   Wpis zostanie dodany w obszarze **parametry usługi sieci Web** u dołu okienka właściwości hello hello nazwy "Ścieżka tooblob rozpoczynający się od kontenera" hello. Jest to parametr usługi sieci Web, która jest teraz hello skojarzony z tym [eksportowanie danych] [ writer] parametru modułu.
4. toorename hello parametr usługi sieci Web, kliknij nazwę hello wprowadź "Ścieżka obiektu Blob" i naciśnij klawisz hello **Enter** klucza. 
5. tooprovide wartość domyślną dla hello parametr usługi sieci Web, kliknij toohello ikona hello prawej strony nazwy hello, wybierz "Podać wartości domyślnej", wprowadź wartość (na przykład "container1/output1.csv") i naciśnij klawisz hello **Enter** klucza.
   
   ![Parametr usługi sieci Web][parameter]
6. Kliknij pozycję **Run** (Uruchom). 
7. Kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]** usługi sieci web hello toodeploy.

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Hello użytkownika usługi sieci web hello można teraz określić nową lokalizację docelową dla hello [eksportowanie danych] [ writer] modułu podczas uzyskiwania dostępu do usługi sieci web hello.

## <a name="more-information"></a>Więcej informacji
Aby uzyskać bardziej szczegółowy przykład zobacz hello [parametry usługi sieci Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) wpisu w hello [Machine Learning blogu](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do usługi sieci web uczenie maszynowe, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

