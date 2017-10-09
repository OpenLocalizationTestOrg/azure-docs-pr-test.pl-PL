---
title: "aaaPublish kontener Docker przy użyciu hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish tooMicrosoft aplikacji sieci web Azure jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publikowanie aplikacji sieci web jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ

Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web. Przy użyciu rozwiązania Docker kontenerów, deweloperzy umożliwiającej obsługę wszystkich plików projektu i zależności w jeden pakiet wdrażania tooa serwera. Hello Azure Toolkit for IntelliJ ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcje tooMicrosoft wdrożenia usługi Azure. W tym artykule przedstawiono toopublish wymagane kroki hello tooAzure Twojej aplikacji jako kontenery Docker.

> [!NOTE]
>
> Więcej informacji na temat rozwiązania Docker jest dostępna na powitania [Docker witryny sieci Web].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker

> [!NOTE]
> * toopublish aplikacji sieci web, należy utworzyć artefaktu gotowe do wdrożenia. toolearn więcej, zobacz hello [dodatkowe informacje na temat tworzenia artefaktów](#artifacts) sekcji.
>
> * Po ukończeniu Kreatora wdrażania hello co najmniej raz, po uruchomieniu kreatora hello ponownie większość ustawień są używane jako domyślne.
>

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

2. Witaj toostart **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących hello:

   * W hello **projektu** okna narzędzia, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**:

      ![Publikuj jako polecenia w kontenerze Docker Hello][PUB01]

   * Na pasku narzędzi IntelliJ hello, kliknij przycisk hello **grupy publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**:

      ![Publikuj jako polecenia w kontenerze Docker Hello][PUB02]  
    Witaj **wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.

   ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB03]

3. W hello **wpisz nazwę obrazu, wybierz artefakt hello ścieżkę i sprawdź toobe hostów Docker, używane** oknie hello następujące: 

   a. W hello **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker. (hello Kreator automatycznie tworzy nazwę, ale można go zmodyfikować). 

   b. Witaj **hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone. Wykonaj jedną z następujących hello: 
      * Jeśli masz istniejącą hosta Docker można wdrażać tooit aplikacji sieci web.
      * toocreate Docker hosta, kliknij znak plus hello zielony (**+**).  
       Witaj **hostów Docker Utwórz** zostanie otwarte okno dialogowe. 

      ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. W hello **skonfigurować nową maszynę wirtualną hello** okna, podaj następujące informacje o hoście Docker hello. (hello Kreator automatycznie generuje większość hello informacje dla Ciebie, ale można ich modyfikować.) 

   a. W hello **nazwa** wprowadź unikatową nazwę hosta Docker hello. (Jest taki sam, jak nazwa obrazu Docker określone wcześniej hello nie hello). 
    
   b. W hello **subskrypcji** wprowadź hello subskrypcji platformy Azure, której użyjesz dla hosta. 
      
   c. W hello **Region** wprowadź hello region geograficzny, gdzie znajduje się na hoście.
      
   d. Na powitania **systemu operacyjnego i rozmiar** pozycję hello następujące:      
      * **System operacyjny hosta**: Wprowadź hello systemu operacyjnego dla maszyny wirtualnej hello zawierający hosta. 
      * **Rozmiar**: wprowadź rozmiar maszyn wirtualnych powitania dla hosta.   
       
   e. Na powitania **grupy zasobów** , a następnie wybierz jedną z następujących hello:      
      * **Nową grupę zasobów**: Utwórz grupę zasobów dla hosta.
      * **Istniejąca grupa zasobów**: Określ istniejącą grupę zasobów z konta platformy Azure. 
       
   f. Na powitania **sieci** , a następnie wybierz jedną z następujących hello:      
      * **Nowa sieć wirtualna**: tworzenie sieci wirtualnej dla hosta.
      * **Istniejącej sieci wirtualnej**: Określ istniejącej sieci wirtualnej z konta platformy Azure. 
       
   g. Na powitania **magazynu** , a następnie wybierz jedną z następujących hello:      
      * **Nowe konto magazynu**: Tworzenie konta magazynu dla hosta.
      * **Istniejące konto magazynu**: określenie istniejącego konta magazynu z konta platformy Azure.
       
5. Kliknij przycisk **Dalej**.  
     Witaj **skonfiguruj dziennika poświadczeń i ustawienia portu** zostanie otwarte okno.

      ![Hello dziennika Konfigurowanie poświadczeń i ustawienia portu][PUB05]

