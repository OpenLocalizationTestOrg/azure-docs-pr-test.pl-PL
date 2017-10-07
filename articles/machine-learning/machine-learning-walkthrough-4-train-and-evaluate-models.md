---
title: 'Krok 4: Nauczanie i Ewaluacja modeli predykcyjnych analityczne hello | Dokumentacja firmy Microsoft'
description: "Krok 4 hello opracowanie wskazówki rozwiązanie predykcyjne: pociągu, wynik i ocena wielu modeli w usłudze Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Wskazówki krok 4: Nauczanie i Ewaluacja modeli predykcyjnych analityczne hello
Ten temat zawiera hello czwarty krok wskazówki hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Nauczanie i Ewaluacja modeli hello**
5. [Wdrażanie usługi sieci Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Witaj dostępu do usługi sieci Web](machine-learning-walkthrough-6-access-web-service.md)

- - -
Jedną z zalet hello przy użyciu usługi Azure Machine Learning Studio do tworzenia modeli uczenia maszyny jest więcej niż jeden typ modelu tootry możliwości hello jednocześnie w jednym eksperymentu i porównywania wyników hello. Ten typ eksperymenty ułatwia hello najlepszego rozwiązania dla danego problemu.

W eksperymencie hello możemy tworzony jest w tym przewodniku, firma Microsoft będzie utworzyć dwa rodzaje modeli a następnie porównaj ich oceniania toodecide wyniki który algorytm chcemy toouse w naszym końcowy eksperyment.  

Istnieją różne modele, firma Microsoft może wyboru. toosee hello modeli dostępnych, rozwiń węzeł hello **Machine Learning** węzła w palecie modułów hello, a następnie rozwiń węzeł **zainicjować modelu** i węzły hello znajdujące się poniżej. Dla celów hello tego eksperymentu, wybierzemy hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] (SVM) i hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułów.    

