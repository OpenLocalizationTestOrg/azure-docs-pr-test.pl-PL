---
title: nauki aaaData na powitania maszyny wirtualnej systemu Linux danych nauki | Dokumentacja firmy Microsoft
description: "Jak tooperform kilka typowych nauki danych zadań z hello maszyny Wirtualnej systemu Linux danych nauki."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Nauki danych na powitania maszyny wirtualnej systemu Linux danych nauki
W tym przewodniku przedstawiono sposób tooperform kilka typowych nauki danych zadania o hello maszyny Wirtualnej systemu Linux danych nauki. Witaj Linux danych nauki maszyny wirtualnej (DSVM) jest obrazu maszyny wirtualnej na platformie Azure, który jest wstępnie zainstalowane z kolekcją narzędzi powszechnie używany do analizy danych i uczenia maszynowego. składniki oprogramowania klucza Hello są wymienione w hello [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md) tematu. Witaj obrazu maszyny Wirtualnej umożliwia łatwe tooget uruchomiona podczas nauki danych (w minutach), bez konieczności tooinstall i skonfiguruj każdy narzędzi hello pojedynczo. Można łatwo skalować hello maszyny Wirtualnej, jeśli to konieczne i zatrzymaj ją nieużywane. Dlatego ten zasób jest zarówno elastyczne i ekonomiczne.

Hello zadania nauki danych zostało to pokazane w tym przewodniku wykonaj hello kroki opisane w hello [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Ten proces obejmuje nauki toodata systematyczne podejście, umożliwiającą zespoły analityków danych tooeffectively współpracę cyklem hello tworzenia aplikacji inteligentnego. w procesie nauki Hello danych umożliwia również iteracyjne framework analizy danych, które można wykonać przez osobę.

Możemy przeanalizować hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) zestawu danych w ramach tego przewodnika. Jest to zestaw wiadomości e-mail, które są oznaczone jako wiadomości-śmieci lub pichcisz (tzn. nie są one spamu), i zawiera także statystykami dotyczącymi zawartości hello hello wiadomości e-mail. statystyki Hello uwzględnione omówiono hello obok ale jedną sekcję.

## <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem maszyny wirtualnej systemu Linux danych nauki, musi mieć następujące hello:

