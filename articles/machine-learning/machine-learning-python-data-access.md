---
title: "zestawy danych aaaAccess z biblioteki klienta usługi Machine Learning Python | Dokumentacja firmy Microsoft"
description: "Zainstalować i używać hello Python klienta biblioteki tooaccess danych i zarządzać nimi usługi Azure Machine Learning bezpiecznie z lokalnym środowiskiem Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Zestawy danych dostęp za pomocą biblioteki klienta usługi Azure Machine Learning Python hello języka Python
Podgląd Hello biblioteki klienta usługi Microsoft Azure Machine Learning Python można włączyć bezpieczny dostęp tooyour zestawy danych usługi Azure Machine Learning z lokalnym środowiskiem Python i umożliwia tworzenie hello i Zarządzanie zestawami danych w obszarze roboczym.

Ten temat zawiera instrukcje dotyczące sposobu:

* Zainstaluj biblioteki klienta usługi Machine Learning Python hello 
* dostęp i przekazać zestawów danych, w tym instrukcje dotyczące tooget autoryzacji tooaccess zestawy danych usługi Azure Machine Learning z lokalnego środowiska Python
* dostęp do pośredniego zestawów danych z eksperymentów
* używać zestawów danych hello Python klienta biblioteki tooenumerate, uzyskuje dostęp do metadanych, odczytu zawartości hello zestawu danych, Utwórz nowy zestaw danych i zaktualizować istniejący zestaw danych

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Wymagania wstępne
Biblioteka klienta Python Hello był testowany w obszarze hello następującego środowiska:

* Windows, Mac i Linux
* Python 2.7 3.3 i 3.4

Ma ona zależność na powitania następujące pakiety:

* żądania
* dateutil języka Python
* pandas

