---
title: "aaaConfigure zasady Hive w usłudze HDInsight przyłączonych do domeny - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight (wersja zapoznawcza)
Dowiedz się, jak zasady zakres Apache tooconfigure gałęzi. W tym artykule możesz utworzyć dwa hivesampletable toohello dostępu toorestrict zakres zasad. Hello hivesampletable jest dostarczany z klastrów usługi HDInsight. Po skonfigurowaniu zasad hello używasz programu Excel i ODBC tabel tooHive tooconnect sterowników w usłudze HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne
* Przyłączony do domeny klaster usługi HDInsight. Zobacz [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).
* Stacja robocza z pakietem Office 2016, pakietem Office 2013 Professional Plus, usługą Office 365 Pro Plus, programem Excel 2013 Standalone lub pakietem Office 2010 Professional Plus.

## <a name="connect-tooapache-ranger-admin-ui"></a>Połącz tooApache interfejsu użytkownika administratora zakres
**tooRanger tooconnect interfejsu użytkownika administratora**

1. Z poziomu przeglądarki Połącz tooRanger interfejsu użytkownika Administrator. adres URL Hello jest https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Poświadczenia używane na platformie Ranger są inne niż w klastrze usługi Hadoop. przeglądarki tooprevent przy użyciu buforowanych poświadczeń Hadoop, używają nowego inprivate przeglądarki okna tooconnect toohello interfejsu użytkownika administratora zakres.
   >
   >
2. Zaloguj się przy użyciu nazwy użytkownika hello klastra administrator domeny i hasła:

    ![Strona główna platformy Ranger z przyłączonym do domeny klastrem usługi HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Obecnie platforma Ranger współpracuje tylko z usługami Yarn i Hive.

## <a name="create-domain-users"></a>Tworzenie użytkowników domeny
W temacie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight) utworzono użytkowników hiveuser1 i hiveuser2. W tym samouczku użyjesz hello dwa konta.

## <a name="create-ranger-policies"></a>Tworzenie zasad platformy Ranger
W tej sekcji utworzysz dwie zasady platformy Ranger umożliwiające uzyskiwanie dostępu do tabeli hivesampletable. Możesz przydzielić uprawnienie select (wybór) do innego zestawu kolumn. Obydwaj użytkownicy zostali utworzeni przy użyciu instrukcji podanych w temacie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).  W następnej sekcji hello przetestuje Witaj dwie zasady w programie Excel.

**toocreate zakres zasad**

