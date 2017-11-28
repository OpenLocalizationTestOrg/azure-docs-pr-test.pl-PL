---
title: "Dodaj CDN usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dodaj usługę Content Delivery Network (CDN) do usługi Azure App Service, aby buforować i dostarczać pliki statyczne z serwerów znajdujących się blisko klientów na całym świecie."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="a4175-103">Dodawanie usługi Content Delivery Network (CDN) do usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a4175-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="a4175-104">Usługa [Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) buforuje zawartość statyczną sieci Web w strategicznie rozmieszczonych lokalizacjach w celu zapewnienia maksymalnej przepływności dostarczania zawartości dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a4175-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="a4175-105">Usługa CDN zmniejsza również obciążenie serwera w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a4175-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="a4175-106">W tym samouczku przedstawiono sposób dodawania usługi Azure CDN do [aplikacji sieci Web w usłudze Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4175-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="a4175-107">Oto strona główna przykładowej statycznej witryny HTML, z którą będziesz pracować:</span><span class="sxs-lookup"><span data-stu-id="a4175-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Strona główna przykładowej aplikacji](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="a4175-109">Zawartość:</span><span class="sxs-lookup"><span data-stu-id="a4175-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4175-110">Tworzenie punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="a4175-111">Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="a4175-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="a4175-112">Używanie ciągów zapytań do sterowania zbuforowanymi wersjami.</span><span class="sxs-lookup"><span data-stu-id="a4175-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="a4175-113">Używanie domeny niestandardowej na potrzeby punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4175-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4175-114">Prerequisites</span></span>

<span data-ttu-id="a4175-115">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="a4175-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="a4175-116">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="a4175-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="a4175-117">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a4175-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="a4175-118">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a4175-118">Create the web app</span></span>

<span data-ttu-id="a4175-119">Aby utworzyć aplikację sieci web, która będzie współpracować, wykonaj [statycznych Szybki Start — HTML](app-service-web-get-started-html.md) za pośrednictwem **przejdź do aplikacji** kroku.</span><span class="sxs-lookup"><span data-stu-id="a4175-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="a4175-120">Przygotowywanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="a4175-120">Have a custom domain ready</span></span>

<span data-ttu-id="a4175-121">Aby wykonać krok domeny niestandardowej z tego samouczka, należy właścicielem domeny niestandardowej i uzyskiwania dostępu do rejestru systemu DNS dla domeny dostawcy (takie jak GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="a4175-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="a4175-122">Aby na przykład dodać wpisy DNS dla domen `contoso.com` i `www.contoso.com`, musisz mieć możliwość skonfigurowania ustawień DNS dla domeny głównej `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a4175-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="a4175-123">Jeśli nie masz jeszcze nazwy domeny, możesz postępować według instrukcji zawartych w [samouczku dotyczącym domeny usługi App Service](custom-dns-web-site-buydomains-web-app.md) w celu zakupienia domeny za pośrednictwem witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a4175-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="a4175-124">Logowanie do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a4175-124">Log in to the Azure portal</span></span>

<span data-ttu-id="a4175-125">Otwórz przeglądarkę i przejdź do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4175-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="a4175-126">Tworzenie profilu i punktu końcowego usługi CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="a4175-127">Na lewym panelu nawigacyjnym wybierz pozycję **App Services**, a następnie wybierz aplikację utworzoną w samouczku [tworzenie statycznej witryny HTML — szybki start](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="a4175-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Wybieranie aplikacji usługi App Service w portalu](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="a4175-129">Na stronie **App Service** w sekcji **Ustawienia** wybierz pozycję **Sieć > Skonfiguruj usługę Azure CDN dla aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a4175-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Wybieranie usługi CDN w portalu](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="a4175-131">Na stronie **Azure Content Delivery Network** określ ustawienia dla **nowego punktu końcowego** zgodnie z informacjami podanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a4175-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Tworzenie profilu i punktu końcowego w portalu](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="a4175-133">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="a4175-133">Setting</span></span> | <span data-ttu-id="a4175-134">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="a4175-134">Suggested value</span></span> | <span data-ttu-id="a4175-135">Opis</span><span class="sxs-lookup"><span data-stu-id="a4175-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="a4175-136">**Profil CDN**</span><span class="sxs-lookup"><span data-stu-id="a4175-136">**CDN profile**</span></span> | <span data-ttu-id="a4175-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="a4175-137">myCDNProfile</span></span> | <span data-ttu-id="a4175-138">Wybierz **Utwórz nowy** można utworzyć profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="a4175-139">Profil CDN jest kolekcją punktów końcowych usługi CDN znajdujących się w tej samej warstwie cenowej.</span><span class="sxs-lookup"><span data-stu-id="a4175-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="a4175-140">**Warstwa cenowa**</span><span class="sxs-lookup"><span data-stu-id="a4175-140">**Pricing tier**</span></span> | <span data-ttu-id="a4175-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="a4175-141">Standard Akamai</span></span> | <span data-ttu-id="a4175-142">[Warstwa cenowa](../cdn/cdn-overview.md#azure-cdn-features) określa dostawcę i dostępne funkcje.</span><span class="sxs-lookup"><span data-stu-id="a4175-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="a4175-143">W tym samouczku używamy Akamai standardowa.</span><span class="sxs-lookup"><span data-stu-id="a4175-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="a4175-144">**Nazwa punktu końcowego usługi CDN**</span><span class="sxs-lookup"><span data-stu-id="a4175-144">**CDN endpoint name**</span></span> | <span data-ttu-id="a4175-145">Dowolna unikatowa nazwa w domenie azureedge.net</span><span class="sxs-lookup"><span data-stu-id="a4175-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="a4175-146">Dostęp do zbuforowanych zasobów można uzyskać w domenie *\<nazwapunktukoncowego>.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="a4175-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="a4175-147">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a4175-147">Select **Create**.</span></span>

<span data-ttu-id="a4175-148">Na platformie Azure zostanie utworzony profil i punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="a4175-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="a4175-149">Nowy punkt końcowy zostanie wyświetlony na liście **Punkty końcowe**, a kiedy zostanie zaprowizowany, będzie miał stan **Uruchomiono**.</span><span class="sxs-lookup"><span data-stu-id="a4175-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Nowy punkt końcowy na liście](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="a4175-151">Testowanie punktu końcowego usługi CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-151">Test the CDN endpoint</span></span>

<span data-ttu-id="a4175-152">W przypadku wybrania warstwy cenowej Verizon propagacja punktu końcowego trwa zwykle około 90 minut.</span><span class="sxs-lookup"><span data-stu-id="a4175-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="a4175-153">W przypadku warstwy Akamai propagacja zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a4175-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="a4175-154">Przykładowa aplikacja ma plik `index.html` i foldery *css*, *img* oraz *js*, które zawierają inne statyczne elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4175-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="a4175-155">Ścieżki zawartości dla wszystkich tych plików są takie same w punkcie końcowym usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="a4175-156">Na przykład oba następujące adresy URL umożliwiają dostęp do pliku *bootstrap.css* w folderze *css*:</span><span class="sxs-lookup"><span data-stu-id="a4175-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="a4175-157">Przejdź przeglądarki pod następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="a4175-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Strona główna aplikacji przykładowej udostępnianej przez usługę CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="a4175-159">Zostanie wyświetlona strona tego samego, który został przeprowadzony wcześniej w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4175-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="a4175-160">Usługi Azure CDN ma pobrać zasobów aplikacji sieci web pochodzenia i obsługujący z punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="a4175-161">Odśwież tę stronę, aby się upewnić, że jest ona buforowana w usłudze CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="a4175-162">Aby usługa CDN umieściła żądaną zawartość w pamięci podręcznej, czasami wymagane są dwa żądania tego samego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4175-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="a4175-163">Aby uzyskać więcej informacji o sposobie tworzenia profilów i punktów końcowych usługi Azure CDN, zobacz [Wprowadzenie do usługi Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a4175-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="a4175-164">Przeczyszczanie usługi CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-164">Purge the CDN</span></span>

<span data-ttu-id="a4175-165">Usługa CDN okresowo odświeża swoje zasoby z oryginalnej aplikacji sieci Web zgodnie z konfiguracją czasu wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="a4175-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="a4175-166">Domyślny czas wygaśnięcia wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="a4175-166">The default TTL is seven days.</span></span>

<span data-ttu-id="a4175-167">Czasami może zajść konieczność odświeżenia usługi CDN przed upływem czasu wygaśnięcia — na przykład podczas wdrażania zaktualizowanej zawartości w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a4175-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="a4175-168">Aby wyzwolić odświeżanie, można ręcznie przeczyścić zasoby usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="a4175-169">W tej części samouczka zostanie wdrożona zmiana w aplikacji sieci Web i nastąpi przeczyszczenie usługi CDN w celu wyzwolenia odświeżenia pamięci podręcznej tej usługi.</span><span class="sxs-lookup"><span data-stu-id="a4175-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="a4175-170">Wdrażanie zmiany w aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a4175-170">Deploy a change to the web app</span></span>

<span data-ttu-id="a4175-171">Otwórz plik `index.html` i dodaj ciąg „-V2” do nagłówka H1, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a4175-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="a4175-172">Zatwierdź zmianę i wdróż ją w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a4175-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="a4175-173">Po zakończeniu wdrażania przejdź do adresu URL aplikacji sieci Web i zobacz, czy zmiana jest widoczna.</span><span class="sxs-lookup"><span data-stu-id="a4175-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Ciąg V2 w tytule aplikacji sieci Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="a4175-175">Po przejściu do adresu URL punktu końcowego usługi CDN dla strony głównej zobaczysz, że wprowadzona zmiana nie jest widoczna, ponieważ wersja zbuforowana w usłudze CDN jeszcze nie wygasła.</span><span class="sxs-lookup"><span data-stu-id="a4175-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Brak ciągu V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="a4175-177">Przeczyszczanie usługi CDN w portalu</span><span class="sxs-lookup"><span data-stu-id="a4175-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="a4175-178">Aby w usłudze CDN wyzwolić zaktualizowanie zbuforowanej wersji, przeczyść usługę CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="a4175-179">Na lewym panelu nawigacyjnym portalu wybierz pozycję **Grupy zasobów**, a następnie wybierz grupę zasobów utworzoną na potrzeby aplikacji sieci Web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="a4175-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Wybieranie grupy zasobów](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="a4175-181">Na liście zasobów wybierz punkt końcowy usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-181">In the list of resources, select your CDN endpoint.</span></span>

![Wybieranie punktu końcowego](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="a4175-183">W górnej części strony **Punkt końcowy** kliknij pozycję **Przeczyść**.</span><span class="sxs-lookup"><span data-stu-id="a4175-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Wybieranie pozycji Przeczyść](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="a4175-185">Wprowadź ścieżki zawartości, które chcesz przeczyścić.</span><span class="sxs-lookup"><span data-stu-id="a4175-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="a4175-186">Możesz podać pełną ścieżkę, aby przeczyścić pojedynczy plik, lub segment ścieżki, aby przeczyścić i odświeżyć całą zawartość folderu.</span><span class="sxs-lookup"><span data-stu-id="a4175-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="a4175-187">Ponieważ zmieniono plik `index.html`, upewnij się, że znajduje się on w jednej ze ścieżek.</span><span class="sxs-lookup"><span data-stu-id="a4175-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="a4175-188">W dolnej części strony wybierz pozycję **Przeczyść**.</span><span class="sxs-lookup"><span data-stu-id="a4175-188">At the bottom of the page, select **Purge**.</span></span>

![Strona przeczyszczania](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="a4175-190">Sprawdzanie zaktualizowania usługi CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="a4175-191">Poczekaj na zakończenie przetwarzania żądania przeczyszczenia (zwykle trwa to kilka minut).</span><span class="sxs-lookup"><span data-stu-id="a4175-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="a4175-192">Aby wyświetlić bieżący stan, wybierz ikonę dzwonka w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="a4175-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Powiadomienie o przeczyszczaniu](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="a4175-194">Przejdź do adresu URL punktu końcowego usługi CDN dla pliku `index.html`, a zobaczysz, że teraz ciąg V2 jest już widoczny w tytule strony głównej.</span><span class="sxs-lookup"><span data-stu-id="a4175-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="a4175-195">Oznacza to, że pamięć podręczna usługi CDN została odświeżona.</span><span class="sxs-lookup"><span data-stu-id="a4175-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Ciąg V2 w tytule w usłudze CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="a4175-197">Aby uzyskać więcej informacji, zobacz [Przeczyszczanie punktu końcowego usługi Azure CDN](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a4175-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="a4175-198">Używanie ciągów zapytań do sterowania wersjami zawartości</span><span class="sxs-lookup"><span data-stu-id="a4175-198">Use query strings to version content</span></span>

<span data-ttu-id="a4175-199">Usługa Azure CDN oferuje następujące opcje zachowania podczas buforowania:</span><span class="sxs-lookup"><span data-stu-id="a4175-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="a4175-200">Ignoruj ciągi zapytań</span><span class="sxs-lookup"><span data-stu-id="a4175-200">Ignore query strings</span></span>
* <span data-ttu-id="a4175-201">Pomiń buforowanie dla ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="a4175-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="a4175-202">Buforuj każdy unikatowy adres URL</span><span class="sxs-lookup"><span data-stu-id="a4175-202">Cache every unique URL</span></span> 

<span data-ttu-id="a4175-203">Pierwszy z nich jest wartość domyślna, co oznacza, że istnieje tylko jedna wersja buforowanych zasobów, niezależnie od tego ciągu zapytania w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="a4175-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="a4175-204">W tej części samouczka zostanie zmienione zachowanie buforowania w taki sposób, że w pamięci podręcznej będzie umieszczany każdy unikatowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="a4175-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="a4175-205">Zmienianie zachowania buforowania</span><span class="sxs-lookup"><span data-stu-id="a4175-205">Change the cache behavior</span></span>

<span data-ttu-id="a4175-206">W witrynie Azure Portal na stronie **Punkt końcowy usługi CDN** wybierz pozycję **Pamięć podręczna**.</span><span class="sxs-lookup"><span data-stu-id="a4175-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="a4175-207">Z listy rozwijanej **Zachowanie buforowania ciągu kwerendy** wybierz pozycję **Buforuj każdy unikatowy adres URL**.</span><span class="sxs-lookup"><span data-stu-id="a4175-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="a4175-208">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a4175-208">Select **Save**.</span></span>

![Wybieranie zachowania buforowania ciągów zapytań](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="a4175-210">Sprawdzanie, czy unikatowe adresy URL są buforowane osobno</span><span class="sxs-lookup"><span data-stu-id="a4175-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="a4175-211">W przeglądarce przejdź do strony głównej w punkcie końcowym usługi CDN, ale dołącz ciąg zapytania:</span><span class="sxs-lookup"><span data-stu-id="a4175-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="a4175-212">Usługa CDN zwraca bieżącą zawartość aplikacji sieci Web, w tym ciąg „V2” w nagłówku.</span><span class="sxs-lookup"><span data-stu-id="a4175-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="a4175-213">Odśwież tę stronę, aby się upewnić, że jest ona buforowana w usłudze CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="a4175-214">Otwórz plik `index.html` i zamień ciąg „V2” na „V3”, a następnie wdróż tę zmianę.</span><span class="sxs-lookup"><span data-stu-id="a4175-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="a4175-215">W przeglądarce przejdź do adresu URL punktu końcowego usługi CDN, korzystając z nowego ciągu zapytania, na przykład `q=2`.</span><span class="sxs-lookup"><span data-stu-id="a4175-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="a4175-216">Usługa CDN pobierze bieżący plik `index.html` i wyświetli ciąg „V3”.</span><span class="sxs-lookup"><span data-stu-id="a4175-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="a4175-217">Jednak jeśli przejdziesz do punktu końcowego usługi CDN, korzystając z ciągu zapytania `q=1`, zobaczysz ciąg „V2”.</span><span class="sxs-lookup"><span data-stu-id="a4175-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 w tytule w usłudze CDN, ciąg zapytania 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 w tytule w usłudze CDN, ciąg zapytania 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="a4175-220">Te dane wyjściowe pokazuje, czy każdy ciąg zapytania jest traktowane inaczej:</span><span class="sxs-lookup"><span data-stu-id="a4175-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="a4175-221">q = 1 był używany przed, więc zawartości z pamięci podręcznej są zwracane (V2).</span><span class="sxs-lookup"><span data-stu-id="a4175-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="a4175-222">q = 2 jest nowy, więc pobierania najnowszej zawartości aplikacji sieci web i zwracane (V3).</span><span class="sxs-lookup"><span data-stu-id="a4175-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="a4175-223">Aby uzyskać więcej informacji, zobacz [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md) (Sterowanie zachowaniem buforowania usługi CDN za pomocą ciągów zapytań).</span><span class="sxs-lookup"><span data-stu-id="a4175-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="a4175-224">Mapowanie domeny niestandardowej na punkt końcowy usługi CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="a4175-225">Mapowanie domeny niestandardowej na punkt końcowy usługi CDN odbywa się przez utworzenie rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="a4175-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="a4175-226">Rekord CNAME jest funkcją systemu DNS, która mapuje domenę źródłową na domenę docelową.</span><span class="sxs-lookup"><span data-stu-id="a4175-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="a4175-227">Na przykład można mapować domenę `cdn.contoso.com` lub `static.contoso.com` na `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="a4175-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="a4175-228">Jeśli nie masz domeny niestandardowej, możesz postępować według instrukcji zawartych w [samouczku dotyczącym domeny usługi App Service](custom-dns-web-site-buydomains-web-app.md) w celu zakupienia domeny za pośrednictwem witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a4175-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="a4175-229">Znajdowanie nazwy hosta do użycia z rekordem CNAME</span><span class="sxs-lookup"><span data-stu-id="a4175-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="a4175-230">W witrynie Azure Portal na stronie **Punkt końcowy** wybierz na lewym panelu nawigacyjnym pozycję **Przegląd** i w górnej części strony wybierz przycisk **+ Domena niestandardowa**.</span><span class="sxs-lookup"><span data-stu-id="a4175-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Wybieranie opcji dodawania domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="a4175-232">Na stronie **Dodaj domenę niestandardową** zobaczysz nazwę hosta punktu końcowego do użycia w celu utworzenia rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="a4175-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="a4175-233">Nazwa hosta jest tworzona na podstawie adresu URL punktu końcowego usługi CDN:  **&lt;NazwaPunktuKoncowego>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="a4175-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Strona dodawania domeny](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="a4175-235">Konfigurowanie rekordu CNAME u rejestratora domen</span><span class="sxs-lookup"><span data-stu-id="a4175-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="a4175-236">Przejdź do witryny sieci Web swojego rejestratora domen i znajdź sekcję tworzenia rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="a4175-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="a4175-237">Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).</span><span class="sxs-lookup"><span data-stu-id="a4175-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="a4175-238">Znajdź sekcję zarządzania rekordami CNAME.</span><span class="sxs-lookup"><span data-stu-id="a4175-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="a4175-239">W tym celu może być konieczne przejście do strony ustawień zaawansowanych i poszukanie słów CNAME, Alias lub Subdomains (Poddomeny).</span><span class="sxs-lookup"><span data-stu-id="a4175-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="a4175-240">Utwórz rekord CNAME mapujący z wybranym domeny podrzędnej (na przykład **statycznych** lub **cdn**) do **nazwę hosta punktu końcowego** pokazano wcześniej w portalu.</span><span class="sxs-lookup"><span data-stu-id="a4175-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="a4175-241">Wprowadzanie domeny niestandardowej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a4175-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="a4175-242">Powróć do strony **Dodaj domenę niestandardową** i wprowadź w oknie dialogowym domenę niestandardową, w tym poddomenę.</span><span class="sxs-lookup"><span data-stu-id="a4175-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="a4175-243">Na przykład wprowadź wartość `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a4175-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="a4175-244">Platforma Azure sprawdzi, czy dla wprowadzonej nazwy domeny istnieje rekord CNAME.</span><span class="sxs-lookup"><span data-stu-id="a4175-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="a4175-245">Jeśli rekord CNAME jest poprawny, domena niestandardowa jest weryfikowana.</span><span class="sxs-lookup"><span data-stu-id="a4175-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="a4175-246">Może upłynąć trochę czasu, zanim rekord CNAME zostanie rozpropagowany do serwerów nazw w Internecie.</span><span class="sxs-lookup"><span data-stu-id="a4175-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="a4175-247">Jeśli domena nie została zweryfikowana natychmiast, zaczekaj kilka minut i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="a4175-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="a4175-248">Testowanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="a4175-248">Test the custom domain</span></span>

<span data-ttu-id="a4175-249">W przeglądarce przejdź do pliku `index.html`, korzystając z domeny niestandardowej (na przykład `cdn.contoso.com/index.html`), aby sprawdzić, czy wynik jest taki sam jak podczas bezpośredniego przechodzenia do adresu `<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="a4175-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Strona główna przykładowej aplikacji wyświetlona przy użyciu adresu URL domeny niestandardowej](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="a4175-251">Aby uzyskać więcej informacji, zobacz [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md) (Mapowanie zawartości usługi Azure CDN na domenę niestandardową).</span><span class="sxs-lookup"><span data-stu-id="a4175-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="a4175-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4175-252">Next steps</span></span>

<span data-ttu-id="a4175-253">Wiadomości:</span><span class="sxs-lookup"><span data-stu-id="a4175-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4175-254">Tworzenie punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="a4175-255">Odświeżanie elementów zawartości zapisanych w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="a4175-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="a4175-256">Używanie ciągów zapytań do sterowania zbuforowanymi wersjami.</span><span class="sxs-lookup"><span data-stu-id="a4175-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="a4175-257">Używanie domeny niestandardowej na potrzeby punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="a4175-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="a4175-258">Dowiedz się, jak zoptymalizować wydajność sieci CDN w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="a4175-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4175-259">Poprawianie wydajności poprzez kompresowanie plików w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4175-260">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a4175-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
