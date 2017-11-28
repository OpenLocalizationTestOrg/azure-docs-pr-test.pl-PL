---
title: "Wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć aplikację w usłudze Azure App Service przy użyciu FTP i FTPS."
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="ec2fa-103">Wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S</span><span class="sxs-lookup"><span data-stu-id="ec2fa-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="ec2fa-104">W tym artykule przedstawiono sposób użycia FTP i FTPS, aby wdrożyć aplikację sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="ec2fa-105">Punkt końcowy FTP/S dla aplikacji jest już aktywna.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="ec2fa-106">Konfiguracja nie jest niezbędne do obsługi wdrożenia FTP/S.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec2fa-107">Firma Microsoft stale trwa kroków w celu poprawy zabezpieczeń platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="ec2fa-108">Jako część tego ciągłego wysiłku regiony Niemcy centralnej i Niemcy północno-wschodnie planowana jest uaktualnienie aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="ec2fa-109">Podczas tego aplikacje sieci Web spowoduje wyłączenie użycia protokołu zwykły tekst FTP dla wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="ec2fa-110">Nasze zalecenie, aby klientów jest aby przełączyć się do FTPS wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="ec2fa-111">Firma Microsoft nie oczekuje żadnych przerw w działaniu z usługą podczas tego uaktualnienia, którą jest planowana 9/5.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="ec2fa-112">Dziękujemy za obsługuje w tym wysiłku.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="ec2fa-113">Krok 1: Konfigurowanie poświadczeń wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ec2fa-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="ec2fa-114">Aby uzyskać dostęp do serwera FTP dla aplikacji, najpierw poświadczenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="ec2fa-115">Aby skonfigurować lub zresetować poświadczenia wdrażania, zobacz [poświadczenia wdrożenia usługi aplikacji Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="ec2fa-116">W tym samouczku przedstawiono na używanie poświadczeń na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="ec2fa-117">Krok 2: Pobieranie informacji o połączeniu FTP</span><span class="sxs-lookup"><span data-stu-id="ec2fa-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="ec2fa-118">W [portalu Azure](https://portal.azure.com), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="ec2fa-119">Wybierz **omówienie** w menu po lewej stronie, a następnie zanotuj wartości **użytkownika serwera FTP/wdrożenia**, **nazwa hosta FTP**, i **nazwy hosta FTPS**.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informacje o połączeniu FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="ec2fa-121">**Użytkownika serwera FTP/wdrożenia** użytkownika wartość wyświetlaną w portalu Azure, łącznie z nazwą aplikacji w celu zapewnienia prawidłowego kontekstu dla serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="ec2fa-122">Te same informacje można znaleźć po wybraniu **właściwości** w lewym menu.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="ec2fa-123">Ponadto hasła wdrożenia nigdy nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="ec2fa-124">Jeśli użytkownik zapomni hasła wdrożenia, wróć do [krok 1](#step1) i zresetuj hasło wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="ec2fa-125">Krok 3: Wdrażanie plików na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ec2fa-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="ec2fa-126">Z tego klienta FTP ([programu Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)itp), Użyj zebranych do nawiązania połączenia aplikacji informacje o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="ec2fa-127">Kopiowanie plików i ich struktury katalogów odpowiednich do [ **/lokacji/wwwroot** katalogu](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) na platformie Azure (lub **/lokacji/wwwroot/App_Data/zadania/** katalogu dla zadań Webjob).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="ec2fa-128">Przejdź do adresu URL aplikacji, aby sprawdzić, czy aplikacja działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ec2fa-129">W odróżnieniu od [wdrożenia oparte na Git](app-service-deploy-local-git.md), wdrożenie FTP nie obsługuje następujących automatyzacji wdrażania:</span><span class="sxs-lookup"><span data-stu-id="ec2fa-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="ec2fa-130">Przywracanie zależności (na przykład automatyzacji NuGet, NPM, PIP i kompozytor)</span><span class="sxs-lookup"><span data-stu-id="ec2fa-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="ec2fa-131">Kompilacja plików binarnych .NET</span><span class="sxs-lookup"><span data-stu-id="ec2fa-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="ec2fa-132">Generowanie pliku Web.config (w tym miejscu jest [przykład Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="ec2fa-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="ec2fa-133">Należy przywrócić, kompilacji i generuje te niezbędne pliki ręcznie na komputerze lokalnym i wdrażać je razem z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ec2fa-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec2fa-134">Next steps</span></span>

<span data-ttu-id="ec2fa-135">W przypadku bardziej zaawansowanych scenariuszy wdrażania, spróbuj [wdrażanie na platformie Azure za pomocą narzędzia Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="ec2fa-136">Wdrożenie oparte na Git na platformie Azure umożliwia kontroli wersji, Przywracanie pakietu MSBuild i więcej.</span><span class="sxs-lookup"><span data-stu-id="ec2fa-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="ec2fa-137">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="ec2fa-137">More Resources</span></span>

* <span data-ttu-id="ec2fa-138">[Tworzenie aplikacji sieci web PHP MySQL i wdrażanie za pomocą protokołu FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="ec2fa-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="ec2fa-139">Poświadczenia wdrożenia usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="ec2fa-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
