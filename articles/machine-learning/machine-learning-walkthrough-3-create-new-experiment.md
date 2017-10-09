---
title: 'Krok 3: Tworzenie nowego eksperymentu uczenia maszynowego | Dokumentacja firmy Microsoft'
description: "Krok 3 hello opracowanie wskazówki rozwiązanie predykcyjne: Tworzenie nowego eksperymentu uczenia w usłudze Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Przewodnik, krok 3. Tworzenie nowego eksperymentu usługi Azure Machine Learning
To hello trzeci krok wskazówki hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. **Tworzenie nowego eksperymentu**
4. [Nauczanie i Ewaluacja modeli hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Wdrażanie usługi sieci Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Witaj dostępu do usługi sieci Web](machine-learning-walkthrough-6-access-web-service.md)

- - -
następnym krokiem Hello w ramach tego przewodnika jest toocreate eksperymentu w usłudze Machine Learning Studio używającej hello zestawu danych, które możemy przekazać.  

1. W Studio, kliknij przycisk **+ nowy** u dołu okna hello hello.
2. Wybierz **EKSPERYMENTU**, a następnie wybierz pozycję "Pusty eksperyment". 

    ![Tworzenie nowego eksperymentu][0]

2. Wybierz hello domyślna nazwa u góry hello hello kanwy eksperymentu i zmień jego nazwę toosomething łatwy do rozpoznania.

    ![Zmień nazwę eksperymentu][5]
   
   > [!TIP]
   > Toofill dobrym rozwiązaniem jest **Podsumowanie** i **opis** do eksperymentu hello w hello **właściwości** okienka. Przyznanie tych właściwości hello szansy toodocument hello eksperymentu, aby każdy, kto analizuje go później będzie zrozumiałe, cele i metodologii.
   > 
   > ![Właściwości eksperymentu][6]
   > 
3. W hello modułu palety toohello lewej strony obszaru roboczego eksperymentu hello, rozwiń węzeł **zapisane zestawów danych**.
4. Znajdź hello dataset utworzono w obszarze **Moje zestawów danych** i przeciągnij go na powitania kanwy. Możesz również znaleźć hello zestawu danych, wprowadzając nazwę hello w hello **wyszukiwania** pole powyżej hello palety.  

    ![Dodaj hello dataset toohello eksperymentu][7]

## <a name="prepare-hello-data"></a>Przygotowanie danych hello
Możesz wyświetlić hello pierwszych 100 wierszy danych hello i niektóre informacje statystyczne dla całego zestawu danych hello: kliknij port wyjściowy hello hello DataSet (hello małe kółko u dołu hello) i wybierz **Visualize**.  

Ponieważ hello plik danych nie został dostarczony z nagłówków kolumn, Studio udostępnił ogólnego nagłówki (Col1, Col2, *itp.*). Dobrym nagłówki nie są istotne toocreating modelu, ale ich stał się łatwiejsze toowork z danymi hello w eksperymencie hello. Gdy firma Microsoft ostatecznie opublikować ten model usługi sieci web, nagłówki hello pomóc w identyfikacji użytkownika toohello kolumn hello hello usługi.  

Można dodać nagłówków kolumn za pomocą hello [edytowanie metadanych] [ edit-metadata] modułu.
Użyj hello [edytowanie metadanych] [ edit-metadata] modułu toochange metadane skojarzone z zestawu danych. W takim przypadku stosujemy go tooprovide więcej przyjazne nazwy dla nagłówków kolumn. 

toouse [edytowanie metadanych][edit-metadata], należy najpierw określić które toomodify kolumn (w tym przypadku wszystkie z nich.) Następnie określ hello toobe działania wykonywane na podstawie tych kolumn (w tym przypadku zmiana nagłówków kolumn.)

1. W palecie modułów hello, wpisz "metadanych" w hello **wyszukiwania** pole. Witaj [edytowanie metadanych] [ edit-metadata] jest widoczna na liście modułu hello.

2. Kliknij i przeciągnij hello [edytowanie metadanych] [ edit-metadata] modułu na powitania obszaru roboczego i upuść ją poniżej dataset hello dodane wcześniej.

