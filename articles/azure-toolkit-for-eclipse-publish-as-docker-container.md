---
title: "zestaw narzędzi platformy Azure dla programu Eclipse hello aaaPublish kontener Docker przy użyciu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish tooMicrosoft aplikacji sieci web Azure jako kontener Docker przy użyciu hello zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publikowanie aplikacji sieci web jako kontener Docker przy użyciu hello Azure zestawu narzędzi dla programu Eclipse

Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web. Przy użyciu rozwiązania Docker kontenerów, deweloperzy umożliwiającej obsługę wszystkich plików projektu i zależności w jeden pakiet wdrażania tooa serwera. Witaj zestawu narzędzi platformy Azure dla programu Eclipse ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcje tooMicrosoft wdrożenia usługi Azure. W tym artykule przedstawiono toopublish wymagane kroki hello tooAzure Twojej aplikacji jako kontenery Docker.

> [!NOTE]
> Więcej informacji na temat rozwiązania Docker jest dostępna na powitania [Docker witryny sieci Web].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker

1. Otwórz projekt aplikacji sieci web w programie Eclipse.

2. Witaj toostart **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących hello:

   * W hello **Nawigator** wyświetlić, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**.

      ![Nawigator widoku Publikuj jako polecenia w kontenerze Docker][PUB01]

   * Na pasku narzędzi Eclipse hello, kliknij przycisk hello **publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**.

      ![Pasek narzędzi Eclipse Publikuj jako polecenia w kontenerze Docker][PUB02]
      
    Witaj **wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.

    ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB03]

3. W hello **wpisz nazwę obrazu, wybierz artefakt hello ścieżkę i sprawdź toobe hostów Docker, używane** oknie hello następujące:

    a. W hello **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker. (hello Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).

    b. Witaj **hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone. Wykonaj jedną z następujących hello:

    * Jeśli masz istniejącą hosta Docker można wdrażać tooit aplikacji sieci web.
    * Kliknij toocreate nowego hosta platformy Docker **Dodaj**.  
      
    Witaj **hostów Docker Utwórz** zostanie otwarte okno dialogowe.

    ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. W hello **skonfigurować nową maszynę wirtualną hello** okna, określ następujące opcje dla hosta Docker hello. (hello Kreator automatycznie generuje większość opcji hello można, ale można ich modyfikować.)

   a. **Nazwa**: wprowadź unikatową nazwę hosta Docker hello. (Jest taki sam, jak nazwa obrazu Docker określone wcześniej hello nie hello).

   b. **Subskrypcja**: Wprowadź hello subskrypcji platformy Azure, której użyjesz dla hosta.

   c. **Region**: Wprowadź hello region geograficzny, gdzie znajduje się na hoście.

   d. Na powitania **systemu operacyjnego hosta i rozmiar** karty:
     * **System operacyjny hosta**: Wprowadź hello systemu operacyjnego dla maszyny wirtualnej hello zawierający hosta.
     * **Rozmiar**: wprowadź rozmiar maszyn wirtualnych powitania dla hosta.

   e. Na powitania **grupy zasobów** karty:
     * **Nową grupę zasobów**: Utwórz nową grupę zasobów dla hosta.
     * **Istniejąca grupa zasobów**: Wprowadź istniejącą grupę zasobów z konta platformy Azure.

   f. Na powitania **sieci** karty:
     * **Nowa sieć wirtualna**: Utwórz nową sieć wirtualną dla hosta.
     * **Istniejącej sieci wirtualnej**: Wprowadź istniejącą sieć wirtualną z konta platformy Azure.

   g. Na powitania **magazynu** karty:
     * **Nowe konto magazynu**: Utwórz nowe konto magazynu dla hosta.
     * **Istniejące konto magazynu**: Wprowadź istniejącego konta magazynu z konta platformy Azure.

5. Kliknij przycisk **Dalej**.

