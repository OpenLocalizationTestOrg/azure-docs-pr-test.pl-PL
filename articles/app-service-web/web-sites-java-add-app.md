---
title: "aaaAdd tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji"
description: "Ten samouczek pokazuje, jak tooadd strony lub aplikacji wystąpienia tooyour aplikacji sieci Web usługi aplikacji Azure, który jest już skonfigurowany toouse Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Dodaj tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji
Gdy już zainicjować aplikacji sieci web Java w [usłudze Azure App Service] [ Azure App Service] zgodnie z opisem w [tworzenie aplikacji sieci web Java w usłudze Azure App Service](web-sites-java-get-started.md), możesz przekazać aplikacji przez umieszczenie Twoje WAR w hello **webapps** folderu.

Witaj nawigacji ścieżki toohello **webapps** folderu różni się w zależności od konfiguracji wystąpienia aplikacji sieci Web.

* Jeśli konfigurujesz aplikacji sieci web przy użyciu portalu Azure Marketplace hello hello toohello ścieżka **webapps** folder jest w formie hello **d:\home\site\wwwroot\bin\application\_server\webapps**, gdzie **aplikacji\_serwera** jest nazwą powitania serwera aplikacji hello dotyczące wystąpienia aplikacji sieci Web. 
* Jeśli konfigurujesz aplikacji sieci web przy użyciu hello Azure interfejs użytkownika konfiguracji hello toohello ścieżka **webapps** folder jest w formie hello **d:\home\site\wwwroot\webapps**. 

Należy pamiętać, której można tooupload kontroli źródła, aplikacji lub strony sieci web, w tym [scenariuszy integracji ciągłej](app-service-continuous-deployment.md). FTP jest również opcja przekazywania aplikacji lub strony sieci web; Aby uzyskać więcej informacji na temat wdrażania aplikacji za pośrednictwem FTP, zobacz [wdrażanie tooAzure Twojej aplikacji usługi App Service].

Uwaga dla aplikacji sieci web Tomcat: po przesłaniu Twojej toohello pliku WAR **webapps** folderu, serwera aplikacji Tomcat hello wykryje, że został dodany i załaduje go automatycznie. Należy zauważyć, że po skopiowaniu plików (innych niż pliki WAR) toohello katalogu serwera aplikacji hello będzie toobe po ponownym uruchomieniu te pliki są używane. Hello funkcjonalność automatyczne ładowanie aplikacji sieci web Tomcat Java hello działających na platformie Azure jest oparta na plik WAR dodawany lub dodawanie nowych plików lub katalogów toohello **webapps** folderu. 

<a name="see-also"></a>

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].

[Application-insights-App-insights-Java-Get-Started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[wdrażanie tooAzure Twojej aplikacji usługi App Service]: ./web-sites-deploy.md
