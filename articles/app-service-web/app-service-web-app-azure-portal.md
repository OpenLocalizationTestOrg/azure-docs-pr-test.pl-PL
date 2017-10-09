---
title: aaaReference do nawigowania hello portalu Azure
description: "Dowiedz się hello możliwości różnych użytkowników dla aplikacji sieci Web usługi między hello portalu zarządzania i hello portalu Azure"
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
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a><span data-ttu-id="6b221-103">Odwołanie do nawigowania hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b221-103">Reference for navigating hello Azure portal</span></span>
<span data-ttu-id="6b221-104">Witryn sieci Web Azure są teraz nazywane [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="6b221-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="6b221-105">Aktualizujemy wszystkie tooreflect naszej dokumentacji tej nazwy zmiany i tooprovide instrukcje hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b221-105">We're updating all of our documentation tooreflect this name change and tooprovide instructions for hello Azure Portal.</span></span> <span data-ttu-id="6b221-106">Dopóki ten proces odbywa się, można użyć tego dokumentu jako wskazówki dotyczące pracy z aplikacjami sieci Web w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6b221-106">Until that process is done, you can use this document as a guide for working with Web Apps in hello Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a><span data-ttu-id="6b221-107">przyszłość Hello hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b221-107">hello future of hello Azure Classic Portal</span></span>
<span data-ttu-id="6b221-108">Podczas zauważysz hello znakowania zmian na powitania klasycznego portalu Azure tego portalu jest proces hello zastępowane przez hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b221-108">While you will notice hello branding changes on hello Azure Classic Portal, that portal is in hello process of being replaced by hello Azure Portal.</span></span> <span data-ttu-id="6b221-109">Zgodnie z klasycznego portalu hello jest obecnie wycofywane, hello fokusu dla nowych aplikacji jest przesunięcie toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b221-109">As hello classic portal is being phased out, hello focus for new development is shifting toohello Azure Portal.</span></span> <span data-ttu-id="6b221-110">Wszystkie nowe funkcje nadchodzących dla aplikacji sieci Web będą dostępne w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b221-110">All upcoming new features for Web Apps will come in hello Azure Portal.</span></span> <span data-ttu-id="6b221-111">Zacznij używać hello Azure Portal tootake zaletą hello najnowszej i najlepszej, że aplikacje sieci Web mają toooffer.</span><span class="sxs-lookup"><span data-stu-id="6b221-111">Start using hello Azure Portal tootake advantage of hello latest and greatest that Web Apps have toooffer.</span></span>

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="6b221-112">Układ różnice między hello klasycznego portalu Azure i portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b221-112">Layout differences between hello Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="6b221-113">W portalu klasycznym hello wszystkie hello Azure usługi są wyświetlane na powitania lewą stronę.</span><span class="sxs-lookup"><span data-stu-id="6b221-113">In hello classic portal, all hello Azure services are listed on hello left hand side.</span></span> <span data-ttu-id="6b221-114">Nawigacja w portalu klasycznym hello następuje struktury drzewa, gdzie uruchomić z usługi hello i przejdź do każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="6b221-114">Navigation in hello classic portal follows a tree structure, where you start from hello service and navigate into each element.</span></span> <span data-ttu-id="6b221-115">Ta struktura działa dobrze w przypadku, gdy zarządzanie składnikami niezależne.</span><span class="sxs-lookup"><span data-stu-id="6b221-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="6b221-116">Jednak aplikacje utworzone na platformie Azure są kolekcja połączonych usług i ta struktura drzewa nie jest idealne rozwiązanie w przypadku pracy z kolekcji usług.</span><span class="sxs-lookup"><span data-stu-id="6b221-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="6b221-117">Hello portalu Azure umożliwia łatwe toobuild aplikacji end-to-end ze składnikami z wielu usług.</span><span class="sxs-lookup"><span data-stu-id="6b221-117">hello Azure portal makes it easy toobuild applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="6b221-118">Hello portal jest zorganizowana jako *podróże*.</span><span class="sxs-lookup"><span data-stu-id="6b221-118">hello portal is organized as *journeys*.</span></span> <span data-ttu-id="6b221-119">A *podróży* jest szereg *bloków*, które są kontenerami dla hello różnych składników.</span><span class="sxs-lookup"><span data-stu-id="6b221-119">A *journey* is a series of *blades*, which are containers for hello different components.</span></span> <span data-ttu-id="6b221-120">Na przykład ustawienie automatyczne skalowanie aplikacji sieci web jest *podróży* który przejście kilku bloków pokazane na powitania poniższy przykład: hello **witryny sieci web** bloku (czy Tytuł bloku nie został jeszcze zaktualizowany toouse Witaj terminologii nowy), hello **ustawienia** bloku i hello **skalowanie w poziomie** bloku.</span><span class="sxs-lookup"><span data-stu-id="6b221-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in hello following example: hello **web-site** blade (that blade title has not yet been updated toouse hello new terminology), hello **Settings** blade, and hello **Scale out** blade.</span></span> <span data-ttu-id="6b221-121">W przykładzie hello automatyczne skalowanie jest konfigurowana toodepend na użycie procesora CPU, więc jest również **procent użycia procesora CPU** bloku.</span><span class="sxs-lookup"><span data-stu-id="6b221-121">In hello example, auto scaling is being set up toodepend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="6b221-122">Witaj składniki w ramach hello *bloków* są nazywane *części*, który wygląda jak kafelki.</span><span class="sxs-lookup"><span data-stu-id="6b221-122">hello components within hello *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="6b221-123">Przykład nawigacji: tworzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="6b221-123">Navigation example: create a web app</span></span>
<span data-ttu-id="6b221-124">Tworzenie nowej aplikacji sieci web jest nadal tak proste, jak 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="6b221-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="6b221-125">powitania po obraz pokazuje hello klasycznego portalu i hello portalu side-by-side toodemonstrate zmodyfikowaną nie znacznie hello liczbę czynności potrzebne tooget aplikacji sieci web w górę i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6b221-125">hello following image shows hello classic portal and hello portal side-by-side toodemonstrate that not much has changed in hello number of steps needed tooget a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="6b221-126">W portalu hello są dostępne z hello najbardziej typowych aplikacji sieci web, w tym galerii popularnych aplikacji, takich jak WordPress.</span><span class="sxs-lookup"><span data-stu-id="6b221-126">In hello portal you can choose from hello most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="6b221-127">Aby uzyskać pełną listę dostępnych aplikacji, odwiedź stronę hello [portalu Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="6b221-127">For a full list of available applications, visit hello [Azure Marketplace].</span></span>

<span data-ttu-id="6b221-128">Podczas tworzenia aplikacji sieci web, określ adres URL, plan usługi aplikacji i lokalizację w portalu hello tak samo jak to zrobić w klasycznym portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6b221-128">When you create a web app, you specify URL, App Service plan, and location in hello portal just as you do in hello classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="6b221-129">Ponadto hello portal pozwala zdefiniować inne typowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6b221-129">In addition, hello portal lets you define other common settings.</span></span> <span data-ttu-id="6b221-130">Na przykład [grup zasobów](../azure-resource-manager/resource-group-overview.md) on toosee proste i zarządzanie nimi powiązanych zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b221-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple toosee and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="6b221-131">Przykład nawigacji: ustawienia i funkcje</span><span class="sxs-lookup"><span data-stu-id="6b221-131">Navigation example: settings and features</span></span>
<span data-ttu-id="6b221-132">Witaj wszystkie ustawienia i funkcje teraz są logicznie pogrupowane w jednej bloku, w którym można nawigować.</span><span class="sxs-lookup"><span data-stu-id="6b221-132">All hello settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="6b221-133">Na przykład można utworzyć domeny niestandardowe, klikając **domen niestandardowych i SSL** w hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="6b221-133">For example, you can create custom domains by clicking **Custom domains and SSL** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="6b221-134">tooset się alert monitorowania, kliknij przycisk **żądań i błędów** , a następnie **dodać Alert**.</span><span class="sxs-lookup"><span data-stu-id="6b221-134">tooset up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="6b221-135">Diagnostyka tooenable, kliknij przycisk **dzienników diagnostycznych** w hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="6b221-135">tooenable diagnostics, click **Diagnostics logs** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="6b221-136">Ustawienia aplikacji tooconfigure, kliknij przycisk **ustawienia aplikacji** w hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="6b221-136">tooconfigure application settings, click **Application settings** in hello **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="6b221-137">Inna niż nazwa marki hello, kilka czynności w portalu hello został przeniesiony lub pogrupowane inaczej toomake go toofind łatwiej je.</span><span class="sxs-lookup"><span data-stu-id="6b221-137">Other than hello brand name, a few things in hello portal have been renamed or grouped differently toomake it easier toofind them.</span></span> <span data-ttu-id="6b221-138">Na przykład poniżej przedstawiono zrzut ekranu hello strony odpowiednie dla ustawienia aplikacji (**Konfiguruj**) w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="6b221-138">For example, below is a screenshot of hello corresponding page for app settings (**Configure**) in hello classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="6b221-139">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="6b221-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
[portalu Azure Marketplace]: /marketplace/

> [!NOTE]
> <span data-ttu-id="6b221-141">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="6b221-141">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6b221-142">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="6b221-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="6b221-143">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="6b221-143">What's changed</span></span>
* <span data-ttu-id="6b221-144">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6b221-144">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

