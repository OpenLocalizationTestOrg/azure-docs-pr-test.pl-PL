---
title: "aaaUsing Ruby w aplikacji sieci Web usługi aplikacji Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Używanie Ruby w aplikacji sieci Web usługi aplikacji Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, często zadawane pytania, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="60605-104">W aplikacji sieci Web w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="60605-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="60605-105">Z hello najnowszych aktualizacji tooour wewnętrznej bazy danych wprowadzono obsługę v.2.3 dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="60605-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="60605-106">Przez ustawienie hello konfigurację aplikacji sieci web systemu Linux można zmienić hello stosu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60605-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="60605-107">Przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="60605-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="60605-108">Z menu Nowy hello w hello [portalu Azure](https://portal.azure.com), można wybrać toocreate aplikacji sieci Web w systemie Linux Witaj Web + opcji mobilnych pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="60605-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Rozpocznij tworzenie aplikacji sieci web na powitania portalu Azure][1]

<span data-ttu-id="60605-110">Następnie hello **bloku Utwórz** otwiera pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="60605-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![bloku Utwórz Hello][2]

1. <span data-ttu-id="60605-112">Nadaj nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="60605-112">Give your web app a name.</span></span>
2. <span data-ttu-id="60605-113">Wybierz istniejącą grupę zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="60605-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="60605-114">(Zobacz dostępnych regionów w hello [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="60605-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="60605-115">Wybierz istniejący plan usługi aplikacji Azure lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="60605-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="60605-116">(Zobacz uwagi planu usługi aplikacji w hello [sekcji ograniczenia](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="60605-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="60605-117">Wybierz hello Ruby z hello stosów wbudowanych środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="60605-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="60605-118">Po utworzeniu aplikacji sieci web dopisków fonetycznych pobiera można wdrożyć tooit przy użyciu narzędzia Git i FTP.</span><span class="sxs-lookup"><span data-stu-id="60605-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="60605-119">więcej informacji o toolearn tworzenie aplikacji dopisków fonetycznych, sprawdź hello [przewodnika get](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="60605-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="60605-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60605-120">Next steps</span></span>
* [<span data-ttu-id="60605-121">Co to jest aplikacja sieci Web w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="60605-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="60605-122">Lokalnego wdrożenia Git tooAzure usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="60605-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="60605-123">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="60605-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="60605-124">Tworzenie aplikacji dopisków fonetycznych w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="60605-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png