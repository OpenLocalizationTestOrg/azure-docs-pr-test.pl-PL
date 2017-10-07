---
title: "tunelowania SSH aaaUse — tooaccess Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toosecurely tunelu SSH Przeglądaj zasobów sieci web znajdujących się na węzły HDInsight opartych na systemie Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Użyj tunelowania SSH tooaccess interfejsu użytkownika sieci web Ambari, JobHistory, NameNode, Oozie i innych sieci web UI

Klastry usługi HDInsight opartej na systemie Linux zapewniają dostęp tooAmbari interfejsu użytkownika sieci web za pośrednictwem Internetu hello, ale niektóre funkcje hello interfejsu użytkownika nie są. Na przykład hello interfejsu użytkownika sieci web dla innych usług, które są udostępniane za pośrednictwem narzędzia Ambari. Funkcje programu hello interfejsu użytkownika sieci web Ambari należy użyć SSH tunelu toohello klastra head.

## <a name="why-use-an-ssh-tunnel"></a>Dlaczego warto korzystać z tunelowania SSH

Tylko kilka Ambari hello menu pracy za pośrednictwem tunelu SSH. Tych menu korzystają z witryny sieci web i usług działających na inne typy węzłów, takich jak węzłów procesu roboczego. Często tych witryn sieci web nie są zabezpieczone, więc nie toodirectly bezpieczne Uwidacznianie hello je na internet.

powitania po UI sieci Web wymagają tunelu SSH:

* JobHistory
* NameNode
* Stosy wątków
* Oozie interfejsu użytkownika sieci web
* Główna baza danych HBase i dzienniki interfejsu użytkownika

Jeśli używasz toocustomize akcji skryptu klastra żadnych usług ani narzędzi, które można zainstalować z użyciem interfejsu użytkownika sieci web wymagają tunelu SSH. Na przykład po zainstalowaniu aplikacji Hue za pomocą akcji skryptu, należy użyć SSH tunelu tooaccess hello Hue interfejsu użytkownika sieci web.

> [!IMPORTANT]
> Jeśli masz tooHDInsight bezpośredni dostęp do sieci wirtualnej, nie trzeba toouse tuneli SSH. Przykład bezpośredni dostęp do usługi HDInsight za pośrednictwem sieci wirtualnej, zobacz hello [sieć lokalną tooyour połączyć HDInsight](connect-on-premises-network.md) dokumentu.

## <a name="what-is-an-ssh-tunnel"></a>Co to jest tunelu SSH

[Secure Shell (SSH) tunelowania](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) kieruje ruch przesyłany portu tooa na lokalnej stacji roboczej. Witaj, ruch jest kierowany przez SSH połączenia tooyour HDInsight węzła głównego klastra. Żądanie hello jest rozwiązywany tak, jakby pochodziły hello węzła głównego. odpowiedź Hello jest następnie kierowane za pośrednictwem stacji roboczej tooyour tunelu hello.

## <a name="prerequisites"></a>Wymagania wstępne