3. Połącz hello dataset toohello [edytowanie metadanych][edit-metadata]: kliknij port wyjściowy hello hello DataSet (hello małe kółko u dołu hello hello zestawu danych), przeciągnij toohello port wejściowy z [edytowanie metadanych ] [ edit-metadata] (hello małe koło u góry hello modułu hello), następnie zwolnij przycisk myszy hello. nawet w przypadku przenoszenia jednej na kanwie hello Hello zestawu danych i modułu pozostały połączone.
   
   Hello eksperyment powinien teraz wyglądać mniej więcej tak:  
   
   ![Dodawanie metadanych edycji][1]
   
   Witaj czerwony wykrzyknik wskazuje, że firma Microsoft nie zostało to jeszcze ustawiony hello właściwości dla tego modułu. Robimy tego dalej.
   
   > [!TIP]
   > Można dodać moduł tooa komentarza, klikając dwukrotnie pozycję modułu hello i wprowadzanie tekstu. Może to ułatwić jednym rzutem oka ocenić zadań jakie hello modułu w eksperymencie. W takim przypadku kliknij dwukrotnie hello [edytowanie metadanych] [ edit-metadata] moduł i wpisz hello komentarz "Dodaj nagłówki kolumn". Kliknij pole tekstowe hello tooclose kanwy hello gdziekolwiek. toodisplay hello komentarza, kliknij przycisk strzałki hello na powitania modułu.
   > 
   > ![Edytuj moduł metadanych z komentarzem dodane][8]
   > 
4. Wybierz [edytowanie metadanych][edit-metadata]w hello **właściwości** kliknij okienko toohello prawo do kanwy hello **Uruchom selektor kolumn**.

5. W hello **wybierz kolumny** okno dialogowe, wybierz wszystkie hello wierszy w **dostępne kolumny** i kliknij przycisk > toomove ich zbyt**wybrane kolumny**.
   okno dialogowe Hello powinien wyglądać następująco:

   ![Selektor kolumn z wybrano wszystkich kolumn][2]

6. Kliknij przycisk hello **OK** znacznik wyboru.

7. Po powrocie do hello **właściwości** okienka, poszukaj hello **nowych nazw kolumn** parametru. W tym miejscu wprowadź listę nazw kolumn 21 hello w zestawie danych hello, oddzielonych przecinkami i kolejność kolumn. Nazwy kolumn hello można uzyskać z hello dataset dokumentacji w witrynie sieci Web hello UCI lub dla wygody można skopiować i wkleić hello następującej listy:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   w okienku właściwości Hello wygląda następująco:
   
   ![Właściwości metadanych edycji][3]

> [!TIP]
> Nagłówki kolumn hello tooverify, należy uruchomić eksperyment hello (kliknij **Uruchom** poniżej kanwy eksperymentu hello). Po zakończeniu pracy (zielony znacznik wyboru jest wyświetlane na [edytowanie metadanych][edit-metadata]), kliknij port wyjściowy hello hello [edytowanie metadanych] [ edit-metadata] Moduł, a następnie wybierz **Visualize**. Można wyświetlić dane wyjściowe hello każdy moduł w hello sam sposób tooview hello postęp hello danych za pośrednictwem hello eksperymentu.
> 
> 

## <a name="create-training-and-test-datasets"></a>Tworzenie szkolenia i testowanie zbiory danych
Potrzebujemy niektórych danych tootrain hello modelu i niektóre tootest go.
Dlatego w hello następnego kroku hello eksperymentu, możemy podzielić hello zestawu danych na dwa oddzielne zestawy danych: jeden dla uczenie modelu, a drugi do testowania go.

toodo, używamy hello [podziału danych] [ split] modułu.  

1. Znajdź hello [podziału danych] [ split] moduł, przeciągnij je na kanwie hello i podłącz go toohello [edytowanie metadanych] [ edit-metadata] modułu.