6. W hello **skonfiguruj dziennika poświadczeń i ustawienia portu** okna, wybierz jedną z hello następujące opcje:

    * **Importuj poświadczeń z usługi Azure Key Vault**: Określa wcześniej zapisany zestaw poświadczeń, które są przechowywane w ramach subskrypcji platformy Azure.

      >[!NOTE]
      >Usługa Azure Key Vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, który współużytkuje hello subskrypcji. tooallow innego konta lub usługa główna toouse hello magazyn kluczy, należy użyć hello konta hello tooadd portalu Azure lub nazwy głównej usługi.

    * **Nowy dziennik poświadczenia**: tworzy nowy zestaw poświadczeń logowania. Jeśli wybierzesz tę opcję, hello następujące:
    
      * Na powitania **poświadczenia wirtualna** , wybierz pozycję Opcje jedną z następujących hello hello poświadczeń logowania do maszyn wirtualnych z hosta Docker:

          * **Nazwa użytkownika**: Wprowadź nazwę hello użytkownika o podanie poświadczeń logowania maszyny wirtualnej.
          * **Hasło** i **Potwierdź**: Wprowadź hasło hello poświadczenia logowania maszyny wirtualnej.
          * **SSH**: Wprowadź hello ustawienia protokołu Secure Shell (SSH) dla hosta Docker. Możesz wybrać hello następujące opcje:
            * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.
            * **Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.
            * **Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień SSH. katalog Hello musi zawierać hello następujące dwa pliki:
                * *id_rsa*: zawiera hello RSA identyfikacji użytkownika.
                * *id_rsa.pub*: zawiera hello klucza publicznego RSA, który jest używany do uwierzytelniania.
        
        ![Utwórz hosta Docker][PUB05]

      * Na powitania **Docker demon poświadczenia** karcie, określ hello następujące opcje:

          * **Port demon docker**: Wprowadź hello unikatowy port TCP dla hosta Docker.
          * **Zabezpieczeń TLS**: Wprowadź hello Transport Layer Security ustawienia dla hosta Docker. Możesz wybrać hello następujące opcje:
            * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia TLS.
            * **Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu TLS.
            * **Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień protokołu TLS. W szczególności katalog hello musi zawierać następujące pliki sześciu hello:
                * *CA.PEM* i *key.pem urzędu certyfikacji*: zawierają hello certyfikat i klucz publiczny dla hello TLS urzędu certyfikacji.
                * *CERT.PEM* i *key.pem*: zawierają hello certyfikatu klienta i klucz publiczny, który jest używany do uwierzytelniania protokołu TLS.
                * *Server.PEM* i *key.pem serwera*: zawierają hello certyfikat i klucz publiczny hello hosta.

        ![Utwórz hosta Docker][PUB06]

7. Po wprowadzeniu wszystkich hello poprzedzających informacji, kliknij przycisk **Zakończ**.

8. W hello **wdrożenia kontenera Docker na platformie Azure** kreatora, kliknij przycisk **dalej**.

   ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB07]

9. W hello **skonfigurować toobe kontenera Docker hello utworzony** oknie hello następujące:

   a. W hello **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.

   b. Wybierz jedną z hello następujące obrazy usługi Docker:
     * **Wstępnie zdefiniowane obrazu Docker**: Określa istniejącego obrazu platformy Docker na platformie Azure.

       >[!NOTE]
       >Witaj lista obrazy usługi Docker w tym polu zawiera kilka obrazów tego hello zestawu narzędzi platformy Azure został skonfigurowany toopatch tak, aby Twoje artefaktu zostanie wdrożona automatycznie.

     * **Niestandardowy plik Dockerfile**: Określa wcześniej zapisany plik Dockerfile z komputera lokalnego.

       >[!NOTE]
       >Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą toodeploy własny plik Dockerfile. Jednak to maksymalnie toodevelopers korzystającym z tooensure tej opcji, ich plik Dockerfile korzysta z wbudowanej poprawnie. Hello Azure Toolkit nie można zweryfikować zawartości hello niestandardowy plik Dockerfile tak hello wdrażania może się nie powieść, jeśli hello plik Dockerfile występują problemy. Ponadto hello Azure Toolkit oczekuje hello niestandardowy plik Dockerfile toocontain artefaktu aplikacji sieci web i będzie podejmować tooopen połączenia HTTP. Deweloperzy publikowania innego typu artefaktu, mogą otrzymywać nieszkodliwe błędy po wdrożeniu.

   c. **Ustawienia portów**: Wprowadź hello unikatowe TCP port powiązanie z kontenera Docker.

     ![Witaj Konfiguruj hello Docker kontenera toobe utworzone okno][PUB08]

10. Po wykonaniu wszystkich poprzednich krokach powitania kliknij **Zakończ**.

Hello Azure Toolkit rozpoczyna wdrażanie Twojego tooAzure aplikacji sieci web w kontenerze Docker. 

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

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].

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

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png