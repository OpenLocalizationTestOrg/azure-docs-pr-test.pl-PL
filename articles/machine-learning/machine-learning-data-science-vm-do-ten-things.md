---
title: "aaaTen sposobów na hello maszyny wirtualnej nauki danych | Dokumentacja firmy Microsoft"
description: "Wykonaj różne Eksploracja danych i zadań modelowania na powitania nauki danych maszyny wirtualnej."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Dziesięć czynności, które można wykonywać na powitania nauki danych maszyny wirtualnej
Witaj Microsoft danych nauki maszyny wirtualnej (DSVM) jest środowisko projektowe nauki zaawansowanych danych, umożliwiający tooperform można poszczególne zadania eksploracji i modelowania danych. Witaj środowisko zawiera już wbudowanych i powiązane z kilku popularnych danych narzędzia do analizy, dzięki któremu można łatwo tooget szybko rozpocząć z analizy dla lokalnych w chmurze czy hybrydowa wdrożeń. Witaj DSVM ściśle współpracuje z wielu usług Azure i jest w stanie tooread i przetwarzania danych, które są już przechowywane na platformie Azure, Magazyn danych SQL Azure, usługa Azure Data Lake, usługi Azure Storage lub w usłudze Azure DB rozwiązania Cosmos. Można też skorzystać innych narzędzi analizy, takich jak uczenie maszynowe Azure i fabryki danych Azure.

W tym artykule firma Microsoft przeprowadzi użytkownika przez proces jak toouse Twojego tooperform DSVM różnych nauki danych zadań i interakcję z innymi usługami Azure. Poniżej podano niektóre czynności hello, które można wykonać na powitania DSVM:

1. Eksplorowanie danych i tworzenie modeli lokalnie na powitania DSVM przy użyciu programu Microsoft Server R, Python
2. Użyj tooexperiment notesu Jupyter z danymi w przeglądarce przy użyciu języka Python, 2, Python 3 Microsoft R wersji gotowe enterprise elementu R, skalowalności i wydajności
3. Operacjonalizuj modele utworzony przy użyciu języków R i Python w usłudze Azure Machine Learning, aby aplikacje klienckie mogą uzyskiwać dostęp do modeli przy użyciu prostego interfejsu sieci web usług
4. Administrowanie zasobami platformy Azure przy użyciu portalu Azure lub programu Powershell
5. Rozszerzanie miejsca do magazynowania i udostępniania dużych zestawów danych / kodu w całym zespołem przez tworzenie usługi Magazyn plików Azure jako dysk instalację na DSVM Twojego
6. Udostępnianie kodu z zespołem przy użyciu usługi GitHub i uzyskać dostępu do repozytorium, używając hello wstępnie zainstalowane Git klienci - Git Bash Git graficznego interfejsu użytkownika.
7. Dostęp do różnych Azure danych i ich analiza usług przykład do magazynu obiektów blob platformy Azure, Azure Data Lake Azure HDInsight (Hadoop), bazy danych rozwiązania Cosmos platformy Azure, Magazyn danych SQL Azure & bazy danych
8. Twórz raporty i pulpit nawigacyjny za pomocą hello Power BI Desktop wstępnie zainstalowanych na powitania DSVM i wdrażanie ich w chmurze hello
9. Dynamiczne skalowanie toomeet Twojego DSVM, potrzebne w projekcie
10. Instalowanie dodatkowych narzędzi na maszynie wirtualnej   

