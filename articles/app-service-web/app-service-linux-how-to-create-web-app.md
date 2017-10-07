---
title: aaaCreate platformy Azure w sieci web aplikacji uruchomionej w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="507e2-104">Utwórz aplikację sieci web platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="507e2-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="507e2-105">Użyj aplikacji sieci web hello toocreate portalu Azure</span><span class="sxs-lookup"><span data-stu-id="507e2-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="507e2-106">Można utworzyć aplikacji sieci web w systemie Linux z hello [portalu Azure](https://portal.azure.com) pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="507e2-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Rozpocznij tworzenie aplikacji sieci web na powitania portalu Azure][1]

<span data-ttu-id="507e2-108">Następnie hello **bloku Utwórz** otwiera pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="507e2-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![bloku Utwórz Hello][2]

1. <span data-ttu-id="507e2-110">Nadaj nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="507e2-110">Give your web app a name.</span></span>
2. <span data-ttu-id="507e2-111">Wybierz istniejącą grupę zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="507e2-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="507e2-112">(Zobacz dostępnych regionów w hello [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="507e2-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="507e2-113">Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="507e2-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="507e2-114">(Zobacz uwagi planu usługi aplikacji w hello [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="507e2-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="507e2-115">Wybierz aplikację hello stosu, który ma toouse.</span><span class="sxs-lookup"><span data-stu-id="507e2-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="507e2-116">Można wybrać różne wersje programu Node.js, PHP, .net Core i Ruby.</span><span class="sxs-lookup"><span data-stu-id="507e2-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="507e2-117">Po utworzeniu aplikacji hello pokazane na powitania po obrazu można zmienić stosu aplikacji hello z ustawień aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="507e2-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Ustawienia aplikacji][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="507e2-119">Wdrażanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="507e2-119">Deploy your web app</span></span>
<span data-ttu-id="507e2-120">Wybieranie **opcje wdrażania** z zapewnia portalu zarządzania hello hello opcja toouse lokalnego Git i GitHub repozytorium toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="507e2-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="507e2-121">rest Hello instrukcji hello są podobne toothose dla aplikacji sieci web z systemem innym niż Linux.</span><span class="sxs-lookup"><span data-stu-id="507e2-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="507e2-122">Możesz wykonać instrukcje hello [lokalnego wdrożenia Git](app-service-deploy-local-git.md) lub [ciągłe wdrażanie](app-service-continuous-deployment.md) toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="507e2-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="507e2-123">Umożliwia także FTP tooupload w witrynie tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="507e2-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="507e2-124">Można pobrać punktu końcowego FTP powitania dla aplikacji sieci web z diagnostyki hello sekcji dzienniki pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="507e2-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Dzienniki diagnostyczne][4]

## <a name="next-steps"></a><span data-ttu-id="507e2-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="507e2-126">Next steps</span></span>
* [<span data-ttu-id="507e2-127">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="507e2-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="507e2-128">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="507e2-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="507e2-129">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="507e2-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="507e2-130">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="507e2-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
