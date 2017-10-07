---
title: "zestaw narzędzi platformy Azure dla programu Eclipse hello aaaPublish aplikacji Spring rozruchu, jako kontener Docker przy użyciu | Dokumentacja firmy Microsoft"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publikowanie aplikacji rozruchu Spring jako kontener Docker przy użyciu hello Azure zestawu narzędzi dla programu Eclipse

Witaj [Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.

[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.

W tym samouczku przedstawiono hello kroki toodeploy aplikacja rozruchu Spring jako Docker tooMicrosoft kontenera Azure za pomocą hello Azure zestawu narzędzi dla programu Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Klonuj repozytorium Docker rozruchu Spring domyślne hello

### <a name="import-hello-public-repository"></a>Importuj hello publicznego repozytorium

Witaj kolejnych krokach objaśniono sposób przez klonowanie komputera lokalnego repozytorium tooyour hello Spring Docker rozruch przy użyciu IntelliJ. Jeśli chcesz toouse wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].

1. Otwórz środowisko Eclipse.

1. Kliknij przycisk **pliku** > **importu**.

   ![Menu Plik importu][CL01]

1. Gdy hello **importu** zostanie otwarte okno dialogowe:

   a. Rozwiń węzeł **Git**.

   b. Wybierz **projekty z Git**.
   
   c. Kliknij przycisk **Dalej**.

   ![Okno dialogowe Importowanie][CL02]

1. Na powitania **wybierz źródło repozytorium** strony:

   a. Wybierz **Clone URI**.
   
   b. Kliknij przycisk **Dalej**.

   ![Wybierz źródło repozytorium strony][CL03]

1. Na powitania **repozytorium Git źródła** strony:

   a. Aby uzyskać **URI**, wprowadź `https://github.com/spring-guides/gs-spring-boot-docker.git`. Ten krok powinien automatycznie wypełnić hello **hosta** i **ścieżki repozytorium** pola z hello Popraw wartości.
   
   b. repozytorium rozruchu Spring Hello jest publiczny, więc nie powinien mieć tooenter Git nazwę użytkownika i hasło.
   
   c. Kliknij przycisk **Dalej**.

   ![Źródło repozytorium Git strony][CL04]

1. Na powitania **wybór gałęzi** kliknij przycisk **dalej**.

   ![Strona wybierania gałęzi][CL05]

1. Na powitania **lokalne miejsce docelowe** strony:

   a. Określ folder lokalny hello miejscu użytkownika lokalnego repozytorium.
   
   b. Kliknij przycisk **Dalej**.

   ![Strona docelowa lokalnego][CL06]

1. Na powitania **wybierz toouse Kreatora importowania projektów** strony:

   a. Wybierz **importu jako ogólne projekt**.
   
   b. Kliknij przycisk **Dalej**.

   ![Strony "Wybierz toouse Kreatora importowania projektów"][CL07]

1. Na powitania **Import projektów** strony:

   a. Określ nazwę projektu.
   
   b. Kliknij przycisk **Zakończ**.

   ![Importowanie projektów][CL08]

1. W repozytorium hello został pomyślnie sklonowany, widoczne wszystkie pliki hello na liście w programie Eclipse.

   ![Lokalne repozytorium][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Utwórz projekt Maven z lokalnym repozytorium

repozytorium Docker rozruchu Spring Hello zawiera ukończone projekt Maven, który będzie używany na potrzeby tego samouczka. 

1. Kliknij przycisk **pliku** > **importu**.

   ![Zaimportuj polecenia menu Plik hello][CL01]

1. Gdy hello **importu** zostanie otwarte okno dialogowe:

   a. Rozwiń węzeł **Maven**.
   
   b. Wybierz **istniejące projekty Maven**.
   
   c. Kliknij przycisk **Dalej**.

   ![Okno dialogowe Importowanie][MV01]

1. Na powitania **projekty Maven** strony:

   a. Dla **katalog główny**, określ hello **pełną** folderu w lokalnym repozytorium.
   
   b. Rozwiń węzeł hello **zaawansowane** , a następnie wprowadź niestandardową nazwę **szablon nazwy**.
   
   c. Wybierz hello pole hello **pom.xml** plik w projekcie hello.
   
   d. Kliknij przycisk **Zakończ**.

   ![Strona Projekty maven][MV02]

1. Otwarcie projekt Maven hello pomyślnie, zostanie wyświetlony drugi projektu Eclipse na liście.

   ![Projekt Maven lokalnego][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Tworzenie aplikacji Spring rozruch przy użyciu narzędzia Maven

1. Wybierz projekt Maven hello hello Eksplorator projektów programu Eclipse.

1. Kliknij przycisk **Uruchom** > **Uruchom jako** > **kompilacja Maven**.

   ![Polecenia toorun jako kompilacja Maven][BU01]

1. Po pomyślnym utworzeniu aplikacji hello okna konsoli Pokazuje stan hello.

   ![Pomyślne kompilacja Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker

1. Wybierz projekt Maven hello hello Eksplorator projektów programu Eclipse.

1. Kliknij przycisk hello Azure **publikowania** menu, a następnie kliknij przycisk **Publikuj jako kontener Docker**.

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. Gdy hello **wdrażanie kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe:

   a. Wprowadź nazwę niestandardowego obrazu Docker.
   
   b. Dla **toodeploy artefaktu**, określ hello ścieżki toohello **gs-spring — rozruchu docker-0.1.0.jar** plików, które zostały utworzone.

   ![Określ opcje Docker][PU02]

   Wyświetlane są wszystkie istniejące hosty Docker. 

1. Jeśli wybierzesz toodeploy tooan istniejącą hosta, możesz pominąć toostep 5. W przeciwnym razie użyj hello następujące kroki toocreate hosta:

   a. Kliknij pozycję **Dodaj**.

      ![Dodaj nowy host platformy Docker][PU03]

   b. Gdy hello **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, możesz wybrać domyślne hello tooaccept lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker. (Aby uzyskać szczegółowe opisy hello różne ustawienia, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu które toouse ustawienia.

      ![Określ opcje hostów Docker][PU04]

   c. Możesz wybrać toouse istniejących poświadczeń logowania usługi Azure key vault lub tooenter można wybrać nowe poświadczenia logowania Docker. Kliknij przycisk **Zakończ** po określeniu opcji.

      ![Określ poświadczenia hostów Docker][PU05]

1. Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.

   ![Wybierz toouse hostów Docker][PU06]

1. Na ostatniej stronie powitania hello **wdrażanie kontenera Docker na platformie Azure** oknie dialogowym Określ hello następujące opcje:

   a. Można wybrać toospecify niestandardową nazwę kontenera hello, który będzie obsługiwał z kontenera Docker lub możesz zaakceptować domyślną hello.

   b. Wprowadź porty TCP powitania dla hosta docker przy użyciu składni hello: *[portu zewnętrznego]*:*[wewnętrznego portu]*. Na przykład **80:8080** określa zewnętrznego portu 80 i hello domyślnego wewnętrzny rozruchu Spring portu 8080.
   
      Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml hello), należy numer portu hello toospecify dla hello poprawne toooccur routingu na platformie Azure.

   c. Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.

   ![Wdrażanie kontenera Docker na platformie Azure][PU07]

1. Po zakończeniu publikowania hello Azure Toolkit hello Wyświetla dziennika aktywności platformy Azure **opublikowano** hello stanu.

   ![Pomyślnie wdrożono hostów Docker][PU08]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