6. Wybierz jedną z hello następujące opcje:

      * **Importuj poświadczeń z usługi Azure Key Vault**: Określ wcześniej zapisany zestaw poświadczeń, które są przechowywane w Twojej subskrypcji platformy Azure.

          > [!NOTE]
          > Usługi Azure key vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, który współużytkuje hello subskrypcji. tooallow innego konta lub usługi klucza podmiotu zabezpieczeń toouse w hello magazynu, należy użyć hello konta hello tooadd portalu Azure lub nazwy głównej usługi.

      * **Nowy dziennik poświadczenia**: Tworzenie nowego zestawu poświadczeń logowania. Jeśli wybierzesz tę opcję, hello następujące:

        a. Na powitania **wirtualna poświadczenia** karcie, podaj następujące informacje dla poświadczeń logowania do maszyn wirtualnych hello hosta Docker hello: * **Username**: Wprowadź nazwę użytkownika hello logowania z maszyn wirtualnych poświadczenia.
             * **Hasło** i **Potwierdź**: Wprowadź hasło hello o podanie poświadczeń logowania do maszyn wirtualnych.
             * **SSH**: Wprowadź hello ustawienia protokołu Secure Shell (SSH) dla hosta Docker. Można wybrać jedną z hello następujące opcje: * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.
                * **Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.
                * **Importuj z katalogu**: pozwala toospecify katalogu, który zawiera zestaw wcześniej zapisanych ustawień SSH. katalog Hello musi zawierać hello następujące dwa pliki:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. Na powitania **Docker demon dostępu** karcie, podaj hello następujących informacji:

          ![Utwórz hosta Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Po wprowadzeniu hello wymaganych informacji, kliknij przycisk **Zakończ**.  
    Witaj **wdrożenia kontenera Docker na platformie Azure** kreatora pojawi się ponownie.

   ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB07]

8. Kliknij przycisk **Dalej**.  
    Witaj **skonfigurować toobe kontenera Docker hello utworzony** zostanie otwarte okno.

   ![Witaj Konfiguruj hello Docker kontenera toobe utworzone okno][PUB08]

9. W hello **skonfigurować toobe kontenera Docker hello utworzony** okna, podaj hello następujących informacji: 

   a. W hello **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.

   b. Wybierz jedną z hello następujące obrazy usługi Docker: 

      * **Wstępnie zdefiniowane obrazu Docker**: Określ istniejącego obrazu platformy Docker na platformie Azure. 

        > [!NOTE]
        > Witaj lista obrazy usługi Docker w tym polu zawiera kilka obrazów tego hello zestawu narzędzi platformy Azure został skonfigurowany toopatch tak, aby Twoje artefaktu zostanie wdrożona automatycznie. 

      * **Niestandardowy plik Dockerfile**: Określ wcześniej zapisany plik Dockerfile z komputera lokalnego.

        > [!NOTE]
        > Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą toodeploy własny plik Dockerfile. Jednak to maksymalnie toodevelopers korzystającym z tooensure tej opcji, ich plik Dockerfile korzysta z wbudowanej poprawnie. Ponieważ hello Azure Toolkit nie można zweryfikować zawartości hello niestandardowy plik Dockerfile, hello wdrażania może się nie powieść Jeśli hello plik Dockerfile występują problemy. Ponadto ponieważ hello Azure Toolkit oczekuje hello niestandardowy plik Dockerfile toocontain artefaktu aplikacji sieci web, podejmuje tooopen połączenia HTTP. Deweloperzy publikowania innego typu artefaktu, otrzymają może nieszkodliwe błędy po wdrożeniu.

   c. W hello **ustawienia portu** wprowadź hello unikatowe TCP port powiązanie z kontenera Docker. 

10. Po wykonaniu poprzednich krokach hello, kliknij przycisk **Zakończ**. 

Hello Azure Toolkit rozpoczyna wdrażanie Twojego tooAzure aplikacji sieci web w kontenerze Docker. Jeśli nie skonfigurowano wdrożone w tle hello toobe IntelliJ **wdrażanie tooAzure** zostanie wyświetlony pasek postępu. 

![pasek postępu wdrożenia Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Dodatkowe informacje na temat tworzenia artefaktów

toocreate artefaktu gotowe do wdrożenia, hello następujące:

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

2. Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.

   ![Witaj polecenia struktury projektu][ART01]

3. tooadd jako artefaktu, kliknij znak plus hello zielony (**+**), a następnie kliknij przycisk **aplikacji sieci Web: archiwum**.

   ![polecenie "Archiwum: aplikacja sieci Web" Hello][ART02]

4. W hello **nazwa** wprowadź nazwę użytkownika artefaktu (nie dołączaj hello *.war* rozszerzenia), a następnie kliknij przycisk **OK**.

   ![pole Nazwa Hello artefaktów][ART03]

Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na powitania JetBrains witryny sieci Web.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [What's new in hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

Aby uzyskać dodatkowe zasoby dla Docker, zobacz oficjalne hello [Docker witryny sieci Web].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Docker witryny sieci Web]: https://www.docker.com/
[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
