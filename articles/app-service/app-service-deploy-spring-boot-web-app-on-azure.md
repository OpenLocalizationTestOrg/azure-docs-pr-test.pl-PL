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
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="880e2-103">Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="880e2-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="880e2-104">Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa, a drugi hello popularnych więcej projektów, które jest oparty na danej platformie [Rozruchu spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="880e2-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="880e2-105">W tym samouczku opisano jednak tworzenia przykładową hello Spring wprowadzenie rozruchu aplikację sieci web i wdrażania go za[usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="880e2-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="880e2-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="880e2-106">Prerequisites</span></span>

<span data-ttu-id="880e2-107">Kolejność toocomplete hello kroków w tym samouczku niezbędne są następujące hello toohave:</span><span class="sxs-lookup"><span data-stu-id="880e2-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="880e2-108">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="880e2-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="880e2-109">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="880e2-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="880e2-110">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="880e2-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="880e2-111">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="880e2-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="880e2-112">Tworzenie aplikacji sieci web Spring wprowadzenie rozruchu hello</span><span class="sxs-lookup"><span data-stu-id="880e2-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="880e2-113">Witaj poniższe kroki objaśniają hello kroki, które są wymagane toocreate prostą aplikację sieci web Spring rozruchu i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="880e2-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="880e2-114">Otwórz wiersz polecenia i utworzyć toohold lokalnego katalogu aplikacji i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="880e2-115">--lub--</span><span class="sxs-lookup"><span data-stu-id="880e2-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="880e2-116">Witaj w klonowania [Spring wprowadzenie rozruchu] przykładowy projekt do katalogu hello właśnie utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="880e2-117">Zmień katalog projektu toohello ukończone; na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="880e2-118">Kompiluj plik JAR hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="880e2-119">Po utworzeniu aplikacji sieci web hello Zmień plik JAR toohello katalogu i uruchomić aplikacji sieci web hello; na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="880e2-120">Testowanie aplikacji sieci web hello przechodząc toohttp://localhost:8080 za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="880e2-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="880e2-121">Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**</span><span class="sxs-lookup"><span data-stu-id="880e2-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Przejdź do przykładowej aplikacji][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="880e2-123">Tworzenie aplikacji sieci web platformy Azure do użycia z językiem Java</span><span class="sxs-lookup"><span data-stu-id="880e2-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="880e2-124">Hello następujące kroki umożliwia przeprowadzenie toocreate kroki hello aplikacji sieci Web platformy Azure, skonfigurować ustawienia hello wymagany dla języka Java i skonfigurować poświadczenia FTP.</span><span class="sxs-lookup"><span data-stu-id="880e2-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="880e2-125">Przeglądaj toohello [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="880e2-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="880e2-126">Gdy użytkownik zalogował się na koncie na powitania portalu Azure, kliknij ikonę menu hello **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="880e2-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure Portal][AZ01]

1. <span data-ttu-id="880e2-128">Gdy hello **usługi aplikacji** strona jest wyświetlana, kliknij przycisk **+ Dodaj** toocreate nowej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="880e2-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Tworzenie usługi App Service][AZ02]

1. <span data-ttu-id="880e2-130">Gdy zostanie wyświetlona lista hello szablonów aplikacji sieci web, kliknij łącze hello hello Podstawowa aplikacja sieci Web firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="880e2-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Szablony aplikacji sieci Web][AZ03]

1. <span data-ttu-id="880e2-132">Gdy zostanie wyświetlona strona informacji hello hello szablonu aplikacji sieci Web, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="880e2-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Tworzenie aplikacji sieci Web][AZ04]

1. <span data-ttu-id="880e2-134">Podaj unikatową nazwę aplikacji sieci web i określ dodatkowe ustawienia, a następnie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="880e2-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Tworzenie ustawień aplikacji sieci Web][AZ05]

1. <span data-ttu-id="880e2-136">Po utworzeniu aplikacji sieci web, kliknij ikonę menu hello **usługi aplikacji**, a następnie kliknij przycisk z nowo utworzonych aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="880e2-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lista aplikacji sieci Web][AZ06]

1. <span data-ttu-id="880e2-138">Po wyświetleniu aplikacji sieci web, określ wersję Java hello, używając hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="880e2-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="880e2-139">a.</span><span class="sxs-lookup"><span data-stu-id="880e2-139">a.</span></span> <span data-ttu-id="880e2-140">Kliknij przycisk hello **ustawienia aplikacji** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="880e2-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="880e2-141">b.</span><span class="sxs-lookup"><span data-stu-id="880e2-141">b.</span></span> <span data-ttu-id="880e2-142">Wybierz **Java 8** hello wersji języka Java.</span><span class="sxs-lookup"><span data-stu-id="880e2-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="880e2-143">c.</span><span class="sxs-lookup"><span data-stu-id="880e2-143">c.</span></span> <span data-ttu-id="880e2-144">Wybierz **najnowszych** dla wersję pomocniczą Java hello.</span><span class="sxs-lookup"><span data-stu-id="880e2-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="880e2-145">d.</span><span class="sxs-lookup"><span data-stu-id="880e2-145">d.</span></span> <span data-ttu-id="880e2-146">Wybierz **najnowsze 8.5 Tomcat** hello kontenera sieci web.</span><span class="sxs-lookup"><span data-stu-id="880e2-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="880e2-147">(Ten kontener nie będzie faktycznie używane; Azure użyje kontenera hello aplikację Spring rozruchu).</span><span class="sxs-lookup"><span data-stu-id="880e2-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="880e2-148">e.</span><span class="sxs-lookup"><span data-stu-id="880e2-148">e.</span></span> <span data-ttu-id="880e2-149">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="880e2-149">Click **Save**.</span></span>

   ![Ustawienia aplikacji][AZ07]

1. <span data-ttu-id="880e2-151">Określ poświadczenia wdrażania FTP przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="880e2-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="880e2-152">a.</span><span class="sxs-lookup"><span data-stu-id="880e2-152">a.</span></span> <span data-ttu-id="880e2-153">Kliknij przycisk hello **poświadczenia wdrażania** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="880e2-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="880e2-154">b.</span><span class="sxs-lookup"><span data-stu-id="880e2-154">b.</span></span> <span data-ttu-id="880e2-155">Określ nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="880e2-155">Specify your username and password.</span></span>

   <span data-ttu-id="880e2-156">c.</span><span class="sxs-lookup"><span data-stu-id="880e2-156">c.</span></span> <span data-ttu-id="880e2-157">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="880e2-157">Click **Save**.</span></span>

   ![Określ poświadczenia wdrożenia][AZ08]

1. <span data-ttu-id="880e2-159">Pobierz informacje o połączeniu FTP przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="880e2-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="880e2-160">a.</span><span class="sxs-lookup"><span data-stu-id="880e2-160">a.</span></span> <span data-ttu-id="880e2-161">Kliknij przycisk hello **poświadczenia wdrażania** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="880e2-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="880e2-162">b.</span><span class="sxs-lookup"><span data-stu-id="880e2-162">b.</span></span> <span data-ttu-id="880e2-163">Kopiuj pełną FTP nazwę użytkownika i adres URL i zapisane w celu hello następnej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="880e2-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![Adresu URL usługi FTP i poświadczenia][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="880e2-165">Wdrażanie sieci tooAzure aplikacji sieci web Spring rozruchu</span><span class="sxs-lookup"><span data-stu-id="880e2-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="880e2-166">Hello następujące kroki objaśniają hello kroki toodeploy tooAzure aplikacji sieci web programu rozruchu sprężyny.</span><span class="sxs-lookup"><span data-stu-id="880e2-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="880e2-167">Otwórz Edytor tekstu, takiego jak Notatnik systemu Windows i Wklej powitania po tekst na nowy dokument, a następnie zapisz plik hello jako *web.config*:</span><span class="sxs-lookup"><span data-stu-id="880e2-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
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

1. <span data-ttu-id="880e2-168">Po zapisaniu hello *web.config* tooyour systemu plików, połączyć tooyour aplikację sieci web za pośrednictwem protokołu FTP przy użyciu adresu URL hello, username i password z hello powyższej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="880e2-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="880e2-169">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="880e2-170">Zmiany hello katalog zdalny toohello folder główny aplikacji sieci web (czyli w */lokacji/wwwroot*), następnie skopiuj plik JAR hello aplikację Spring rozruchu i hello *web.config* z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="880e2-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="880e2-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="880e2-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="880e2-172">Po wdrożeniu sieci JAR i *web.config* plików tooyour aplikacji sieci web, należy toorestart aplikacji sieci web przy użyciu hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="880e2-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="880e2-173">Testowanie aplikacji sieci web hello przechodząc adres URL aplikacji sieci web tooyour za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="880e2-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="880e2-174">Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**</span><span class="sxs-lookup"><span data-stu-id="880e2-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Przejdź do przykładowej aplikacji][SB02]

## <a name="next-steps"></a><span data-ttu-id="880e2-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="880e2-176">Next steps</span></span>

<span data-ttu-id="880e2-177">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="880e2-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="880e2-178">Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="880e2-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="880e2-179">Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="880e2-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="880e2-180">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="880e2-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="880e2-181">Aby uzyskać dodatkowe informacje o tooAzure aplikacji sieci web depoying za pomocą protokołu FTP, zobacz [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S].</span><span class="sxs-lookup"><span data-stu-id="880e2-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="880e2-182">Dodatkowe szczegóły dotyczące hello rozruchu Spring przykładowy projekt, zobacz [Spring wprowadzenie rozruchu].</span><span class="sxs-lookup"><span data-stu-id="880e2-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="880e2-183">Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz hello **Spring Initializr** na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="880e2-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="880e2-184">Aby uzyskać więcej informacji o konfigurowaniu dodatkowych ustawień dla aplikacji sieci web, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="880e2-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

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
