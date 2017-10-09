---
title: "aaaContinuous kompilacji i integracji aplikacji Linux Java sieci szkieletowej usług Azure przy użyciu Wpięć | Dokumentacja firmy Microsoft"
description: "Ciągła kompilacja i ciągłe integrowanie aplikacji Java w systemie Linux przy użyciu narzędzia Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Użyj toobuild Wpięć i wdrażanie aplikacji w języku Java systemu Linux
Jenkins to popularne narzędzie służące do przeprowadzania ciągłej integracji i ciągłego wdrażania aplikacji. Oto jak toobuild i wdrażania aplikacji sieci szkieletowej usług Azure przy użyciu Wpięć.

## <a name="general-prerequisites"></a>Ogólne wymagania wstępne
- Lokalnie zainstalowane narzędzie Git. Można zainstalować odpowiednią wersję Git hello z [hello Git pobiera strony](https://git-scm.com/downloads), oparte na systemie operacyjnym. W przypadku nowych tooGit Dowiedz się więcej o go z hello [dokumentacji Git](https://git-scm.com/docs).
- Ma hello wtyczki Wpięć sieci szkieletowej usług pod ręką. Możesz ją pobrać z [witryny pobierania usługi Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Konfigurowanie narzędzia Jenkins w ramach klastra usługi Service Fabric

Narzędzie Jenkins możesz skonfigurować wewnątrz klastra usługi Service Fabric lub poza nim. Witaj poniższych sekcjach przedstawiono Pokaż jak tooset go w klastrze podczas korzystania z usługi Azure storage konta toosave hello stan wystąpienia kontenera hello.

### <a name="prerequisites"></a>Wymagania wstępne
1. Przygotuj klaster systemu Linux usługi Service Fabric. Klaster sieci szkieletowej usług już utworzone na podstawie hello portalu Azure ma zainstalowany Docker. Jeśli korzystasz z klastra hello lokalnie, sprawdź, czy Docker jest zainstalowany za pomocą polecenia hello ``docker info``. Jeśli nie jest zainstalowany, zainstaluj go przy użyciu odpowiednio hello następujących poleceń:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Mają aplikacji kontenera usługi sieć szkieletowa hello wdrożone w klastrze hello za pomocą hello następujące kroki:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Należy hello połączyć opcję Szczegóły hello magazynu Azure udziałów plików, miejsce stanu hello toopersist hello Wpięć kontenera wystąpienia. Jeśli używasz portalu Microsoft Azure hello hello takie same, należy wykonaj kroki hello — Tworzenie konta magazynu platformy Azure, powiedz ``sfjenkinsstorage1``. Utwórz **udziału plików** na tym koncie magazynu powiedzieć ``sfjenkins``. Kliknij **Connect** dla hello hello udziału plików i zanotuj wartości wyświetlane w obszarze **łączących się z systemem Linux**, oznacza to będzie wyglądać następująco -
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Zaktualizuj hello symbole zastępcze w hello ```setupentrypoint.sh``` skryptu z odpowiednimi szczegółami magazyn azure.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Zastąp ``[REMOTE_FILE_SHARE_LOCATION]`` z wartością hello ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` z danych wyjściowych hello hello connect w punkcie 3 powyżej.
Zastąp ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` z wartością hello ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` od punktu 3 powyżej.

5. Połącz toohello klastra i zainstaluj hello kontenera aplikacji.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Instaluje kontenera Wpięć na powitania klastra, a można monitorować za pomocą hello Service Fabric Explorer.

### <a name="steps"></a>Kroki
1. W przeglądarce Przejdź zbyt``http://PublicIPorFQDN:8081``. Zawiera ścieżkę hello toosign wymagane jest hasło administratora początkowej hello w. Możesz kontynuować toouse Wpięć jako administrator. Lub możesz utworzyć i zmienić hello użytkownika, po zalogowaniu się przy użyciu konta administratora początkowej hello.

   > [!NOTE]
   > Upewnij się, że hello 8081 port jest określony jako port punktu końcowego aplikacji hello podczas tworzenia klastra hello.
   >

2. Uzyskiwanie Identyfikatora wystąpienia kontenera hello przy użyciu ``docker ps -a``.
3. Secure Shell (SSH) znak w kontenerze toohello i wklej ścieżkę hello, były wyświetlane w portalu Wpięć hello. Na przykład, jeśli w portalu hello zawiera ścieżkę hello `PATH_TO_INITIAL_ADMIN_PASSWORD`, uruchom następujące hello:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Konfigurowanie toowork GitHub z Wpięć, za pomocą kroków hello wspomnianego [generowanie klucza SSH i dodanie go agenta SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Użyj instrukcji hello klucza SSH hello toogenerate GitHub i tooadd hello SSH klucza toohello konto GitHub, który jest hostem repozytorium.
    * Uruchom polecenia hello wspomnianego hello poprzedzających łącze w hello Docker Wpięć powłoki (a nie na hoście).
    * toosign w toohello powłoki Wpięć z hosta, hello Użyj następującego polecenia:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Konfigurowanie narzędzia Jenkins poza klastrem usługi Service Fabric

Narzędzie Jenkins możesz skonfigurować wewnątrz klastra usługi Service Fabric lub poza nim. Witaj, jak następujące sekcje Pokaż tooset go poza klastrem.

### <a name="prerequisites"></a>Wymagania wstępne
Należy toohave Docker zainstalowane. Hello następujące polecenia mogą być używane tooinstall Docker z hello terminala:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Teraz po uruchomieniu ``docker info`` w terminalu hello, powinna zostać wyświetlona w danych wyjściowych hello tego hello Docker usługa jest uruchomiona.

### <a name="steps"></a>Kroki
  1. Ściąganie hello usługi sieć szkieletowa Wpięć kontener obrazu:``docker pull raunakpandya/jenkins:v1``
  2. Uruchom hello kontener obrazu:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Pobierz identyfikator hello hello kontener obrazu wystąpienia. Możesz wyświetlić listę wszystkich kontenerów Docker hello za pomocą polecenia hello``docker ps –a``
  4. Zaloguj się toohello Wpięć portalu przy użyciu hello następujące kroki:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Jeśli identyfikator kontenera to 2d24a73b5964, użyj wartości 2d24.
    * To hasło jest wymagane do podpisywania na pulpicie nawigacyjnym Wpięć toohello z portalu, który jest``http://<HOST-IP>:8080``
    * Po zalogowaniu do powitania po raz pierwszy, może utworzyć konta użytkownika i użyć jej do celów przyszłych lub konto administratora hello toouse można kontynuować. Po utworzeniu użytkownika należy toocontinue ze specyfikacją.
  5. Konfigurowanie toowork GitHub z Wpięć, za pomocą kroków hello wspomnianego [generowanie klucza SSH i dodanie go agenta SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Użyj instrukcji hello klucza SSH hello toogenerate GitHub i tooadd hello SSH klucza toohello konto GitHub, obsługujący hello repozytorium.
        * Uruchom polecenia hello wspomnianego hello poprzedzających łącze w hello Docker Wpięć powłoki (a nie na hoście).
      * toosign w toohello powłoki Wpięć z hosta, hello Użyj następującego polecenia:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Upewnij się, że hello klastra lub maszyny, gdzie hello Wpięć kontener obrazu jest hostowana zawiera adres IP publicznych. Dzięki temu hello Wpięć wystąpienia tooreceive powiadomienia z usługi GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Zainstaluj hello usługi sieć szkieletowa Wpięć wtyczki z portalu hello

1. Przejdź za``http://PublicIPorFQDN:8081``
2. Z poziomu pulpitu nawigacyjnego hello Wpięć wybierz **Zarządzanie Wpięć** > **Zarządzanie wtyczkami** > **zaawansowane**.
W tym miejscu możesz przekazać wtyczkę. Wybierz **wybierz plik**, a następnie wybierz hello **serviceFabric.hpi** pliku, który został pobrany w obszarze wymagania wstępne. Po wybraniu **przekazać**, Wpięć automatycznie instaluje program hello wtyczki. Zezwól na ponowne uruchomienie komputera, jeśli zostanie wyświetlony odpowiedni monit.

## <a name="create-and-configure-a-jenkins-job"></a>Tworzenie i konfigurowanie zadania narzędzia Jenkins

1. Utwórz **nowy element** z poziomu pulpitu nawigacyjnego.
2. Wprowadź nazwę elementu (na przykład **MyJob**). Wybierz pozycję **free-style project** (projekt w stylu dowolnym) i kliknij przycisk **OK**.
3. Przejdź do strony zadania hello, a następnie kliknij przycisk **Konfiguruj**.

   a. W sekcji Ogólne hello w obszarze **projektu GitHub**, określ adres URL projektu usługi GitHub. Ten adres URL hostów hello Java sieci szkieletowej usług aplikacji, które mają toointegrate z hello Wpięć ciągłej integracji, ciągłe wdrażanie (CI/CD) przepływu (na przykład ``https://github.com/sayantancs/SFJenkins``).

   b. W obszarze hello **zarządzania kodem źródłowym** zaznacz **Git**. Określ adres URL repozytorium hello obsługującego hello aplikacji Java sieci szkieletowej usług, które mają toointegrate z hello przepływu Wpięć CI/CD (na przykład ``https://github.com/sayantancs/SFJenkins.git``). Ponadto można określić w tym miejscu które toobuild gałęzi (na przykład **/wzorca**).
4. Konfigurowanie sieci *GitHub* (który jest hostem hello repozytorium) tak, aby mogli tootalk tooJenkins. Użyj hello następujące kroki:

   a. Przejdź na stronę repozytorium GitHub tooyour. Przejdź za**ustawienia** > **integracji i usług**.

   b. Wybierz **Dodaj usługę**, typ **Wpięć**i wybierz hello **wtyczki GitHub Wpięć**.

   c. Wprowadź adres URL elementu webhook narzędzia Jenkins (domyślnie adres URL powinien być następujący: ``http://<PublicIPorFQDN>:8081/github-webhook/``). Kliknij pozycję **add/update service** (dodaj/aktualizuj usługę).

   d. Zdarzenie testowe są wysyłane tooyour Wpięć wystąpienia. Powinny pojawić się zielonego znacznika wyboru przez element webhook hello w usłudze GitHub i projekt zostanie skompilowany.

   e. W obszarze hello **kompilacji wyzwalaczy** wybierz opcję kompilacji, które. Na przykład chcesz tootrigger kompilacji zawsze, gdy niektóre repozytorium toohello wypychania sytuacji. Dlatego wybierz pozycję **GitHub hook trigger for GITScm polling** (Wyzwalacz punktu zaczepienia GitHub na potrzeby sondowania GITScm). (Wcześniej, ta opcja została wywołana **kompilacji podczas zmiany spoczywa tooGitHub**.)

   f. W obszarze hello **kompilacji sekcji**, z listy rozwijanej hello **kroku kompilacji Dodaj**, wybierz opcję hello **wywołanie skryptu narzędzia Gradle**. W widget hello wchodzącej, określ ścieżkę hello zbyt**głównego kompilacji skryptu** aplikacji. Wybiera build.gradle z określonej ścieżki hello i odpowiednio działa. W przypadku utworzenia projektu o nazwie ``MyActor`` (przy użyciu hello generator wtyczki lub narzędzia Yeoman Eclipse) powinna zawierać hello głównego kompilacji skryptu ``${WORKSPACE}/MyActor``. Zobacz powitania po zrzut ekranu przedstawiający przykładowy to wygląda następująco:

    ![Akcja kompilacji narzędzia Jenkins w usłudze Service Fabric][build-step]

   g. Z hello **akcje Postkompilacyjnego** listy rozwijanej, wybierz pozycję **wdrażanie projektu sieci szkieletowej usług**. W tym miejscu należy tooprovide klastra, który będzie można wdrożyć szczegółów, w którym hello Wpięć skompilowane aplikacji usługi Service Fabric. Można też podać szczegóły dodatkowych aplikacji używanych aplikacji hello toodeploy. Zobacz powitania po zrzut ekranu przedstawiający przykładowy to wygląda następująco:

    ![Akcja kompilacji narzędzia Jenkins w usłudze Service Fabric][post-build-step]

   > [!NOTE]
   > tutaj Hello klastra może być taka sama jak hello jeden hello hostingu Wpięć aplikacji kontenera, w przypadku korzystania z usługi Service Fabric toodeploy hello Wpięć kontener obrazu.
   >

## <a name="next-steps"></a>Następne kroki
Usługa GitHub i narzędzie Jenkins są teraz skonfigurowane. Należy rozważyć zmianę niektóre przykładowe zmiany w Twojej ``MyActor`` projektu w przykładzie repozytorium hello https://github.com/sayantancs/SFJenkins. Wypychanie tooa Twoje zmiany zdalnego ``master`` gałęzi (lub skonfigurowanego toowork z działu). Spowoduje to zainicjowanie zadania Wpięć hello ``MyJob``, który został skonfigurowany. Pobiera hello zmiany z usługi GitHub, ich tworzenia i wdraża hello toohello klastra punkt końcowy aplikacji określonej w akcji po kompilacji.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
