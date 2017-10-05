---
title: "Dodawanie aplikacji Java do aplikacji sieci Web usługi aplikacji Azure"
description: "W tym samouczku przedstawiono sposób dodawania strony lub aplikacji do Twojego wystąpienia usługi aplikacje sieci Web usługi aplikacji Azure, która jest już skonfigurowana do używania języka Java."
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
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="d0495-103">Dodawanie aplikacji Java do aplikacji sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="d0495-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="d0495-104">Po już zainicjować aplikacji sieci web Java w [usłudze Azure App Service] [ Azure App Service] zgodnie z opisem w [tworzenie aplikacji sieci web Java w usłudze Azure App Service](web-sites-java-get-started.md), możesz przekazać aplikacji przez umieszczenie Twojej WAR w **webapps** folderu.</span><span class="sxs-lookup"><span data-stu-id="d0495-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="d0495-105">Ścieżka nawigacji do **webapps** folderu różni się w zależności od konfiguracji wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d0495-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="d0495-106">Po skonfigurowaniu aplikacji sieci web przy użyciu portalu Azure Marketplace, ścieżka do **webapps** folder znajduje się w formularzu **d:\home\site\wwwroot\bin\application\_server\webapps**, gdzie **aplikacji\_serwera** jest nazwą serwera aplikacji dotyczące wystąpienia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d0495-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="d0495-107">Po skonfigurowaniu aplikacji sieci web przy użyciu interfejsu użytkownika, ścieżka do konfiguracji platformy Azure **webapps** folder znajduje się w formularzu **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="d0495-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="d0495-108">Należy pamiętać, że można użyć do kontroli źródła do przekazania aplikacji lub strony sieci web, w tym [scenariuszy integracji ciągłej](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d0495-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="d0495-109">FTP jest również opcja przekazywania aplikacji lub strony sieci web; Aby uzyskać więcej informacji na temat wdrażania aplikacji za pośrednictwem FTP, zobacz [wdrażanie aplikacji w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="d0495-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="d0495-110">Uwaga dla aplikacji sieci web Tomcat: po przesłaniu pliku WAR do **webapps** folderu, serwera aplikacji Tomcat wykryje, że został dodany i załaduje go automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d0495-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="d0495-111">Należy zauważyć, że po skopiowaniu plików (innych niż pliki WAR) do katalogu głównego serwera aplikacji będzie należy ponownie uruchomić te pliki są używane.</span><span class="sxs-lookup"><span data-stu-id="d0495-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="d0495-112">Funkcjonalność automatyczne ładowanie aplikacji sieci web Tomcat Java działających na platformie Azure jest oparta na plik WAR dodawany lub nowe pliki lub katalogi są dodawane do **webapps** folderu.</span><span class="sxs-lookup"><span data-stu-id="d0495-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="d0495-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d0495-113">See Also</span></span>
<span data-ttu-id="d0495-114">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d0495-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="d0495-115">Application-insights-App-insights-Java-Get-Started</span><span class="sxs-lookup"><span data-stu-id="d0495-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="d0495-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="d0495-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="d0495-117">[wdrażanie aplikacji w usłudze Azure App Service]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="d0495-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
