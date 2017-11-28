---
title: "aaaMap istniejących niestandardowe DNS nazwa aplikacji sieci Web tooAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd istniejącą domenę DNS niestandardowej nazwy aplikacji sieci web (domena niestandardowych) tooa, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="e026b-103">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="e026b-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="e026b-104">Usługa [Azure Web Apps](app-service-web-overview.md) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="e026b-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e026b-105">Ten samouczek pokazuje, jak toomap istniejących DNS niestandardowej nazwy tooAzure aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e026b-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="e026b-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e026b-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e026b-108">Mapowanie poddomeny (na przykład `www.contoso.com`) przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="e026b-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="e026b-109">Mapowanie domeny katalogu głównego (na przykład `contoso.com`) przy użyciu rekord a.</span><span class="sxs-lookup"><span data-stu-id="e026b-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="e026b-110">Zamapować domenę symboli wieloznacznych (na przykład `*.contoso.com`) przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="e026b-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="e026b-111">Mapowanie domeny przy użyciu skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="e026b-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="e026b-112">Możesz użyć dowolnej **rekord CNAME** lub **rekordu** toomap DNS niestandardowej nazwy tooApp usługi.</span><span class="sxs-lookup"><span data-stu-id="e026b-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="e026b-113">Zalecane jest użycie rekord CNAME dla wszystkich niestandardowych nazw DNS z wyjątkiem domeny katalogu głównego (na przykład `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e026b-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="e026b-114">toomigrate witryny na żywo i jego tooApp nazwy domeny DNS usługi, zobacz [migracji active tooAzure nazwę DNS usługi aplikacji](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e026b-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e026b-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e026b-115">Prerequisites</span></span>

