---
title: "Utwórz aplikację sieci web platformy Azure z systemem Linux | Dokumentacja firmy Microsoft"
description: "Przepływ tworzenia aplikacji sieci Web dla aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="73143-104">Utwórz aplikację sieci web platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="73143-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="73143-105">Użyj portalu Azure, aby utworzyć aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="73143-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="73143-106">Można utworzyć aplikacji sieci web w systemie Linux z [portalu Azure](https://portal.azure.com) jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="73143-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Rozpocznij tworzenie aplikacji sieci web w portalu Azure][1]

<span data-ttu-id="73143-108">Następnie **bloku Utwórz** otwiera, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="73143-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Tworzenie bloku][2]

1. <span data-ttu-id="73143-110">Nadaj nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="73143-110">Give your web app a name.</span></span>
2. <span data-ttu-id="73143-111">Wybierz istniejącą grupę zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="73143-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="73143-112">(Zobacz dostępnych regionów w [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="73143-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="73143-113">Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="73143-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="73143-114">(Zobacz uwagi planu usługi aplikacji w [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="73143-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="73143-115">Wybierz stosu aplikacji, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="73143-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="73143-116">Można wybrać różne wersje programu Node.js, PHP, .net Core i Ruby.</span><span class="sxs-lookup"><span data-stu-id="73143-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="73143-117">Po utworzeniu aplikacji można zmienić stosu aplikacji z ustawień aplikacji, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="73143-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Ustawienia aplikacji][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="73143-119">Wdrażanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="73143-119">Deploy your web app</span></span>
<span data-ttu-id="73143-120">Wybieranie **opcje wdrażania** z zarządzania portalu daje możliwość użycia lokalnego repozytorium Git i GitHub do wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73143-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="73143-121">Pozostałe instrukcje są podobne do tych aplikacji sieci web z systemem innym niż Linux.</span><span class="sxs-lookup"><span data-stu-id="73143-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="73143-122">Można postępuj zgodnie z instrukcjami [lokalnego wdrożenia Git](app-service-deploy-local-git.md) lub [ciągłe wdrażanie](app-service-continuous-deployment.md) do wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73143-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="73143-123">Umożliwia także FTP do przekazywania aplikacji do witryny.</span><span class="sxs-lookup"><span data-stu-id="73143-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="73143-124">Można uzyskać punktu końcowego FTP dla aplikacji sieci web, z sekcji dzienników diagnostyki, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="73143-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Dzienniki diagnostyczne][4]

## <a name="next-steps"></a><span data-ttu-id="73143-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73143-126">Next steps</span></span>
* [<span data-ttu-id="73143-127">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="73143-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="73143-128">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="73143-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="73143-129">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="73143-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="73143-130">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="73143-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
