---
title: "Migracji active nazwy DNS w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przeprowadzić migrację niestandardowej nazwy domeny DNS, który jest już przypisany do lokacji na żywo w usłudze Azure App Service bez żadnego przestoju."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="199db-103">Migracji active nazwy DNS w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="199db-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="199db-104">W tym artykule przedstawiono sposób migracji active nazwy DNS [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) bez żadnego przestoju.</span><span class="sxs-lookup"><span data-stu-id="199db-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="199db-105">Podczas migracji na żywo lokacji i nazwy domeny DNS do usługi App Service, tej nazwy DNS jest już obsługujące ruch na żywo.</span><span class="sxs-lookup"><span data-stu-id="199db-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="199db-106">Aby uniknąć przestój w przypadku rozpoznawania nazw DNS podczas migracji, można preemptively powiązanie nazwy DNS active aplikację usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="199db-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="199db-107">Jeśli nie możesz Obawiamy o przestój w przypadku rozpoznawania nazw DNS, zobacz [mapowania istniejącej nazwy DNS niestandardowej aplikacji sieci Web Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="199db-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="199db-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="199db-108">Prerequisites</span></span>

<span data-ttu-id="199db-109">Aby ukończyć ten Porada:</span><span class="sxs-lookup"><span data-stu-id="199db-109">To complete this how-to:</span></span>

- <span data-ttu-id="199db-110">[Upewnij się, że aplikację usługi aplikacji nie znajduje się w warstwie bezpłatna](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="199db-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="199db-111">Powiąż preemptively nazwy domeny</span><span class="sxs-lookup"><span data-stu-id="199db-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="199db-112">Gdy powiąże preemptively niestandardową domenę, wykonywać następujące przed wprowadzeniem jakichkolwiek zmian w rekordach DNS:</span><span class="sxs-lookup"><span data-stu-id="199db-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="199db-113">Zweryfikuj prawo własności do domeny</span><span class="sxs-lookup"><span data-stu-id="199db-113">Verify domain ownership</span></span>
- <span data-ttu-id="199db-114">Włącz nazwy domeny dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="199db-114">Enable the domain name for your app</span></span>

<span data-ttu-id="199db-115">Na koniec migracji nazwę DNS niestandardowych ze starej witryny do aplikacji usługi app Service, nie będzie bez przestojów w rozpoznawania nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="199db-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="199db-116">Utwórz rekord weryfikacji domeny</span><span class="sxs-lookup"><span data-stu-id="199db-116">Create domain verification record</span></span>

<span data-ttu-id="199db-117">Aby zweryfikować prawo własności do domeny, Dodaj rekord TXT.</span><span class="sxs-lookup"><span data-stu-id="199db-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="199db-118">Rekord TXT mapy z _awverify.&lt; Poddomena >_ do  _&lt;nazwa_aplikacji >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="199db-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="199db-119">Rekord TXT, które są potrzebne, zależy od rekord DNS, który chcesz przeprowadzić migrację.</span><span class="sxs-lookup"><span data-stu-id="199db-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="199db-120">Aby uzyskać przykłady, zobacz poniższą tabelę (`@` zazwyczaj reprezentuje domeny katalogu głównego):</span><span class="sxs-lookup"><span data-stu-id="199db-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="199db-121">Przykładowy rekord DNS</span><span class="sxs-lookup"><span data-stu-id="199db-121">DNS record example</span></span> | <span data-ttu-id="199db-122">TXT Host</span><span class="sxs-lookup"><span data-stu-id="199db-122">TXT Host</span></span> | <span data-ttu-id="199db-123">Wartość TXT</span><span class="sxs-lookup"><span data-stu-id="199db-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="199db-124">@ (root)</span><span class="sxs-lookup"><span data-stu-id="199db-124">@ (root)</span></span> | <span data-ttu-id="199db-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="199db-125">_awverify_</span></span> | <span data-ttu-id="199db-126">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="199db-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="199db-127">WWW (sub)</span><span class="sxs-lookup"><span data-stu-id="199db-127">www (sub)</span></span> | <span data-ttu-id="199db-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="199db-128">_awverify.www_</span></span> | <span data-ttu-id="199db-129">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="199db-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="199db-130">\*(symbol wieloznaczny)</span><span class="sxs-lookup"><span data-stu-id="199db-130">\* (wildcard)</span></span> | <span data-ttu-id="199db-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="199db-131">_awverify.\*_</span></span> | <span data-ttu-id="199db-132">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="199db-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="199db-133">Na stronie rekordy DNS należy pamiętać, typ rekordu nazwy DNS, które chcesz migrować.</span><span class="sxs-lookup"><span data-stu-id="199db-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="199db-134">Usługa aplikacji obsługuje mapowania z CNAME i.</span><span class="sxs-lookup"><span data-stu-id="199db-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="199db-135">Włącz domeny aplikacji</span><span class="sxs-lookup"><span data-stu-id="199db-135">Enable the domain for your app</span></span>

<span data-ttu-id="199db-136">W [portalu Azure](https://portal.azure.com), w lewym obszarze nawigacji strony aplikacji, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="199db-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="199db-138">W **domen niestandardowych** wybierz pozycję  **+**  obok opcji **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="199db-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="199db-140">Wpisz w pełni kwalifikowaną nazwę domeny dodaje rekord TXT, takich jak `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="199db-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="199db-141">Dla domeny symbolu wieloznacznego (takich jak \*. contoso.com), można użyć dowolnej nazwy DNS, która pasuje do domeny symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="199db-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="199db-142">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="199db-142">Select **Validate**.</span></span>

<span data-ttu-id="199db-143">**Dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="199db-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="199db-144">Upewnij się, że **typu rekordu Hostname** ustawiono typ rekordu DNS chcesz migrować.</span><span class="sxs-lookup"><span data-stu-id="199db-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="199db-145">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="199db-145">Select **Add hostname**.</span></span>

![Dodaj nazwę DNS do aplikacji](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="199db-147">Może upłynąć trochę czasu, zanim nowej nazwy hosta zostaną odzwierciedlone w aplikacji **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="199db-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="199db-148">Spróbuj odświeżyć przeglądarkę, aby zaktualizować dane.</span><span class="sxs-lookup"><span data-stu-id="199db-148">Try refreshing the browser to update the data.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="199db-150">Niestandardowe nazwę DNS jest teraz włączone w aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="199db-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="199db-151">Ponowne mapowanie active nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="199db-151">Remap the active DNS name</span></span>

<span data-ttu-id="199db-152">Tylko po lewej co zrobić jest ponowne mapowanie sieci active rekord DNS, aby wskazywał usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="199db-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="199db-153">Prawo teraz, nadal wskazuje stare witryny.</span><span class="sxs-lookup"><span data-stu-id="199db-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="199db-154">Skopiuj adres IP aplikacji (tylko rekord)</span><span class="sxs-lookup"><span data-stu-id="199db-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="199db-155">Jeśli są ponowne mapowanie rekord CNAME, Pomiń tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="199db-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="199db-156">Aby ponownie zamapować rekord A, należy zewnętrzny adres IP aplikację usługi aplikacji, który jest wyświetlany w **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="199db-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="199db-157">Zamknij **dodać nazwę hosta** strony, wybierając **X** w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="199db-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="199db-158">W **domen niestandardowych** strony, skopiuj adres IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="199db-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="199db-160">Zaktualizuj rekord DNS</span><span class="sxs-lookup"><span data-stu-id="199db-160">Update the DNS record</span></span>

<span data-ttu-id="199db-161">Ponownie na stronie rekordy DNS dostawcy domeny wybierz rekord DNS, aby ponownie zamapować.</span><span class="sxs-lookup"><span data-stu-id="199db-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="199db-162">Aby uzyskać `contoso.com` przykładowa domena główna, ponownie zamapować rekord A lub CNAME, podobnie jak w przykładach w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="199db-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="199db-163">Przykład nazwy FQDN</span><span class="sxs-lookup"><span data-stu-id="199db-163">FQDN example</span></span> | <span data-ttu-id="199db-164">Typ rekordu</span><span class="sxs-lookup"><span data-stu-id="199db-164">Record type</span></span> | <span data-ttu-id="199db-165">Host</span><span class="sxs-lookup"><span data-stu-id="199db-165">Host</span></span> | <span data-ttu-id="199db-166">Wartość</span><span class="sxs-lookup"><span data-stu-id="199db-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="199db-167">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="199db-167">contoso.com (root)</span></span> | <span data-ttu-id="199db-168">A</span><span class="sxs-lookup"><span data-stu-id="199db-168">A</span></span> | `@` | <span data-ttu-id="199db-169">Adres IP z [skopiuj adres IP aplikacji](#info)</span><span class="sxs-lookup"><span data-stu-id="199db-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="199db-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="199db-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="199db-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="199db-171">CNAME</span></span> | `www` | <span data-ttu-id="199db-172">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="199db-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="199db-173">\*. contoso.com (symbol wieloznaczny)</span><span class="sxs-lookup"><span data-stu-id="199db-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="199db-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="199db-174">CNAME</span></span> | _\*_ | <span data-ttu-id="199db-175">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="199db-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="199db-176">Zapisz ustawienia.</span><span class="sxs-lookup"><span data-stu-id="199db-176">Save your settings.</span></span>

<span data-ttu-id="199db-177">Zapytania DNS powinien rozpocząć rozpoznawania aplikację usługi aplikacji natychmiast po sytuacji propagacji DNS.</span><span class="sxs-lookup"><span data-stu-id="199db-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="199db-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="199db-178">Next steps</span></span>

<span data-ttu-id="199db-179">Dowiedz się, jak powiązać niestandardowego certyfikatu SSL z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="199db-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="199db-180">Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="199db-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