* Klient SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Przeglądarki sieci web, które mogą być skonfigurowane toouse SOCKS5 serwera proxy.

    > [!WARNING]
    > Obsługa serwera proxy SOCKS Hello wbudowanych w system Windows nie obsługuje SOCKS5 i nie działa z hello kroków w tym dokumencie. Witaj następujące przeglądarki zależą od ustawień serwera proxy systemu Windows, a nie obecnie pracy hello kroków w tym dokumencie:
    >
    > * Przeglądarka Microsoft Edge
    > * Program Microsoft Internet Explorer
    >
    > Google Chrome również zależy od ustawień serwera proxy systemu Windows hello. Można jednak zainstalować rozszerzenia, które obsługują SOCKS5. Firma Microsoft zaleca [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Tworzenie tunelu przy użyciu polecenia SSH hello

Użyj hello następujące polecenie toocreate tunelu SSH za pomocą hello `ssh` polecenia. Zastąp **USERNAME** użytkownika SSH dla klastra usługi HDInsight i Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

To polecenie tworzy połączenia, który przekierowuje ruch toolocal portu 9876 toohello klastra za pomocą protokołu SSH. dostępne są opcje Hello:

* **D 9876** — Witaj port lokalny, który przekierowuje ruch za pośrednictwem tunelu hello.
* **C** -Kompresuj wszystkich danych, ponieważ ruchu w sieci web jest przeważnie tekstu.
* **2** -force SSH tootry protocol w wersji 2 tylko.
* **q** — tryb cichy.
* **T** — Wyłącz pseudo-tty alokacji, ponieważ będziemy są po prostu przekazywania portu.
* **n**— Wartość pola Zapobiegaj odczytu STDIN, ponieważ będziemy są po prostu przekazywania portu.
* **N** -nie wykonuj polecenia zdalnego, ponieważ będziemy są po prostu przekazywania portu.
* **f** -wykonywane w tle hello.

Po zakończeniu działania polecenia hello ruch wysyłany tooport 9876 na komputerze lokalnym hello jest kierowany toohello węzła głównego klastra.

## <a name="useputty"></a>Tworzenie tunelu przy użyciu programu PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) graficznego klienta SSH dla systemu Windows. Użyj hello następujące kroki toocreate tunelu SSH przy użyciu programu PuTTY:

1. Otwórz program PuTTY i wprowadzić informacje o połączeniu. Jeśli nie masz doświadczenia w obsłudze programu PuTTY, zobacz hello [programu PuTTY dokumentacji (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. W hello **kategorii** toohello sekcji lewej strony okna dialogowego hello, rozwiń **połączenia**, rozwiń węzeł **SSH**, a następnie wybierz **tuneli**.

3. Podaj następujące informacje na powitania hello **przekierowanie portów opcje kontrolujące SSH** formularza:
   
   * **Port źródłowy** — Witaj port na powitania klienta, że chcesz tooforward. Na przykład **9876**.

   * **Docelowy** — Witaj adres SSH dla klastra usługi HDInsight opartej na systemie Linux hello. Na przykład **mójklaster-ssh.azurehdinsight.net**.

   * **Dynamic** (Dynamiczny) — umożliwia dynamiczny routing serwera proxy SOCKS.
     
     ![Obraz tunelowania opcje](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Kliknij przycisk **Dodaj** tooadd hello ustawienia, a następnie kliknij przycisk **Otwórz** tooopen połączenie SSH.

5. Po wyświetleniu monitu zaloguj się na serwerze toohello.

## <a name="use-hello-tunnel-from-your-browser"></a>Użyj tunelu hello z przeglądarki

> [!IMPORTANT]
> Witaj kroki w tej sekcji hello użyj przeglądarki Mozilla FireFox, ponieważ tworzy ona hello tych samych ustawień serwera proxy na wszystkich platformach. Inne nowoczesne przeglądarki, takich jak Google Chrome, mogą wymagać rozszerzenia, takie jak toowork FoxyProxy z hello tunelu.

1. Skonfiguruj hello przeglądarki toouse **localhost** i portu hello używane podczas tworzenia tunelu hello jako **SOCKS v5** serwera proxy. Poniżej przedstawiono wygląd hello Firefox ustawienia. Jeśli użyto innego portu niż 9876 zmienić toohello portu hello, używanego jednego:
   
    ![Obraz ustawień przeglądarki Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Wybieranie **DNS zdalnego** rozpoznaje żądania systemu nazw domen (DNS, Domain Name System) przy użyciu hello klastra usługi HDInsight. To ustawienie jest rozpoznawany jako DNS za pomocą węzła głównego hello hello klastra.

2. Weryfikowanie działania tego tunelu hello odwiedzając witrynę, takich jak [http://www.whatismyip.com/](http://www.whatismyip.com/). Hello IP zwrócił powinna być jeden używana przez hello Microsoft Azure w centrum danych.

## <a name="verify-with-ambari-web-ui"></a>Weryfikacja Ambari web UI

Po ustanowieniu hello klastra, użyj hello następujące kroki tooverify, czy są dostępne usługi sieci web UI hello Ambari Web:

1. W przeglądarce Przejdź toohttp://headnodehost:8080. Witaj `headnodehost` adres są wysyłane za pośrednictwem hello tunelu toohello klastra i rozwiązać headnode toohello, który Ambari działa na. Po wyświetleniu monitu wprowadź nazwę użytkownika hello admin (Administrator) i hasło dla klastra. Może pojawić się prośba po raz drugi przez hello Ambari web UI. Jeśli tak, należy ponownie wprowadzić informacje o hello.

   > [!NOTE]
   > Używając hello http://headnodehost:8080 adres tooconnect toohello klastra jest nawiązywane za pośrednictwem tunelu hello. Komunikat jest zabezpieczony przy użyciu tunelu SSH hello zamiast protokołu HTTPS. tooconnect ponad hello internet przy użyciu protokołu HTTPS, należy użyć https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą hello hello klastra.

2. Hello Interfejsu sieci Web Ambari zaznacz na liście hello na powitania po lewej stronie powitania systemu plików HDFS.

    ![Obraz o wybrany system plików HDFS](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Po wyświetleniu hello informacje o systemie plików HDFS usługi wybierz **szybkie linki**. Zostanie wyświetlona lista hello głównymi węzłami klastra. Wybierz jeden z węzłów głównych hello, a następnie wybierz **interfejsu użytkownika NameNode**.

    ![Obraz powitania QuickLinks menu rozwinięty](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Po wybraniu __szybkie linki__, mogą wystąpić wskaźnik oczekiwania. Ten stan może wystąpić, jeśli masz wolne połączenie internetowe. Zaczekaj minutę lub dwie na toobe danych hello otrzymany z serwera hello, a następnie spróbuj ponownie hello listy.
   >
   > Niektóre wpisy w hello **szybkie linki** menu może zostać przerwane przez hello prawej krawędzi ekranu hello. Jeśli tak, rozwiń menu hello przy użyciu myszy i użyj hello strzałki w prawo klucza tooscroll hello ekranu toohello prawo toosee hello reszty hello menu.

4. Jest wyświetlana strona toohello podobne, po obrazu:

    ![Obraz powitania NameNode interfejsu użytkownika](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Zwróć uwagę, adres URL hello na tej stronie; powinien być podobny zbyt**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/klaster**. Ten identyfikator URI używa hello wewnętrzny pełną nazwę domeny (FQDN) węzła hello i jest dostępny tylko przy użyciu tunelu SSH.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już toocreate i używania tunelu SSH, zobacz temat powitania po dokumentu do innych metod toouse Ambari:

* [Zarządzanie klastrami usługi HDInsight przy użyciu Ambari](hdinsight-hadoop-manage-ambari.md)

Aby uzyskać więcej informacji o korzystaniu z protokołu SSH z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

