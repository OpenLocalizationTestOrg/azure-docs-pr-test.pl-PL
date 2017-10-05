---
title: "Łączenie programu Excel do platformy Hadoop za pomocą sterownika ODBC Hive — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania i używania danych zapytania w klastrach HDInsight sterownik Microsoft Hive ODBC dla programu Excel z programu Microsoft Excel."
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="6ecc0-104">Łączenie programu Excel do platformy Hadoop w usłudze Azure HDInsight z sterownik Microsoft Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="6ecc0-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="6ecc0-105">Rozwiązania danych Big Data firmy Microsoft składniki Microsoft Business Intelligence (BI) jest zintegrowany z klastrów platformy Apache Hadoop, które zostały wdrożone w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="6ecc0-106">Przykładem takiej integracji jest możliwość łączenia programu Excel w magazynie danych gałęzi klastra usługi Hadoop w usłudze HDInsight za pomocą sterownika Microsoft Hive bazy danych połączenia ODBC (Open).</span><span class="sxs-lookup"><span data-stu-id="6ecc0-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="6ecc0-107">Istnieje również możliwość łączenia danych związanych z klastrem usługi HDInsight i innych źródeł danych, w tym inne klastry Hadoop (z systemem innym niż HDInsight), w programie Excel przy użyciu dodatku Microsoft Power Query dla programu Excel.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="6ecc0-108">Aby uzyskać informacje na temat instalowania i za pomocą dodatku Power Query, zobacz [łączenie programu Excel do usługi HDInsight za pomocą dodatku Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="6ecc0-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="6ecc0-109">Chociaż kroki opisane w tym artykule mogą być używane z klastra z systemem Linux lub HDInsight opartych na systemie Windows, Windows jest wymagany dla stacji roboczej klienta.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="6ecc0-110">**Wymagania wstępne**:</span><span class="sxs-lookup"><span data-stu-id="6ecc0-110">**Prerequisites**:</span></span>

<span data-ttu-id="6ecc0-111">Przed rozpoczęciem tego artykułu, musi mieć następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6ecc0-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="6ecc0-112">**Klaster usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="6ecc0-113">Aby go utworzyć, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="6ecc0-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="6ecc0-114">**Stacja robocza** z pakietu Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 autonomicznej lub Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="6ecc0-115">Zainstalować sterownik Microsoft Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="6ecc0-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="6ecc0-116">Pobierz i zainstaluj sterownik Microsoft Hive ODBC z [Centrum pobierania][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="6ecc0-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="6ecc0-117">W 32-bitowy lub 64-bitowych wersjach systemu Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 i Windows Server 2012 można zainstalować ten sterownik.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="6ecc0-118">Sterownik umożliwia połączenie do usługi Azure HDInsight (w wersji 1.6 lub nowszy) i emulatora usługi Azure HDInsight (v.1.0.0.0 i nowsze).</span><span class="sxs-lookup"><span data-stu-id="6ecc0-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="6ecc0-119">Jest zainstalowanie wersji zgodnej z wersją aplikacji, w którym korzystać ze sterownika ODBC.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="6ecc0-120">W tym samouczku sterownik jest używany z Office Excel.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="6ecc0-121">Tworzenie źródła danych ODBC usługi Hive</span><span class="sxs-lookup"><span data-stu-id="6ecc0-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="6ecc0-122">Poniższe kroki pokazują, jak utworzyć Hive źródła danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="6ecc0-123">Z systemu Windows 8 lub Windows 10, naciśnij klawisz systemu Windows, aby otworzyć ekranu startowego, a następnie wpisz **źródeł danych**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="6ecc0-124">Kliknij przycisk **skonfigurować źródła danych ODBC (32-bitowy)** lub **Konfigurowanie źródeł danych ODBC (64-bitowy)** w zależności od używanej wersji pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="6ecc0-125">Jeśli korzystasz z systemu Windows 7, wybierz **źródła danych ODBC (32 bity)** lub **źródła danych ODBC (64 bity)** z **narzędzia administracyjne**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="6ecc0-126">Powinna zostać wyświetlona **Administrator źródła danych ODBC** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="6ecc0-127">![Administrator źródeł danych OBDC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "skonfigurować DSN przy użyciu Administrator źródła danych ODBC")</span><span class="sxs-lookup"><span data-stu-id="6ecc0-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="6ecc0-128">Przy użyciu serwera DNS użytkownika, kliknij przycisk **Dodaj** otworzyć **Utwórz nowe źródło danych** kreatora.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="6ecc0-129">Wybierz **sterownik Microsoft Hive ODBC**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="6ecc0-130">Powinna zostać wyświetlona **Instalator programu Microsoft Hive ODBC sterownika DNS** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="6ecc0-131">Wpisz lub wybierz poniższe wartości:</span><span class="sxs-lookup"><span data-stu-id="6ecc0-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="6ecc0-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ecc0-132">Property</span></span> | <span data-ttu-id="6ecc0-133">Opis</span><span class="sxs-lookup"><span data-stu-id="6ecc0-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="6ecc0-134">Data Source Name (Nazwa źródła danych)</span><span class="sxs-lookup"><span data-stu-id="6ecc0-134">Data Source Name</span></span> |<span data-ttu-id="6ecc0-135">Nadaj nazwę źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="6ecc0-136">Host</span><span class="sxs-lookup"><span data-stu-id="6ecc0-136">Host</span></span> |<span data-ttu-id="6ecc0-137">Wprowadź ciąg &lt;nazwa_klastra_usługi_HDInsight>.azurehdinsight.net,</span><span class="sxs-lookup"><span data-stu-id="6ecc0-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="6ecc0-138">np. myHDICluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="6ecc0-139">Port</span><span class="sxs-lookup"><span data-stu-id="6ecc0-139">Port</span></span> |<span data-ttu-id="6ecc0-140">Użyj portu <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="6ecc0-141">(Ten port został zmieniony z 563 na 443).</span><span class="sxs-lookup"><span data-stu-id="6ecc0-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="6ecc0-142">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="6ecc0-142">Database</span></span> |<span data-ttu-id="6ecc0-143">Użyj wartości <strong>Default</strong> (Domyślna).</span><span class="sxs-lookup"><span data-stu-id="6ecc0-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="6ecc0-144">Mechanism (Mechanizm)</span><span class="sxs-lookup"><span data-stu-id="6ecc0-144">Mechanism</span></span> |<span data-ttu-id="6ecc0-145">Wybierz wartość <strong>Azure HDInsight Service</strong> (Usługa Azure HDInsight).</span><span class="sxs-lookup"><span data-stu-id="6ecc0-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="6ecc0-146">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ecc0-146">User Name</span></span> |<span data-ttu-id="6ecc0-147">Wprowadź username użytkownika HTTP klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="6ecc0-148">Domyślna nazwa użytkownika to <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="6ecc0-149">Hasło</span><span class="sxs-lookup"><span data-stu-id="6ecc0-149">Password</span></span> |<span data-ttu-id="6ecc0-150">Wprowadź hasło użytkownika klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="6ecc0-151">Istnieją pewne ważne parametry znać po kliknięciu **zaawansowane opcje**:</span><span class="sxs-lookup"><span data-stu-id="6ecc0-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="6ecc0-152">Parametr</span><span class="sxs-lookup"><span data-stu-id="6ecc0-152">Parameter</span></span> | <span data-ttu-id="6ecc0-153">Opis</span><span class="sxs-lookup"><span data-stu-id="6ecc0-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="6ecc0-154">Użyj natywnego zapytania</span><span class="sxs-lookup"><span data-stu-id="6ecc0-154">Use Native Query</span></span> |<span data-ttu-id="6ecc0-155">Gdy jest wybrana, sterownik ODBC nie próbuje przekonwertować TSQL HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="6ecc0-156">Są go używać tylko wtedy, gdy 100% się, że przesyłasz czysty instrukcje HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="6ecc0-157">Podczas nawiązywania połączenia z serwerem SQL lub bazy danych SQL Azure, należy pozostawić niezaznaczone.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="6ecc0-158">Pobranych na blok wierszy</span><span class="sxs-lookup"><span data-stu-id="6ecc0-158">Rows fetched per block</span></span> |<span data-ttu-id="6ecc0-159">Podczas pobierania dużej liczby rekordów, dostrajanie ten parametr może zajść konieczność zapewnienia optymalnej wydajności.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="6ecc0-160">Domyślna długość kolumny ciąg, długość kolumny binarnej, skala kolumny dziesiętnej</span><span class="sxs-lookup"><span data-stu-id="6ecc0-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="6ecc0-161">Typ danych długości i opisie może mieć wpływ na sposób dane są zwracane.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="6ecc0-162">Spowodują one nieprawidłowe informacje będą zwracane z powodu utraty dokładność i/lub obcięcie.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="6ecc0-163">![Zaawansowane opcje](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN zaawansowane opcje konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="6ecc0-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="6ecc0-164">Kliknij przycisk **Test** do testowania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="6ecc0-165">Gdy źródło danych jest skonfigurowane poprawnie, pokazuje *testy ZAKOŃCZYŁO się pomyślnie!*.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="6ecc0-166">Kliknij przycisk **OK** aby zamknąć okno dialogowe testu.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="6ecc0-167">Nowe źródło danych musi zostać umieszczony w **Administrator źródła danych ODBC**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="6ecc0-168">Kliknij przycisk **OK** aby zakończyć pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="6ecc0-169">Importowanie danych do programu Excel z usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ecc0-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="6ecc0-170">W poniższych krokach opisano sposób importowania danych z tabeli programu Hive do skoroszytu programu Excel przy użyciu źródła danych ODBC, który został utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="6ecc0-171">Otwórz nowy lub istniejący skoroszyt w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="6ecc0-172">Z **danych** , kliknij pozycję **Pobierz dane**, kliknij przycisk **z innych źródeł**, a następnie kliknij przycisk **z ODBC** można uruchomić **danych Kreator połączenia**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="6ecc0-173">![Kreator połączenia danych otwartych](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Kreator połączenia danych otwartych")</span><span class="sxs-lookup"><span data-stu-id="6ecc0-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="6ecc0-174">Wybierz nazwę źródła danych, który został utworzony w ostatniej sekcji, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="6ecc0-175">Wprowadź nazwę użytkownika Hadoop (domyślną nazwą jest admin) i hasło, a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="6ecc0-176">W Nawigatorze, rozwiń węzeł **HIVE**, rozwiń węzeł **domyślne**, kliknij przycisk **hivesampletable**, a następnie kliknij przycisk **obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="6ecc0-177">Importowanie danych do programu Excel może potrwać kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="6ecc0-178">![Nawigator ODBC programu Hive HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Kreator połączenia danych otwartych")</span><span class="sxs-lookup"><span data-stu-id="6ecc0-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="6ecc0-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ecc0-179">Next steps</span></span>
<span data-ttu-id="6ecc0-180">W tym artykule przedstawiono sposób użycia sterownik Microsoft Hive ODBC do pobierania danych z usługi HDInsight do programu Excel.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="6ecc0-181">Podobnie można pobierać dane z usługi HDInsight do bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="6ecc0-182">Istnieje również możliwość do przekazania danych do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ecc0-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="6ecc0-183">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="6ecc0-183">To learn more, see:</span></span>

* <span data-ttu-id="6ecc0-184">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="6ecc0-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="6ecc0-185">[Przekazywanie danych do usługi HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6ecc0-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6ecc0-186">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="6ecc0-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


