---
title: "Mapowanie istniejących niestandardową nazwę DNS do aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać istniejącą nazwę domeny DNS niestandardowe (niestandardowych domeny) do aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
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
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="b018f-103">Mapowanie istniejących niestandardową nazwę DNS do aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="b018f-104">Usługa [Azure Web Apps](app-service-web-overview.md) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="b018f-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b018f-105">W tym samouczku przedstawiono sposób odwzorowywania istniejącej nazwy DNS niestandardowej aplikacji sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="b018f-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="b018f-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b018f-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b018f-108">Mapowanie poddomeny (na przykład `www.contoso.com`) przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b018f-109">Mapowanie domeny katalogu głównego (na przykład `contoso.com`) przy użyciu rekord a.</span><span class="sxs-lookup"><span data-stu-id="b018f-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="b018f-110">Zamapować domenę symboli wieloznacznych (na przykład `*.contoso.com`) przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b018f-111">Mapowanie domeny przy użyciu skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="b018f-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="b018f-112">Możesz użyć dowolnej **rekord CNAME** lub **rekordu** do mapowania niestandardową nazwę DNS usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="b018f-113">Zalecane jest użycie rekord CNAME dla wszystkich niestandardowych nazw DNS z wyjątkiem domeny katalogu głównego (na przykład `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b018f-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="b018f-114">Aby przeprowadzić migrację na żywo lokacji i nazwy domeny DNS do usługi App Service, zobacz [migracji active nazwy DNS w usłudze Azure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b018f-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b018f-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b018f-115">Prerequisites</span></span>

<span data-ttu-id="b018f-116">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="b018f-116">To complete this tutorial:</span></span>

