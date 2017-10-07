---
title: "aaaUse Apache Storm w usłudze Power BI - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Tworzenie raportu usługi Power BI przy użyciu danych z topologii C# uruchomiona w klastrze Apache Storm w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Użyj usługi Power BI toovisualize danych od topologii Apache Storm

Usługa Power BI umożliwia toovisually Wyświetl dane jako raporty. Ten dokument zawiera przykładowy sposób toouse Apache Storm na HDInsight toogenerate danych dla usługi Power BI.

> [!NOTE]
> Witaj kroki opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio. Hello skompilowany projekt może być przesłane tooa opartych na systemie Linux klaster usługi HDInsight. Tylko opartych na systemie Linux klastrów utworzone po 10/28/2016 Obsługa SCP.NET topologii.
>
> toouse topologii C# z opartą na systemie Linux klastrem, hello aktualizacji pakietu Microsoft.SCP.Net.SDK NuGet używana przez tooversion Twojego projektu 0.10.0.6 lub nowszej. Hello wersję pakietu hello musi być również zgodna wersja główna hello Storm zainstalowany w usłudze HDInsight. Na przykład system Storm występujący w usłudze HDInsight w wersjach 3.3 i 3.4 jest w wersji 0.10.x, a usługa HDInsight 3.5 używa systemu Storm 1.0.x.
>
> Topologie języka C# w klastrach opartych na systemie Linux należy użyć .NET 4.5 i użyj Mono toorun na powitania klastra usługi HDInsight. Większość elementów pracy. Należy jednak sprawdzić hello [zgodności Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.
>
> Wersja języka Java tego projektu, który współpracuje z usługą HDInsight opartą na systemie Linux lub z systemem Windows, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Użytkownik usługi Azure Active Directory z [usługi Power BI](https://powerbi.com) dostępu.
* Klaster usługi HDInsight. Aby uzyskać więcej informacji, zobacz [wprowadzenie Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Visual Studio (jedna hello następujące wersje)

  * Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Program Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (dowolna wersja)

* Witaj narzędzia HDInsight Tools for Visual Studio: zobacz [rozpocząć korzystanie z hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) uzyskać informacji o informacje dotyczące instalacji.

## <a name="how-it-works"></a>Jak to działa

Ten przykład zawiera topologii Storm C# losowo generowany danych dziennika usług Internet Information Services (IIS). Te dane są następnie zapisywane tooa bazy danych SQL i tam jest używane toogenerate raporty w usłudze Power BI.

Witaj następujące główne funkcje hello wdrożenie plików w tym przykładzie:

* **SqlAzureBolt.cs**: zapisuje informacje wygenerowane w tooSQL topologii Storm hello bazy danych.
* **IISLogsTable.sql**: hello języka Transact-SQL instrukcje używane toogenerate hello bazy danych, która hello dane są przechowywane w.

> [!WARNING]
> Utwórz tabelę hello w bazie danych SQL, przed rozpoczęciem powitalne topologii w klastrze usługi HDInsight.

## <a name="download-hello-example"></a>Pobierz przykład Witaj

Pobierz hello [przykład HDInsight C# Storm usługi Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, albo rozwidlenia/klonowania za pomocą [git](http://git-scm.com/), lub użyj hello **Pobierz** toodownload łącze .zip hello archiwum.

## <a name="create-a-database"></a>Tworzenie bazy danych

1. toocreate bazy danych, wykonaj kroki hello w hello [samouczek usługi SQL Database](../sql-database/sql-database-get-started.md) dokumentu.

2. Bazy danych toohello Połącz przez hello następujące kroki w hello [połączyć tooa bazy danych SQL z programem Visual Studio](../sql-database/sql-database-connect-query.md) dokumentu.

3. W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazy danych, a następnie wybierz **nowe zapytanie**. Wklej zawartość hello hello **IISLogsTable.sql** dołączony hello pobrany projekt w oknie zapytania hello, a następnie użyj klawiszy Ctrl + Shift + E tooexecute hello zapytania. Wiadomość hello polecenia zakończyła się pomyślnie, powinien zostać wyświetlony.

## <a name="configure-hello-sample"></a>Konfigurowanie przykładowej hello

1. Z hello [portalu Azure](https://portal.azure.com), wybierz bazę danych SQL. Z hello **Essentials** sekcji hello SQL bloku bazy danych, wybierz opcję **Pokaż parametry połączenia bazy danych**. Na wyświetlonej liście hello skopiuj hello **ADO.NET (uwierzytelnianie SQL)** informacji.

2. Przykład Witaj Otwórz w programie Visual Studio. Z **Eksploratora rozwiązań**, otwórz hello **App.config** pliku, a następnie znajdź hello wejścia:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Zastąp hello **TOBEFILLED ##** wartości z ciągu połączenia bazy danych hello skopiowany w poprzednim kroku hello. Zastąp **{Twojej\_username}** i **{Twojej\_hasło}** hello nazwy użytkownika i hasło na powitania bazy danych.

3. Zapisz i zamknij hello plików.

## <a name="deploy-hello-sample"></a>Wdrażanie przykładowej hello

1. Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **StormToSQL** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**. Wybierz hello klastra usługi HDInsight z hello **klaster Storm** okna dialogowego z listy rozwijanej.

   > [!NOTE]
   > Może to potrwać kilka sekund na powitania **klaster Storm** toopopulate listy rozwijanej o nazwy serwerów.
   >
   > Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.

2. Po przesłaniu topologii hello hello __podglądu topologii__ pojawi się. tooview tej topologii, wybierz hello SqlAzureWriterTopology wpisu z listy hello.

    ![topologie Hello, z topologią hello wybrane](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Można użyć tego widoku toosee informacji na temat topologii hello, lub kliknij dwukrotnie wpis (na przykład hello SqlAzureBolt) toosee informacji tooa określonego składnika w topologii hello.

3. Po hello topologii ma był uruchamiany przez kilka minut, oknie zapytania SQL zwracany toohello używane toocreate hello w bazie danych. Zastąp istniejące instrukcje hello hello następujące zapytania:

        select * from iislogs;

    Użyj klawiszy Ctrl + Shift + E tooexecute hello zapytania, a powinien zostać wyświetlony wyniki toohello podobne następujące dane:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Te dane od topologii Storm hello została zapisana.

## <a name="create-a-report"></a>Tworzenie raportu

1. Połącz toohello [łącznika usługi Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) dla usługi Power BI. 

2. W ramach **baz danych**, wybierz pozycję **uzyskać**.

3. Wybierz **bazy danych SQL Azure**, a następnie wybierz **Connect**.

    > [!NOTE]
    > Konieczne podanie toodownload hello Power BI Desktop toocontinue. Jeśli tak, użyj powitania po tooconnect kroki:
    >
    > 1. Otwórz Power BI Desktop i wybierz __Pobierz dane__.
    > Wybierz 2 __Azure__, a następnie __bazy danych Azure SQL__.

4. Wprowadź hello informacji tooconnect tooyour bazy danych SQL Azure. Te informacje można znaleźć na stronie powitania [portalu Azure](https://portal.azure.com) i wybrać bazę danych SQL.

   > [!NOTE]
   > Można również ustawić interwał odświeżania hello i filtry niestandardowe przy użyciu **włączyć zaawansowane opcje** hello Połącz okna dialogowego.

5. Po nawiązaniu połączenia, pojawi się nowy zestaw danych z hello takie same nazwy jako hello bazy danych zostanie połączony. Wybierz toobegin dataset hello projektowania raportu.

6. Z **pola**, rozwiń węzeł hello **IISLOGS** wpisu. toocreate raport, że listy hello URI wynika, zaznacz pole wyboru powitania dla **URISTEM**.

    ![Tworzenie raportu](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Następnie przeciągnij **metody** toohello raportu. Witaj raport aktualizacje toolist Witaj wynika i hello odpowiedniej metody HTTP używany do hello żądania HTTP.

    ![Dodawanie hello danych — metoda](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Z hello **wizualizacje** kolumnę, wybierz hello **pola** ikonę, a następnie wybierz hello Strzałka w dół obok zbyt**— metoda** w hello **wartości**sekcji. Wybierz toodisplay uzyskaniu liczba ile razy identyfikatora URI **liczba**.

    ![Zmiana liczby tooa metod](./media/hdinsight-storm-power-bi-topology/count.png)

9. Następnie wybierz pozycję hello **skumulowany wykres kolumnowy** toochange sposób wyświetlania informacji hello.

    ![Zmiana tooa skumulowany wykres.](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. toosave hello raportu, wybierz opcję **zapisać** , a następnie wprowadź nazwę raportu hello.

## <a name="stop-hello-topology"></a>Zatrzymywanie topologii hello

toorun topologii Hello będzie nadal występował, zatrzymaj ją lub usunąć hello Storm w klastrze usługi HDInsight. toostop hello topologii, wykonaj następujące kroki hello:

1. W programie Visual Studio wróć toohello topologii Podgląd i wybierz hello topologii.

2. Wybierz hello **Kill** przycisk toostop hello topologii.

    ![Kasowanie przycisk w topologii hello podsumowania](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

W tym dokumencie przedstawiono sposób toosend danych z tooSQL topologii Storm bazy danych, następnie wizualizacji danych hello przy użyciu usługi Power BI. Aby uzyskać informacje na temat toowork z innymi technologiami Azure za pomocą Storm w usłudze HDInsight, zobacz następujące dokumentu hello:

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)
