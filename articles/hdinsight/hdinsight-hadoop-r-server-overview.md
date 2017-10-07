---
title: "tooR aaaIntroduction serwera w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse R Server w przypadku aplikacji toocreate HDInsight do analizy danych big data."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Wprowadzenie tooR serwera i open source możliwości R w usłudze HDInsight

Serwer R firmy Microsoft jest dostępny jako opcję wdrażania, podczas tworzenia klastrów usługi HDInsight w systemie Azure. Ta nowa funkcja zapewnia analityków danych, chi i programistów R z tooscalable na żądanie dostępu rozproszonego metody analizy w usłudze HDInsight.

Klastrów mogą być rozmiary toohello projektów i zadań i następnie działo po nie są już potrzebne. Ponieważ są one częścią usługi Azure HDInsight, te klastry pochodzą z obsługą 24/7 przedsiębiorstw, umową SLA gwarantującą 99,9% czasu i hello możliwości toointegrate z innymi składnikami w hello ekosystemu platformy Azure.

Serwer R w usłudze HDInsight zawiera hello najnowszych funkcji analizy na podstawie R po zestawów danych w praktycznie dowolnej wielkości, załadować tooeither magazynu obiektów Blob platformy Azure lub usługi Data Lake. Ponieważ serwer R jest oparty na typu open source R, hello R aplikacji tworzonych mogą korzystać z dowolnej pakietów hello 8000 + R typu open source. dostępne są także procedury Hello w ScaleR, pakiet analizy danych big data firmy Microsoft dołączony R Server.

Witaj krawędzi węzła klastra zawiera wygodne miejsce tooconnect toohello klastra i toorun skrypty języka R. Z węzłem krawędzi masz hello opcja uruchomionych hello zarządzana z przetwarzaniem rozproszonych funkcji ScaleR na powitania rdzeni hello krawędzi węzeł serwera. Można również uruchomić je w węzłach hello hello klastra przy użyciu Zmniejsz mapy platformy Hadoop w ScaleR lub Spark kontekstów obliczeń.

