---
title: aaaBuy niestandardowej nazwy domeny dla aplikacji sieci Web Azure
description: "Dowiedz się, jak nazwa toobuy domeny niestandardowej z aplikacją sieci web w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="51b9f-103">Kup niestandardowej nazwy domeny dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="51b9f-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="51b9f-104">Domeny aplikacji usługi (wersja zapoznawcza) są domeny najwyższego poziomu, które są zarządzane bezpośrednio na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="51b9f-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="51b9f-105">One był łatwy toomanage domen niestandardowych dla [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51b9f-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="51b9f-106">Ten samouczek pokazuje, jak toobuy domeny usługi aplikacji i przypisz DNS nazwy tooAzure aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="51b9f-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="51b9f-107">Ten artykuł dotyczy usługi Azure App Service (aplikacje sieci Web, aplikacje API Apps, Mobile Apps, Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="51b9f-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="51b9f-108">Dla maszyny Wirtualnej platformy Azure lub usługi Azure Storage, zobacz [tooAzure domeny przypisać usługi aplikacji maszyny Wirtualnej lub usługi Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="51b9f-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="51b9f-109">Dla usług w chmurze, zobacz [Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51b9f-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51b9f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51b9f-110">Prerequisites</span></span>

<span data-ttu-id="51b9f-111">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="51b9f-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="51b9f-112">[Utwórz aplikację usługi aplikacji](/azure/app-service/), lub użyć utworzonego w samouczku innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51b9f-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="51b9f-113">Przygotowywanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="51b9f-113">Prepare hello app</span></span>

<span data-ttu-id="51b9f-114">domen niestandardowych toouse w aplikacji sieci Web Azure, aplikacji sieci web firmy [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być płatną warstwy (**współużytkowane**, **podstawowe**, **standardowe**, lub **Premium**).</span><span class="sxs-lookup"><span data-stu-id="51b9f-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="51b9f-115">W tym kroku, możesz upewnij się, że tej aplikacji sieci web hello jest w hello obsługiwane warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="51b9f-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="51b9f-116">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="51b9f-116">Sign in tooAzure</span></span>

<span data-ttu-id="51b9f-117">Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51b9f-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="51b9f-118">Przejdź do aplikacji toohello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="51b9f-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="51b9f-119">Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="51b9f-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="51b9f-121">Zostanie wyświetlona strona zarządzania hello z hello aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="51b9f-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="51b9f-122">Sprawdź hello warstwy cenowej</span><span class="sxs-lookup"><span data-stu-id="51b9f-122">Check hello pricing tier</span></span>

<span data-ttu-id="51b9f-123">Lewy pasek nawigacyjny strony aplikacji hello hello, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="51b9f-125">Warstwa bieżąca aplikacja Hello zostanie wyróżniona niebieskim obramowaniem.</span><span class="sxs-lookup"><span data-stu-id="51b9f-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="51b9f-126">Sprawdź toomake się, że aplikacja hello nie jest hello **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="51b9f-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="51b9f-127">Niestandardowe DNS nie jest obsługiwany w hello **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="51b9f-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="51b9f-129">Jeśli hello planu usługi aplikacji nie jest **wolne**, zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[domeny hello Kup](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="51b9f-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="51b9f-130">Skalowanie w górę hello planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="51b9f-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="51b9f-131">Wybierz jedno z warstw — wolne hello (**Shared**, **podstawowe**, **standardowe**, lub **Premium**).</span><span class="sxs-lookup"><span data-stu-id="51b9f-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="51b9f-132">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-132">Click **Select**.</span></span>

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="51b9f-134">Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="51b9f-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Potwierdzenie operacji skalowania](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="51b9f-136">Kup hello domeny</span><span class="sxs-lookup"><span data-stu-id="51b9f-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="51b9f-137">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="51b9f-137">Sign in tooAzure</span></span>
<span data-ttu-id="51b9f-138">Otwórz hello [portalu Azure](https://portal.azure.com/) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51b9f-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="51b9f-139">Uruchamianie Kup domen</span><span class="sxs-lookup"><span data-stu-id="51b9f-139">Launch Buy domains</span></span>
<span data-ttu-id="51b9f-140">W hello **aplikacje sieci Web** , kliknij pozycję hello nazwę aplikacji sieci web, wybierz opcję **ustawienia**, a następnie wybierz **domen niestandardowych**</span><span class="sxs-lookup"><span data-stu-id="51b9f-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="51b9f-141">W hello **domen niestandardowych** kliknij przycisk **kupić domen**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="51b9f-142">Skonfiguruj hello domeny zakupu</span><span class="sxs-lookup"><span data-stu-id="51b9f-142">Configure hello domain purchase</span></span>

<span data-ttu-id="51b9f-143">W hello **aplikacji usługi domeny** strony w hello **wyszukiwania dla domeny** okno, nazwa domeny hello typu toobuy i typ `Enter`.</span><span class="sxs-lookup"><span data-stu-id="51b9f-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="51b9f-144">Witaj sugerowane dostępnych domen są wyświetlane poniżej pola tekstowego hello.</span><span class="sxs-lookup"><span data-stu-id="51b9f-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="51b9f-145">Wybierz co najmniej jedna domena ma toobuy.</span><span class="sxs-lookup"><span data-stu-id="51b9f-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="51b9f-146">Kliknij przycisk hello **informacje kontaktowe** i wypełnij formularz informacji kontaktowych hello domeny.</span><span class="sxs-lookup"><span data-stu-id="51b9f-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="51b9f-147">Gdy skończysz, kliknij przycisk **OK** tooreturn toohello aplikacji usługi domeny strony.</span><span class="sxs-lookup"><span data-stu-id="51b9f-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="51b9f-148">Należy wypełnić wszystkie wymagane pola z dokładnością tak jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="51b9f-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="51b9f-149">Nieprawidłowe dane, aby uzyskać więcej informacji może spowodować niepowodzenie toopurchase domen.</span><span class="sxs-lookup"><span data-stu-id="51b9f-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="51b9f-150">Następnie wybierz opcje hello potrzebne dla danej domeny.</span><span class="sxs-lookup"><span data-stu-id="51b9f-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="51b9f-151">Zobacz hello w poniższej tabeli objaśnienia:</span><span class="sxs-lookup"><span data-stu-id="51b9f-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="51b9f-152">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="51b9f-152">Setting</span></span> | <span data-ttu-id="51b9f-153">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="51b9f-153">Suggested Value</span></span> | <span data-ttu-id="51b9f-154">Opis</span><span class="sxs-lookup"><span data-stu-id="51b9f-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="51b9f-155">Automatycznego odnawiania</span><span class="sxs-lookup"><span data-stu-id="51b9f-155">Auto renew</span></span> | <span data-ttu-id="51b9f-156">**Włączanie**</span><span class="sxs-lookup"><span data-stu-id="51b9f-156">**Enable**</span></span> | <span data-ttu-id="51b9f-157">Odnawia domenę usługi App automatycznie co roku.</span><span class="sxs-lookup"><span data-stu-id="51b9f-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="51b9f-158">Karty kredytowej jest rozliczana hello tej samej cenie zakupu w czasie hello odnawiania.</span><span class="sxs-lookup"><span data-stu-id="51b9f-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="51b9f-159">Ochrona prywatności</span><span class="sxs-lookup"><span data-stu-id="51b9f-159">Privacy protection</span></span> | <span data-ttu-id="51b9f-160">Włączanie</span><span class="sxs-lookup"><span data-stu-id="51b9f-160">Enable</span></span> | <span data-ttu-id="51b9f-161">Zgódź się zbyt "Ochrona prywatności", który jest dostępny w hello zapłaconej kwoty _bezpłatnie_ (z wyjątkiem domen najwyższego poziomu, którego rejestr nie obsługują ochrony prywatności, takich jak _. co.in_, _. co.uk_i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="51b9f-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="51b9f-162">Przypisz domyślne nazwy hostów</span><span class="sxs-lookup"><span data-stu-id="51b9f-162">Assign default hostnames</span></span> | <span data-ttu-id="51b9f-163">**www** i**@**</span><span class="sxs-lookup"><span data-stu-id="51b9f-163">**www** and **@**</span></span> | <span data-ttu-id="51b9f-164">Wybierz hello żądana powiązań z nazwami hostów, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="51b9f-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="51b9f-165">Po zakończeniu operacji zakupu domeny hello aplikacji sieci web są dostępne na powitania wybrane nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="51b9f-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="51b9f-166">Jeśli aplikacja sieci web hello jest za [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), nie widzisz domeny głównej hello hello opcja tooassign (@), ponieważ Menedżera ruchu jest nie rekordów A pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="51b9f-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="51b9f-167">Należy wprowadzić zmiany przypisania hostname toohello po zakończeniu zakupu domeny hello.</span><span class="sxs-lookup"><span data-stu-id="51b9f-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="51b9f-168">Zaakceptuj postanowienia i zakupu</span><span class="sxs-lookup"><span data-stu-id="51b9f-168">Accept terms and purchase</span></span>

<span data-ttu-id="51b9f-169">Kliknij przycisk **postanowienia prawne** tooreview hello warunków i opłat hello, następnie kliknij przycisk **kupić**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="51b9f-170">Domeny aplikacji usługi użyj domeny hello toohost usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51b9f-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="51b9f-171">Ponadto toohello opłata rejestracja domeny, użycia dla usługi Azure DNS opłaty.</span><span class="sxs-lookup"><span data-stu-id="51b9f-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="51b9f-172">Aby uzyskać informacje, zobacz [cennik usługi Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="51b9f-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="51b9f-173">Po powrocie do hello **aplikacji usługi domeny** kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="51b9f-174">Gdy trwa operacja hello, zostanie wyświetlony hello następujące powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="51b9f-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="51b9f-175">Nazwy hostów hello testu</span><span class="sxs-lookup"><span data-stu-id="51b9f-175">Test hello hostnames</span></span>

<span data-ttu-id="51b9f-176">Jeśli zostały przypisane domyślne nazwy hostów tooyour sieci web aplikacji, również wyświetlane jest powiadomienie Powodzenie dla każdej wybranej nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="51b9f-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="51b9f-177">Umożliwia wyświetlenie nazwy hostów hello wybrane w hello **domen niestandardowych** strony w hello **Hostnames** sekcji.</span><span class="sxs-lookup"><span data-stu-id="51b9f-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="51b9f-178">nazwy hostów hello tootest, przejdź toohello wymienione nazwy hostów, w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="51b9f-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="51b9f-179">W przykładzie hello hello poprzedzających zrzut ekranu, spróbuj nawigowanie po too_kontoso.net_ i _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="51b9f-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="51b9f-180">Przypisanie nazwy hostów tooweb aplikacji</span><span class="sxs-lookup"><span data-stu-id="51b9f-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="51b9f-181">Jeśli wybierzesz nie tooassign, jeden lub więcej domyślnej nazwy hostów tooyour aplikacji sieci web podczas hello proces zakupu lub jeśli nie potrzebujesz tooassign nazwy hosta na liście, można przypisać nazwy hosta w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="51b9f-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="51b9f-182">Można również przypisywać nazwy hostów w tooany domena usługi aplikacji hello innych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="51b9f-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="51b9f-183">Witaj kroki zależą od czy hello domeny aplikacji usługi i aplikacji sieci web hello należą toohello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="51b9f-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="51b9f-184">Inną subskrypcję: Mapowanie niestandardowych rekordów DNS z aplikacji sieci web toohello domena usługi aplikacji hello jak zewnętrznie zakupionych domeny.</span><span class="sxs-lookup"><span data-stu-id="51b9f-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="51b9f-185">Aby uzyskać informacji na temat dodawania DNS niestandardowej nazwy tooan domena usługi aplikacji, zobacz [Zarządzanie niestandardowych rekordów DNS](#custom).</span><span class="sxs-lookup"><span data-stu-id="51b9f-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="51b9f-186">toomap aplikacji sieci web tooa zakupionych domen zewnętrznych, zobacz [mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacje sieci Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="51b9f-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="51b9f-187">Tej samej subskrypcji: hello Użyj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="51b9f-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="51b9f-188">Uruchom dodać nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="51b9f-188">Launch add hostname</span></span>
<span data-ttu-id="51b9f-189">W hello **usługi aplikacji** strony, hello wybierz nazwę aplikacji sieci web przewidzianych tooassign nazwy hostów, aby wybrać **ustawienia**, a następnie wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="51b9f-190">Upewnij się, że zakupione domeny jest wymieniony w hello **domenami usługi aplikacji** sekcji, ale nie wybierz go.</span><span class="sxs-lookup"><span data-stu-id="51b9f-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="51b9f-191">Wszystkich domen usługi aplikacji w tej samej subskrypcji są wyświetlane w aplikacji sieci web hello hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="51b9f-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="51b9f-192">Jeśli Twoja domena to w aplikacji sieci web hello subskrypcji, ale niewidoczna w aplikacji sieci web hello **domen niestandardowych** strony, spróbuj otworzyć hello **domen niestandardowych** strony lub odświeżanie hello strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="51b9f-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="51b9f-193">Sprawdź również, dzwonka powiadomień hello u góry hello hello portalu Azure niepowodzeń postępu lub utworzenia.</span><span class="sxs-lookup"><span data-stu-id="51b9f-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="51b9f-194">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="51b9f-195">Konfigurowanie nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="51b9f-195">Configure hostname</span></span>
<span data-ttu-id="51b9f-196">W hello **dodać nazwę hosta** okno dialogowe, nazwy FQDN hello typu domenę usługi aplikacji lub dowolnej domeny podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="51b9f-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="51b9f-197">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="51b9f-197">For example:</span></span>

- <span data-ttu-id="51b9f-198">kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="51b9f-198">kontoso.net</span></span>
- <span data-ttu-id="51b9f-199">www.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="51b9f-199">www.kontoso.net</span></span>
- <span data-ttu-id="51b9f-200">ABC.kontoso.NET</span><span class="sxs-lookup"><span data-stu-id="51b9f-200">abc.kontoso.net</span></span>

<span data-ttu-id="51b9f-201">Po zakończeniu wybierz **weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-201">When finished, select **Validate**.</span></span> <span data-ttu-id="51b9f-202">Typ rekordu hostname Hello jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="51b9f-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="51b9f-203">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-203">Select **Add hostname**.</span></span>

<span data-ttu-id="51b9f-204">Po zakończeniu operacji hello jest wyświetlone powiadomienie Powodzenie dla hello przypisane nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="51b9f-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="51b9f-205">Zamknij dodać nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="51b9f-205">Close add hostname</span></span>
<span data-ttu-id="51b9f-206">W hello **dodać nazwę hosta** Przypisz żadnych innych hostname tooyour aplikacji sieci web, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="51b9f-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="51b9f-207">Po zakończeniu zamknij hello **dodać nazwę hosta** strony.</span><span class="sxs-lookup"><span data-stu-id="51b9f-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="51b9f-208">Powinien zostać wyświetlony hostname(s) hello przydzielone w Twojej aplikacji **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="51b9f-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="51b9f-209">Nazwy hostów hello testu</span><span class="sxs-lookup"><span data-stu-id="51b9f-209">Test hello hostnames</span></span>

<span data-ttu-id="51b9f-210">Przejdź toohello wymienione nazwy hostów, w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="51b9f-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="51b9f-211">W przykładzie hello hello zrzut ekranu poprzedzającym spróbuj nawigowanie po too_abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="51b9f-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="51b9f-212">Zarządzanie niestandardowych rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="51b9f-212">Manage custom DNS records</span></span>

<span data-ttu-id="51b9f-213">Na platformie Azure rekordy DNS dla domeny usługi aplikacji są zarządzane przy użyciu [usługi Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="51b9f-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="51b9f-214">Można dodać, usunąć i Aktualizuj rekordy DNS, podobnie jak zewnętrznie zakupionych domeny.</span><span class="sxs-lookup"><span data-stu-id="51b9f-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="51b9f-215">Domena Otwórz usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="51b9f-215">Open App Service Domain</span></span>

<span data-ttu-id="51b9f-216">W portalu Azure, w menu po lewej stronie powitania hello wybierz **więcej usług** > **domenami usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="51b9f-217">Wybierz hello toomanage domeny.</span><span class="sxs-lookup"><span data-stu-id="51b9f-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="51b9f-218">Dostęp do strefy DNS</span><span class="sxs-lookup"><span data-stu-id="51b9f-218">Access DNS zone</span></span>

<span data-ttu-id="51b9f-219">W menu po lewej stronie powitania domeny wybierz **strefy DNS**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="51b9f-220">Ta akcja powoduje otwarcie hello [strefy DNS](../dns/dns-zones-records.md) strony domenę usługi aplikacji w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51b9f-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="51b9f-221">Aby uzyskać informacje na temat tooedit rekordy DNS, zobacz [jak toomanage strefy DNS w hello portalu Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51b9f-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="51b9f-222">Anuluj zakupu (usuwania domeny)</span><span class="sxs-lookup"><span data-stu-id="51b9f-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="51b9f-223">Po zakupie hello domena usługi aplikacji masz pięć dni toocancel zakupu dla pełny zwrot kosztów.</span><span class="sxs-lookup"><span data-stu-id="51b9f-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="51b9f-224">Po pięć dni można usunąć hello domena usługi aplikacji, ale nie można otrzymać zwrot kosztów.</span><span class="sxs-lookup"><span data-stu-id="51b9f-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="51b9f-225">Domena Otwórz usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="51b9f-225">Open App Service Domain</span></span>

<span data-ttu-id="51b9f-226">W portalu Azure, w menu po lewej stronie powitania hello wybierz **więcej usług** > **domenami usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="51b9f-227">Wybierz hello domeny tooyou chcesz toocancel lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="51b9f-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="51b9f-228">Usuń powiązań z nazwami hostów</span><span class="sxs-lookup"><span data-stu-id="51b9f-228">Delete hostname bindings</span></span>

<span data-ttu-id="51b9f-229">W menu po lewej stronie powitania domeny wybierz **powiązań z nazwami hostów**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="51b9f-230">Poniżej przedstawiono Hello powiązań z nazwami hostów ze wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51b9f-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="51b9f-231">Nie można usunąć hello domena usługi aplikacji, dopóki nie zostaną usunięte wszystkie powiązań z nazwami hostów.</span><span class="sxs-lookup"><span data-stu-id="51b9f-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="51b9f-232">Usuń powiązanie każdej nazwy hosta, wybierając **... **  >  **Usunąć**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="51b9f-233">Po usunięciu wszystkich powiązań hello wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="51b9f-234">Anuluj lub delete</span><span class="sxs-lookup"><span data-stu-id="51b9f-234">Cancel or delete</span></span>

<span data-ttu-id="51b9f-235">W menu po lewej stronie powitania domeny wybierz **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="51b9f-236">Czy nie upłynął termin anulowania hello na powitania zakupionych domeny, wybierz **anulować zakup**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="51b9f-237">W przeciwnym razie zobacz **usunąć** zamiast tego przycisku.</span><span class="sxs-lookup"><span data-stu-id="51b9f-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="51b9f-238">toodelete hello domeny bez zwrotu kosztów, wybierz opcję **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="51b9f-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="51b9f-239">Wybierz **OK** tooconfirm hello operacji.</span><span class="sxs-lookup"><span data-stu-id="51b9f-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="51b9f-240">Jeśli nie chcesz tooproceed, kliknij w dowolnym miejscu poza powitalne okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="51b9f-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="51b9f-241">Po zakończeniu operacji hello domeny hello jest zwolnione z subskrypcji i wszyscy toopurchase ponownie.</span><span class="sxs-lookup"><span data-stu-id="51b9f-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