> [!TIP]
> tooget dodatkową pomoc przy wyborze Algorytm uczenia maszynowego, które najlepiej pasujące do konkretnych problemów hello próbujesz toosolve, zobacz [jak toochoose algorytmów uczenia maszynowego Azure Microsoft](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Modele hello pociągu

Dodamy zarówno hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu i [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu, w tym eksperymentu.

### <a name="two-class-boosted-decision-tree"></a>Two-Class Boosted algorytm

Najpierw skonfiguruj hello boosted decyzji drzewa modelu.

1. Znajdź hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu w palecie modułów hello i przeciągnij go na powitania kanwy.

2. Znajdź hello [Train Model] [ train-model] modułu, przeciągnij je na kanwie hello, a następnie połącz dane wyjściowe hello hello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree]toohello modułu pozostałych port wejściowy z hello [Train Model] [ train-model] modułu.
   
   Witaj [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] modułu inicjuje hello rodzajowy modelu i [Train Model] [ train-model] używa danych szkoleniowych tootrain hello modelu. 

3. Połącz powitania po lewej stronie dane wyjściowe lewej hello [wykonanie skryptu języka R] [ execute-r-script] portu hello danych wejściowych modułu toohello prawo [Train Model] [ train-model] modułu (Firma Microsoft decyzje podejmowane w [kroku 3](machine-learning-walkthrough-3-create-new-experiment.md) tych danych hello toouse wskazówki pochodzące z powitania po lewej stronie powitania podziału danych modułu szkoleń).
   
   > [!TIP]
   > Firma Microsoft nie ma potrzeby dwóch danych wejściowych hello i jeden hello elementy wyjściowe hello [wykonanie skryptu języka R] [ execute-r-script] modułu do tego eksperymentu, dlatego firma Microsoft może narazić je odłączyć. 
   > 
   > 

Ta część eksperymentu hello teraz wygląda następująco:  

![Uczenie modelu][1]

Teraz potrzebujemy tootell hello [Train Model] [ train-model] modułu czy chcemy hello modelu toopredict hello ryzyka kredytowego wartość.

1. Wybierz hello [Train Model] [ train-model] modułu. W hello **właściwości** okienku, kliknij przycisk **Uruchom selektor kolumn**.

2. W hello **wybrać pojedynczą kolumnę** okna dialogowego, wpisz "ryzyko kredytowe" w polu wyszukiwania hello w obszarze **dostępne kolumny**, wybierz "Ryzyko kredytowe" poniżej i kliknij przycisk strzałki w prawo hello ( **>** ) toomove "Karty kredytowej ryzyka" zbyt**wybrane kolumny**. 

    ![Wybierz kolumnę ryzyka kredytowego hello modułu Train Model hello][0]

3. Kliknij przycisk hello **OK** znacznik wyboru.

### <a name="two-class-support-vector-machine"></a>Algorytm SVM dla problemu dwuklasowego

Następnie skonfiguruj firma Microsoft hello SVM modelu.  

Pierwszy, nieco wyjaśnienie SVM. Drzewa decyzyjne boosted działają prawidłowo w przypadku funkcji dowolnego typu. Jednak ponieważ moduł SVM hello generuje klasyfikatora liniowego, hello modelu, który generuje ma najlepsze błąd testu hello gdy wszystkie funkcje numeryczne hello samej skali. tooconvert cyfr toohello funkcje skalowania takie same, używamy transformację "Tanh" (z hello [normalizacji danych] [ normalize-data] modułu). To przekształca naszych numery w zakresie hello [0,1]. Moduł SVM Hello konwertuje ciąg funkcji toocategorical funkcje i następnie toobinary 0/1, dlatego firma Microsoft nie muszą toomanually transformacja funkcje ciągu. Ponadto nie chcemy tootransform hello ryzyka kredytowego kolumna (kolumna 21) — jest liczbowego, ale jest wartość hello możemy uczony hello toopredict modelu, potrzebujemy tooleave ją samodzielnie.  

tooset model SVM hello, hello następujące:

1. Znajdź hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu w palecie modułów hello i przeciągnij go na powitania kanwy.

2. Powitania kliknij prawym przyciskiem myszy [Train Model] [ train-model] modułu, wybierz opcję **kopiowania**, a następnie kliknij prawym przyciskiem myszy hello kanwy i wybierz **Wklej**. Witaj kopię hello [Train Model] [ train-model] moduł ma hello tego samego wyboru kolumny jako hello oryginalnego.

3. Połącz dane wyjściowe hello hello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] toohello modułu w lewo drugi port wejściowy z hello [Train Model] [ train-model] Moduł.

4. Znajdź hello [normalizacji danych] [ normalize-data] modułu i przeciągnij go na powitania kanwy.

5. Połącz powitania po lewej stronie dane wyjściowe lewej hello [wykonanie skryptu języka R] [ execute-r-script] wejścia modułu toohello tego modułu (powiadomienie, że hello port wyjściowy modułu mogą być połączone toomore niż inny moduł).

6. Połącz hello pozostałych portem wyjściowym hello [normalizacji danych] [ normalize-data] prawo toohello modułu drugie dane wejściowe portu hello [Train Model] [ train-model] modułu.

Ta część naszego eksperyment powinien teraz wyglądać mniej więcej tak:  

![Szkolenie hello drugim modelu][2]  

Teraz skonfigurować hello [normalizacji danych] [ normalize-data] modułu:

1. Kliknij przycisk tooselect hello [normalizacji danych] [ normalize-data] modułu. W hello **właściwości** okienku wybierz **Tanh** dla hello **metody przekształcania** parametru.

2. Kliknij przycisk **Uruchom selektor kolumn**, wybierz opcję "Brak kolumn" dla **od**, wybierz pozycję **Include** hello pierwszej listy rozwijanej, wybierz **typ kolumny**w hello drugi listy rozwijanej i wybierz **liczbowych** w hello trzeci listy rozwijanej. To ustawienie określa przekształcone wszystkich hello liczbowych kolumn (i tylko numeryczne).

