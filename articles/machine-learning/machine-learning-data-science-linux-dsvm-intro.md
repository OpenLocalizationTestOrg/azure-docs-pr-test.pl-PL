---
title: Witaj aaaProvision maszyny wirtualnej systemu Linux danych nauki | Dokumentacja firmy Microsoft
description: Konfigurowanie i tworzenia maszyny wirtualnej systemu Linux danych nauki na analityka Azure toodo i uczenia maszynowego.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 81dfa90f6cd4b4f33535a20fb97442bf9152d829
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-linux-data-science-virtual-machine"></a>Zainicjuj obsługę hello maszyny wirtualnej systemu Linux danych nauki
Witaj maszyny wirtualnej systemu Linux danych nauki jest oparte na CentOS Azure maszyny wirtualnej, która pochodzi z kolekcją narzędzi wstępnie zainstalowane. Te narzędzia są często używane do wykonywania analizy danych oraz uczenia maszynowego. składniki oprogramowania klucza Hello uwzględnione są:

* System operacyjny: Linux CentOS dystrybucji.
* Microsoft R Server Developer Edition
* Dystrybucję oprogramowania Python anaconda (wersji 2.7 i 3.5), łącznie z biblioteki analiz danych popularnych
* JuliaPro - wyselekcjonowanych dystrybucji języka Julia z popularnych bibliotek analizy danych i naukowe
* Wystąpienia autonomicznego Spark i jednego węzła Hadoop (HDFS, Yarn)
* JupyterHub — Obsługa R, Python, PySpark, Julia jądra wielodostępnym serwera notesu Jupyter
* Eksplorator usługi Azure Storage
* Azure interfejs wiersza polecenia (CLI) do zarządzania zasobami platformy Azure
* PostgresSQL bazy danych
* Machine learning narzędzia
  * [Obliczeniowa sieci Toolkit (CNTK)](https://github.com/Microsoft/CNTK): bezpośrednie uczenia toolkit oprogramowania Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): szybki komputer uczenia systemu obsługującego technik, takich jak online, wyznaczania wartości skrótu, allreduce, redukcji, learning2search, aktywna i uczenie się interakcyjne.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): narzędzie, zapewniając szybkie i dokładne boosted drzewa wykonania.
  * [Rattle](http://rattle.togaware.com/) (łatwo hello tooLearn narzędzie analityczne R): narzędzie, które umożliwia wprowadzenie do analizy danych i machine learning w R, udostępniając Eksploracja danych z Graficznym interfejsem użytkownika i modelowanie z automatycznego generowania kodu języka R.
* Zestaw Azure SDK w języku Java, Python, node.js, Ruby, PHP
* Biblioteki języka R i Python dla programu uczenie maszynowe Azure i innych usług Azure
* Narzędzia deweloperskie i edytory (programu RStudio, PyCharm, IntelliJ, Emacs, gedit, vi)


Podczas analizy danych obejmuje iteracja w sekwencji zadań:

1. Znajdowanie, ładowania i wstępne przetworzenie danych
2. Tworzenie i testowanie modeli
3. Wdrażanie modeli hello do wykorzystania w aplikacji inteligentnego

Analityków danych używać różnych narzędzi toocomplete tych zadań. Może być bardzo czasochłonne toofind hello odpowiedniej wersji oprogramowania hello, a następnie toodownload, skompilować i zainstalować te wersje.

Hello maszyny wirtualnej systemu Linux danych nauki może znacznie ułatwić to obciążenie. Użyć toojump rozpoczęcia projektu analizy. Umożliwia toowork zadań w różnych językach, łącznie z R, Python, SQL, Java i C++. Eclipse zapewnia toodevelop IDE i przetestować swój kod, który jest łatwo toouse. Hello zestawu Azure SDK objęte hello maszyny Wirtualnej umożliwia toobuild aplikacji przy użyciu różnych usług w systemie Linux dla platformy w chmurze firmy Microsoft hello. Ponadto masz dostęp tooother w językach Ruby, Perl, PHP i node.js również wstępnie zainstalowane.

Nie ma żadnych opłat oprogramowania dla tego obrazu maszyny Wirtualnej do analizy danych. Płaci się tylko hello Azure sprzętu użycia opłat, które są oceniane na podstawie hello rozmiaru hello maszynę wirtualną, którą można udostępnić hello obrazu maszyny Wirtualnej. Więcej informacji na temat hello obliczeniowe opłaty znajduje się na powitania [strony listę maszyn wirtualnych na hello Azure Marketplace ](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Inne wersje hello maszyny wirtualnej nauki danych
[Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) obrazu jest również dostępna, z wieloma hello narzędzi takie same jak hello CentOS obrazu i głębokie uczenia struktury. A [Windows](machine-learning-data-science-provision-vm.md) obraz jest również dostępny.

## <a name="prerequisites"></a>Wymagania wstępne
Przed utworzeniem maszyny wirtualnej systemu Linux danych nauki musi mieć następujące hello:

* **Subskrypcji platformy Azure**: jeden, zobacz tooobtain [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/free/).
* **Konto magazynu platformy Azure**: jeden, zobacz toocreate [utworzyć konto magazynu platformy Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Alternatywnie można utworzyć konta magazynu hello jako część procesu hello tworzenia hello maszyny Wirtualnej, jeśli nie chcesz, aby toouse istniejącego konta.

## <a name="create-your-linux-data-science-virtual-machine"></a>Tworzenie maszyny wirtualnej systemu Linux danych nauki
Oto toocreate kroki hello wystąpienie maszyny wirtualnej systemu Linux danych nauki hello:

1. Przejdź do wyświetlania na powitania maszyny wirtualnej toohello [portalu Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vmlinuxdsvm).
2. Kliknij przycisk **Utwórz** (u dołu hello) toobring kreatora hello.![ Konfigurowanie danych nauki vm](./media/machine-learning-data-science-linux-dsvm-intro/configure-linux-data-science-virtual-machine.png)
3. następujące sekcje Hello zapewniają hello wejścia dla poszczególnych kroków powitania w Kreatorze hello (wyliczyć na powitania rogu hello powyższej ilustracji) używane hello toocreate maszyny wirtualnej nauki danych firmy Microsoft. Poniżej przedstawiono hello potrzebne dane wejściowe tooconfigure każdego z następujących czynności:
   
   a. **Podstawy**:
   
   * **Nazwa**: Nazwa serwera nauki danych tworzona.
   * **Nazwa użytkownika**: pierwsze konto logowania identyfikatora.
   * **Hasło**: pierwszy hasło do konta (zamiast hasła można użyć klucza publicznego SSH).
   * **Subskrypcja**: Jeśli masz więcej niż jedną subskrypcję, wybierz jedną na które hello maszyna jest toobe utworzone i rozliczane hello. Musi mieć uprawnienia do tworzenia zasobów dla tej subskrypcji.
   * **Grupy zasobów**: można utworzyć nowej lub istniejącej grupy.
   * **Lokalizacja**: hello wybierz centrum danych, która jest najbardziej odpowiednia. Zazwyczaj jest hello centrum danych, która zawiera większość danych, lub najbliższej lokalizacji fizycznej tooyour najszybszy dostęp do sieci.
   
   b. **Rozmiar**:
   
   * Wybierz jeden z typów serwerów hello, które spełnia Twoje wymagania funkcjonalne i ograniczenia kosztów. Wybierz **Wyświetl wszystko** toosee więcej opcji dotyczących rozmiarów maszyn wirtualnych.
   
   c. **Ustawienia**:
   
   * **Typ dysku**: Wybierz **Premium** również dysków półprzewodnikowych (SSD). W przeciwnym razie wybierz **standardowe**.
   * **Konto magazynu**: Utwórz nowe konto magazynu Azure w ramach subskrypcji lub użyć istniejącego w hello tej samej lokalizacji, która została wybrana na powitania **podstawy** kroku kreatora hello.
   * **Inne parametry**: W większości przypadków użycia hello wartości domyślne. tooconsider wartości innych niż domyślne, przesuń kursor myszy łącze informacyjną hello pomoc na temat hello określonych pól.
   
   d. **Podsumowanie**:
   
   * Sprawdź, czy wszystkie wprowadzone informacje jest poprawna.
   
   e. **Kup**:
   
   * toostart hello inicjowania obsługi, kliknij przycisk **kupić**. Łącze jest dostępne toohello warunki hello transakcji. Hello maszyny Wirtualnej nie ma żadnych dodatkowych kosztów poza hello obliczeniowe dla rozmiaru serwera hello w hello **rozmiar** kroku.

Inicjowanie obsługi administracyjnej Hello powinny zająć około 10-20 minut. Stan Hello hello inicjowania obsługi administracyjnej jest wyświetlany na powitania portalu Azure.

## <a name="how-tooaccess-hello-linux-data-science-virtual-machine"></a>Jak tooaccess hello maszyny wirtualnej systemu Linux danych nauki
Po hello utworzenia maszyny Wirtualnej Aby móc zalogować w tooit przy użyciu protokołu SSH. Użyj hello poświadczenia konta, które zostały utworzone w hello **podstawy** sekcji Krok 3 hello tekst powłoki interfejsu. W systemie Windows, możesz pobrać narzędzie klienta SSH, takie jak [Putty](http://www.putty.org). Jeśli wolisz pulpitu graficznego (X Windows System), można użyć X11 przekazywania na Putty lub zainstalować hello X2Go klienta.

> [!NOTE]
> X2Go powitania klienta jest wykonywane znacznie lepszą niż X11 przekazywania podczas testowania. Zalecamy używanie powitania klienta X2Go dla graficzny interfejs użytkownika.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Instalowanie i konfigurowanie klienta X2Go
Witaj maszyny Wirtualnej systemu Linux jest już udostępniony z połączeń klienta gotowa tooaccept X2Go serwera i. toohello tooconnect pulpitu graficznego maszyny Wirtualnej systemu Linux, hello po na komputerze klienckim:

1. Pobierz i zainstaluj klienta hello X2Go dla danej platformy klienta z [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Uruchom klienta hello X2Go i wybierz **nowej sesji**. Otwiera okno konfiguracji z wieloma kartami. Wprowadź następujące parametry konfiguracji hello:
   * **Karta sesji**:
     * **Host**: hello nazwę hosta lub adres IP maszyny Wirtualnej systemu Linux danych nauki.
     * **Logowania**: nazwa użytkownika na powitania maszyny Wirtualnej systemu Linux.
     * **SSH Port**: pozostaw wartość domyślną hello 22,.
     * **Typ sesji**: tooXFCE wartość hello zmiany. Obecnie hello maszyny Wirtualnej systemu Linux obsługuje tylko XFCE pulpitu.
   * **Karta nośnika**: Obsługa dźwięku i drukowanie, jeśli nie ma potrzeby toouse klienta można wyłączyć je.
   * **Foldery udostępnione**: katalogi z komputerów klienckich, z zainstalowanym na powitania maszyny Wirtualnej systemu Linux, należy dodać katalogów na komputerze klienckim hello, które mają tooshare z hello maszyny Wirtualnej na tej karcie.

Po zalogowaniu toohello maszyny Wirtualnej przy użyciu klienta SSH hello lub XFCE graficznego pulpitu za pośrednictwem powitania klienta X2Go jesteś gotowy toostart przy użyciu narzędzia hello, które są zainstalowane i skonfigurowane na powitania maszyny Wirtualnej. Na XFCE Zobacz aplikacje menu skrótów i ikony pulpitu dla wielu narzędzi hello.

## <a name="tools-installed-on-hello-linux-data-science-virtual-machine"></a>Narzędzi zainstalowanych na powitania maszyny wirtualnej systemu Linux danych nauki
### <a name="microsoft-r-server"></a>Serwer R firmy Microsoft
R jest jednym z najbardziej popularnych języków hello do analizowania danych i uczenia maszynowego. Jeśli chcesz toouse R z analizy hello maszyna wirtualna ma Microsoft R Server (PANI) z hello Microsoft Open R (MRO) i biblioteki jądra matematyczne (MKL). Witaj MKL optymalizuje operacji matematycznych typowe w przypadku algorytmów analitycznych. MRO wynosi 100% zgodny z sieci CRAN-R, a wszelkie bibliotek hello R opublikowane w sieci CRAN można zainstalować na powitania MRO. PANI umożliwia skalowanie i operationalization R modeli do usług sieci web. Można edytować w jednym z hello domyślne edytory, takich jak programu RStudio vi, Emacs albo gedit programy R. Korzystając z edytora emacs: hello, należy zwrócić uwagę tego pakietu emacs: hello dostępu (mówi Statystyka Emacs), który upraszcza Praca z plikami R edytora emacs: hello został wstępnie zainstalowany.

Konsola toolaunch R, możesz po prostu wpisz **R** w powłoce hello. Trwa tooan interaktywnego środowiska. toodevelop R program, zwykle za pomocą edytora Emacs lub vi lub gedit, a następnie uruchom skrypty hello w R. W przypadku programu RStudio mają pełni graficznego toodevelop środowiska IDE programu R.

Jest także skrypt R tooinstall hello [pakietów języka R z góry 20](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) Jeśli chcesz. Ten skrypt może działać po hello R interaktywnego interfejsu, który można wprowadzić (jak wspomniano), wpisując **R** w powłoce hello.  

### <a name="python"></a>Python
Do tworzenia aplikacji przy użyciu języka Python dystrybucja Anaconda Python 2.7 i 3.5 została zainstalowana. Rozkład ten zawiera hello podstawowa Python wraz z około 300 hello najpopularniejszych matematyczne, inżynieria i danych analizy pakietów. Możesz użyć edytory tekstów hello domyślne. Ponadto można użyć Spyder, IDE języka Python, który jest powiązany z dystrybucji Anaconda Python. Spyder wymaga graficznego pulpitu lub X11 przekazywania. TooSpyder skrótów znajduje się w hello graficznego pulpitu.

Ponieważ mamy zarówno Python 2.7 i 3.5 należy toospecifically aktywować hello potrzeby wersji języka Python (środowisko conda) ma toowork na w hello bieżącej sesji. proces aktywacji Hello ustawia hello ścieżki zmiennej toohello żądanej wersji języka Python.

tooactivate hello Python 2.7 conda środowiska, uruchom następujące hello z powłoki hello:

    source /anaconda/bin/activate root

Python 2.7 jest zainstalowany na */anaconda/bin*.

tooactivate hello Python 3.5 conda środowiska, uruchom następujące hello z powłoki hello:

    source /anaconda/bin/activate py35


Python 3.5 jest zainstalowana w */anaconda/envs/py35/bin*.

tooinvoke sesję interakcyjne Python, wystarczy wpisać **python** w powłoce hello. Jeśli w graficznym interfejsie lub mieć X11 przekazywania zestawu w górę, można wpisać **pycharm** toolaunch hello PyCharm środowiska IDE języka Python.

tooinstall dodatkowych bibliotek języka Python, należy toorun ```conda``` lub ````pip```` polecenia w obszarze sudo i podaj pełną ścieżkę Menedżera pakietów języka Python hello (conda lub pip) tooinstall toohello poprawne Python środowisko. Na przykład:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Notesu Jupyter
Witaj dystrybucji Anaconda również jest dostarczany z notesu Jupyter, kod tooshare środowiska i analizy. notesu Jupyter Hello jest dostępny za pośrednictwem JupyterHub. Zaloguj się przy użyciu lokalnego nazwę użytkownika systemu Linux i hasło.

wstępnie skonfigurowano serwer notesu Jupyter Hello Python 2, Python 3 i jądra R. Brak ikony pulpitu o nazwie "Notesu Jupyter" toolaunch hello przeglądarki tooaccess hello notesu serwera. Jeśli na powitania maszyny Wirtualnej przy użyciu klienta SSH lub X2Go, możesz również odwiedzić [https://localhost:8000 /](https://localhost:8000/) tooaccess hello serwera notesu Jupyter.

> [!NOTE]
> Kontynuuj, jeśli możesz uzyskać wyświetlania ostrzeżeń dotyczących certyfikatów.
> 
> 

Można uzyskać dostępu do serwera notesu Jupyter hello od dowolnego hosta. Po prostu wpisz *https://\<nazwę DNS maszyny Wirtualnej lub adres IP\>: 8000 /*

> [!NOTE]
> Port 8000 jest otwarty w zaporze hello domyślnie po udostępnieniu hello maszyny Wirtualnej.
> 
> 

Firma Microsoft ma spakowane próbki notesów — jeden w języku Python i jeden w języku R. Na stronie głównej notesu hello można zobaczyć hello łącze toohello próbek, po uwierzytelniania notesu Jupyter toohello przy użyciu lokalnego nazwę użytkownika systemu Linux i hasło. Można utworzyć nowy notes, wybierając **nowy**, a następnie hello odpowiedni język jądra. Jeśli nie widzisz hello **nowy** , kliknij hello **Jupyter** ikony na stronie głównej toohello górnego lewego toogo hello hello notesu serwera.

### <a name="apache-spark-standalone"></a>Apache Spark autonomiczny 
Autonomicznego wystąpienia programu Apache Spark jest preinstalowany na powitania toohelp Linux DSVM najpierw opracowywania aplikacji Spark lokalnie przed testowanie i wdrażanie w dużych klastrach. Za pośrednictwem jądra Jupyter hello można uruchamiać programy PySpark. Po otwarciu Jupyter i kliknij przycisk "Nowy" hello powinno wyświetlić listę dostępnych jądra. Witaj "Python — Spark" jest hello jądra PySpark, która umożliwia tworzenie aplikacji przy użyciu języka Python Spark. Można również użyć IDE języka Python, takie jak PyCharm lub Spyder toobuild możesz Spark program. Począwszy od to wystąpienia autonomicznego, stos Spark hello jest uruchamiany w ramach hello wywoływania programu klienckiego. Dzięki temu szybsze i łatwiejsze problemów tootroubleshoot porównaniu toodeveloping w klastrze Spark. 

Przykładowy notes PySpark znajduje się na Jupyter, który znajduje się w katalogu "SparkML" hello w katalogu macierzystego hello Jupyter ($ głównej/notesów/SparkML/pySpark). 

Jeśli w R są programowania dla platformy Spark, można użyć Microsoft R Server SparkR lub sparklyr. 

Przed uruchomieniem w kontekście Spark Microsoft R Server, należy toodo jeden czas instalacji krok tooenable jednego węzła lokalnego systemu plików HDFS Hadoop i Yarn wystąpienia. Domyślnie usługi Hadoop są zainstalowane, ale na powitania DSVM wyłączony. W kolejności tooenable, potrzebujesz hello toorun następujących poleceń jako główny powitania po raz pierwszy:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Można zatrzymać hello Hadoop powiązane usługi, gdy nie są potrzebne, uruchamiając ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` próbkę prezentacja jak PANI toodevelop i testowania w zdalnym kontekście Spark (czyli wystąpienia Spark autonomicznego hello na powitania DSVM) są dostępne w hello `/dsvm/samples/MRS` katalogu. 

### <a name="ides-and-editors"></a>IDEs i Redaktorzy
Należy wybrać kilka edytory kodu. Dotyczy to również vi/VIM, Emacs, gEdit, PyCharm i programu RStudio, Eclipse IntelliJ. gEdit, Eclipse, IntelliJ i programu RStudio PyCharm są edytory graficzne i konieczne jest toobe podpisaną w graficzny toouse pulpitu tooa je. Edytory te mają pulpitu i aplikacji menu skrótów toolaunch je.

**VIM** i **Emacs** są edytory oparte na tekst. Na Emacs możemy został zainstalowany pakiet dodatku o nazwie Emacs mówi statystyki (dostępu), który ułatwia edytora emacs: hello pracy z R. Więcej informacji można znaleźć w folderze [dostępu](http://ess.r-project.org/).

**Eclipse** jest typu open source, rozszerzalne IDE, która obsługuje wiele języków. Wersja deweloperów języka Java Hello jest wystąpieniem hello zainstalowane na powitania maszyny Wirtualnej. Brak dostępnych wtyczek dla kilku popularnych języków, które mogą być zainstalowane tooextend hello środowiska. Mamy także dodatek zainstalowany w środowisku Eclipse o nazwie **zestawu narzędzi platformy Azure dla programu Eclipse**. Pozwala toocreate, tworzenie, testowanie i wdrażanie aplikacji platformy Azure przy użyciu Środowisko deweloperskie Eclipse hello obsługującą w językach Java. Istnieje również **zestawu Azure SDK dla języka Java** umożliwiająca toodifferent dostępu z usług Azure w środowisku Java. Więcej informacji na temat zestawu narzędzi platformy Azure dla programu Eclipse można znaleźć w folderze [zestawu narzędzi platformy Azure dla programu Eclipse](../azure-toolkit-for-eclipse.md).

**Lateksu** jest instalowane za pomocą pakietu texlive hello wraz z dodatku Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) pakiet, który upraszcza tworzenie dokumentów lateksu w emacs:.  

### <a name="databases"></a>Bazy danych
#### <a name="postgres"></a>Postgres
bazy danych typu open source Hello **Postgres** jest dostępny na powitania maszyny Wirtualnej, z hello usługi są uruchomione i initdb już ukończone. Nadal potrzebujesz toocreate baz danych i użytkowników. Aby uzyskać więcej informacji, zobacz hello [dokumentacji Postgres](https://www.postgresql.org/docs/).  

#### <a name="graphical-sql-client"></a>Graficzny klienta SQL
**SQuirrel SQL**, graficznego klienta SQL, dostarczono tooconnect toodifferent z bazy danych (takich jak Microsoft SQL Server, Postgres i MySQL) i toorun zapytania SQL. Można to wykonać, z sesji pulpitu graficznym (na przykład za pomocą klienta X2Go hello,). tooinvoke SQuirrel SQL, możesz uruchomić go z hello ikony na pulpicie hello lub uruchom następujące polecenie w powłoce hello hello.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Przed hello pierwsze użycie, skonfigurować sterowniki i aliasów bazy danych. Witaj JDBC sterowników znajdują się w folderze:

*/usr/share/Java/jdbcdrivers*

Aby uzyskać więcej informacji, zobacz [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Narzędzia wiersza polecenia do uzyskiwania dostępu do programu Microsoft SQL Server
Witaj pakiet sterownika ODBC dla programu SQL Server zawiera również dwa narzędzia wiersza polecenia:

**Narzędzie BCP**: zbiorczego narzędzie bcp hello kopiuje dane między wystąpienia programu Microsoft SQL Server i plik danych w formacie określone przez użytkownika. Narzędzie bcp Hello mogą być używane tooimport dużą liczbą nowych wierszy do tabel programu SQL Server lub tooexport danych z tabel do plików danych. tooimport dane do tabeli, należy użyć pliku formatu utworzonego dla tej tabeli, lub zrozumieć hello struktura tabeli hello i hello typów danych, które są prawidłowe dla kolumn.

Aby uzyskać więcej informacji, zobacz [połączenie za pomocą narzędzia bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**narzędzia sqlcmd**: Wprowadź instrukcji języka Transact-SQL z narzędzia sqlcmd hello, a także systemowych procedur i pliki w wierszu polecenia hello skryptów. Narzędzie to wykorzystuje partie tooexecute języka Transact-SQL ODBC.

Aby uzyskać więcej informacji, zobacz [połączenie przy użyciu narzędzia sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Istnieją pewne różnice w to narzędzie między platformami systemu Linux i Windows. Zapoznaj się dokumentacją hello, aby uzyskać szczegółowe informacje.
> 
> 

#### <a name="database-access-libraries"></a>Biblioteki dostępu do bazy danych
Brak dostępnych bibliotek w bazach danych tooaccess R i Python.

* W R, hello **RODBC** pakietu lub **dplyr** pakietu pozwala tooquery lub wykonywania instrukcji SQL na powitania serwera bazy danych.
* W języku Python, hello **pyodbc** Biblioteka zapewnia dostęp do bazy danych z ODBC jako hello warstwy podstawowej.  

tooaccess **Postgres**:

* Z R: Użyj hello pakietu **RPostgreSQL**.
* W języku Python: Hello użyj **psycopg2** biblioteki.

### <a name="azure-tools"></a>Narzędzia platformy Azure
Witaj następujące narzędzia Azure są zainstalowane na powitania maszyny Wirtualnej:

* **Interfejs wiersza polecenia platformy Azure**: hello wiersza polecenia platformy Azure pozwala toocreate i zarządzania zasobami Azure za pomocą powłoki poleceń. tooinvoke hello narzędzi platformy Azure, po prostu wpisz **azure pomocy**. Aby uzyskać więcej informacji, zobacz hello [stronę dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Eksplorator magazynu Microsoft Azure**: Eksploratora usługi Microsoft Azure Storage jest graficzne narzędzie, które jest używane toobrowse za pośrednictwem hello obiektów, które są przechowywane w Twoje konto magazynu Azure i tooupload i pobierania tooand danych z obiektów blob Azure. Ikona skrótu na pulpicie hello dostępne Eksploratora usługi Storage. Można wywołać z poziomu wiersza powłoki, wpisując **StorageExplorer**. Konieczne toobe zalogowany na kliencie X2Go lub mieć X11 przekazywania zestawu w górę.
* **Biblioteki Azure**: hello poniżej przedstawiono niektóre hello wstępnie zainstalowane bibliotek.
  
  * **Python**: hello Azure związane z biblioteki w języku Python, które są zainstalowane są **azure**, **uczenie maszynowe Azure**, **pydocumentdb —**, i **pyodbc** . Z hello pierwsze trzy biblioteki, można uzyskać dostępu do usług Azure storage, uczenie maszynowe Azure i bazy danych Azure rozwiązania Cosmos (danych nosql opartej na platformie Azure). Hello czwarty biblioteki pyodbc (wraz z hello sterownika Microsoft ODBC dla programu SQL Server), umożliwia tooSQL dostęp do serwera Azure SQL Database i Azure SQL Data Warehouse w języku Python za pomocą interfejsu ODBC. Wprowadź **listy pip** toosee hello wszystkie wymienione biblioteki. Można toorun się, że to polecenie w obu hello Python 2.7 i środowisk 3.5.
  * **R**: hello Azure związane z biblioteki w R zainstalowanych są **uczenie maszynowe Azure** i **RODBC**.
  * **Java**: hello listy bibliotek Azure Java można znaleźć w katalogu hello **/dsvm/sdk/AzureSDKJava** na powitania maszyny Wirtualnej. biblioteki klucza Hello są Azure sterowniki magazynów i zarządzania interfejsów API, bazy danych Azure rozwiązania Cosmos i JDBC dla programu SQL Server.  

Dostęp można uzyskać hello [portalu Azure](https://portal.azure.com) z hello wstępnie zainstalowane przeglądarki Firefox. Na powitania portalu Azure można utworzyć, zarządzanie i monitorowanie zasobów platformy Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Usługa Azure Machine Learning to usługa w chmurze w pełni zarządzana, umożliwiającą toobuild, wdrażanie i udostępniać rozwiązania analizy predykcyjnej. Możesz utworzyć modele i eksperymenty Azure Machine Learning Studio. Jest dostępny z przeglądarki sieci web na maszynie wirtualnej nauki danych hello odwiedzając [Microsoft Azure Machine Learning](https://studio.azureml.net).

Po zalogowaniu tooAzure Machine Learning Studio masz kanwy, gdzie można utworzyć przepływ logiczny dla algorytmów uczenia maszynowego hello eksperymenty tooan dostępu. Możesz również notesu Jupyter tooa dostępu do hostowanych w usłudze Azure Machine Learning i może bezproblemowo współpracować z hello eksperymentów w usłudze Machine Learning Studio. Operacjonalizuj modeli, utworzonych przez zawijania je w interfejsie usługi sieci web uczenia maszynowego hello. Dzięki temu klienci napisane w dowolnym prognoz tooinvoke języka z modeli uczenia maszynowego hello. Aby uzyskać więcej informacji, zobacz hello [dokumentacji uczenia maszynowego](https://azure.microsoft.com/documentation/services/machine-learning/).

Można również rozbudowywać modeli w języku R lub Python hello maszyny Wirtualnej, a następnie wdrożyć go w środowisku produkcyjnym w usłudze Azure Machine Learning. Firma Microsoft zainstalowano bibliotek w R (**uczenie maszynowe Azure**) i języka Python (**uczenie maszynowe Azure**) tooenable tej funkcji.

Informacje dotyczące sposobu toodeploy modele R i Python w usłudze Azure Machine Learning, sekcji [10 sposobów na powitania nauki danych maszyny wirtualnej](machine-learning-data-science-vm-do-ten-things.md) (w szczególności hello sekcji "tworzenie modeli przy użyciu R lub Python i Operacjonalizacji je przy użyciu usługi Azure Machine Learning").

> [!NOTE]
> Instrukcje te zostały napisane dla wersji systemu Windows hello hello wirtualna analizy danych. Ale informacje hello pod warunkiem że na temat wdrażania tooAzure modeli uczenia maszynowego jest zastosowanie toohello maszyny Wirtualnej systemu Linux.
> 
> 

### <a name="machine-learning-tools"></a>Machine learning narzędzia
Witaj maszyna wirtualna ma kilka machine learning narzędzia i algorytmy, które zostały wstępnie skompilowany i wstępnie zainstalowane lokalnie. Należą do nich:

* **CNTK** (obliczeniową sieci zestawu narzędzi firmy Microsoft Research): bezpośrednich uczenia zestawu narzędzi.
* **Vowpal Wabbit**: Algorytm uczenia fast online.
* **xgboost**: narzędzie, które zapewnia zoptymalizowane, boosted drzewa algorytmów.
* **Python**: Anaconda Python jest powiązane z algorytmów uczenia maszynowego z bibliotekami, takich jak Scikit Dowiedz się więcej. Inne biblioteki można zainstalować za pomocą hello `pip install` polecenia.
* **R**: Biblioteka sformatowanego machine learning funkcji jest dostępna dla R. Niektóre hello bibliotek, które są wstępnie zainstalowane są lm, glm, randomForest, rpart. Inne biblioteki można zainstalować, uruchamiając:
  
        install.packages(<lib name>)

Oto niektóre dodatkowe informacje na temat hello najpierw trzy machine learning narzędzia hello na liście.

#### <a name="cntk"></a>CNTK
Jest to typu open source, głębokie uczenia zestawu narzędzi. To narzędzie wiersza polecenia (cntk) i jest już hello ścieżki.

toorun podstawowy przykład, wykonaj następujące polecenia w powłoce hello hello:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Aby uzyskać więcej informacji, zobacz hello sekcji CNTK [GitHub](https://github.com/Microsoft/CNTK)i hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit jest system, który używa technik, takich jak online, wyznaczania wartości skrótu, allreduce, redukcji, learning2search, aktywne, uczenia maszynowego i uczenie się interakcyjne.

Narzędzie hello toorun na bardzo prosty przykład Witaj następujące:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Istnieją inne, większy pokazy w tym katalogu. Aby uzyskać więcej informacji dotyczących VW, zobacz [tej sekcji GitHub](https://github.com/JohnLangford/vowpal_wabbit)i hello [wiki Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>xgboost
Jest to biblioteka, który został zaprojektowany i zoptymalizowany pod kątem algorytmów boosted (drzewo). cel Hello tej biblioteki jest potrzebne toopush hello obliczeń limitów ekstremalnymi toohello maszyny tooprovide na dużą skalę drzewa zwiększania skalowalności, przenośne i dokładne.

Jest podana jako wiersz polecenia, a także biblioteki R.

toouse tej biblioteki w R, można uruchomić sesji interaktywnej R (przez wpisanie po prostu **R** w powłoce hello) i biblioteki hello obciążenia.

Poniżej przedstawiono prosty przykład, który można uruchomić w wierszu R:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

toorun hello xgboost wiersza polecenia, w tym miejscu są tooexecute polecenia hello w powłoce hello:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


.Model — plik jest zapisywany określony katalog toohello. Można znaleźć informacje o tym przykładzie pokaz [w serwisie GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Aby uzyskać więcej informacji na temat xgboost Zobacz hello [stronę dokumentacji xgboost](https://xgboost.readthedocs.org/en/latest/), a jego [repozytorium GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Rattle (hello **R** **A**nalytical **T**pismo odręczne — narzędzie **T**o **L**zdobyć **E** asily) korzysta z Graficznym interfejsem użytkownika Eksplorowanie danych oraz modelowania. Przedstawia informacje statystyczne visual podsumowania danych, transformacji danych, które mogą być łatwo modelowane, tworzy zarówno nienadzorowanych i nadzorowanym modeli z danych hello, przedstawia graficznie hello wydajności modeli i ustawia wyniki nowych danych. Generuje kod języka R, replikowanie operacje hello w hello interfejsu użytkownika, które można uruchomić bezpośrednio w R lub używany jako punkt początkowy do dalszej analizy.

toorun Rattle należy toobe w graficznym logowania w sesji pulpitu. Na terminalu hello wpisz ```R``` tooenter hello R środowiska. W wierszu hello R wprowadź hello następującego polecenia:

    library(rattle)
    rattle()

Teraz interfejsu graficznego otwartej z zestawu kart. Poniżej przedstawiono hello szybki start czynnościach w ramach toouse Rattle potrzebne zestawu danych przykładowych pogody i utworzyć model. W niektórych hello poniższe kroki są instalacji zostanie wyświetlony monit o tooautomatically i załadować niektórych wymaganych pakietów języka R, które nie są już w systemie hello.

> [!NOTE]
> Jeśli nie masz dostępu tooinstall hello pakietu w katalogu systemu hello (domyślnie: hello) może zostanie wyświetlony monit na R konsoli okna tooinstall pakiety tooyour bibliotece osobistych. Odpowiedzi *y* Jeśli wyświetlane monity.
> 
> 

1. Kliknij przycisk **Execute** (Wykonaj).
2. Okno dialogowe wyskakującej, prosząc, jeśli chcesz hello toouse pogody Przykładowy zestaw danych. Kliknij przycisk **tak** przykład Witaj tooload.
3. Kliknij przycisk hello **modelu** kartę.
4. Kliknij przycisk **Execute** toobuild drzewa decyzyjnego.
5. Kliknij przycisk **rysowania** drzewa decyzyjnego hello toodisplay.
6. Kliknij przycisk hello **lasu** przycisk radiowy, a następnie kliknij przycisk **Execute** toobuild losowe lasu.
7. Kliknij przycisk hello **Evaluate** kartę.
8. Kliknij przycisk hello **ryzyka** przycisk radiowy, a następnie kliknij przycisk **Execute** toodisplay dwa ryzyka (skumulowany) wydajności powierzchni.
9. Kliknij przycisk hello **dziennika** hello tooshow kartę generowania kodu języka R dla hello powyższej operacji.
   (Ze względu na błąd tooa w bieżącej wersji Rattle hello, należy tooinsert  *#*  znak przed *wyeksportować ten dziennik...*  w tekście hello dziennika hello.)
10. Kliknij przycisk hello **wyeksportować** przycisk toosave hello R pliku skryptu o nazwie *weather_script. R* toohello folder macierzysty.

Można zamknąć Rattle i R. Teraz można zmodyfikować skrypt języka R hello wygenerowany lub go użyć, ponieważ jest on toorun go w każdej chwili toorepeat wszystkie elementy, które zostało wykonane w ramach hello Rattle interfejsu użytkownika. Szczególnie dla początkujących użytkowników w R jest prosty sposób tooquickly do analizy i komputera learning prostego interfejsu graficznego, podczas automatycznego generowania kodu w R toomodify i/lub Dowiedz się więcej.

## <a name="next-steps"></a>Następne kroki
Oto, jak można kontynuować swoją uczenie i eksploracja:

* Witaj [nauki danych na powitania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-walkthrough.md) przewodniku zademonstrowano, jak tooperform kilka typowych nauki danych zadania o hello danych nauki maszyny Wirtualnej systemu Linux udostępnione w tym miejscu. 
* Poznaj hello różnych narzędzi analizy danych na hello nauki danych maszyny Wirtualnej przez wypróbować narzędzia hello opisane w tym artykule. Można również uruchomić *dsvm więcej info* na powitania powłoki maszynie wirtualnej hello podstawowe informacje toomore wprowadzenie oraz wskaźniki o hello narzędzia są zainstalowane na powitania maszyny Wirtualnej.  
* Dowiedz się, jak hello rozwiązań analitycznych end-to-end toobuild systematycznie przy użyciu [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Odwiedź hello [Cortana Analytics Gallery](http://gallery.cortanaanalytics.com) dla analizy danych i uczenie maszyny przykłady tego hello Użyj Cortana Analytics Suite.

