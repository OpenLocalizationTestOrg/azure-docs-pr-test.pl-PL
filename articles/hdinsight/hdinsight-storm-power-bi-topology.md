---
title: "Apache Storm za pomocą usługi Power BI — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a>Wizualizuj dane z topologii Apache Storm przy użyciu usługi Power BI

Usługa Power BI pozwala wizualnie wyświetlanie danych w postaci raportów. Ten dokument zawiera przykładowy sposób użycia systemu Apache Storm w usłudze HDInsight można wygenerować danych do usługi Power BI.

> [!NOTE]
> Kroki opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio. Skompilowany projekt może zostać przesłane do klastra usługi HDInsight opartej na systemie Linux. Tylko opartych na systemie Linux klastrów utworzone po 10/28/2016 Obsługa SCP.NET topologii.
>
> Aby używać topologii C# z klastrem opartych na systemie Linux, należy zaktualizować pakiet Microsoft.SCP.Net.SDK NuGet używanych w projekcie do wersji 0.10.0.6 lub nowszej. Wersja pakietu musi być również zgodna z wersją główną systemu Storm zainstalowanego w usłudze HDInsight. Na przykład system Storm występujący w usłudze HDInsight w wersjach 3.3 i 3.4 jest w wersji 0.10.x, a usługa HDInsight 3.5 używa systemu Storm 1.0.x.
>
> Topologie C# w klastrach opartych na systemie Linux muszą korzystać z platformy .NET 4.5 i używać platformy Mono, aby mogły działać w klastrze usługi HDInsight. Większość elementów pracy. Należy jednak sprawdzić [zgodności Mono](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.
>
> Wersja języka Java tego projektu, który współpracuje z usługą HDInsight opartą na systemie Linux lub z systemem Windows, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Użytkownik usługi Azure Active Directory z [usługi Power BI](https://powerbi.com) dostępu.
* Klaster usługi HDInsight. Aby uzyskać więcej informacji, zobacz [wprowadzenie Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Visual Studio (jedna z następujących wersji)

  * Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Program Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (dowolna wersja)

* Narzędzia HDInsight Tools for Visual Studio: zobacz [rozpocząć korzystanie z narzędzia HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) uzyskać informacji o informacje dotyczące instalacji.

## <a name="how-it-works"></a>Jak to działa

Ten przykład zawiera topologii Storm C# losowo generowany danych dziennika usług Internet Information Services (IIS). Następnie napisano te dane do bazy danych SQL i tam jest używany do generowania raportów w usłudze Power BI.

Następujące pliki wdrożenia główne funkcje w tym przykładzie:

* **SqlAzureBolt.cs**: zapisuje informacje wygenerowane w topologii Storm do bazy danych SQL.
* **IISLogsTable.sql**: instrukcji języka Transact-SQL używanego do generowania danych przechowywanych w bazie danych.

> [!WARNING]
> Tworzenie tabeli w bazie danych SQL, przed rozpoczęciem topologii w klastrze usługi HDInsight.

## <a name="download-the-example"></a>Pobierz przykład

Pobierz [przykład HDInsight C# Storm usługi Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). Aby go pobrać, albo rozwidlenia/klonowania za pomocą [git](http://git-scm.com/), lub użyj **Pobierz** łącze, aby pobrać .zip archiwum.

## <a name="create-a-database"></a>Tworzenie bazy danych

1. Aby utworzyć bazę danych, wykonaj czynności w [samouczek usługi SQL Database](../sql-database/sql-database-get-started.md) dokumentu.

2. Połącz z bazą danych, wykonując kroki opisane w [nawiązywanie połączenia z bazą danych SQL z programem Visual Studio](../sql-database/sql-database-connect-query.md) dokumentu.

3. W Eksploratorze obiektów kliknij prawym przyciskiem myszy bazę danych, a następnie wybierz **nowe zapytanie**. Wklej zawartość **IISLogsTable.sql** plik dołączony do projektu pobrany do okna zapytania, a następnie użyć Ctrl + Shift + E do wykonania zapytania. Powinien zostać wyświetlony komunikat pomyślnie ukończyć polecenia.

## <a name="configure-the-sample"></a>Konfigurowanie przykładowej

1. Z [portalu Azure](https://portal.azure.com), wybierz bazę danych SQL. Z **Essentials** części bloku bazy danych SQL, wybierz opcję **Pokaż parametry połączenia bazy danych**. Na liście Skopiuj **ADO.NET (uwierzytelnianie SQL)** informacji.

2. Otwórz próbki w programie Visual Studio. Z **Eksploratora rozwiązań**, otwórz **App.config** pliku, a następnie znajdź następujący wpis:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Zastąp **TOBEFILLED ##** wartości z ciągu połączenia bazy danych skopiowany w poprzednim kroku. Zastąp **{Twojej\_username}** i **{Twojej\_hasło}** przy użyciu nazwy użytkownika i hasła dla bazy danych.

3. Zapisz i zamknij plik.

## <a name="deploy-the-sample"></a>Wdrażanie przykładowej

1. Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **StormToSQL** projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**. Wybierz klaster usługi HDInsight z **klaster Storm** okna dialogowego z listy rozwijanej.

   > [!NOTE]
   > Może potrwać kilka sekund **klaster Storm** listy rozwijanej, aby umieścić nazwy serwera.
   >
   > Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się za jedną, która zawiera Storm w klastrze usługi HDInsight.

2. Po przesłaniu topologii __podglądu topologii__ pojawi się. Aby wyświetlić tej topologii, wybierz wpis SqlAzureWriterTopology z listy.

    ![Topologie, w przypadku topologii wybrane](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Użyj tego widoku, aby wyświetlić informacje o topologii lub kliknij dwukrotnie wpis (na przykład SqlAzureBolt), aby wyświetlić informacje dotyczące składnika w topologii.

3. Po topologii był uruchamiany przez kilka minut, wróć do okna zapytania SQL używanego do utworzenia bazy danych. Zastąp istniejące instrukcje następujące zapytanie:

        select * from iislogs;

    Użyj klawiszy Ctrl + Shift + E można wykonać zapytania, a powinien zostać wyświetlony wyniki podobne do następujących danych:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Te dane został zapisany od topologii Storm.

## <a name="create-a-report"></a>Tworzenie raportu

1. Połączyć się z [łącznika usługi Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) dla usługi Power BI. 

2. W ramach **baz danych**, wybierz pozycję **uzyskać**.

3. Wybierz **bazy danych SQL Azure**, a następnie wybierz **Connect**.

    > [!NOTE]
    > Może wystąpić konieczność pobrania Power BI Desktop, aby kontynuować. Jeśli tak, wykonaj następujące kroki, aby połączyć:
    >
    > 1. Otwórz Power BI Desktop i wybierz __Pobierz dane__.
    > Wybierz 2 __Azure__, a następnie __bazy danych Azure SQL__.

4. Wprowadź informacje do połączenia z bazą danych SQL Azure. Te informacje można znaleźć, odwiedzając [portalu Azure](https://portal.azure.com) i wybrać bazę danych SQL.

   > [!NOTE]
   > Należy również określić interwał odświeżania i filtry niestandardowe przy użyciu **włączyć zaawansowane opcje** z okna dialogowego połączenia.

5. Po nawiązaniu połączenia, pojawi się nowy zestaw danych o takiej samej nazwie jako bazy danych, z którym połączenie. Wybierz zestaw danych, aby rozpocząć projektowanie raportu.

6. Z **pola**, rozwiń węzeł **IISLOGS** wpisu. Aby utworzyć raport zawierający listę łodyg identyfikatora URI, zaznacz pole wyboru **URISTEM**.

    ![Tworzenie raportu](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Następnie przeciągnij **metody** do raportu. Aktualizacje raport listy łodyg i odpowiedniej metody HTTP użytej dla żądania HTTP.

    ![Dodawanie danych — metoda](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Z **wizualizacje** wybierz opcję **pola** ikony, a następnie wybierz strzałkę w dół obok pozycji **— metoda** w **wartości** sekcji. Aby wyświetlić liczbę razy ile dostęp do identyfikatora URI, zaznacz **liczba**.

    ![Zmiana liczby metod](./media/hdinsight-storm-power-bi-topology/count.png)

9. Następnie wybierz pozycję **skumulowany wykres kolumnowy** Aby zmienić sposób wyświetlania informacji.

    ![Zmiana na wykresach skumulowanych](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. Aby zapisać raport, wybierz **zapisać** i wprowadź nazwę dla raportu.

## <a name="stop-the-topology"></a>Zatrzymywanie topologii

Topologia jest nadal uruchomiona do momentu Zatrzymaj ją lub usunąć Storm w klastrze usługi HDInsight. Aby zatrzymać topologii, wykonaj następujące czynności:

1. W programie Visual Studio wróć do podglądu topologii i wybierz topologii.

2. Wybierz **Kill** przycisk, aby zatrzymać topologii.

    ![Kasowanie przycisk w topologii podsumowania](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

W tym dokumencie przedstawiono sposób wysyłania danych z topologii Storm do bazy danych SQL, a następnie wizualizacji danych przy użyciu usługi Power BI. Aby uzyskać informacje na temat pracy z innymi technologiami Azure za pomocą Storm w usłudze HDInsight zobacz następujący dokument:

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)
