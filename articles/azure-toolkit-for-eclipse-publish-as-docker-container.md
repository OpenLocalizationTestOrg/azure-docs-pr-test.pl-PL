---
title: "Publikowanie kontenera Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikację sieci web do systemu Microsoft Azure jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publikowanie aplikacji sieci web jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse

Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web. Przy użyciu rozwiązania Docker kontenerów, deweloperzy mogą konsolidację wszystkie pliki projektu i zależności w jeden pakiet do wdrożenia na serwerze. Zestaw narzędzi platformy Azure dla programu Eclipse ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcji dla wdrożenia do systemu Microsoft Azure. W tym artykule przedstawiono kroki wymagane do publikowania aplikacji na platformie Azure jako kontenery Docker.

> [!NOTE]
> Więcej informacji na temat rozwiązania Docker jest dostępna na [Docker witryny sieci Web].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker

1. Otwórz projekt aplikacji sieci web w programie Eclipse.

2. Aby uruchomić **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących czynności:

   * W **Nawigator** wyświetlić, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**.

      ![Nawigator widoku Publikuj jako polecenia w kontenerze Docker][PUB01]

   * Na pasku narzędzi Eclipse kliknij **publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**.

      ![Pasek narzędzi Eclipse Publikuj jako polecenia w kontenerze Docker][PUB02]
      
    **Wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.

    ![Kontener Docker wdrażanie w Kreatorze Azure][PUB03]

3. W **wpisz nazwę obrazu, wybierz artefakt ścieżkę i sprawdź Docker hosta do użycia** okna, wykonaj następujące czynności:

    a. W **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker. (Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).

    b. **Hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone. Wykonaj jedną z następujących czynności:

    * Jeśli masz istniejącą hosta Docker można wdrożyć aplikację sieci web do niego.
    * Aby utworzyć nowy host platformy Docker, kliknij przycisk **Dodaj**.  
      
    **Hostów Docker Utwórz** zostanie otwarte okno dialogowe.

    ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. W **skonfigurować nową maszynę wirtualną** okna, określ następujące opcje dla hosta Docker. (Kreator automatycznie generuje większość opcji dla Ciebie, ale można ich modyfikować.)

   a. **Nazwa**: wprowadź unikatową nazwę hosta Docker. (Go nie jest taka sama jak nazwa obrazu Docker określone wcześniej.)

   b. **Subskrypcja**: Wprowadź subskrypcji platformy Azure, której użyjesz dla hosta.

   c. **Region**: Wprowadź region geograficzny, w którym znajduje się na hoście.

   d. Na **systemu operacyjnego hosta i rozmiar** karty:
     * **System operacyjny hosta**: Wprowadź system operacyjny dla maszyny wirtualnej, która zawiera hosta.
     * **Rozmiar**: wprowadź rozmiar maszyn wirtualnych dla hosta.

   e. Na **grupy zasobów** karty:
     * **Nową grupę zasobów**: Utwórz nową grupę zasobów dla hosta.
     * **Istniejąca grupa zasobów**: Wprowadź istniejącą grupę zasobów z konta platformy Azure.

   f. Na **sieci** karty:
     * **Nowa sieć wirtualna**: Utwórz nową sieć wirtualną dla hosta.
     * **Istniejącej sieci wirtualnej**: Wprowadź istniejącą sieć wirtualną z konta platformy Azure.

   g. Na **magazynu** karty:
     * **Nowe konto magazynu**: Utwórz nowe konto magazynu dla hosta.
     * **Istniejące konto magazynu**: Wprowadź istniejącego konta magazynu z konta platformy Azure.

5. Kliknij przycisk **Dalej**.