3. Kliknij przycisk hello toohello znak plus (+) bezpośrednio z tego wiersza — spowoduje to utworzenie wiersza listę rozwijaną. Wybierz **wykluczyć** hello pierwszej listy rozwijanej, wybierz **nazwy kolumn** w hello drugi listy rozwijanej, a następnie wprowadź "Ryzyko kredytowe" w polu tekstowym hello. Określa, należy ją ignorować tej kolumny ryzyka kredytowego hello (potrzebujemy toodo to ponieważ ta kolumna jest liczbowych i tak może zostać przekształcone, jeśli firma Microsoft nie go wykluczyć).

4. Kliknij przycisk hello **OK** znacznik wyboru.  

    ![Wybierz kolumny hello normalizacji danych modułu][5]

Witaj [normalizacji danych] [ normalize-data] modułu jest teraz tooperform zestaw transformację Tanh na wszystkich kolumn liczbowych, z wyjątkiem hello ryzyka kredytowego.  

## <a name="score-and-evaluate-hello-models"></a>Wynik i ocena hello modeli

Używamy hello testowanie danych, który został oddzielony przez hello [podziału danych] [ split] tooscore modułu naszych przeszkolone modeli. Firma Microsoft następnie porównaj wyniki hello hello dwa modele toosee który wygenerować lepsze wyniki.  

### <a name="add-hello-score-model-modules"></a>Dodaj moduły Score Model hello

1. Znajdź hello [Score Model] [ score-model] modułu i przeciągnij go na powitania kanwy.

2. Połącz hello [Train Model] [ train-model] moduł, który został podłączony toohello [Two-Class Boosted drzewa decyzyjnego] [ two-class-boosted-decision-tree] wejścia po lewej stronie toohello modułu Port hello [Score Model] [ score-model] modułu.

3. Połącz prawo hello [wykonanie skryptu języka R] [ execute-r-script] prawo toohello modułu (danych testowych) danych wejściowych portu hello [Score Model] [ score-model] modułu.

    ![Moduł score Model połączenia][6]
   
   Witaj [Score Model] [ score-model] modułu teraz może zająć hello środki informacji z hello testowanie danych, uruchom go za pomocą modelu hello i porównaj hello prognoz modelu hello generuje z rzeczywistego hello karty kredytowej ryzyka Kolumna w hello testowanie danych.

4. Skopiuj i Wklej hello [Score Model] [ score-model] toocreate modułu drugiej kopii.

5. Połącz dane wyjściowe hello hello SVM modelu (to znaczy hello output portu hello [Train Model] [ train-model] moduł, który został podłączony toohello [maszyny wektorowa obsługa Two-Class] [ two-class-support-vector-machine] modułu) toohello drugie dane wejściowe portu hello [Score Model] [ score-model] modułu.

6. Model SVM hello zostały toodo hello tych samych danych test toohello przekształcania, jak robiliśmy toohello danych szkoleniowych. Dlatego skopiuj i Wklej hello [normalizacji danych] [ normalize-data] toocreate modułu drugiej kopii i podłącz go prawo toohello [wykonanie skryptu języka R] [ execute-r-script] modułu.

7. Drugie połączenie powitania po lewej stronie dane wyjściowe hello [normalizacji danych] [ normalize-data] prawo toohello modułu drugie dane wejściowe portu hello [Score Model] [ score-model] Moduł.

    ![Zarówno modułów Score Model połączenia][7]

### <a name="add-hello-evaluate-model-module"></a>Dodawanie modułu Evaluate Model hello

tooevaluate Witaj dwie wyników oceniania i porównaj je, używamy [Evaluate Model] [ evaluate-model] modułu.  

1. Znajdź hello [Evaluate Model] [ evaluate-model] modułu i przeciągnij go na powitania kanwy.

2. Połącz port wyjściowy hello hello [Score Model] [ score-model] moduł skojarzony z hello boosted decyzji drzewa po lewej toohello modelu danych wejściowych portu hello [Evaluate Model] [ evaluate-model] modułu.

