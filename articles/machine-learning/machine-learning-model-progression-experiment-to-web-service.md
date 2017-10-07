---
title: "usługi sieci web staje się aaaHow modelu usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Omówienie mechanika hello sposób realizowany modelu z usługi Azure Machine Learning z rozwinięcie eksperymentu tooan operationalized usługi sieci Web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Sposób realizowany modelu uczenia maszynowego, z tooan eksperymentu operationalized usługi sieci Web
Azure Machine Learning Studio udostępnia interaktywny kanwy, która pozwala toodevelop, uruchom, testowanie i iteracji ***eksperymentu*** modelu analizy predykcyjnej. Istnieje szereg dostępne moduły, które można:

* Dane wejściowe do eksperymentu
* Manipulować danymi hello
* Uczenie modelu przy użyciu przy użyciu algorytmów uczenia maszynowego
* Wynik hello modelu
* Ocena wyników hello
* Wartości ostateczne dane wyjściowe

Po zakończeniu eksperymentu można wdrożyć go jako ***usługi sieci Web klasycznego Azure Machine Learning*** lub ***usługi sieci Web nowego Azure Machine Learning*** tak, aby użytkownicy mogli przesyła nowych danych i odbierania Wstecz wyniki.

W tym artykule zapewniamy im omówienie mechanika hello jak Twoje realizowany modelu uczenia maszynowego z tooan eksperymentu programowanie operationalized usługi sieci Web.

