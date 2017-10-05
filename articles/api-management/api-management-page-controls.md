---
title: "Formanty strony Zarządzanie interfejsami API Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat dostępnych do użycia w szablonach portalu deweloperów w usłudze Azure API Management formantów strony."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="1773c-103">Formanty strony Zarządzanie interfejsami API Azure</span><span class="sxs-lookup"><span data-stu-id="1773c-103">Azure API Management page controls</span></span>
<span data-ttu-id="1773c-104">Azure API Management zapewnia następujące formanty do użycia w dewelopera szablony portalu.</span><span class="sxs-lookup"><span data-stu-id="1773c-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="1773c-105">Aby użyć formantu, należy umieścić w dowolnym miejscu w szablonie portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="1773c-106">Niektóre formanty, takie jak [akcje aplikacji](#app-actions) kontrolować, mieć parametrów, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1773c-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="1773c-107">Wartości parametrów są przekazywane w jako część modelu danych dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="1773c-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="1773c-108">W większości przypadków można po prostu wkleić w podanym przykładzie dla każdego formantu, aby działać poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1773c-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="1773c-109">Aby uzyskać więcej informacji o wartościach parametrów widać sekcji modelu danych do każdego szablonu, w którym można użyć formantu.</span><span class="sxs-lookup"><span data-stu-id="1773c-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="1773c-110">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="1773c-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="1773c-111">Formantów strony szablonu portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="1773c-112">Akcje aplikacji</span><span class="sxs-lookup"><span data-stu-id="1773c-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="1773c-113">Rejestrowanie Basic</span><span class="sxs-lookup"><span data-stu-id="1773c-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="1773c-114">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="1773c-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="1773c-115">dostawców</span><span class="sxs-lookup"><span data-stu-id="1773c-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="1773c-116">formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1773c-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="1773c-117">rejestracji</span><span class="sxs-lookup"><span data-stu-id="1773c-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="1773c-118">przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1773c-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="1773c-119">Anuluj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="1773c-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="1773c-120"><a name="app-actions"></a>Akcje aplikacji</span><span class="sxs-lookup"><span data-stu-id="1773c-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="1773c-121">`app-actions` Kontroli udostępnia interfejs użytkownika do interakcji z aplikacjami na stronie profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="1773c-122">![& #45 aplikacji; kontrolka akcje](./media/api-management-page-controls/APIM-app-actions-control.png "APIM kontroli akcje aplikacji")</span><span class="sxs-lookup"><span data-stu-id="1773c-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-123">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-124">Parameters</span></span>  
  
