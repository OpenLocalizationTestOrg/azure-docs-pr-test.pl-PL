---
title: "aaaDeploy toohello Spring rozruchu aplikacji usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeprowadzi deweloperzy za pośrednictwem hello kroki toodeploy hello Spring wprowadzenie rozruchu sieci web aplikacji tooAzure usługi aplikacji."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service

Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa, a drugi hello popularnych więcej projektów, które jest oparty na danej platformie [Rozruchu spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.

W tym samouczku opisano jednak tworzenia przykładową hello Spring wprowadzenie rozruchu aplikację sieci web i wdrażania go za[usłudze Azure App Service].

### <a name="prerequisites"></a>Wymagania wstępne

Kolejność toocomplete hello kroków w tym samouczku niezbędne są następujące hello toohave:

* Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].
* Aktualne [Java Developer Kit (JDK)].
* Apache na [Maven] (w wersji 3) Narzędzie kompilacji.
* A [Git] klienta.

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Tworzenie aplikacji sieci web Spring wprowadzenie rozruchu hello

Witaj poniższe kroki objaśniają hello kroki, które są wymagane toocreate prostą aplikację sieci web Spring rozruchu i przetestować go lokalnie.

1. Otwórz wiersz polecenia i utworzyć toohold lokalnego katalogu aplikacji i zmień katalog toothat; na przykład:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   --lub--
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Witaj w klonowania [Spring wprowadzenie rozruchu] przykładowy projekt do katalogu hello właśnie utworzony; na przykład:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Zmień katalog projektu toohello ukończone; na przykład:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Kompiluj plik JAR hello za pomocą programu Maven; na przykład:
   ```
   mvn package
   ```

1. Po utworzeniu aplikacji sieci web hello Zmień plik JAR toohello katalogu i uruchomić aplikacji sieci web hello; na przykład:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Testowanie aplikacji sieci web hello przechodząc toohttp://localhost:8080 za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:
   ```
   curl http://localhost:8080
   ```

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**

   ![Przejdź do przykładowej aplikacji][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Tworzenie aplikacji sieci web platformy Azure do użycia z językiem Java

Hello następujące kroki umożliwia przeprowadzenie toocreate kroki hello aplikacji sieci Web platformy Azure, skonfigurować ustawienia hello wymagany dla języka Java i skonfigurować poświadczenia FTP.

1. Przeglądaj toohello [portalu Azure] i zaloguj się.

1. Gdy użytkownik zalogował się na koncie na powitania portalu Azure, kliknij ikonę menu hello **usługi aplikacji**:
   
   ![Azure Portal][AZ01]

1. Gdy hello **usługi aplikacji** strona jest wyświetlana, kliknij przycisk **+ Dodaj** toocreate nowej usługi aplikacji.

   ![Tworzenie usługi App Service][AZ02]

1. Gdy zostanie wyświetlona lista hello szablonów aplikacji sieci web, kliknij łącze hello hello Podstawowa aplikacja sieci Web firmy Microsoft.

   ![Szablony aplikacji sieci Web][AZ03]

1. Gdy zostanie wyświetlona strona informacji hello hello szablonu aplikacji sieci Web, kliknij przycisk **Utwórz**.

   ![Tworzenie aplikacji sieci Web][AZ04]

1. Podaj unikatową nazwę aplikacji sieci web i określ dodatkowe ustawienia, a następnie **Utwórz**.

   ![Tworzenie ustawień aplikacji sieci Web][AZ05]

1. Po utworzeniu aplikacji sieci web, kliknij ikonę menu hello **usługi aplikacji**, a następnie kliknij przycisk z nowo utworzonych aplikacji sieci web:

   ![Lista aplikacji sieci Web][AZ06]

1. Po wyświetleniu aplikacji sieci web, określ wersję Java hello, używając hello następujące kroki:

   a. Kliknij przycisk hello **ustawienia aplikacji** elementu menu.

   b. Wybierz **Java 8** hello wersji języka Java.

   c. Wybierz **najnowszych** dla wersję pomocniczą Java hello.

   d. Wybierz **najnowsze 8.5 Tomcat** hello kontenera sieci web. (Ten kontener nie będzie faktycznie używane; Azure użyje kontenera hello aplikację Spring rozruchu).

   e. Kliknij pozycję **Zapisz**.

   ![Ustawienia aplikacji][AZ07]

1. Określ poświadczenia wdrażania FTP przy użyciu hello następujące kroki:

   a. Kliknij przycisk hello **poświadczenia wdrażania** elementu menu.

   b. Określ nazwę użytkownika i hasło.

   c. Kliknij pozycję **Zapisz**.

   ![Określ poświadczenia wdrożenia][AZ08]

1. Pobierz informacje o połączeniu FTP przy użyciu hello następujące kroki:

   a. Kliknij przycisk hello **poświadczenia wdrażania** elementu menu.

   b. Kopiuj pełną FTP nazwę użytkownika i adres URL i zapisane w celu hello następnej sekcji tego samouczka.

   ![Adresu URL usługi FTP i poświadczenia][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Wdrażanie sieci tooAzure aplikacji sieci web Spring rozruchu

Hello następujące kroki objaśniają hello kroki toodeploy tooAzure aplikacji sieci web programu rozruchu sprężyny.

1. Otwórz Edytor tekstu, takiego jak Notatnik systemu Windows i Wklej powitania po tekst na nowy dokument, a następnie zapisz plik hello jako *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Po zapisaniu hello *web.config* tooyour systemu plików, połączyć tooyour aplikację sieci web za pośrednictwem protokołu FTP przy użyciu adresu URL hello, username i password z hello powyższej sekcji tego samouczka. Na przykład:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Zmiany hello katalog zdalny toohello folder główny aplikacji sieci web (czyli w */lokacji/wwwroot*), następnie skopiuj plik JAR hello aplikację Spring rozruchu i hello *web.config* z wcześniej. Na przykład:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Po wdrożeniu sieci JAR i *web.config* plików tooyour aplikacji sieci web, należy toorestart aplikacji sieci web przy użyciu hello portalu Azure:

   ![][AZ10]

1. Testowanie aplikacji sieci web hello przechodząc adres URL aplikacji sieci web tooyour za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**

   ![Przejdź do przykładowej aplikacji][SB02]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:

* [Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

Aby uzyskać dodatkowe informacje o tooAzure aplikacji sieci web depoying za pomocą protokołu FTP, zobacz [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S].

Dodatkowe szczegóły dotyczące hello rozruchu Spring przykładowy projekt, zobacz [Spring wprowadzenie rozruchu].

Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz hello **Spring Initializr** na https://start.spring.io/.

Aby uzyskać więcej informacji o konfigurowaniu dodatkowych ustawień dla aplikacji sieci web, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service].

<!-- URL List -->

[usłudze Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[Konfigurowanie aplikacji sieci web w usłudze Azure App Service]: /azure/app-service-web/web-sites-configure
[wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Rozruchu spring]: http://projects.spring.io/spring-boot/
[Spring wprowadzenie rozruchu]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