> [!NOTE]
> Istnieją inne sposoby toodevelop i wdrażanie modeli uczenia maszyny, ale ten artykuł koncentruje się na sposobie korzystania z usługi Machine Learning Studio. Na przykład tooread opis toocreate klasycznego predykcyjnej usługi sieci Web za pomocą R, zobacz temat hello blogu [kompilacji i wdrażania predykcyjnej sieci Web aplikacji przy użyciu programu RStudio i uczenie Maszynowe Azure](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Gdy Azure Machine Learning Studio jest zaprojektowana toohelp opracowywania i wdrażania *modelu analizy predykcyjnej*, jest możliwe toouse Studio toodevelop eksperymentu, która nie zawiera modelu analizy predykcyjnej. Na przykład eksperymentu może po prostu wprowadzania danych, manipulować ją, a następnie hello wynik. Podobnie jak eksperymentu analizy predykcyjnej można wdrożyć tego eksperymentu predykcyjny jako usługę sieci Web, ale jest prostsze procesu, ponieważ eksperyment hello nie jest szkolenia lub oceniania modelu uczenia maszynowego. Mimo że nie jest hello typowe toouse Studio w ten sposób, firma Microsoft będzie dołączyć dyskusji hello tak, aby firma Microsoft zapewnia pełne wyjaśnienie działania Studio.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Tworzenie i wdrażanie predykcyjnej usługi sieci Web
Oto etapy hello, które są typowe rozwiązania postępuje zgodnie z tworzenia i wdrażania go za pomocą usługi Machine Learning Studio:

![Przepływ wdrożenia](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Rysunek 1 — etapy modelu analizy predykcyjnej typowe*

### <a name="hello-training-experiment"></a>eksperyment uczenia Hello
Witaj ***eksperyment uczenia*** jest hello początkowym etapie projektowania usługi sieci Web w usłudze Machine Learning Studio. Celem Hello eksperyment uczenia hello jest toogive toodevelop miejsce, testowanie, iteracji i ostatecznie uczenia modelu uczenia maszynowego. Możesz to zrobić nawet później wielu modeli jednocześnie Wyszukaj hello najlepszego rozwiązania, ale po zakończeniu eksperymentowanie możesz wybrać jeden uczenia modelu i wyeliminować hello rest z hello eksperymentu. Na przykład opracowania eksperymentu analizy predykcyjnej, zobacz [tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>eksperyment predykcyjny Hello
Po uzyskaniu nauczonego modelu w eksperymencie szkolenia, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web** w usłudze Machine Learning Studio tooinitiate hello proces konwersji do szkolenia eksperymentu tooa ***eksperyment predykcyjny***. Witaj celem eksperyment predykcyjny hello jest toouse uczonego modelu tooscore nowych danych, z celem hello ostatecznie staje się operationalized jako usługi sieci Web platformy Azure.

Ta konwersja jest realizowane automatycznie za pomocą hello następujące kroki:

* Konwertuj hello zbiór moduły używane do trenowania w jednym module i zapisz go jako uczonego modelu
* Wyeliminowanie wszelkich modułów nadmiarowe niezwiązanych tooscoring
* Dodawanie danych wejściowych i wyjściowych porty, które hello ostatecznego sieci Web, które będzie używane przez usługę

Może być więcej zmiany toomake tooget Twojego toodeploy gotowy eksperyment predykcyjny jako usługę sieci Web. Na przykład aby toooutput usługi sieci Web hello tylko podzestaw wyników, można dodać moduł filtrowania przed hello port wyjściowy.

W tym procesie konwersji eksperyment uczenia hello nie zostaną odrzucone. Po zakończeniu procesu hello ma dwie karty w Studio: jeden dla eksperyment uczenia hello i jeden dla eksperyment predykcyjny hello. W ten sposób można wprowadzać zmiany eksperyment uczenia toohello przed wdrożeniem usługi sieci Web i Odbuduj eksperyment predykcyjny hello. Lub możesz zapisać kopię toostart eksperymentu uczenia hello innego wiersza eksperymenty.

> [!NOTE]
> Po kliknięciu **predykcyjnej usługi sieci Web** uruchomić proces automatycznego tooconvert eksperymentu predykcyjnej tooa eksperymentu uczenia i to działa dobrze w większości przypadków. Jeśli eksperymentu uczenia jest złożony (na przykład masz wiele ścieżek szkolenia, do której należy dołączyć razem), można wybrać toodo konwersji ręcznie. Aby uzyskać więcej informacji, zobacz [jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Witaj usługi sieci Web
Po zakończeniu eksperymentu predykcyjnej jest gotowy, można wdrożyć usługi jako usługi sieci Web klasycznego czy usługi sieci Web nowego oparte na usłudze Azure Resource Manager. toooperationalize modelu przez wdrożenie jej jako *klasycznego Machine Learning w sieci Web usługi*, kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**. toodeploy jako *nowe Machine Learning w sieci Web usługi*, kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**. Użytkownicy mogą teraz wysyłać dane tooyour modelu przy użyciu interfejsu API REST usługi sieci Web hello i otrzymywać wyniki hello Wstecz. Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>Witaj-typowy przypadek: tworzenie-predykcyjnej usługi sieci Web
Jeśli eksperymentu nie uczenia modelu analizy predykcyjnej, możesz nie ma potrzeby toocreate zarówno eksperyment uczenia i oceniania eksperymentu — istnieje tylko jeden eksperymentu i można go wdrożyć jako usługę sieci Web. Usługa Machine Learning Studio wykrywa, czy eksperymentu zawiera model predykcyjny analizując hello moduły, w których używano.

Po zostały iterowane w eksperymencie i uzyskaniu go:

1. Kliknij przycisk **ustawić usługę sieci Web** i wybierz **ponownego trenowania usługi sieci Web** — wejściowa i wyjściowa węzły są dodawane automatycznie
2. Kliknij przycisk **Uruchom**
3. Kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]** w zależności od toowhich środowiska hello ma toodeploy.

Usługi sieci Web został wdrożony i można uzyskać dostęp i zarządzać nią tak samo jak predykcyjnej usługi sieci Web.

## <a name="updating-your-web-service"></a>Aktualizowanie usługi sieci Web
Po wdrożeniu eksperymentu jako usługę sieci Web, co zrobić, jeśli należy tooupdate go?

To zależy od potrzebnych tooupdate:

**Ma toochange hello w danych wejściowych lub wyjściowych lub ma toomodify jak hello usługi sieci Web manipulowanie danymi**

Jeśli nie chcesz zmienić hello model, ale tylko zmiana jak hello usługi sieci Web obsługuje danych można edytować eksperyment predykcyjny hello, a następnie kliknij przycisk **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]** ponownie. Hello usługi sieci Web zostanie zatrzymana, hello zaktualizowane eksperyment predykcyjny jest wdrożony i hello usługi sieci Web zostanie ponownie uruchomiony.

Oto przykład: Załóżmy, że Twoje eksperyment predykcyjny zwraca hello cały wiersz danych wejściowych z hello przewidzieć wynik. Użytkownik może określić, że hello sieci Web usługi toojust hello zwracanych wyników. Dzięki czemu można dodać **kolumny projektu** modułu w eksperymencie predykcyjnej hello, tuż przed hello output portu, tooexclude kolumn niż hello wyniku. Po kliknięciu **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]** ponownie hello usługi sieci Web jest aktualizowany.

**Ma modelu hello tooretrain nowymi danymi**

Jeśli chcesz tookeep komputerze uczenie modelu, ale chcesz tooretrain go z nowymi danymi, dostępne są dwie opcje:

1. **Ponownie ucz modelu hello hello usługi sieci Web jest uruchomiona** — Jeśli chcesz tooretrain modelu hello predykcyjnej usługi sieci Web jest uruchomiona, można to zrobić, wykonując kilka zmian toohello szkolenia eksperymentu toomake go *** ponownego trenowania eksperymentu***, a następnie wdrożyć go jako  ***web ponownego trenowania* usługi**. Aby uzyskać instrukcje dotyczące toodo tego, zobacz [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).
2. **Przejdź wstecz toohello oryginalnego eksperyment uczenia i użyj innego szkolenia toodevelop danych modelu** — predykcyjnej eksperymentu jest toohello połączonej usługi sieci Web, ale eksperyment uczenia hello nie jest bezpośrednio połączony w ten sposób. Jeśli zmodyfikujesz hello oryginalnego eksperyment uczenia i kliknij przycisk **ustawić usługę sieci Web**, utworzy on *nowe* predykcyjnej eksperymentu, która utworzy po wdrożeniu *nowe* sieci Web Usługa. Jednak nie tylko aktualizacji hello oryginalnego usługi sieci Web.
   
   Eksperyment uczenia hello toomodify, należy otworzyć go i kliknij przycisk **Zapisz jako** toomake kopii. Spowoduje to pozostawienie oryginalnego eksperyment uczenia hello nienaruszone, eksperyment predykcyjny i usługi sieci Web. Można teraz utworzyć nową usługę sieci Web ze zmianami. Po wdrożeniu hello nową usługę sieci Web, które następnie można zdecydować, czy toostop hello poprzedniej usługi sieci Web, czy też pozostawić będzie działać równolegle z hello nową.

**Ma tootrain innego modelu**

Jeśli chcesz toomake zmianach tooyour oryginalnego eksperyment predykcyjny, takie jak wybranie innej maszyny Algorytm uczenia, w trakcie szkolenia innej metody, itd., następnie należy toofollow hello drugiej procedury opisane powyżej, aby ponownego trenowania modelu: Otwórz eksperyment uczenia hello, kliknij pozycję **Zapisz jako** toomake kopii, a następnie uruchom nową ścieżkę hello opracowywania modelu, eksperyment predykcyjny hello tworzenie i wdrażanie w dół hello usługi sieci web. Spowoduje to utworzenie nowej usługi sieci Web niepowiązane toohello oryginału — można zdecydować, które tookeep jeden lub oba, systemem.

## <a name="next-steps"></a>Następne kroki
Więcej szczegółów na powitania procesu tworzenia i doświadczenia zobacz następujące artykuły hello:

* Konwertowanie eksperymentu hello - [jak tooprepare modelu do wdrożenia w usłudze Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* Wdrażanie usługi sieci Web hello - [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* model hello ponownego trenowania — [Retrain Machine Learning modeli](machine-learning-retrain-models-programmatically.md)

Przykłady hello całego procesu zobacz:

* [Samouczek dotyczący uczenia maszynowego: Tworzenie pierwszego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Przewodnik: Tworzenie rozwiązania analizy predykcyjnej w celu oceny ryzyka kredytowego w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

