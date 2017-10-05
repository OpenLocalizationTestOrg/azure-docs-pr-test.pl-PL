---
title: "Klonowanie aplikacji sieci Web przy użyciu portalu Azure"
description: "Dowiedz się, jak klonowanie aplikacji sieci Web do nowej aplikacji sieci Web przy użyciu portalu Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="8758c-103">Usługa aplikacji Azure aplikacji klonowania za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8758c-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="8758c-104">Funkcję klonowania w [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) umożliwia łatwe Sklonowanie istniejących sieci web aplikacji do nowo utworzonej aplikacji w innym regionie lub w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="8758c-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="8758c-105">Umożliwi to klienci mogą wdrożyć wiele aplikacji w różnych regionach, szybkie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="8758c-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="8758c-106">Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium.</span><span class="sxs-lookup"><span data-stu-id="8758c-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="8758c-107">Nowa funkcja używa tego samego ograniczenia jako funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="8758c-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="8758c-108">Klonowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8758c-108">Cloning an existing App</span></span>
<span data-ttu-id="8758c-109">Aplikacja sieci web musi być uruchomiona **Premium** trybu, aby możliwe utworzenia klona dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8758c-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="8758c-110">W [Azure Portal](https://portal.azure.com/), otwarcie bloku aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8758c-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="8758c-111">Kliknij przycisk **narzędzia**.</span><span class="sxs-lookup"><span data-stu-id="8758c-111">Click **Tools**.</span></span> <span data-ttu-id="8758c-112">Następnie w **narzędzia** bloku, kliknij przycisk **aplikacji w klonowania**.</span><span class="sxs-lookup"><span data-stu-id="8758c-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="8758c-113">Jeśli aplikacja sieci web nie jest już w **Premium** tryb, zostanie wyświetlony komunikat informujący o obsługiwanych tryby w klonowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8758c-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="8758c-114">W tym momencie masz możliwość wybrania **uaktualnienia**.</span><span class="sxs-lookup"><span data-stu-id="8758c-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="8758c-115">W **aplikacji w klonowania** bloku Podaj nazwę nowej aplikacji sieci web, grupy zasobów i Plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="8758c-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="8758c-116">Również użytkownik będzie mógł zdecydować się na potrzeby klonowania szereg ustawień aplikacji sieci web źródła lub nie.</span><span class="sxs-lookup"><span data-stu-id="8758c-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="8758c-117">Po kliknięciu przycisku **utworzyć** platformy rozpoczęcia pracy na tworzenie własnego klonu źródłowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8758c-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="8758c-118">Klonowanie istniejącej aplikacji do środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="8758c-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="8758c-119">W **aplikacji w klonowania** bloku klienta będzie mieć możliwość wyboru z puli aplikacji w istniejącym środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8758c-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="8758c-120">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="8758c-120">Current Restrictions</span></span>
<span data-ttu-id="8758c-121">Ta funkcja jest obecnie w przeglądzie, pracujemy, aby dodać nowe funkcje w czasie, poniżej są znane ograniczenia dotyczące obsługi bieżącego klonowania aplikacji w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="8758c-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="8758c-122">Ustawienia usługi Azure Traffic Manager nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="8758c-123">Ustawienia skalowania automatycznego nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="8758c-124">Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="8758c-125">Ustawienia sieci Wirtualnej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="8758c-126">Wgląd w aplikację nie są automatycznie skonfigurowane na docelowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="8758c-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="8758c-127">Łatwe ustawienia uwierzytelniania nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="8758c-128">Program kudu rozszerzenia nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="8758c-129">Porada reguły nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="8758c-130">Baza danych zawartości nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="8758c-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="8758c-131">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="8758c-131">References</span></span>
* [<span data-ttu-id="8758c-132">Klonowanie aplikacji sieci Web przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8758c-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="8758c-133">Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8758c-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="8758c-134">Jak utworzyć środowisko App Service Environment</span><span class="sxs-lookup"><span data-stu-id="8758c-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="8758c-135">Tworzenie aplikacji sieci Web w środowisku usługi App Service</span><span class="sxs-lookup"><span data-stu-id="8758c-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="8758c-136">Wprowadzenie do usługi App Service Environment</span><span class="sxs-lookup"><span data-stu-id="8758c-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