|<span data-ttu-id="1773c-125">Parametr</span><span class="sxs-lookup"><span data-stu-id="1773c-125">Parameter</span></span>|<span data-ttu-id="1773c-126">Opis</span><span class="sxs-lookup"><span data-stu-id="1773c-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1773c-127">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="1773c-127">appId</span></span>|<span data-ttu-id="1773c-128">Identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1773c-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-129">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-129">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-130">`app-actions` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-131">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="1773c-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="1773c-132"><a name="basic-signin"></a>Rejestrowanie Basic</span><span class="sxs-lookup"><span data-stu-id="1773c-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="1773c-133">`basic-signin` Kontroli udostępnia kontrolkę do zbierania informacji w stronie logowania w portalu dla deweloperów logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1773c-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="1773c-134">![Basic &#45; kontrolka signin](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic Rejestrowanie formantu")</span><span class="sxs-lookup"><span data-stu-id="1773c-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-135">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-136">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-136">Parameters</span></span>  
 <span data-ttu-id="1773c-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-138">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-138">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-139">`basic-signin` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-140">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="1773c-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="1773c-141"><a name="paging-control"></a>Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="1773c-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="1773c-142">`paging-control` Zawiera funkcje stronicowania po developer portal stron, które wyświetlania listy elementów.</span><span class="sxs-lookup"><span data-stu-id="1773c-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="1773c-143">![stronicowanie kontroli](./media/api-management-page-controls/APIM-paging-control.png "APIM formant stronicowania")</span><span class="sxs-lookup"><span data-stu-id="1773c-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-144">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-145">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-145">Parameters</span></span>  
 <span data-ttu-id="1773c-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-147">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-147">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-148">`paging-control` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-149">Lista interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1773c-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="1773c-150">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="1773c-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="1773c-151">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="1773c-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="1773c-152"><a name="providers"></a>dostawców</span><span class="sxs-lookup"><span data-stu-id="1773c-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="1773c-153">`providers` Kontroli udostępnia kontrolkę wyboru dostawcy uwierzytelniania w stronie logowania w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="1773c-154">![Formant dostawców](./media/api-management-page-controls/APIM-providers-control.png "APIM dostawców kontroli")</span><span class="sxs-lookup"><span data-stu-id="1773c-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-155">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-156">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-156">Parameters</span></span>  
 <span data-ttu-id="1773c-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-158">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-158">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-159">`providers` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-160">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="1773c-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="1773c-161"><a name="search-control"></a>formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1773c-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="1773c-162">`search-control` Udostępnia funkcje wyszukiwania na deweloperów na stronach portalu zawierające listę elementów.</span><span class="sxs-lookup"><span data-stu-id="1773c-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="1773c-163">![Wyszukaj kontroli](./media/api-management-page-controls/APIM-search-control.png "APIM formant wyszukiwania")</span><span class="sxs-lookup"><span data-stu-id="1773c-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-164">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-165">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-165">Parameters</span></span>  
 <span data-ttu-id="1773c-166">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-167">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-167">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-168">`search-control` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-169">Lista interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1773c-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="1773c-170">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="1773c-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="1773c-171"><a name="sign-up"></a>rejestracji</span><span class="sxs-lookup"><span data-stu-id="1773c-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="1773c-172">`sign-up` Kontroli udostępnia kontrolkę do zbierania informacji o profilu użytkownika w rejestracji strony w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="1773c-173">![znak &#45; w górę kontrolki](./media/api-management-page-controls/APIM-sign-up-control.png "APIM zapisywania kontrolki")</span><span class="sxs-lookup"><span data-stu-id="1773c-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-174">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-175">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-175">Parameters</span></span>  
 <span data-ttu-id="1773c-176">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-177">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-177">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-178">`sign-up` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-179">Zarejestruj się</span><span class="sxs-lookup"><span data-stu-id="1773c-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="1773c-180"><a name="subscribe-button"></a>przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1773c-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="1773c-181">`subscribe-button` Udostępnia kontrolkę do subskrypcji użytkownika produktu.</span><span class="sxs-lookup"><span data-stu-id="1773c-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="1773c-182">![Subskrypcja &#45; button — formant](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM formantu przycisku subskrypcji")</span><span class="sxs-lookup"><span data-stu-id="1773c-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-183">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-184">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-184">Parameters</span></span>  
 <span data-ttu-id="1773c-185">Brak.</span><span class="sxs-lookup"><span data-stu-id="1773c-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-186">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-186">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-187">`subscribe-button` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-188">Produktu</span><span class="sxs-lookup"><span data-stu-id="1773c-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="1773c-189"><a name="subscription-cancel"></a>Anuluj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="1773c-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="1773c-190">`subscription-cancel` Kontroli udostępnia kontrolkę do anulowania subskrypcji produktu na stronie profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="1773c-191">![Subskrypcja &#45; Anuluj kontroli](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM kontroli Anuluj subskrypcję")</span><span class="sxs-lookup"><span data-stu-id="1773c-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1773c-192">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1773c-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="1773c-193">Parametry</span><span class="sxs-lookup"><span data-stu-id="1773c-193">Parameters</span></span>  
  
|<span data-ttu-id="1773c-194">Parametr</span><span class="sxs-lookup"><span data-stu-id="1773c-194">Parameter</span></span>|<span data-ttu-id="1773c-195">Opis</span><span class="sxs-lookup"><span data-stu-id="1773c-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1773c-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1773c-196">subscriptionId</span></span>|<span data-ttu-id="1773c-197">Identyfikator subskrypcji można anulować.</span><span class="sxs-lookup"><span data-stu-id="1773c-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="1773c-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="1773c-198">cancelUrl</span></span>|<span data-ttu-id="1773c-199">Adres URL anulowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1773c-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1773c-200">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="1773c-200">Developer portal templates</span></span>  
 <span data-ttu-id="1773c-201">`subscription-cancel` Formant może być używany w następujących szablonów portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1773c-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1773c-202">Produktu</span><span class="sxs-lookup"><span data-stu-id="1773c-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="1773c-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1773c-203">Next steps</span></span>
<span data-ttu-id="1773c-204">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1773c-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>