1. Otwórz interfejs użytkownika administratora platformy Ranger. Zobacz [połączyć tooApache interfejsu użytkownika administratora zakres](#connect-to-apache-ranager-admin-ui).
2. Kliknij pozycję **&lt;nazwa_klastra>_hive** w obszarze **Hive**. Zostaną wyświetlone dwie wstępnie skonfigurowane zasady.
3. Kliknij przycisk **Dodaj nowe zasady**, a następnie wprowadź hello następujące wartości:

   * Policy Name (Nazwa zasad): read-hivesampletable-all
   * Hive Database (Baza danych Hive): default
   * table (tabela): hivesampletable
   * Hive Column (Kolumna usługi Hive): *
   * Select User (Wybierz użytkownika): hiveuser1
   * Permissions (Uprawnienia): select

     ![Konfigurowanie zasad usługi Hive na platformie Ranger z przyłączonym do domeny klastrem usługi HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Jeśli użytkownik domeny nie jest wypełnione wybierz użytkownika, poczekaj kilka chwil toosync zakres przy użyciu usługi AAD.
     >
     >
4. Kliknij przycisk **Dodaj** toosave hello zasad.
5. Powtórz toocreate ostatnie dwa kroki hello inne zasady z hello następujące właściwości:

   * Policy Name (Nazwa zasad): read-hivesampletable-devicemake
   * Hive Database (Baza danych Hive): default
   * table (tabela): hivesampletable
   * Hive Column (Kolumna usługi Hive): clientid, devicemake
   * Select User (Wybierz użytkownika): hiveuser2
   * Permissions (Uprawnienia): select

## <a name="create-hive-odbc-data-source"></a>Tworzenie źródła danych ODBC usługi Hive
Witaj instrukcje można znaleźć w [źródła danych ODBC utwórz gałąź rejestru](hdinsight-connect-excel-hive-odbc-driver.md).  

    Właściwość|Opis
    ---|---
    Data Source Name (Nazwa źródła danych)|Nadaj nazwę źródła danych tooyour
    Host|Wprowadź ciąg &lt;nazwa_klastra_usługi_HDInsight>.azurehdinsight.net, np. myHDICluster.azurehdinsight.net.
    Port|Użyj portu <strong>443</strong>. (Ten port została zmieniona z 563 too443.)
    Database (Baza danych)|Użyj wartości <strong>Default</strong> (Domyślna).
    Hive Server Type (Typ serwera Hive)|Wybierz wartość <strong>Hive Server 2</strong>.
    Mechanism (Mechanizm)|Wybierz wartość <strong>Azure HDInsight Service</strong> (Usługa Azure HDInsight).
    HTTP Path (Ścieżka HTTP)|Pozostaw to pole puste.
    Nazwa użytkownika|Wprowadź hiveuser1@contoso158.onmicrosoft.com. Zaktualizuj hello nazwy domeny, jeśli jest inny.
    Hasło|Wprowadź hasło hello hiveuser1.
    </table>

Upewnij się, że tooclick **testu** przed zapisaniem hello źródła danych.

## <a name="import-data-into-excel-from-hdinsight"></a>Importowanie danych do programu Excel z usługi HDInsight
W ostatniej sekcji hello zostały skonfigurowane dwie zasady.  hiveuser1 ma hello wybierz uprawnienia dla wszystkich kolumn hello, a hiveuser2 ma hello wybierz uprawnienie na dwóch kolumn. W tej sekcji można personifikować hello dwóch użytkowników tooimport danych do programu Excel.

1. Otwórz nowy lub istniejący skoroszyt w programie Excel.
2. Z hello **danych** , kliknij pozycję **z innych źródeł danych**, a następnie kliknij przycisk **Kreator połączenia danych z** toolaunch hello **Kreator połączenia danych**.

    ![Otwieranie Kreatora połączenia danych][img-hdi-simbahiveodbc.excel.dataconnection]
3. Wybierz **ODBC DSN** hello źródła danych, a następnie kliknij przycisk **dalej**.
4. Ze źródeł danych ODBC, nazwy utworzonego w poprzednim kroku hello źródła danych wybierz hello, a następnie kliknij **dalej**.
5. Wprowadź ponownie hasło hello klastra powitania w Kreatorze hello, a następnie kliknij przycisk **OK**. Poczekaj, aż hello **wybierz bazę danych i tabeli** tooopen okna dialogowego. Może to potrwać kilka sekund.
6. Wybierz pozycję **hivesampletable**, a następnie kliknij przycisk **Dalej**.
7. Kliknij przycisk **Zakończ**.
8. W hello **i zaimportuj dane** okna dialogowego, można zmienić lub określić hello zapytanie. tak, kliknij przycisk toodo **właściwości**. Może to potrwać kilka sekund.
9. Kliknij przycisk hello **definicji** tekst polecenia kartę hello jest:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Przy użyciu zasad zakres hello zdefiniowane przez użytkownika hiveuser1 ma uprawnienia select dla wszystkich kolumn hello.  To zapytanie działa z poświadczeniami użytkownika hiveuser1, ale nie z poświadczeniami użytkownika hiveuser2.

   ![Właściwości połączenia][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Kliknij przycisk **OK** tooclose hello właściwości połączenia w oknie dialogowym.
11. Kliknij przycisk **OK** tooclose hello **i zaimportuj dane** okna dialogowego.  
12. Wprowadź ponownie hasło hello hiveuser1, a następnie kliknij przycisk **OK**. Trwa kilka sekund przed importowanych tooExcel pobiera dane. Po zakończeniu zobaczysz 11 kolumn danych.

drugie zasady hello tootest (odczyt hivesampletable-devicemake) utworzonego w ostatniej sekcji hello

1. Dodaj nowy arkusz w programie Excel.
2. Wykonaj hello ostatnio procedury tooimport hello dane.  zostaną wprowadzone zmiany Hello tylko jest poświadczeń toouse hiveuser2 zamiast hiveuser1 firmy. To zakończy się niepowodzeniem, ponieważ hiveuser2 ma tylko uprawnienia toosee dwie kolumny. Stosuje uzyskać hello następujący błąd:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Wykonaj hello same procedury tooimport danych. Teraz, Użyj poświadczeń w hiveuser2 oraz modyfikowania hello instrukcji select z:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    na:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Po zakończeniu zobaczysz dwie kolumny zaimportowanych danych.

## <a name="next-steps"></a>Następne kroki
* Aby skonfigurować przyłączony do domeny klaster usługi HDInsight, zobacz [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).
* Aby zarządzać przyłączonymi do domeny klastrami usługi HDInsight, zobacz [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Zarządzanie przyłączonymi do domeny klastrami usługi HDInsight).
* Do uruchamiania zapytań Hive przy użyciu protokołu SSH w klastrach HDInsight przyłączonych do domeny, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Do łączenia Hive za pomocą Hive JDBC, zobacz [połączyć tooHive w usłudze Azure HDInsight przy użyciu sterownik Hive JDBC hello](hdinsight-connect-hive-jdbc-driver.md)
* Do łączenia tooHadoop programu Excel za pomocą ODBC programu Hive, zobacz [tooHadoop łączenie programu Excel z hello dysku Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)
* Do łączenia programu Excel tooHadoop za pomocą dodatku Power Query, zobacz [tooHadoop łączenie programu Excel za pomocą dodatku Power Query](hdinsight-connect-excel-power-query.md)
