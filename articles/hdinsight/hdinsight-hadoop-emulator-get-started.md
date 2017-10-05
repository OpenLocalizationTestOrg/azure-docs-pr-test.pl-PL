---
title: "Dowiedz się przy użyciu piaskownicy — emulator — Azure HDInsight Hadoop | Dokumentacja firmy Microsoft"
description: "Aby rozpocząć, informacje o użyciu ekosystemu Hadoop, skonfigurowaniem piaskownicy Hadoop z Hortonworks na maszynie wirtualnej platformy Azure. "
keywords: "emulator usługi hadoop, piaskownicy hadoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="7f7db-104">Rozpoczynanie pracy z piaskownicą Hadoop, emulator na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7f7db-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="7f7db-105">Dowiedz się, jak zainstalować piaskownicy Hadoop z Hortonworks na maszynie wirtualnej, aby dowiedzieć się więcej o ekosystemu Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7f7db-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="7f7db-106">Piaskownica udostępnia środowisko deweloperskie lokalne informacje na temat usługi Hadoop, System plików rozproszonych Hadoop (HDFS) i przesyłanie zadań.</span><span class="sxs-lookup"><span data-stu-id="7f7db-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="7f7db-107">Po zapoznaniu się z usługi Hadoop, można uruchomić przy użyciu platformy Hadoop na platformie Azure przez utworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f7db-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="7f7db-108">Aby uzyskać więcej informacji o tym, jak rozpocząć pracę, zobacz [Rozpoczynanie pracy z platformą Hadoop w HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7f7db-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f7db-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f7db-109">Prerequisites</span></span>
* <span data-ttu-id="7f7db-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="7f7db-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="7f7db-111">Pobierz i zainstaluj go z [tutaj](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="7f7db-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="7f7db-112">Pobierz i zainstaluj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="7f7db-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="7f7db-113">Przejdź do [pobiera Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="7f7db-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="7f7db-114">Kliknij przycisk **Pobierz VIRTUALBOX** pobrać najnowsze piaskownicy Hortonworks na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7db-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="7f7db-115">Zostanie wyświetlony monit Zarejestruj Hortonworks przed rozpoczęciem pobierania.</span><span class="sxs-lookup"><span data-stu-id="7f7db-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="7f7db-116">Trwa jednej do dwóch godzin, aby pobrać w zależności od szybkości sieci.</span><span class="sxs-lookup"><span data-stu-id="7f7db-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Łącze obrazu do pobrania izolowanego Hortonworks VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="7f7db-118">W tej samej stronie sieci web, kliknij polecenie **importu na pole wirtualnego** łącze, aby pobrać plik PDF zawierający instrukcje instalacji dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7db-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="7f7db-119">Aby pobrać starsze piaskownicy wersji HDP, rozwiń archiwum:</span><span class="sxs-lookup"><span data-stu-id="7f7db-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Archiwum Hortonworks piaskownicy](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="7f7db-121">Uruchom maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="7f7db-121">Start the virtual machine</span></span>

1. <span data-ttu-id="7f7db-122">Otwórz program Oracle VirtualBox maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7db-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="7f7db-123">Z **pliku** menu, kliknij przycisk **urządzenia importu**, a następnie określ obraz piaskownicy Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="7f7db-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="7f7db-124">Wybierz piaskownicy Hortonworks, kliknij przycisk **Start**, a następnie **Start normalny**.</span><span class="sxs-lookup"><span data-stu-id="7f7db-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="7f7db-125">Po zakończeniu procesu rozruchu maszyny wirtualnej zawiera instrukcje dotyczące logowania.</span><span class="sxs-lookup"><span data-stu-id="7f7db-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Normalnego uruchomienia](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="7f7db-127">Otwórz przeglądarkę sieci web i przejdź do wyświetlany adres URL (zazwyczaj http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="7f7db-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="7f7db-128">Ustawianie hasła piaskownicy</span><span class="sxs-lookup"><span data-stu-id="7f7db-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="7f7db-129">Z **wprowadzenie** krok piaskownicy Hortonworks stronie wybierz **zaawansowane opcje wyświetlania**.</span><span class="sxs-lookup"><span data-stu-id="7f7db-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="7f7db-130">Skorzystaj z informacji na tej stronie, aby zalogować się do piaskownicy przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="7f7db-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="7f7db-131">Użyj nazwy i hasła.</span><span class="sxs-lookup"><span data-stu-id="7f7db-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7f7db-132">Jeśli nie ma zainstalowanego klienta SSH, możesz użyć SSH opartych na sieci web, dostępnych na przez maszynę wirtualną na **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="7f7db-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="7f7db-133">Podczas pierwszego, gdy nawiązujesz połączenie przy użyciu protokołu SSH, monit o zmianę hasła dla konta głównego.</span><span class="sxs-lookup"><span data-stu-id="7f7db-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="7f7db-134">Wprowadź nowe hasło, które zostaną użyte podczas logowania przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="7f7db-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="7f7db-135">Po zalogowaniu, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7f7db-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="7f7db-136">Po wyświetleniu monitu podaj hasło dla konta administratora narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="7f7db-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="7f7db-137">To jest używany, gdy uzyskujesz dostęp do Interfejsu sieci Web Ambari.</span><span class="sxs-lookup"><span data-stu-id="7f7db-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="7f7db-138">Używanie Hive poleceń</span><span class="sxs-lookup"><span data-stu-id="7f7db-138">Use Hive commands</span></span>

1. <span data-ttu-id="7f7db-139">Połączenie SSH piaskownicy Użyj następującego polecenia, aby uruchomić powłokę programu Hive:</span><span class="sxs-lookup"><span data-stu-id="7f7db-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="7f7db-140">Po rozpoczęciu powłoki, należy użyć następującego, aby wyświetlić tabele, które są udostępniane w piaskownicy:</span><span class="sxs-lookup"><span data-stu-id="7f7db-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="7f7db-141">Użyj następujących funkcji do pobrania 10 wierszy z `sample_07` tabeli:</span><span class="sxs-lookup"><span data-stu-id="7f7db-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="7f7db-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f7db-142">Next steps</span></span>
* [<span data-ttu-id="7f7db-143">Dowiedz się, jak używać programu Visual Studio z piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7f7db-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="7f7db-144">Learning liny piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7f7db-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="7f7db-145">Samouczek Hadoop — wprowadzenie HDP</span><span class="sxs-lookup"><span data-stu-id="7f7db-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