6. W **skonfiguruj dziennika poświadczeń i ustawienia portu** okna, wybierz jedną z następujących opcji:

    * **Importuj poświadczeń z usługi Azure Key Vault**: Określa wcześniej zapisany zestaw poświadczeń, które są przechowywane w ramach subskrypcji platformy Azure.

      >[!NOTE]
      >Usługa Azure Key Vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, które współużytkują subskrypcji. Aby umożliwić podmiotu zabezpieczeń do użycia usługi Key Vault innego konta lub usługi, musi użyć portalu Azure i Dodaj konto lub nazwy głównej usługi.

    * **Nowy dziennik poświadczenia**: tworzy nowy zestaw poświadczeń logowania. Jeśli wybierzesz tę opcję, wykonaj następujące czynności:
    
      * Na **poświadczenia wirtualna** , wybierz pozycję jedną z następujących opcji z poświadczeniami logowania maszyn wirtualnych na hoście Docker:

          * **Nazwa użytkownika**: Wprowadź nazwę użytkownika o podanie poświadczeń logowania maszyny wirtualnej.
          * **Hasło** i **Potwierdź**: Wprowadź hasło dla poświadczeń logowania maszyny wirtualnej.
          * **SSH**: Wprowadź ustawienia protokołu Secure Shell (SSH) dla hosta Docker. Możesz wybrać spośród następujących opcji:
            * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.
            * **Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.
            * **Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień SSH. Katalog musi zawierać następujące dwa pliki:
                * *id_rsa*: zawiera identyfikator RSA dla użytkownika.
                * *id_rsa.pub*: zawiera klucza publicznego RSA, który jest używany do uwierzytelniania.
        
        ![Utwórz hosta Docker][PUB05]

      * Na **Docker demon poświadczenia** karcie, określ następujące opcje:

          * **Port demon docker**: wprowadź unikatowy port TCP dla hosta Docker.
          * **Zabezpieczeń TLS**: Wprowadź ustawienia Transport Layer Security dla platformy Docker hosta. Możesz wybrać spośród następujących opcji:
            * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia TLS.
            * **Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu TLS.
            * **Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień protokołu TLS. W szczególności katalogu musi zawierać następujące pliki sześć:
                * *CA.PEM* i *key.pem urzędu certyfikacji*: zawiera certyfikat i klucz publiczny certyfikatu urzędu certyfikacji TLS.
                * *CERT.PEM* i *key.pem*: zawierają certyfikat klienta i klucz publiczny, który jest używany do uwierzytelniania protokołu TLS.
                * *Server.PEM* i *key.pem serwera*: zawierają certyfikat i klucz publiczny dla hosta.

        ![Utwórz hosta Docker][PUB06]

7. Po wprowadzeniu wszystkich powyższych informacji, kliknij przycisk **Zakończ**.

8. W **wdrożenia kontenera Docker na platformie Azure** kreatora, kliknij przycisk **dalej**.

   ![Kontener Docker wdrażanie w Kreatorze Azure][PUB07]

9. W **skonfigurować w celu utworzenia kontenera Docker** okna, wykonaj następujące czynności:

   a. W **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.

   b. Wybierz jedną z poniższych ilustracjach Docker:
     * **Wstępnie zdefiniowane obrazu Docker**: Określa istniejącego obrazu platformy Docker na platformie Azure.

       >[!NOTE]
       >Lista obrazy usługi Docker w tym polu zawiera kilka obrazów, które zestawu narzędzi platformy Azure został skonfigurowany do stosowania poprawek, aby Twoje artefaktu zostanie wdrożona automatycznie.

     * **Niestandardowy plik Dockerfile**: Określa wcześniej zapisany plik Dockerfile z komputera lokalnego.

       >[!NOTE]
       >Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą wdrożyć własny plik Dockerfile. Jednak jest deweloperzy, którzy używają tę opcję, aby upewnić się, że ich plik Dockerfile jest poprawnie zbudowany. Zestaw narzędzi platformy Azure nie można zweryfikować zawartości niestandardowy plik Dockerfile, wdrożenie może się nie powieść, jeśli plik Dockerfile występują problemy. Ponadto zestaw narzędzi Azure oczekuje niestandardowy plik Dockerfile zawiera artefaktu aplikacji sieci web i będzie podejmować próby otwarcia połączenia HTTP. Deweloperzy publikowania innego typu artefaktu, mogą otrzymywać nieszkodliwe błędy po wdrożeniu.

   c. **Ustawienia portów**: Wprowadź unikatowe powiązanie port TCP dla Twojego kontenera Docker.

     ![Konfiguruj kontenera Docker można utworzyć okna][PUB08]

10. Po wykonaniu wszystkich poprzednich kroków, kliknij przycisk **Zakończ**.

Zestaw narzędzi Azure rozpoczyna wdrażanie aplikacji sieci web na platformie Azure w kontenerze Docker. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Nowości w zestawie narzędzi programu Azure dla programu Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * [Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Nowości w zestawie narzędzi programu Azure for IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].

Aby uzyskać dodatkowe zasoby dla Docker można znaleźć w oficjalnej [Docker witryny sieci Web].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

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