3. Połącz hello innych [Score Model] [ score-model] toohello modułu prawo wejściowych portu.  

    ![Ocena modelu modułu połączone][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Uruchom eksperyment hello i hello wyniki sprawdzenia

toorun hello eksperyment, kliknij przycisk hello **Uruchom** znajdujący się poniżej hello kanwy. Może upłynąć kilka minut. Wskaźnik Obracająca dla każdego modułu pokazuje, że jest uruchomiona, i czym wyświetlany po zakończeniu modułu hello zielony znacznik wyboru. Jeśli zaznaczono wszystkie moduły hello eksperymentu hello zakończył działanie.

Hello eksperyment powinien teraz wyglądać mniej więcej tak:  

![Ocena obu modeli][3]

toocheck hello wyników, kliknij port wyjściowy hello hello [Evaluate Model] [ evaluate-model] moduł i zaznacz **Visualize**.  

Witaj [Evaluate Model] [ evaluate-model] modułu tworzy parę krzywych i metryki, które pozwalają wyniki hello toocompare dwa modele scored hello. Można wyświetlić wyniki hello jako krzywych cech Operator odbiornika (ROC), krzywych dokładności/wycofania lub krzywych przyrostu. Dodatkowe dane wyświetlane obejmuje macierz pomyłek, łączne wartości dla hello obszarze hello krzywej (AUC) i innych metryk. Można zmienić wartości progowej hello przez przenoszenie hello suwak w lewo lub w prawo i zobacz, jak wpływa na powitania zbiór metryki.  

Kliknij toohello rogu wykresu hello **oceniane zestawu danych** lub **oceniane toocompare zestawu danych** toohighlight hello skojarzone krzywej i toodisplay hello skojarzone metryki poniżej. Legenda hello krzywych na powitania, "Oceniane zestawu danych" odpowiada toohello pozostałych port wejściowy z hello [Evaluate Model] [ evaluate-model] moduł — w tym przypadku jest to hello boosted decyzji drzewa modelu. "Oceniane toocompare zestawu danych" odpowiada prawy port wejściowy toohello - hello SVM modelu w tym przypadku. Po kliknięciu jednego z tych etykiet zostanie wyróżniona krzywej hello modelu i metryki odpowiedniego hello są wyświetlane, pokazane na powitania po grafiki.  

![Krzywe ROC dla modeli][4]

Badanie tych wartości, można zdecydować, model, który jest najbliższy toogiving hello wyników, którego szukasz. Możesz wrócić do poprzedniej strony i iterację eksperymentu, zmieniając wartości parametrów w różne modele hello. 

Witaj nauki i grafik interpretowanie te wyniki i dostrajania wydajności modelu hello jest hello poza zakres tego przewodnika. Aby uzyskać dodatkową pomoc mogą odczytać hello następujące artykuły:
- [Jak tooevaluate modelu wydajności w usłudze Azure Machine Learning](machine-learning-evaluate-model-performance.md)
- [Wybierz parametry toooptimize algorytmy w usłudze Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md)
- [Interpretowanie wyników modelu w usłudze Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Każdym uruchomieniu eksperymentu hello rekord tego iteracji jest przechowywany w hello Uruchom historii. Można wyświetlić te iteracji i zwracać tooany z nich, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** poniżej hello kanwy. Możesz również kliknąć **uprzedniego uruchomienia** w hello **właściwości** iteracji toohello tooreturn okienko poprzedzającego hello mają otwarte.
> 
> Można utworzyć kopię dowolną iterację eksperymentu, klikając **SAVE AS** poniżej hello kanwy. 
> Użyj eksperymentu hello **Podsumowanie** i **opis** tookeep właściwości rekordu zawierającego co podjęto w Twojej iteracje eksperymentu.
> 
> Aby uzyskać więcej informacji, zobacz [Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Następnie: [wdrażanie usługi sieci web hello](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
