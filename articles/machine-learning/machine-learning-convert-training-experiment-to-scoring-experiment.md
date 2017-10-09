---
title: "aaaHow tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "W jaki sposób tooprepare uczonego modelu do wdrożenia jako sieci web usługi za pomocą konwersji do szkolenia Machine Learning Studio eksperymentu eksperyment predykcyjny tooa."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio

Azure Machine Learning Studio udostępnia hello narzędzia należy toodevelop modelu analizy predykcyjnej i operacjonalizacji go przez wdrożenie jej jako usługi sieci web platformy Azure.

toodo, użyj toocreate Studio eksperymentu - o nazwie *eksperyment uczenia* — której uczenia, wynik, a następnie edytować model. Po zakończeniu, Pobierz toodeploy gotowy z modelu poprzez konwersję z tooa eksperymentu uczenia *eksperyment predykcyjny* który skonfigurowany tooscore danych użytkownika.

Można zobaczyć przykład tego procesu w [wskazówki: tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

Ten artykuł przedstawia nowości hello uzyskać szczegółowe informacje, jak eksperyment uczenia zostaje przekształcona na eksperyment predykcyjny i wdrażanie tego eksperyment predykcyjny. Zrozumienie tych informacji, aby dowiedzieć się jak tooconfigure toomake Twojego wdrożonym modelu go bardziej skuteczne.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Omówienie 

Hello proces konwersji szkolenia eksperyment predykcyjny tooa eksperyment obejmuje trzy kroki:

1. Zastąp maszyny hello uczenia algorytm modułów z trenowanego modelu.
2. Przytnij hello eksperymentu tooonly moduły, które są potrzebne w przypadku oceniania. Eksperyment uczenia zawiera szereg modułów, które są niezbędne do szkolenia, ale nie są wymagane, gdy jest uczony hello model.
3. Zdefiniuj sposób modelu będzie akceptować dane użytkownika usługi sieci web hello i jakie dane zostaną zwrócone.

> [!TIP]
> W eksperymencie szkolenia już został związanych z szkolenia i oceniania modelu za pomocą własnych danych. Jednak po wdrożeniu użytkownicy będą wysyłać nowy model tooyour danych i zwróci wyniki prognozowania. Tak jak przekonwertować z eksperymentu uczenia tooa tooget eksperyment predykcyjny go gotowe do wdrożenia, należy pamiętać, jak hello model będzie używany przez inne osoby.
> 
> 

## <a name="set-up-web-service-button"></a>Przycisk Ustaw usługi sieci Web
Po uruchomieniu eksperymentu (kliknij **Uruchom** u dołu hello kanwy eksperymentu hello), kliknij hello **ustawić usługę sieci Web** przycisk (Wybierz hello **predykcyjnej usługi sieci Web** Opcja). **Ustaw usługę sieci Web** wykonuje dla hello trzy kroki konwersji eksperymentu predykcyjnej tooa eksperymentu uczenia:

1. Zapisuje uczonego modelu w hello **przeszkolone modele** części palety modułów hello (toohello lewej strony obszaru roboczego eksperymentu hello). Następnie zastępuje algorytmu uczenia maszynowego hello i [Train Model] [ train-model] modułów z hello zapisane uczenia modelu.
2. Analizuje eksperymentu, a usuwa modułów, które zostały wyraźnie używana tylko w przypadku szkolenia i nie są już potrzebne.
3. Wstawia _sieci Web dane wejściowe usługi_ i _dane wyjściowe_ moduły do domyślnej lokalizacji w eksperymencie (zaakceptować te moduły i zwrócić dane użytkownika).

Na przykład następujące hello eksperymentu pociągu decyzji boosted dwuklasowych drzewa modelu przy użyciu przykładowych danych spisu:

![Eksperyment uczenia][figure1]

Moduły Hello w tym eksperymencie wykonywać zasadniczo cztery różne funkcje:

![Moduł funkcji][figure2]

Po przekonwertowaniu tego szkolenia eksperymentu tooa eksperyment predykcyjny niektóre z tych modułów nie są już potrzebne, lub ich teraz służą do różnych celów:

* **Dane** -hello danych w tym przykładowego zestawu danych nie jest używany podczas oceniania — hello użytkownika usługi sieci web hello będzie dostarczać toobe danych hello oceniane. Jednak hello metadane z tego zestawu danych, takich jak typy danych jest używany przez hello trenowanego modelu. Dlatego należy tookeep hello dataset w eksperyment predykcyjny hello, dzięki czemu umożliwia ona metadanych.

* **Przedprodukcyjnym** — w zależności od hello danych użytkownika, które zostaną przesłane do oceniania, te moduły mogą lub nie jest konieczne tooprocess hello przychodzących danych. Witaj **ustawić usługę sieci Web** przycisku nie touch te — należy toodecide sposób toohandle je.
  
    Na przykład, w tym przykładzie hello przykładowego zestawu danych może mieć brakujące wartości, więc [Clean Missing Data] [ clean-missing-data] moduł został uwzględniony toodeal z nimi. Ponadto hello przykładowego zestawu danych zawiera kolumny, które nie są wymagane tootrain hello modelu. Dlatego [Select Columns in Dataset] [ select-columns] moduł został uwzględniony tooexclude te dodatkowe kolumny z hello przepływu danych. Jeśli znasz danych hello przesłania przez oceniania za pośrednictwem hello usługi sieci web nie ma brakujących wartości, a następnie można usunąć hello [Clean Missing Data] [ clean-missing-data] modułu. Jednak ponieważ hello [Select Columns in Dataset] [ select-columns] pomaga modułu definiowania hello kolumn danych uczonego modelu hello oczekuje, tooremain wymaga tego modułu.

* **Train** — te moduły są używane tootrain hello modelu. Po kliknięciu **ustawić usługę sieci Web**, te moduły są zamieniane na jeden moduł, który zawiera model hello szkolenia. Ten nowy moduł jest zapisywany w hello **przeszkolone modele** części palety modułów hello.

* **Wynik** — w tym przykładzie hello [podziału danych] [ split] modułu jest strumienia danych hello toodivide używane w danych testowych i danych szkoleniowych. W eksperyment predykcyjny hello, firma Microsoft nie uczony, dlatego [podziału danych] [ split] mogą zostać usunięte. Podobnie, hello drugi [Score Model] [ score-model] modułu i hello [Evaluate Model] [ evaluate-model] modułu są używane toocompare wyniki z testów hello dane, dzięki czemu te moduły nie są potrzebne w hello predykcyjnej eksperymentu. pozostały Hello [Score Model] [ score-model] modułu, jest jednak wymagana tooreturn wynik wynik za pośrednictwem usługi sieci web hello.

Oto, jak naszym przykładzie wygląda po kliknięciu przycisku **ustawić usługę sieci Web**:

![Przekonwertować eksperyment predykcyjny][figure3]

Witaj pracy przez **ustawić usługę sieci Web** może być wystarczające tooprepare Twojego toobe eksperymentu wdrożyć jako usługę sieci web. Jednak możesz toodo niektórych eksperymentu tooyour określonych dodatkowych działań.

### <a name="adjust-input-and-output-modules"></a>Dostosuj wejściowymi i wyjściowymi modułów
W eksperymencie szkolenia używany zestaw danych szkoleniowych i następnie czy niektóre tooget przetwarzania hello dane w postaci hello algorytmu uczenia maszynowego potrzebne. Jeśli oczekujesz tooreceive za pośrednictwem usługi sieci web hello danych hello nie będzie to przetwarzanie, można pominąć go: Połącz dane wyjściowe hello hello **wejściowych modułu usługi sieci Web** tooa innego modułu w eksperymencie. dane użytkownika Hello pojawią się teraz w modelu hello w tej lokalizacji.

Na przykład domyślnie **ustawić usługę sieci Web** hello naraża **sieci Web dane wejściowe usługi** modułu u góry hello przepływu danych, jak pokazano na rysunku hello powyżej. Ale możemy ręcznie pozycji hello **sieci Web dane wejściowe usługi** poza modułów danych przetwarzania hello:

![Przenoszenie danych wejściowych usługi sieci web hello][figure4]

dane wejściowe Hello, pod warunkiem za pośrednictwem hello usługi sieci web zostanie teraz przekazać bezpośrednio do modułu Score Model hello bez żadnych przetwarzania wstępnego.

Podobnie, domyślnie **ustawić usługę sieci Web** naraża hello modułu wyjście usługi sieci Web u dołu hello. Twoje przepływu danych. W tym przykładzie Usługa sieci web hello zwróci toohello użytkownika hello dane wyjściowe hello [Score Model] [ score-model] moduł, który zawiera hello wektor zakończenie danych wejściowych oraz hello oceniania wyników.
Jednak jeśli chcesz użyć tooreturn coś innego, następnie można dodać dodatkowe moduły przed hello **sieci Web usług** modułu. 

Na przykład dodać tylko wyników oceniania tooreturn hello i hello całego wektor danych wejściowych, [Select Columns in Dataset] [ select-columns] tooexclude modułu wszystkich kolumn z wyjątkiem hello oceniania wyników. Następnie przenieś hello **sieci Web usług** dane wyjściowe toohello modułu hello [Select Columns in Dataset] [ select-columns] modułu. Witaj eksperymentu wygląda następująco:

![Przenoszenie danych wyjściowych usługi sieci web hello][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Dodawanie lub usuwanie modułów dodatkowego przetwarzania danych
Jeśli istnieje więcej modułów w eksperymencie wiadomo, że nie będą potrzebne podczas oceniania, można usunąć je. Na przykład ponieważ przenieśliśmy hello **sieci Web dane wejściowe usługi** tooa modułu punktu po hello przetwarzania modułów danych, można usunąć hello [Clean Missing Data] [ clean-missing-data] modułu na podstawie eksperyment predykcyjny Hello.

Nasze eksperyment predykcyjny teraz wygląda następująco:

![Usuwanie dodatkowych modułów][figure6]


### <a name="add-optional-web-service-parameters"></a>Dodaj opcjonalne parametry usługi sieci Web
W niektórych przypadkach może być tooallow hello użytkownika sieci web usługi toochange hello zachowania modułów podczas uzyskiwania dostępu do usługi hello. *Parametry usługi sieci Web* pozwalają toodo to.

Typowym przykładem jest konfigurowanie [i zaimportuj dane] [ import-data] modułu, dlatego użytkownik hello hello wdrożyć usługi sieci web można określić innego źródła danych podczas uzyskiwania dostępu do usługi sieci web hello. Lub konfigurowania [eksportowanie danych] [ export-data] modułu, dzięki czemu można określić inną lokalizację docelową.

Można zdefiniować parametry usługi sieci Web i skojarz je z jednego lub więcej parametrów modułu i czy są one wymagane lub opcjonalne. Użytkownik Hello hello usługi sieci web zawiera wartości tych parametrów podczas uzyskiwania dostępu do usługi hello i hello modułu akcje są modyfikowane w związku z tym.

Więcej informacji na temat jakie parametry usługi sieci Web są i toouse, zobacz temat [przy użyciu parametry usługi sieci Web Azure Machine Learning][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Wdrażanie hello eksperyment predykcyjny jako usługę sieci web
Teraz, eksperyment predykcyjny hello został odpowiednio przygotowany, można go wdrożyć jako usługę sieci web platformy Azure. Przy użyciu usługi sieci web hello, użytkownicy mogą wysyłać modelu tooyour danych i modelu hello zwróci jego prognoz.

Aby uzyskać więcej informacji na proces wdrażania pełną hello, zobacz [wdrażanie usługi sieci web Azure Machine Learning][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
