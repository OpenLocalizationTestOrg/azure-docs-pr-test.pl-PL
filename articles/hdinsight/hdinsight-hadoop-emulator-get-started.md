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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Rozpoczynanie pracy z piaskownicą Hadoop, emulator na maszynie wirtualnej

Dowiedz się, jak tooinstall hello piaskownicy Hadoop z Hortonworks na toolearn maszyny wirtualnej o hello ekosystemu Hadoop. piaskownica Hello zapewnia toolearn środowisko rozwoju lokalnego, o Hadoop, System plików rozproszonych Hadoop (HDFS) i przesyłanie zadań. Po zapoznaniu się z usługi Hadoop, można uruchomić przy użyciu platformy Hadoop na platformie Azure przez utworzenie klastra usługi HDInsight. Aby uzyskać więcej informacji dotyczących sposobu uruchamiania tooget, zobacz [Rozpoczynanie pracy z platformą Hadoop w HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Wymagania wstępne
* [Oracle VirtualBox](https://www.virtualbox.org/). Pobierz i zainstaluj go z [tutaj](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Pobierz i zainstaluj hello maszyny wirtualnej
1. Przeglądaj toohello [pobiera Hortonworks](http://hortonworks.com/downloads/#sandbox).

2. Kliknij przycisk **Pobierz VIRTUALBOX** toodownload hello najnowsze piaskownicy Hortonworks na maszynie Wirtualnej. Jesteś tooregister zostanie wyświetlony monit o firmie Hortonworks przed rozpoczęciem powitalne pobierania. Trwa jeden tootwo toodownload godzin w zależności od szybkości sieci.
   
    ![Łącze obrazu do pobrania izolowanego Hortonworks VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. Z hello tej samej stronie sieci web, kliknij przycisk hello **importu na pole wirtualnego** link toodownload plik PDF zawierający instrukcje instalacji hello maszyny wirtualnej.

toodownload piaskownicy wersji starszej HDP rozwiń archiwum hello:

![Archiwum Hortonworks piaskownicy](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Uruchom maszynę wirtualną hello

1. Otwórz program Oracle VirtualBox maszyny Wirtualnej.
2. Z hello **pliku** menu, kliknij przycisk **urządzenia importu**, a następnie określ hello piaskownicy Hortonworks obrazu.
1. Wybierz hello Hortonworks piaskownicy, kliknij przycisk **Start**, a następnie **Start normalny**. Po zakończeniu procesu rozruchu hello hello maszyny wirtualnej zawiera instrukcje dotyczące logowania.
   
    ![Normalnego uruchomienia](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Otwórz przeglądarkę sieci web i przejdź toohello wyświetlany adres URL (zazwyczaj http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Ustawianie hasła piaskownicy

1. Z hello **wprowadzenie** krok hello Hortonworks piaskownicy, wybierz **zaawansowane opcje wyświetlania**. Użyj informacji hello na tej stronie toolog w piaskownicy toohello przy użyciu protokołu SSH. Użyj hello nazwy i hasła.
   
   > [!NOTE]
   > Jeśli nie ma zainstalowanego klienta SSH, możesz użyć hello SSH opartych na sieci web dostępnych na przez maszynę wirtualną hello na **http://localhost:4200 /**.
   > 
   
    Witaj pierwszego, gdy nawiązujesz połączenie przy użyciu protokołu SSH, jesteś toochange zostanie wyświetlony monit o hasło hello hello konta głównego. Wprowadź nowe hasło, które zostaną użyte podczas logowania przy użyciu protokołu SSH.

2. Po zalogowaniu, wprowadź następujące polecenie hello:
   
        ambari-admin-password-reset
   
    Po wyświetleniu monitu podaj hasło dla hello Ambari konta administratora. To jest używany, gdy uzyskujesz dostęp do Interfejsu sieci Web Ambari hello.

## <a name="use-hive-commands"></a>Używanie Hive poleceń

1. Z toohello piaskownicy połączenia SSH Użyj hello następujące polecenia toostart hello Hive powłoki:
   
        hive
2. Po rozpoczęciu powłoki hello, użyj następującego tooview hello tabel, które są udostępniane w piaskownicy hello hello:
   
        show tables;
3. Witaj Użyj poniższych tooretrieve 10 wierszy z hello `sample_07` tabeli:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się, jak toouse programu Visual Studio z hello Hortonworks piaskownicy](hdinsight-hadoop-emulator-visual-studio.md)
* [Learning liny hello hello Hortonworks piaskownicy](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Samouczek Hadoop — wprowadzenie HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

