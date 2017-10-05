---
title: "Wdrażanie aplikacji rozruchu Spring w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeprowadzi deweloperzy przez kroki wdrażania aplikacji sieci web Spring rozruchu wprowadzenie do usługi Azure App Service."
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
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="70b44-103">Wdrażanie aplikacji platformy Spring Boot w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="70b44-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="70b44-104"> **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa i jest jeden z popularnych więcej projektów, które jest oparty na danej platformie [ Powierzchni rozruchu], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="70b44-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="70b44-105">W tym samouczku opisano jednak tworzenia przykładowej aplikacji sieci web Spring wprowadzenie rozruchu i wdrażania go do [usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="70b44-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="70b44-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="70b44-106">Prerequisites</span></span>

<span data-ttu-id="70b44-107">Aby wykonać kroki opisane w tym samouczku, należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="70b44-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="70b44-108">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="70b44-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="70b44-109">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="70b44-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="70b44-110">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="70b44-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="70b44-111">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="70b44-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="70b44-112">Tworzenie aplikacji sieci web Spring wprowadzenie rozruchu</span><span class="sxs-lookup"><span data-stu-id="70b44-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="70b44-113">Poniższe kroki przeprowadzi Cię przez kolejne kroki, które są wymagane do tworzenia prostej aplikacji sieci web Spring rozruchu i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="70b44-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="70b44-114">Otwórz wiersz polecenia i utworzyć katalogu lokalnego do przechowywania aplikacji, przejdź do tego katalogu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="70b44-115">--lub--</span><span class="sxs-lookup"><span data-stu-id="70b44-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="70b44-116">Klonowanie [Spring wprowadzenie rozruchu] przykładowy projekt do katalogu, który został właśnie utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="70b44-117">Zmień katalog na ukończone projektu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="70b44-118">Kompiluj plik JAR za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="70b44-119">Po utworzeniu aplikacji sieci web, zmień katalog na plik JAR i uruchomić aplikację sieci web; na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="70b44-120">Testowanie aplikacji sieci web, przechodząc do adresem http://localhost: 8080 przy użyciu przeglądarki sieci web, lub użyj składni, jak w następującym przykładzie, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="70b44-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="70b44-121">Powinien zostać wyświetlony następujący komunikat wyświetlany: **pozdrowienia z Spring rozruchowe!**</span><span class="sxs-lookup"><span data-stu-id="70b44-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Przejdź do przykładowej aplikacji][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="70b44-123">Tworzenie aplikacji sieci web platformy Azure do użycia z językiem Java</span><span class="sxs-lookup"><span data-stu-id="70b44-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="70b44-124">Poniższe kroki przeprowadzi Cię przez kolejne kroki do tworzenia aplikacji sieci Web platformy Azure, skonfiguruj wymagane ustawienia dla języka Java i skonfigurować poświadczenia FTP.</span><span class="sxs-lookup"><span data-stu-id="70b44-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="70b44-125">Przejdź do [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="70b44-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="70b44-126">Gdy użytkownik zalogował się na koncie w portalu Azure, kliknij ikonę menu **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="70b44-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Azure Portal][AZ01]

1. <span data-ttu-id="70b44-128">Gdy **usługi aplikacji** strona jest wyświetlana, kliknij przycisk **+ Dodaj** do utworzenia nowej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="70b44-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Tworzenie usługi App Service][AZ02]

1. <span data-ttu-id="70b44-130">Gdy zostanie wyświetlona lista szablonów aplikacji sieci web, kliknij łącze dla podstawowej aplikacji sieci Web firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70b44-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Szablony aplikacji sieci Web][AZ03]

1. <span data-ttu-id="70b44-132">Po stronie informacje o szablonu aplikacji sieci Web zostanie wyświetlony, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="70b44-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Tworzenie aplikacji sieci Web][AZ04]

1. <span data-ttu-id="70b44-134">Podaj unikatową nazwę aplikacji sieci web i określ dodatkowe ustawienia, a następnie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="70b44-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Tworzenie ustawień aplikacji sieci Web][AZ05]

1. <span data-ttu-id="70b44-136">Po utworzeniu aplikacji sieci web, kliknij ikonę menu **usługi aplikacji**, a następnie kliknij przycisk z nowo utworzonych aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="70b44-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lista aplikacji sieci Web][AZ06]

1. <span data-ttu-id="70b44-138">Po wyświetleniu aplikacji sieci web, określ wersję języka Java przy użyciu następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="70b44-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="70b44-139">a.</span><span class="sxs-lookup"><span data-stu-id="70b44-139">a.</span></span> <span data-ttu-id="70b44-140">Kliknij przycisk **ustawienia aplikacji** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="70b44-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="70b44-141">b.</span><span class="sxs-lookup"><span data-stu-id="70b44-141">b.</span></span> <span data-ttu-id="70b44-142">Wybierz **Java 8** dla wersji języka Java.</span><span class="sxs-lookup"><span data-stu-id="70b44-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="70b44-143">c.</span><span class="sxs-lookup"><span data-stu-id="70b44-143">c.</span></span> <span data-ttu-id="70b44-144">Wybierz **najnowszych** dla wersji pomocniczej Java.</span><span class="sxs-lookup"><span data-stu-id="70b44-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="70b44-145">d.</span><span class="sxs-lookup"><span data-stu-id="70b44-145">d.</span></span> <span data-ttu-id="70b44-146">Wybierz **najnowsze 8.5 Tomcat** kontenera sieci web.</span><span class="sxs-lookup"><span data-stu-id="70b44-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="70b44-147">(Ten kontener nie będzie faktycznie używane; Azure użyje kontenera aplikację Spring rozruchu).</span><span class="sxs-lookup"><span data-stu-id="70b44-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="70b44-148">e.</span><span class="sxs-lookup"><span data-stu-id="70b44-148">e.</span></span> <span data-ttu-id="70b44-149">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="70b44-149">Click **Save**.</span></span>

   ![Ustawienia aplikacji][AZ07]

