---
title: "Odwołanie do nawigowania portalu Azure"
description: "Dowiedz się więcej możliwości różnych użytkowników dla aplikacji sieci Web usługi między portalu zarządzania i portalu Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="67c91-103">Odwołanie do nawigowania portalu Azure</span><span class="sxs-lookup"><span data-stu-id="67c91-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="67c91-104">Witryn sieci Web Azure są teraz nazywane [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="67c91-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="67c91-105">Aktualizujemy wszystkie naszej dokumentacji w celu odzwierciedlenia tej zmiany nazwy i zapewniające instrukcje dotyczące portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c91-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="67c91-106">Dopóki ten proces odbywa się, można użyć tego dokumentu jako wskazówki dotyczące pracy z aplikacjami sieci Web w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c91-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="67c91-107">Przyszłość klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="67c91-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="67c91-108">Gdy zauważysz zmiany znakowania w portalu klasycznym Azure tego portalu trwa zastępowane przez Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="67c91-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="67c91-109">Zgodnie z klasycznego portalu są obecnie wycofywane, fokus dla nowych aplikacji jest zmieni się do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c91-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="67c91-110">Wszystkie nowe funkcje nadchodzących dla aplikacji sieci Web rozpocznie się w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c91-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="67c91-111">Uruchom przy użyciu portalu Azure, aby móc korzystać z najnowszej i najlepszej, że aplikacje sieci Web mają do zaoferowania.</span><span class="sxs-lookup"><span data-stu-id="67c91-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="67c91-112">Układ różnice między klasycznego portalu Azure i portalu Azure</span><span class="sxs-lookup"><span data-stu-id="67c91-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="67c91-113">W klasycznym portalu usług Azure znajduje się na lewą stronę.</span><span class="sxs-lookup"><span data-stu-id="67c91-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="67c91-114">Nawigacja w klasycznym portalu następuje struktury drzewa, gdzie uruchomić z usługi i przejdź do każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="67c91-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="67c91-115">Ta struktura działa dobrze w przypadku, gdy zarządzanie składnikami niezależne.</span><span class="sxs-lookup"><span data-stu-id="67c91-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="67c91-116">Jednak aplikacje utworzone na platformie Azure są kolekcja połączonych usług i ta struktura drzewa nie jest idealne rozwiązanie w przypadku pracy z kolekcji usług.</span><span class="sxs-lookup"><span data-stu-id="67c91-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="67c91-117">Azure portal ułatwia tworzenie aplikacji end-to-end ze składnikami z wielu usług.</span><span class="sxs-lookup"><span data-stu-id="67c91-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="67c91-118">Portalu są organizowane jako *podróże*.</span><span class="sxs-lookup"><span data-stu-id="67c91-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="67c91-119">A *podróży* jest szereg *bloków*, które są kontenerami dla różnych składników.</span><span class="sxs-lookup"><span data-stu-id="67c91-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="67c91-120">Na przykład ustawienie automatyczne skalowanie aplikacji sieci web jest *podróży* który przejście kilku bloków jak pokazano w poniższym przykładzie: **witryny sieci web** bloku (czy Tytuł bloku ma jeszcze nie zostały zaktualizowane do używania nowych terminologia) **ustawienia** bloku i **skalowanie** bloku.</span><span class="sxs-lookup"><span data-stu-id="67c91-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="67c91-121">W tym przykładzie automatyczne skalowanie jest konfigurowany do są zależne od użycia procesora CPU, więc jest również **procent użycia procesora CPU** bloku.</span><span class="sxs-lookup"><span data-stu-id="67c91-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="67c91-122">Składniki w ramach *bloków* są nazywane *części*, który wygląda jak kafelki.</span><span class="sxs-lookup"><span data-stu-id="67c91-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="67c91-123">Przykład nawigacji: tworzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="67c91-123">Navigation example: create a web app</span></span>
<span data-ttu-id="67c91-124">Tworzenie nowej aplikacji sieci web jest nadal tak proste, jak 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="67c91-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="67c91-125">Na poniższej ilustracji przedstawiono portalu klasycznego i portalu side-by-side aby zademonstrować znacznie nie została zmieniona w liczbie kroki potrzebne do uruchomienia aplikacji sieci web i systemem.</span><span class="sxs-lookup"><span data-stu-id="67c91-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="67c91-126">W portalu można wybrać z najbardziej typowych aplikacji sieci web, w tym galerii popularnych aplikacji, takich jak WordPress.</span><span class="sxs-lookup"><span data-stu-id="67c91-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="67c91-127">Aby uzyskać pełną listę dostępnych aplikacji, odwiedź stronę [portalu Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="67c91-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="67c91-128">Podczas tworzenia aplikacji sieci web, określ adres URL, plan usługi aplikacji i lokalizację w portalu tak samo jak to zrobić w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="67c91-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="67c91-129">Ponadto portalu pozwala zdefiniować inne typowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="67c91-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="67c91-130">Na przykład [grup zasobów](../azure-resource-manager/resource-group-overview.md) ułatwiają wyświetlanie i zarządzanie nimi powiązanych zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c91-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="67c91-131">Przykład nawigacji: ustawienia i funkcje</span><span class="sxs-lookup"><span data-stu-id="67c91-131">Navigation example: settings and features</span></span>
<span data-ttu-id="67c91-132">Wszystkie ustawienia i funkcje teraz są logicznie pogrupowane w jednej bloku, w którym można nawigować.</span><span class="sxs-lookup"><span data-stu-id="67c91-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="67c91-133">Na przykład można utworzyć domeny niestandardowe, klikając **domen niestandardowych i SSL** w **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="67c91-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="67c91-134">Aby skonfigurować alert monitorowania, kliknij przycisk **żądań i błędów** , a następnie **dodać Alert**.</span><span class="sxs-lookup"><span data-stu-id="67c91-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="67c91-135">Aby włączyć diagnostykę, kliknij **dzienników diagnostycznych** w **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="67c91-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="67c91-136">Kliknij, aby skonfigurować ustawienia aplikacji **ustawienia aplikacji** w **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="67c91-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="67c91-137">Inna niż nazwa marki zostały zmieniona lub pogrupowane inaczej, aby ułatwić ich wyszukiwanie kilka czynności w portalu.</span><span class="sxs-lookup"><span data-stu-id="67c91-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="67c91-138">Na przykład poniżej przedstawiono zrzut ekranu strony odpowiednie dla ustawienia aplikacji (**Konfiguruj**) w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="67c91-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="67c91-139">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="67c91-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="67c91-140">[portalu Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="67c91-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="67c91-141">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="67c91-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="67c91-142">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="67c91-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="67c91-143">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="67c91-143">What's changed</span></span>
* <span data-ttu-id="67c91-144">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="67c91-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

