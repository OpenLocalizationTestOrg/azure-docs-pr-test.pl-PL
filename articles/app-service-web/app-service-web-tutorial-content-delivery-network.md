---
title: "aaaAdd tooan CDN usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dodaj toocache usłudze Azure App Service tooan sieci dostarczania zawartości (CDN) i dostarczanie plików statycznych z serwerów klientów Zamknij tooyour wokół hello world."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="aa845-103">Dodaj tooan sieci dostarczania zawartości (CDN) usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aa845-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="aa845-104">[Usługa Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) buforuje zawartość statyczną sieci web w strategicznie rozmieszczonych lokalizacjach tooprovide maksymalnej przepływności dostarczania zawartości toousers.</span><span class="sxs-lookup"><span data-stu-id="aa845-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="aa845-105">Hello CDN również zmniejsza obciążenie serwera w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa845-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="aa845-106">Ten samouczek pokazuje, jak tooa Azure CDN tooadd [aplikacji sieci web w usłudze Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa845-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="aa845-107">Oto strony głównej hello hello próbki statycznego HTML lokacji, która będzie współpracować:</span><span class="sxs-lookup"><span data-stu-id="aa845-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Strona główna przykładowej aplikacji](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="aa845-109">Zawartość:</span><span class="sxs-lookup"><span data-stu-id="aa845-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa845-110">Tworzenie punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="aa845-111">Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="aa845-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="aa845-112">Użyj zapytania ciągi wersji toocontrol w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="aa845-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="aa845-113">Użyj domeny niestandardowej dla punktu końcowego CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa845-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aa845-114">Prerequisites</span></span>

<span data-ttu-id="aa845-115">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="aa845-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="aa845-116">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="aa845-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="aa845-117">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="aa845-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="aa845-118">Tworzenie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="aa845-118">Create hello web app</span></span>

<span data-ttu-id="aa845-119">Aplikacja sieci web hello toocreate, który będzie działać z hello wykonaj [statycznych Szybki Start — HTML](app-service-web-get-started-html.md) za pośrednictwem hello **przeglądania toohello aplikacji** krok.</span><span class="sxs-lookup"><span data-stu-id="aa845-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="aa845-120">Przygotowywanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="aa845-120">Have a custom domain ready</span></span>

<span data-ttu-id="aa845-121">krok domeny niestandardowej hello toocomplete tego samouczka należy tooown niestandardową domenę i mają dostęp tooyour DNS rejestru dla dostawcy domeny (na przykład GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="aa845-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="aa845-122">Na przykład tooadd wpisów DNS dla `contoso.com` i `www.contoso.com`, musi mieć ustawienia DNS hello tooconfigure dostępu dla hello `contoso.com` domeny głównej.</span><span class="sxs-lookup"><span data-stu-id="aa845-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="aa845-123">Jeśli nie masz jeszcze nazwy domeny, należy wziąć pod uwagę następujące hello [usługi aplikacji — samouczek domeny](custom-dns-web-site-buydomains-web-app.md) toopurchase domeny przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="aa845-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="aa845-124">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="aa845-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="aa845-125">Otwórz przeglądarkę i przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa845-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="aa845-126">Tworzenie profilu i punktu końcowego usługi CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="aa845-127">Hello lewy pasek nawigacyjny, wybierz **usługi aplikacji**, a następnie wybierz aplikacji hello, który został utworzony w hello [statycznych Szybki Start — HTML](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="aa845-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Wybierz aplikację usługi aplikacji w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="aa845-129">W hello **usługi aplikacji** strony w hello **ustawienia** zaznacz **sieci > Konfigurowanie usługi Azure CDN aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="aa845-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Wybierz sieci CDN w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="aa845-131">W hello **Azure Content Delivery Network** Podaj hello **nowy punkt końcowy** ustawień określonych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Tworzenie profilu i punktu końcowego w portalu hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="aa845-133">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="aa845-133">Setting</span></span> | <span data-ttu-id="aa845-134">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="aa845-134">Suggested value</span></span> | <span data-ttu-id="aa845-135">Opis</span><span class="sxs-lookup"><span data-stu-id="aa845-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="aa845-136">**Profil CDN**</span><span class="sxs-lookup"><span data-stu-id="aa845-136">**CDN profile**</span></span> | <span data-ttu-id="aa845-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="aa845-137">myCDNProfile</span></span> | <span data-ttu-id="aa845-138">Wybierz **Utwórz nowy** toocreate profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="aa845-139">Profil CDN jest kolekcją punktów końcowych usługi CDN z hello samą warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="aa845-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="aa845-140">**Warstwa cenowa**</span><span class="sxs-lookup"><span data-stu-id="aa845-140">**Pricing tier**</span></span> | <span data-ttu-id="aa845-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="aa845-141">Standard Akamai</span></span> | <span data-ttu-id="aa845-142">Witaj [warstwy cenowej](../cdn/cdn-overview.md#azure-cdn-features) określa hello dostawcy i dostępnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="aa845-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="aa845-143">W tym samouczku używamy Akamai standardowa.</span><span class="sxs-lookup"><span data-stu-id="aa845-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="aa845-144">**Nazwa punktu końcowego usługi CDN**</span><span class="sxs-lookup"><span data-stu-id="aa845-144">**CDN endpoint name**</span></span> | <span data-ttu-id="aa845-145">Dowolną nazwę, która jest unikatowa w domenie azureedge.net hello</span><span class="sxs-lookup"><span data-stu-id="aa845-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="aa845-146">Możesz uzyskać dostępu do buforowanych zasobów w domenie hello  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="aa845-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="aa845-147">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="aa845-147">Select **Create**.</span></span>

<span data-ttu-id="aa845-148">Platforma Azure tworzy hello profilu i punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="aa845-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="aa845-149">Witaj nowy punkt końcowy jest wyświetlany w hello **punkty końcowe** listy na hello tej samej stronie, a jego obsługa została zainicjowana hello stan to **systemem**.</span><span class="sxs-lookup"><span data-stu-id="aa845-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Nowy punkt końcowy na liście](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="aa845-151">Test hello punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="aa845-152">W przypadku wybrania warstwy cenowej Verizon propagacja punktu końcowego trwa zwykle około 90 minut.</span><span class="sxs-lookup"><span data-stu-id="aa845-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="aa845-153">W przypadku warstwy Akamai propagacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="aa845-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="aa845-154">Witaj Przykładowa aplikacja ma `index.html` pliku i *css*, *img*, i *js* foldery, które zawierają inne zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="aa845-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="aa845-155">Hello zawartości ścieżki wszystkie te pliki są takie same hello na powitania punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="aa845-156">Na przykład dostęp zarówno hello następujące adresy URL hello *bootstrap.css* pliku w hello *css* folderu:</span><span class="sxs-lookup"><span data-stu-id="aa845-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="aa845-157">Przejdź toohello przeglądarki, następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="aa845-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Strona główna aplikacji przykładowej udostępnianej przez usługę CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="aa845-159">Zostanie wyświetlony hello sama strona uruchomiono wcześniej w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="aa845-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="aa845-160">Usługi Azure CDN ma pobrać zasoby aplikacji hello pochodzenia sieci web i obsługujący z hello punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="aa845-161">tooensure, że ta strona jest buforowany w hello CDN, strona hello odświeżania.</span><span class="sxs-lookup"><span data-stu-id="aa845-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="aa845-162">Dwa żądania dla hello zasobów tego samego są czasami wymagane dla hello CDN toocache hello żądanej zawartości.</span><span class="sxs-lookup"><span data-stu-id="aa845-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="aa845-163">Aby uzyskać więcej informacji o sposobie tworzenia profilów i punktów końcowych usługi Azure CDN, zobacz [Wprowadzenie do usługi Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="aa845-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="aa845-164">Przeczyść hello CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-164">Purge hello CDN</span></span>

<span data-ttu-id="aa845-165">Witaj CDN okresowo odświeża jej zasobach z aplikacji sieci web pochodzenia hello na podstawie hello time to live (TTL) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="aa845-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="aa845-166">Witaj, domyślny czas wygaśnięcia wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="aa845-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="aa845-167">W czasie należy toorefresh hello CDN przed hello wygaśnięcia TTL — na przykład podczas wdrażania aplikacji sieci web zaktualizowane toohello zawartości.</span><span class="sxs-lookup"><span data-stu-id="aa845-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="aa845-168">tootrigger odświeżania, można ręcznie przeczyścić hello CDN zasobów.</span><span class="sxs-lookup"><span data-stu-id="aa845-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="aa845-169">W tej sekcji samouczka hello wdrażanie aplikacji sieci web toohello zmiany i przeczyścić hello CDN tootrigger hello CDN toorefresh pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="aa845-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="aa845-170">Wdrażanie aplikacji sieci web toohello zmiany</span><span class="sxs-lookup"><span data-stu-id="aa845-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="aa845-171">Otwórz hello `index.html` i Dodaj "-V2" toohello H1 nagłówka, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="aa845-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="aa845-172">Zatwierdź zmiany i wdróż je toohello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="aa845-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="aa845-173">Po zakończeniu wdrażania URL aplikacji sieci web toohello przeglądania i zostanie wyświetlony hello zmienić.</span><span class="sxs-lookup"><span data-stu-id="aa845-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Ciąg V2 w tytule aplikacji sieci Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="aa845-175">Adres URL punktu końcowego CDN toohello przeglądania dla strony głównej hello, a nie widzisz hello zmienić, ponieważ wersja buforowana hello w hello CDN nie jeszcze wygasł.</span><span class="sxs-lookup"><span data-stu-id="aa845-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Brak ciągu V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="aa845-177">Przeczyść hello sieci CDN w portalu hello</span><span class="sxs-lookup"><span data-stu-id="aa845-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="aa845-178">tootrigger hello CDN tooupdate jego wersja buforowana, Przeczyść hello CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="aa845-179">W nawigacji po lewej stronie portalu hello, wybierz **grup zasobów**, a następnie wybierz grupę zasobów hello, który został utworzony dla aplikacji sieci web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="aa845-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Wybieranie grupy zasobów](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="aa845-181">Hello listy zasobów wybierz punkt końcowy CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-181">In hello list of resources, select your CDN endpoint.</span></span>

![Wybieranie punktu końcowego](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="aa845-183">U góry hello hello **punktu końcowego** kliknij przycisk **przeczyścić**.</span><span class="sxs-lookup"><span data-stu-id="aa845-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Wybieranie pozycji Przeczyść](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="aa845-185">Wprowadź hello ścieżek zawartości mają toopurge.</span><span class="sxs-lookup"><span data-stu-id="aa845-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="aa845-186">Można przekazywać toopurge ścieżka całego pliku pojedynczego pliku lub toopurge segmentu ścieżki i Odśwież całą zawartość w folderze.</span><span class="sxs-lookup"><span data-stu-id="aa845-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="aa845-187">Ponieważ zmieniono `index.html`, upewnij się, że jest jedna ze ścieżek hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="aa845-188">U dołu hello strony hello, zaznacz pole wyboru **przeczyścić**.</span><span class="sxs-lookup"><span data-stu-id="aa845-188">At hello bottom of hello page, select **Purge**.</span></span>

![Strona przeczyszczania](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="aa845-190">Sprawdź, że hello CDN jest aktualizowany</span><span class="sxs-lookup"><span data-stu-id="aa845-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="aa845-191">Poczekaj, aż żądanie przeczyszczenia hello zakończy przetwarzanie zwykle kilka minut.</span><span class="sxs-lookup"><span data-stu-id="aa845-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="aa845-192">toosee hello bieżący stan, hello wybierz ikonę dzwonka na początku hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="aa845-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Powiadomienie o przeczyszczaniu](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="aa845-194">Przeglądaj URL punktu końcowego CDN toohello `index.html`, i teraz zobaczyć hello dodane toohello tytuł na stronie głównej hello V2.</span><span class="sxs-lookup"><span data-stu-id="aa845-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="aa845-195">Ta operacja wyświetla odświeżeniu pamięci podręcznej CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Ciąg V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="aa845-197">Aby uzyskać więcej informacji, zobacz [Przeczyszczanie punktu końcowego usługi Azure CDN](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="aa845-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="aa845-198">Korzystać z zawartości tooversion ciągi zapytania</span><span class="sxs-lookup"><span data-stu-id="aa845-198">Use query strings tooversion content</span></span>

<span data-ttu-id="aa845-199">Hello Azure CDN oferuje następujące opcje zachowanie buforowania hello:</span><span class="sxs-lookup"><span data-stu-id="aa845-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="aa845-200">Ignoruj ciągi zapytań</span><span class="sxs-lookup"><span data-stu-id="aa845-200">Ignore query strings</span></span>
* <span data-ttu-id="aa845-201">Pomiń buforowanie dla ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="aa845-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="aa845-202">Buforuj każdy unikatowy adres URL</span><span class="sxs-lookup"><span data-stu-id="aa845-202">Cache every unique URL</span></span> 

<span data-ttu-id="aa845-203">Witaj pierwszy z nich jest hello domyślnej, co oznacza, że istnieje tylko jedna wersja buforowanych zasobów, niezależnie od hello ciągu zapytania w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="aa845-204">W tej sekcji samouczka hello zmienisz hello buforowanie toocache zachowanie każdy unikatowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="aa845-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="aa845-205">Należy zmienić to zachowanie pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="aa845-205">Change hello cache behavior</span></span>

<span data-ttu-id="aa845-206">W portalu Azure hello **punktu końcowego CDN** wybierz pozycję **pamięci podręcznej**.</span><span class="sxs-lookup"><span data-stu-id="aa845-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="aa845-207">Wybierz **Buforuj każdy unikatowy adres URL** z hello **zachowanie buforowania ciągu kwerendy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="aa845-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="aa845-208">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="aa845-208">Select **Save**.</span></span>

![Wybieranie zachowania buforowania ciągów zapytań](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="aa845-210">Sprawdzanie, czy unikatowe adresy URL są buforowane osobno</span><span class="sxs-lookup"><span data-stu-id="aa845-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="aa845-211">W przeglądarce przejdź do strony głównej toohello na punkt końcowy CDN hello, ale zawierają ciąg zapytania:</span><span class="sxs-lookup"><span data-stu-id="aa845-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="aa845-212">Witaj CDN zwraca hello bieżącej zawartości sieci web aplikacji, w tym "V2" hello nagłówka.</span><span class="sxs-lookup"><span data-stu-id="aa845-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="aa845-213">tooensure, że ta strona jest buforowany w hello CDN, strona hello odświeżania.</span><span class="sxs-lookup"><span data-stu-id="aa845-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="aa845-214">Otwórz `index.html` i zmień "V2" za "3" i wdrażanie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="aa845-215">W przeglądarce Przejdź takie jak adres URL punktu końcowego CDN toohello z nowego ciągu zapytania `q=2`.</span><span class="sxs-lookup"><span data-stu-id="aa845-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="aa845-216">Witaj CDN pobiera hello bieżącego `index.html` plików i wyświetla "3".</span><span class="sxs-lookup"><span data-stu-id="aa845-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="aa845-217">Ale jeśli oddalisz się punkt końcowy CDN toohello z hello `q=1` ciągu, zapytania zobacz "2".</span><span class="sxs-lookup"><span data-stu-id="aa845-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 w tytule w usłudze CDN, ciąg zapytania 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 w tytule w usłudze CDN, ciąg zapytania 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="aa845-220">Te dane wyjściowe pokazuje, czy każdy ciąg zapytania jest traktowane inaczej:</span><span class="sxs-lookup"><span data-stu-id="aa845-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="aa845-221">q = 1 był używany przed, więc zawartości z pamięci podręcznej są zwracane (V2).</span><span class="sxs-lookup"><span data-stu-id="aa845-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="aa845-222">q = 2 jest nowy, więc hello najnowszą zawartość aplikacji sieci web są pobierane i zwracane (V3).</span><span class="sxs-lookup"><span data-stu-id="aa845-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="aa845-223">Aby uzyskać więcej informacji, zobacz [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md) (Sterowanie zachowaniem buforowania usługi CDN za pomocą ciągów zapytań).</span><span class="sxs-lookup"><span data-stu-id="aa845-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="aa845-224">Mapa punktu końcowego usługi CDN tooa domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="aa845-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="aa845-225">Twoje domeny niestandardowej tooyour punktu końcowego CDN będzie mapy przez utworzenie rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="aa845-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="aa845-226">Rekord CNAME jest funkcją DNS, która mapuje domeny docelowej tooa domeny źródłowej.</span><span class="sxs-lookup"><span data-stu-id="aa845-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="aa845-227">Na przykład mogą być mapowane `cdn.contoso.com` lub `static.contoso.com` zbyt`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="aa845-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="aa845-228">Jeśli nie masz domenę niestandardową, należy wziąć pod uwagę następujące hello [usługi aplikacji — samouczek domeny](custom-dns-web-site-buydomains-web-app.md) toopurchase domeny przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="aa845-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="aa845-229">Znajdź hello toouse nazwy hosta z hello CNAME</span><span class="sxs-lookup"><span data-stu-id="aa845-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="aa845-230">W portalu Azure hello **punktu końcowego** upewnij się, że **omówienie** wybrano hello pozostałych nawigacji, a następnie wybierz opcję hello **+ domeny niestandardowe** przycisk u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="aa845-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Wybieranie opcji dodawania domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="aa845-232">W hello **dodać niestandardową domenę** strony, zobacz hello punktu końcowego host name toouse utworzyć rekord CNAME.</span><span class="sxs-lookup"><span data-stu-id="aa845-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="aa845-233">Nazwa hosta Hello jest pochodną adres URL punktu końcowego CDN:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="aa845-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Strona dodawania domeny](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="aa845-235">Skonfiguruj hello CNAME u rejestratora domen</span><span class="sxs-lookup"><span data-stu-id="aa845-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="aa845-236">Przejdź do witryny sieci web rejestratora domen tooyour, a następnie zlokalizuj hello sekcji do tworzenia rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="aa845-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="aa845-237">Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).</span><span class="sxs-lookup"><span data-stu-id="aa845-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="aa845-238">Znajdź sekcję hello zarządzania CNAME.</span><span class="sxs-lookup"><span data-stu-id="aa845-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="aa845-239">Może mieć toogo tooan Zaawansowane ustawienia strony i poszukaj słowa hello CNAME, aliasu lub poddomeny.</span><span class="sxs-lookup"><span data-stu-id="aa845-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="aa845-240">Utwórz rekord CNAME mapujący z wybranym domeny podrzędnej (na przykład **statycznych** lub **cdn**) toohello **nazwę hosta punktu końcowego** pokazano wcześniej w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="aa845-241">Wprowadź domenę niestandardową hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="aa845-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="aa845-242">Zwraca toohello **dodać niestandardową domenę** strony, a następnie wprowadź domenę niestandardową, w tym poddomeny hello, w oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="aa845-243">Na przykład wprowadź wartość `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aa845-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="aa845-244">Azure sprawdza, czy istnieje rekord CNAME powitania dla hello nazwy domeny, który został wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="aa845-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="aa845-245">Jeśli hello CNAME jest poprawny, domeny niestandardowej jest weryfikowana.</span><span class="sxs-lookup"><span data-stu-id="aa845-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="aa845-246">Może upłynąć czasu dla serwerów tooname toopropagate rekordów CNAME z hello na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="aa845-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="aa845-247">Jeśli domena nie została zweryfikowana natychmiast, zaczekaj kilka minut i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="aa845-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="aa845-248">Domena niestandardowa hello testu</span><span class="sxs-lookup"><span data-stu-id="aa845-248">Test hello custom domain</span></span>

<span data-ttu-id="aa845-249">W przeglądarce Przejdź toohello `index.html` pliku używania domeny niestandardowej (na przykład `cdn.contoso.com/index.html`) tooverify będący wynikiem hello hello takie same jak przejściu bezpośrednio za`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="aa845-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Strona główna przykładowej aplikacji wyświetlona przy użyciu adresu URL domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="aa845-251">Aby uzyskać więcej informacji, zobacz [domeny niestandardowej tooa zawartości mapy usługi Azure CDN](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aa845-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="aa845-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa845-252">Next steps</span></span>

<span data-ttu-id="aa845-253">Wiadomości:</span><span class="sxs-lookup"><span data-stu-id="aa845-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa845-254">Tworzenie punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="aa845-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="aa845-255">Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="aa845-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="aa845-256">Użyj zapytania ciągi wersji toocontrol w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="aa845-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="aa845-257">Użyj domeny niestandardowej dla punktu końcowego CDN hello.</span><span class="sxs-lookup"><span data-stu-id="aa845-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="aa845-258">Dowiedz się, jak toooptimize wydajność sieci CDN w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="aa845-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa845-259">Poprawianie wydajności poprzez kompresowanie plików w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa845-260">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="aa845-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
