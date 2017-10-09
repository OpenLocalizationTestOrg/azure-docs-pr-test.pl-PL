---
title: "tooAzure aaaConnect HDInsight przy użyciu narzędzi Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i użycia narzędzi Data Lake Tools dla Visual Studio tooconnect tooHadoop klastrów w usłudze Azure HDInsight i uruchamiania zapytań Hive."
keywords: hadoop tools,hive query,visual studio,visual studio hadoop
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Łączenie tooAzure HDInsight i uruchamianie zapytań Hive przy użyciu narzędzi Data Lake Tools dla programu Visual Studio

Dowiedz się, jak toouse narzędzi Data Lake Tools dla Visual Studio tooconnect tooHadoop klastrów w [Azure HDInsight](hdinsight-hadoop-introduction.md) i wysyłanie zapytań programu Hive. Aby uzyskać więcej informacji o korzystaniu z usługi HDInsight, zobacz [tooHDInsight wprowadzenie](hdinsight-hadoop-introduction.md) i [Rozpoczynanie pracy z usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Aby uzyskać więcej informacji na temat łączącego klaster Storm tooa zobacz [topologii opracowywania C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Narzędzia Data Lake Tools dla programu Visual Studio może być używane tooaccess zarówno usługi Data Lake Analytics i HDInsight.  Aby hello informacji na temat narzędzia Data Lake Tools, zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Wymagania wstępne**

toocomplete tego samouczka i użyj hello Data Lake Tools w programie Visual Studio, potrzebne są następujące hello:

* Klaster Azure HDInsight: jeden, zobacz toocreate [rozpocząć korzystanie z usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Stacja robocza z hello następującego oprogramowania:
  
  * Windows 10, Windows 8.1, Windows 8 lub Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Obecnie hello Data Lake Tools dla programu Visual Studio występują tylko hello angielską wersję.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Instalacja narzędzi Data Lake Tools for Visual Studio

Narzędzia Data Lake Tools są domyślnie instalowane w programie Visual Studio 2017. Dla starszych wersji, można zainstalować za pomocą hello [Instalatora platformy sieci Web](https://www.microsoft.com/web/downloads/). Musisz wybrać hello, który odpowiada używanej wersji programu Visual Studio. Jeśli nie masz zainstalowanego programu Visual Studio, możesz zainstalować hello najnowsze Visual Studio Community i zestawu SDK platformy Azure przy użyciu hello [Instalatora platformy sieci Web](https://www.microsoft.com/web/downloads/):

![Narzędzia Data Lake Tools dla Instalatora platformy sieci Web w usłudze Visual Studio. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Tooinstall Instalatora platformy sieci Web użycia narzędzi Data Lake Tools dla programu Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Połącz tooAzure subskrypcji
Narzędzia Data Lake Tools dla Visual Studio umożliwia tooconnect tooyour klastrów usługi HDInsight, wykonywania podstawowych operacji zarządzania i uruchamianie zapytań Hive.

> [!NOTE]
> Informacje dotyczące łączenia tooa ogólnym klastrem Hadoop znajdują się w temacie [zapisu i wysyłanie zapytań programu Hive za pomocą programu Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooyour tooconnect subskrypcji platformy Azure**

1. Otwórz program Visual Studio.
2. Z hello **widoku** menu, kliknij przycisk **Eksploratora serwera** okno Eksploratora serwera na powitania tooopen.
3. Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.
   
   > [!NOTE]
   > Powiadomienie hello **listy zadań HDInsight** okno powinno być otwarte. Jeśli nie widzisz, kliknij przycisk **inne okna** z hello **widoku** menu, a następnie kliknij przycisk **okno listy zadań HDInsight**.  
   > 
   > 
4. Wprowadź swoje poświadczenia subskrypcji platformy Azure, a następnie kliknij przycisk **Zaloguj**. Jest to tylko wymagane, jeśli nigdy nie nawiązano toohello subskrypcji platformy Azure w programie Visual Studio na tej stacji roboczej.
5. W oknie Eksploratora serwera zostanie wyświetlona lista istniejących klastrów usługi HDInsight. Jeśli nie masz żadnych klastrów, można utworzyć za pomocą hello portalu Azure, programu Azure PowerShell lub hello zestawu SDK HDInsight. Więcej informacji można znaleźć w artykule [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów usługi HDInsight).
   
   ![Lista klastrów Eksploratora serwera narzędzi Data Lake Tools for Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Eksplorator serwera narzędzi Data Lake Tools for Visual Studio")
6. Rozwiń węzeł klastra usługi HDInsight. Zobaczysz **Bazy danych programu Hive**, domyślne konto magazynu, połączone konta magazynu i **Dziennik usługi Hadoop**. Witaj jednostki można rozwinąć.

Po nawiązaniu połączenia tooyour subskrypcji platformy Azure, będziesz w stanie toodo hello poniżej:

**toohello tooconnect portalu Azure w programie Visual Studio**

* Z poziomu Eksploratora serwera rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy klaster usługi HDInsight, a następnie kliknij przycisk **Zarządzaj klastrem w witrynie Azure Portal**.

**tooask pytania i wyrazić swoją opinię w programie Visual Studio**

* Z hello **narzędzia** menu, kliknij przycisk **HDInsight**, a następnie kliknij przycisk **MSDN Forum** tooask pytania, lub kliknij przycisk **Przekaż opinię**.

## <a name="navigate-hello-linked-resources"></a>Przejdź hello połączonych zasobów
W Eksploratorze serwera widać hello domyślne konto magazynu i wszystkie połączone konta magazynu. Po rozwinięciu hello domyślne konto magazynu, można wyświetlić kontenery hello na powitania konta magazynu. Witaj domyślne konto magazynu i hello domyślny kontener są oznaczone. Użytkownik może również prawym przyciskiem myszy dowolny hello kontenery tooview hello zawartość.

![Połączone zasoby listy Eksploratora serwera narzędzi Data Lake Tools for Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "połączone zasoby listy")

Po otwarciu kontener, można użyć hello następujące przyciski tooupload, usuwania i pobierania obiektów blob:

![Operacje obiektów blob Eksploratora serwera narzędzi Data Lake Tools for Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "przekazywanie, usuwanie i pobieranie obiektów blob")

## <a name="run-a-hive-query"></a>Uruchomienie zapytania programu Hive
[Apache Hive](http://hive.apache.org) to infrastruktura magazynu danych oparta na usłudze Hadoop umożliwiająca dostarczanie podsumowań, zapytań i analizy danych. Narzędzia Data Lake Tools for Visual Studio obsługują uruchamianie zapytań programu Hive w programie Visual Studio. Aby uzyskać więcej informacji na temat programu Hive, zobacz artykuł [Use Hive with HDInsight](hdinsight-use-hive.md) (Korzystanie z programu Hive z usługą HDInsight).

Jest czasochłonne tootest skryptu Hive w odniesieniu do klastra usługi HDInsight. Może potrwać kilka minut lub dłużej. Narzędzia Data Lake Tools dla programu Visual Studio jest w stanie sprawdzić poprawność skryptu Hive lokalnie bez łączącego tooa działającym klastrem.

Narzędzia Data Lake Tools dla programu Visual Studio umożliwia również użytkownikom toosee zawartość jest widoczna hello zadania Hive, zbierając i udostępniając dzienniki YARN wybranych zadań Hive hello.

### <a name="view-hello-hivesampletable"></a>Widok hello **hivesampletable**
Wszystkie klastry usługi HDInsight zawierają przykładową tabelę programu Hive o nazwie *hivesampletable*. Użyjemy tooshow tej tabeli, należy jak toolist tabele programu Hive, przeglądać schematy tabeli hello i wyświetlać wiersze hello hello Hive tabeli.

**tabele programu Hive toolist i schemat tabeli programu Hive widoku**

1. Z **Eksploratora serwera**, rozwiń węzeł **Azure** > **HDInsight** > hello klaster > **bazy danych programu Hive**  >  **Domyślne** > **hivesampletable** toosee hello tabeli schematu.
2. Kliknij prawym przyciskiem myszy **hivesampletable**, a następnie kliknij przycisk **Wyświetl pierwszych 100 wierszy** toolist hello wierszy. Jest równoważne toorunning hello następujące zapytanie Hive za pomocą sterownika ODBC programu Hive:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Liczba wierszy hello można dostosować.
   
   ![Narzędzia Data Lake Tools: zapytanie schematu HDInsight Hive Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Wyniki zapytania programu Hive")

### <a name="create-hive-tables"></a>Tworzenie tabel programu Hive
Można użyć toocreate GUI hello tabeli programu Hive lub zapytań programu Hive. Aby uzyskać informacje o używaniu zapytań programu Hive, zobacz temat [Uruchamianie zapytań Hive](#run.queries).

**toocreate tabeli programu Hive**

1. Z poziomu **Eksploratora serwera** rozwiń węzeł **Azure** > **Klastry usługi HDInsight** klaster usługi HDInsight > **Bazy danych programu Hive**, następnie kliknij prawym przyciskiem myszy pozycję **domyślne** i kliknij przycisk **Utwórz tabelę**.
2. Skonfiguruj hello tabeli.
3. Kliknij przycisk **Create Table** toosubmit hello zadania toocreate hello nową tabelę programu Hive.
   
    ![Narzędzia Data Lake Tools: narzędzia HDInsight Visual Studio Tools tworzą tabelę programu Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Tworzenie tabeli programu Hive")

### <a name="run.queries"></a>Weryfikowanie i uruchamianie zapytań Hive
Istnieją dwa sposoby toocreate i wykonywania zapytań Hive:

* Tworzenie zapytań ad hoc
* Tworzenie aplikacji Hive

**toocreate, weryfikowanie i uruchamianie zapytań ad hoc**

1. Z poziomu **Eksploratora serwera** rozwiń węzeł **Azure**, a następnie rozwiń pozycję **Klastry usługi HDInsight**.
2. Kliknij prawym przyciskiem myszy hello klastra, gdzie mają toorun hello zapytania, a następnie kliknij **Napisz zapytanie Hive**.
3. Wprowadź zapytania Hive hello. Edytor Hive hello powiadomienia obsługuje funkcję IntelliSense. Narzędzia Data Lake Tools dla Visual Studio obsługuje ładowanie hello zdalnych metadanych podczas edycji skryptu Hive. Na przykład po wpisaniu "SELECT * FROM", powitalne IntelliSense wyświetla hello wszystkie sugerowane nazwy tabeli. Po określeniu nazwy tabeli nazwy kolumn hello są wyświetlane według hello IntelliSense. narzędzia Hello obsługuje prawie wszystkie instrukcje DML programu Hive, podzapytania i hello wbudowane sterowniki UDF.
   
    ![Narzędzia Data Lake Tools: funkcja IntelliSense narzędzi HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Narzędzia Data Lake Tools: funkcja IntelliSense narzędzi HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Zostaną zasugerowane tylko hello metadane klastrów hello wybranego w pasku narzędzi usługi HDInsight.
   > 
   > 
4. (Opcjonalnie): kliknij **Weryfikuj skrypt** błędy składniowe skryptu hello toocheck.
   
    ![Data Lake Tools: lokalna weryfikacja narzędzi Data Lake Tools for Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Weryfikacja skryptu")
5. Kliknij przycisk **Prześlij** lub **Prześlij (zaawansowane)**. Z hello zaawansowanych opcji przesyłania, należy skonfigurować **Nazwa zadania**, **argumenty**, **dodatkowe konfiguracje**, i **katalog stanu**hello skryptu:
   
    ![Zapytanie programu Hive w usłudze HDInsight Hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Przesłanie zapytań")
   
    Po przesłaniu zadania hello zobacz **Podsumowanie zadania Hive** okna.
   
    ![Podsumowanie zapytania programu Hive w usłudze HDInsight Hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Podsumowanie zadania Hive")
6. Użyj hello **Odśwież** przycisk tooupdate hello stan do momentu zmiany stanu zadania hello zbyt**Ukończono**.
7. Kliknij łącza hello na powitania dolnej toosee hello następujących: **zapytanie dotyczące zadań**, **dane wyjściowe zadania**, **dziennik zadań**, lub **dziennik Yarn**.

**toocreate i uruchamianie rozwiązania Hive**

1. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
2. Wybierz **HDInsight** w okienku po lewej stronie powitania, wybierz **aplikacji Hive** w środkowym okienku hello, wprowadź właściwości hello, a następnie kliknij przycisk **OK**.
   
    ![Narzędzia Data Lake Tools: nowy projekt programu Hive w usłudze HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Tworzenie aplikacji Hive z programu Visual Studio")
3. Z **Eksploratora rozwiązań**, kliknij dwukrotnie **Script.hql** tooopen go.
4. toovalidate hello skryptu Hive, możesz kliknąć hello **Weryfikuj skrypt** przycisku, lub kliknij prawym przyciskiem myszy skrypt hello w edytorze Hive hello, a następnie kliknij przycisk **Weryfikuj skrypt** z menu kontekstowego hello.

### <a name="view-hive-jobs"></a>Wyświetlanie zadań Hive
Istnieje możliwość wyświetlenia zapytań dotyczących zadań, danych wyjściowych zadań, dzienników zadań oraz dzienników Yarn dla zadań Hive. Aby uzyskać więcej informacji zobacz poprzedni zrzut ekranu: hello.

Witaj najbardziej aktualną wersją narzędzi hello umożliwia toosee co to jest zadań Hive, zbierając i udostępniając dzienniki YARN. Dziennik YARN może być pomocny w badaniu problemów z wydajnością.  Więcej informacji na temat sposobu zbierania dzienników YARN przez usługę HDInsight można znaleźć w artykule [Access HDInsight Application Logs Programmatically](hdinsight-hadoop-access-yarn-app-logs.md) (Programowe uzyskiwanie dostępu do dzienników aplikacji usługi HDInsight).

**tooview zadań Hive**

1. Z poziomu **Eksploratora serwera** rozwiń węzeł **Azure**, a następnie rozwiń pozycję **HDInsight**.
2. Kliknij prawym przyciskiem myszy klaster usługi HDInsight, a następnie kliknij przycisk **Wyświetl zadania**. Zobaczysz listę hello zadań uruchomionych w klastrze hello Hive.
3. Kliknij zadanie w tooselect listy zadań hello ją, a następnie użyj hello **Podsumowanie zadania Hive** tooopen okna **zapytanie dotyczące zadań**, **dane wyjściowe zadania**, **dziennik zadań**, lub **dziennik Yarn**.
   
    ![Narzędzia Data Lake Tools: zadania Hive widoku narzędzi HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Wyświetlanie zadań Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Szybsza ścieżka wykonywania zadań Hive za pośrednictwem serwera HiveServer2
> [!NOTE]
> Ta funkcja działa tylko w klastrze HDInsight w wersji 3.2 i nowszej.
> 
> 

Witaj Data Lake Tools używane toosubmit zadań Hive za pośrednictwem [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (znanej także jako Templeton). Zajęło tooreturn długo szczegółów zadania i informacji o błędzie.
Kolejność toosolve ten problem z wydajnością, powitalne wykonuje narzędzi Data Lake Tools Hive zadania bezpośrednio w klastrze hello za pośrednictwem serwera HiveServer2, dzięki czemu pozwala pominąć użycie protokołu RDP/SSH.
Dodanie toobetter wydajności użytkowników można również wyświetlić gałęzi na wykresach Tez oraz hello szczegóły zadania.

W przypadku klastra HDInsight w wersji 3.2 lub nowszej widoczny jest przycisk **Wykonaj na serwerze HiveServer2**:

![Wykonywanie przez narzędzia Data Lake Visual Studio Tools na serwerze hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Wykonywanie zapytań Hive przy użyciu serwera HiveServer2")

I możesz wyświetlić hello dzienniki przesyłane strumieniowo z powrotem w czasie rzeczywistym i zobacz hello wykresy zadań, jeśli zapytanie Hive hello jest wykonywane w aplikacji Tez.

![Szybka ścieżka wykonywania zadań Hive w usłudze Data Lake Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Wyświetlanie wykresów zadań")

**Różnica między wykonywaniem zapytań za pomocą serwera HiveServer2 i wysyłaniem zapytań przy użyciu usługi WebHCat**

Mimo że wykonywanie zapytań za pośrednictwem serwera HiveServer2 ma wiele zalet dotyczących wydajności, ma również kilka ograniczeń. Niektóre ograniczenia hello nie są odpowiednie do użycia w produkcji. Witaj poniższej tabeli przedstawiono różnice hello:

|  | Wykonywanie za pośrednictwem serwera HiveServer2 | Przesyłanie za pośrednictwem usługi WebHCat |
| --- | --- | --- |
| Wykonywanie zapytań |Eliminuje obciążenie hello w usłudze WebHCat (co spowoduje uruchomienie zadania MapReduce o nazwie "TempletonControllerJob"). |Jeśli zapytanie jest wykonywane przy użyciu usługi WebHCat, spowoduje ona uruchomienie zadania MapReduce, które wprowadza dodatkowe opóźnienia. |
| Strumieniowe przesyłanie dzienników z powrotem |Niemal w czasie rzeczywistym. |Dzienniki wykonywania zadania Hello są dostępne tylko wtedy, gdy hello zadanie zostało zakończone. |
| Wyświetlanie historii zadań |Jeśli zapytanie jest wykonywane przy użyciu serwera HiveServer2, jego historia zadania, dziennik zadania ani dane wyjściowe zadania nie są zachowywane. Aplikacja Hello można wyświetlić w interfejsie użytkownika YARN z ograniczonymi informacjami. |Jeśli zapytanie jest wykonywane przy użyciu usługi WebHCat, historia zadania, dziennik zadania i dane wyjściowe zadania są zachowywane i można je wyświetlać za pomocą programu Visual Studio/HDInsight SDK PowerShell. |
| Zamykanie okna |Wykonywanie za pośrednictwem serwera HiveServer2 jest sposób "synchroniczny", dlatego należy pozostawić powitalne windows Otwórz; Jeśli system windows hello są zamknięte hello wykonywania zapytania zostaną anulowane. |Przesyłanie za pośrednictwem usługi WebHCat jest sposób "asynchroniczny", dlatego może przesłać kwerendy hello przy użyciu usługi WebHCat i zamknąć program Visual Studio. Można wrócić i wyświetlić wyniki hello w dowolnym momencie. |

### <a name="tez-hive-job-performance-graph"></a>Wykres wydajności zadania Hive w aplikacji Tez
Obsługa narzędzi Data Lake Tools Hello wyświetlanie wykresów wydajności dla hello zadań Hive uruchomionych przez aparat wykonywania Tez hello. Aby uzyskać informacje na temat włączania aplikacji Tez, zobacz artykuł [Use Hive in HDInsight](hdinsight-use-hive.md) (Używanie programu Hive w usłudze HDInsight). Po przesłaniu gałąź pokazuje zadania w programie Visual Studio, Visual Studio hello wykres po zakończeniu zadania hello.  Może być konieczne tooclick hello **Odśwież** przycisk tooget hello najnowszego stanu zadania.

> [!NOTE]
> Ta funkcja jest dostępna tylko dla klastra usługi HDInsight w wersji nowszej niż 3.2.4.593 i można jej używać tylko w przypadku zakończonych zadań (jeśli zadanie zostało przesłane za pośrednictwem usługi WebHCat; ten wykres zostanie wyświetlony podczas wykonywania zapytania za pośrednictwem serwera HiveServer2). Działa to zarówno w przypadku klastrów w systemie Windows, jak i Linux.
> 
> 

![Wykres wydajności aplikacji Tez w usłudze Hadoop Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Stan zadania")

toohelp zrozumieć programu Hive kwerendy lepsze, narzędzia hello Dodaj widok operatorów Hive hello w tej wersji. Wystarczy toodouble, kliknij pozycję hello wierzchołki wykresu zadania hello, aby zobaczyć wszystkie operatory hello wewnątrz wierzchołka hello. Możesz również przesunąć na tooview konkretnym operatorze więcej szczegółów dotyczących tego operatora.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Widok wykonywania zadania dla zadań Hive w aplikacji Tez
Witaj widok wykonywania zadania dla Hive w aplikacji Tez zadania można użyć tooget strukturalnych i wizualizowanych informacji na temat zadań Hive i uzyskać więcej szczegółów zadania. Gdy występują problemy z wydajnością, można użyć widoku hello tooget dalszych szczegółów. Na przykład jak każdego zadania działa i hello szczegółowe informacje dotyczące każdego zadania (odczytu i zapisu danych, harmonogramu/rozpoczęcia/zakończenia, itp.), tak, aby dostroić konfigurację zadania lub architekturę systemu na podstawie informacji hello wizualizowane.

![Widok wykonywania zadań narzędzi Data Lake Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Widok wykonywania zadań")

## <a name="run-pig-scripts"></a>Uruchamianie skryptów usługi Pig
Narzędzia Data Lake Tools dla programu Visual Studio obsługują tworzenie i przesyłanie klastrów tooHDInsight skrypty Pig. Użytkownicy mogą utworzyć projekt usługi Pig na podstawie szablonu i przesłać hello skryptu tooHDInsight klastrów.

## <a name="feedbacks--known-issues"></a>Opinie i znane problemy
* Obecnie wyniki serwera HiveServer2 są wyświetlane w formie czystego tekstu, co nie jest idealnym rozwiązaniem. Pracujemy nad rozwiązaniem tego problemu.
* Jeśli hello rozpoczynające się od wartości NULL, obecnie hello wyników nie są pokazywane. Firma Microsoft ten problem, a jeśli są zablokowane na ten problem, możesz wolnego toodrop zespołu pomocy technicznej dla instytucji adres e-mail lub skontaktuj się z pomocą.
* skrypt HQL Hello utworzony przez program Visual Studio jest zakodowany w zależności od ustawienia lokalnego regionu użytkownika. Go może zostać wykonane nieprawidłowo Jeśli użytkownik prześle hello toocluster skryptu jako wartość binarną.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób tooconnect tooHDInsight klastrów w programie Visual Studio za pomocą usługi Data Lake hello (HDInsight) pakietu narzędzi i w jaki sposób toorun zapytań programu Hive. Aby uzyskać więcej informacji, zobacz:

* [Use Hadoop Hive in HDInsight](hdinsight-use-hive.md) (Używanie usługi Hadoop Hive w usłudze HDInsight)
* [Rozpoczęcie korzystania z usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Przesyłanie zadań Hadoop w usłudze HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Analizowanie danych z serwisu Twitter na platformie Hadoop w usłudze HDInsight](hdinsight-analyze-twitter-data.md)

