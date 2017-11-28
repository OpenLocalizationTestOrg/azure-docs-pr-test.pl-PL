---
title: "aaaQuery Hive za pośrednictwem sterownik JDBC hello - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj sterownik JDBC hello z tooHadoop zapytań Hive toosubmit Java aplikacji w usłudze HDInsight. Połącz programowo i z powitania klienta SQuirrel SQL."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="4e230-104">Zapytanie Hive za pośrednictwem sterownik JDBC hello w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="4e230-105">Dowiedz się, jak sterownik JDBC hello toouse z toosubmit aplikacji Java Hive odpytuje tooHadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="4e230-106">Witaj informacje w tym dokumencie przedstawiono sposób tooconnect programowo i z hello SQuirrel klienta SQL.</span><span class="sxs-lookup"><span data-stu-id="4e230-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="4e230-107">Aby uzyskać więcej informacji na powitania interfejsu JDBC Hive, zobacz [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="4e230-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e230-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4e230-108">Prerequisites</span></span>

* <span data-ttu-id="4e230-109">Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="4e230-110">Praca klastrach opartych na systemie Linux albo systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="4e230-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4e230-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4e230-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4e230-112">Aby uzyskać więcej informacji, zobacz [wycofanie HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4e230-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4e230-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="4e230-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="4e230-114">SQuirreL jest aplikacją kliencką JDBC.</span><span class="sxs-lookup"><span data-stu-id="4e230-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="4e230-115">Witaj [Java Developer Kit (JDK) w wersji 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4e230-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="4e230-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="4e230-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="4e230-117">Maven jest projektem systemu dla projektów języka Java, używanego przez projekt hello skojarzone z tym artykułem kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4e230-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="4e230-118">Parametry połączenia sterownika JDBC</span><span class="sxs-lookup"><span data-stu-id="4e230-118">JDBC connection string</span></span>

<span data-ttu-id="4e230-119">Klaster usługi HDInsight tooan JDBC połączeń na platformie Azure są wprowadzane ponad 443, a ruch hello jest zabezpieczone przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="4e230-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="4e230-120">Hello publicznego bramy, która klastrów hello sit za przekierowuje hello ruchu toohello portu nasłuchiwania serwera HiveServer2 faktycznie na.</span><span class="sxs-lookup"><span data-stu-id="4e230-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="4e230-121">Witaj poniżej znajduje się przykład parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="4e230-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="4e230-122">Zastąp `CLUSTERNAME` o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="4e230-123">Authentication</span><span class="sxs-lookup"><span data-stu-id="4e230-123">Authentication</span></span>

<span data-ttu-id="4e230-124">Podczas ustanawiania połączenia hello, musisz użyć hello HDInsight klastra Administrator nazwy i hasła tooauthenticate toohello klastra bramy.</span><span class="sxs-lookup"><span data-stu-id="4e230-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="4e230-125">Podczas nawiązywania połączenia z klientami JDBC, takich jak SQuirreL SQL, wprowadź hello admin nazwy i hasła w ustawieniach klienta.</span><span class="sxs-lookup"><span data-stu-id="4e230-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="4e230-126">Z poziomu aplikacji Java musi używać hello nazwy i hasła podczas ustanawiania połączenia.</span><span class="sxs-lookup"><span data-stu-id="4e230-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="4e230-127">Na przykład hello następujący kod w języku Java otwiera nowe połączenie przy użyciu parametrów połączenia hello, nazwę administratora i hasła:</span><span class="sxs-lookup"><span data-stu-id="4e230-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="4e230-128">Połączenie z klientem SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="4e230-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="4e230-129">SQuirreL SQL jest klientem JDBC, które mogą być używane tooremotely uruchamiania zapytań Hive z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="4e230-130">Witaj następujących krokach założono zainstalowano SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="4e230-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="4e230-131">Skopiuj hello Hive JDBC sterowniki z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="4e230-132">Dla **HDInsight opartych na systemie Linux**, użyj następujących hello kroki pliki jar hello wymagane toodownload.</span><span class="sxs-lookup"><span data-stu-id="4e230-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="4e230-133">Utwórz katalog zawierający pliki hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="4e230-134">Na przykład `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="4e230-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="4e230-135">Z wiersza polecenia użyj następujących hello polecenia toocopy hello plików z klastrem usługi HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="4e230-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="4e230-136">Zastąp `USERNAME` z nazwą konta użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4e230-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="4e230-137">Zastąp `CLUSTERNAME` o nazwie klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="4e230-138">Dla **HDInsight opartych na systemie Windows**, użyj następujących hello kroki pliki jar hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="4e230-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="4e230-139">Z hello portalu Azure, wybierz z klastrem usługi HDInsight, a następnie wybierz hello **pulpitu zdalnego** ikony.</span><span class="sxs-lookup"><span data-stu-id="4e230-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Ikony pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="4e230-141">W bloku hello pulpitu zdalnego za pomocą hello **Connect** przycisk tooconnect toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="4e230-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="4e230-142">Jeśli hello pulpitu zdalnego nie jest włączona, użyj hello formularza tooprovide nazwę użytkownika i hasło, a następnie wybierz **włączyć** tooenable pulpitu zdalnego dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Blok pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="4e230-144">Po wybraniu **Connect**, zostanie pobrany plik RDP.</span><span class="sxs-lookup"><span data-stu-id="4e230-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="4e230-145">Korzystając z tego pliku toolaunch hello pulpitu zdalnego klienta.</span><span class="sxs-lookup"><span data-stu-id="4e230-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="4e230-146">Po wyświetleniu monitu użyj hello nazwę użytkownika i hasło dostępu do pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4e230-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="4e230-147">Po nawiązaniu połączenia, skopiuj następujące pliki z komputera lokalnego tooyour sesji pulpitu zdalnego hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="4e230-148">Umieść je w lokalnym katalogu o nazwie `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="4e230-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="4e230-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-Standalone.JAR</span><span class="sxs-lookup"><span data-stu-id="4e230-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="4e230-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="4e230-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="4e230-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="4e230-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="4e230-152">Witaj w wersji numery objęte hello ścieżki i nazwy plików mogą być inne dla klastra.</span><span class="sxs-lookup"><span data-stu-id="4e230-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="4e230-153">Rozłączenie sesji pulpitu zdalnego powitania po zakończeniu kopiowania plików hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="4e230-154">Uruchom aplikację SQuirreL SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="4e230-155">Od lewej hello hello okna, wybierz **sterowniki**.</span><span class="sxs-lookup"><span data-stu-id="4e230-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Sterowniki karty po lewej stronie powitania hello okna](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="4e230-157">Z ikon hello u góry hello hello **sterowniki** okno dialogowe, wybierz opcję hello  **+**  toocreate ikona sterownika.</span><span class="sxs-lookup"><span data-stu-id="4e230-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Ikony sterowniki](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="4e230-159">W oknie dialogowym Dodawanie sterownika hello Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="4e230-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="4e230-160">**Nazwa**: Hive</span><span class="sxs-lookup"><span data-stu-id="4e230-160">**Name**: Hive</span></span>
    * <span data-ttu-id="4e230-161">**Przykładowy adres URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="4e230-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="4e230-162">**Dodatkowe ścieżki klasy**: Użyj hello Dodaj przycisk tooadd hello jar pliki pobrane wcześniej</span><span class="sxs-lookup"><span data-stu-id="4e230-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="4e230-163">**Nazwa klasy**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="4e230-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![Dodaj sterownik okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="4e230-165">Kliknij przycisk **OK** toosave te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="4e230-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="4e230-166">Powitania po lewej stronie okna SQuirreL SQL hello wybierz **aliasy**.</span><span class="sxs-lookup"><span data-stu-id="4e230-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="4e230-167">Następnie kliknij przycisk hello  **+**  toocreate ikona alias połączenia.</span><span class="sxs-lookup"><span data-stu-id="4e230-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![Dodaj nowy alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="4e230-169">Użyj następujących hello wartości hello **Dodaj Alias** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e230-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="4e230-170">**Nazwa**: Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="4e230-171">**Sterownik**: Użyj hello listy rozwijanej tooselect hello **Hive** sterownika</span><span class="sxs-lookup"><span data-stu-id="4e230-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="4e230-172">**Adres URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="4e230-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="4e230-173">Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="4e230-174">**Nazwa użytkownika**: Nazwa konta logowania hello klastra dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="4e230-175">Domyślnie Hello `admin`.</span><span class="sxs-lookup"><span data-stu-id="4e230-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="4e230-176">**Hasło**: hello hasła konta logowania hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4e230-176">**Password**: hello password for hello cluster login account.</span></span>

 ![Dodaj alias okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="4e230-178">Użyj hello **testu** tooverify przycisku, który hello połączenie działa.</span><span class="sxs-lookup"><span data-stu-id="4e230-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="4e230-179">Gdy **nawiązać: Hive w usłudze HDInsight** zostanie wyświetlone okno dialogowe, wybierz **Connect** tooperform hello testu.</span><span class="sxs-lookup"><span data-stu-id="4e230-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="4e230-180">Jeśli hello test zakończy się pomyślnie, zostanie wyświetlony **połączenie przebiegło pomyślnie** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e230-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="4e230-181">połączenie hello toosave alias, użyj hello **Ok** u dołu hello hello **Dodaj Alias** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4e230-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="4e230-182">Z hello **nawiązać** wybierz z listy rozwijanej na górze hello SQuirreL SQL **Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4e230-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="4e230-183">Po wyświetleniu monitu wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="4e230-183">When prompted, select **Connect**.</span></span>

    ![w oknie dialogowym połączenia](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="4e230-185">Po nawiązaniu połączenia, wprowadź hello następujące zapytanie do okna dialogowego zapytania SQL hello, a następnie wybierz hello **Uruchom** ikony.</span><span class="sxs-lookup"><span data-stu-id="4e230-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="4e230-186">obszar wyników Hello powinny być wyświetlane hello wyniki zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![okno dialogowe kwerendy SQL, łącznie z wynikami](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="4e230-188">Połącz się z przykładem aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="4e230-188">Connect from an example Java application</span></span>

<span data-ttu-id="4e230-189">Przykład użycia tooquery klienta Java Hive w usłudze HDInsight jest dostępna w [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="4e230-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="4e230-190">Wykonaj te instrukcje hello hello toobuild repozytorium, a następnie uruchom przykładowe hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4e230-191">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="4e230-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="4e230-192">Wystąpił nieoczekiwany błąd podczas próby tooopen połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="4e230-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="4e230-193">**Objawy**: podczas łączenia z klastrem usługi HDInsight tooan, który jest w wersji 3.3 lub 3.4, może zostać wyświetlony błąd, który wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="4e230-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="4e230-194">Witaj śladu stosu dla tego błędu rozpoczyna się od hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="4e230-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="4e230-195">**Przyczyna**: niezgodność wersji hello pliku commons codec.jar hello używanego przez SQuirreL i hello wymagana przez składniki Hive JDBC hello przyczyną tego błędu.</span><span class="sxs-lookup"><span data-stu-id="4e230-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="4e230-196">**Rozdzielczość**: toofix tego błędu, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4e230-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="4e230-197">Pobierz plik jar koder-dekoder commons hello z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="4e230-198">Zakończ SQuirreL, a następnie przejdź katalogu toohello zainstalowanym SQuirreL w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="4e230-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="4e230-199">W katalogu SquirreL hello, hello `lib` katalogu, Zastąp hello istniejących na commons codec.jar z jedną pobrane z klastrem usługi HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e230-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="4e230-200">Uruchom ponownie SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="4e230-200">Restart SQuirreL.</span></span> <span data-ttu-id="4e230-201">Błąd Hello już powinien wystąpić, gdy połączenie tooHive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e230-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e230-202">Next steps</span></span>

<span data-ttu-id="4e230-203">Teraz, kiedy znasz już jak toowork JDBC toouse przy użyciu Hive, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e230-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="4e230-204">Przekazywanie danych tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="4e230-205">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4e230-206">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4e230-207">Korzystanie z zadań MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e230-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