2. Współczynnik rozdzielania hello jest domyślnie 0,5 i hello **podziału Randomized** ustawiono parametr. Oznacza, że losowe pół hello danych wyjściowych za pośrednictwem jednego portu hello [podziału danych] [ split] modułu i połowa za pomocą hello innych. Użytkownik może dostosować te parametry, a także hello **Random seed** parametru hello toochange podzielony między celów szkoleniowych i testów danych. Na przykład możemy pozostaw je jako — jest.
   
   > [!TIP]
   > Witaj właściwości **ułamek wierszy w hello najpierw wyjściowy zestaw danych** Określa, ile danych hello przekazywane za pośrednictwem hello są *po lewej stronie* output portu. Na przykład jeśli ustawisz too0.7 stosunek hello, 70% hello danych są kierowane za pośrednictwem hello lewego portu i 30% za pośrednictwem hello prawy port.  
   > 
   > 

3. Kliknij dwukrotnie hello [podziału danych] [ split] modułu i wprowadź komentarz Witaj, "dane szkoleniowe/testowania podzielić 50%". 

Możemy użyć hello elementy wyjściowe hello [podziału danych] [ split] modułu jednak firma Microsoft, takich jak, ale ta funkcja pozwala wybrać toouse hello po lewej stronie dane wyjściowe jako dane szkoleniowe i hello prawo testowania jako dane wyjściowe.  

Jak wspomniano w hello [poprzedniego kroku](machine-learning-walkthrough-2-upload-data.md), misclassifying ryzyko kredytowe wysokiej jako niski koszt hello jest pięć razy wyższa niż koszt hello misclassifying niskie ryzyko kredytowe jako wysoki. tooaccount tego, firma Microsoft generuje nowy zestaw danych, które odzwierciedla tej funkcji koszt. W hello nowy zestaw danych każdy przykład wysokiego ryzyka są replikowane pięć razy, gdy nie jest replikowany każdy przykład niskiego ryzyka.   

Możemy replikacja za pomocą kodu języka R:  

1. Znajdź i przeciągnij hello [wykonanie skryptu języka R] [ execute-r-script] modułu na kanwie eksperymentu hello. 

2. Połącz hello pozostałych portem wyjściowym hello [podziału danych] [ split] toohello modułu pierwsze dane wejściowe portu ("Dataset1") z hello [wykonanie skryptu języka R] [ execute-r-script] Moduł.

3. Kliknij dwukrotnie hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie wprowadź komentarz Witaj, "Ustaw korekty kosztu".

4. W hello **właściwości** okienku i Usuń hello domyślny tekst w hello **skrypt języka R** parametr, a następnie wprowadź ten skrypt:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Skrypt języka R w module wykonanie skryptu języka R hello][9]

Potrzebujemy toodo tej samej operacji replikacji dla każdego danych wyjściowych hello [podziału danych] [ split] moduł, tak że hello celów szkoleniowych i testów danych ma takie same hello Koszt korekty. Witaj najprostszym toodo sposób jest duplikując hello [wykonanie skryptu języka R] [ execute-r-script] modułu właśnie wprowadziliśmy i połączenia jej toohello innych danych wyjściowych port hello [podziału danych] [ split] modułu.

1. Kliknij prawym przyciskiem myszy hello [wykonanie skryptu języka R] [ execute-r-script] modułu, a następnie wybierz **kopiowania**.

2. Kliknij prawym przyciskiem myszy hello roboczego eksperymentu, a następnie wybierz **Wklej**.

3. Przeciągnij hello nowy moduł w określonej pozycji, a następnie połącz port wyjściowy prawo hello hello [podziału danych] [ split] toohello modułu pierwsze dane wejściowe port to nowy [wykonanie skryptu języka R] [ execute-r-script] modułu. 

4. U dołu hello hello kanwy, kliknij przycisk **Uruchom**. 

> [!TIP]
> Hello kopii modułu wykonania skryptu języka R hello zawiera hello sam skrypt jako hello oryginalnego modułu. Podczas kopiowania i wklejania modułu na kanwie hello kopiowania hello zachowuje wszystkie właściwości hello hello oryginalnego.  
> 
> 

Naszym doświadczeniu teraz wygląda następująco:

![Dodanie modułu podziału i skrypty języka R][4]

Aby uzyskać więcej informacji na używanie skryptów języka R w eksperymentów, zobacz [rozszerzanie eksperymentu z R](machine-learning-extend-your-experiment-with-r.md).

**Następnie: [pociągu i ocena hello modeli](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