> [!NOTE]
> Użycie dodatkowe opłaty dla wielu hello dodatkowe dane magazynu i analiza usług wymienionych w tym artykule. Zobacz toohello [cennik usługi Azure](https://azure.microsoft.com/pricing/) strony, aby uzyskać szczegółowe informacje.
> 
> 

**Wymagania wstępne**

* Potrzebujesz subskrypcji platformy Azure. Można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/free/).
* Instrukcje dotyczące obsługi danych maszyny wirtualnej nauki na powitania portalu Azure są dostępne pod adresem [tworzenia maszyny wirtualnej](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Eksplorowanie danych i tworzenie modeli przy użyciu programu Microsoft Server R lub Python
Można użyć w językach toodo R i Python z analizy danych bezpośrednio na powitania DSVM.

Dla języka R możesz użyć IDE o nazwie "Enterprise 8.0 obrotów R", który można znaleźć w hello start menu lub hello pulpitu. Firma Microsoft udostępnia dodatkowe biblioteki u góry hello Otwórz tooenable sieci CRAN-źródła R skalowalne analizy i hello możliwości tooanalyze danych większy niż rozmiar pamięci hello dozwolone w sposób równoległy podzielony analizy. Można także zainstalować IDE języka R z wyborem LIKE [programu RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Dla języka Python możesz użyć IDE, takich jak Visual Studio Community Edition, mającej hello narzędzi Python Tools dla wstępnie zainstalowane rozszerzenia programu Visual Studio (PTVS). Domyślnie tylko podstawowe środowisko Python 2.7 jest skonfigurowany na PTVS (bez żadnych biblioteki analizy, takich jak SciKit, Pandas). W kolejności tooenable Anaconda Python 2.7 i 3.5 należy toodo hello poniżej:

* Tworzenie niestandardowego środowiska dla każdej wersji przechodząc zbyt**narzędzia** -> **narzędzi Python Tools** -> **środowiska Python** , a następnie klikając polecenie " **+ Niestandardowe**"w hello Visual Studio 2015 Community Edition
* Wprowadź opis i ustawić hello środowiska ścieżki prefiks jako *c:\anaconda* Anaconda Python 2.7 lub *c:\anaconda\envs\py35* dla Anaconda Python 3.5
* Kliknij przycisk **Autowykrywanie** , a następnie **Zastosuj** toosave hello środowiska.

Oto ustawieniach niestandardowych środowiska hello wygląda jak w programie Visual Studio.

![Instalator PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Zobacz hello [dokumentacji PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) dodatkowe informacje na temat toocreate środowiska Python.

Teraz możesz ustawiono toocreate nowy projekt języka Python. Przejdź za**pliku** -> **nowy** -> **projektu** -> **Python** i wybierz typ hello Aplikacja języka Python, które tworzysz. Można ustawić środowiska Python hello hello bieżącego projektu toohello wymaganej wersji (Anaconda 2.7 lub 3.5): kliknij prawym przyciskiem myszy hello **środowiska Python**, wybierz pozycję **środowiska Python Dodaj lub usuń**, i następnie wybierz hello żądana tooassociate środowisko z hello projektu. Można znaleźć więcej informacji na temat pracy z narzędziami PTVS produktu hello [dokumentacji](https://github.com/Microsoft/PTVS/wiki) strony.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Używanie tooexplore notesu Jupyter i modelu danych z programem Python lub R
Witaj notesu Jupyter jest zaawansowane środowisko, które zapewnia przeglądarki "IDE" Eksploracja danych i modelowania. Można użyć języka Python, 2, Python 3 lub R (Open Source i hello Microsoft R Server) w notesu Jupyter.

Witaj toolaunch notesu Jupyter kliknij ikonę menu start hello / zatytułowany ikony pulpitu **notesu Jupyter**. Na powitania DSVM możesz również przejść za "https://localhost:9999 /" tooaccess hello Jupiter notesu. Jeśli monituje o podanie hasła, użyj instrukcji podanych w hello ***jak toocreate silnego hasła na serwerze notesu Jupyter hello*** sekcji hello [hello udostępniania maszyny wirtualnej nauki danych Microsoft](machine-learning-data-science-provision-vm.md)toocreate tematu notesu Jupyter hello tooaccess silne hasło. 

Po otwarciu notesu hello katalog, który zawiera kilka notesów przykładzie, które są wstępnie utworzonych pakietów do hello DSVM powinna zostać wyświetlona. Teraz możesz:

* polecenie hello notesu toosee hello kodu.
* Wykonanie każdej komórki naciskając **wprowadź SHIFT**.
* Uruchom hello cały notes klikając **komórki** -> **Uruchom**
* Tworzenie nowego notesu kliknięcie hello Jupyter ikona (w lewym górnym rogu), a następnie klikając polecenie **nowy** przycisk na powitania prawo, a następnie wybierając hello notesu języka (znanej także jako jądra).   

> [!NOTE]
> Obecnie firma Microsoft obsługuje Python 2.7, Python 3.5 i R. jądra hello R obsługuje programowanie w zarówno typu Open source R, jak i hello enterprise skalowalne Microsoft R Server.   
> 
> 

Po przejściu w notesie hello można eksplorować dane, budowanie modelu hello, model hello przy użyciu bibliotek wybór testów.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Tworzenie modeli przy użyciu R lub Python i Operationalize je za pomocą usługi Azure Machine Learning
Po wbudowane i sprawdzić poprawności modelu hello następnym krokiem jest zwykle toodeploy go w środowisku produkcyjnym. Dzięki temu klient aplikacji tooinvoke hello modelu prognozy w czasie rzeczywistym lub na podstawie trybu partii. Usługa Azure Machine Learning zapewnia toooperationalize mechanizmu model wbudowane R lub Python.

Gdy użytkownik operacjonalizować model w usłudze Azure Machine Learning, usługi sieci web jest narażony, umożliwiającą klientom toomake wywołania REST, które należy przekazać w parametrach wejściowych i otrzymywać prognoz hello modelu jako dane wyjściowe.   

> [!NOTE]
> Jeśli użytkownik ma nie jeszcze zarejstrowano w usłudze Azure Machine Learning, odwiedzając hello można uzyskać wolnego obszaru roboczego lub standardowy obszaru roboczego [Azure Machine Learning Studio](https://studio.azureml.net/) strony głównej i kliknięcie na "wprowadzenie".   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Kompilowanie i Python Operacjonalizuj modele
Oto fragment kodu w notesu Jupyter Python korzystająca z modelu prostego za pomocą biblioteki informacje SciKit hello.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

Metoda Hello używane toodeploy Twojego python tooAzure modeli uczenia maszynowego zawija hello prognozowania modelu hello funkcji i decorates go z atrybutami podał hello wstępnie zainstalowane usługi Azure Machine Learning biblioteka języka python, które oznaczają komputerze Azure Identyfikator obszaru roboczego uczenia, klucz interfejsu API i hello danych wejściowych i zwracać parametrów.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Klient może teraz utworzyć usługi sieci web toohello wywołania. Brak otoki wygody, które skonstruować hello żądania interfejsu API REST. Oto przykładowy kod tooconsume hello sieci web usługi.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> Biblioteka usługi Azure Machine Learning Hello jest obsługiwana tylko na Python 2.7 obecnie.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Modele kompilacji i Operacjonalizacji R
Można wdrożyć modeli R zbudowane na powitania maszyny wirtualnej nauki danych lub w innym miejscu na uczenie maszynowe Azure w taki sposób, który jest podobne toohow, które jest wykonywane dla języka Python. Jej hello kroków:

* Utwórz tooprovide pliku settings.json, uwierzytelniania i identyfikator obszaru roboczego, na których token pokazane na powitania po przykładowy kod.
* Funkcja prognozowania modelu hello zapisać otokę.
* wywołanie ```publishWebService``` w hello toopass biblioteki usługi Azure Machine Learning w hello funkcja otoki.  

Oto wstawki procedurą i kod hello, które można tooset używane górę, kompilacji, publikowania i zużywać model jako usługę sieci web w usłudze Azure Machine Learning.

#### <a name="setup"></a>Konfiguracja
1. Zainstaluj pakiet Machine Learning R hello wpisując ```install.packages("AzureML")``` w porównaniu R Enterprise 8.0 IDE lub środowiskiem IDE R.
2. Pobierz RTools z [tutaj](https://cran.r-project.org/bin/windows/Rtools/). Należy toooperationalize narzędzie Ścieżka hello (i nazwane zip.exe) zip hello pakietu R do uczenia maszynowego.
3. Utwórz plik settings.json w obszarze katalog o nazwie ```.azureml``` w katalogu macierzystym i wprowadź parametry hello z obszaru roboczego uczenia maszynowego Azure:

Settings.JSON struktury plików:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Tworzenie modelu w R i opublikować ją w usłudze Azure Machine Learning
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Korzystanie z modelu hello wdrożony w usłudze Azure Machine Learning
model hello tooconsume od aplikacji klienckiej, używamy toolook biblioteki usługi Azure Machine Learning hello zapasowej hello opublikowane usługi sieci web wg nazwy przy użyciu hello `services` punkt końcowy hello toodetermine wywołania interfejsu API. Następnie po prostu Wywołaj hello `consume` funkcji i podaj toobe ramki danych hello przewidzieć.
Witaj następującego kodu to model hello tooconsume używane publikowane jako usługi sieci web uczenie maszynowe Azure.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Więcej informacji na temat hello Azure Machine Learning R biblioteki można znaleźć [tutaj](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Administrowanie zasobami platformy Azure przy użyciu portalu Azure lub programu Powershell
Witaj DSVM nie zezwala tylko toobuild Twojego rozwiązania analizy lokalnie na hello maszyny wirtualnej, ale można też tooaccess usług w chmurze Azure firmy Microsoft. Platforma Azure udostępnia kilka obliczeń, magazynu, usługi analizy danych i innych usług, które mogą administrować i uzyskać dostęp z Twojej DSVM.

tooadminister zasobami subskrypcji i w chmurze Azure można użyć przeglądarki i toothe punktu [portalu Azure](https://portal.azure.com). Umożliwia także tooadminister programu Azure Powershell Twojej subskrypcji platformy Azure i zasobów za pomocą skryptu.
Można uruchomić programu Azure Powershell przy użyciu skrótu na pulpicie hello, lub z hello start menu zatytułowany "Microsoft Azure Powershell". Zapoznaj się [dokumentacji programu Microsoft Azure Powershell](../powershell-azure-resource-manager.md) Aby uzyskać więcej informacji na temat sposobu do administrowania subskrypcji platformy Azure i zasobów za pomocą skryptów programu Windows Powershell.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Rozszerzanie miejsca do magazynowania w systemie plików udostępnionych
Analityków danych można udostępniać dużych zestawów danych, kodu lub innych zasobów w ramach hello zespołu. Witaj DSVM sam ma około 70GB dostępnego miejsca. tooextend Twojego magazynu, można użyć hello Azure usługi plików i zainstalować go na powitania DSVM lub uzyskać do niego dostęp za pośrednictwem interfejsu API REST.   

> [!NOTE]
> Maksymalna ilość miejsca Hello hello Azure usługa plików udziału jest 5TB i limit rozmiaru poszczególnych plików wynosi 1TB.   
> 
> 

Możesz użyć programu Azure Powershell toocreate udziału usługa plików Azure. Oto hello toorun skryptu w obszarze toocreate programu Azure PowerShell udział plików Azure usługi.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Teraz, po utworzeniu udziału plików na platformę Azure, możesz go zainstalować w żadnej maszyny wirtualnej na platformie Azure. Zaleca się, że hello maszyna wirtualna jest w tym samym centrum danych Azure jako hello magazynu konta tooavoid opóźnienia i danych opłat za transfer. Poniżej przedstawiono hello polecenia toomount hello dysku na powitania DSVM, która może działać na programu Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Teraz jak w przypadku dowolnego normalne dysku na powitania maszyny Wirtualnej można dostępu do dysku.

## <a name="6-share-code-with-your-team-using-github"></a>6. Udostępnianie kodu z zespołem przy użyciu usługi GitHub
GitHub jest repozytorium kodu, gdzie można znaleźć wiele przykładowy kod i źródła dla różnych narzędzi z użyciem różnych technologii udostępnione przez społeczność deweloperów hello. Jak hello technologii tootrack, a także przechowywać wersje plików kodu hello jest używany Git. GitHub jest również platformy umożliwiającego utworzenie własnych repozytorium toostore Twojego zespołu udostępnionego kodu i dokumentacji zaimplementować kontroli wersji i również kontroli którzy tooview dostępu i współtworzenia kodu. Odwiedź stronę hello [GitHub strony pomocy](https://help.github.com/) uzyskać więcej informacji na temat używania narzędzia Git. Można użyć GitHub wśród toocollaborate sposoby hello z zespołem, użyj kodu opracowanych przez społeczność hello i współtworzenia społeczności wstecz toohello kodu.

Hello DSVM już zawiera załadowane z narzędziami klienckimi zarówno wiersza polecenia, jak dobrze tooaccess graficznego interfejsu użytkownika repozytorium GitHub. Witaj toowork narzędzia wiersza polecenia Git i GitHub jest nazywany Git Bash. Visual Studio zainstalowanych na powitania DSVM ma hello Git. Ikony rozruchu można znaleźć dla tych narzędzi w hello start menu i hello pulpitu.

Kod toodownload z repozytorium GitHub używasz hello ```git clone``` polecenia. Na przykład repozytorium nauki danych toodownload opublikowane przez firmę Microsoft do bieżącego katalogu hello można uruchomić hello następujące polecenia, po przejściu do ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

W programie Visual Studio, czy hello tej samej operacji klonowania. powitania po zrzut ekranu pokazuje, jak tooaccess Git i GitHub narzędzia w programie Visual Studio.

![Git w programie Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Można znaleźć więcej informacji dotyczących korzystania z repozytorium GitHub z kilku zasobów dostępnych w witrynie github.com Git toowork. Witaj [ściągawka](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) jest przydatne odwołanie.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Dostęp do różnych usług Azure danych i ich analiza
### <a name="azure-blob"></a>Obiekt bob Azure
Obiektów blob platformy Azure to niezawodne, ekonomiczny chmurze magazynu danych dużych i małych. Daj nam przyjrzeć się, jak można przenosić tooAzure danych obiektów Blob i uzyskiwanie dostępu do danych przechowywanych w obiekcie Blob Azure.

**Wymagania wstępne**

* **Tworzenie konta magazynu obiektów Blob platformy Azure z [portalu Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Upewnij się, że hello wstępnie zainstalowane narzędzie wiersza polecenia AzCopy znajduje się na ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Podczas uruchamiania tego narzędzia można dodać hello zawierającego hello azcopy.exe tooyour ŚCIEŻKA środowiska zmiennej tooavoid pisania hello pełne polecenie ścieżki katalogu. Aby uzyskać więcej informacji na temat narzędzia AzCopy można znaleźć zbyt[dokumentację programu AzCopy](../storage/common/storage-use-azcopy.md)
* Uruchom narzędzie Eksploratora usługi Storage Azure hello. Można go pobrać z [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Przenoszenia danych z maszyny Wirtualnej tooAzure obiektu Blob: AzCopy**

toomove danych między lokalnych plików i magazynu obiektów blob, AzCopy można użyć w wierszu polecenia lub środowiska PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Zastąp **C:\myfolder** przechowywania pliku, ścieżka toohello **mojekontomagazynu** tooyour nazwy konta magazynu obiektów blob, **mojkontener** nazwę kontenera toohello **klucz konta magazynu** klucz dostępu do magazynu obiektów blob tooyour. Można znaleźć poświadczeń konta magazynu w [portalu Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Uruchom polecenie AzCopy, programu PowerShell lub z wiersza polecenia. Poniżej przedstawiono niektóre Przykładowe użycie polecenia programu AzCopy:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Po uruchomieniu programu AzCopy polecenia toocopy tooan obiektów blob platformy Azure, zobacz plik zostaną wyświetlone w Eksploratorze usługi Storage Azure wkrótce.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Przenoszenia danych z maszyny Wirtualnej tooAzure obiektu Blob: Eksploratora usługi Storage platformy Azure**

Możesz również przekazywać dane z pliku lokalnego hello w maszynie Wirtualnej za pomocą Eksploratora usługi Storage platformy Azure:

* kontener tooa danych tooupload, hello wybierz docelowy kontener i kliknij przycisk hello **przekazać** przycisku.![ Przekazywanie do Eksploratora usługi Storage](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Polecenie hello **...**  toohello rogu hello **pliki** wybierz jednego lub wielu tooupload pliki z systemu plików hello a kliknij **przekazać** toobegin przekazywania plików hello.![ Przekazywanie plików tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Odczytywanie danych z obiektów Blob platformy Azure: moduł czytnika uczenia maszynowego**

W usłudze Azure Machine Learning Studio można użyć **modułu importu danych** tooread dane z Twojego obiektu blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Odczytywanie danych z obiektów Blob platformy Azure: Python ODBC**

Można użyć **BlobService** biblioteki tooread danych bezpośrednio z obiektu blob w programie notesu Jupyter lub Python.

Po pierwsze zaimportuj wymagane pakiety:

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Następnie podłącz poświadczeń konta obiektów Blob platformy Azure i odczytywanie danych z obiektu Blob:

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

dane Hello jest do odczytu jako ramki danych:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Azure Data Lake Storage to repozytorium hiperskali obciążeń analizy danych big data i zgodny z Hadoop Distributed pliku System (HDFS). Działa z ekosystemem Hadoop hello i hello Azure Data Lake Analytics. Zostanie przedstawiony sposób przenoszenia danych do hello Azure Data Lake Store i uruchom analytics przy użyciu usługi Azure Data Lake Analytics.

**Wymagania wstępne**

* Tworzenie z usługą Azure Data Lake Analytics w [portalu Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Witaj **Azure Data Lake Tools** w **programu Visual Studio** znaleziono w tej [łącze](https://www.microsoft.com/download/details.aspx?id=49504) jest już zainstalowana na powitania Visual Studio Community Edition, który znajduje się na maszynie wirtualnej hello. Po uruchomieniem programu Visual Studio i rejestrowanie w Twojej subskrypcji platformy Azure, powinna zostać wyświetlona Twoje konto usługi Azure Data Analytics i magazynu w lewym panelu hello programu Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Przenoszenia danych z maszyny Wirtualnej tooData Lake: Azure Data Lake Explorer**

Można użyć **Azure Data Lake Explorer** tooupload danych z plików lokalne powitania w Twoim magazynie Lake tooData maszyny wirtualnej.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

Można również tworzyć tooproductionize potoku danych Twojej tooor przeniesienia danych z usługi Azure Data Lake za pomocą hello [Factory(ADF) danych Azure](https://azure.microsoft.com/services/data-factory/). Firma Microsoft możesz znaleźć toothis [artykułu](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide przez hello kroki toobuild hello danych potoków.

**Odczytywanie danych z usługi Azure Blob tooData Lake: U-SQL**

Jeśli dane znajdują się w magazynie obiektów Blob platformy Azure, mogą bezpośrednio odczytywać dane z obiektu blob magazynu Azure w zapytaniu U-SQL. Przed tworzenia kwerendy U-SQL, upewnij się, że Twoje konto magazynu obiektów blob jest tooyour połączonej usługi Azure Data Lake. Przejdź za**portalu Azure**, Znajdź pulpitu nawigacyjnego usługi Azure Data Lake Analytics, kliknij przycisk **Dodaj źródło danych**, wybierz typ magazynu zbyt**usługi Azure Storage** i dołączyć usługi magazynu Azure Nazwa konta i klucz. To może tooreference hello danych przechowywanych w hello konta magazynu.

![Wprowadź konto magazynu i klucz](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

W programie Visual Studio można odczytać danych z magazynu obiektów blob, niektóre manipulowania danymi, inżynieria funkcji i danych wyjściowych hello wynikowy danych tooeither usługi Azure Data Lake lub magazynu obiektów Blob Azure. Podając odniesienie hello danych w magazynie obiektów blob, użyj **wasb: / /**; w przypadku odwołania hello danych w usłudze Azure Data Lake, użyj **swbhdfs: / /**

![Ramki danych](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Może używać powitania po zapytań U-SQL w programie Visual Studio:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Zapytanie po serwera toohello przesłane diagram przedstawiający hello stan zadania jest wyświetlany.

![Diagram stanu zadania](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Zapytania na danych w usłudze Data Lake: U-SQL**

Po hello dataset jest pozyskanych w usłudze Azure Data Lake, można użyć [języka U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery i eksplorować dane hello. Języka U-SQL jest podobne tooT-SQL, ale łączy niektóre funkcje w języku C#, dzięki czemu użytkownicy mogą zapisywać niestandardowych modułów, funkcje zdefiniowane przez użytkownika i itp. Można użyć skryptów hello hello poprzedniego kroku.

Po tooserver przesłane, tripdata_summary hello zapytania. CSV znajdują się wkrótce w **Azure Data Lake Explorer**, można podejrzeć hello danych przez plik powitania kliknij prawym przyciskiem myszy.

![Plik w Eksploratorze Lake danych Azure](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

informacje o pliku hello toosee:

![Podsumowanie pliku](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Klastrów HDInsight Hadoop
Usługa Azure HDInsight to zarządzana usługa Apache Hadoop, Spark, HBase i Storm w chmurze hello. Można łatwo pracować z klastrami Azure HDInsight z maszyny wirtualnej nauki danych hello.

**Wymagania wstępne**

* Tworzenie konta magazynu obiektów Blob platformy Azure z [portalu Azure](https://portal.azure.com). To konto magazynu jest danych toostore używanej dla klastrów usługi HDInsight.

![Tworzenie konta magazynu obiektów Blob platformy Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Dostosowywanie Azure platforma Hadoop w usłudze Hdinsight z [portalu Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Należy połączyć hello konta magazynu utworzone z klastrem usługi HDInsight podczas jego tworzenia. To konto magazynu jest używane do uzyskiwania dostępu do danych, które mogą być przetwarzane w ramach klastra hello.

![Konto toostorage łącze utworzone z klastrem usługi HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Należy włączyć **dostępu zdalnego** toohello węzła głównego klastra powitania po jego utworzeniu. Pamiętaj poświadczenia dostępu zdalnego hello określone w tym miejscu (różne od tych określonych hello klastra podczas jego tworzenia): potrzebne w następnej procedurze hello.

![Włączenie dostępu zdalnego](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Utwórz obszar roboczy usługi Azure Machine Learning. Z uczeniem maszynowym są przechowywane w tym obszaru roboczego uczenia maszynowego. Wybierz opcje hello wyróżniane w portalu, jak pokazano w powitania po zrzut ekranu:

![Tworzenie obszaru roboczego usługi Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Następnie wprowadź parametry hello obszaru roboczego

![Wprowadź parametry obszaru roboczego uczenia maszynowego](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Przekazywanie danych za pomocą notesu IPython. Najpierw zaimportuj wymagane pakiety, podłącz poświadczeń, Utwórz bazę danych na koncie magazynu, a następnie załadować klastry tooHDI danych.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* Alternatywnie można to wykonać [wskazówki](machine-learning-data-science-process-hive-walkthrough.md) tooupload taksówki NYC danych tooHDI klastra. Główne kroki obejmują:
  
  * Narzędzie AzCopy: Pobierz zip CSV z folderu lokalnego tooyour publicznego obiektu blob
  * Narzędzie AzCopy: Przekaż rozpakowane udostępnionych woluminach Klastra z folderu lokalnego tooHDI klastra
  * Zaloguj się do hello węzła głównego klastra usługi Hadoop i Przygotuj się do analizy danych poznawcze

Po danych hello jest załadowany tooHDI klastra, można sprawdzić dane w Eksploratorze usługi Storage platformy Azure. I masz nyctaxidb bazy danych, utworzonych w klastra HDI.

**Eksploracja danych: zapytań programu Hive w języku Python**

Ponieważ hello dane pochodzą z klastra usługi Hadoop, może użyć hello pyodbc pakietu tooconnect tooHadoop klastrów i kwerendy bazy danych przy użyciu Hive toodo eksploracji i inżynieria funkcji. Witaj istniejące tabele, utworzone w kroku wymagań wstępnych hello jest widoczny.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Wyświetlanie istniejących tabel](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Przyjrzyjmy się hello liczby rekordów w każdym miesiącu i hello częstotliwości Przechylony lub nie znajduje się w tabeli podróży hello:

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Wykres liczby rekordów w każdym miesiącu](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Wykres programu końcówkę częstotliwości](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

Możemy również obliczeniowe hello odległości między lokalizacją podnoszenia dropoff lokalizacji i porównania go po toohello rzeczy przed wyjazdem odległości.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Odbiór i dropoff tabeli](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Wykres odległość tootrip odległość podnoszenia/dropoff](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Teraz załóżmy przygotowanie próbkowany down (1%) zbiór danych do modelowania. Możemy użyć tych danych w module czytnika uczenia maszynowego.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Po chwili można zauważyć, że dane hello został załadowany w klastrów platformy Hadoop:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabela danych](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Odczytywanie danych z HDI za pomocą uczenia maszynowego: moduł czytnika**

Można także użyć hello **czytnika** modułu w bazie danych hello tooaccess Machine Learning Studio w klastra usługi Hadoop. Podłącz hello poświadczeń klastrów HDI i konto magazynu Azure tooenable tworzenie modeli przy użyciu bazy danych w klastrach HDI uczenia maszynowego lasycznego, dokującego.

![Właściwości modułu Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Witaj scored zestaw danych można następnie wyświetlić:

![Widok oceniane zestawu danych](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>& Baz danych Azure SQL Data Warehouse
Usługa Azure SQL Data Warehouse jest magazyn danych elastycznej jako usługi za pomocą klasy korporacyjnej środowisko programu SQL Server.

Azure SQL Data Warehouse można udostępnić, wykonując następujące instrukcje hello podane w tym [artykułu](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Po zainicjowanie obsługi usługi Azure SQL Data Warehouse, możesz użyć tej funkcji [wskazówki](machine-learning-data-science-process-sqldw-walkthrough.md) przekazywanie danych toodo, badanie i modelowania przy użyciu danych w ramach hello SQL Data Warehouse.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure DB rozwiązania Cosmos jest bazą danych NoSQL w chmurze hello. Pozwala toowork z dokumentami, takich jak JSON, a pozwala dokumentów hello toostore i zapytania.

Należy hello toodo po tooaccess kroki na wymagania bazy danych Azure rozwiązania Cosmos z hello DSVM.

1. Zainstaluj zestaw SDK Python usługi DocumentDB (Uruchom ```pip install pydocumentdb``` z wiersza polecenia)
2. Tworzenie konta bazy danych Azure rozwiązania Cosmos i bazę danych z [portalu Azure](https://portal.azure.com)
3. Pobierz "Narzędzie migracji DB rozwiązania Cosmos Azure" z [tutaj](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) i wyodrębniać tooa katalogu
4. Importuj dane JSON (dane swe dzieła) przechowywanych w [publicznego obiektu blob](https://cahandson.blob.core.windows.net/samples/volcano.json) w bazie danych rozwiązania Cosmos przy użyciu narzędzia migracji toohello parametry polecenia następujące (dtui.exe z katalogu hello zainstalowaną hello rozwiązania Cosmos narzędzia do migracji bazy danych). Wprowadź lokalizację źródłowa i docelowa hello z następującymi parametrami:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/; AccountKey = [[klucz]; Baza danych = /t.Collection:volcano1 swe dzieła

Po zaimportowaniu danych hello, możesz przejść tooJupyter i otwórz hello notesu zatytułowany *DocumentDBSample* zawierającą python code tooaccess usługi DocumentDB i czy niektóre podstawowe zapytań. Możesz dodatkowe informacje na temat rozwiązania Cosmos DB, przechodząc na stronę usługi hello [stronę dokumentacji](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Twórz raporty i pulpit nawigacyjny za pomocą hello Power BI Desktop
Daj nam wizualizacji pliku JSON swe dzieła hello, którą widzieliśmy w hello poprzedzających przykład DB rozwiązania Cosmos w usłudze Power BI toogain visual wgląd w dane hello. Szczegółowy opis kroków są dostępne w hello [artykułu usługi Power BI](../cosmos-db/powerbi-visualize.md). Poniżej przedstawiono ogólne kroki hello:

1. Otwórz Power BI Desktop i wykonaj "Pobierz dane". Określ adres URL hello: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Powinny pojawić zaimportowany jako listę rekordów JSON hello
3. Konwertuj Tabela tooa listy hello dzięki usłudze Power BI można pracować z hello takie same
4. Rozwiń kolumny hello, klikając hello Rozwiń ikonę (hello jedną ikoną "Strzałka w lewo i Strzałka w prawo" hello na powitania rogu hello kolumny)
5. Należy zauważyć, że lokalizacja znajduje się pole "Rekordu". Rozwiń hello rekordu i wybierz tylko hello współrzędnych. Współrzędna jest kolumna listy
6. Dodaj nową kolumnę tooconvert hello listy współrzędnych kolumnę do przecinkami osobna kolumna LatLong łączenie hello dwa elementy w polu listy współrzędnych hello przy użyciu formuły hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Na koniec przekonwertować hello ```Elevation``` tooDecimal kolumny i wybierz hello **Zamknij** i **Zastosuj**.

Zamiast poprzednich krokach, możesz wkleić hello następującego kodu, który skrypty czynności hello używane w hello Zaawansowany edytor w usłudze Power BI umożliwia przekształcenia danych hello toowrite język kwerendy.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Masz teraz hello danych w modelu danych usługi Power BI. Usługa Power BI pulpitu powinna wyglądać następująco:

![Program Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Można rozpocząć tworzenie raportów i wizualizacje przy użyciu hello modelu danych. Możesz wykonać kroki hello na tym [artykułu usługi Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild raportu. wynik końcowy Hello jest raport, który wygląda hello.

![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Dynamiczne skalowanie toomeet Twojego DSVM, potrzebne w projekcie
Możesz skalować toomeet DSVM hello, który projekt w górę i w dół. Jeśli nie potrzebujesz hello toouse maszyny Wirtualnej w hello wieczorem lub w weekendy, można po prostu zamknąć hello maszyny Wirtualnej z hello [portalu Azure](https://portal.azure.com).

> [!NOTE]
> Ponosisz opłat za obliczenia, jeśli używasz tylko hello przycisku zamknięcia systemu operacyjnego na powitania maszyny Wirtualnej.  
> 
> 

Jeśli konieczne toohandle analizy dużych i potrzebujesz większej pojemności procesora CPU, pamięć lub dysk można znaleźć wybór dużych rozmiarów maszyn wirtualnych w postaci liczby rdzeni Procesora, pamięci i typów dysków (w tym dysków półprzewodnikowych), które spełniają Twoich potrzeb dotyczących budżetowych i obliczeń. Witaj Pełna lista maszyn wirtualnych wraz z ich ceny co godzinę obliczeń jest dostępna na powitania [cennik maszyn wirtualnych Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) strony.

Podobnie jeśli zmniejsza potrzeby wydajności przetwarzania maszyny Wirtualnej (na przykład: przenieść tooa najważniejszych obciążeń Hadoop lub w klastrze Spark), można skalować w dół hello klastra z hello [portalu Azure](https://portal.azure.com) i będą toohello ustawienia maszyny wirtualnej wystąpienie. Poniżej przedstawiono zrzut ekranu.

![Ustawienia wystąpienie maszyny Wirtualnej](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Instalowanie dodatkowych narzędzi na maszynie wirtualnej
Firma Microsoft ma spakowane kilka narzędzi, które mamy nadzieję, że są w stanie tooaddress wielu hello wspólne dane analizy potrzeb, a powinien zaoszczędzić czas, przez co pozwala uniknąć konieczności tooinstall i konfigurowanie środowiska jeden po drugim i oszczędność pieniędzy przez płatności tylko dla zasobów, które Użycie.

Można korzystać z innych danych Azure i usługi analizy profilowane w tym artykule tooenhance środowiska analytics. Zdajemy w niektórych przypadkach potrzeb może wymagać dodatkowych narzędzi, w tym niektórych zastrzeżonych innych firm. Masz pełny dostęp administracyjny na powitania maszyny wirtualnej tooinstall nowe narzędzia potrzebne. Można także zainstalować dodatkowe pakiety Python i R, które nie są wstępnie zainstalowane. Dla języka Python możesz użyć dowolnej ```conda``` lub ```pip```. R można użyć hello ```install.packages()``` w hello R konsoli lub za pomocą hello IDE i wybierz "**pakiety** -> **instalowanie pakietów** ".

## <a name="summary"></a>Podsumowanie
Są to tylko niektóre hello czynności, które można wykonać na powitania maszyny wirtualnej nauki danych firmy Microsoft. Istnieje wiele więcej sposobów toomake go środowisku analytics skuteczne.

