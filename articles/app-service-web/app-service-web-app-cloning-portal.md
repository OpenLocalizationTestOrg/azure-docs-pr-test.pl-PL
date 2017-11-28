---
title: "aaaWeb w klonowania aplikacji przy użyciu portalu Azure"
description: "Dowiedz się, jak tooclone toonew Twojej aplikacji sieci Web aplikacji sieci Web przy użyciu portalu Azure."
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="90eb5-103">Usługa aplikacji Azure aplikacji klonowania za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="90eb5-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="90eb5-104">Funkcja w klonowania Hello [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) umożliwia łatwe sklonować istniejącej aplikacji sieci web apps tooa nowo utworzony w innym regionie lub hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="90eb5-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="90eb5-105">Spowoduje to włączenie toodeploy klientów liczba aplikacji w różnych regionach, szybkie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="90eb5-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="90eb5-106">Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium.</span><span class="sxs-lookup"><span data-stu-id="90eb5-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="90eb5-107">Hello nowej używa funkcji hello takie same ograniczenia co funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="90eb5-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="90eb5-108">Klonowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="90eb5-108">Cloning an existing App</span></span>
<span data-ttu-id="90eb5-109">Witaj aplikacji sieci web musi być uruchomiona w hello **Premium** tryb aby toocreate klonowania dla aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="90eb5-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="90eb5-110">W hello [Azure Portal](https://portal.azure.com/), otwarcie bloku aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="90eb5-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="90eb5-111">Kliknij przycisk **narzędzia**.</span><span class="sxs-lookup"><span data-stu-id="90eb5-111">Click **Tools**.</span></span> <span data-ttu-id="90eb5-112">Następnie w hello **narzędzia** bloku, kliknij przycisk **aplikacji w klonowania**.</span><span class="sxs-lookup"><span data-stu-id="90eb5-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="90eb5-113">Jeśli hello aplikacji sieci web nie jest już hello **Premium** tryb, zostanie wyświetlony komunikat informujący o hello obsługiwane tryby aplikacji klonowania.</span><span class="sxs-lookup"><span data-stu-id="90eb5-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="90eb5-114">W tym momencie masz hello opcja tooselect **uaktualnienia**.</span><span class="sxs-lookup"><span data-stu-id="90eb5-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="90eb5-115">W hello **aplikacji w klonowania** bloku Podaj nazwę nowej aplikacji sieci web hello, grupy zasobów i Plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="90eb5-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="90eb5-116">Również hello użytkownik będzie możliwe toochoose czy tooclone szereg ustawień aplikacji sieci web źródła lub nie.</span><span class="sxs-lookup"><span data-stu-id="90eb5-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="90eb5-117">Po kliknięciu przycisku **utworzyć** platformy hello rozpoczęcia pracy na tworzenie własnego klonu hello źródłowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="90eb5-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="90eb5-118">Klonowanie tooan aplikacji istniejącego środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="90eb5-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="90eb5-119">W hello **aplikacji w klonowania** bloku powitania klienta będzie mieć hello opcja toochoose puli aplikacji w istniejącym środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90eb5-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="90eb5-120">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="90eb5-120">Current Restrictions</span></span>
<span data-ttu-id="90eb5-121">Ta funkcja jest obecnie w przeglądzie, pracujemy nad tooadd nowe funkcje w czasie, następujące listy hello są hello znane ograniczenia dotyczące obsługi bieżącego hello klonowania aplikacji w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="90eb5-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="90eb5-122">Ustawienia usługi Azure Traffic Manager nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="90eb5-123">Ustawienia skalowania automatycznego nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="90eb5-124">Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="90eb5-125">Ustawienia sieci Wirtualnej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="90eb5-126">Wgląd w aplikację nie są automatycznie skonfigurowane w aplikacji sieci web docelowym hello</span><span class="sxs-lookup"><span data-stu-id="90eb5-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="90eb5-127">Łatwe ustawienia uwierzytelniania nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="90eb5-128">Program kudu rozszerzenia nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="90eb5-129">Porada reguły nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="90eb5-130">Baza danych zawartości nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="90eb5-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="90eb5-131">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="90eb5-131">References</span></span>
* [<span data-ttu-id="90eb5-132">Klonowanie aplikacji sieci Web przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="90eb5-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="90eb5-133">Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="90eb5-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="90eb5-134">Jak tooCreate środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="90eb5-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="90eb5-135">Tworzenie aplikacji sieci Web w środowisku usługi App Service</span><span class="sxs-lookup"><span data-stu-id="90eb5-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="90eb5-136">Wprowadzenie tooApp środowiska usługi</span><span class="sxs-lookup"><span data-stu-id="90eb5-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
