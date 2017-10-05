---
title: "Zapytanie Hive za pośrednictwem sterownik JDBC - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Sterownik JDBC z aplikacji Java umożliwia wysyłanie zapytań programu Hive do platformy Hadoop w usłudze HDInsight. Połącz programowo i z klienta SQuirrel SQL."
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
ms.openlocfilehash: f2de58c2763b2ddd0926336164738929c477c4ae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="1bd7a-104">Zapytanie Hive za pośrednictwem sterownik JDBC w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="1bd7a-105">Dowiedz się, jak umożliwia wysyłanie zapytań programu Hive do platformy Hadoop w usłudze Azure HDInsight sterownik JDBC z aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="1bd7a-106">Informacje przedstawione w tym dokumencie pokazano, jak połączyć programowo i z klienta SQuirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="1bd7a-107">Aby uzyskać więcej informacji na interfejsie JDBC Hive, zobacz [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="1bd7a-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bd7a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1bd7a-108">Prerequisites</span></span>

* <span data-ttu-id="1bd7a-109">Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="1bd7a-110">Praca klastrach opartych na systemie Linux albo systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1bd7a-111">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1bd7a-112">Aby uzyskać więcej informacji, zobacz [wycofanie HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1bd7a-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1bd7a-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="1bd7a-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="1bd7a-114">SQuirreL jest aplikacją kliencką JDBC.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="1bd7a-115">[Java Developer Kit (JDK) w wersji 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-115">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="1bd7a-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="1bd7a-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="1bd7a-117">Maven jest projektem systemu dla projektów języka Java, używanego przez projekt skojarzony z tym artykułem kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-117">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="1bd7a-118">Parametry połączenia sterownika JDBC</span><span class="sxs-lookup"><span data-stu-id="1bd7a-118">JDBC connection string</span></span>

<span data-ttu-id="1bd7a-119">JDBC połączenia z klastrem usługi HDInsight na platformie Azure są nawiązywane ponad 443, a ruch jest zabezpieczony przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-119">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="1bd7a-120">Publiczny bramy, która klastrów sit za przekierowuje ruch do portu, który faktycznie nasłuchiwanie serwera HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-120">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="1bd7a-121">Poniżej przedstawiono przykład parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-121">The following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="1bd7a-122">Element `CLUSTERNAME` należy zastąpić nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-122">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="1bd7a-123">Authentication</span><span class="sxs-lookup"><span data-stu-id="1bd7a-123">Authentication</span></span>

<span data-ttu-id="1bd7a-124">Podczas ustanawiania połączenia, należy użyć nazwy administratora klastra usługi HDInsight i hasła do uwierzytelnienia klastra bramy.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-124">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="1bd7a-125">Podczas nawiązywania połączenia z klientami JDBC, takich jak SQuirreL SQL, wprowadź nazwę administratora i hasła w ustawieniach klienta.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="1bd7a-126">Z poziomu aplikacji Java należy użyć nazwy i hasła podczas nawiązywania połączenia.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-126">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="1bd7a-127">Na przykład następujący kod w języku Java otwiera nowe połączenie przy użyciu parametrów połączenia, nazwa administratora i hasła:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-127">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="1bd7a-128">Połączenie z klientem SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="1bd7a-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="1bd7a-129">SQuirreL SQL jest klienta JDBC, który umożliwia zdalne uruchamianie zapytań Hive z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-129">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="1bd7a-130">W następujących krokach założono zainstalowano SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-130">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="1bd7a-131">Skopiuj sterownik Hive JDBC z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-131">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="1bd7a-132">Aby uzyskać **HDInsight opartych na systemie Linux**, wykonaj następujące kroki, aby pobrać pliki jar wymagane.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-132">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="1bd7a-133">Utwórz katalog zawierający pliki.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-133">Create a directory that contains the files.</span></span> <span data-ttu-id="1bd7a-134">Na przykład `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="1bd7a-135">Z wiersza polecenia użyj następujących poleceń, aby skopiować pliki z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-135">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="1bd7a-136">Zastąp `USERNAME` o nazwie konta użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-136">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="1bd7a-137">Zastąp `CLUSTERNAME` z nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-137">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

    * <span data-ttu-id="1bd7a-138">Aby uzyskać **HDInsight opartych na systemie Windows**, wykonaj następujące kroki, aby pobrać pliki jar.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-138">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="1bd7a-139">W portalu Azure, wybierz z klastrem usługi HDInsight, a następnie wybierz **pulpitu zdalnego** ikony.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-139">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![Ikony pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="1bd7a-141">W bloku pulpitu zdalnego za pomocą **Connect** przycisk, aby połączyć się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-141">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="1bd7a-142">Jeśli nie włączono pulpitu zdalnego, użyj formularza, aby podać nazwę użytkownika i hasło, a następnie wybierz **włączyć** można włączyć pulpitu zdalnego dla klastra.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-142">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![Blok pulpitu zdalnego](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="1bd7a-144">Po wybraniu **Connect**, zostanie pobrany plik RDP.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="1bd7a-145">Aby uruchomić klienta usług pulpitu zdalnego, należy użyć tego pliku.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-145">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="1bd7a-146">Po wyświetleniu monitu użyj nazwy użytkownika i hasło dostępu do pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-146">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="1bd7a-147">Po nawiązaniu połączenia, skopiuj następujące pliki z sesji pulpitu zdalnego na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-147">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="1bd7a-148">Umieść je w lokalnym katalogu o nazwie `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="1bd7a-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-Standalone.JAR</span><span class="sxs-lookup"><span data-stu-id="1bd7a-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="1bd7a-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="1bd7a-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="1bd7a-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.JAR</span><span class="sxs-lookup"><span data-stu-id="1bd7a-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="1bd7a-152">Numery wersji dołączony do ścieżki i nazwy plików mogą być inne dla klastra.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-152">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="1bd7a-153">Rozłączenie sesji pulpitu zdalnego, po zakończeniu kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-153">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="1bd7a-154">Uruchom aplikację SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-154">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="1bd7a-155">Od lewej części okna wybierz **sterowniki**.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-155">From the left of the window, select **Drivers**.</span></span>

    ![Sterowniki karty po lewej stronie okna](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="1bd7a-157">Z ikony w górnej części **sterowniki** okno dialogowe, wybierz opcję  **+**  ikonę, aby utworzyć sterownika.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-157">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![Ikony sterowniki](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="1bd7a-159">W oknie dialogowym dodawania sterowników Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-159">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="1bd7a-160">**Nazwa**: Hive</span><span class="sxs-lookup"><span data-stu-id="1bd7a-160">**Name**: Hive</span></span>
    * <span data-ttu-id="1bd7a-161">**Przykładowy adres URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="1bd7a-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="1bd7a-162">**Dodatkowe ścieżki klasy**: Użyj przycisk Dodaj, aby dodać pliki jar pobrane wcześniej</span><span class="sxs-lookup"><span data-stu-id="1bd7a-162">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="1bd7a-163">**Nazwa klasy**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="1bd7a-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![Dodaj sterownik okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="1bd7a-165">Kliknij przycisk **OK** Aby zapisać te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-165">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="1bd7a-166">Po lewej stronie okna SQuirreL SQL, wybierz **aliasy**.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-166">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="1bd7a-167">Następnie kliknij przycisk  **+**  ikonę, aby utworzyć alias połączenia.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-167">Then click the **+** icon to create a connection alias.</span></span>

    ![Dodaj nowy alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="1bd7a-169">Użyj poniższych wartości **Dodaj Alias** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-169">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="1bd7a-170">**Nazwa**: Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="1bd7a-171">**Sterownik**: Użyj listy rozwijanej, aby wybrać **Hive** sterownika</span><span class="sxs-lookup"><span data-stu-id="1bd7a-171">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="1bd7a-172">**Adres URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="1bd7a-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="1bd7a-173">Zastąp **CLUSTERNAME** nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-173">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="1bd7a-174">**Nazwa użytkownika**: Nazwa konta logowania klastra dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-174">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="1bd7a-175">Wartość domyślna to `admin`.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-175">The default is `admin`.</span></span>

    * <span data-ttu-id="1bd7a-176">**Hasło**: hasło do konta logowania klastra.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-176">**Password**: The password for the cluster login account.</span></span>

 ![Dodaj alias okna dialogowego](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="1bd7a-178">Użyj **testu** przycisk, aby sprawdzić, czy połączenie działa.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-178">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="1bd7a-179">Gdy **nawiązać: Hive w usłudze HDInsight** zostanie wyświetlone okno dialogowe, wybierz **Connect** do wykonania testu.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="1bd7a-180">Jeśli test zakończy się powodzeniem, zobacz **połączenie przebiegło pomyślnie** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-180">If the test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="1bd7a-181">Aby zapisać alias połączenie, użyj **Ok** przycisk w dolnej części **Dodaj Alias** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-181">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

7. <span data-ttu-id="1bd7a-182">Z **nawiązać** wybierz z listy rozwijanej w górnej części SQuirreL SQL **Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-182">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="1bd7a-183">Po wyświetleniu monitu wybierz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-183">When prompted, select **Connect**.</span></span>

    ![w oknie dialogowym połączenia](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="1bd7a-185">Po nawiązaniu połączenia, wpisz poniższe zapytanie w oknie dialogowym zapytania SQL, a następnie wybierz **Uruchom** ikony.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-185">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="1bd7a-186">Wyniki zapytania powinien być wyświetlony w obszarze wyniki.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-186">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![okno dialogowe kwerendy SQL, łącznie z wynikami](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="1bd7a-188">Połącz się z przykładem aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="1bd7a-188">Connect from an example Java application</span></span>

<span data-ttu-id="1bd7a-189">Przykład użycia Java klientowi zapytania Hive w usłudze HDInsight jest dostępna w [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="1bd7a-189">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="1bd7a-190">Postępuj zgodnie z instrukcjami w repozytorium, aby skompilować i uruchomić próbki.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-190">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1bd7a-191">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="1bd7a-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="1bd7a-192">Wystąpił nieoczekiwany błąd wystąpił podczas próby otwarcia połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="1bd7a-192">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="1bd7a-193">**Objawy**: podczas łączenia z klastra usługi HDInsight, który jest w wersji 3.3 lub 3.4, może zostać wyświetlony błąd, który wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-193">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="1bd7a-194">Ślad stosu dla tego błędu rozpoczyna się od następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-194">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="1bd7a-195">**Przyczyna**: niezgodność wersji pliku commons codec.jar używane przez SQuirreL i wersji wymaganej przez składniki programu Hive JDBC przyczyną tego błędu.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-195">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components.</span></span>

<span data-ttu-id="1bd7a-196">**Rozdzielczość**: Aby naprawić ten błąd, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1bd7a-196">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="1bd7a-197">Pobierz plik jar koder-dekoder commons z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-197">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="1bd7a-198">Zamknij SQuirreL, a następnie przejdź do katalogu, którym SQuirreL jest zainstalowany w systemie.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-198">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="1bd7a-199">W katalogu SquirreL w obszarze `lib` katalogu, Zastąp istniejące codec.jar commons każdy z nich pobrane z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-199">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="1bd7a-200">Uruchom ponownie SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-200">Restart SQuirreL.</span></span> <span data-ttu-id="1bd7a-201">Błąd nie powinien wystąpić podczas nawiązywania połączenia Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-201">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bd7a-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bd7a-202">Next steps</span></span>

<span data-ttu-id="1bd7a-203">Teraz, kiedy znasz jak pracować z Hive za pomocą JDBC, użyj następujących linków, aby poznać inne sposoby pracy z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bd7a-203">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="1bd7a-204">Przekazywanie danych do usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-204">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="1bd7a-205">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1bd7a-206">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1bd7a-207">Korzystanie z zadań MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bd7a-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
