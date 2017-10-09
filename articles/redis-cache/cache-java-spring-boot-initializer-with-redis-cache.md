---
title: "tooconfigure aaaHow toouse aplikacji Spring rozruchu inicjator pamięci podręcznej Redis"
description: "Dowiedz się, jak tooconfigure aplikacja rozruchu Spring utworzona przy hello Spring Initializr toouse pamięć podręczna Redis Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "Pamięć podręczna Redis Spring, Spring początkowego rozruchu,"
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="e0270-104">Jak tooconfigure toouse aplikacji Spring rozruchu inicjator pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="e0270-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="e0270-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e0270-105">Overview</span></span>

<span data-ttu-id="e0270-106">Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="e0270-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e0270-107">Jeden hello popularnych więcej projektów, które jest wbudowane znajdujący się na platformy jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="e0270-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e0270-108">Deweloperzy toohelp rozpocząć pracę z rozruchem Spring, kilka pakietów rozruchu Spring próbki są dostępne pod adresem <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="e0270-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e0270-109">Ponadto toochoosing z hello Lista podstawowa rozruchu Spring projektów, hello  **[Spring Initializr]**  ułatwia deweloperom szybkie wprowadzenie do tworzenia niestandardowych aplikacji rozruchu sprężyny.</span><span class="sxs-lookup"><span data-stu-id="e0270-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="e0270-110">W tym artykule przedstawiono tworzenie pamięci podręcznej Redis przy użyciu portalu Azure za pomocą hello hello **Spring Initializr** toocreate aplikacji niestandardowej, a następnie utworzenie Java sieci web aplikacji, która przechowuje i pobiera danych przy użyciu programu Pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="e0270-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0270-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e0270-111">Prerequisites</span></span>

<span data-ttu-id="e0270-112">Witaj, następujące wymagania wstępne są wymagane w kolejności toofollow hello opisanych w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="e0270-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="e0270-113">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="e0270-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="e0270-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), wersji 1,7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e0270-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="e0270-115">[Apache Maven](http://maven.apache.org/), w wersji 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e0270-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e0270-116">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e0270-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="e0270-117">Przeglądaj toohello Azure w portalu <https://portal.azure.com/> i kliknij element hello **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="e0270-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="e0270-119">Kliknij przycisk **bazy danych**, a następnie kliknij przycisk **pamięci podręcznej Redis**.</span><span class="sxs-lookup"><span data-stu-id="e0270-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="e0270-121">Na powitania **nowa pamięć podręczna Redis** wprowadź hello **nazwy DNS** dla pamięci podręcznej, następnie określ Twojej **subskrypcji**, **grupy zasobów**,  **Lokalizacja**, i **warstwa cenowa**.</span><span class="sxs-lookup"><span data-stu-id="e0270-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="e0270-122">Po określeniu tych opcji, kliknij przycisk **Utwórz** toocreate pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e0270-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="e0270-124">Po zakończeniu pamięć podręczną, pojawi się one dostępne w sieci Azure **pulpitu nawigacyjnego**, jak również zgodnie z hello **wszystkie zasoby**, i **pamięci podręczne Redis** stron.</span><span class="sxs-lookup"><span data-stu-id="e0270-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="e0270-125">Możesz kliknąć na pamięć podręczną na żadnym z tych lokalizacji tooopen hello właściwości strony dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e0270-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="e0270-127">Gdy zostanie wyświetlona strona hello, zawierający hello listę właściwości dla pamięci podręcznej, kliknij przycisk **klucze dostępu** i kopiowanie kluczy dostępu do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e0270-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="e0270-129">Tworzenie niestandardowych aplikacji przy użyciu hello Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e0270-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="e0270-130">Przeglądaj zbyt<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e0270-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e0270-131">Określ, czy toogenerate **Maven** projektu z **Java**, wprowadź hello **grupy** i **Aritifact** nazwy aplikacji, a następnie kliknij łącze hello zbyt**przełącznika toohello pełną wersję** z hello Initializr sprężyny.</span><span class="sxs-lookup"><span data-stu-id="e0270-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Opcje Initializr Basic Spring][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e0270-133">Witaj Spring Initializr użyje hello **grupy** i **Aritifact** nazwy pakietu hello toocreate nazwy, na przykład: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="e0270-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="e0270-134">Przewiń w dół toohello **sieci Web** sekcji i sprawdź pole hello **Web**, następnie przewiń w dół toohello **NoSQL** sekcji i sprawdź pole hello **Redis**, następnie przewiń toohello u dołu strony hello i kliknij przycisk hello zbyt**Generowanie projektu**.</span><span class="sxs-lookup"><span data-stu-id="e0270-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Opcje Initializr Spring pełny][SI02]

