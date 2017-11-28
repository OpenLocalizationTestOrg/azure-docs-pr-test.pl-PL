---
title: "aaaMigrate DNS usługi active nazwa tooAzure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate niestandardowej nazwy domeny DNS, który jest już przypisany tooa live tooAzure witryny usługi aplikacji bez żadnego przestoju."
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
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="d4293-103">Migrowanie active tooAzure nazwę DNS usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4293-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="d4293-104">W tym artykule opisano, jak nazwa toomigrate DNS usługi active zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) bez żadnego przestoju.</span><span class="sxs-lookup"><span data-stu-id="d4293-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="d4293-105">Podczas migracji na żywo lokacji i jej tooApp nazwy domeny DNS usługi, tej nazwy DNS jest już obsługujące ruch na żywo.</span><span class="sxs-lookup"><span data-stu-id="d4293-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="d4293-106">Można uniknąć przestoju w rozpoznawania nazw DNS podczas migracji hello przez powiązanie preemptively hello active DNS nazwy tooyour aplikacji usługi app Service.</span><span class="sxs-lookup"><span data-stu-id="d4293-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="d4293-107">Jeśli nie możesz Obawiamy o przestój w przypadku rozpoznawania nazw DNS, zobacz [mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacje sieci Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d4293-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4293-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4293-108">Prerequisites</span></span>

<span data-ttu-id="d4293-109">toocomplete tym porad:</span><span class="sxs-lookup"><span data-stu-id="d4293-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="d4293-110">[Upewnij się, że aplikację usługi aplikacji nie znajduje się w warstwie bezpłatna](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="d4293-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="d4293-111">Powiąż preemptively hello nazwy domeny</span><span class="sxs-lookup"><span data-stu-id="d4293-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="d4293-112">Gdy powiąże preemptively niestandardową domenę, osiągnąć obu z następujących hello przed wprowadzeniem jakichkolwiek zmian w rekordach DNS:</span><span class="sxs-lookup"><span data-stu-id="d4293-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="d4293-113">Zweryfikuj prawo własności do domeny</span><span class="sxs-lookup"><span data-stu-id="d4293-113">Verify domain ownership</span></span>
- <span data-ttu-id="d4293-114">Włącz hello nazwę domeny aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4293-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="d4293-115">Podczas migracji na koniec nazwę DNS niestandardowych z hello starego lokacji toohello aplikacji usługi app Service, nie będzie bez przestojów w rozpoznawania nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="d4293-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="d4293-116">Utwórz rekord weryfikacji domeny</span><span class="sxs-lookup"><span data-stu-id="d4293-116">Create domain verification record</span></span>

<span data-ttu-id="d4293-117">rekord tooverify własność domeny, Dodaj TXT.</span><span class="sxs-lookup"><span data-stu-id="d4293-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="d4293-118">mapuje Hello rekord TXT z _awverify.&lt; Poddomena >_ too_&lt;nazwa_aplikacji >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="d4293-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="d4293-119">Hello rekord TXT, które są potrzebne, zależy od hello rekord DNS ma toomigrate.</span><span class="sxs-lookup"><span data-stu-id="d4293-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="d4293-120">Przykłady można znaleźć w poniższej tabeli hello (`@` zazwyczaj reprezentuje hello domeny katalogu głównego):</span><span class="sxs-lookup"><span data-stu-id="d4293-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="d4293-121">Przykładowy rekord DNS</span><span class="sxs-lookup"><span data-stu-id="d4293-121">DNS record example</span></span> | <span data-ttu-id="d4293-122">TXT Host</span><span class="sxs-lookup"><span data-stu-id="d4293-122">TXT Host</span></span> | <span data-ttu-id="d4293-123">Wartość TXT</span><span class="sxs-lookup"><span data-stu-id="d4293-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="d4293-124">@ (root)</span><span class="sxs-lookup"><span data-stu-id="d4293-124">@ (root)</span></span> | <span data-ttu-id="d4293-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="d4293-125">_awverify_</span></span> | <span data-ttu-id="d4293-126">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d4293-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d4293-127">WWW (sub)</span><span class="sxs-lookup"><span data-stu-id="d4293-127">www (sub)</span></span> | <span data-ttu-id="d4293-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="d4293-128">_awverify.www_</span></span> | <span data-ttu-id="d4293-129">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d4293-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d4293-130">\*(symbol wieloznaczny)</span><span class="sxs-lookup"><span data-stu-id="d4293-130">\* (wildcard)</span></span> | <span data-ttu-id="d4293-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="d4293-131">_awverify.\*_</span></span> | <span data-ttu-id="d4293-132">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d4293-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="d4293-133">Na stronie rekordy DNS należy pamiętać, typ rekordu hello hello ma toomigrate nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="d4293-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="d4293-134">Usługa aplikacji obsługuje mapowania z CNAME i.</span><span class="sxs-lookup"><span data-stu-id="d4293-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="d4293-135">Włącz hello domeny aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4293-135">Enable hello domain for your app</span></span>

