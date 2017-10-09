---
title: "aaaWhat jest maszyną wirtualną nauki danych? | Microsoft Docs"
description: "Sposób tooget uruchamiania wykonywania scenariuszy analizy klucza z maszyn wirtualnych analizy danych."
keywords: "narzędzia do analizy danych, maszyny wirtualnej analizy danych, narzędzia do analizy danych, nauki danych systemu linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Wprowadzenie toohello oparte na chmurze danych nauki maszyny wirtualnej systemu Linux i Windows
Witaj danych nauki maszyny wirtualnej (DSVM) jest dostosowany obraz maszyny Wirtualnej w chmurze Azure firmy Microsoft, opracowane pod kątem wykonywania analizy danych. Składa się z wielu popularnych danych nauki i inne narzędzia preinstalowanym i wstępnie skonfigurowane toojump-start tworzenia aplikacji inteligentnego zaawansowana analityka. Jest dostępna w systemach Windows Server i Linux. Oferujemy wersje maszyny wirtualnej dla systemów Windows Server 2016 i Windows Server 2012. Firma Microsoft oferuje wersji hello DSVM na Ubuntu 16.04 LTS i na podstawie OpenLogic 7.2 CentOS Linux dystrybucje systemu Linux. 

W tym temacie opisano, co można zrobić hello wirtualna analizy danych, opisano niektóre najważniejsze scenariusze hello przy użyciu hello wirtualna itemizes hello najważniejsze funkcje dostępne w hello systemu Windows i Linux wersjach i zawiera instrukcje dotyczące sposobu uruchamiania tooget za ich pomocą.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>Co można zrobić z hello maszyny wirtualnej nauki danych?
Celem Hello hello maszyny wirtualnej nauki danych jest tooprovide specjalistów danych na wszystkich poziomach umiejętności oraz role ze środowiskiem nauki tarcia dane. Ta maszyna wirtualna jest zapisywany wiele czasu, który poświęcić Jeśli samodzielnie miał wdrażana środowisku można porównywać pod względem. Zamiast tego uruchomić projektu nauki danych bezpośrednio w nowo utworzone wystąpienie maszyny Wirtualnej. 

Witaj wirtualna nauki danych został zaprojektowany i skonfigurowane do pracy ze scenariuszami użycia szeroki. Środowiska można skalować w górę lub w dół zgodnie z projektu zmieniających się potrzeb. Możesz są możliwe toouse zadań nauki preferowany język tooprogram danych. Można zainstalować narzędzi i dostosowywania systemu hello na potrzeby użytkowników.

## <a name="key-scenarios"></a>Najważniejsze scenariusze
W tej części podano niektóre najważniejsze scenariusze, dla których hello można wdrożyć maszyny Wirtualnej analizy danych.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Wstępnie pulpitu analityka w chmurze hello
Witaj wirtualna nauki danych udostępnia konfiguracji bazowej dla zespołów nauki danych wyszukiwania tooreplace lokalnych komputerów stacjonarnych z pulpitem zarządzanej chmury. Tej linii bazowej gwarantuje, że wszystkie analityków danych hello w zespole spójne Instalator, z których eksperymenty tooverify i wspierania współpracy. Również obniża koszty dzięki zmniejszeniu obciążenia sysadmin hello i zapisywania na czas hello potrzeby tooevaluate, zainstalować i obsługa hello różnych pakietów oprogramowania wymagane toodo zaawansowane analizy.  

### <a name="data-science-training-and-education"></a>Szkolenia i edukacja w zakresie analizy danych
Instruktorów przedsiębiorstwa i instytucjom pokazujące klasy nauki danych zwykle zapewnia obrazu maszyny wirtualnej w tooensure że ich studentów spójne ustawienia i przewidywalnego pracy hello próbek. Hello wirtualna nauki danych tworzy środowisko na żądanie z Instalatorem spójne, który ułatwia hello wyzwania niezgodności i pomocy technicznej. Przypadkach, gdy tych środowisk muszą toobe wbudowane często, zwłaszcza w przypadku krótszą klasy szkolenia, znacznie korzyści.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Elastyczne pojemności na żądanie dla dużych projektów
Dane nauki hackathons/konkursami lub modelowania danych na dużą skalę i eksploracja wymagają skalowana w poziomie wydajności sprzętu i zwykle przez krótki czas trwania. Hello wirtualna nauki danych może pomóc replikować hello danych nauki środowiska szybko na żądanie, uruchom na skalowanej serwerów, które umożliwia eksperymenty wymagające silnych toobe zasobów obliczeniowych.

### <a name="short-term-experimentation-and-evaluation"></a>Eksperymenty krótkoterminowej i ocena
Hello wirtualna nauki danych mogą być używane tooevaluate lub narzędzia takich jak Microsoft R Server, SQL Server, Visual Studio tools, Jupyter głębokość uczenia / ML zestaw narzędzi i nowe narzędzia popularnych w hello społeczności przy instalacji z minimalnym wysiłku. Ponieważ hello wirtualna nauki danych można szybko skonfigurować, mogą być stosowane w innych krótkoterminowej scenariusze użycia, takie jak replikowanie opublikowanych eksperymentów, pokazy, następujące wskazówki w sesji online lub samouczki konferencji wykonywania.