* **Subskrypcji platformy Azure**. Jeśli nie masz już jeden, zobacz [utworzyć bezpłatne konto platformy Azure obecnie](https://azure.microsoft.com/free/).
* A [ **nauki danych Linux VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Aby uzyskać informacje o inicjowaniu obsługi tej maszyny Wirtualnej, zobacz [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) zainstalowany na tym komputerze i otworzyć sesję XFCE. Aby uzyskać informacje o instalowaniu i konfigurowaniu **klienta X2Go**, zobacz [Instalowanie i konfigurowanie klienta X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* **Konta uczenie maszynowe Azure**. Jeśli nie masz jeszcze jeden Załóż nowe hasło w hello [strony głównej uczenie maszynowe Azure](https://studio.azureml.net/). Brak toohelp warstwy bezpłatna użycia, możesz rozpocząć pracę.

## <a name="download-hello-spambase-dataset"></a>Pobierz zestaw hello spambase danych
Witaj [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) zestaw danych jest stosunkowo mały zestaw danych, który zawiera tylko 4601 przykłady. Jest to toouse rozmiarów wykazać, że niektóre główne funkcje hello hello wirtualna analizy danych, ponieważ utrzymuje wymagań dotyczących zasobów hello niewielkie.

> [!NOTE]
> Ten przewodnik został utworzony na D2 rozmiar v2 danych nauki maszyny wirtualnej systemu Linux. Ten rozmiar jest w stanie obsługiwać hello procedur w tym przewodniku DSVM.
>
>

Jeśli potrzebujesz więcej miejsca w magazynie, można tworzyć dodatkowe dyski i dołącz je tooyour maszyny Wirtualnej. Te dyski używać trwałego magazynu Azure, dlatego ich dane zostaną zachowane nawet wtedy, gdy jest ponownie udostępnić powitania serwera z powodu tooresizing lub jest zamknięty. tooadd dysku i dołącz je tooyour maszyny Wirtualnej, wykonaj te instrukcje hello [dodać tooa dysku maszyny Wirtualnej systemu Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Kroki przy użyciu interfejsu wiersza polecenia platformy Azure (Azure CLI), który jest już zainstalowany na powitania DSVM hello. Dlatego te procedury może odbywać się wyłącznie z hello samej maszyny Wirtualnej. Inną opcją tooincrease magazynu jest toouse [pliki Azure](../storage/files/storage-how-to-use-files-linux.md).

toodownload hello danych, Otwórz okno terminalu i uruchom to polecenie:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

Witaj pobrany plik nie ma wiersz nagłówka, więc warto utworzyć innego pliku, który ma nagłówka. Uruchom plik toocreate tego polecenia, z nagłówkami odpowiednie hello:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Następnie połącz hello dwa pliki z poleceniem hello:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Witaj dataset zawiera kilka typów statystyk w każdej wiadomości e-mail:

* Kolumn, takich jak ***word\_Częst\_WORD*** wskazuje procent hello w wiadomości e-mail hello wyrazy, które odpowiadają *WORD*. Na przykład jeśli *word\_Częst\_upewnij* ma wartość 1, a następnie zostały 1% wszystkich wyrazów w wiadomości e-mail hello *upewnij*.
* Kolumn, takich jak ***char\_Częst\_CHAR*** wskazuje procent hello wszystkich znaków w wiadomości e-mail hello, które były *CHAR*.
* ***kapitału\_Uruchom\_długość\_najdłuższym*** jest hello najdłuższy okres sekwencję wielkimi literami.
* ***kapitału\_Uruchom\_długość\_średni*** jest średnią długość hello wszystkich sekwencji wielkimi literami.
* ***kapitału\_Uruchom\_długość\_całkowita*** jest hello łączna długość wszystkich sekwencji wielkimi literami.
* ***spamu*** wskazuje, czy hello e-mail został uznany za spam, lub nie (1 = wiadomości-śmieci, 0 = nie spamu).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Eksploruj hello zestawu danych otwórz R firmy Microsoft
Teraz zbadać hello danych i wykonaj niektórych uczenia maszynowego podstawowe z hello R. wirtualna nauki danych jest dostarczany z [Microsoft R Otwórz](https://mran.revolutionanalytics.com/open/) wstępnie zainstalowane. Hello bibliotek wielowątkowych matematyczne w tej wersji R oferuje lepszą wydajność niż w różnych wersjach jednowątkowy. Otwórz R firmy Microsoft są także powtarzalności przy użyciu migawek z repozytorium pakietów hello sieci CRAN.

kopie tooget hello kodu próbek używanych w tym przewodniku hello w klonowania **Azure-maszyny-Learning-danych-nauki** repozytorium przy użyciu usługi git, który jest wstępnie zainstalowane na powitania maszyny Wirtualnej. Z wiersza polecenia git hello Uruchom polecenie:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Otwórz okno terminala i rozpocznij nową sesję R z konsolą interakcyjne hello R.

> [!NOTE]
> Umożliwia także programu RStudio dla hello zgodnie z procedurami. tooinstall programu RStudio, wykonanie tego polecenia w terminalu:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

Uruchom tooimport hello danych i skonfigurować środowisko hello:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee podsumowania statystyk dotyczących poszczególnych kolumn:

    summary(data)

Do innego widoku danych hello:

    str(data)

Oznacza to, hello typu każdej zmiennej i hello najpierw kilka wartości hello zestawu danych.

Witaj *spamu* kolumna została odczytana jako liczba całkowita, ale jest rzeczywiście kategorii zmiennej (lub współczynnik). tooset jej typ:

    data$spam <- as.factor(data$spam)

toodo niektóre poznawcze analizy, użyj hello [ggplot2](http://ggplot2.org/) pakietu popularnych biblioteki graficznych dla języka R, która jest już zainstalowana na powitania maszyny Wirtualnej. Uwaga: z danych podsumowania hello wyświetlane wcześniej, będziemy mieć podsumowania statystyk od częstotliwości hello hello wykrzyknik znaku. Załóżmy wykreślenia tych częstotliwości tutaj z hello następującego polecenia:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Ponieważ pasek hello zero pochylenie kreślenia hello umożliwia pozbyć się go:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Brak nieuproszczony gęstości powyżej 1, która wygląda interesujące. Przyjrzyjmy się tylko te dane:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Następnie podziel go przez pichcisz vs spamu:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Te przykłady należy włączyć, należy toomake podobne wykresy hello tooexplore innych kolumn hello dane zawarte w nich.

## <a name="train-and-test-an-ml-model"></a>Nauczenia i przetestowania modelu usługi uczenie Maszynowe
Teraz załóżmy train kilka uczenia maszynowego modele tooclassify wiadomości powitania w zestawie danych hello jako zawierające albo span lub pichcisz. Firma Microsoft train model drzewa decyzyjnego i model lasu losowe w tej sekcji, a następnie sprawdź ich dokładność ich prognoz.

> [!NOTE]
> Witaj rpart (cykliczne partycjonowania i drzew regresji) pakietu używane w hello następującego kodu jest już zainstalowana na powitania wirtualna analizy danych.
>
>

Po pierwsze możemy podzielić zestawu danych hello w zestawy szkoleniowe i testu:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

A następnie utworzyć hello tooclassify drzewa decyzyjnego wiadomości e-mail.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

W tym miejscu jest wynikiem hello:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

jak wykonuje szkolenia hello toodetermine ustawić, użyj hello następującego kodu:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

jak dobrze toodetermine wykonuje na powitania zestawu testowego:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Spróbujmy również modelu losowe lasu. Losowe lasów wiele algorytmów uczenia i wyjściowych klasę, która jest tryb hello hello klasyfikacje ze wszystkich hello poszczególnych algorytmów. Udostępniają one bardziej wydajny komputer uczenia podejście, jak Usuń hello tendencję decyzji toooverfit modelu drzewa zestawu danych szkoleniowych.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Wdrażanie tooAzure modelu uczenia Maszynowego
[Azure Machine Learning Studio](https://studio.azureml.net/) (uczenie maszynowe Azure) to usługa w chmurze, który umożliwia łatwe toobuild i wdrażanie modeli analizy predykcyjnej. Jedną z funkcji nieuprzywilejowany hello uczenie maszynowe Azure jest jego toopublish możliwości żadnych R działać jako usługi sieci web. Witaj pakietu języka R uczenie maszynowe Azure nawiązuje toodo łatwe wdrożenia bezpośrednio z naszych sesji R hello DSVM.

drzewa decyzyjne kodu toodeploy hello z poprzedniej sekcji hello należy toosign w tooAzure Machine Learning Studio. Należy identyfikator obszaru roboczego i toosign token autoryzacji w. toofind te wartości i zainicjować hello uczenie maszynowe Azure zmiennych z nimi:

Wybierz **ustawienia** na powitania menu po lewej stronie. Uwaga użytkownika **identyfikator obszaru roboczego**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Wybierz **tokeny autoryzacji** z menu narzutów hello i notatki z **podstawowego tokenu autoryzacji**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Witaj obciążenia **uczenie maszynowe Azure** pakietu, a następnie ustaw wartości zmiennych hello za pomocą Identyfikatora tokenu i obszar roboczy w sesji R na powitania DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Odrobinę uprościmy badane toomake modelu hello tego pokazu tooimplement łatwiejsze. Wybierz hello trzy zmienne w hello decyzji najbliższego toohello katalogu głównego drzewa i utworzyć nowe drzewo przy użyciu tylko tych trzech zmiennych:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Potrzebujemy, funkcja prognozowania, która przyjmuje jako dane wejściowe funkcji hello i zwraca hello przewidywane wartości:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Publikowanie tooAzureML funkcja predictSpam hello przy użyciu hello **publishWebService** funkcji:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Ta funkcja przyjmuje hello **predictSpam** funkcji, tworzy usługi sieci web o nazwie **spamWebService** z zdefiniowane wejściach i wyjściach i zwraca informacje na temat hello nowy punkt końcowy.

Wyświetl szczegóły hello opublikować usługi sieci web, w tym jego klucze interfejsu API punktu końcowego i dostęp za pomocą polecenia hello:

    spamWebService[[2]]

tootry hello go na pierwszych 10 wierszy hello zestawu testów:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Użyj innych dostępnych narzędzi
Witaj pozostałe sekcje pokazują, jak toouse niektóre narzędzia hello zainstalowane na hello maszyny Wirtualnej systemu Linux danych nauki. Poniżej znajduje się lista hello narzędzia opisem:

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL & Squirrel SQL
* Magazyn danych serwera SQL Server

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) to narzędzie, które udostępnia implementację szybkich i dokładnych boosted drzewa.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost można również wywołać z języka python lub wiersza polecenia.

## <a name="python"></a>Python
Do tworzenia aplikacji przy użyciu języka Python zostały zainstalowane w hello DSVM hello Anaconda Python dystrybucje 2.7 i 3.5.

> [!NOTE]
> obejmuje Hello dystrybucji Anaconda [Condas](http://conda.pydata.org/docs/index.html), które mogą być używane toocreate niestandardowego środowiska dla języka Python, które mają różne wersje i/lub pakietów zainstalowanych w nich.
>
>

Umożliwia odczytu w niektórych hello spambase dataset i klasyfikowania wiadomości powitania maszynom wektorowa obsługa w scikit — Dowiedz się więcej:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

operacje przewidywania dla toomake:

    clf.predict(X.ix[0:20, :])

tooshow jak toopublish punkt końcowy uczenie maszynowe Azure umożliwia łatwiejsze modelu upewnij hello trzy zmienne jako robiliśmy po opublikowaniu firma Microsoft hello R modelu wcześniej.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish tooAzureML modelu hello:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> To jest dostępne tylko dla języka python 2.7 i nie jest jeszcze obsługiwana w 3.5. Uruchom z **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
Witaj Anaconda dystrybucji w hello DSVM jest dostarczany z notesu Jupyter, kod języka Python, R lub Julia tooshare środowiska i platform i analizy. notesu Jupyter Hello jest dostępny za pośrednictwem JupyterHub. Zaloguj się przy użyciu lokalnego nazwę użytkownika systemu Linux i hasło na ***https://\<nazwę DNS maszyny Wirtualnej lub adres IP\>: 8000 /***. Wszystkie pliki konfiguracji dla JupyterHub znajdują się w katalogu **/etc/jupyterhub**.

Kilka przykładowych notesów są już zainstalowane na powitania maszyny Wirtualnej:

* Zobacz hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) notesu Python próbki.
* Zobacz [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) przykładowe **R** notesu.
* Zobacz hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) dla innej próbki **Python** notesu.

> [!NOTE]
> Witaj Julia języka jest również dostępna z wiersza polecenia hello na powitania maszyny Wirtualnej systemu Linux danych nauki.
>
>

## <a name="rattle"></a>Rattle
[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (łatwo hello tooLearn narzędzie analityczne R) jest narzędziem graficznym R do wyszukiwania danych. Ma ona intuicyjny interfejs, który umożliwia łatwe tooload, Eksploruj i przekształcania danych i tworzenie i oceny modeli.  Artykuł Hello [Rattle: A danych wyszukiwania graficznego interfejsu użytkownika dla R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) zawiera wskazówki, który demonstruje jego funkcje.

Zainstaluj i uruchom Rattle z hello następującego polecenia:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Instalacja nie jest wymagana na powitania DSVM. Ale Rattle może monitować dodatkowe pakiety tooinstall podczas jego ładowania.
>
>

Rattle używa interfejsu oparte na karcie. Większość kart hello odpowiada toosteps w hello [proces nauki danych](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), takie jak ładowanie danych lub jej eksplorację. proces nauki danych Hello wypływających z lewym tooright przez hello karty. Ale hello ostatniej karty zawiera dziennik uruchamiając Rattle poleceń hello R.

tooload i skonfigurować hello zestawu danych:

* Plik hello tooload, wybierz opcję hello **danych** karcie następnie
* Wybierz opcję selektora hello dalej zbyt**Filename** i wybierz polecenie **spambaseHeaders.data**.
* Plik hello tooload. Wybierz **Execute** w hello najwyższego rzędu przycisków. Powinny pojawić się podsumowanie każdej kolumny, w tym jego typu danych zidentyfikowanych, czy dane wejściowe, cel lub innego typu zmienną i hello liczbę unikatowych wartości.
* Rattle poprawnie identyfikuje hello **spamu** kolumny jako cel hello. Wybierz hello spamu kolumny, a następnie hello zestaw **docelowy typ danych** za**Categoric**.

dane hello tooexplore:

* Wybierz hello **Eksploruj** kartę.
* Kliknij przycisk **podsumowania**, następnie **Execute**, toosee niektóre informacje na temat typów zmiennych hello i niektórych podsumowania statystyk.
* tooview innych typów danych statystycznych dotyczących każdej zmiennej, wybierz inne opcje, takie jak **Opisz** lub **podstawy**.

Witaj **Eksploruj** kartę można też toogenerate wiele interesującego geograficzne. tooplot histogram hello danych:

* Wybierz **dystrybucje**.
* Sprawdź **Histogram** dla **word_freq_remove** i **word_freq_you**.
* Wybierz **wykonania**. Powinny pojawić się, że oba gęstość geograficzne w oknie pojedynczego wykresu, jeżeli jest jasne wyrazie hello częściej pojawia się "musisz" wiadomości e-mail niż "Usuń".

krzywe korelacji Hello są również interesujące. toocreate co:

* Wybierz **korelacji** jako hello **typu**, następnie
* Wybierz **wykonania**.
* Rattle wyświetli ostrzeżenie, że zaleca maksymalnie 40 zmiennych. Wybierz **tak** tooview hello kreślenia.

Istnieją pewne interesujące korelacji, które znaleziona: "technologii" silnie skorelowane zbyt "HP" i "laboratoria", na przykład. Ponadto jest skorelowany zbyt "650", ponieważ kod obszaru hello dawcy dataset hello jest 650.

Hello wartości liczbowych hello korelacji między wyrazami są dostępne w oknie Eksploruj hello. Jest interesujące toonote, na przykład, że "technologii" negatywnie są skorelowane z "UR" i "cenę".

Rattle można przekształcać hello dataset toohandle niektórych typowych problemów. Na przykład można funkcje toorescale, przypisują brakujące wartości obsługi wartości odstających i Usuń zmienne lub uwagi z brakującymi danymi. Rattle mogą też wskazać reguły skojarzenia między uwag i/lub zmienne. Te karty wykraczają poza zakres tego przewodnika wstępne.

Rattle można również wykonywać analizy klastra. Umożliwia wykluczenie niektórych funkcji toomake hello dane wyjściowe łatwiejsze tooread. Na powitania **danych** , wybierz pozycję **Ignoruj** dalej tooeach hello zmiennych z wyjątkiem tych pozycji 10:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spamu

Następnie wróć toohello **klastra** , wybierz pozycję **KMeans**i ustaw hello *liczby klastrów* too4. Następnie **wykonania**. w oknie danych wyjściowych hello są wyświetlane wyniki Hello. Jeden klaster ma wysoką częstotliwość "george" i "hp" i prawdopodobnie jest uzasadnione służbowy adres e-mail.

toobuild modelu uczenia maszynowego drzewa proste decyzji:

* Wybierz hello **modelu** karcie
* Wybierz **drzewa** jako hello **typu**.
* Wybierz **Execute** toodisplay hello drzewa w postaci tekstu w hello okna wyjściowego.
* Wybierz hello **rysowania** tooview przycisk graficzny wersji. Wygląda ona podobna drzewa toohello możemy uzyskany wcześniej przy użyciu *rpart*.

Jedną z funkcji nieuprzywilejowany hello Rattle jest jego możliwości toorun metody kilka uczenia maszynowego i szybko ich oceny. Poniżej przedstawiono procedurę hello:

* Wybierz **wszystkie** dla hello **typu**.
* Wybierz **wykonania**.
* Po zakończeniu kliknięcie dowolnego pojedynczego **typu**, takiej jak **SVM**i wyświetlić wyniki hello.
* Można także porównać wydajności hello modeli hello weryfikacji hello ustawić za pomocą hello **Evaluate** kartę. Na przykład Witaj **macierzy błąd** zaznaczenie zawiera macierz pomyłek hello, ogólny błąd i błąd uśrednionej klasy dla każdego modelu hello sprawdzania poprawności zestawu.
* Można również wykreślenia krzywych ROC, analiza czułości i czy innych typów oceny modelu.

Po zakończeniu budowania modeli wybierz hello **dziennika** karcie tooview hello R kodu przez Rattle podczas sesji. Możesz wybrać hello **wyeksportować** toosave przycisk go.

> [!NOTE]
> Jest to błąd w bieżącej wersji Rattle. toomodify hello skryptu lub użyć toorepeat etapów później, należy wstawić przed znak # * wyeksportować ten dziennik... * w tekście hello hello dziennika.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL & Squirrel SQL
Witaj DSVM jest dostarczany z PostgreSQL zainstalowane. PostgreSQL jest złożone, open source relacyjnej bazy danych. W tej sekcji przedstawiono sposób tooload naszych spamu zestawu danych do PostgreSQL, a następnie wykonasz zapytania.

Przed załadowaniem danych hello należy tooallow uwierzytelniania hasła z hello localhost. W wierszu polecenia:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Dolnej hello pliku konfiguracyjnego hello są kilka wierszy, które zawierają hello dozwolone połączenia:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Zmień hello "Lokalnych połączeń IPv4" wiersza toouse md5 zamiast ident, aby firma Microsoft może logować się przy użyciu nazwy użytkownika i hasła:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

I ponownie uruchom usługę postgres hello:

    sudo systemctl restart postgresql

psql toolaunch, terminalu interactive PostgreSQL jako użytkownik wbudowanych postgres hello, uruchom następujące polecenie w wierszu hello:

    sudo -u postgres psql

Utwórz nowe konto użytkownika, za pomocą hello tej samej nazwy użytkownika, jak hello konta systemu Linux, który jest obecnie zalogowany jako i nadaj mu hasło:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Następnie zaloguj się toopsql jako użytkownika:

    psql

I zaimportuj dane hello do nowej bazy danych:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Teraz załóżmy Eksplorowanie danych hello i uruchom kilka zapytań przy użyciu **Squirrel SQL**, graficzne narzędzie, które umożliwia interakcję z bazami danych za pośrednictwem sterownik JDBC.

Rozpoczęto tooget, uruchomić Squirrel SQL z menu aplikacji hello. tooset zapasową sterownika hello:

* Wybierz **Windows**, następnie **Wyświetl sterowniki**.
* Kliknij prawym przyciskiem myszy **PostgreSQL** i wybierz **zmodyfikować sterownika**.
* Wybierz **bardzo klasy ścieżki**, następnie **dodać**.
* Wprowadź ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** dla hello **nazwę pliku** i
* Wybierz **Otwórz**.
* Wybierz z listy sterowniki, a następnie wybierz **org.postgresql.Driver** w **Nazwa klasy**i wybierz **OK**.

tooset hello połączenia toohello lokalnego serwera:

* Wybierz **Windows**, następnie **wyświetlić aliasy.**
* Wybierz hello  **+**  toomake przycisk Nowy alias.
* Nadaj mu nazwę *bazy danych spamu*, wybierz **PostgreSQL** w hello **sterownika** listy rozwijanej.
* Ustaw adres URL hello zbyt*jdbc:postgresql://localhost/spam*.
* Wprowadź użytkownika *username* i *hasło*.
* Kliknij przycisk **OK**.
* Witaj tooopen **połączenia** okna, kliknij dwukrotnie hello ***spamu bazy danych*** alias.
* Wybierz przycisk **Połącz**.

toorun niektóre kwerendy:

* Wybierz hello **SQL** kartę.
* Wprowadź na przykład prostego zapytania `SELECT * from data;` w polu tekstowym kwerendy hello u góry hello hello SQL karty.
* Naciśnij klawisz **Wprowadź Ctrl** toorun go. Domyślnie Squirrel SQL zwraca hello pierwszych 100 wierszy z zapytania.

Istnieje wiele zapytań więcej tooexplore można uruchomić te dane. Na przykład, jak hello częstotliwość hello word *upewnij* różnią się spamem i pichcisz?

    SELECT avg(word_freq_make), spam from data group by spam;

Lub co to są właściwości hello poczty e-mail, które często zawierają *3d*?

    SELECT * from data order by word_freq_3d desc;

Większość wiadomości e-mail, które mają wysokie wystąpienie *3d* są najwyraźniej wysyłania spamu, dlatego może być przydatne do tworzenia hello tooclassify model predykcyjny wiadomości e-mail.

Jeśli potrzebujesz uczenia maszynowego tooperform dane przechowywane w bazie danych programu PostgreSQL, rozważ użycie [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>Magazyn danych serwera SQL Server
Azure SQL Data Warehouse to oparta na chmurze i skalowalna w poziomie baza danych, która może przetwarzać ogromne ilości danych relacyjnych i nierelacyjnych. Aby uzyskać więcej informacji, zobacz [co to jest Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

dane toohello tooconnect magazynu i tworzenie tabeli hello hello uruchom następujące polecenie w wierszu polecenia:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Następnie w wierszu sqlcmd hello:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Kopiowanie danych za pomocą narzędzia bcp:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> zakończenia wierszy Hello w pobrany plik hello są styl systemu Windows, ale bcp oczekuje typu UNIX, potrzebujemy bcp tootell, że w programie hello flagi - r.
>
>

I zapytania przy użyciu narzędzia sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

Można także zbadać z Squirrel SQL. Należy wykonać podobne kroki w przypadku PostgreSQL hello sterownik JDBC serwera MSSQL firmy Microsoft, za pomocą której można znaleźć w ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Następne kroki
Omówienie tematów, które umożliwia przeprowadzenie zadań hello, wchodzące w skład procesu nauki danych hello na platformie Azure, zobacz [proces nauki danych zespołu](http://aka.ms/datascienceprocess).

Opis innych end-to-end wskazówki, które pokazują hello kroki hello proces nauki danych zespołu dla konkretnych scenariuszy, zobacz [wskazówki dotyczące procesu nauki danych zespołu](data-science-process-walkthroughs.md). wskazówki dotyczące Hello również ilustrują sposób toocombine w chmurze i lokalnie narzędzia i usługi do toocreate przepływu pracy lub potoku inteligentnego aplikacji.
