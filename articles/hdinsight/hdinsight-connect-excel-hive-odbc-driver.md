---
title: aaaConnect tooHadoop programu Excel z hello Hive ODBC Driver - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się i użyj hello sterownik Microsoft Hive ODBC dla programu Excel tooquery danych w klastrach HDInsight z programu Microsoft Excel."
keywords: hadoop w programie excel, hive w programie excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Uzyskuj dostęp sterownik Microsoft Hive ODBC hello tooHadoop programu Excel w usłudze Azure HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Rozwiązania danych Big Data firmy Microsoft składniki Microsoft Business Intelligence (BI) jest zintegrowany z klastrów platformy Apache Hadoop, które zostały wdrożone przez hello Azure HDInsight. Przykładem takiej integracji to hello możliwości tooconnect Excel toohello Hive magazyn danych klastra usługi Hadoop w HDInsight przy użyciu hello sterownika Microsoft Hive bazy danych połączenia ODBC (Open).

Jest również możliwe tooconnect hello danych skojarzonych z klastra usługi HDInsight i innych źródeł danych, łącznie z innymi (z systemem innym niż — usługi HDInsight) klastrów Hadoop, w programie Excel przy użyciu hello dodatku Microsoft Power Query dla programu Excel. Aby uzyskać informacje na temat instalowania i za pomocą dodatku Power Query, zobacz [tooHDInsight łączenie programu Excel z dodatku Power Query][hdinsight-power-query].

> [!NOTE]
> Gdy hello kroki opisane w temacie w tym artykule może być używany z albo Linux lub klastra usługi HDInsight opartej na systemie Windows, Windows jest wymagany dla stacji roboczej powitania klienta.
> 
> 

**Wymagania wstępne**:

Przed rozpoczęciem tego artykułu, musi mieć hello następujące elementy:

* **Klaster usługi HDInsight**. Zobacz toocreate, [Rozpoczynanie pracy z usługą Azure HDInsight][hdinsight-get-started].
* **Stacja robocza** z pakietu Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 autonomicznej lub Office 2010 Professional Plus.

## <a name="install-microsoft-hive-odbc-driver"></a>Zainstalować sterownik Microsoft Hive ODBC
Pobierz i zainstaluj sterownik Microsoft Hive ODBC z hello [Centrum pobierania][hive-odbc-driver-download].

W 32-bitowy lub 64-bitowych wersjach systemu Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 i Windows Server 2012 można zainstalować ten sterownik. Sterownik Hello umożliwia połączenia tooAzure HDInsight (w wersji 1.6 lub nowszy) i emulatora usługi Azure HDInsight (v.1.0.0.0 i nowsze). Stosuje zainstalować hello wersja jest taka sama wersja hello aplikacji hello których sterownika ODBC hello jest używany. W tym samouczku sterownik hello jest używany z Office Excel.

## <a name="create-hive-odbc-data-source"></a>Tworzenie źródła danych ODBC usługi Hive
Witaj poniższej procedurze pokazano, jak toocreate Hive źródła danych ODBC.

1. Z systemu Windows 8 lub Windows 10, naciśnij klawisz ekranu startowego hello klucza tooopen Windows hello, a następnie wpisz **źródeł danych**.
2. Kliknij przycisk **skonfigurować źródła danych ODBC (32-bitowy)** lub **Konfigurowanie źródeł danych ODBC (64-bitowy)** w zależności od używanej wersji pakietu Office. Jeśli korzystasz z systemu Windows 7, wybierz **źródła danych ODBC (32 bity)** lub **źródła danych ODBC (64 bity)** z **narzędzia administracyjne**. Zostanie wyświetlona hello **Administrator źródła danych ODBC** okna dialogowego.
   
    ![Administrator źródeł danych OBDC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "skonfigurować DSN przy użyciu Administrator źródła danych ODBC")

