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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="f17de-103">Dodaj tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji</span><span class="sxs-lookup"><span data-stu-id="f17de-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="f17de-104">Gdy już zainicjować aplikacji sieci web Java w [usłudze Azure App Service] [ Azure App Service] zgodnie z opisem w [tworzenie aplikacji sieci web Java w usłudze Azure App Service](web-sites-java-get-started.md), możesz przekazać aplikacji przez umieszczenie Twoje WAR w hello **webapps** folderu.</span><span class="sxs-lookup"><span data-stu-id="f17de-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="f17de-105">Witaj nawigacji ścieżki toohello **webapps** folderu różni się w zależności od konfiguracji wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f17de-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="f17de-106">Jeśli konfigurujesz aplikacji sieci web przy użyciu portalu Azure Marketplace hello hello toohello ścieżka **webapps** folder jest w formie hello **d:\home\site\wwwroot\bin\application\_server\webapps**, gdzie **aplikacji\_serwera** jest nazwą powitania serwera aplikacji hello dotyczące wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f17de-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="f17de-107">Jeśli konfigurujesz aplikacji sieci web przy użyciu hello Azure interfejs użytkownika konfiguracji hello toohello ścieżka **webapps** folder jest w formie hello **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="f17de-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="f17de-108">Należy pamiętać, której można tooupload kontroli źródła, aplikacji lub strony sieci web, w tym [scenariuszy integracji ciągłej](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f17de-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f17de-109">FTP jest również opcja przekazywania aplikacji lub strony sieci web; Aby uzyskać więcej informacji na temat wdrażania aplikacji za pośrednictwem FTP, zobacz [wdrażanie tooAzure Twojej aplikacji usługi App Service].</span><span class="sxs-lookup"><span data-stu-id="f17de-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="f17de-110">Uwaga dla aplikacji sieci web Tomcat: po przesłaniu Twojej toohello pliku WAR **webapps** folderu, serwera aplikacji Tomcat hello wykryje, że został dodany i załaduje go automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f17de-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="f17de-111">Należy zauważyć, że po skopiowaniu plików (innych niż pliki WAR) toohello katalogu serwera aplikacji hello będzie toobe po ponownym uruchomieniu te pliki są używane.</span><span class="sxs-lookup"><span data-stu-id="f17de-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="f17de-112">Hello funkcjonalność automatyczne ładowanie aplikacji sieci web Tomcat Java hello działających na platformie Azure jest oparta na plik WAR dodawany lub dodawanie nowych plików lub katalogów toohello **webapps** folderu.</span><span class="sxs-lookup"><span data-stu-id="f17de-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="f17de-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f17de-113">See Also</span></span>
<span data-ttu-id="f17de-114">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f17de-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="f17de-115">Application-insights-App-insights-Java-Get-Started</span><span class="sxs-lookup"><span data-stu-id="f17de-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[wdrażanie tooAzure Twojej aplikacji usługi App Service]: ./web-sites-deploy.md