* <span data-ttu-id="b018f-117">[Utwórz aplikację usługi aplikacji](/azure/app-service/), lub użyć utworzonego w samouczku innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="b018f-118">Kup nazwę domeny i upewnij się, że masz dostęp do rejestru DNS dla domeny dostawcy (takie jak GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="b018f-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="b018f-119">Na przykład, aby dodać wpisów DNS dla `contoso.com` i `www.contoso.com`, użytkownik musi mieć możliwość skonfigurowania ustawień DNS dla `contoso.com` domeny głównej.</span><span class="sxs-lookup"><span data-stu-id="b018f-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b018f-120">Jeśli nie masz istniejącej domeny nazwa, należy wziąć pod uwagę [zakupu domeny przy użyciu portalu Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b018f-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="b018f-121">Przygotowywanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b018f-121">Prepare the app</span></span>

<span data-ttu-id="b018f-122">Aby zamapować niestandardową nazwę DNS w aplikacji sieci web, aplikacji sieci web firmy [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być płatną warstwy (**Shared**, **podstawowe**, **standardowe**, lub  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="b018f-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="b018f-123">W tym kroku należy upewnić się, że aplikacja usługi aplikacji jest w obsługiwanym warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="b018f-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="b018f-124">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-124">Sign in to Azure</span></span>

<span data-ttu-id="b018f-125">Otwórz [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b018f-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="b018f-126">Przejdź do aplikacji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="b018f-127">Wybierz z menu po lewej stronie **usługi aplikacji**, a następnie wybierz nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="b018f-129">Zostanie wyświetlona strona zarządzania aplikacji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="b018f-130">Sprawdź warstwę cenową</span><span class="sxs-lookup"><span data-stu-id="b018f-130">Check the pricing tier</span></span>

<span data-ttu-id="b018f-131">W lewym obszarze nawigacji strony aplikacji, przewiń **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.</span><span class="sxs-lookup"><span data-stu-id="b018f-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="b018f-133">Warstwa bieżąca aplikacja zostanie wyróżniona niebieskim obramowaniem.</span><span class="sxs-lookup"><span data-stu-id="b018f-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="b018f-134">Upewnij się, że aplikacja nie znajduje się w **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b018f-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="b018f-135">Niestandardowe DNS nie jest obsługiwany w **wolne** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b018f-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="b018f-137">Jeśli plan usługi aplikacji nie jest **wolne**, Zamknij **wybierz warstwę cenową** strony i przejść [mapy rekord CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="b018f-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="b018f-138">Skalowanie w górę plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b018f-138">Scale up the App Service plan</span></span>

<span data-ttu-id="b018f-139">Wybierz jedno z systemem innym niż bez warstw (**Shared**, **podstawowe**, **standardowe**, lub **Premium**).</span><span class="sxs-lookup"><span data-stu-id="b018f-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="b018f-140">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="b018f-140">Click **Select**.</span></span>

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="b018f-142">Gdy zostanie wyświetlone następujące powiadomienie, zakończeniu operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b018f-142">When you see the following notification, the scale operation is complete.</span></span>

![Potwierdzenie operacji skalowania](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="b018f-144">Mapa rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-144">Map a CNAME record</span></span>

<span data-ttu-id="b018f-145">W przykładzie samouczek, Dodaj rekord CNAME dla `www` domeny podrzędnej (na przykład `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b018f-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="b018f-146">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-146">Create the CNAME record</span></span>

<span data-ttu-id="b018f-147">Dodaj rekord CNAME do mapowania poddomeny hostname domyślnej aplikacji (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="b018f-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="b018f-148">Aby uzyskać `www.contoso.com` przykład domeny, Dodaj rekord CNAME, który mapuje nazwę `www` do `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b018f-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b018f-149">Po dodaniu CNAME stronie rekordy DNS wygląda jak w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b018f-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="b018f-151">Włącz mapowania rekord CNAME w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="b018f-152">W lewym obszarze nawigacji strony aplikacji w portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="b018f-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b018f-154">W **domen niestandardowych** strony aplikacji, należy dodać w pełni kwalifikowana nazwa DNS niestandardowe (`www.contoso.com`) do listy.</span><span class="sxs-lookup"><span data-stu-id="b018f-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="b018f-155">Wybierz  **+**  obok opcji **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-155">Select the **+** icon next to **Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b018f-157">Wpisz w pełni kwalifikowaną nazwę domeny dodaje rekord CNAME, takich jak `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b018f-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="b018f-158">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="b018f-158">Select **Validate**.</span></span>

<span data-ttu-id="b018f-159">**Dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="b018f-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b018f-160">Upewnij się, że **typu rekordu Hostname** ustawiono **CNAME (www.example.com lub wszystkie poddomeny)**.</span><span class="sxs-lookup"><span data-stu-id="b018f-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b018f-161">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-161">Select **Add hostname**.</span></span>

![Dodaj nazwę DNS do aplikacji](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="b018f-163">Może upłynąć trochę czasu, zanim nowej nazwy hosta zostaną odzwierciedlone w aplikacji **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="b018f-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b018f-164">Spróbuj odświeżyć przeglądarkę, aby zaktualizować dane.</span><span class="sxs-lookup"><span data-stu-id="b018f-164">Try refreshing the browser to update the data.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="b018f-166">Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="b018f-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="b018f-168">Mapa rekord a.</span><span class="sxs-lookup"><span data-stu-id="b018f-168">Map an A record</span></span>

<span data-ttu-id="b018f-169">W przykładzie samouczek dodaniu rekordu A dla domeny katalogu głównego (na przykład `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b018f-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="b018f-170">Skopiuj adres IP aplikacji</span><span class="sxs-lookup"><span data-stu-id="b018f-170">Copy the app's IP address</span></span>

<span data-ttu-id="b018f-171">Aby zamapować rekord A, należy aplikacji zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="b018f-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="b018f-172">Ten adres IP można znaleźć w aplikacji **domen niestandardowych** strony w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b018f-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="b018f-173">W lewym obszarze nawigacji strony aplikacji w portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="b018f-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b018f-175">W **domen niestandardowych** strony, skopiuj adres IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="b018f-177">Utwórz rekord a.</span><span class="sxs-lookup"><span data-stu-id="b018f-177">Create the A record</span></span>

<span data-ttu-id="b018f-178">Aby mapować rekordu A dla aplikacji, usługa aplikacji wymaga **dwóch** rekordy DNS:</span><span class="sxs-lookup"><span data-stu-id="b018f-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="b018f-179">**A** rekordu mapowane na adres IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b018f-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="b018f-180">A **TXT** rekordu do mapowania nazwy hosta domyślnego aplikacji `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b018f-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="b018f-181">Usługa aplikacji używa tego rekordu tylko podczas konfiguracji, aby sprawdzić, czy jesteś właścicielem domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="b018f-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="b018f-182">Po domeny niestandardowej jest weryfikowane i skonfigurowaniu w usłudze App Service, można usunąć tego rekordu TXT.</span><span class="sxs-lookup"><span data-stu-id="b018f-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="b018f-183">Dla `contoso.com` przykład domeny utworzyć rekordy A i TXT, zgodnie z poniższą tabelą (`@` zazwyczaj reprezentuje domeny głównej).</span><span class="sxs-lookup"><span data-stu-id="b018f-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="b018f-184">Typ rekordu</span><span class="sxs-lookup"><span data-stu-id="b018f-184">Record type</span></span> | <span data-ttu-id="b018f-185">Host</span><span class="sxs-lookup"><span data-stu-id="b018f-185">Host</span></span> | <span data-ttu-id="b018f-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="b018f-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="b018f-187">A</span><span class="sxs-lookup"><span data-stu-id="b018f-187">A</span></span> | `@` | <span data-ttu-id="b018f-188">Adres IP z [skopiuj adres IP aplikacji](#info)</span><span class="sxs-lookup"><span data-stu-id="b018f-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="b018f-189">TXT</span><span class="sxs-lookup"><span data-stu-id="b018f-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="b018f-190">Rekordy są dodawane, stronie rekordy DNS wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b018f-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Strona rekordów DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="b018f-192">Włącz mapowanie rekord A w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b018f-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="b018f-193">W aplikacji **domen niestandardowych** w portalu Azure, należy dodać w pełni kwalifikowana nazwa DNS niestandardowe (na przykład `contoso.com`) do listy.</span><span class="sxs-lookup"><span data-stu-id="b018f-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="b018f-194">Wybierz  **+**  obok opcji **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-194">Select the **+** icon next to **Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="b018f-196">Wpisz w pełni kwalifikowaną nazwę domeny skonfigurować rekord A, takich jak `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b018f-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="b018f-197">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="b018f-197">Select **Validate**.</span></span>

<span data-ttu-id="b018f-198">**Dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="b018f-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b018f-199">Upewnij się, że **typu rekordu Hostname** ustawiono **rekordu (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="b018f-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="b018f-200">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-200">Select **Add hostname**.</span></span>

![Dodaj nazwę DNS do aplikacji](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="b018f-202">Może upłynąć trochę czasu, zanim nowej nazwy hosta zostaną odzwierciedlone w aplikacji **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="b018f-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b018f-203">Spróbuj odświeżyć przeglądarkę, aby zaktualizować dane.</span><span class="sxs-lookup"><span data-stu-id="b018f-203">Try refreshing the browser to update the data.</span></span>

![Dodaje rekord](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="b018f-205">Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="b018f-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="b018f-207">Zamapować domenę symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="b018f-207">Map a wildcard domain</span></span>

<span data-ttu-id="b018f-208">W tym przykładzie samouczek mapy [nazwa DNS z symbolem wieloznacznym](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (na przykład `*.contoso.com`) do aplikacji usługi app Service przez dodanie rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="b018f-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="b018f-209">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-209">Create the CNAME record</span></span>

<span data-ttu-id="b018f-210">Dodaj rekord CNAME do mapowania nazwy symbolu wieloznacznego hostname domyślnej aplikacji (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="b018f-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="b018f-211">Dla `*.contoso.com` przykład domeny rekord CNAME przypisze nazwę `*` do `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b018f-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b018f-212">Po dodaniu CNAME stronie rekordy DNS wygląda jak w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b018f-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="b018f-214">Włącz mapowanie rekord CNAME w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b018f-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="b018f-215">Można teraz dodawać żadnych poddomeny zgodnej z nazwą symbolu wieloznacznego w aplikacji (na przykład `sub1.contoso.com` i `sub2.contoso.com` odpowiada `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b018f-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="b018f-216">W lewym obszarze nawigacji strony aplikacji w portalu Azure, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="b018f-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b018f-218">Wybierz  **+**  obok opcji **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-218">Select the **+** icon next to **Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b018f-220">Wpisz nazwę FQDN, która pasuje do domeny symbolu wieloznacznego (na przykład `sub1.contoso.com`), a następnie wybierz **weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="b018f-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="b018f-221">**Dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="b018f-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b018f-222">Upewnij się, że **typu rekordu Hostname** ustawiono **rekord CNAME (www.example.com lub wszystkie poddomeny)**.</span><span class="sxs-lookup"><span data-stu-id="b018f-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b018f-223">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="b018f-223">Select **Add hostname**.</span></span>

![Dodaj nazwę DNS do aplikacji](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="b018f-225">Może upłynąć trochę czasu, zanim nowej nazwy hosta zostaną odzwierciedlone w aplikacji **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="b018f-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b018f-226">Spróbuj odświeżyć przeglądarkę, aby zaktualizować dane.</span><span class="sxs-lookup"><span data-stu-id="b018f-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="b018f-227">Wybierz  **+**  ikonę ponownie, aby dodać inną nazwę hosta odpowiadający domenie symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="b018f-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="b018f-228">Na przykład dodać `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b018f-228">For example, add `sub2.contoso.com`.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="b018f-230">Testowanie w przeglądarce</span><span class="sxs-lookup"><span data-stu-id="b018f-230">Test in browser</span></span>

<span data-ttu-id="b018f-231">Przejdź do nazwy DNS, który został wcześniej skonfigurowany (na przykład `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, i `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b018f-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="b018f-233">Zautomatyzować za pomocą skryptów</span><span class="sxs-lookup"><span data-stu-id="b018f-233">Automate with scripts</span></span>

<span data-ttu-id="b018f-234">Można zautomatyzować zarządzanie domenami niestandardowymi za pomocą skryptów, za pomocą [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b018f-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="b018f-235">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-235">Azure CLI</span></span> 

<span data-ttu-id="b018f-236">Polecenie dodaje skonfigurowanej niestandardowe nazwy DNS do aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="b018f-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="b018f-237">Aby uzyskać więcej informacji, zobacz [zamapować niestandardową domenę do aplikacji sieci web](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b018f-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="b018f-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b018f-238">Azure PowerShell</span></span> 

<span data-ttu-id="b018f-239">Polecenie dodaje skonfigurowanej niestandardowe nazwy DNS do aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="b018f-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="b018f-240">Aby uzyskać więcej informacji, zobacz [przypisać niestandardową domenę do aplikacji sieci web](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b018f-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b018f-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b018f-241">Next steps</span></span>

<span data-ttu-id="b018f-242">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b018f-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b018f-243">Mapa poddomeny przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="b018f-244">Mapa domeny głównej, przy użyciu rekord a.</span><span class="sxs-lookup"><span data-stu-id="b018f-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="b018f-245">Zamapować domenę symboli wieloznacznych przy użyciu rekordu CNAME</span><span class="sxs-lookup"><span data-stu-id="b018f-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="b018f-246">Mapowanie domeny przy użyciu skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="b018f-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="b018f-247">Przejdź do następnego samouczek informacje na temat wiązania niestandardowego certyfikatu SSL w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b018f-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b018f-248">Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="b018f-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
