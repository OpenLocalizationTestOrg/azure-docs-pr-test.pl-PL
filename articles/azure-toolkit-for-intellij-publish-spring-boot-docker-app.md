---
title: "aaaPublish aplikacji Spring rozruchu, jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publikowanie aplikacji rozruchu Spring jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ

Witaj [Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.

[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.

W tym samouczku przedstawiono hello kroki toodeploy aplikacja rozruchu Spring jako Docker tooMicrosoft kontenera Azure za pomocą hello Azure Toolkit for IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Klonowanie repozytorium Docker rozruchu Spring domyślne hello

Witaj kolejnych krokach objaśniono sposób za pomocą klonowania repozytorium Docker rozruchu Spring hello przy użyciu IntelliJ. Jeśli chcesz toouse wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].

1. Otwórz środowisko IntelliJ.

1. Na ekranie powitalnym hello, wybierz hello **GitHub** opcję hello **wyewidencjonowania z kontroli wersji** listy.

   ![Opcja GitHub kontroli wersji][CL01]

1. Wprowadź swoje poświadczenia, jeśli zostanie wyświetlony monit o toolog w.

   * Jeśli używasz toolog nazwy użytkownika i hasła w tooGitHub:

      ![Okno dialogowe wprowadzanie GitHub nazwy użytkownika i hasła][CL02a]

   * Jeśli używasz tokenu toolog w tooGitHub:

      ![Okno dialogowe wprowadzanie GitHub token][CL02b]

1. Wprowadź **https://github.com/spring-guides/gs-spring-boot-docker.git** dla adresu URL repozytorium hello, określ informacje o Twoich ścieżka lokalna i folder, a następnie kliknij **klonowania**.

   ![Okno dialogowe klonowanie repozytorium][CL03]

1. Gdy pojawi się monit toocreate IntelliJ projektu wybierz **nr**.

   ![Odrzucanie toocreate projektu IntelliJ][CL04]

1. Na stronie powitalnej powitania kliknij **Importowanie projektu**.

   ![Wybór projektu importu][CL05]

1. Znajdź ścieżki hello gdzie sklonować repozytorium rozruchu Spring hello, wybierz hello **pełną** folder główny hello, a następnie kliknij przycisk **OK**.

   ![Wybierz folder do zaimportowania][CL06]

1. Po wyświetleniu monitu wybierz **Tworzenie projektu z istniejących źródeł**.

   ![Opcja toocreate projekt z istniejących źródeł][CL07]

1. Określ nazwę projektu lub zaakceptuj domyślną hello, sprawdź hello poprawną ścieżkę toohello **pełną** folder, a następnie kliknij przycisk **dalej**.

   ![Określ nazwę projektu hello][CL08]

1. Dostosowywanie wszelkich katalogów do zaimportowania, a następnie kliknij przycisk **dalej**.

   ![Wybierz katalogów][CL09]

1. Przejrzyj hello tooimport biblioteki, a następnie kliknij przycisk **dalej**.

   ![Przegląd biblioteki projektu][CL10]

1. Przejrzyj hello struktury modułu, a następnie kliknij przycisk **dalej**.

   ![Przejrzyj struktury modułu][CL11]

1. Określ użytkownika JDK, a następnie kliknij przycisk **dalej**.

   ![Określ JDK][CL12]

1. Kliknij przycisk **Zakończ**.

   ![Przycisk Zakończ][CL13]

IntelliJ importuje hello rozruchu Spring aplikacji jako projekt i wyświetla struktury powitania po zakończeniu importowania hello.

![Spring aplikacji rozruchu w IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Tworzenie rozruchowych Spring aplikacji

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Tworzenie aplikacji hello przy użyciu hello Maven POM

1. Otwórz okno narzędzia Maven hello, jeśli nie jest już otwarty. Kliknij przycisk **widoku** > **narzędzia systemu Windows** > **projekty Maven**.

   ![Polecenia narzędzia Windows i projekty Maven][BU01]

1. W oknie narzędzia Maven hello, kliknij prawym przyciskiem myszy **pakietu** i wybierz **Uruchom kompilacja Maven**. (Jeśli projekt Maven nie występuje automatycznie, kliknij przycisk hello **ponownie zaimportować** ikonę na pasku narzędzi Maven hello.)

   ![Uruchom polecenie kompilacja Maven][BU02]

1. Powinna zostać wyświetlona IntelliJ **BUDOWANIE powiodło** podczas rozruchu Spring aplikacji został utworzony pomyślnie.

   ![Komunikat BUDOWANIE powiodło się][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Tworzenie artefaktu gotowe do wdrożenia

toopublish aplikacji Spring rozruchu, należy toocreate artefaktu gotowe do wdrożenia. Użyj hello następujące kroki:

1. Otwórz projekt aplikacji sieci web w środowisko IntelliJ.

1. Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.

   ![Struktura projekt — polecenie][ART01]

1. Kliknij zielony oraz hello (**+**) symboli tooadd artefaktu, kliknij przycisk **JAR**, a następnie kliknij przycisk **pusty**.

   ![Dodaj artefaktów][ART02]

1. Nazwa Twojej artefaktu pamiętając nie tooadd rozszerzenia "JAR" hello, a następnie określ hello folderu docelowego dla danych wyjściowych Maven powitalne.

   ![Określ właściwości artefaktów][ART03]

1. Tworzenie manifestu dla Twojego artefaktu (opcjonalnie):

   a. Kliknij przycisk **tworzenie manifestu**.

      ![Kliknij przycisk Utwórz manifestu hello][ART04a]

   b. Wybierz hello domyślną ścieżkę dla artefaktu hello, a następnie kliknij przycisk **OK**.

      ![Określ ścieżkę artefaktów][ART04b]

   c. Kliknij przycisk wielokropka hello (**...** ) klasy głównym hello toolocate.

      ![Zlokalizuj klasy głównym][ART04c]

   d. Wybierz klasy głównym, a następnie kliknij przycisk **OK**.

      ![Określ klasy głównym][ART04d]

1. Kliknij przycisk **OK**.

   ![Zamknij okno dialogowe hello struktury projektu][ART05]

> [!NOTE]
> Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na powitania JetBrains witryny sieci Web.
>

### <a name="build-hello-artifact-for-deployment"></a>Tworzenie artefaktu hello wdrożenia

1. Kliknij przycisk **kompilacji**, a następnie kliknij przycisk **artefakty**.

   ![Polecenie artefaktów kompilacji][BU04]

1. Gdy hello **artefaktów kompilacji** zostanie wyświetlone menu kontekstowego, kliknij przycisk **kompilacji**.

   ![Tworzenie artefaktu menu kontekstowe][BU05]

IntelliJ artefaktu ukończyć powitalnych dla aplikacji rozruchu Spring powinien być wyświetlany w oknie narzędzia projektu hello.

   ![Utworzony artefaktów][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker

1. Jeśli użytkownik nie ma zarejestrowany tooyour konto platformy Azure, wykonaj kroki hello w [logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].

1. W oknie narzędzia hello Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako kontener Docker**.

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. Gdy hello **wdrożenia kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe, wyświetlane są wszystkie istniejące hosty Docker. Jeśli wybierzesz toodeploy tooan istniejącą hosta, możesz pominąć toostep 4. W przeciwnym razie użyj hello następujące kroki toocreate hosta:

   a. Kliknij zielony oraz hello (**+**) symbolu.

      ![Dodaj nowy host platformy Docker][PU02]

   b. Gdy hello **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, możesz wybrać domyślne hello tooaccept lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker. (Aby uzyskać szczegółowe opisy hello różne ustawienia, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu które toouse ustawienia.

      ![Określ opcje hostów Docker][PU03a]

   c. Możesz wybrać toouse istniejących poświadczeń logowania usługi Azure key vault lub tooenter można wybrać nowe poświadczenia logowania Docker. Kliknij przycisk **Zakończ** po określeniu opcji.

      ![Określ poświadczenia hostów Docker][PU03b]

1. Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.

   ![Wybierz toouse hostów Docker hello][PU04]

1. Na ostatniej stronie powitania hello **wdrożenia kontenera Docker na platformie Azure** oknie dialogowym Określ hello następujące opcje:

   a. Można wybrać toospecify niestandardową nazwę kontenera hello, który będzie obsługiwał z kontenera Docker lub możesz zaakceptować domyślną hello.

   b. Wprowadź porty TCP powitania dla hosta docker przy użyciu składni hello: *[portu zewnętrznego]*:*[wewnętrznego portu]*. Na przykład **80:8080** określa zewnętrznego portu 80 i hello domyślnego wewnętrzny rozruchu Spring portu 8080.
   
      Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml hello), należy numer portu hello toospecify dla hello poprawne toooccur routingu na platformie Azure.

   c. Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.

   ![Wdrażanie kontenera Docker na platformie Azure][PU05]

1. Po zakończeniu publikowania hello Azure Toolkit hello Wyświetla dziennika aktywności platformy Azure **opublikowano** hello stanu.

   ![Pomyślnie wdrożono hostów Docker][PU06]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn o dodatkowe metody do tworzenia aplikacji Spring rozruch przy użyciu IntelliJ, zobacz [tworzenia projektów rozruchu Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) na powitania JetBrains witryny sieci Web.

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
