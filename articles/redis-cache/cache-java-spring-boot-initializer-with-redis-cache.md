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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Jak tooconfigure toouse aplikacji Spring rozruchu inicjator pamięci podręcznej Redis

## <a name="overview"></a>Omówienie

Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jeden hello popularnych więcej projektów, które jest wbudowane znajdujący się na platformy jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych. Deweloperzy toohelp rozpocząć pracę z rozruchem Spring, kilka pakietów rozruchu Spring próbki są dostępne pod adresem <https://github.com/spring-guides/>. Ponadto toochoosing z hello Lista podstawowa rozruchu Spring projektów, hello  **[Spring Initializr]**  ułatwia deweloperom szybkie wprowadzenie do tworzenia niestandardowych aplikacji rozruchu sprężyny.

W tym artykule przedstawiono tworzenie pamięci podręcznej Redis przy użyciu portalu Azure za pomocą hello hello **Spring Initializr** toocreate aplikacji niestandardowej, a następnie utworzenie Java sieci web aplikacji, która przechowuje i pobiera danych przy użyciu programu Pamięci podręcznej redis.

## <a name="prerequisites"></a>Wymagania wstępne

Witaj, następujące wymagania wstępne są wymagane w kolejności toofollow hello opisanych w tym artykule:

* Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].

* A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), wersji 1,7 lub nowszej.

* [Apache Maven](http://maven.apache.org/), w wersji 3.0 lub nowszej.

## <a name="create-a-redis-cache-on-azure"></a>Tworzenie pamięci podręcznej Redis na platformie Azure

1. Przeglądaj toohello Azure w portalu <https://portal.azure.com/> i kliknij element hello **+ nowy**.

   ![Azure Portal][AZ01]

1. Kliknij przycisk **bazy danych**, a następnie kliknij przycisk **pamięci podręcznej Redis**.

   ![Azure Portal][AZ02]

1. Na powitania **nowa pamięć podręczna Redis** wprowadź hello **nazwy DNS** dla pamięci podręcznej, następnie określ Twojej **subskrypcji**, **grupy zasobów**,  **Lokalizacja**, i **warstwa cenowa**. Po określeniu tych opcji, kliknij przycisk **Utwórz** toocreate pamięci podręcznej.

   ![Azure Portal][AZ03]

1. Po zakończeniu pamięć podręczną, pojawi się one dostępne w sieci Azure **pulpitu nawigacyjnego**, jak również zgodnie z hello **wszystkie zasoby**, i **pamięci podręczne Redis** stron. Możesz kliknąć na pamięć podręczną na żadnym z tych lokalizacji tooopen hello właściwości strony dla pamięci podręcznej.

   ![Azure Portal][AZ04]

1. Gdy zostanie wyświetlona strona hello, zawierający hello listę właściwości dla pamięci podręcznej, kliknij przycisk **klucze dostępu** i kopiowanie kluczy dostępu do pamięci podręcznej.

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Tworzenie niestandardowych aplikacji przy użyciu hello Spring Initializr

1. Przeglądaj zbyt<https://start.spring.io/>.

1. Określ, czy toogenerate **Maven** projektu z **Java**, wprowadź hello **grupy** i **Aritifact** nazwy aplikacji, a następnie kliknij łącze hello zbyt**przełącznika toohello pełną wersję** z hello Initializr sprężyny.

   ![Opcje Initializr Basic Spring][SI01]

   > [!NOTE]
   >
   > Witaj Spring Initializr użyje hello **grupy** i **Aritifact** nazwy pakietu hello toocreate nazwy, na przykład: *com.contoso.myazuredemo*.
   >

1. Przewiń w dół toohello **sieci Web** sekcji i sprawdź pole hello **Web**, następnie przewiń w dół toohello **NoSQL** sekcji i sprawdź pole hello **Redis**, następnie przewiń toohello u dołu strony hello i kliknij przycisk hello zbyt**Generowanie projektu**.

   ![Opcje Initializr Spring pełny][SI02]

1. Po wyświetleniu monitu, Pobierz hello ścieżka tooa projektu na komputerze lokalnym.

   ![Pobierz niestandardowy projekt Spring rozruchu][SI03]

1. Po wyodrębnieniu plików hello w systemie lokalnym, niestandardową aplikację Spring rozruchu będzie gotowy do edycji.

   ![Pliki projektu rozruchu Spring niestandardowe][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Konfigurowanie Twojego niestandardowego toouse rozruchu Spring pamięci podręcznej Redis

1. Zlokalizuj hello *application.properties* pliku w hello *zasobów* katalogu aplikacji, lub utworzenia pliku hello, jeśli jeszcze nie istnieje.

   ![Znajdź plik application.properties hello][RE01]

1. Otwórz hello *application.properties* plik w edytorze tekstów i Dodaj poniższe wiersze toohello plik hello i Zastąp wartości przykładowe hello hello odpowiednie właściwości z pamięci podręcznej:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Edytowanie pliku application.properties hello][RE02]

1. Zapisz i zamknij hello *application.properties* pliku.

1. Utwórz folder o nazwie *kontrolera* w folderze źródłowym hello pakietu; na przykład:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   — lub —

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Utwórz nowy plik o nazwie *HelloController.java* w hello *kontrolera* folderu. Otwórz plik hello w edytorze tekstów i Dodaj powitania po tooit kodu:

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
   
   Jeżeli konieczne będzie tooreplace `com.contoso.myazuredemo` z hello nazwy pakietu dla projektu.

1. Zapisz i zamknij hello *HelloController.java* pliku.

1. Tworzenie aplikacji Spring rozruchu z Maven i uruchamianie na przykład:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testowanie aplikacji sieci web hello przechodząc toohttp://localhost:8080 za pomocą przeglądarki sieci web, lub użyj składni hello jak hello poniższy przykład, jeśli masz curl dostępne:

   ```shell
   curl http://localhost:8080
   ```

   Powinny pojawić się powitania "Hello World!" komunikat z Twojej kontrolera próbki wyświetlany, który dynamicznie pobierania z pamięci podręcznej Redis.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:

* [Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Działającej aplikacja rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

Uruchomiony przy użyciu pamięci podręcznej Redis z językiem Java na platformie Azure, można znaleźć więcej informacji na temat uzyskiwania [jak toouse Azure pamięci podręcznej Redis z językiem Java][Redis Cache with Java].

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
