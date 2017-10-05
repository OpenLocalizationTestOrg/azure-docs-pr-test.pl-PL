---
title: "Publikowania aplikacji rozruchu Spring jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla IntelliJ | Dokumentacja firmy Microsoft"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publikowania aplikacji rozruchu Spring jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla IntelliJ

[Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jeden z popularnych więcej projektów, które jest wbudowane znajdujący się na platformy jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.

[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.

Ten samouczek przedstawia kroki wdrażania aplikacji rozruchu Spring jako kontener Docker do systemu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Sklonuj repozytorium Docker rozruchu Spring domyślne

W poniższych krokach objaśniono przez klonowanie repozytorium Spring Docker rozruch przy użyciu IntelliJ. Jeśli chcesz użyć wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].

1. Otwórz środowisko IntelliJ.

1. Na ekranie powitalnym zaznacz **GitHub** opcji **wyewidencjonowania z kontroli wersji** listy.

   ![Opcja GitHub kontroli wersji][CL01]

1. Jeśli zostanie wyświetlony monit, aby się zalogować, wprowadź swoje poświadczenia.

   * Jeśli używane są nazwy użytkownika i hasła do logowania witrynie GitHub:

      ![Okno dialogowe wprowadzanie GitHub nazwy użytkownika i hasła][CL02a]

   * Jeśli używasz tokenu do logowania witrynie GitHub:

      ![Okno dialogowe wprowadzanie GitHub token][CL02b]

1. Wprowadź **https://github.com/spring-guides/gs-spring-boot-docker.git** dla adresu URL repozytorium, określ informacje o Twoich ścieżka lokalna i folder, a następnie kliknij przycisk **klonowania**.

   ![Okno dialogowe klonowanie repozytorium][CL03]

1. Po wyświetleniu monitu, aby utworzyć projekt IntelliJ, wybierz **nr**.

   ![Odrzucanie do tworzenia projektu IntelliJ][CL04]

1. Na stronie powitalnej kliknij **Importowanie projektu**.

   ![Wybór projektu importu][CL05]

1. Znajdź ścieżki, gdzie sklonować repozytorium Spring rozruchu, wybierz **pełną** folderu głównego, a następnie kliknij przycisk **OK**.

   ![Wybierz folder do zaimportowania][CL06]

1. Po wyświetleniu monitu wybierz **Tworzenie projektu z istniejących źródeł**.

   ![Opcję, aby utworzyć projekt z istniejących źródeł][CL07]

1. Określ nazwę projektu lub zaakceptuj wartość domyślną, Sprawdź poprawną ścieżkę do **pełną** folder, a następnie kliknij przycisk **dalej**.

   ![Określ nazwę projektu][CL08]

1. Dostosowywanie wszelkich katalogów do zaimportowania, a następnie kliknij przycisk **dalej**.

   ![Wybierz katalogów][CL09]

1. Przegląd biblioteki do zaimportowania, a następnie kliknij przycisk **dalej**.

   ![Przegląd biblioteki projektu][CL10]

1. Przejrzyj struktury modułu, a następnie kliknij przycisk **dalej**.

   ![Przejrzyj struktury modułu][CL11]

1. Określ użytkownika JDK, a następnie kliknij przycisk **dalej**.

   ![Określ JDK][CL12]

1. Kliknij przycisk **Zakończ**.

   ![Przycisk Zakończ][CL13]

IntelliJ importuje aplikacji rozruchu Spring jako projekt i wyświetla strukturę po zakończeniu importowania.

![Spring aplikacji rozruchu w IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Tworzenie rozruchowych Spring aplikacji

### <a name="build-the-app-by-using-the-maven-pom"></a>Tworzenie aplikacji przy użyciu Maven POM

1. Otwórz okno narzędzia Maven, jeśli nie jest już otwarty. Kliknij przycisk **widoku** > **narzędzia systemu Windows** > **projekty Maven**.

   ![Polecenia narzędzia Windows i projekty Maven][BU01]

1. W oknie narzędzia Maven, kliknij prawym przyciskiem myszy **pakietu** i wybierz **Uruchom kompilacja Maven**. (Jeśli projekt Maven nie występuje automatycznie, kliknij przycisk **ponownie zaimportować** ikonę na pasku narzędzi Maven.)

   ![Uruchom polecenie kompilacja Maven][BU02]

1. Powinna zostać wyświetlona IntelliJ **BUDOWANIE powiodło** podczas rozruchu Spring aplikacji został utworzony pomyślnie.

   ![Komunikat BUDOWANIE powiodło się][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Tworzenie artefaktu gotowe do wdrożenia

Aby opublikować aplikację Spring rozruchu, należy utworzyć artefaktu gotowe do wdrożenia. Wykonaj następujące czynności:

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

1. Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.

   ![Struktura projekt — polecenie][ART01]

1. Kliknij zielony plus (**+**) symbolu, aby dodać artefaktu, kliknij polecenie **JAR**, a następnie kliknij przycisk **pusty**.

   ![Dodaj artefaktów][ART02]

1. Nazwa użytkownika artefaktu pamiętając nie można dodać rozszerzenia "JAR", a następnie określ folder docelowy dla danych wyjściowych Maven.

   ![Określ właściwości artefaktów][ART03]

1. Tworzenie manifestu dla Twojego artefaktu (opcjonalnie):

   a. Kliknij przycisk **tworzenie manifestu**.

      ![Kliknij przycisk Utwórz manifestu][ART04a]

   b. Wybierz domyślną ścieżkę dla artefaktu, a następnie kliknij przycisk **OK**.

      ![Określ ścieżkę artefaktów][ART04b]

   c. Kliknij przycisk wielokropka (**...** ) można znaleźć klasy głównym.

      ![Zlokalizuj klasy głównym][ART04c]

   d. Wybierz klasy głównym, a następnie kliknij przycisk **OK**.

      ![Określ klasy głównym][ART04d]

1. Kliknij przycisk **OK**.

   ![Zamknij okno dialogowe struktury projektu][ART05]

> [!NOTE]
> Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na JetBrains witryny sieci Web.
>

### <a name="build-the-artifact-for-deployment"></a>Tworzenie artefaktu dla wdrożenia

1. Kliknij przycisk **kompilacji**, a następnie kliknij przycisk **artefakty**.

   ![Polecenie artefaktów kompilacji][BU04]

1. Gdy **artefaktów kompilacji** zostanie wyświetlone menu kontekstowego, kliknij przycisk **kompilacji**.

   ![Tworzenie artefaktu menu kontekstowe][BU05]

IntelliJ ukończone artefaktu dla aplikacji rozruchu Spring powinien być wyświetlany w oknie narzędzia projektu.

   ![Utworzony artefaktów][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker

1. Jeśli użytkownik nie ma zalogowany do konta platformy Azure, postępuj zgodnie z instrukcjami [logowania instrukcje dotyczące zestawu narzędzi Azure for IntelliJ][Azure Sign In for IntelliJ].

1. W oknie narzędzia Eksplorator projektów kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Azure** > **Publikuj jako kontener Docker**.

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. Gdy **wdrożenia kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe, wyświetlane są wszystkie istniejące hosty Docker. Jeśli chcesz wdrożyć istniejącą hosta można przejdź do kroku 4. W przeciwnym razie wykonaj następujące kroki, aby utworzyć hosta:

   a. Kliknij przycisk plus zielony (**+**) symbolu.

      ![Dodaj nowy host platformy Docker][PU02]

   b. Gdy **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, użytkownik może zaakceptować wartości domyślne lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker. (Aby uzyskać szczegółowe opisy różnych ustawień, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą narzędzi Azure for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu ustawień.

      ![Określ opcje hostów Docker][PU03a]

   c. Istnieje możliwość używania istniejących poświadczeń logowania z usługi Azure key vault, lub użytkownik może wprowadzić nowe poświadczenia logowania Docker. Kliknij przycisk **Zakończ** po określeniu opcji.

      ![Określ poświadczenia hostów Docker][PU03b]

1. Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.

   ![Wybierz host Docker do użycia][PU04]

1. Na ostatniej stronie **wdrożenia kontenera Docker na platformie Azure** oknie dialogowym określ następujące opcje:

   a. Użytkownik może określić niestandardową nazwę kontenera, który będzie hostem z kontenera Docker lub zaakceptować ustawienia domyślne.

   b. Wprowadź porty TCP dla hosta docker przy użyciu następującej składni: *[portu zewnętrznego]*:*[wewnętrznego portu]*. Na przykład **80:8080** określa zewnętrznego portu 80 oraz domyślnego portu rozruchu Spring wewnętrzny 8080.
   
      Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml), należy określić numer portu dla poprawne routingu w usłudze Azure.

   c. Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.

   ![Wdrażanie kontenera Docker na platformie Azure][PU05]

1. Po zakończeniu publikowania narzędzi Azure dziennika aktywności platformy Azure Wyświetla **opublikowano** stanu.

   ![Pomyślnie wdrożono hostów Docker][PU06]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Informacje na temat dodatkowych metod do tworzenia aplikacji Spring rozruch przy użyciu IntelliJ, zobacz [tworzenia projektów rozruchu Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) na JetBrains witryny sieci Web.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
