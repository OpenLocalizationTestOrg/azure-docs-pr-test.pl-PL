---
title: "Publikowanie kontenera Docker przy użyciu zestawu narzędzi Azure for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikację sieci web do systemu Microsoft Azure jako kontener Docker za pomocą narzędzi Azure for IntelliJ."
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
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publikowanie aplikacji sieci web jako kontener Docker przy użyciu zestawu narzędzi Azure for IntelliJ

Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web. Przy użyciu rozwiązania Docker kontenerów, deweloperzy mogą konsolidację wszystkie pliki projektu i zależności w jeden pakiet do wdrożenia na serwerze. Zestaw narzędzi platformy Azure dla IntelliJ ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcji dla wdrożenia do systemu Microsoft Azure. W tym artykule przedstawiono kroki wymagane do publikowania aplikacji na platformie Azure jako kontenery Docker.

> [!NOTE]
>
> Więcej informacji na temat rozwiązania Docker jest dostępna na [Docker witryny sieci Web].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker

> [!NOTE]
> * Aby opublikować aplikację sieci web, należy utworzyć artefaktu gotowe do wdrożenia. Aby dowiedzieć się więcej, zobacz [dodatkowe informacje na temat tworzenia artefaktów](#artifacts) sekcji.
>
> * Po ukończeniu Kreatora wdrażania co najmniej raz, większość ustawień są używane jako domyślne podczas uruchom kreatora ponownie.
>

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

2. Aby uruchomić **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących czynności:

   * W **projektu** okna narzędzia, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**:

      ![Publikuj jako polecenia w kontenerze Docker][PUB01]

   * Kliknij na pasku narzędzi IntelliJ **grupy publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**:

      ![Publikuj jako polecenia w kontenerze Docker][PUB02]  
    **Wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.

   ![Kontener Docker wdrażanie w Kreatorze Azure][PUB03]

3. W **wpisz nazwę obrazu, wybierz artefakt ścieżkę i sprawdź Docker hosta do użycia** okna, wykonaj następujące czynności: 

   a. W **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker. (Kreator automatycznie tworzy nazwę, ale można go zmodyfikować). 

   b. **Hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone. Wykonaj jedną z następujących czynności: 
      * Jeśli masz istniejącą hosta Docker można wdrożyć aplikację sieci web do niego.
      * Aby utworzyć hostów Docker, kliknij zielony znak plus (**+**).  
       **Hostów Docker Utwórz** zostanie otwarte okno dialogowe. 

      ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. W **skonfigurować nową maszynę wirtualną** okna, podaj następujące informacje o hoście Docker. (Kreator automatycznie generuje większość informacji dla Ciebie, ale można ich modyfikować.) 

   a. W **nazwa** wprowadź unikatową nazwę hosta Docker. (Go nie jest taka sama jak nazwa obrazu Docker określone wcześniej.) 
    
   b. W **subskrypcji** wprowadź subskrypcji platformy Azure, której użyjesz dla hosta. 
      
   c. W **Region** wprowadź region geograficzny, w którym znajduje się na hoście.
      
   d. Na **systemu operacyjnego i rozmiar** karcie, wykonaj następujące czynności:      
      * **System operacyjny hosta**: Wprowadź system operacyjny dla maszyny wirtualnej, która zawiera hosta. 
      * **Rozmiar**: wprowadź rozmiar maszyn wirtualnych dla hosta.   
       
   e. Na **grupy zasobów** , a następnie wybierz jedną z następujących czynności:      
      * **Nową grupę zasobów**: Utwórz grupę zasobów dla hosta.
      * **Istniejąca grupa zasobów**: Określ istniejącą grupę zasobów z konta platformy Azure. 
       
   f. Na **sieci** , a następnie wybierz jedną z następujących czynności:      
      * **Nowa sieć wirtualna**: tworzenie sieci wirtualnej dla hosta.
      * **Istniejącej sieci wirtualnej**: Określ istniejącej sieci wirtualnej z konta platformy Azure. 
       
   g. Na **magazynu** , a następnie wybierz jedną z następujących czynności:      
      * **Nowe konto magazynu**: Tworzenie konta magazynu dla hosta.
      * **Istniejące konto magazynu**: określenie istniejącego konta magazynu z konta platformy Azure.
       
5. Kliknij przycisk **Dalej**.  
     **Skonfiguruj dziennika poświadczeń i ustawienia portu** zostanie otwarte okno.

      ![Dziennika Konfigurowanie poświadczeń i ustawienia portu][PUB05]

6. Wybierz jedną z następujących opcji:

      * **Importuj poświadczeń z usługi Azure Key Vault**: Określ wcześniej zapisany zestaw poświadczeń, które są przechowywane w Twojej subskrypcji platformy Azure.

          > [!NOTE]
          > Usługi Azure key vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, które współużytkują subskrypcji. Aby umożliwić głównych do używania magazynu kluczy innego konta lub usługi, musi użyć portalu Azure, aby dodać konto lub nazwy głównej usługi.

      * **Nowy dziennik poświadczenia**: Tworzenie nowego zestawu poświadczeń logowania. Jeśli wybierzesz tę opcję, wykonaj następujące czynności:

        a. Na **poświadczenia wirtualna** karcie, podaj następujące informacje dotyczące poświadczeń logowania do maszyn wirtualnych z hosta Docker: * **Username**: Wprowadź nazwę użytkownika dla nazwy logowania użytkownika maszyny wirtualnej poświadczenia.
             * **Hasło** i **Potwierdź**: Wprowadź hasło dla poświadczeń logowania do maszyn wirtualnych.
             * **SSH**: Wprowadź ustawienia protokołu Secure Shell (SSH) dla hosta Docker. Można wybrać jedną z następujących opcji: * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.
                * **Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.
                * **Importuj z katalogu**: można określić katalogu, który zawiera zestaw wcześniej zapisanych ustawień SSH. Katalog musi zawierać następujące dwa pliki:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Na **Docker demon dostępu** karcie, podaj następujące informacje:

          ![Utwórz hosta Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Po wprowadzeniu wymaganych informacji kliknij **Zakończ**.  
    **Wdrożenia kontenera Docker na platformie Azure** kreatora pojawi się ponownie.

   ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB07]

8. Kliknij przycisk **Dalej**.  
    **Skonfigurować w celu utworzenia kontenera Docker** zostanie otwarte okno.

   ![Konfiguruj kontenera Docker można utworzyć okna][PUB08]

9. W **skonfigurować w celu utworzenia kontenera Docker** okna, podaj następujące informacje: 

   a. W **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.

   b. Wybierz jedną z poniższych ilustracjach Docker: 

      * **Wstępnie zdefiniowane obrazu Docker**: Określ istniejącego obrazu platformy Docker na platformie Azure. 

        > [!NOTE]
        > Lista obrazy usługi Docker w tym polu zawiera kilka obrazów, które zestawu narzędzi platformy Azure został skonfigurowany do stosowania poprawek, aby Twoje artefaktu zostanie wdrożona automatycznie. 

      * **Niestandardowy plik Dockerfile**: Określ wcześniej zapisany plik Dockerfile z komputera lokalnego.

        > [!NOTE]
        > Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą wdrożyć własny plik Dockerfile. Jednak jest deweloperzy, którzy używają tę opcję, aby upewnić się, że ich plik Dockerfile jest poprawnie zbudowany. Ponieważ zestaw narzędzi platformy Azure nie można zweryfikować zawartości niestandardowy plik Dockerfile, wdrożenie może się nie powieść, jeśli plik Dockerfile występują problemy. Ponadto ponieważ zestaw narzędzi Azure oczekuje niestandardowy plik Dockerfile zawiera artefaktu aplikacji sieci web, próbuje otworzyć połączenie HTTP. Deweloperzy publikowania innego typu artefaktu, otrzymają może nieszkodliwe błędy po wdrożeniu.

   c. W **ustawienia portu** wprowadź unikatowe powiązanie port TCP dla Twojego kontenera Docker. 

10. Po wykonaniu powyższych kroków, kliknij przycisk **Zakończ**. 

Zestaw narzędzi Azure rozpoczyna wdrażanie aplikacji sieci web na platformie Azure w kontenerze Docker. Jeśli nie skonfigurowano IntelliJ wdrażanych w tle, **wdrażanie na platformie Azure** zostanie wyświetlony pasek postępu. 

![Pasek postępu wdrożenia][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Dodatkowe informacje na temat tworzenia artefaktów

Aby utworzyć artefaktu gotowe do wdrożenia, wykonaj następujące czynności:

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

2. Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.

   ![Polecenie struktury projektu][ART01]

3. Aby dodać artefaktu, kliknij zielony znak plus (**+**), a następnie kliknij przycisk **aplikacji sieci Web: archiwum**.

   ![Polecenie "Archiwum sieci Web aplikacji:"][ART02]

4. W **nazwa** wprowadź nazwę użytkownika artefaktu (nie dołączaj *.war* rozszerzenia), a następnie kliknij przycisk **OK**.

   ![Pole Nazwa artefaktów][ART03]

Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na JetBrains witryny sieci Web.

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

Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).

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

[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/
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
