---
title: Witaj aaaProvision maszyny wirtualnej nauki danych firmy Microsoft | Dokumentacja firmy Microsoft
description: "Konfigurowanie i Utwórz maszynę wirtualną nauki danych na platformie Azure w celu wykonania analizy i uczenia maszynowego."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Zainicjuj obsługę hello maszyny wirtualnej nauki danych firmy Microsoft
Maszyny wirtualnej nauki danych Microsoft Hello jest obraz maszyny wirtualnej (VM) systemu Windows Azure wstępnie zainstalowany i skonfigurowany z kilku popularnych narzędzi, które są często używane do analizy danych i uczenia maszynowego. narzędzia Hello uwzględnione są:

* Microsoft R Server Developer Edition
* Dystrybucję oprogramowania Python anaconda
* Notesu Jupyter (z R, Python jądra)
* Visual Studio Community Edition
* Program Power BI Desktop
* SQL Server 2016 Developer Edition
* Uczenie maszynowe i narzędzia do analizy danych
  * [Obliczeniowa sieci Toolkit (CNTK)](https://github.com/Microsoft/CNTK): bezpośrednie uczenia toolkit oprogramowania Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): szybki komputer uczenia systemu obsługującego technik, takich jak online, wyznaczania wartości skrótu, allreduce, redukcji, learning2search, aktywna i uczenie się interakcyjne.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): narzędzie, zapewniając szybkie i dokładne boosted drzewa wykonania.
  * [Rattle](http://rattle.togaware.com/) (łatwo hello tooLearn narzędzie analityczne R): narzędzie, które umożliwia wprowadzenie do analizy danych i machine learning w R, udostępniając Eksploracja danych z Graficznym interfejsem użytkownika i modelowanie z automatycznego generowania kodu języka R.
  * [mxnet](https://github.com/dmlc/mxnet): struktury głębokie nauki przeznaczony dla wydajność i elastyczność
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : wyszukiwania danych wizualnych i oprogramowania w języku Java uczenia maszynowego.
  * [Przechodzenie do szczegółów Apache](https://drill.apache.org/): aparatu zapytań SQL bez schematu dla platformy Hadoop, NoSQL i magazynu w chmurze.  Obsługuje ODBC i JDBC tooenable interfejsy badania NoSQL i pliki ze standardowych narzędzi do analizy Biznesowej, takich jak usługi Power BI, Excel, Tableau.
* Biblioteki języka R i Python dla programu uczenie maszynowe Azure i innych usług Azure
* W tym toowork Git Bash z tym GitHub, Visual Studio Team Services repozytoriach kodów źródłowych Git
* Porty Windows kilku popularnych Linux narzędzia wiersza polecenia (w tym awk, mniejszyć, perl, grep, znajdowanie, wget, curl itp.) dostępny za pośrednictwem wiersza polecenia. 

Podczas analizy danych obejmuje iteracja w sekwencji zadań:

1. Znajdowanie, ładowania i wstępne przetworzenie danych
2. Tworzenie i testowanie modeli
3. Wdrażanie modeli hello do wykorzystania w aplikacji inteligentnego

Analityków danych użycia różnych narzędzi toocomplete tych zadań. Go może być bardzo czasochłonne toofind hello odpowiedniej wersji oprogramowania hello, a następnie Pobierz i zainstaluj je. Hello maszyny wirtualnej nauki danych firmy Microsoft może ułatwić to obciążenie poprzez dostarczanie obrazu gotowe do użycia, które można udostępnić na platformie Azure wszystkich kilka narzędzi popularnych wstępnie zainstalowane i skonfigurowane. 

Maszyny wirtualnej nauki danych Microsoft Hello jump-starts projektu analizy. Umożliwia toowork zadań w różnych językach, w tym R, Python, SQL i C#. Visual Studio udostępnia toodevelop IDE i przetestować swój kod, który jest łatwo toouse. Hello objęte hello maszyny Wirtualnej zestawu SDK platformy Azure pozwala toobuild aplikacji przy użyciu różnych usług na platformy w chmurze firmy Microsoft. 

Nie ma żadnych opłat oprogramowania dla tego obrazu maszyny Wirtualnej do analizy danych. Płacisz tylko za hello Azure użycia opłat które w zależności od rozmiaru hello hello maszyny wirtualnej, które należy udostępnić. Więcej informacji na temat hello obliczeniowe opłaty znajdują się w hello sekcja szczegóły cennik na powitania [maszyny wirtualnej nauki danych](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) strony. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Inne wersje hello maszyny wirtualnej nauki danych
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) obrazu jest również dostępna, z wieloma hello narzędzi takie same jak hello obrazu systemu Windows. [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) obraz jest dostępny, jak również w przypadku wielu podobne narzędzia oraz bezpośrednich uczenia struktury.

## <a name="prerequisites"></a>Wymagania wstępne
Przed utworzeniem maszyny wirtualnej nauki danych firmy Microsoft, musi mieć następujące hello:

* **Subskrypcji platformy Azure**: jeden, zobacz tooobtain [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Konto magazynu platformy Azure**: jeden, zobacz toocreate [utworzyć konto magazynu platformy Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Alternatywnie można utworzyć konta magazynu hello jako część procesu hello tworzenia hello maszyny Wirtualnej, jeśli nie chcesz, aby toouse istniejącego konta.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Tworzenie maszyny wirtualnej nauki danych firmy Microsoft
Oto toocreate kroki hello wystąpienia hello maszyny wirtualnej nauki danych firmy Microsoft:

1. Przejdź do wyświetlania na maszynie wirtualnej toohello [portalu Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Wybierz hello **Utwórz** u toobe dolnej hello uwzględnić kreatora.![ Konfigurowanie danych nauki vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Witaj kreatora używanego toocreate Witaj maszyna wirtualna nauki danych firmy Microsoft wymaga **dane wejściowe** dla każdego hello **pięć kroków** wyliczyć na powitania rogu tego rysunku. Poniżej przedstawiono hello potrzebne dane wejściowe tooconfigure każdego z następujących czynności:
   
   1. **Podstawy**
      
      1. **Nazwa**: Nazwa serwera nauki danych tworzona.
      2. **Nazwa użytkownika**: identyfikator logowania konta administratora.
      3. **Hasło**: hasło konta administratora.
      4. **Subskrypcja**: Jeśli masz więcej niż jedną subskrypcję, wybierz jedną na które hello maszyna jest toobe utworzone i rozliczane hello.
      5. **Grupy zasobów**: można utworzyć nowej lub istniejącej grupy.
      6. **Lokalizacja**: hello wybierz centrum danych, która jest najbardziej odpowiednia. Zazwyczaj jest hello centrum danych, która zawiera większość danych lub najbliższej lokalizacji fizycznej tooyour najszybszy dostęp do sieci.
   2. **Rozmiar**: Wybierz jeden z typów powitania serwera, które spełnia Twoje wymagania funkcjonalne i ograniczenia kosztów. Więcej opcji dotyczących rozmiarów maszyn wirtualnych można uzyskać, wybierając polecenie "Wyświetl wszystko".
   3. **Ustawienia**:
      
      1. **Typ dysku**: Wybierz Premium również dysków półprzewodnikowych (SSD), przeciwnym razie wybierz "Standard".
      2. **Konto magazynu**: można utworzyć nowe konto magazynu Azure w ramach subskrypcji lub użyć istniejącego w hello tego samego *lokalizacji* wybrano na powitania **podstawy** kroku kreatora hello.
      3. **Inne parametry**: zwykle po prostu użyć wartości domyślnych hello. W przypadku, gdy ma zostać użyta hello tooconsider wartości innych niż domyślne można umieść kursor nad hello informacyjną łącze, aby uzyskać pomoc dotyczącą hello określonych pól.
   4. **Podsumowanie**: Sprawdź, czy wszystkie informacje wprowadzone jest poprawna.
   5. **Kup**: kliknij **kupić** toostart hello inicjowania obsługi administracyjnej. Łącze jest dostępne toohello warunki hello transakcji. Hello maszyny Wirtualnej nie ma żadnych dodatkowych kosztów poza hello obliczeniowe dla rozmiaru serwera hello w hello **rozmiar** kroku. 

> [!NOTE]
> Inicjowanie obsługi administracyjnej Hello powinny zająć około 10-20 minut. Stan Hello hello inicjowania obsługi administracyjnej jest wyświetlany na powitania portalu Azure.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Jak tooaccess hello maszyny wirtualnej nauki danych firmy Microsoft
Raz hello zostanie utworzona maszyna wirtualna, możesz pulpitu zdalnego do niego przy użyciu poświadczeń konta administratora hello skonfigurowanych w poprzednim hello **podstawy** sekcji. 

Gdy maszyna wirtualna jest utworzone i udostępnione, jest gotowy toostart przy użyciu narzędzia hello, które są zainstalowane i skonfigurowane na nim. Brak Kafelki menu start i ikony pulpitu dla wielu narzędzi hello. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Jak toocreate silne hasło do Jupyter i rozpocząć hello notesu serwera
Domyślnie serwer notesu Jupyter hello jest wstępnie skonfigurowane, ale wyłączone na powitania maszyny Wirtualnej, dopiero po ustawieniu hasła Jupyter. wywołuje hello uruchom następujące polecenie w wierszu polecenia na powitania danych nauki maszyny wirtualnej lub kliknij dwukrotnie skrót hello firma Microsoft umieściła toocreate silne hasło do serwera notesu Jupyter hello zainstalowany na komputerze hello  **Ustaw hasło Jupyter & Start** z konta lokalnego administratora maszyny Wirtualnej.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Wykonaj wiadomości powitania, a następnie wybierz silne hasło po wyświetleniu monitu.

Witaj powyższy skrypt tworzy skrót hasła i znajduje się on w pliku konfiguracyjnym aplikacji Jupyter hello w magazynie: **C:\ProgramData\jupyter\jupyter_notebook_config.py** pod nazwą parametru hello ***c. NotebookApp.password***.

skrypt Hello również umożliwia i uruchamiania serwera Jupyter hello w tle hello. Serwer Jupyter jest tworzony jako zadania systemu windows w hello harmonogramu zadań systemu WIndows o nazwie **Start_IPython_Notebook**.  Toowait może mieć kilka sekund po ustawieniu hasła hello przed otwarciem notesu hello w przeglądarce. Zobacz hello sekcji poniżej **notesu Jupyter** w sposób tooaccess hello serwera notesu Jupyter. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Narzędzi zainstalowanych na powitania maszyny wirtualnej nauki danych firmy Microsoft

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Jeśli chcesz toouse R z analizy hello maszyna wirtualna ma zainstalowanej wersji programu Microsoft R Server Developer. Microsoft R Server to platforma analytics przedsiębiorstw szeroko do wdrożenia oparte na R, która jest obsługiwana, skalowalną oraz bezpieczną. Obsługa różnych statystyk danych big data, modelowania predykcyjnego i możliwości uczenia maszynowego, R Server obsługuje hello pełnego zakresu analytics — eksploracji, analizy wizualizacji i modelowania. Dzięki użyciu i rozszerzanie typu open source R, Microsoft R Server jest całkowicie zgodnej z skrypty języka R, funkcji i pakietów sieci CRAN, tooanalyze danych w skali przedsiębiorstwa. Dotyczy również ograniczeń w pamięci hello Otwórz r źródło przez dodanie równoległe i podzielony przetwarzania danych. Dzięki temu toorun analizy danych niż co mieści się w pamięci głównej.  Visual Studio Community Edition na powitania maszyny Wirtualnej zawiera narzędzia R hello rozszerzenia programu Visual Studio, które zapewnia pełne IDE do pracy z R. Można również pobrać i użyć innych IDEs również takiego jak [programu RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Do tworzenia aplikacji przy użyciu języka Python dystrybucja Anaconda Python 2.7 i 3.5 została zainstalowana. Rozkład ten zawiera hello podstawowa Python wraz z około 300 hello najpopularniejszych matematyczne, inżynieria i danych analizy pakietów. Można użyć narzędzia Python Tools dla programu Visual Studio (PTVS) zainstalowanej w wersji Visual Studio 2015 Community hello lub jednego z powitalne IDEs dołączany Anaconda bezczynności lub Spyder. Można uruchomić te według wyszukiwania na pasku wyszukiwania hello (**Win** + **S** klucza).

> [!NOTE]
> Witaj toopoint narzędzi Python Tools for Visual Studio w Anaconda Python 2.7 i 3.5 należy toocreate niestandardowego środowiska dla każdej wersji. tooset tych ścieżek środowiska w Visual Studio 2015 Community Edition, hello Przejdź zbyt**narzędzia** -> **narzędzi Python Tools** -> **środowiska Python** , a następnie kliknij przycisk **+ niestandardowe**. 
> 
> 

Anaconda Python 2.7 jest zainstalowana w C:\Anaconda i Anaconda Python 3.5 jest zainstalowana w c:\Anaconda\envs\py35. Zobacz [dokumentacji PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) szczegółowy opis kroków. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Dystrybucji anaconda również jest dostarczany z notesu Jupyter, kod tooshare środowiska i analizy. Wstępnie skonfigurowano serwer notesu Jupyter z Python 2.7, języka Python 3.4, Python 3.5 i jądra R. Brak ikony pulpitu o nazwie "notesu Jupyter toolaunch hello przeglądarki tooaccess hello serwera notesu. Jeśli na powitania maszyny Wirtualnej za pośrednictwem pulpitu zdalnego, możesz również odwiedzić [https://localhost:9999 /](https://localhost:9999/) tooaccess hello serwera notesu Jupyter po zalogowaniu toohello maszyny Wirtualnej.

> [!NOTE]
> Kontynuuj, jeśli możesz uzyskać wyświetlania ostrzeżeń dotyczących certyfikatów. 
> 
> 

Firma Microsoft ma umieszczone kilka przykładowych notesów w języku Python i w języku R. hello Pokaż notesów Jupyter jak toowork z Microsoft R Server, SQL Server 2016 R Services (analityka w bazie danych), Python, Microsoft kognitywnych ToolKit (CNTK) głębokie szkoleniowe i innych Azure technologie po zalogowaniu tooJupyter. Na stronie głównej notesu hello można zobaczyć hello łącze toohello próbek, po uwierzytelniania notesu Jupyter toohello przy użyciu hasła hello, utworzony w poprzednim kroku. 

### <a name="visual-studio-2015-community-edition"></a>Program Visual Studio 2015 Community edition
Program Visual Studio Community edition zainstalowany na powitania maszyny Wirtualnej. Jest to bezpłatna wersja hello popularnych IDE firmy Microsoft, który służy do celów ewaluacyjnych i dla małych zespołów. Można wyewidencjonować hello umowy licencyjnej [tutaj](https://www.visualstudio.com/support/legal/mt171547).  Otwórz program Visual Studio przez dwukrotne kliknięcie ikony pulpitu hello lub hello **Start** menu. Możesz również wyszukać programy z **Win** + **S** i wprowadzając "Visual Studio". Gdy można tworzyć projektów w językach C#, Python, R, transport, node.js. Wtyczki instalowane są również ułatwiające wygodne toowork z usługami Azure, takich jak Azure Data Catalog, Azure HDInsight (Hadoop, Spark) i usługi Azure Data Lake. 

> [!NOTE]
> Może wystąpić komunikat informujący, że okres próbny minął. Wprowadź poświadczenia konta Microsoft lub Utwórz nowe bezpłatne konto tooget dostępu toohello programu Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer edition
Deweloperskiej wersji SQL Server 2016 z usługami R toorun w bazie danych analytics znajduje się na powitania maszyny Wirtualnej. Usługi R udostępniają platformę do opracowywania i wdrażania aplikacji inteligentnego. Można użyć języka R hello bogaty i wydajne i hello wiele pakietów hello społeczności toocreate modeli i generowanie prognoz dla danych programu SQL Server. Można zachować dane analityczne Zamknij toohello R usług (w database) zintegrowane języka hello R z programem SQL Server. Eliminuje koszty hello i zagrożenia bezpieczeństwa związane z przepływu danych.

> [!NOTE]
> Hello SQL Server 2016 developer edition można używać tylko do tworzenia i testowania celów. Należy toorun licencji go w środowisku produkcyjnym. 
> 
> 

Dostęp do programu SQL server hello uruchamiając **programu SQL Server Management Studio**. Nazwa maszyny Wirtualnej jest wprowadzana jako hello nazwy serwera. Użyj uwierzytelniania systemu Windows, gdy zalogowany jako administrator w systemie Windows hello. Po przejściu do programu SQL Server Management Studio można utworzyć innych użytkowników, tworzenie baz danych, importowanie danych i uruchamiać zapytania SQL. 

analytics tooenable w bazie danych przy użyciu Microsoft R, uruchom hello następujące polecenia jeden czasu działania w programie SQL Server management studio po zalogowaniu się jako administrator serwera hello. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Kilku narzędzi platformy Azure są zainstalowane na powitania maszyny Wirtualnej:

* Brak tooaccess skrót na pulpicie hello dokumentacji zestawu SDK platformy Azure. 
* **Narzędzie AzCopy**: używane toomove danych do i z konta magazynu Microsoft Azure. Użycie toosee, typ **Azcopy** na użycie hello toosee wiersza polecenia. 
* **Eksplorator magazynu Microsoft Azure**: używane toobrowse za pośrednictwem hello obiektów, które są przechowywane w ramach Twojej tooand konto magazynu Azure i transfer danych z usługi Azure storage. Możesz wpisać **Eksploratora usługi Storage** wyszukiwania lub znajdź go na hello tooaccess menu Start systemu Windows to narzędzie. 
* **Adlcopy**: używane toomove danych tooAzure Data Lake. Użycie toosee, typ **adlcopy** w wierszu polecenia. 
* **dtui**: używane toomove tooand danych z bazy danych NoSQL w chmurze hello Azure rozwiązania Cosmos DB. Typ **dtui** w wierszu polecenia. 
* **Brama zarządzania danymi firmy Microsoft**: umożliwia przenoszenie danych między źródłami danych lokalnych i w chmurze. Jest on używany w ramach narzędzi, takich jak fabryki danych Azure. 
* **Microsoft Azure Powershell**: narzędzie służące tooadminister zasobów platformy Azure w hello Powershell język skryptowy również jest zainstalowany na maszynie Wirtualnej. 

### <a name="power-bi"></a>Power BI
toohelp tworzenia pulpitów nawigacyjnych i wspaniałych wizualizacji hello **Power BI Desktop** został zainstalowany. Użyj tego narzędzia toopull danych z różnych źródeł, tooauthor z pulpitami nawigacyjnymi i raportami i toopublish ich toohello chmury. Aby uzyskać informacje, zobacz hello [usługi Power BI](http://powerbi.microsoft.com) lokacji. W hello Start menu można znaleźć usługi Power BI desktop. 

> [!NOTE]
> Należy tooaccess konta usługi Office 365 usługi Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Dodatkowe narzędzi programistycznych firmy Microsoft
Witaj [ **Instalatora platformy sieci Web firmy Microsoft** ](https://www.microsoft.com/web/downloads/platform.aspx) można toodiscover używane i Pobierz innych narzędzi programistycznych firmy Microsoft. Istnieje również narzędzia toohello skrót na pulpicie maszyny wirtualnej nauki danych Microsoft hello.  

## <a name="important-directories-on-hello-vm"></a>Ważne katalogów na powitania maszyny Wirtualnej
| Element | Katalog |
| --- | --- |
| Konfiguracje serwera notesu Jupyter |C:\ProgramData\jupyter |
| Katalog macierzysty przykłady notesu Jupyter |c:\dsvm\notebooks |
| Inne przykłady |c:\dsvm\samples |
| Anaconda (domyślne: Python 2.7) |c:\Anaconda |
| Środowisko Python 3.5 anaconda |c:\Anaconda\envs\py35 |
| Katalog wystąpienia autonomicznego serwera R (oparte na R3.2.2 wystąpienie domyślne R) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| Serwer R w bazie danych wystąpienia katalogu (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES |
| Katalog wystąpienia Microsoft Open R (R3.3.1) |C:\Program Files\Microsoft\MRO-3.3.1 |
| Różne narzędzia |c:\dsvm\tools |

> [!NOTE]
> Wystąpienia hello utworzone przez maszynę wirtualną systemu Microsoft danych nauki przed 1.5.0 (przed 3 września 2016) używane struktury katalogów nieco inne niż określone w powyższej tabeli hello. 
> 
> 

## <a name="next-steps"></a>Następne kroki
Poniżej przedstawiono niektóre dalej toocontinue czynności użytkownika uczenie i eksploracja. 

* Poznaj hello różnych narzędzi analizy danych na powitania nauki danych maszyny Wirtualnej, klikając hello menu start i wyewidencjonowywanie narzędzia hello menu hello na liście.
* Przejdź za**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** dla przykładów przy użyciu biblioteki RevoScaleR hello w R obsługującego analizy danych w skali przedsiębiorstwa.  
* Przeczytaj artykuł hello: [10 sposobów na powitania nauki danych maszyny wirtualnej](http://aka.ms/dsvmtenthings)
* Dowiedz się, jak hello toobuild tooend analitycznych rozwiązania systematycznie przy użyciu [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Odwiedź hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com) dla analizy danych i uczenie maszyny przykłady tego hello Użyj pakietu Cortana Intelligence Suite. Ikona zostały również zamieszczone na powitania **Start** menu i na pulpicie hello hello maszyny wirtualnej toothis galerii.

