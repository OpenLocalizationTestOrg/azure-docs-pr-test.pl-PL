---
title: "Krok 5: Wdrażanie usługi sieci web uczenie maszynowe hello | Dokumentacja firmy Microsoft"
description: "Krok 5 hello opracowanie wskazówki rozwiązanie predykcyjne: Wdrażanie eksperyment predykcyjny w usłudze Machine Learning Studio jako usługę sieci web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello
Jest hello krok piątym powitania przewodnika, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Nauczanie i Ewaluacja modeli hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Wdrażanie usługi sieci web hello**
6. [Usługa sieci web hello dostępu](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive innych toouse szansy hello model predykcyjny opracowaliśmy w ramach tego przewodnika, możemy wdrożyć go jako usługę sieci web na platformie Azure.

Zapasowej punktu toothis możemy były zmieniane uczenie modelu. Ale hello wdrożona usługa ma już szkolenia toodo — będzie prognoz nowe toogenerate przez oceniania danych wejściowych użytkownika hello oparte na modelu. Dlatego chcemy toodo niektórych tooconvert przygotowania, to eksperymentować z ***szkolenia*** eksperymentu tooa ***predykcyjnej*** eksperymentu. 

Jest to proces trzech etapów:  

1. Usuń jeden z modeli hello
2. Konwertuj hello *eksperyment uczenia* utworzyliśmy do *eksperyment predykcyjny*
3. Wdrażanie hello eksperyment predykcyjny jako usługę sieci web

## <a name="remove-one-of-hello-models"></a>Usuń jeden z modeli hello

Najpierw należy tootrim tego eksperymentu w dół nieco. Obecnie istnieją dwa różne modele w eksperymencie hello, ale będą tylko jeden model toouse podczas możemy wdrożyć ją jako usługę sieci web.  

Załóżmy, że firma Microsoft decydujesz się tym hello boosted drzewa model działa lepiej niż hello SVM modelu. Dlatego hello pierwszy element toodo hello Usuń [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu i hello modułów, które były używane na potrzeby uczenia go. Może być toomake kopię eksperymentu hello najpierw klikając **Zapisz jako** u dołu hello hello eksperymentu kanwy.

Potrzebujemy hello toodelete następujących modułów:  

* [Obsługa Two-Class wektor maszyny][two-class-support-vector-machine]
* [Uczenie modelu] [ train-model] i [Score Model] [ score-model] modułów, które zostały połączone tooit
* [Normalizuj danych] [ normalize-data] (oba)
* [Ocena modelu] [ evaluate-model] (ponieważ jesteśmy zakończono ocenę modeli hello)

Wybierz każdego modułu i naciśnij klawisz Delete hello lub moduł powitania kliknij prawym przyciskiem myszy i wybierz **usunąć**. 

![Usunięte hello SVM modelu][3a]

Nasz model powinien teraz wyglądać mniej więcej tak:

![Usunięte hello SVM modelu][3]

Teraz jest gotowy toodeploy model to przy użyciu hello [Two-Class Boosted drzewa decyzyjnego][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Konwertuj eksperyment predykcyjny tooa hello szkolenia eksperymentu

tooget to modelu gotowe do wdrożenia, potrzebujemy tooconvert to szkolenia eksperyment predykcyjny tooa eksperymentu. Obejmuje to trzy kroki:

1. Zapisz model hello możemy gdy udało się nauczyć, a następnie zastąp naszych modułów szkoleniowych
2. TRIM hello eksperymentu tooremove modułów, które były potrzebne tylko w przypadku szkolenia
3. Zdefiniuj gdzie hello usługi sieci web będzie akceptować dane wejściowe i gdzie generuje dane wyjściowe hello

Firma Microsoft może to zrobić ręcznie, ale na szczęście wszystkie trzy kroki można wykonać, klikając **ustawić usługę sieci Web** u dołu hello kanwy eksperymentu hello (i wybierając hello **predykcyjnej usługi sieci Web** Opcja).

> [!TIP]
> Jeśli chcesz bardziej szczegółowe informacje na, co się stanie po przekonwertowaniu tooa eksperymentu uczenia predykcyjnej eksperymentu, zobacz [jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Po kliknięciu **ustawić usługę sieci Web**, ma miejsce kilka rzeczy:

* Hello uczonego modelu jest przekonwertowanego tooa pojedynczego **Uczonego modelu** modułu i przechowywane w toohello palety modułu hello lewej hello kanwy eksperymentu (można znaleźć go w **przeszkolone modele**)
* Moduły, które były używane do trenowania zostaną usunięte; w szczególności:
  * [Two-Class Boosted algorytm][two-class-boosted-decision-tree]
  * [Train Model][train-model]
  * [Podział danych][split]
  * Witaj drugi [wykonanie skryptu języka R] [ execute-r-script] moduł, który był używany dla danych testowych
* Hello zapisane uczonego modelu zostanie dodany do eksperymentu hello
* **Usługi danych wejściowych w sieci Web** i **sieci Web usług** moduły są dodawane (te informacje pozwalają określić gdzie wprowadzić dane użytkownika hello hello modelu i jakie dane są zwracane podczas uzyskiwania dostępu do usługi sieci web hello)

> [!NOTE]
> Widać, że hello eksperyment został zapisany w dwóch częściach na kartach dodanych u góry hello kanwy eksperymentu hello. Witaj oryginalnego eksperyment uczenia jest karcie hello **eksperyment uczenia**, i podlega hello nowo utworzony eksperyment predykcyjny **eksperyment predykcyjny**. eksperyment predykcyjny Hello jest hello jedną, które firma Microsoft będzie wdrożyć jako usługę sieci web.

Potrzebujemy tootake jednego dodatkowego kroku z tego konkretnego eksperymentu.
Dodaliśmy dwie [wykonanie skryptu języka R] [ execute-r-script] tooprovide modułów wagi funkcji toohello danych. Po prostu lewy, czego potrzeba do uczenie i testowanie, który został, firma Microsoft może zająć się tych modułów w hello ostatecznego modelu.
Usługa Machine Learning Studio usunąć jedną [wykonanie skryptu języka R] [ execute-r-script] modułu usunięcie hello [podziału] [ split] modułu. Teraz można usunąć hello innych i połącz [Edytor metadanych] [ metadata-editor] bezpośrednio za[Score Model][score-model].    

Naszym doświadczeniu powinna wyglądać następująco:  

![Oceniania hello trenowanego modelu.][4]  

> [!NOTE]
> Możesz się zastanawiać, dlaczego możemy left hello danych karty kredytowej niemiecki UCI dataset w eksperyment predykcyjny hello. Usługa Hello przechodzi tooscore hello danych użytkownika, nie hello oryginalnego zestawu danych, więc Dlaczego pozostaw hello oryginalnego zestawu danych w modelu hello?
> 
> Jest PRAWDA, nie wymagają hello oryginalnych danych karty kredytowej hello usługi. Jednak musi hello schematu dla danych, które obejmują takie informacje jak liczbę kolumn są i kolumny, które są liczbowych. Informacje o schemacie jest konieczne toointerpret hello danych użytkownika. Firma Microsoft pozostawić te składniki, połączony, dzięki czemu hello oceniania moduł ma hello schemat zestawu danych podczas hello usługa jest uruchomiona. Witaj danych nie jest używana, tylko hello schematu.  
> 
> 

Uruchom eksperyment hello raz ostatni (kliknij **Uruchom**.) Nadal działa tooverify, który hello modelu, kliknij przycisk dane wyjściowe hello hello [Score Model] [ score-model] moduł i zaznacz **wyświetlanie wyników**. Widać, że oryginalne dane hello zostanie wyświetlona, wraz z hello środki ryzyka wartość ("oceniane etykiety") i hello oceniania wartość prawdopodobieństwa ("wynik prawdopodobieństwa".) 

## <a name="deploy-hello-web-service"></a>Wdrażanie usługi sieci web hello
Hello eksperymentu można wdrożyć jako albo klasycznym usługi sieci web, lub Nowa usługa sieci web, która jest oparta na usłudze Azure Resource Manager.

### <a name="deploy-as-a-classic-web-service"></a>Wdrożyć jako usługę sieci web klasycznego
Kliknij toodeploy pochodzące z naszych eksperymentu usługi sieci web Klasyczny **wdrażanie usługi sieci Web** poniżej hello obszar roboczy i wybierz **wdrażanie usługi sieci Web [klasyczny]**. Usługa Machine Learning Studio wdraża hello eksperymentu jako usługę sieci web i przejście pulpitu nawigacyjnego toohello dla tej usługi sieci web. Na tej stronie można zwrócić eksperymentu toohello (**widoku migawki** lub **wyświetlić najnowszych**) i uruchamianie testu prostego powitania usługi sieci web (zobacz **testowanie usługi sieci web hello** poniżej). Istnieje również tutaj informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web hello (omówiona w następnym kroku hello tego przewodnika).

![Pulpit nawigacyjny usługi sieci Web][6]

Można skonfigurować usługę hello klikając hello **konfiguracji** kartę. W tym miejscu można zmodyfikować hello nazwy usługi (jest nazwę eksperymentu danego hello domyślnie) i nadaj mu opis. Możesz też udzielić większej liczby etykiet przyjazną dla hello danych wejściowych i wyjściowych.  

![Konfiguruj usługę sieci web hello][5]  

### <a name="deploy-as-a-new-web-service"></a>Wdrożyć jako nową usługę sieci web

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji, które wdrażasz hello usługi sieci web. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy nową usługę sieci web pochodzące z naszym doświadczeniu:

1. Kliknij przycisk **wdrażanie usługi sieci Web** poniżej hello obszar roboczy i wybierz **wdrażanie usługi sieci Web [New]**. Usługa Machine Learning Studio transfery usługi sieci web Azure Machine Learning toohello **wdrażanie eksperymentu** strony.

2. Wprowadź nazwę usługi sieci web hello. 

3. Aby uzyskać **planu cen**, można wybrać planu cenowego istniejących lub wybierz opcję "Utwórz nowe" i podać hello nowego planu nazwę i wybierz hello miesięczne opcji plan. plan Hello się, że warstw domyślne plany toohello Twojego domyślnego regionu i usługi sieci web jest wdrożone toothat regionu.

4. Kliknij przycisk **wdrażanie**.

Po kilku minutach hello **szybkiego startu** zostanie otwarta strona dla usługi sieci web.

Można skonfigurować usługę hello klikając hello **Konfiguruj** kartę. W tym miejscu można zmodyfikować usługi hello tytuł i nadaj mu opis. 

tootest hello usługi sieci web, kliknij przycisk hello **testu** kartę (zobacz **testowanie usługi sieci web hello** poniżej). Informacje dotyczące tworzenia aplikacji, które mogą uzyskiwać dostęp do usługi sieci web hello, kliknij przycisk hello **Consume** kartę (hello następnego kroku w tym przewodniku zostaną umieszczone w bardziej szczegółowo).

> [!TIP]
> Po jej wdrożeniu można aktualizować hello usługi sieci web. Na przykład, jeśli chcesz toochange modelu, następnie należy można edytować eksperyment uczenia hello, dostosować parametry modelu hello i kliknij przycisk **wdrażanie usługi sieci Web**, wybierając żądane **wdrażanie usługi sieci Web [klasyczny]** lub  **Wdrażanie usługi sieci Web [New]**. Wdrażając hello eksperyment ponownie, zastępuje hello usługi sieci web, teraz, używając zaktualizowanych modelu.  
> 
> 

## <a name="test-hello-web-service"></a>Usługa sieci web hello testu

Podczas uzyskiwania dostępu do usługi sieci web hello dane użytkownika hello przechodzi przez hello **sieci Web dane wejściowe usługi** modułu, w którym przekazany toohello [Score Model] [ score-model] modułu i oceniane. sposób Hello skonfigurowaliśmy eksperyment predykcyjny hello, hello model oczekuje danych w hello takie same w formacie zestawu danych hello oryginalnego środki ryzyka.
Hello są zwracane wyniki toohello użytkownika z hello usługi sieci web za pośrednictwem hello **sieci Web usług** modułu.

> [!TIP]
> sposób Hello mamy hello eksperyment predykcyjny skonfigurowane, hello całego wynikiem hello [Score Model] [ score-model] modułu są zwracane. W tym wszystkich danych wejściowych hello oraz wartość ryzyko kredytowe hello i hello oceniania prawdopodobieństwa. Ale może inny zwracać — na przykład można zwrócić tylko hello wartość ryzyko kredytowe. toodo, Wstaw [kolumny projektu] [ project-columns] modułu między [Score Model] [ score-model] i hello **sieci Web produktu** nie ma kolumn tooeliminate hello tooreturn usługi sieci web. 
> 
> 

Można przetestować web klasycznym usługi w **Machine Learning Studio** lub hello **usługi sieci Web systemu Azure Machine Learning** portalu.
Możesz przetestować nową usługę sieci web tylko w hello **usługi sieci Web usługi Machine Learning** portalu.

> [!TIP]
> Podczas testowania, w portalu usługi sieci Web systemu Azure Machine Learning hello, może mieć portalu hello Utwórz dane przykładowe służy tootest hello żądań i odpowiedzi usługi. Na powitania **Konfiguruj** wybierz przycisk Tak, aby uzyskać **przykładowych danych włączone?**. Po otwarciu karty hello żądań i odpowiedzi na powitania **testu** strony portalu hello wypełnia przykładowych danych z zestawu danych hello oryginalnego środki ryzyka.

### <a name="test-a-classic-web-service"></a>Testowanie usługi sieci web klasycznego

W usłudze Machine Learning Studio lub w portalu usługi sieci Web usługi Machine Learning hello można testować usługi sieci web klasycznego. 

#### <a name="test-in-machine-learning-studio"></a>Testowanie w usłudze Machine Learning Studio

1. Na powitania **pulpitu NAWIGACYJNEGO** usługi sieci web powitania kliknij pozycję hello **testu** przycisku w obszarze **domyślny punkt końcowy**. Okno dialogowe wyskakującej i monituje o dane wejściowe hello hello usługi. Te są hello tej samej kolumny, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka.  

2. Wprowadź zestaw danych, a następnie kliknij przycisk **OK**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Testowanie w portalu usługi sieci Web usługi Machine Learning hello

1. Na powitania **pulpitu NAWIGACYJNEGO** usługi sieci web powitania kliknij pozycję hello **Podgląd testów** łącze w obszarze **domyślny punkt końcowy**. Strona testowa Hello w portalu usługi sieci Web systemu Azure Machine Learning hello punktu końcowego usługi sieci web hello otwiera i monituje o dane wejściowe hello hello usługi. Te są hello tej samej kolumny, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka.

2. Kliknij przycisk **Test żądań i odpowiedzi**. 

### <a name="test-a-new-web-service"></a>Przetestować nową usługę sieci web

Tylko w portalu usługi sieci Web usługi Machine Learning hello można przetestować nową usługę sieci web.

1. W hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net/quickstart) portalu, kliknij przycisk **testu** u góry hello hello strony. Witaj **testu** zostanie otwarta strona i można wprowadzić dane dotyczące hello usługi. Hello pól wejściowych wyświetlane odpowiada toohello kolumn, które znajdowały się w zestawie danych hello oryginalnego środki ryzyka. 

2. Wprowadź zestaw danych, a następnie kliknij przycisk **testu żądanie-odpowiedź**.

Witaj wyniki testu hello są wyświetlane na hello prawej strony hello hello kolumny wyjściowej. 


## <a name="manage-hello-web-service"></a>Zarządzanie usługą sieci web hello

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Zarządzanie usługą sieci web klasycznego w hello klasycznego portalu Azure

Po wdrożeniu usługi sieci web klasycznego, można było zarządzać nim z hello [klasycznego portalu Azure](https://manage.windowsazure.com).

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com)
2. Witaj Panel usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**
3. Kliknij obszar roboczy
4. Kliknij przycisk hello **usług sieci Web** kartę
5. Kliknij opcję usługi sieci web hello utworzyliśmy
6. Kliknij punkt końcowy "domyślne" hello

W tym miejscu można wykonywać czynności, takie jak monitorowanie, jak robi hello usługi sieci web i upewnij ulepszeń wydajności przez zmianę liczby równoczesnych wywołań hello usługi może obsłużyć.

Aby uzyskać więcej informacji, zobacz:

* [Tworzenie punktów końcowych](machine-learning-create-endpoint.md)
* [Skalowanie usługi sieci web](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Zarządzanie Classic lub nową usługę sieci web w portalu usługi sieci Web systemu Azure Machine Learning hello

Po wdrożeniu usługi sieci web, czy klasycznego lub nowe, można było zarządzać nim z hello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu.

wydajność hello toomonitor usługi sieci web:

1. Zaloguj się toohello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portalu
2. Kliknij przycisk **usług sieci Web**
3. Kliknij opcję usługi sieci web
4. Kliknij przycisk hello **pulpitu nawigacyjnego**

- - -
**Następnie: [dostępu do usługi sieci web hello](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