1. <span data-ttu-id="e0270-136">Po wyświetleniu monitu, Pobierz hello ścieżka tooa projektu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e0270-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Pobierz niestandardowy projekt Spring rozruchu][SI03]

1. <span data-ttu-id="e0270-138">Po wyodrębnieniu plików hello w systemie lokalnym, niestandardową aplikację Spring rozruchu będzie gotowy do edycji.</span><span class="sxs-lookup"><span data-stu-id="e0270-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Pliki projektu rozruchu Spring niestandardowe][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="e0270-140">Konfigurowanie Twojego niestandardowego toouse rozruchu Spring pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="e0270-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="e0270-141">Zlokalizuj hello *application.properties* pliku w hello *zasobów* katalogu aplikacji, lub utworzenia pliku hello, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="e0270-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Znajdź plik application.properties hello][RE01]

1. <span data-ttu-id="e0270-143">Otwórz hello *application.properties* plik w edytorze tekstów i Dodaj poniższe wiersze toohello plik hello i Zastąp wartości przykładowe hello hello odpowiednie właściwości z pamięci podręcznej:</span><span class="sxs-lookup"><span data-stu-id="e0270-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Edytowanie pliku application.properties hello][RE02]

1. <span data-ttu-id="e0270-145">Zapisz i zamknij hello *application.properties* pliku.</span><span class="sxs-lookup"><span data-stu-id="e0270-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="e0270-146">Utwórz folder o nazwie *kontrolera* w folderze źródłowym hello pakietu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e0270-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="e0270-147">— lub —</span><span class="sxs-lookup"><span data-stu-id="e0270-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="e0270-148">Utwórz nowy plik o nazwie *HelloController.java* w hello *kontrolera* folderu.</span><span class="sxs-lookup"><span data-stu-id="e0270-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="e0270-149">Otwórz plik hello w edytorze tekstów i Dodaj powitania po tooit kodu:</span><span class="sxs-lookup"><span data-stu-id="e0270-149">Open hello file in a text editor and add hello following code tooit:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="e0270-150">Jeżeli konieczne będzie tooreplace `com.contoso.myazuredemo` z hello nazwy pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="e0270-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="e0270-151">Zapisz i zamknij hello *HelloController.java* pliku.</span><span class="sxs-lookup"><span data-stu-id="e0270-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="e0270-152">Tworzenie aplikacji Spring rozruchu z Maven i uruchamianie na przykład:</span><span class="sxs-lookup"><span data-stu-id="e0270-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e0270-153">Testowanie aplikacji sieci web hello przechodząc toohttp://localhost:8080 za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="e0270-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="e0270-154">Powinny pojawić się powitania "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e0270-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="e0270-155">komunikat z Twojej kontrolera próbki wyświetlany, który dynamicznie pobierania z pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="e0270-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0270-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0270-156">Next steps</span></span>

<span data-ttu-id="e0270-157">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="e0270-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="e0270-158">Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e0270-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="e0270-159">Działającej aplikacja rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e0270-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="e0270-160">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e0270-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e0270-161">Uruchomiony przy użyciu pamięci podręcznej Redis z językiem Java na platformie Azure, można znaleźć więcej informacji na temat uzyskiwania [jak toouse Azure pamięci podręcznej Redis z językiem Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0270-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
