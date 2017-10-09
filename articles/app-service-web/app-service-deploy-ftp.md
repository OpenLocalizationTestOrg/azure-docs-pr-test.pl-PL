---
title: "aaaDeploy Twojego tooAzure aplikacji App Service przy użyciu FTP/S | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Twojego tooAzure aplikacji App Service przy użyciu FTP i FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="67f18-103">Wdrażanie sieci tooAzure aplikacji App Service przy użyciu FTP/S</span><span class="sxs-lookup"><span data-stu-id="67f18-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="67f18-104">W tym artykule opisano sposób toouse FTP i FTPS toodeploy aplikację sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API za[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="67f18-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="67f18-105">Hello końcowego FTP/S dla aplikacji jest już aktywna.</span><span class="sxs-lookup"><span data-stu-id="67f18-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="67f18-106">Konfiguracja nie jest konieczne tooenable wdrożenia FTP/S.</span><span class="sxs-lookup"><span data-stu-id="67f18-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67f18-107">Firma Microsoft stale wykonywanie czynności tooimprove zabezpieczeń platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="67f18-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="67f18-108">Jako część tego ciągłego wysiłku regiony Niemcy centralnej i Niemcy północno-wschodnie planowana jest uaktualnienie aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="67f18-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="67f18-109">Podczas tego aplikacje sieci Web będzie wyłączanie hello użycie protokołu zwykły tekst FTP wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="67f18-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="67f18-110">Naszym klientom tooour zalecenie jest tooFTPS tooswitch wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="67f18-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="67f18-111">Firma Microsoft nie będzie przerw w działaniu usługi tooyour podczas tego uaktualnienia, którą jest planowana 9/5.</span><span class="sxs-lookup"><span data-stu-id="67f18-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="67f18-112">Dziękujemy za obsługuje w tym wysiłku.</span><span class="sxs-lookup"><span data-stu-id="67f18-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="67f18-113">Krok 1: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="67f18-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="67f18-114">tooaccess hello FTP serwera dla aplikacji, należy najpierw poświadczenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="67f18-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="67f18-115">tooset lub zresetowania poświadczenia wdrażania, zobacz [poświadczenia wdrożenia usługi aplikacji Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="67f18-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="67f18-116">W tym samouczku przedstawiono używanie hello poświadczeń na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="67f18-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="67f18-117">Krok 2: Pobieranie informacji o połączeniu FTP</span><span class="sxs-lookup"><span data-stu-id="67f18-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="67f18-118">W hello [portalu Azure](https://portal.azure.com), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="67f18-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="67f18-119">Wybierz **omówienie** w menu po lewej stronie powitania, a następnie zanotuj wartości hello **użytkownika serwera FTP/wdrożenia**, **nazwa hosta FTP**, i **nazwy hosta FTPS**.</span><span class="sxs-lookup"><span data-stu-id="67f18-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informacje o połączeniu FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="67f18-121">Witaj **użytkownika serwera FTP/wdrożenia** użytkownika wartości wyświetlanej przez hello portalu Azure, łącznie z nazwą aplikacji hello w kolejności tooprovide prawidłowego kontekstu serwera hello FTP.</span><span class="sxs-lookup"><span data-stu-id="67f18-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="67f18-122">Można znaleźć hello tych samych informacji po wybraniu **właściwości** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="67f18-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="67f18-123">Ponadto hello wdrożenia hasło nigdy nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="67f18-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="67f18-124">Jeśli zapomnisz hasła wdrożenia, wróć za[krok 1](#step1) i zresetuj hasło wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="67f18-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="67f18-125">Krok 3: Wdrażanie tooAzure plików</span><span class="sxs-lookup"><span data-stu-id="67f18-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="67f18-126">Z tego klienta FTP ([programu Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)itp), użyj informacji o połączeniu hello zebranych tooconnect tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67f18-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="67f18-127">Kopiowanie plików i ich toohello struktury katalogu odpowiednich [ **/lokacji/wwwroot** katalogu](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) na platformie Azure (lub hello **/lokacji/wwwroot/App_Data/zadania/** katalogu dla Zadania Webjob).</span><span class="sxs-lookup"><span data-stu-id="67f18-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="67f18-128">Aplikacja hello tooverify adres URL przeglądania tooyour aplikacji działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="67f18-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="67f18-129">W odróżnieniu od [wdrożenia oparte na Git](app-service-deploy-local-git.md), wdrożenie FTP nie obsługuje powitania po automatyzacji wdrażania:</span><span class="sxs-lookup"><span data-stu-id="67f18-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="67f18-130">Przywracanie zależności (na przykład automatyzacji NuGet, NPM, PIP i kompozytor)</span><span class="sxs-lookup"><span data-stu-id="67f18-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="67f18-131">Kompilacja plików binarnych .NET</span><span class="sxs-lookup"><span data-stu-id="67f18-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="67f18-132">Generowanie pliku Web.config (w tym miejscu jest [przykład Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="67f18-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="67f18-133">Należy przywrócić, kompilacji i generuje te niezbędne pliki ręcznie na komputerze lokalnym i wdrażać je razem z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67f18-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="67f18-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67f18-134">Next steps</span></span>

<span data-ttu-id="67f18-135">W przypadku bardziej zaawansowanych scenariuszy wdrażania, spróbuj [wdrażanie tooAzure za pomocą narzędzia Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="67f18-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="67f18-136">Wdrażanie na podstawie Git tooAzure umożliwia kontroli wersji, Przywracanie pakietu MSBuild i więcej.</span><span class="sxs-lookup"><span data-stu-id="67f18-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="67f18-137">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="67f18-137">More Resources</span></span>

* <span data-ttu-id="67f18-138">[Tworzenie aplikacji sieci web PHP MySQL i wdrażanie za pomocą protokołu FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="67f18-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="67f18-139">Poświadczenia wdrożenia usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="67f18-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
