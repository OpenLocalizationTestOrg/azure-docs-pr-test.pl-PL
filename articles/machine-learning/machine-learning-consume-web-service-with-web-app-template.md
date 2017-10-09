---
title: "aaaConsume usługi sieci web uczenie maszynowe za pomocą szablonu aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Szablon aplikacji sieci web w portalu Azure Marketplace tooconsume usługi sieci web predykcyjnej w usłudze Azure Machine Learning."
keywords: "Usługa sieci Web, operationalization, interfejsu API REST, uczenia maszynowego"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Korzystanie z usługi sieci Web Azure Machine Learning za pomocą szablonu aplikacji sieci Web

Po opracowany model predykcyjny i wdrożyć go jako usługi sieci web platformy Azure przy użyciu usługi Machine Learning Studio lub za pomocą narzędzi, takich jak R lub Python, są dostępne hello operationalized modelu, używając interfejsu API REST.

Istnieją różne sposoby tooconsume hello dostępu i interfejsu API REST hello usługi sieci web. Na przykład można napisać aplikację w języku C#, R lub Python za pomocą hello przykładowy kod wygenerowany przez po wdrożeniu usługi sieci web hello (dostępne w hello [usługi Machine Learning portalu](https://services.azureml.net/quickstart) lub na pulpicie nawigacyjnym usługi sieci web hello w Usługa Machine Learning Studio). Lub użyć hello przykładowy program Microsoft Excel skoroszyt utworzony na powitania tym samym czasie.