### <a name="deep-learning"></a>Głębokie learning
Witaj nauki danych maszyny Wirtualnej może służyć do szkolenia modelu przy użyciu algorytmów uczenia głębokie na procesora GPU (jednostki przetwarzania grafiki) oparte na sprzęcie. Przy użyciu maszyn wirtualnych, skalowanie możliwości chmury Azure, DSVM pomaga użycia procesora GPU na podstawie sprzętu w chmurze hello zgodnie z harmonogramem potrzeby. Co można przełączać tooa GPU na podstawie maszyny Wirtualnej podczas dużych modeli uczenia lub wymagają hello obliczenia szybkich przy zachowaniu tego samego dysku systemu operacyjnego.  wersji systemu Windows Server 2016 Hello DSVM jest wstępnie zainstalowane z wersji sterowników procesora GPU, struktur i wersja procesora GPU hello głębokie algorytmów uczenia. Na powitania Linux bezpośrednich learning na procesor GPU jest włączone tylko na powitania [danych maszyny wirtualnej nauki dla wersji systemu Linux (Ubuntu)](http://aka.ms/dsvm/ubuntu). Wersji 2016-Windows-Ubuntu hello wirtualna nauki danych toonon GPU na podstawie maszyny wirtualnej platformy Azure można wdrożyć w takim przypadku wszystkich platform głębokie learning hello będzie tryb rezerwowy toohello procesora CPU. Wcześniej, systemu Windows Server 2012 firma Microsoft opublikowane [głębokie uczenia toolkit](http://aka.ms/dsvm/deeplearning) , ale teraz zaleca się użycie systemu Windows Server 2016 dla obciążeń głębokie uczenia z systemem Windows. Witaj wersji na podstawie CentOS Linux hello DSVM zawiera tylko hello Procesora kompilacje niektórych hello głębokie narzędzie (CNTK, Tensorflow, MXNet), ale nie pochodzi preinstalowanym hello wersji sterowników procesora GPU i platform. 

## <a name="whats-included-in-hello-data-science-vm"></a>Zawartość hello wirtualna nauki danych?
Hello maszyny wirtualnej nauki danych ma wiele popularnych danych nauki i bezpośrednie narzędzie już zainstalowany i skonfigurowany. Zawiera również narzędzia, które umożliwiają łatwe toowork z różnych Azure danych i ich analiza produktów. Można eksplorować i tworzenie modeli predykcyjnych w dużych zestawów danych przy użyciu hello Microsoft R Server lub SQL Server 2016. Host innych narzędzi hello typu open source społeczność i firmy Microsoft są uwzględnione, a także przykładowy kod i notesów. Witaj poniższej tabeli itemizes i porównuje hello główne składniki objęte hello systemu Windows i Linux wersje hello maszyny wirtualnej analizy danych.


| **Narzędzie**                                                           | **Wersja systemu Windows** | **Wersja systemu Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Otwórz R Microsoft](https://mran.microsoft.com/open/) z pakietami popularnych preinstalowanym   |Tak                      | Tak             |
| [Serwer R Microsoft](https://msdn.microsoft.com/microsoft-r/) zawiera Developer Edition, <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) framework równoległych rozproszonej wysokiej wydajności i R<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) -nowych algorytmów uczenia Maszynowego stanu grafiki firmy Microsoft <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [R Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |Tak                      | Tak <br/> (MicrosoftML nie jest jeszcze dostępna)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) wykraczającego Plus z udostępnionego aktywacji - programu Excel, Word i PowerPoint   |Tak                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 z pakietami popularnych preinstalowanym    |Tak                      |Tak              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) z popularnych pakiety języka Julia preinstalowanym                         |Tak                      |Tak              |
| Relacyjne bazy danych                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Narzędzia bazy danych                                                       | * Programu SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [BCP i sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * Sterowniki ODBC/JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (podczas badania narzędzie) <br /> * narzędzia bcp i sqlcmd <br /> * Sterowniki ODBC/JDBC|
| Skalowalna analityka w bazie danych z usługami SQL Server R | Tak     |N              |
| **[Serwer notesu Jupyter](http://jupyter.org/) z następujących jądra**                                  | Tak     | Tak |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | Tak | Tak |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 & 3.5 | Tak | Tak |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | Tak | Tak |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | Tak |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | T (tylko Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | Tak |
| JupyterHub (serwer notesów przez wielu użytkowników)| N | Tak |
| **Narzędzia deweloperskie, edytory IDEs i kod**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) > Wtyczki Git, Azure HDInsight (Hadoop), usługi Data Lake tools danych programu SQL Server [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs), i [R Narzędzia dla programu Visual Studio (RTVS)](http://microsoft.github.io/RTVS-docs/) | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Kod Visual Studio](https://code.visualstudio.com/) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Programu RStudio pulpitu](https://www.rstudio.com/products/rstudio/#Desktop) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Serwer programu RStudio](https://www.rstudio.com/products/rstudio/#Server) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (Julia IDE)](http://junolab.org/)| Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim i emacs: | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git i GitBash | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* .net framework | Tak | N |
| Usługa Power BI Desktop | Tak | N |
| Tooaccess zestawów SDK platformy Azure i pakietu Cortana Intelligence Suite usług | Tak | Tak |
| **Przenoszenie danych i narzędzia do zarządzania** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Eksplorator usługi azure Storage | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/overview) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* Program azure Powershell | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Narzędzie Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy (usługi Azure Data Lake Storage)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Narzędzie migracji danych o nazwie DocDB](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Brama zarządzania danymi firmy Microsoft](https://msdn.microsoft.com/library/dn879362.aspx) : przenoszenie danych między lokalnego programu i w chmurze | Tak | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Narzędzia wiersza polecenia systemu Unix/Linux | Tak | Tak |
| [Przechodzenie do szczegółów Apache](http://drill.apache.org) dla Eksploracja danych | Tak | Tak |
| **Narzędzia uczenia maszynowego** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* Integracji z [uczenie maszynowe Azure](https://azure.microsoft.com/services/machine-learning/) (R, Python) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | T (tylko Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | N | T (tylko Ubuntu) |
| **Głębokie Learning narzędzia oparte na Graficznym** |Wersja systemu Windows Server 2016  |Ubuntu edition |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Kognitywnych zestaw narzędzi firmy Microsoft (CNTK)](http://cntk.ai) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | Tak | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | Tak | Tak|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe & Caffe2](https://github.com/caffe2/caffe2) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Latarka](http://torch.ch/) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia cyfr](https://github.com/NVIDIA/DIGITS) | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Sterownik Nvidia CUDA, CUDNN,](https://developer.nvidia.com/cuda-toolkit) | Tak | Tak |
| **Platformy danych big Data (tylko Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* Lokalnego [Spark](http://spark.apache.org/) autonomiczny | N | Tak |
| &nbsp;&nbsp;&nbsp;&nbsp;* Lokalnego [Hadoop](http://hadoop.apache.org/) (HDFS, YARN) | N | Tak |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Jak tooget pracę z hello maszyny Wirtualnej nauki danych systemu Windows
* Utwórz wystąpienie edition Windows DSVM hello potrzeby przechodząc do
  * [Windows Server 2016 na podstawie DSVM](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  lub 
  * [Windows Server 2012 na podstawie DSVM](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Kliknij przycisk hello **UZYSKAĆ IT** przycisku.
* Zaloguj się toohello maszyny Wirtualnej z pulpitu zdalnego przy użyciu poświadczeń hello określony podczas tworzenia hello maszyny Wirtualnej.
* toodiscover, a następnie uruchom hello dostępnych narzędzi, kliknij przycisk hello **Start** menu.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Rozpoczynanie pracy z hello maszyny Wirtualnej systemu Linux danych nauki
* Utwórz wystąpienie hello potrzeby wersji systemu Linux DSVM przechodząc zbyt
  * [Ubuntu na podstawie DSVM](http://aka.ms/dsvm/ubuntu)

  lub

  * [OpenLogic CentOS na podstawie DSVM](http://aka.ms/dsvm/centos)

  
* Kliknij przycisk hello **Pobierz teraz** przycisku.
* Zaloguj się toohello maszyny Wirtualnej z klienta SSH, takiego jak Putty lub polecenia SSH, przy użyciu poświadczeń hello określony podczas tworzenia hello maszyny Wirtualnej.
* W wierszu polecenia powłoki hello wprowadź informacje o innych dsvm.
* Graficzny komputerów stacjonarnych, Pobierz klienta hello X2Go dla danej platformy klienta [tutaj](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) i postępuj zgodnie z instrukcjami hello w dokumencie maszyny Wirtualnej systemu Linux danych nauki hello [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Następne kroki
### <a name="for-hello-windows-data-science-vm"></a>Dla maszyny Wirtualnej nauki danych systemu Windows hello
* Aby uzyskać więcej informacji o jak toorun określonego narzędzia dostępne w wersji Windows hello, zobacz [hello udostępniania maszyny wirtualnej nauki danych Microsoft](machine-learning-data-science-provision-vm.md) i
* Aby uzyskać więcej informacji na temat tooperform różne zadania wymagane do projektu analizy danych na powitania maszyny Wirtualnej systemu Windows, zobacz temat [10 sposobów na powitania nauki danych maszyny wirtualnej](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Dla maszyny Wirtualnej systemu Linux danych nauki hello
* Aby uzyskać więcej informacji na jak toorun określonego narzędzia dostępne w wersji systemu Linux hello, zobacz [hello udostępniania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-intro.md).
* Aby uzyskać wskazówki, który pokazuje, jak tooperform kilka typowych nauki danych zadania o hello maszyny Wirtualnej systemu Linux, zobacz [nauki danych na powitania maszyny wirtualnej systemu Linux danych nauki](machine-learning-data-science-linux-dsvm-walkthrough.md).

