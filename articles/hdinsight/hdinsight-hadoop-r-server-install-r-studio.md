---
title: "aaaInstall programu RStudio z serwerem R w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Jak tooinstall programu RStudio z serwerem R w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Instalowanie programu RStudio z serwerem R w usłudze HDInsight

W tym artykule opisano, jak tooinstall hello społecznościową wersję (bezpłatnie) [serwera programu RStudio](https://www.rstudio.com/products/rstudio-server/) hello krawędzi węzeł klastra przy użyciu niestandardowego skryptu. Serwer programu RStudio udostępnia środowiska IDE bazujące na przeglądarce do użycia przez klientów zdalnych i jest powszechnie używany w systemie Linux. Istnieje wiele zintegrowane środowisk deweloperskich (IDE) dostępnych dla R dzisiaj, w tym:

- Firmy Microsoft [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) 
- [Serwer programu RStudio](https://www.rstudio.com/products/rstudio-server/) 
- Walware na podstawie Eclipse [StatET](http://www.walware.de/goto/statet).

Zaletą Hello instalacji programu RStudio serwera na powitania krawędzi węzła z klastra usługi HDInsight jest pełne środowisko IDE dla rozwoju hello i wykonywanie skryptów R z serwerem R w klastrze hello. Ta konfiguracja może być znacznie większą wydajność niż domyślne hello konsoli R.

> [!NOTE]
> Hello procedury opisane w tym artykule jest stosowana tylko, jeśli nie wybrano tooinstall serwera programu RStudio community edition podczas inicjowania obsługi klastra. Jeśli dodano podczas inicjowania obsługi, następnie tooaccess go kliknij na powitania **pulpity nawigacyjne serwera R** kafelka w hello Azure portalu wpis dla klastra, a następnie na powitania **R Studio Server** kafelka. 

Wolisz toouse wersji Pro hello komercyjnie licencję programu RStudio serwera, należy postępować zgodnie z instrukcjami instalacji hello [serwera programu RStudio](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Jeśli korzystasz z klastra usługi HDInsight, dla którego R został zainstalowany przy użyciu hello [zainstalować akcji skryptu języka R](hdinsight-hadoop-r-scripts-linux.md), hello kroków w tym dokumencie nie będą działać poprawnie, ponieważ wymagają one R Server w klastrze usługi HDInsight hello.
>
> 

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Azure HDInsight z zainstalowanym serwerem R. Aby uzyskać instrukcje, zobacz [wprowadzenie R Server w klastrach HDInsight](hdinsight-hadoop-r-server-get-started.md).
* Klient SSH. Dystrybucje systemu Linux i Unix lub Macintosh OS X, hello `ssh` polecenie jest dostępne w systemie operacyjnym hello. W systemie Windows, firma Microsoft zaleca [programów Cygwin](http://www.redhat.com/services/custom/cygwin/) z hello [opcji OpenSSH](https://www.youtube.com/watch?v=CwYSvvGaiWU), lub [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Instalowanie programu RStudio na powitania klastra przy użyciu niestandardowego skryptu

Poniżej przedstawiono kroki hello:

1. Zidentyfikuj węzła krawędzi hello hello klastra. Dla klastra usługi HDInsight, z serwerem R poniżej przedstawiono hello konwencję nazewnictwa dla węzła głównego i węzła krawędzi.
   * Nagłówek węzła`CLUSTERNAME-ssh.azurehdinsight.net`
   * Węzeł krawędzi`CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH do węzła krawędzi hello hello klastra przy użyciu wzorca nazewnictwa hello w kroku 1. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Po nawiązaniu połączenia stają się w klastrze hello użytkownika root. W sesji SSH hello Użyj hello następujące polecenie:

        sudo su -

4. Pobierz hello tooinstall skryptu niestandardowego programu RStudio. Witaj Użyj następującego polecenia:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Zmień uprawnienia hello hello skryptu niestandardowego pliku, a następnie uruchom skrypt hello. Witaj Użyj następującego polecenia:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Hasło SSH jest używany podczas tworzenia klastra usługi HDInsight z serwerem R, można pominąć ten krok i przejdź dalej toohello. Jeśli używasz klucza SSH zamiast toocreate hello klastra, należy ustawić hasło dla użytkownika SSH. Należy to hasło, łącząc tooRStudio. Uruchom następujące polecenia hello:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Po wyświetleniu monitu o **Kerberos bieżącego hasła**, naciśnij klawisz **ENTER**.  Należy pamiętać, że należy zastąpić `USERNAME` użytkownika SSH dla klastra usługi HDInsight. Jeśli pomyślnie ustawiono hasło, powinny być widoczne następujące wiadomość hello:

        passwd: password updated successfully

    Zamknij hello sesji SSH.

8. Tworzenie klastra toohello tunelu SSH przez mapowanie `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` na powitania HDInsight klastra toohello komputera klienckiego. Należy utworzyć tunel SSH przed otwarciem nowej sesji przeglądarki.

   * Klient systemu Linux lub klienta systemu Windows z [programów Cygwin](http://www.redhat.com/services/custom/cygwin/), otwórz sesję terminala i użyj hello następujące polecenie:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Zastąp **USERNAME** użytkownika SSH dla klastra usługi HDInsight i Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.
       Umożliwia także klucz SSH, zamiast hasła przez dodanie `-i id_rsa_key`.        
   * Jeśli następnie używany klient systemu Windows z programu PuTTY

     1. Otwórz program PuTTY i wprowadzić informacje o połączeniu.
     2. W hello **kategorii** toohello sekcji lewej strony okna dialogowego hello, rozwiń **połączenia**, rozwiń węzeł **SSH**, a następnie wybierz **tuneli**.
     3. Podaj następujące informacje na powitania hello **przekierowanie portów opcje kontrolujące SSH** formularza:

        * **Port źródłowy** — Witaj port na powitania klienta, że chcesz tooforward. Na przykład **8787**.
        * **Docelowy** — Witaj lokalizacji docelowej, która musi być zamapowany toohello maszyny lokalnej klienta. Na przykład **localhost:8787**.

            ![Tworzenie tunelu SSH](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Tworzenie tunelu SSH")

     4. Kliknij przycisk **Dodaj** tooadd hello ustawienia, a następnie kliknij przycisk **Otwórz** tooopen połączenie SSH.
     5. Po wyświetleniu monitu zaloguj się za tooestablish serwera toohello sesji i Włącz hello tunelu SSH.

9. Otwórz przeglądarkę sieci web i wprowadź hello następującego adresu URL na podstawie portu hello, wprowadzonych w tunelu hello:

        http://localhost:8787/ 

10. Jesteś tooenter zostanie wyświetlony monit o hello SSH nazwy użytkownika i hasła tooconnect toohello klastra. Jeśli podczas tworzenia klastra hello jest używany klucz SSH, musi wprowadzić hasło hello, który został utworzony w kroku 5.

    ![Połącz tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Tworzenie tunelu SSH")

11. tootest czy hello instalacji programu RStudio zakończyło się pomyślnie, można uruchomić skrypt testu, który wykonuje R zadań MapReduce i Spark na powitania klastra. toodownload hello testu skryptu toorun w programu RStudio, przejdź wstecz toohello SSH konsoli i wprowadź hello następującego polecenia:

    *    Jeśli utworzono klastra usługi Hadoop z R, użyj tego polecenia:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Jeśli utworzono klaster Spark z R, użyj tego polecenia:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. W programu RStudio zobacz temat hello przetestować skrypt, który został pobrany. Kliknij dwukrotnie hello pliku tooopen, wybierz zawartość hello hello pliku, a następnie kliknij **Uruchom**. Powinny pojawić się dane wyjściowe hello w hello **konsoli** okienka:

   ![Testowanie instalacji hello](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "testowanie hello instalacji")

Innym rozwiązaniem byłoby tootype `source(testhdi.r)` lub `source(testhdi_spark.r)` tooexecute hello skryptu.

## <a name="see-also"></a>Zobacz też

* [Opcje kontekstu platformy R Server w klastrach HDInsight obliczania](hdinsight-hadoop-r-server-compute-contexts.md)
* [Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)