<span data-ttu-id="e026b-116">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="e026b-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="e026b-117">[Utwórz aplikację usługi aplikacji](/azure/app-service/), lub użyć utworzonego w samouczku innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e026b-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="e026b-118">Kup nazwę domeny i upewnij się, że masz dostęp toohello DNS rejestru dla dostawcy domeny (na przykład GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="e026b-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="e026b-119">Na przykład tooadd wpisów DNS dla `contoso.com` i `www.contoso.com`, musi być możliwe tooconfigure hello ustawień DNS na potrzeby hello `contoso.com` domeny głównej.</span><span class="sxs-lookup"><span data-stu-id="e026b-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e026b-120">Jeśli nie masz istniejącej domeny nazwa, należy wziąć pod uwagę [zakupu domeny przy użyciu hello portalu Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="e026b-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="e026b-121">Przygotowywanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e026b-121">Prepare hello app</span></span>

<span data-ttu-id="e026b-122">toomap niestandardowe DNS nazwy tooa aplikacji sieci web, aplikacji sieci web hello [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być płatną warstwy (**Shared**, **podstawowe**, **standardowe**, lub  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e026b-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="e026b-123">W tym kroku, możesz upewnij się, że tej aplikacji usługi aplikacji znajduje się w hello hello obsługiwane warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="e026b-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="e026b-124">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="e026b-124">Sign in tooAzure</span></span>

<span data-ttu-id="e026b-125">Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e026b-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="e026b-126">Przejdź do aplikacji toohello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e026b-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="e026b-127">Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e026b-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="e026b-129">Zostanie wyświetlona strona zarządzania hello z hello aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="e026b-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="e026b-130">Sprawdź hello warstwy cenowej</span><span class="sxs-lookup"><span data-stu-id="e026b-130">Check hello pricing tier</span></span>

<span data-ttu-id="e026b-131">Lewy pasek nawigacyjny strony aplikacji hello hello, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.</span><span class="sxs-lookup"><span data-stu-id="e026b-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="e026b-133">Warstwa bieżąca aplikacja Hello zostanie wyróżniona niebieskim obramowaniem.</span><span class="sxs-lookup"><span data-stu-id="e026b-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="e026b-134">Sprawdź toomake się, że aplikacja hello nie jest hello **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="e026b-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="e026b-135">Niestandardowe DNS nie jest obsługiwany w hello **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="e026b-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="e026b-137">Jeśli hello planu usługi aplikacji nie jest **wolne**, zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[mapy rekord CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="e026b-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="e026b-138">Skalowanie w górę hello planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e026b-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="e026b-139">Wybierz jedno z warstw — wolne hello (**Shared**, **podstawowe**, **standardowe**, lub **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e026b-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="e026b-140">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="e026b-140">Click **Select**.</span></span>

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="e026b-142">Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="e026b-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Potwierdzenie operacji skalowania](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="e026b-144">Mapa rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="e026b-144">Map a CNAME record</span></span>

<span data-ttu-id="e026b-145">W samouczku przykład Witaj, Dodaj rekord CNAME dla hello `www` domeny podrzędnej (na przykład `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e026b-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="e026b-146">Utwórz rekord CNAME hello</span><span class="sxs-lookup"><span data-stu-id="e026b-146">Create hello CNAME record</span></span>

<span data-ttu-id="e026b-147">Dodaj toomap rekordów CNAME hostname domyślnej aplikacji toohello domeny podrzędnej (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e026b-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="e026b-148">Dla hello `www.contoso.com` przykład domeny, Dodaj rekord CNAME, który mapuje nazwę hello `www` zbyt`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e026b-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="e026b-149">Po dodaniu hello CNAME strony rekordy DNS hello wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e026b-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="e026b-151">Włącz mapowanie rekordu CNAME hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e026b-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="e026b-152">Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="e026b-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e026b-154">W hello **domen niestandardowych** strony aplikacji hello, Dodaj hello w pełni kwalifikowana nazwa DNS niestandardowe (`www.contoso.com`) toohello listy.</span><span class="sxs-lookup"><span data-stu-id="e026b-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="e026b-155">Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="e026b-157">Typ hello pełną nazwę domeny dodaje rekord CNAME, takich jak `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e026b-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="e026b-158">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="e026b-158">Select **Validate**.</span></span>

<span data-ttu-id="e026b-159">Witaj **dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="e026b-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e026b-160">Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**CNAME (www.example.com lub wszystkie poddomeny)**.</span><span class="sxs-lookup"><span data-stu-id="e026b-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="e026b-161">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-161">Select **Add hostname**.</span></span>

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="e026b-163">Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="e026b-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="e026b-164">Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="e026b-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="e026b-166">Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="e026b-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="e026b-168">Mapa rekord a.</span><span class="sxs-lookup"><span data-stu-id="e026b-168">Map an A record</span></span>

<span data-ttu-id="e026b-169">W przykładzie samouczek hello dodaniu rekordu A dla domeny głównej hello (na przykład `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e026b-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="e026b-170">Skopiuj adres IP aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e026b-170">Copy hello app's IP address</span></span>

<span data-ttu-id="e026b-171">rekord A toomap należy aplikacji hello zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="e026b-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="e026b-172">Ten adres IP można znaleźć w aplikacji hello **domen niestandardowych** strony w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e026b-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="e026b-173">Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="e026b-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e026b-175">W hello **domen niestandardowych** pozycję Kopiuj aplikacji hello adres IP.</span><span class="sxs-lookup"><span data-stu-id="e026b-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="e026b-177">Utwórz rekord A hello</span><span class="sxs-lookup"><span data-stu-id="e026b-177">Create hello A record</span></span>

<span data-ttu-id="e026b-178">wymaga usługi aplikacji toomap A tooan rekordów aplikacji, **dwóch** rekordy DNS:</span><span class="sxs-lookup"><span data-stu-id="e026b-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="e026b-179">**A** rejestrowany adres IP toomap toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e026b-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="e026b-180">A **TXT** zarejestrować nazwę hosta domyślnego toomap toohello aplikacji `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e026b-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e026b-181">Usługa aplikacji używa tego rekordu tylko podczas konfiguracji, czy jesteś właścicielem domeny niestandardowej hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="e026b-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="e026b-182">Po domeny niestandardowej jest weryfikowane i skonfigurowaniu w usłudze App Service, można usunąć tego rekordu TXT.</span><span class="sxs-lookup"><span data-stu-id="e026b-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="e026b-183">Dla hello `contoso.com` przykład domeny utworzyć rekordy A i TXT hello zgodnie z poniższej tabeli toohello (`@` zazwyczaj reprezentuje hello domeny głównej).</span><span class="sxs-lookup"><span data-stu-id="e026b-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="e026b-184">Typ rekordu</span><span class="sxs-lookup"><span data-stu-id="e026b-184">Record type</span></span> | <span data-ttu-id="e026b-185">Host</span><span class="sxs-lookup"><span data-stu-id="e026b-185">Host</span></span> | <span data-ttu-id="e026b-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="e026b-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="e026b-187">A</span><span class="sxs-lookup"><span data-stu-id="e026b-187">A</span></span> | `@` | <span data-ttu-id="e026b-188">Adres IP z [aplikacji hello kopiowania adresu IP](#info)</span><span class="sxs-lookup"><span data-stu-id="e026b-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="e026b-189">TXT</span><span class="sxs-lookup"><span data-stu-id="e026b-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="e026b-190">Dodanie rekordów hello hello strony rekordy DNS wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e026b-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Strona rekordów DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="e026b-192">Włącz hello mapowanie rekordu w aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e026b-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="e026b-193">W aplikacji hello **domen niestandardowych** strony hello portalu Azure, należy dodać hello w pełni kwalifikowana nazwa DNS niestandardowe (na przykład `contoso.com`) toohello listy.</span><span class="sxs-lookup"><span data-stu-id="e026b-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="e026b-194">Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="e026b-196">Typ hello pełną nazwę domeny skonfigurować rekord hello A, takich jak `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e026b-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="e026b-197">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="e026b-197">Select **Validate**.</span></span>

<span data-ttu-id="e026b-198">Witaj **dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="e026b-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e026b-199">Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**rekordu (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="e026b-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="e026b-200">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-200">Select **Add hostname**.</span></span>

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="e026b-202">Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="e026b-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="e026b-203">Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="e026b-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Dodaje rekord](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="e026b-205">Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="e026b-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="e026b-207">Zamapować domenę symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="e026b-207">Map a wildcard domain</span></span>

<span data-ttu-id="e026b-208">W przykładzie samouczek hello mapy [nazwa DNS z symbolem wieloznacznym](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (na przykład `*.contoso.com`) toohello aplikacji usługi app Service przez dodanie rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="e026b-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="e026b-209">Utwórz rekord CNAME hello</span><span class="sxs-lookup"><span data-stu-id="e026b-209">Create hello CNAME record</span></span>

<span data-ttu-id="e026b-210">Dodaj nazwę hosta domyślnego symbolu wieloznacznego nazwa toohello aplikacji toomap rekordów CNAME (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e026b-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="e026b-211">Dla hello `*.contoso.com` przykład domeny hello rekord CNAME przypisze nazwę hello `*` zbyt`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e026b-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="e026b-212">Po dodaniu hello CNAME hello strony rekordy DNS wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e026b-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="e026b-214">Włącz mapowanie rekordu CNAME hello w aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e026b-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="e026b-215">Można teraz dodawać żadnych poddomeny odpowiadający hello symbolu wieloznacznego nazwa toohello aplikacji (na przykład `sub1.contoso.com` i `sub2.contoso.com` odpowiada `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e026b-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="e026b-216">Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="e026b-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e026b-218">Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="e026b-220">Wpisz w pełni kwalifikowaną nazwą domeny odpowiadający hello domenie symbolu wieloznacznego (na przykład `sub1.contoso.com`), a następnie wybierz **weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="e026b-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="e026b-221">Witaj **dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="e026b-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e026b-222">Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**rekord CNAME (www.example.com lub wszystkie poddomeny)**.</span><span class="sxs-lookup"><span data-stu-id="e026b-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="e026b-223">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="e026b-223">Select **Add hostname**.</span></span>

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="e026b-225">Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="e026b-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="e026b-226">Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="e026b-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="e026b-227">Wybierz hello  **+**  ikonę ponownie tooadd innej nazwy hosta odpowiadający hello domenie symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="e026b-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="e026b-228">Na przykład dodać `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e026b-228">For example, add `sub2.contoso.com`.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="e026b-230">Testowanie w przeglądarce</span><span class="sxs-lookup"><span data-stu-id="e026b-230">Test in browser</span></span>

<span data-ttu-id="e026b-231">Przeglądaj toohello nazwy DNS, który został wcześniej skonfigurowany (na przykład `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, i `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e026b-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="e026b-233">Zautomatyzować za pomocą skryptów</span><span class="sxs-lookup"><span data-stu-id="e026b-233">Automate with scripts</span></span>

<span data-ttu-id="e026b-234">Można zautomatyzować zarządzanie domenami niestandardowymi za pomocą skryptów, za pomocą hello [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e026b-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="e026b-235">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e026b-235">Azure CLI</span></span> 

<span data-ttu-id="e026b-236">Witaj następujące polecenie dodaje skonfigurowane niestandardowe DNS nazwy tooan aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="e026b-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="e026b-237">Aby uzyskać więcej informacji, zobacz [mapy domeny niestandardowej aplikacji sieci web tooa](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e026b-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="e026b-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e026b-238">Azure PowerShell</span></span> 

<span data-ttu-id="e026b-239">Witaj następujące polecenie dodaje skonfigurowane niestandardowe DNS nazwy tooan aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="e026b-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="e026b-240">Aby uzyskać więcej informacji, zobacz [przypisać domeny niestandardowej aplikacji sieci web tooa](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e026b-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e026b-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e026b-241">Next steps</span></span>

<span data-ttu-id="e026b-242">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e026b-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e026b-243">Mapa poddomeny przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="e026b-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="e026b-244">Mapa domeny głównej, przy użyciu rekord a.</span><span class="sxs-lookup"><span data-stu-id="e026b-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="e026b-245">Zamapować domenę symboli wieloznacznych przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="e026b-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="e026b-246">Mapowanie domeny przy użyciu skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="e026b-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="e026b-247">Przejść dalej toolearn samouczka toohello jak toobind SSL niestandardowych certyfikatów tooa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e026b-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e026b-248">Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="e026b-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