1. <span data-ttu-id="70b44-151">Określ poświadczenia wdrażania FTP przy użyciu następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="70b44-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="70b44-152">a.</span><span class="sxs-lookup"><span data-stu-id="70b44-152">a.</span></span> <span data-ttu-id="70b44-153">Kliknij przycisk **poświadczenia wdrażania** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="70b44-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="70b44-154">b.</span><span class="sxs-lookup"><span data-stu-id="70b44-154">b.</span></span> <span data-ttu-id="70b44-155">Określ nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="70b44-155">Specify your username and password.</span></span>

   <span data-ttu-id="70b44-156">c.</span><span class="sxs-lookup"><span data-stu-id="70b44-156">c.</span></span> <span data-ttu-id="70b44-157">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="70b44-157">Click **Save**.</span></span>

   ![Określ poświadczenia wdrożenia][AZ08]

1. <span data-ttu-id="70b44-159">Pobierz informacje o połączeniu FTP przy użyciu następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="70b44-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="70b44-160">a.</span><span class="sxs-lookup"><span data-stu-id="70b44-160">a.</span></span> <span data-ttu-id="70b44-161">Kliknij przycisk **poświadczenia wdrażania** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="70b44-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="70b44-162">b.</span><span class="sxs-lookup"><span data-stu-id="70b44-162">b.</span></span> <span data-ttu-id="70b44-163">Kopiuj pełną FTP nazwę użytkownika i adres URL i zapisywać je w następnej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="70b44-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![Adresu URL usługi FTP i poświadczenia][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="70b44-165">Wdrażanie aplikacji sieci web Spring rozruchowego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="70b44-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="70b44-166">Poniższe kroki objaśniają proces wdrażania aplikacji sieci web Spring rozruchowego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="70b44-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="70b44-167">Otwórz Edytor tekstu, takiego jak Notatnik systemu Windows i wklej poniższy tekst do nowego dokumentu, a następnie zapisz plik jako *web.config*:</span><span class="sxs-lookup"><span data-stu-id="70b44-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="70b44-168">Po zapisaniu *web.config* plików do systemu, nawiązać połączenia z aplikacji sieci web za pośrednictwem protokołu FTP przy użyciu adresu URL, nazwę użytkownika i hasło z poprzedniej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="70b44-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="70b44-169">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="70b44-170">Zmień katalog zdalny folder główny aplikacji sieci web (czyli w */lokacji/wwwroot*), następnie skopiuj plik JAR aplikację Spring rozruchu i *web.config* z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="70b44-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="70b44-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="70b44-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="70b44-172">Po wdrożeniu sieci JAR i *web.config* pliki do aplikacji sieci web, musisz ponownie uruchomić aplikacji sieci web przy użyciu portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="70b44-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="70b44-173">Testowanie aplikacji sieci web, przechodząc do adresu URL aplikacji sieci web w przeglądarce sieci web, lub użyj składni, jak w następującym przykładzie, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="70b44-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="70b44-174">Powinien zostać wyświetlony następujący komunikat wyświetlany: **pozdrowienia z Spring rozruchowe!**</span><span class="sxs-lookup"><span data-stu-id="70b44-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Przejdź do przykładowej aplikacji][SB02]

## <a name="next-steps"></a><span data-ttu-id="70b44-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70b44-176">Next steps</span></span>

<span data-ttu-id="70b44-177">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="70b44-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="70b44-178">Wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="70b44-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="70b44-179">Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w usłudze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="70b44-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="70b44-180">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="70b44-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="70b44-181">Aby uzyskać dodatkowe informacje o depoying aplikacje sieci web na platformie Azure za pomocą protokołu FTP, zobacz [wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S].</span><span class="sxs-lookup"><span data-stu-id="70b44-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="70b44-182">Dodatkowe szczegóły dotyczące rozruchu Spring przykładowy projekt, zobacz [Spring wprowadzenie rozruchu].</span><span class="sxs-lookup"><span data-stu-id="70b44-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="70b44-183">Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz **Spring Initializr** na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="70b44-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="70b44-184">Aby uzyskać więcej informacji o konfigurowaniu dodatkowych ustawień dla aplikacji sieci web, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="70b44-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="70b44-185">[usłudze Azure App Service]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="70b44-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="70b44-186">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="70b44-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="70b44-187">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="70b44-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="70b44-188">[Konfigurowanie aplikacji sieci web w usłudze Azure App Service]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="70b44-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="70b44-189">[wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="70b44-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="70b44-190">[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="70b44-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="70b44-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="70b44-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="70b44-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="70b44-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="70b44-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="70b44-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="70b44-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="70b44-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="70b44-195">[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="70b44-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="70b44-196">[ Powierzchni rozruchu]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="70b44-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="70b44-197">[Spring wprowadzenie rozruchu]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="70b44-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="70b44-198">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="70b44-198">[Spring Framework]: https://spring.io/</span></span>

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