modele Hello lub prognoz, które mogą być pobierane w wyniku analizy do użyć lokalnego. One może również być operationalized w innym miejscu na platformie Azure, w szczególności za pośrednictwem [Azure Machine Learning Studio](http://studio.azureml.net) [usługi sieci web](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-started-with-r-on-hdinsight"></a>Wprowadzenie do języka R w usłudze HDInsight
tooinclude R Server w klastrze usługi HDInsight, musisz wybrać hello typ klastra R Server podczas tworzenia klastra usługi HDInsight przy użyciu hello portalu Azure. Hello typ klastra R Server zawiera R Server na powitania danych węzłów klastra hello i na węzeł krawędzi, która służy jako strefy docelowej na serwerze R analizy. Zobacz [wprowadzenie R Server w usłudze HDInsight](hdinsight-hadoop-r-server-get-started.md) przewodnik dotyczący sposobu toocreate hello klastra.

## <a name="learn-about-data-storage-options"></a>Więcej informacji na temat opcji magazynu danych
Domyślny magazyn dla systemu plików HDFS hello klastrów usługi HDInsight można skojarzyć z konta magazynu Azure lub usługi Azure Data Lake store. To skojarzenie gwarantuje, że niezależnie od danych została przekazana toohello magazynu klastra podczas analizy staje się trwałych. Istnieją różne narzędzia do obsługi hello danych transfer toohello magazynu opcji wybranych, tym funkcje oparte na portalu przekazywania hello hello konto magazynu i hello [AzCopy](../storage/common/storage-use-azcopy.md) narzędzia.

Dostępna jest opcja hello Dodawanie dostępu tooadditional obiektów Blob i Data lake magazynów w trakcie procesu niezależnie od opcji magazynu podstawowego hello używany udostępniania klastra hello. Zobacz [wprowadzenie R Server w usłudze HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) informacji na temat dodawania konta dostępu do tooadditional. Zobacz dodatkowe hello [opcje usługi Azure Storage platformy R Server w usłudze HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) toolearn artykułu więcej informacji na temat korzystania z wielu kont magazynu.

Można również użyć [plików Azure](../storage/files/storage-how-to-use-files-linux.md) jako opcji magazynu do użycia na powitania węzła krawędzi. Usługa pliki Azure umożliwia toomount udział pliku, który został utworzony w toohello usługi Azure Storage systemu plików w systemie Linux. Aby uzyskać więcej informacji o tych opcjach przechowywania danych platformy R Server w klastrze usługi HDInsight, zobacz [usługi Azure Storage opcje dla klastrów serwerów R w usłudze HDInsight](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Serwer R dostępu w klastrze hello
Możesz połączyć tooR serwera w węźle krawędzi hello za pomocą przeglądarki, możesz podać podczas procesu udostępniania hello wybraną tooinclude serwera programu RStudio. Jeśli nie został on zainstalowany, podczas inicjowania obsługi administracyjnej hello klastra, możesz dodać ją później. Aby uzyskać informacje o instalowaniu serwera programu RStudio po utworzeniu klastra, zobacz [Instalowanie serwera programu RStudio w klastrach HDInsight](hdinsight-hadoop-r-server-install-r-studio.md). Umożliwia też łączność toohello R Server przy użyciu konsoli hello R tooaccess SSH/PuTTY. 

## <a name="develop-and-run-r-scripts"></a>Tworzenie i uruchamianie skryptów R
skrypty Hello R, tworzenie i uruchamianie można użyć dowolnego z hello 8000 + pakietów typu open source R w toohello dodanie zarządzana z przetwarzaniem i procedury, które są dostępne w bibliotece ScaleR hello rozproszonych. Ogólnie rzecz biorąc skrypt, który jest uruchamiany z serwerem R w węźle krawędzi hello jest uruchamiany w ramach interpreter hello R w tym węźle. Wyjątki Hello są te kroki, które wymagają toocall funkcję ScaleR z kontekstem obliczeniowych ustawiona tooHadoop mapy Zmniejsz (RxHadoopMR) lub Spark (RxSpark). W takim przypadku funkcja hello działa w sposób rozproszonych w tych węzłów danych (zadania) hello klastra, które są powiązane z danymi hello odwołuje się do. Aby uzyskać więcej informacji na temat opcji kontekstu obliczeń różnych hello zobacz [obliczeniowe kontekstu opcje serwera R w usłudze HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Operacjonalizuj modelu
Po zakończeniu Twojej modelowania danych, aby operacjonalizować hello modelu toomake prognoz dotyczących nowych danych z platformy Azure i lokalnymi. Ten proces jest nazywany oceniania. Ocenianie może odbywać się w HDInsight, uczenie maszynowe Azure lub lokalnie.

### <a name="score-in-hdinsight"></a>Wynik w usłudze HDInsight
tooscore w usłudze HDInsight, zapisać R funkcję, która wywołuje z modelu toomake prognoz dla nowego pliku danych czy załadowany tooyour konta magazynu. Następnie zapisz prognoz hello wstecz toohello konta magazynu. Hello rutynowych na żądanie można uruchamiać na powitania krawędzi węzła klastra lub przy użyciu zaplanowanego zadania.  

### <a name="score-in-azure-machine-learning-aml"></a>Wynik na platformie Azure maszyny uczenia (AML)
przy użyciu usługi sieci web AML, użyj hello tooscore otwórz źródłowy pakiet Azure Machine Learning R znany jako [uczenie maszynowe Azure](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish model jako usługę sieci web platformy Azure. Dla wygody ten pakiet jest wstępnie zainstalowane w węźle krawędzi hello. Następnie używać urządzeń hello w toocreate uczenia maszynowego interfejsu użytkownika dla usługi sieci web hello, a następnie wywoływania usługi sieci web hello odpowiednio do oceniania.

Jeśli wybierzesz tę opcję, należy używać żadnych ScaleR modelu obiektów tooequivalent open source model obiektów dla z usługą sieci web hello tooconvert. Używać funkcji koercja ScaleR, takich jak `as.randomForest()` dla modeli opartych na zespół, dla tej konwersji.

### <a name="score-on-premises"></a>Wynik lokalnymi
tooscore lokalnego po utworzeniu modelu, może serializować hello modelu w R, pobierania, zdeserializować go, a następnie użyć jej do oceniania nowych danych. Można oceniać nowe dane przy użyciu hello podejścia opisanego wcześniej w [oceniania w usłudze HDInsight](#scoring-in-hdinsight) lub za pomocą [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Obsługa klastra hello
### <a name="install-and-maintain-r-packages"></a>Zainstalowanie i konserwowanie pakiety języka R
Na węzeł brzegowy hello od większości kroki skryptów R uruchomienia są wymagane większość pakietów hello R, których używasz. tooinstall dodatkowe pakiety języka R w węźle krawędzi hello, można użyć hello zwykle `install.packages()` metody w języku R.

Jeśli właśnie używasz procedury z biblioteki ScaleR hello w klastrze hello, zazwyczaj zbędna, nie tooinstall dodatkowe pakiety języka R na powitania węzły danych. Jednak może być konieczne użycie hello toosupport dodatkowe pakiety **rxExec** lub **RxDataStep** wykonywania na powitania węzły danych.

W takich przypadkach można zainstalować dodatkowe pakiety hello przy użyciu akcji skryptu po utworzeniu klastra hello. Aby uzyskać więcej informacji, zobacz [tworzenia klastra usługi HDInsight z serwerem R](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Zmiany ustawień pamięci zmniejszyć mapy usługi Hadoop
Klaster może być zmodyfikowany toochange hello ilość pamięci, która jest dostępna tooR serwera podczas ich działania zadania zmniejszyć mapy. toomodify klaster, użyj hello interfejsu Apache Ambari użytkownika, który jest dostępny za pośrednictwem hello Azure bloku portalu dla klastra. Aby uzyskać instrukcje dotyczące sposobu tooaccess hello Ambari interfejsu użytkownika dla klastra, zobacz [Zarządzanie klastrów usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md).

Jest również możliwe toochange hello ilość pamięci, która jest dostępna tooR serwera przy użyciu Hadoop przełączników zbyt w wywołaniu hello**RxHadoopMR** w następujący sposób:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Skalowanie klastra
Istniejącego klastra można skalować w górę lub w dół za pośrednictwem portalu hello. Skalowanie, można uzyskać hello dodatkowej pojemności może być potrzebny większy zadań przetwarzania lub można skalować wstecz klastra w stanie bezczynności. Aby uzyskać instrukcje dotyczące tooscale klastra, zobacz [Zarządzanie klastrami usługi HDInsight](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Obsługa systemu hello
Poprawek systemu operacyjnego tooapply konserwacji i inne aktualizacje odbywa się na powitania bazowy maszyn wirtualnych systemu Linux w klastrze HDInsight poza godzinami. Zazwyczaj każdy poniedziałek i czwartek konserwacji odbywa się na 3:30 AM (oparty na czasie lokalnym hello hello maszyny Wirtualnej). Aktualizacji są wykonywane w taki sposób, że ich nie mieć wpływ na więcej niż kwartału hello klastra w czasie.  

Ponieważ węzłów głównych hello są zbędne, a nie wszystkie węzły danych ma wpływ, wszystkie zadania, które są uruchomione w tym czasie może spowolnić. One nadal uruchamiać toocompletion, jednak. Niestandardowe oprogramowania ani danych lokalnych, czy masz jest zachowywana przez te zdarzenia konserwacji o ile nie wystąpił błąd krytyczny wymagającego odbudowie klastra.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Więcej informacji na temat opcji IDE platformy R Server w klastrze usługi HDInsight
Witaj Linux krawędzi węzeł klastra usługi HDInsight jest hello lądowanie strefę dla analizy na podstawie R. Nowe wersje HDInsight zapewniają domyślną opcją instalacji hello społecznościową wersję [serwera programu RStudio](https://www.rstudio.com/products/rstudio-server/) na powitania węzła krawędzi jako środowiska IDE bazujące na przeglądarce. Korzystania z serwera programu RStudio jako IDE dla rozwoju hello i wykonywanie skryptów R może być znacznie większą wydajność niż tylko przy użyciu konsoli hello R. Jeśli podczas tworzenia hello klastra, a chcesz tooadd nieinstalowanie tooadd serwera programu RStudio go później, następnie zobacz [Instalowanie serwera Studio R w klastrach HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Inną opcją pełnej IDE jest tooinstall pulpitu IDE i użyć tooaccess hello klastra przy użyciu zdalnego kontekstu obliczeń Zmniejsz mapy lub Spark. Dostępne są następujące opcje firmy Microsoft [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS), programu RStudio i Walware na podstawie Eclipse [StatET](http://www.walware.de/goto/statet).

Ponadto dostępnych hello konsoli R Server w węźle krawędzi hello wpisując **R** w wierszu polecenia systemu Linux powitania po nawiązaniu połączenia za pośrednictwem protokołu SSH lub PuTY. Korzystając z interfejsu konsoli hello, go to wygodny toorun Edytor tekstów rozwoju skryptu języka R w innym oknie i wycinanie i wklejanie sekcje skryptu do konsoli hello R, zgodnie z potrzebami.

## <a name="learn-about-pricing"></a>Informacje na temat cen
Witaj opłat skojarzonych z usługą HDInsight, klaster z serwerem R są strukturę podobną toohello opłaty za klastry usługi HDInsight standard hello. Są one oparte na powitania rozmiar hello bazowy maszyn wirtualnych przez nazwę hello, danych i węzły krawędzi, o dodanie hello wzrost core godzinnym. Aby uzyskać więcej informacji o cenach usługi HDInsight i dostępności hello bezpłatnej 30-dniowej wersji próbnej, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat sposobu klastrów toouse R Server z usługą HDInsight, zobacz następujące tematy hello:

* [Rozpoczynanie pracy z serwerem R w usłudze HDInsight](hdinsight-hadoop-r-server-get-started.md)
* [Dodaj serwer programu RStudio tooHDInsight (Jeśli nie zainstalowano podczas tworzenia klastra)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)
* [Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)
