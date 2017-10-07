---
title: "aaaLearn przy użyciu piaskownicy — emulator — Azure HDInsight Hadoop | Dokumentacja firmy Microsoft"
description: "toostart poznawania przy użyciu hello ekosystemu Hadoop, można utworzyć piaskownicy Hadoop z Hortonworks na maszynie wirtualnej platformy Azure. "
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
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="e8747-104">Rozpoczynanie pracy z piaskownicą Hadoop, emulator na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8747-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="e8747-105">Dowiedz się, jak tooinstall hello piaskownicy Hadoop z Hortonworks na toolearn maszyny wirtualnej o hello ekosystemu Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e8747-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="e8747-106">piaskownica Hello zapewnia toolearn środowisko rozwoju lokalnego, o Hadoop, System plików rozproszonych Hadoop (HDFS) i przesyłanie zadań.</span><span class="sxs-lookup"><span data-stu-id="e8747-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="e8747-107">Po zapoznaniu się z usługi Hadoop, można uruchomić przy użyciu platformy Hadoop na platformie Azure przez utworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8747-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="e8747-108">Aby uzyskać więcej informacji dotyczących sposobu uruchamiania tooget, zobacz [Rozpoczynanie pracy z platformą Hadoop w HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8747-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8747-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e8747-109">Prerequisites</span></span>
* <span data-ttu-id="e8747-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="e8747-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="e8747-111">Pobierz i zainstaluj go z [tutaj](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="e8747-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="e8747-112">Pobierz i zainstaluj hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e8747-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="e8747-113">Przeglądaj toohello [pobiera Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e8747-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="e8747-114">Kliknij przycisk **Pobierz VIRTUALBOX** toodownload hello najnowsze piaskownicy Hortonworks na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8747-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="e8747-115">Jesteś tooregister zostanie wyświetlony monit o firmie Hortonworks przed rozpoczęciem powitalne pobierania.</span><span class="sxs-lookup"><span data-stu-id="e8747-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="e8747-116">Trwa jeden tootwo toodownload godzin w zależności od szybkości sieci.</span><span class="sxs-lookup"><span data-stu-id="e8747-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Łącze obrazu do pobrania izolowanego Hortonworks VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="e8747-118">Z hello tej samej stronie sieci web, kliknij przycisk hello **importu na pole wirtualnego** link toodownload plik PDF zawierający instrukcje instalacji hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8747-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="e8747-119">toodownload piaskownicy wersji starszej HDP rozwiń archiwum hello:</span><span class="sxs-lookup"><span data-stu-id="e8747-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Archiwum Hortonworks piaskownicy](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="e8747-121">Uruchom maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="e8747-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="e8747-122">Otwórz program Oracle VirtualBox maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e8747-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="e8747-123">Z hello **pliku** menu, kliknij przycisk **urządzenia importu**, a następnie określ hello piaskownicy Hortonworks obrazu.</span><span class="sxs-lookup"><span data-stu-id="e8747-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="e8747-124">Wybierz hello Hortonworks piaskownicy, kliknij przycisk **Start**, a następnie **Start normalny**.</span><span class="sxs-lookup"><span data-stu-id="e8747-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="e8747-125">Po zakończeniu procesu rozruchu hello hello maszyny wirtualnej zawiera instrukcje dotyczące logowania.</span><span class="sxs-lookup"><span data-stu-id="e8747-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Normalnego uruchomienia](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="e8747-127">Otwórz przeglądarkę sieci web i przejdź toohello wyświetlany adres URL (zazwyczaj http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="e8747-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="e8747-128">Ustawianie hasła piaskownicy</span><span class="sxs-lookup"><span data-stu-id="e8747-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="e8747-129">Z hello **wprowadzenie** krok hello Hortonworks piaskownicy, wybierz **zaawansowane opcje wyświetlania**.</span><span class="sxs-lookup"><span data-stu-id="e8747-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="e8747-130">Użyj informacji hello na tej stronie toolog w piaskownicy toohello przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="e8747-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="e8747-131">Użyj hello nazwy i hasła.</span><span class="sxs-lookup"><span data-stu-id="e8747-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e8747-132">Jeśli nie ma zainstalowanego klienta SSH, możesz użyć hello SSH opartych na sieci web dostępnych na przez maszynę wirtualną hello na **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="e8747-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="e8747-133">Witaj pierwszego, gdy nawiązujesz połączenie przy użyciu protokołu SSH, jesteś toochange zostanie wyświetlony monit o hasło hello hello konta głównego.</span><span class="sxs-lookup"><span data-stu-id="e8747-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="e8747-134">Wprowadź nowe hasło, które zostaną użyte podczas logowania przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="e8747-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="e8747-135">Po zalogowaniu, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e8747-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="e8747-136">Po wyświetleniu monitu podaj hasło dla hello Ambari konta administratora.</span><span class="sxs-lookup"><span data-stu-id="e8747-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="e8747-137">To jest używany, gdy uzyskujesz dostęp do Interfejsu sieci Web Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="e8747-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="e8747-138">Używanie Hive poleceń</span><span class="sxs-lookup"><span data-stu-id="e8747-138">Use Hive commands</span></span>

1. <span data-ttu-id="e8747-139">Z toohello piaskownicy połączenia SSH Użyj hello następujące polecenia toostart hello Hive powłoki:</span><span class="sxs-lookup"><span data-stu-id="e8747-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="e8747-140">Po rozpoczęciu powłoki hello, użyj następującego tooview hello tabel, które są udostępniane w piaskownicy hello hello:</span><span class="sxs-lookup"><span data-stu-id="e8747-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="e8747-141">Witaj Użyj poniższych tooretrieve 10 wierszy z hello `sample_07` tabeli:</span><span class="sxs-lookup"><span data-stu-id="e8747-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="e8747-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8747-142">Next steps</span></span>
* [<span data-ttu-id="e8747-143">Dowiedz się, jak toouse programu Visual Studio z hello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="e8747-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="e8747-144">Learning liny hello hello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="e8747-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="e8747-145">Samouczek Hadoop — wprowadzenie HDP</span><span class="sxs-lookup"><span data-stu-id="e8747-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

