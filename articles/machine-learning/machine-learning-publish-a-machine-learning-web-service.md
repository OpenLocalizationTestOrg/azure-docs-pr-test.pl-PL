---
title: "aaaDeploy usługi sieci web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak tooconvert szkoleniowego eksperymentu eksperyment predykcyjny tooa, przygotowania go do wdrożenia, a następnie wdrożyć go jako usługi sieci web uczenie maszynowe Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Wdrażanie usługi sieci Web Azure Machine Learning
Usługa Azure Machine Learning umożliwia toobuild, testowanie i wdrażanie rozwiązań z zakresu analiz predykcyjnych.

Z wysokiego poziomu punktu widzenia można to zrobić w trzy kroki:

* **[Tworzenie eksperymentu uczenia]**  -Azure Machine Learning Studio to środowisko visual programowanie zespołowe używanie tootrain i testowania analizy predykcyjnej modelu przy użyciu danych szkoleniowych, wprowadzona.
* **[Przekonwertuj go eksperyment predykcyjny tooa]**  — po modelu po zapoznaniu z istniejącymi danymi i wszystko jest gotowe toouse go tooscore nowe dane, przygotowanie i usprawnienia eksperymentu dla prognoz.
* **[Go wdrożyć jako usługę sieci web]**  — można wdrożyć predykcyjnej eksperymentu jako [nowe] lub [klasycznego] usługi sieci web platformy Azure. Użytkownikom modelu tooyour danych wysyłanie i odbieranie do modelu prognozy.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Tworzenie eksperymentu szkolenia
tootrain modelu analizy predykcyjnej, użyj toocreate Azure Machine Learning Studio eksperyment uczenia, gdzie można obejmują różne dane szkoleniowe tooload modułów, przygotowania hello danych w razie potrzeby Zastosuj algorytmów uczenia maszynowego i ocena wyników hello . Można iterację eksperymentu i spróbuj innej maszyny toocompare algorytmów uczenia i ocena wyników hello.

Hello proces tworzenia i zarządzania nimi eksperymenty szkolenia zostało opisane bardziej dokładnie w innym miejscu. Aby uzyskać więcej informacji zobacz następujące artykuły:

* [Tworzenie prostego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Tworzenie rozwiązania predykcyjnego przy użyciu usługi Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)
* [Importowanie danych szkoleniowych w usłudze Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* [Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Konwertuj eksperyment predykcyjny tooa hello szkolenia eksperymentu
Po gdy udało się nauczyć model, wszystko gotowe tooconvert do szkolenia eksperymentu na tooscore eksperyment predykcyjny nowe dane.

Konwertując tooa predykcyjnej eksperymentu, przygotowujemy Twoje gotowe toobe uczonego modelu wdrożyć jako usługę sieci web oceniania. Użytkownicy usługi sieci web hello może wysyłać danych wejściowych tooyour modelu i model będzie wysyłać wyniki prognozowania hello Wstecz. W trakcie konwertowania tooa predykcyjnej eksperymentu, należy pamiętać, jak ma być Twojej toobe modelu używany przez inne osoby.

tooconvert Twojego tooa eksperymentu uczenia predykcyjnej eksperymentu, kliknij przycisk **Uruchom** u dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web**, a następnie wybierz pozycję **predykcyjnej usługi sieci Web** .

![Konwertuj tooscoring eksperymentu](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Aby uzyskać więcej informacji na temat tooperform konwersji, zobacz [jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Witaj poniższych krokach opisano wdrażanie eksperyment predykcyjny jako nową usługę sieci web. Można także wdrożyć hello eksperymentu jako usługi sieci web klasycznego.

## <a name="deploy-it-as-a-web-service"></a>Go wdrożyć jako usługę sieci web

Eksperyment predykcyjny hello można wdrożyć jako nową usługę sieci web lub usługi sieci web klasycznego.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Wdróż hello eksperyment predykcyjny jako nową usługę sieci web
Teraz, eksperyment predykcyjny hello został przygotowany, można go wdrożyć jako nową usługę sieci web platformy Azure. Przy użyciu usługi sieci web hello, użytkownicy mogą wysyłać modelu tooyour danych i modelu hello zwróci jego prognoz.

toodeploy Twojego predykcyjnej eksperymentu, kliknij przycisk **Uruchom** u dołu hello hello eksperymentu kanwy. Po skończeniu pracy eksperymentu powitania kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [nowy]**.  zostanie otwarta strona wdrożenia Hello hello Usługa sieci Web usługi Machine Learning portalu.

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Wdróż eksperymentu strony portalu usługi sieci Web uczenie maszyny
Na stronie eksperymentu wdrażanie hello wprowadź nazwę usługi sieci web hello.
Wybrać planu cenowego. Jeśli masz istniejące planu cenowego, że zostanie ona wybrana, w przeciwnym razie należy utworzyć nowy plan cen hello usługi.

1. W hello **planu cen** listy rozwijanej, wybierz istniejący plan lub hello **wybierz nowy plan** opcji.
2. W **Nazwa planu**, wpisz nazwę identyfikującą planu hello na rachunku.
3. Wybierz jedną z hello **miesięcznych poziomów Planowanie**. plan Hello się, że warstw domyślne plany toohello Twojego domyślnego regionu i usługi sieci web jest wdrożone toothat regionu.

Kliknij przycisk **Wdróż** i hello **szybkiego startu** zostanie otwarta strona dla usługi sieci web.

strony Szybki Start usługi sieci web Hello zapewnia dostęp i wskazówki na powitania najbardziej typowych zadań, które ma zostać wykonane po utworzeniu usługi sieci web. W tym miejscu mogli łatwo uzyskiwać dostęp zarówno hello testu i Consume strony.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Testowanie nowej usługi sieci web
tootest nową usługę sieci web, kliknij przycisk **testu sieci web usługi** w typowych zadań. Na stronie powitania testu można testować usługi sieci web jako usługa żądań i odpowiedzi (RR) lub usługę wykonywania wsadowego (BES).

Strona testowa RR Hello Wyświetla hello wejść, wyjść i globalne parametry, które zostały określone dla hello eksperymentu. Usługa sieci web hello tootest, możesz ręcznie wprowadzić odpowiednie wartości dla danych wejściowych hello lub podaj rozdzielanych przecinkami (CSV) sformatowany pliku wartości zawierającą wartości testowe hello.

tootest przy użyciu rekordów zasobów, hello trybu widoku listy, wprowadź odpowiednie wartości dla danych wejściowych hello i kliknij przycisk **testu żądanie-odpowiedź**. Wyświetl wyniki prognozowania w toohello kolumny danych wyjściowych hello w lewo.

![Wdrażanie usługi sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

tootest Twojego BES kliknij **partii**. Na powitania partii testu w obszarze dane wejściowe użytkownika kliknij przycisk Przeglądaj i wybierz plik CSV zawierający przykładowe odpowiednie wartości. Jeśli nie ma pliku CSV, a utworzona predykcyjnej eksperymentu przy użyciu usługi Machine Learning Studio, można pobrać hello zestawu danych dla Twojego eksperyment predykcyjny i użyć go.

zestaw danych hello toodownload, otwórz Machine Learning Studio. Otwórz predykcyjnej eksperymentu i kliknij prawym przyciskiem myszy hello wejściowe eksperymentu. Wybierz z menu kontekstowego hello **dataset** , a następnie wybierz **Pobierz**.

![Wdrażanie usługi sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Kliknij przycisk **testu**. Stan Hello zadania wsadowe Wyświetla toohello bezpośrednio pod **zadań wsadowych testu**.

![Wdrażanie usługi sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Na powitania **konfiguracji** strony, można zmienić opisu hello, title, zaktualizuj klucz konta magazynu hello i Włącz przykładowe dane do usługi sieci web.

![Konfiguruj usługę sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Po wdrożeniu usługi sieci web hello, możesz:

* **Dostęp** ją przy użyciu interfejsu API usługi sieci web hello.
* **Zarządzanie** przy użyciu usługi Azure Machine Learning sieci web portalu usług lub hello klasycznego portalu Azure.
* **Aktualizacja** go w przypadku zmiany modelu.

#### <a name="access-your-new-web-service"></a>Dostęp do nowej usługi sieci web
Po wdrożeniu usługi sieci web z usługi Machine Learning Studio umożliwiają wysyłanie usługi toohello danych i odbierania odpowiedzi programowo.

Witaj **Consume** zawiera wszystkie informacje hello należy tooaccess usługi sieci web. Na przykład klucz interfejsu API hello podano tooallow autoryzacji dostępu toohello usługi.

Aby uzyskać więcej informacji na temat uzyskiwania dostępu do usługi sieci web uczenie maszynowe, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Zarządzanie nowej usługi sieci web
Możesz zarządzać nowego portalu usługi sieci Web usługi Machine Learning usług sieci web. Z hello [strony głównej portalu](https://services.azureml-test.net/), kliknij przycisk **usług sieci Web**. Z hello stronę usługi sieci web możesz usunąć lub skopiuj usługi. Kliknij usługę hello toomonitor określonej usługi, a następnie kliknij przycisk **pulpitu nawigacyjnego**. zadania wsadowe toomonitor skojarzonego z usługą sieci web hello, kliknij przycisk **dziennika żądania wsadowe**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Wdrażanie hello eksperyment predykcyjny jako usługę sieci web klasycznego

Teraz, eksperyment predykcyjny hello został odpowiednio przygotowany, można go wdrożyć jako usługę sieci web klasycznego Azure. Przy użyciu usługi sieci web hello, użytkownicy mogą wysyłać modelu tooyour danych i modelu hello zwróci jego prognoz.

toodeploy Twojego predykcyjnej eksperymentu, kliknij przycisk **Uruchom** u dołu hello hello eksperymentu kanwy, a następnie kliknij przycisk **wdrażanie usługi sieci Web**. Usługa sieci web Hello jest skonfigurowany i są umieszczane w pulpicie nawigacyjnym usługi sieci web hello.

![Wdrażanie usługi sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Testowanie usługi sieci web klasycznego

Usługa sieci web hello można sprawdzić w portalu usługi sieci Web usługi Machine Learning hello lub Machine Learning Studio.

Witaj tootest odpowiedzi na żądanie usługi sieci web, kliknij przycisk hello **testu** przycisku na pulpicie nawigacyjnym usługi sieci web hello. Okno dialogowe wyskakującej tooask możesz dla danych wejściowych hello hello usługi. To są kolumny hello oczekiwany przez hello oceniania eksperymentu. Wprowadź zestaw danych, a następnie kliknij przycisk **OK**. wyniki Hello generowane przez usługę sieci web hello są wyświetlane u dołu hello hello pulpitu nawigacyjnego.

Możesz kliknąć hello **testu** Podgląd tootest łącze usługi w portalu usługi sieci Web systemu Azure Machine Learning hello, jak pokazano wcześniej hello nową sekcję usługi sieci web.

Witaj tootest usługi wykonywania wsadowego, kliknij przycisk **testu** Podgląd łącza. Na powitania partii testu w obszarze dane wejściowe użytkownika kliknij przycisk Przeglądaj i wybierz plik CSV zawierający przykładowe odpowiednie wartości. Jeśli nie ma pliku CSV, a utworzona predykcyjnej eksperymentu przy użyciu usługi Machine Learning Studio, można pobrać hello zestawu danych dla Twojego eksperyment predykcyjny i użyć go.

![Usługa sieci web hello testu](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Na powitania **konfiguracji** strony, można zmienić nazwę wyświetlaną hello hello usługi i nadaj mu opis. Witaj, nazwę i opis jest wyświetlany w hello [klasycznego portalu Azure](http://manage.windowsazure.com/) gdzie zarządzania usługami sieci web.

Można podać opis dla danych wejściowych, danych wyjściowych i sieci web parametry usługi wpisując ciąg dla każdej kolumny w obszarze **schemat danych wejściowych**, **SCHEMATEM WYJŚCIOWYM**, i **PARAMETR usługi sieci Web**. Opisy te są używane w hello przykładowy kod dokumentację dla usługi sieci web hello.

Można włączyć rejestrowanie toodiagnose wszelkie błędy, które jest wyświetlane, gdy jest uzyskiwany dostęp do usługi sieci web. Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi sieci web uczenie maszynowe](machine-learning-web-services-logging.md).

![Konfiguruj usługę sieci web hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

Można również skonfigurować punkty końcowe hello usługi sieci web hello w hello usługi sieci Web systemu Azure Machine Learning portalu podobne toohello procedury przedstawionej wcześniej w hello nową sekcję usługi sieci web. Opcje Hello są różne, można dodać lub zmienić opisu usługi hello, Włącz rejestrowanie i Włącz przykładowe dane do testowania.

#### <a name="access-your-classic-web-service"></a>Dostęp do usługi sieci web klasycznego
Po wdrożeniu usługi sieci web z usługi Machine Learning Studio umożliwiają wysyłanie usługi toohello danych i odbierania odpowiedzi programowo.

pulpit nawigacyjny Hello zawiera wszystkie informacje hello potrzebne tooaccess usługi sieci web. Na przykład klucz interfejsu API hello jest tooallow uprawnień dostępu do usługi toohello i interfejsu API stron Pomocy znajdują się toohelp, które możesz rozpocząć pisanie kodu.

Aby uzyskać więcej informacji na temat uzyskiwania dostępu do usługi sieci web uczenie maszynowe, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Zarządzanie usługą sieci web klasycznego
Istnieją różne akcje można wykonać toomonitor usługi sieci web. Można ją aktualizować i usuń go. Usługa sieci web klasycznego tooa dodatkowe punkty końcowe można również dodać w dodanie toohello punktu końcowego, który jest tworzony podczas jego wdrażania.

Aby uzyskać więcej informacji, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md) i [zarządzania usługi sieci web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Usługi sieci web hello aktualizacji
Można wprowadzić zmiany tooyour usługi sieci web, takich jak aktualizowanie hello model z danymi dodatkowe szkolenie i wdrażać ją ponownie, zastępowanie hello oryginalnego usługi sieci web.

usługi sieci web hello tooupdate, otwórz hello oryginalnego eksperyment predykcyjny używana usługa sieci web hello toodeploy i wykonanie kopii można edytować, klikając **SAVE AS**. Wprowadź zmiany, a następnie kliknij przycisk **wdrażanie usługi sieci Web**.

Wdrożeniu tego eksperymentu przed, zostanie wyświetlona prośba się, jeśli chcesz toooverwrite (usługa sieci Web klasycznego) lub istniejąca usługa hello aktualizacji (nową usługę sieci web). Kliknięcie przycisku **tak** lub **aktualizacji** zatrzymuje hello istniejącej usługi sieci web i wdraża nowy eksperyment predykcyjny hello jest wdrażana w tym miejscu.

> [!NOTE]
> Jeśli wprowadzono zmiany w konfiguracji hello oryginalnego usługi sieci web, na przykład wprowadzania nową nazwę wyświetlaną i opis, konieczne będzie tooenter tych wartości ponownie.
> 
> 

Jedną z opcji aktualizowania usługi sieci web jest tooretrain hello modelu programowo. Aby uzyskać więcej informacji, zobacz temat [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md) (Ponowne trenowanie modeli uczenia maszynowego programowo).

<!-- internal links -->
[Tworzenie eksperymentu uczenia]: #create-a-training-experiment
[Przekonwertuj go eksperyment predykcyjny tooa]: #convert-the-training-experiment-to-a-predictive-experiment
[Go wdrożyć jako usługę sieci web]: #deploy-it-as-a-web-service
[nowe]: #deploy-the-predictive-experiment-as-a-new-Web-service
[klasycznego]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