3. Przy użyciu serwera DNS użytkownika, kliknij przycisk **Dodaj** tooopen hello **Utwórz nowe źródło danych** kreatora.
4. Wybierz **sterownik Microsoft Hive ODBC**, a następnie kliknij przycisk **Zakończ**. Zostanie wyświetlona hello **Instalator programu Microsoft Hive ODBC sterownika DNS** okna dialogowego.
5. Wpisz lub wybierz hello następujące wartości:
   
   | Właściwość | Opis |
   | --- | --- |
   |  Data Source Name (Nazwa źródła danych) |Nadaj nazwę źródła danych tooyour |
   |  Host |Wprowadź ciąg &lt;nazwa_klastra_usługi_HDInsight>.azurehdinsight.net, np. myHDICluster.azurehdinsight.net. |
   |  Port |Użyj portu <strong>443</strong>. (Ten port została zmieniona z 563 too443.) |
   |  Database (Baza danych) |Użyj wartości <strong>Default</strong> (Domyślna). |
   |  Mechanism (Mechanizm) |Wybierz wartość <strong>Azure HDInsight Service</strong> (Usługa Azure HDInsight). |
   |  Nazwa użytkownika |Wprowadź username użytkownika HTTP klastra usługi HDInsight. Witaj domyślna nazwa użytkownika to <strong>admin</strong>. |
   |  Hasło |Wprowadź hasło użytkownika klastra usługi HDInsight. |
   
    </table>
   
    Niektóre toobe ważne parametry są świadome po kliknięciu **zaawansowane opcje**:
   
   | Parametr | Opis |
   | --- | --- |
   |  Użyj natywnego zapytania |Gdy jest wybrana, hello sterownik ODBC nie spróbuj tooconvert TSQL do HiveQL. Są go używać tylko wtedy, gdy 100% się, że przesyłasz czysty instrukcje HiveQL. Podczas nawiązywania połączenia tooSQL serwera lub bazy danych SQL Azure, należy pozostawić niezaznaczone. |
   |  Pobranych na blok wierszy |Podczas pobierania dużej liczby rekordów, dostrajanie ten parametr może być wymagane tooensure optymalnej wydajności. |
   |  Domyślna długość kolumny ciąg, długość kolumny binarnej, skala kolumny dziesiętnej |Typ danych Hello długości i opisie może mieć wpływ na sposób dane są zwracane. Spowodują one toobe nieprawidłowe informacje zwrócone z powodu tooloss dokładność i/lub obcięcie. |

    ![Zaawansowane opcje](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN zaawansowane opcje konfiguracji")

1. Kliknij przycisk **testu** źródła danych hello tootest. Gdy hello źródło danych jest skonfigurowane poprawnie, pokazuje *testy ZAKOŃCZYŁO się pomyślnie!*.
2. Kliknij przycisk **OK** tooclose hello testu w oknie dialogowym. Witaj nowego źródła danych są wymienione na powitania **Administrator źródła danych ODBC**.
3. Kliknij przycisk **OK** tooexit hello kreatora.

## <a name="import-data-into-excel-from-hdinsight"></a>Importowanie danych do programu Excel z usługi HDInsight
Witaj poniższych krokach opisano hello sposób tooimport danych z tabeli programu Hive w skoroszycie programu Excel za pomocą hello źródła danych ODBC, który został utworzony w poprzedniej sekcji hello.

1. Otwórz nowy lub istniejący skoroszyt w programie Excel.
2. Z hello **danych** , kliknij pozycję **Pobierz dane**, kliknij przycisk **z innych źródeł**, a następnie kliknij przycisk **z ODBC** toolaunch hello  **Kreator połączenia danych**.
   
    ![Kreator połączenia danych otwartych](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Kreator połączenia danych otwartych")
4. Wybierz hello danych nazwy utworzonego w ostatniej sekcji hello źródła, a następnie kliknij **OK**.
5. Wprowadź nazwę użytkownika Hadoop (hello domyślną nazwą jest admin) i hello hasło, a następnie kliknij przycisk **Connect**.
6. W Nawigatorze, rozwiń węzeł **HIVE**, rozwiń węzeł **domyślne**, kliknij przycisk **hivesampletable**, a następnie kliknij przycisk **obciążenia**. Trwa kilka sekund przed importowanych tooExcel pobiera dane.

    ![Nawigator ODBC programu Hive HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Kreator połączenia danych otwartych")


## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób toouse hello danych tooretrieve sterownik Microsoft Hive ODBC z hello usługi HDInsight do programu Excel. Podobnie można pobrać danych z hello usługi HDInsight do bazy danych SQL. Możliwe jest również możliwe tooupload danych do usługi HDInsight. toolearn więcej, zobacz:

* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