Ale hello tooaccess najszybszym i Najprostszym sposobem usługi sieci web jest dostępna w hello szablonów aplikacji sieci Web hello [Azure Marketplace aplikacji sieci Web](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Witaj szablonów aplikacji sieci Web uczenie maszyny Azure
Szablony aplikacji sieci web Hello dostępne w hello Azure Marketplace można utworzyć aplikacji sieci web niestandardowego, który zna usługi sieci web dane wejściowe i oczekiwanych rezultatów. Toodo wystarczy podać hello aplikacji dostępu tooyour Usługa sieci web i danych, a szablon hello hello rest.

Dostępne są dwa szablony:

* [Szablon aplikacji sieci Web usługi Azure ML żądań i odpowiedzi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Szablon aplikacji partii zadań Azure ML wykonywania usługi sieci Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Każdy szablon tworzy przykładowej aplikacji platformy ASP.NET, za pomocą hello URI interfejsu API i klucz dla usługi sieci web i wdraża go jako tooAzure witryny sieci web. Szablon usługi żądań i odpowiedzi (RR) Hello służy do tworzenia aplikacji sieci web, która pozwala toosend pojedynczy wiersz danych toohello sieci web usługi tooget pojedynczego wyniku. Szablon usługi wykonywania wsadowego (BES) Hello tworzenia aplikacji sieci web, która pozwala toosend wiele wierszy danych tooget wiele wyników.

Kodowanie nie jest wymagane toouse tych szablonów. Wystarczy podać hello klucz interfejsu API i identyfikator URI, a hello szablon tworzy aplikację hello.

klucz interfejsu API hello tooget i identyfikator URI żądania usługi sieci web:

1. W hello [Portal usługi sieci Web](https://services.azureml.net/quickstart), nowej usługi sieci web, kliknij przycisk **usług sieci Web** u góry hello. Lub kliknij usługi sieci web klasycznego **klasycznym usługi sieci Web**.
2. Kliknij usługę sieci web hello ma tooaccess.
3. Usługi sieci web klasycznego kliknij punkt końcowy hello ma tooaccess.
4. Kliknij przycisk **Consume** u góry hello.
5. Kopiuj hello **głównej** lub **klucza pomocniczego** i zapisz go.
6. Jeśli tworzysz szablon żądania i odpowiedzi usługi (RR), skopiuj hello **żądań i odpowiedzi** identyfikatora URI i zapisz go. Jeśli tworzysz szablon usługi wykonywania wsadowego (BES), skopiuj hello **żądań wsadowych** identyfikatora URI i zapisz go.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Jak toouse hello szablonu żądań i odpowiedzi usługi (RR)
Wykonaj te kroki toouse hello rekordy zasobów szablonu sieci web app, pokazane na powitania po diagramu.

![Proces toouse rekordy zasobów sieci web szablonu][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Przejdź toohello [portalu Azure](https://portal.azure.com), **logowania**, kliknij przycisk **nowy**, wyszukaj i wybierz **aplikacji sieci Web usługi Azure ML żądanie-odpowiedź**, następnie kliknij przycisk **Utworzyć**. 
   
   * Nadaj unikatową nazwę aplikacji sieci web. adres URL aplikacji sieci web hello Hello będzie tej nazwy, a następnie `.azurewebsites.net.` na przykład`http://carprediction.azurewebsites.net.`
   * Wybierz hello subskrypcji platformy Azure i usługi, w których jest uruchomiona usługa sieci web.
   * Kliknij przycisk **Utwórz**.
     
     ![Tworzenie aplikacji sieci Web][image5]

4. Po zakończeniu Azure wdrażanie aplikacji sieci web powitania kliknij hello **adres URL** na hello strony ustawień aplikacji sieci web na platformie Azure, lub wprowadź adres URL hello w przeglądarce sieci web. Na przykład: `http://carprediction.azurewebsites.net.`
5. Gdy hello uruchamia pierwszej aplikacji sieci web go pojawi się prośba o hello **adresu URL przesyłania interfejsu API** i **klucz interfejsu API**.
   Wprowadź wartości hello został wcześniej zapisany (**przez identyfikator URI żądania** i **klucz interfejsu API**odpowiednio).
     
     Kliknij przycisk **przesłać**.
     
     ![Wprowadź Post identyfikator URI i klucz interfejsu API][image6]

6. Witaj aplikacja sieci web jest wyświetlana jego **konfiguracji aplikacji sieci Web** strony z hello bieżące ustawienia usługi sieci web. Tutaj można wprowadzić zmiany toohello ustawienia używane przez hello aplikacji sieci web.
   
   > [!NOTE]
   > Zmiana ustawień hello tutaj tylko zmiany ich tej aplikacji sieci web. Ustawienia domyślne hello usługi sieci web nie go zmienić. Na przykład, jeśli zmienisz hello **opis** w tym miejscu nie zmienia hello opis wyświetlany na powitania pulpit nawigacyjny usługi sieci web w usłudze Machine Learning Studio.
   > 
   > 
   
    Gdy wszystko będzie gotowe, kliknij przycisk **zapisać zmiany**, a następnie kliknij przycisk **Przejdź tooHome strony**.

7. Z hello stronę główną, którą można wprowadzić wartości usługi sieci web tooyour toosend. Kliknij przycisk **przesyłania** gdy wszystko będzie gotowe, i zostanie zwrócony wynik hello.

Jeśli chcesz, aby tooreturn toohello **konfiguracji** pozycję Przejdź toohello `setting.aspx` strony hello aplikacji sieci web. Na przykład: `http://carprediction.azurewebsites.net/setting.aspx.` klucz interfejsu API hello tooenter zostanie wyświetlony monit o będzie można ponownie — należy czy tooaccess hello strony i zaktualizuj ustawienia hello.

Można zatrzymać, ponownie uruchomić lub usunąć hello aplikacji sieci web w portalu Azure, takich jak każda inna aplikacja sieci web hello. Tak długo, jak działa można wybrać adres sieci web macierzystego toohello i wprowadź nowe wartości.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Jak toouse hello szablonu usługi wykonywania wsadowego (BES)
Można użyć hello BES szablonu aplikacji sieci web w hello sam sposób jako szablon RR hello, z wyjątkiem tego hello aplikacji sieci web, która jest tworzona umożliwi toosubmit wiele wierszy danych i odbierania wiele wyników.

Witaj wartości wejściowe dla usługi sieci web wykonywania wsadowego mogą pochodzić z magazynu Azure lub plikiem lokalnym; wyniki Hello są przechowywane w kontenerze magazynu Azure.
Tak, będzie konieczne toohold kontenera magazynu Azure hello wyników zwróconych przez hello aplikacji sieci web, i będzie trzeba tooget danych wejściowych gotowe.

![Przetwarzanie toouse BES szablonu sieci web][image2]

1. Wykonaj hello same procedury toocreate hello BES zbyt sieci web aplikacji, jak w przypadku hello rekordy zasobów szablonu, z wyjątkiem go[szablonu aplikacji sieci Web Azure ML partii wykonywania usługi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello szablonu usługi BES w portalu Azure Marketplace i kliknij przycisk **tworzenie aplikacji sieci Web** .

2. toospecify miejscu wyniki hello przechowywane, wprowadź informacje o kontenerze docelowego hello na stronie głównej aplikacji sieci web hello. Również określić, gdzie hello aplikacji sieci web można uzyskać wartości wejściowe hello, w pliku lokalnym lub kontener magazynu Azure.
   Kliknij przycisk **przesłać**.
   
    ![Informacje o magazynu][image7]

Hello aplikacji sieci web zostanie wyświetlona strona o stanie zadania.
Po ukończeniu zadania hello będziesz mieć lokalizacji hello hello wyników w magazynie obiektów blob platformy Azure. Istnieje również opcja hello pobierania pliku lokalne powitania wyników tooa.

## <a name="for-more-information"></a>Aby uzyskać więcej informacji
więcej informacji na temat toolearn...

* Tworzenie eksperymentu uczenia maszynowego o usłudze Machine Learning Studio, zobacz [Tworzenie pierwszego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md)
* toodeploy Twojego uczenia maszynowego eksperymentu jako usługi sieci web, zobacz temat [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* inne sposoby tooaccess usługi sieci web, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