<span data-ttu-id="d4293-136">W hello [portalu Azure](https://portal.azure.com), w lewym obszarze nawigacji strony aplikacji hello Witaj, wybierz **domen niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="d4293-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="d4293-138">W hello **domen niestandardowych** strona, wybierz hello ** + ** ikona dalej zbyt**dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="d4293-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="d4293-140">Typ hello pełną nazwę domeny dodaje rekord TXT hello, takich jak `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d4293-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="d4293-141">Dla domeny symbolu wieloznacznego (takich jak \*. contoso.com), można użyć dowolnej nazwy DNS, odpowiadający hello domenie symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="d4293-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="d4293-142">Wybierz **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="d4293-142">Select **Validate**.</span></span>

<span data-ttu-id="d4293-143">Witaj **dodać nazwę hosta** przycisk jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="d4293-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="d4293-144">Upewnij się, że **typu rekordu Hostname** ustawiono typ rekordu DNS toohello ma toomigrate.</span><span class="sxs-lookup"><span data-stu-id="d4293-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="d4293-145">Wybierz **dodać nazwę hosta**.</span><span class="sxs-lookup"><span data-stu-id="d4293-145">Select **Add hostname**.</span></span>

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="d4293-147">Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="d4293-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="d4293-148">Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="d4293-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="d4293-150">Niestandardowe nazwę DNS jest teraz włączone w aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="d4293-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="d4293-151">Ponowne mapowanie hello active nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="d4293-151">Remap hello active DNS name</span></span>

<span data-ttu-id="d4293-152">Witaj tylko element toodo po lewej stronie jest ponowne mapowanie użytkownika active tooApp toopoint rekordów DNS usługi.</span><span class="sxs-lookup"><span data-stu-id="d4293-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="d4293-153">Prawo teraz, nadal wskazuje tooyour starej lokacji.</span><span class="sxs-lookup"><span data-stu-id="d4293-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="d4293-154">Skopiuj adres IP aplikacji hello (rekord tylko)</span><span class="sxs-lookup"><span data-stu-id="d4293-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="d4293-155">Jeśli są ponowne mapowanie rekord CNAME, Pomiń tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="d4293-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="d4293-156">rekord A tooremap należy zewnętrznego adresu IP aplikacji usługi aplikacji hello, który jest wyświetlany w hello **domen niestandardowych** strony.</span><span class="sxs-lookup"><span data-stu-id="d4293-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="d4293-157">Zamknij hello **dodać nazwę hosta** strony, wybierając **X** w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="d4293-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="d4293-158">W hello **domen niestandardowych** pozycję Kopiuj aplikacji hello adres IP.</span><span class="sxs-lookup"><span data-stu-id="d4293-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="d4293-160">Zaktualizuj rekord DNS hello</span><span class="sxs-lookup"><span data-stu-id="d4293-160">Update hello DNS record</span></span>

<span data-ttu-id="d4293-161">Ponownie hello stronie rekordy DNS dostawcy domeny, wybierz tooremap rekordów DNS hello.</span><span class="sxs-lookup"><span data-stu-id="d4293-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="d4293-162">Dla hello `contoso.com` przykładowa domena główna, ponownie zamapować rekord A lub CNAME hello jak przykłady hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="d4293-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="d4293-163">Przykład nazwy FQDN</span><span class="sxs-lookup"><span data-stu-id="d4293-163">FQDN example</span></span> | <span data-ttu-id="d4293-164">Typ rekordu</span><span class="sxs-lookup"><span data-stu-id="d4293-164">Record type</span></span> | <span data-ttu-id="d4293-165">Host</span><span class="sxs-lookup"><span data-stu-id="d4293-165">Host</span></span> | <span data-ttu-id="d4293-166">Wartość</span><span class="sxs-lookup"><span data-stu-id="d4293-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="d4293-167">contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="d4293-167">contoso.com (root)</span></span> | <span data-ttu-id="d4293-168">A</span><span class="sxs-lookup"><span data-stu-id="d4293-168">A</span></span> | `@` | <span data-ttu-id="d4293-169">Adres IP z [aplikacji hello kopiowania adresu IP](#info)</span><span class="sxs-lookup"><span data-stu-id="d4293-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="d4293-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="d4293-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="d4293-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4293-171">CNAME</span></span> | `www` | <span data-ttu-id="d4293-172">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d4293-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d4293-173">\*. contoso.com (symbol wieloznaczny)</span><span class="sxs-lookup"><span data-stu-id="d4293-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="d4293-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4293-174">CNAME</span></span> | _\*_ | <span data-ttu-id="d4293-175">_&lt;Nazwa aplikacji >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d4293-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="d4293-176">Zapisz ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d4293-176">Save your settings.</span></span>

<span data-ttu-id="d4293-177">Zapytania DNS należy zacząć rozwiązywanie tooyour aplikacji usługi app Service, natychmiast po sytuacji propagacji DNS.</span><span class="sxs-lookup"><span data-stu-id="d4293-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4293-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4293-178">Next steps</span></span>

<span data-ttu-id="d4293-179">Dowiedz się, jak toobind SSL niestandardowych certyfikatów tooApp usługi.</span><span class="sxs-lookup"><span data-stu-id="d4293-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4293-180">Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d4293-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