Firma Microsoft zaleca używanie dystrybucję oprogramowania Python, takie jak [Anaconda](http://continuum.io/downloads#all) lub [korony](https://store.enthought.com/downloads/), które pochodzą z języka Python, IPython i zainstalowane pakiety hello trzech z wymienionych powyżej. Chociaż IPython nie jest ścisłym wymogiem, jest doskonałe środowisko manipulowanie i wizualizacja danych interaktywnie.

### <a name="installation"></a>Jak tooinstall hello biblioteki klienta usługi Azure Machine Learning Python
Biblioteka klienta usługi Azure Machine Learning Python Hello musi być zainstalowany toocomplete hello zadania opisane w tym temacie. Jest ona dostępna z hello [indeksu pakietów języka Python](https://pypi.python.org/pypi/azureml). tooinstall uruchom go w środowisku Python hello następujące polecenie z lokalnego środowiska Python:

    pip install azureml

Alternatywnie można pobrać i zainstalować ze źródeł hello na [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Jeśli masz git na komputerze jest zainstalowany program pip tooinstall bezpośrednio z repozytorium git hello:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Użyj zbiorów danych tooaccess wstawki kodu Studio
Biblioteka klienta Python Hello daje istniejący zestaw danych dostęp programistyczny tooyour z doświadczenia, które zostały uruchomione.

Z interfejsem sieci web Studio hello można wygenerować wstawki kodu, obejmujących wszystkie toodownload koniecznych hello oraz deserializacji zestawy danych jako obiekty Pandas DataFrame na komputerze lokalizacji.

### <a name="security"></a>Zabezpieczenia dostępu do danych
Witaj podał Studio do użycia z biblioteki klienta Python hello zawiera identyfikator i autoryzacji wstawki kodu tokenu. Te zapewniają roboczym tooyour pełny dostęp i musi być chroniony, takie jak hasła.

Ze względów bezpieczeństwa funkcja fragment kodu hello jest tylko dostępne toousers, mające ich roli Ustaw jako **właściciela** hello obszaru roboczego. Rola użytkownika jest wyświetlany w usłudze Azure Machine Learning Studio na powitania **użytkowników** w obszarze **ustawienia**.

![Bezpieczeństwo][security]

Jeśli rola użytkownika nie jest ustawiony jako **właściciela**, możesz zażądać toobe reinvited jako właściciela, lub poproś właściciela hello hello tooprovide obszaru roboczego z hello fragment kodu.

token autoryzacji hello tooobtain, możesz wybrać jedną z następujących hello:

* Prosić o token właściciela. Właściciele mogą uzyskiwać dostęp do swoich tokenów autoryzacji ze strony ustawień hello ich obszaru roboczego w Studio. Wybierz **ustawienia** z hello lewego okienka i kliknij przycisk **TOKENY autoryzacji** toosee hello tokeny podstawowego i pomocniczego.  Chociaż hello podstawowego lub tokeny dodatkowej autoryzacji hello można używać we fragmencie kodu hello, zaleca się, że właścicieli udostępniać tylko tokeny dodatkowej autoryzacji hello.

![Tokeny autoryzacji](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Poproś toorole toobe awansowane właściciela.  toodo to bieżącego właściciela hello obszaru roboczego musi toofirst należy usunąć z obszaru roboczego hello, a następnie ponownie Cię zaprosił tooit jako właściciela.

Po uzyskaniu deweloperzy autoryzacji i identyfikator obszaru roboczego hello tokenu, są one możliwe tooaccess hello roboczym przy użyciu hello fragment kodu, niezależnie od ich roli.

Tokeny autoryzacji są zarządzane na powitania **TOKENY autoryzacji** w obszarze **ustawienia**. Ponowne ich wygenerowanie, ale w tej procedurze odwołuje dostęp toohello poprzednim tokenem.

### <a name="accessingDatasets"></a>Zestawy dostępu do danych z aplikacji lokalnej Python
1. W usłudze Machine Learning Studio, kliknij przycisk **zestawów danych** hello pasku nawigacyjnym po lewej stronie powitania.
2. Wybierz zestaw danych hello chcesz tooaccess. Można wybrać dowolny hello zestawów danych z hello **Moje zestawów danych** listy lub hello **przykłady** listy.
3. Witaj dolnym pasku narzędzi kliknij **Generuj kod dostępu do danych**. Jeśli dane hello jest w formacie niezgodne z biblioteki klienta hello Python, ten przycisk jest wyłączone.
   
    ![Zestawy danych][datasets]
4. Wybierz hello fragment kodu z wyświetlonym oknie hello i skopiuj go tooyour Schowka.
   
    ![Kod dostępu][dataset-access-code]
5. Wklej kod hello do notesu hello lokalnej aplikacji Python.
   
    ![Notesu][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Dostęp do pośredniego zestawów danych z eksperymentów uczenia maszynowego
Po uruchomieniu eksperymentu w usłudze Machine Learning Studio hello jest możliwe tooaccess hello pośredniego zestawy danych z węzłów wyjściowych hello modułów. Pośredni zestawów danych są dane, które zostały utworzone i jest używany do pośredniego kroki po uruchomieniu narzędzia modelu.

Tak długo, jak hello format danych jest zgodny z biblioteki klienta Python hello pośredniego zestawów danych są dostępne.

Witaj obsługiwane są następujące formaty (stałe tych znajdują się w hello `azureml.DataTypeIds` klasy):

* W postaci zwykłego tekstu
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

Można określić formatu hello, ustawiając kursor nad węzłem danych wyjściowych modułu. Jest on wyświetlany wraz z hello nazwa węzła, w etykietce narzędzia.

Niektóre moduły hello, na przykład hello [podziału] [ split] modułu, dane wyjściowe tooa formatu o nazwie `Dataset`, który nie jest obsługiwany przez bibliotekę klienta Python hello.

![Format zestawu danych][dataset-format]

Należy toouse moduł konwersji, takich jak [przekonwertować tooCSV][convert-to-csv], tooget dane wyjściowe do obsługiwanego formatu.

![GenericCSV Format][csv-format]

Hello następujących krokach przedstawiono przykład, w którym tworzy eksperyment, uruchamia go i uzyskuje dostęp do hello pośredniego zestawu danych.

1. Tworzenie nowego eksperymentu.
2. Wstaw **zestawu danych dla dorosłych klasyfikacji binarnej dochodu spisu** modułu.
3. Wstaw [podziału] [ split] modułu i połącz dane wyjściowe toohello wejściowy zestaw danych modułu.
4. Wstaw [przekonwertować tooCSV] [ convert-to-csv] modułu i Połącz z jego wejściowych tooone hello [podziału] [ split] danych wyjściowych modułu.
5. Zapisz hello eksperymentu, uruchom go i poczekaj na jej toofinish uruchomiona.
6. Kliknij węzeł danych wyjściowych hello na powitania [przekonwertować tooCSV] [ convert-to-csv] modułu.
7. Po wyświetleniu menu kontekstowe hello zaznacz **Generuj kod dostępu do danych**.
   
    ![Menu kontekstowe][experiment]
8. Wybierz hello fragment kodu i skopiuj go tooyour Schowka z wyświetlonym oknie hello.
   
    ![Kod dostępu][intermediate-dataset-access-code]
9. Wklej kod hello w Notatniku.
   
    ![Notesu][ipython-intermediate-dataset]
10. Można zwizualizować hello danych przy użyciu matplotlib. Spowoduje to wyświetlenie w histogram hello wieku kolumny:
    
    ![Histogram][ipython-histogram]

## <a name="clientApis"></a>Użyj hello tooaccess biblioteki klienta Machine Learning Python, odczytu, tworzenie i zarządzanie nimi zbiory danych
### <a name="workspace"></a>Obszar roboczy
obszar roboczy Hello jest punkt wejścia hello hello Python klienta biblioteki. Podaj hello `Workspace` klasy z z obszaru roboczego toocreate połączeń tokenu identyfikator i autoryzacji wystąpienie:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Wyliczanie obiektów DataSet
tooenumerate wszystkie zestawy danych danego obszaru roboczego:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate hello właśnie utworzone przez użytkownika zestawów danych:

    for ds in ws.user_datasets:
        print(ds.name)

przykład Witaj tylko tooenumerate zestawów danych:

    for ds in ws.example_datasets:
        print(ds.name)

Aby dostęp do zestawu danych, według nazwy (która jest uwzględniana wielkość liter):

    ds = ws.datasets['my dataset name']

Lub zostanie do niego dostęp przez indeks:

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadane
Zestaw danych ma metadanych, w toocontent dodanie. (Zestaw pośrednich danych są reguły toothis wyjątku i nie ma żadnych metadanych).

Niektóre wartości metadanych są przypisane przez użytkownika hello w czasie tworzenia:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Inne są wartości przypisane przez uczenie Maszynowe Azure:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Zobacz hello `SourceDataset` klasy więcej w metadanych dostępnych hello.

### <a name="read-contents"></a>Odczytaj zawartość
wstawki kodu Hello udostępniane przez usługi Machine Learning Studio automatycznie Pobierz i deserializacji obiektu Pandas DataFrame tooa dataset hello. Jest to zrobić za pomocą hello `to_dataframe` metody:

    frame = ds.to_dataframe()

Jeśli preferowane toodownload hello nieprzetworzone dane i samodzielnie przeprowadzić deserializacji hello, który jest opcją. W momencie hello jest tylko opcja hello formatów, takich jak "ARFF", które biblioteki klienta Python hello nie można wykonać deserializacji.

zawartość hello tooread jako tekst:

    text_data = ds.read_as_text()

zawartość hello tooread jako wartość binarną:

    binary_data = ds.read_as_binary()

Możesz także po prostu otworzyć zawartość toohello strumienia:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Utwórz nowy zestaw danych
Biblioteka klienta Python Hello umożliwia zestawów tooupload danych z programu Python. Te zestawy danych będą dostępne do użycia w obszarze roboczym.

Jeśli dane znajdują się w Pandas DataFrame, użyj hello następującego kodu:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Jeśli dane są już serializowane, możesz użyć:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Witaj Python jest biblioteka klienta stanie tooserialize następujące toohello Pandas DataFrame formatuje (stałe tych znajdują się w hello `azureml.DataTypeIds` klasy):

* W postaci zwykłego tekstu
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Aktualizuj istniejący zestaw danych
Jeśli spróbujesz tooupload nowy zestaw danych o nazwie, która odpowiada istniejący zestaw danych, należy pobrać błąd konfliktu.

tooupdate istniejący zestaw danych, należy najpierw tooget toohello istniejący zestaw danych odwołania:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Następnie użyj `update_from_dataframe` tooserialize i Zastąp zawartość hello dataset hello Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Tooserialize hello danych tooa innym formacie należy określić wartość dla hello opcjonalne `data_type_id` parametru.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Opcjonalnie możesz ustawić nowy opis, określając wartość hello `description` parametru.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Opcjonalnie możesz ustawić nową nazwę, określając wartość hello `name` parametru. Od teraz będziesz pobrać hello zestawu danych za pomocą hello tylko nową nazwę. Witaj następującego kodu aktualizuje hello danych, nazwę i opis.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Witaj `data_type_id`, `name` i `description` parametry są opcjonalne i domyślne tootheir poprzedniej wartości. Witaj `dataframe` parametru jest zawsze wymagane.

Jeśli dane są już serializowane, użyj `update_from_raw_data` zamiast `update_from_dataframe`. Jeśli po prostu Przekaż w `raw_data` zamiast `dataframe`, działa w podobny sposób.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

