---
title: "usługi w chmurze Azure z usługą Azure CDN aaaIntegrate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy usługi w chmurze służy do zawartości z punktu końcowego zintegrowane usługi Azure CDN"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="7a5d5-103"><a name="intro"></a>Integracja z usługą w chmurze z usługą Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="7a5d5-104">Usługi w chmurze można zintegrować z usługą Azure CDN, obsługująca zawartość z lokalizacji usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="7a5d5-105">To podejście umożliwia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="7a5d5-106">Łatwe wdrażanie i aktualizowanie obrazów, skrypty i arkusze stylów w katalogu projektu usługi chmury</span><span class="sxs-lookup"><span data-stu-id="7a5d5-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="7a5d5-107">Łatwo przeprowadzić uaktualnienie hello pakietów NuGet w usługi w chmurze, np. jQuery lub ładowania początkowego wersji</span><span class="sxs-lookup"><span data-stu-id="7a5d5-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="7a5d5-108">Zarządzanie aplikacji sieci Web i obsługiwane sieci CDN zawartości wszystkich z hello sam interfejs programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a5d5-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="7a5d5-109">Przepływ pracy ujednoliconego wdrożenia dla aplikacji sieci Web i zawartości obsługiwanych w sieci CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="7a5d5-110">Integracja z usługą Azure CDN ASP.NET tworzenie pakietów i minimalizowanie</span><span class="sxs-lookup"><span data-stu-id="7a5d5-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7a5d5-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="7a5d5-111">What you will learn</span></span>
<span data-ttu-id="7a5d5-112">W tym samouczku przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="7a5d5-113">Integracja punktu końcowego usługi Azure CDN z usługi w chmurze i udostępniać zawartość statyczną na stronach sieci Web z usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="7a5d5-114">Skonfiguruj ustawienia pamięci podręcznej zawartość statyczną w usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="7a5d5-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="7a5d5-115">Udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="7a5d5-116">Służą powiązane i zminimalizowane zawartości za pomocą usługi Azure CDN przy zachowaniu skryptu hello debugowanie w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a5d5-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="7a5d5-117">Skonfigurować powrotu skryptów i CSS z usługi Azure CDN jest w trybie offline</span><span class="sxs-lookup"><span data-stu-id="7a5d5-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="7a5d5-118">Zostanie utworzona</span><span class="sxs-lookup"><span data-stu-id="7a5d5-118">What you will build</span></span>
<span data-ttu-id="7a5d5-119">Wdrażania roli sieci Web usługi chmury, za pomocą hello domyślnego szablonu platformy ASP.NET MVC, Dodaj kod tooserve zawartości z zintegrowane usługi Azure CDN, takich jak obraz, wyniki akcji kontrolera i pliki obsługi języka JavaScript i CSS hello domyślnej i również napisać kod tooconfigure hello mechanizm rezerwowy umożliwiający pakiety obsługiwanych w przypadku hello tego hello CDN jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="7a5d5-120">Dane będą potrzebne</span><span class="sxs-lookup"><span data-stu-id="7a5d5-120">What you will need</span></span>
<span data-ttu-id="7a5d5-121">Ten samouczek ma hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="7a5d5-122">Aktywny [konta Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="7a5d5-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="7a5d5-123">Visual Studio 2015 z [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="7a5d5-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="7a5d5-124">Należy toocomplete konto platformy Azure w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="7a5d5-125">Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu kredytu możesz zachować konto hello i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="7a5d5-126">Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -subskrypcji Your MSDN otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="7a5d5-127">Wdrażanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="7a5d5-127">Deploy a cloud service</span></span>
<span data-ttu-id="7a5d5-128">W tej sekcji zostanie wdrażanie hello domyślnego szablonu aplikacji platformy ASP.NET MVC w roli programu Visual Studio 2015 tooa chmury usługi sieci Web i zintegrować ją z nowy punkt końcowy CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="7a5d5-129">Wykonaj poniższe instrukcje hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="7a5d5-130">W programie Visual Studio 2015, Utwórz nową usługę w chmurze Azure z paska menu hello przechodząc zbyt**pliku > Nowy > Projekt > chmura > usługi w chmurze Azure**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="7a5d5-131">Nadaj mu nazwę, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="7a5d5-132">Wybierz **roli sieci Web ASP.NET** i kliknij przycisk hello  **>**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="7a5d5-133">Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="7a5d5-134">Wybierz **MVC** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="7a5d5-135">Teraz Opublikuj ten tooan roli sieci Web usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="7a5d5-136">Kliknij prawym przyciskiem myszy projekt usługi w chmurze hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="7a5d5-137">Jeśli dany komputer nie ma jeszcze podpisany w Microsoft Azure, kliknij przycisk hello **Dodaj konto...**  hello listy rozwijanej, a następnie kliknij przycisk **Dodaj konto** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="7a5d5-138">W hello strony logowania Zaloguj się przy użyciu hello konta Microsoft użyty tooactivate konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="7a5d5-139">Gdy użytkownik jest zarejestrowany, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="7a5d5-140">Przy założeniu, że nie utworzono konta usługi lub magazynu chmury, Visual Studio pomoże utworzyć jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="7a5d5-141">W hello **Tworzenie usługi w chmurze i konto** okna dialogowego, nazwa żądanej usługi hello typu i hello wybierz odpowiedni region.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="7a5d5-142">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="7a5d5-143">W hello strona ustawień publikowania, sprawdź konfigurację hello i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="7a5d5-144">Witaj proces publikowania dla usługi w chmurze zajmuje dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="7a5d5-145">wprowadzić Hello Włącz narzędzia Web Deploy w dla wszystkich ról opcji debugowania usługi w chmurze znacznie szybsza, bo zapewniając tooyour aktualizacje szybkiego (ale tymczasowe) role sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="7a5d5-146">Aby uzyskać więcej informacji na temat tej opcji, zobacz [publikowania usługi w chmurze przy użyciu narzędzia Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="7a5d5-147">Gdy hello **dziennik aktywności programu Microsoft Azure** pokazuje, że stan publikowania **Ukończono**, spowoduje utworzenie punktu końcowego usługi CDN, który jest zintegrowany z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="7a5d5-148">Jeśli po opublikowaniu hello wdrożona usługa w chmurze wyświetla komunikat o błędzie, prawdopodobnie ponieważ korzysta z usługi w chmurze hello wdrożeniu [gościa systemu operacyjnego, który nie obejmuje .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="7a5d5-149">Można obejść ten problem przez [wdrażanie .NET 4.5.2 jako zadanie uruchamiania](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="7a5d5-150">Tworzenie nowego profilu CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-150">Create a new CDN profile</span></span>
<span data-ttu-id="7a5d5-151">Profil CDN jest kolekcją punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="7a5d5-152">Każdy profil zawiera jeden lub więcej punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="7a5d5-153">Możesz toouse wiele profilów tooorganize punktami końcowymi CDN według domeny internetowej, aplikacji sieci web lub innych kryteriów.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="7a5d5-154">Jeśli masz już profil CDN ma toouse w tym samouczku, kontynuować zbyt[utworzyć nowy punkt końcowy CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="7a5d5-155">Tworzenie nowego punktu końcowego usługi CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="7a5d5-156">**toocreate nowy punkt końcowy CDN dla konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="7a5d5-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="7a5d5-157">W hello [portalu zarządzania Azure](https://portal.azure.com), przejdź tooyour profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="7a5d5-158">Użytkownik może został on przypięty toohello pulpitu nawigacyjnego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="7a5d5-159">Jeśli użytkownik nie, możesz go znaleźć, klikając **Przeglądaj**, następnie **profilów usługi CDN**, i klikając profil hello planujesz tooadd punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="7a5d5-160">zostanie wyświetlony blok profilu CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-160">hello CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="7a5d5-162">Kliknij przycisk hello **Dodawanie punktu końcowego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Przycisk dodawania punktu końcowego][cdn-new-endpoint-button]
   
    <span data-ttu-id="7a5d5-164">Witaj **Dodawanie punktu końcowego** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Blok dodawania punktu końcowego][cdn-add-endpoint]
3. <span data-ttu-id="7a5d5-166">Wprowadź **nazwę** dla tego punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="7a5d5-167">Ta nazwa będzie używana tooaccess buforowanych zasobów w domenie hello `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="7a5d5-168">W hello **typ źródła** listy rozwijanej wybierz *usługi w chmurze*.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="7a5d5-169">W hello **nazwę hosta źródła** listy rozwijanej wybierz usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="7a5d5-170">Pozostaw ustawienia domyślne hello **ścieżki źródła**, **nagłówka hosta źródła**, i **port protokołu/źródła**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="7a5d5-171">Należy określić co najmniej jeden protokół (HTTP lub HTTPS).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="7a5d5-172">Kliknij przycisk hello **Dodaj** toocreate przycisk hello nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="7a5d5-173">Po utworzeniu punktu końcowego hello pojawia się na liście punktów końcowych dla profilu hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="7a5d5-174">Widok listy Hello pokazuje tooaccess toouse adres URL hello w pamięci podręcznej zawartości, a także domeny źródła hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Punkt końcowy usługi CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="7a5d5-176">punkt końcowy Hello nie natychmiast będą dostępne do użycia.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="7a5d5-177">Too90 minut toopropagate rejestracji hello hello sieci CDN może potrwać.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="7a5d5-178">Użytkownicy, którzy natychmiast podjąć próbę nazwy domeny usługi CDN hello toouse może zostać wyświetlony kod stanu 404, dopóki hello zawartość jest dostępna za pośrednictwem hello CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="7a5d5-179">Test hello punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="7a5d5-180">Gdy stan publikowania hello jest **Ukończono**, Otwórz okno przeglądarki i przejść za**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="7a5d5-181">Moje ustawienia ten adres URL jest:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="7a5d5-182">Które odpowiada toohello po źródłowy adres URL w punkcie końcowym CDN hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="7a5d5-183">Po przejściu się zbyt**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, w zależności od przeglądarki, będzie zostanie wyświetlony monit o toodownload lub Otwórz hello bootstrap.css który pochodzi z opublikowanych aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="7a5d5-184">Podobnie można uzyskać dostępu do dowolny publicznie dostępny adres URL w  **http://*&lt;serviceName >*.cloudapp.net/** bezpośrednio z punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="7a5d5-185">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-185">For example:</span></span>

* <span data-ttu-id="7a5d5-186">Pliku ze ścieżki/Script hello js</span><span class="sxs-lookup"><span data-stu-id="7a5d5-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="7a5d5-187">Dowolny plik zawartości z hello argumencie / ścieżki</span><span class="sxs-lookup"><span data-stu-id="7a5d5-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="7a5d5-188">Wszelkie kontrolera/działania</span><span class="sxs-lookup"><span data-stu-id="7a5d5-188">Any controller/action</span></span>
* <span data-ttu-id="7a5d5-189">Jeśli ciąg zapytania hello jest włączona na punkt końcowy CDN dowolny adres URL z ciągami zapytań</span><span class="sxs-lookup"><span data-stu-id="7a5d5-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="7a5d5-190">W rzeczywistości z hello powyżej konfiguracji, może obsługiwać usługę chmury całego hello w  **http://*&lt;cdnName >*.azureedge.net/**. Jeśli można przejść za**http://camservice.azureedge.net/ ** pobrać hello wyniku akcji z głównej/indeksu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="7a5d5-191">Oznacza to, mimo że zawsze jest dobrym rozwiązaniem tooserve usługi w chmurze całego za pośrednictwem usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="7a5d5-192">CDN z optymalizacją dostarczania statycznych nie zawsze przyspiesza dostarczania dynamiczne zasoby, które nie mają w pamięci podręcznej toobe lub bardzo często są aktualizowane, ponieważ hello CDN musi ściągnięcia nowej wersji hello zasobów z serwera źródłowego hello bardzo często.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="7a5d5-193">W tym scenariuszu można włączyć [dynamiczne przyspieszenie lokacji](cdn-dynamic-site-acceleration.md) optymalizacji (DSA) na punkt końcowy CDN używający różnych technik toospeed dostarczenia-buforowalnej zasobów dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="7a5d5-194">Jeśli masz lokacji z różnymi statycznych i dynamicznych zawartości można tooserve zawartość statyczną z sieci CDN z typem optymalizacji statyczne (np. dostarczenie ogólne sieci web), a zawartość dynamiczną tooserve bezpośrednio z serwera źródłowego hello lub za pośrednictwem sieci CDN punkt końcowy z optymalizacją DSA włączone w przypadku.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="7a5d5-195">końcowy toothat ma już widoczny, jak tooaccess zawartość poszczególnych plików z punktu końcowego CDN hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="7a5d5-196">I opisano sposób tooserve akcji kontrolera określonej za pomocą określonego punktu końcowego sieci CDN w obsługiwać zawartość z akcji kontrolera, za pomocą usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="7a5d5-197">Alternatywą Hello jest toodetermine, którego zawartość tooserve z usługi Azure CDN na podstawie przypadku — w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="7a5d5-198">końcowy toothat ma już widoczny, jak tooaccess zawartość poszczególnych plików z punktu końcowego CDN hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="7a5d5-199">I opisano, jak tooserve akcji kontrolera określonej za pomocą hello punkt końcowy sieci CDN w [udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="7a5d5-200">Skonfiguruj opcje buforowania plików statycznych w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="7a5d5-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="7a5d5-201">Azure CDN integracji usługi w chmurze można określić sposób statycznych toobe zawartości w pamięci podręcznej w hello punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="7a5d5-202">toodo, otwórz *Web.config* z roli sieci Web projektu (np. WebRole1) i Dodaj `<staticContent>` element zbyt`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="7a5d5-203">Witaj XML poniżej konfiguruje hello tooexpire pamięci podręcznej w 3 dni.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="7a5d5-204">Po wykonaniu tej czynności wszystkie pliki statyczne z usługi w chmurze będzie obserwować hello same reguły w pamięci podręcznej usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="7a5d5-205">Bardziej szczegółowego kontrolowania ustawień pamięci podręcznej, należy dodać *Web.config* plików do folderu, a następnie dodaj ustawienia istnieje.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="7a5d5-206">Na przykład dodać *Web.config* pliku toohello *\Content* folderu i Zamień hello zawartości z powitania po XML:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="7a5d5-207">To ustawienie powoduje, że wszystkie pliki statyczne z hello *\Content* toobe folderu pamięci podręcznej przez 15 dni.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="7a5d5-208">Aby uzyskać więcej informacji na temat tooconfigure hello `<clientCache>` elementu, zobacz [pamięci podręcznej klienta &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="7a5d5-209">W [udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN](#controller), można również opisano, jak można skonfigurować ustawienia pamięci podręcznej dla wyników akcji kontrolera w hello CDN pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="7a5d5-210">Udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="7a5d5-211">Po zintegrowaniu rolę sieci Web usługi w chmurze z usługą Azure CDN jest stosunkowo łatwa tooserve zawartości z akcji kontrolera za pośrednictwem hello Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="7a5d5-212">Inne niż obsługująca chmury usługi bezpośrednio za pomocą usługi Azure CDN (zostało to pokazane powyżej), [Maarten Balliauw](https://twitter.com/maartenballiauw) przedstawiono toodo go to MemeGenerator kontrolera w [zmniejsza opóźnienie w sieci web hello z hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="7a5d5-213">I będzie po prostu go odtworzyć w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="7a5d5-214">Załóżmy, że w usłudze w chmurze ma memes toogenerate na podstawie małych obrazu Norris Jan (photo przez [światła Alan](http://www.flickr.com/photos/alan-light/218493788/)), takich jak to:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="7a5d5-215">Masz prostą `Index` akcję, która umożliwia klientom Witaj superlatywy hello toospecify w obrazie hello następnie generuje meme powitania po przesyłać toohello akcji.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="7a5d5-216">Ponieważ jest Norris Jan, można oczekiwać toobecome tej strony bardzo popularny globalnie.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="7a5d5-217">Jest to przykład obsługę częściowo dynamicznej zawartości z usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="7a5d5-218">Wykonaj kroki hello powyżej toosetup tej akcji kontrolera:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="7a5d5-219">W hello *\Controllers* folderu, Utwórz nowy plik .cs o nazwie *MemeGeneratorController.cs* i Zastąp hello zawartości z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="7a5d5-220">Należy się tooreplace hello wyróżnione części z nazwy CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="7a5d5-221">Kliknij prawym przyciskiem myszy domyślne hello `Index()` akcji i wybierz **Dodaj widok**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="7a5d5-222">Zaakceptuj ustawienia hello poniżej i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="7a5d5-223">Otwórz nowy hello *Views\MemeGenerator\Index.cshtml* i Zastąp zawartość hello powitania od prostego HTML składania superlatywy hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="7a5d5-224">Ponownie opublikować hello usługi w chmurze i przejdź zbyt**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="7a5d5-225">Podczas przesyłania wartości formularza hello zbyt`/MemeGenerator/Index`, hello `Index_Post` metoda akcji zwraca toohello łącze `Show` metodę akcji za pomocą hello odpowiednich identyfikator wejściowy.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="7a5d5-226">Po kliknięciu łącza hello przejściu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="7a5d5-227">Jeśli lokalne debuger jest dołączony, zostanie wyświetlona hello regularne debugowania środowisko przy użyciu przekierowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="7a5d5-228">Jeśli jest on uruchomiony hello w usłudze w chmurze, następnie go spowoduje przekierowanie do:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="7a5d5-229">Które odpowiada toohello po źródłowy adres URL na punkt końcowy CDN:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="7a5d5-230">Następnie można użyć hello `OutputCacheAttribute` atrybutu na powitania `Generate` toospecify metody jak mają być buforowane hello wynik akcji, które podlegają Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="7a5d5-231">Poniższy kod Hello Określ pamięci podręcznej ważności 1 godzina (3600 sekund).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="7a5d5-232">Podobnie użytkownik może służyć się zawartość z dowolnego akcji kontrolera w usłudze w chmurze za pośrednictwem sieci Azure CDN z opcją buforowania hello potrzeby.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="7a5d5-233">W następnej sekcji hello I opisano sposób tooserve hello powiązane i zminimalizowane skryptów i CSS za pomocą usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="7a5d5-234">Integracja z usługą Azure CDN ASP.NET tworzenie pakietów i minimalizowanie</span><span class="sxs-lookup"><span data-stu-id="7a5d5-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="7a5d5-235">Arkusze stylów CSS i skrypty Zmień rzadko i głównym nadają się do hello Azure CDN pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="7a5d5-236">Obsługa hello całej roli sieci Web za pomocą programu Azure CDN jest hello Najprostszym sposobem toointegrate tworzenie pakietów i minimalizowanie z usługą Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="7a5d5-237">Jednak można dowolnie może nie toodo to, I opisano, jak toodo go przy zachowaniu hello potrzeby środowisko programistyczne ASP.NET tworzenie pakietów i minimalizowanie, takich jak:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="7a5d5-238">Środowisko trybu dużą debugowania</span><span class="sxs-lookup"><span data-stu-id="7a5d5-238">Great debug mode experience</span></span>
* <span data-ttu-id="7a5d5-239">Prostsze wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7a5d5-239">Streamlined deployment</span></span>
* <span data-ttu-id="7a5d5-240">Tooclients natychmiastowej aktualizacji dla uaktualnienia wersji skryptu/CSS</span><span class="sxs-lookup"><span data-stu-id="7a5d5-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="7a5d5-241">Mechanizm rezerwowy, gdy punkt końcowy CDN nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="7a5d5-242">Minimalizowanie modyfikacji kodu</span><span class="sxs-lookup"><span data-stu-id="7a5d5-242">Minimize code modification</span></span>

<span data-ttu-id="7a5d5-243">W hello **WebRole1** projektu, który został utworzony w [integracji punktu końcowego usługi Azure CDN z witryny sieci Web platformy Azure i udostępniać zawartość statyczną na stronach sieci Web z usługi Azure CDN](#deploy), otwórz *App_Start\ BundleConfig.cs* i spójrz na powitania `bundles.Add()` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="7a5d5-244">Witaj najpierw `bundles.Add()` instrukcja dodaje pakiet skryptu w katalogu wirtualnego hello `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="7a5d5-245">Następnie otwórz *Views\Shared\_Layout.cshtml* toosee sposób renderowania tagu pakietu skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="7a5d5-246">Powinny być hello stanie toofind po wierszu kodu Razor:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="7a5d5-247">Po uruchomieniu tego kodu Razor w roli sieci Web Azure hello będą zawierały `<script>` tagu hello skryptu pakietu podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="7a5d5-248">Jednak gdy jest uruchamiana w programie Visual Studio, wpisując `F5`, go spowoduje, że każdy plik skryptu w pakiecie hello pojedynczo (w przypadku hello powyżej, skryptu tylko jeden plik jest w pakiecie hello):</span><span class="sxs-lookup"><span data-stu-id="7a5d5-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="7a5d5-249">Dzięki temu możesz kod JavaScript hello toodebug w środowisku projektowania podczas zmniejszenie połączeń współbieżnych klienta (grupowania) i poprawy pliku Pobierz wydajności (minimalizowanie) w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="7a5d5-250">Jest toopreserve wspaniałych funkcji, dzięki integracji usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="7a5d5-251">Ponadto, ponieważ hello renderowane pakietu już zawiera ciąg wersji automatycznie wygenerowaną, ma tooreplicate, które funkcje tak hello po zaktualizowaniu wersji jQuery za pośrednictwem pakietu NuGet, mogą być aktualizowane po stronie klienta hello jak najszybciej możliwe.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="7a5d5-252">Wykonaj kroki hello poniżej toointegration ASP.NET tworzenie pakietów i minimalizowanie z punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="7a5d5-253">W *App_Start\BundleConfig.cs*, zmodyfikuj hello `bundles.Add()` toouse metody innej [Konstruktor pakietu](http://msdn.microsoft.com/library/jj646464.aspx), który określa adres usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="7a5d5-254">toodo hello, Zastąp `RegisterBundles` definicję metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="7a5d5-255">Należy się tooreplace `<yourCDNName>` hello nazwą Twojej usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="7a5d5-256">Prosty opis ustawienie `bundles.UseCdn = true` i dodać dokładnie przygotowanego pakietu tooeach adresu CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="7a5d5-257">Na przykład hello pierwszy konstruktora w kodzie hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="7a5d5-258">jest hello taki sam jak:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="7a5d5-259">Ten konstruktor informuje ASP.NET tworzenie pakietów i minimalizowanie toorender skryptu poszczególnych plików podczas debugowania lokalnie, ale użyj hello określona zagrożona skryptu hello tooaccess adresu CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="7a5d5-260">Zwróć jednak uwagę dwie najważniejsze czynniki z dokładnie przygotowanego CDN adres URL:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="7a5d5-261">Hello źródła dla tego adresu URL usługi CDN jest `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, który jest rzeczywiście hello katalog wirtualny hello skryptu pakietu w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="7a5d5-262">Ponieważ używasz konstruktora CDN hello tag skryptu CDN dla pakietu hello nie zawiera już hello są generowane automatycznie ciąg wersji w hello renderowane adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="7a5d5-263">Musisz ręcznie wygenerować ciąg wersji unikatowy każdorazowego pakiet skryptu hello jest zmodyfikowany tooforce pamięci podręcznej pominięte w sieci Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="7a5d5-264">At hello sam czas ten ciąg wersji unikatowy musi pozostać niezmienione za pośrednictwem życia hello hello wdrożenia toomaximize trafień w pamięci podręcznej w sieci Azure CDN, po wdrożeniu pakietu hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="7a5d5-265">Witaj ciągu zapytania v = < W.X.Y.Z > ściąga z *Properties\AssemblyInfo.cs* w projekcie roli sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="7a5d5-266">Przepływ pracy wdrożenia, który zawiera przyrostową wersję zestawu hello każdym publikowaniu tooAzure może mieć.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="7a5d5-267">Lub, można zmodyfikować *Properties\AssemblyInfo.cs* w ciągu wersji projektu tooautomatically przyrostu hello za każdym razem, gdy kompilacji, przy użyciu hello wieloznaczny "*".</span><span class="sxs-lookup"><span data-stu-id="7a5d5-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="7a5d5-268">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-268">For example:</span></span>
     
        <span data-ttu-id="7a5d5-269">[zestawu: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="7a5d5-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="7a5d5-270">Wszystkie inne toostreamline strategii generowania unikatowy ciąg dla hello życia wdrożenia będzie działać w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="7a5d5-271">Ponownie opublikować hello chmury dostępu i usługa hello strony głównej.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="7a5d5-272">Widok hello kodu HTML dla strony hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="7a5d5-273">Powinno być możliwe toosee hello renderowane zawierające ciąg wersji unikatowy za każdym razem, gdy opublikować zmian usługi w chmurze tooyour adresu CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="7a5d5-274">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="7a5d5-275">W programie Visual Studio debugowanie hello usługi w chmurze w programie Visual Studio, wpisując `F5`.,</span><span class="sxs-lookup"><span data-stu-id="7a5d5-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="7a5d5-276">Widok hello kodu HTML dla strony hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="7a5d5-277">Będą również widzieć każdego pliku skryptu indywidualnie renderowane, dzięki czemu mają debugowania spójne środowisko w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="7a5d5-278">Mechanizm rezerwowy umożliwiający CDN adresy URL</span><span class="sxs-lookup"><span data-stu-id="7a5d5-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="7a5d5-279">Gdy punktu końcowego usługi Azure CDN nie powiedzie się z jakiegokolwiek powodu, ma toobe Twojego strony sieci Web inteligentne za mało tooaccess serwera sieci Web źródła jako opcji rezerwowej hello ładowania JavaScript lub ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="7a5d5-280">Jest wystarczające toolose obrazów w witrynie sieci Web powodu niedostępności tooCDN, ale wiele poważniejsze toolose strony ważnych funkcji udostępnianych przez usługę własne skrypty i arkusze stylów.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="7a5d5-281">Witaj [pakietu](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) klasa zawiera właściwość o nazwie [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) umożliwiająca tooconfigure hello rezerwowy mechanizm awarii sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="7a5d5-282">toouse tę właściwość, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="7a5d5-283">W projekcie roli sieci Web otwórz *App_Start\BundleConfig.cs*, gdzie adresu CDN jest dodana w każdym [Konstruktor pakietu](http://msdn.microsoft.com/library/jj646464.aspx)i wprowadź następujące hello wyróżnione zmiany toohello mechanizm rezerwowy tooadd Domyślne pakiety:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="7a5d5-284">Gdy `CdnFallbackExpression` jest niezerowa, skrypt jest wstrzykuje tootest hello HTML czy hello pakietu została pomyślnie załadowana i, jeśli nie, uzyskać dostęp do pakietu hello bezpośrednio z serwera sieci Web źródła hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="7a5d5-285">Ta właściwość musi toobe zestaw tooa JavaScript wyrażenie, które sprawdza, czy hello odpowiednich CDN pakietu jest poprawnie załadowany.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="7a5d5-286">wyrażenie Hello potrzebne tootest zgodnie z zawartością toohello różni się każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="7a5d5-287">Dla pakietów domyślne hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="7a5d5-288">`window.jquery`jest zdefiniowany w jquery {wersja}-js</span><span class="sxs-lookup"><span data-stu-id="7a5d5-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="7a5d5-289">`$.validator`jest zdefiniowany w jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="7a5d5-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="7a5d5-290">`window.Modernizr`jest zdefiniowany w modernizer {wersja}-js</span><span class="sxs-lookup"><span data-stu-id="7a5d5-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="7a5d5-291">`$.fn.modal`jest zdefiniowany w bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="7a5d5-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="7a5d5-292">Zwróć uwagę, że nie ustawić CdnFallbackExpression dla hello `~/Cointent/css` pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="7a5d5-293">Ponieważ jest obecnie [usterkę w System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) który injects `<script>` tagu hello oczekiwano rezerwowy CSS zamiast hello `<link>` tagu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="7a5d5-294">Istnieje, jednak duże [powrotu pakietu styl](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferowane przez [Członkowskimi konsultacji grupy](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="7a5d5-295">Obejście hello toouse CSS, Utwórz nowy plik .cs w projekcie roli sieci Web *App_Start* folder o nazwie *StyleBundleExtensions.cs*i zastąpić jej zawartość hello [kodu z GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="7a5d5-296">W *App_Start\StyleFundleExtensions.cs*, Zmień nazwę hello przestrzeni nazw tooyour Web roli (np. **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="7a5d5-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="7a5d5-297">Wróć za`App_Start\BundleConfig.cs` i zmodyfikuj hello ostatnio `bundles.Add` instrukcji z powitania po wyróżniony kod:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="7a5d5-298">Ta nowa metoda rozszerzenia używa hello tego samego pomysł tooinject skryptu w modelu DOM hello toocheck hello HTML dla hello zgodną nazwę klasy, nazwy reguły i wartość reguły zdefiniowany w pakiecie CSS hello i wypada wstecz toohello źródła serwera sieci Web w przypadku niepowodzenia toofind hello dopasowania.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="7a5d5-299">Opublikuj ponownie usługa w chmurze hello i strony głównej hello dostępu.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="7a5d5-300">Widok hello kodu HTML dla strony hello.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="7a5d5-301">Należy znaleźć wprowadzony skrypty podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-301">You should find injected scripts similar toohello following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="7a5d5-302">Należy zauważyć, że wprowadzony skryptu dla pakietu CSS hello nadal zawiera hello niewykorzystany wadliwe z hello `CdnFallbackExpression` właściwości w wierszu hello:</span><span class="sxs-lookup"><span data-stu-id="7a5d5-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="7a5d5-303">Ale od czasu pierwszej części hello hello || wyrażenie zawsze zwróci wartość true (w wierszu hello bezpośrednio powyżej), funkcja wywołania document.write() hello nigdy nie zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="7a5d5-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="7a5d5-304">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="7a5d5-304">More Information</span></span>
* [<span data-ttu-id="7a5d5-305">Omówienie hello Azure sieci dostarczania zawartości (CDN)</span><span class="sxs-lookup"><span data-stu-id="7a5d5-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="7a5d5-306">Za pomocą usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7a5d5-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="7a5d5-307">ASP.NET tworzenie pakietów i minimalizowanie</span><span class="sxs-lookup"><span data-stu-id="7a5d5-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
